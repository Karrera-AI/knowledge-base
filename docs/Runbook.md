#Karrera Infra Runbook

*Set IAM permissions for default compute service account.

1 Deploy Postgres

2 Create Secret Manager

3 Deploy Solid server in VM

4 Deploy CSS server in VM

	4.1 Install Docker: (https://docs.docker.com/engine/install/debian/)

		4.1.1 Add Docker's official GPG key:
		
			sudo apt update
			sudo apt install ca-certificates curl
			sudo install -m 0755 -d /etc/apt/keyrings
			sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
			sudo chmod a+r /etc/apt/keyrings/docker.asc

		4.1.2 Add the repository to Apt sources:
		
			sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
			Types: deb
			URIs: https://download.docker.com/linux/debian
			Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
			Components: stable
			Signed-By: /etc/apt/keyrings/docker.asc
			EOF

		4.1.3 Update and Install Docker
		
			sudo apt update
			sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

	4.2 Install CSS: (https://communitysolidserver.github.io/CommunitySolidServer/latest/usage/starting-server/)

		4.2.1 Clone the repo to get access to the configs
		
			git clone https://github.com/CommunitySolidServer/CommunitySolidServer.git
			cd CommunitySolidServer
			
		4.2.2 Configure CSS Server

			Copy Karrera logo to CommunitySolidServer/templates/images
			Create json CSS config file (karrera.json)
		
		4.2.3 Build the image
		
			docker build -t css-server:1.0.3 .	

	4.3 Install Certbot:

		sudo apt install certbot

	4.4 Configure Firewall
	
		Open ports HTTP (80) and HTTPS (443)

	4.5 Install Certificate: (https://certbot.eff.org/instructions?ws=other&os=snap)

		sudo certbot certonly --standalone

	4.6 Configure cron to renew certificates every Sunday 3:00am

		4.6.1 Create script (/etc/letsencrypt/archive/css-dev.karrera.ai/update.sh) to copy latest version of certificates to certificates used by docker

			#!/bin/bash

			# Directory containing the files
			DIR="/etc/letsencrypt/archive/css-dev.karrera.ai"

			# Find the latest fullchain file by sorting numerically
			LATEST_FULLCHAIN=$(ls "$DIR"/fullchain*.pem 2>/dev/null | \
					 sed -E 's/.*fullchain([0-9]+)\.pem/\1 \0/' | \
					 sort -n | \
					 tail -1 | \
					 cut -d' ' -f2)

			# Check if a file was found
			if [ -n "$LATEST_FULLCHAIN" ]; then
				cp "$LATEST_FULLCHAIN" "$DIR/fullchain.pem"
				echo "Copied $LATEST_FULLCHAIN to $DIR/fullchain.pem"
			else
				echo "No fullchain*.pem files found in $DIR"
			fi

			# Find the latest privkey file by sorting numerically
			LATEST_PRIVKEY=$(ls "$DIR"/privkey*.pem 2>/dev/null | \
					 sed -E 's/.*privkey([0-9]+)\.pem/\1 \0/' | \
					 sort -n | \
					 tail -1 | \
					 cut -d' ' -f2)

			# Check if a file was found
			if [ -n "$LATEST_PRIVKEY" ]; then
				cp "$LATEST_PRIVKEY" "$DIR/privkey.pem"
				echo "Copied $LATEST_PRIVKEY to $DIR/privkey.pem"
			else
				echo "No privkey*.pem files found in $DIR"
			fi
			
		4.6.2 Run update file to create certificates used by Docker
		
			sudo /etc/letsencrypt/archive/css-dev.karrera.ai/update.sh
		
		4.6.3 Add command line to root crontab
		
			0 3 * * 0 docker stop css-server && certbot renew && /etc/letsencrypt/archive/css-dev.karrera.ai/update.sh && docker start css-server

	4.7 Run the image, serving your `/PodData` directory on `https://css.karrera.ai`
	
			docker run -d -p 443:3000 \
			--name css-server \
			--restart always \
			-v /PodData:/data \
			-v /etc/letsencrypt/archive/css.karrera.ai:/certificates \
			-e CSS_ROOT_FILE_PATH=/data \
			-e CSS_CONFIG=config/karrera.json \
			-e CSS_BASE_URL=https://css.karrera.ai/ \
			-e CSS_HTTPS_KEY=/certificates/privkey.pem \
			-e CSS_HTTPS_CERT=/certificates/fullchain.pem \
			css-server:1.0.3

5 Set Cloudrun CD for all micro services
	
  5.1 Deploy Karrera-backend
		
    5.1.1 Update secret manager API call
	
  5.2 Deploy Karrera-web
		
    5.2.1 Inject process.env.GCP_PROJECT_ID in Cloudrun config
		
    5.2.2 Update secret manager API call(DB connection)
		
    5.2.3 Update Solid connection(providerOptions)
		
    5.2.4 Domain mapping(app.karrera.ai)
	
  5.3 Deploy Queue publisher
	
  5.4 Deploy WorkDNA
		
    5.4.1 Deploy ChromaDB(Insert initial collections)
		
    5.4.2 Update ChromaDB connection
	
  5.5 Deploy Biography API

6 Deploy Artifact Consumer in Worker Pool

7 Deploy Chat Consumer in Worker Pool

8 Deploy Scrape Consumer in Worker Pool

9 Deploy CV Consumer in Worker Pool
