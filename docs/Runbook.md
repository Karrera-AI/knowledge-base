#Karrera Infra Runbook

*Set IAM permissions for default compute service account.

1 Deploy Postgres

	1.1 Install Postgres via docker in VM(https://hub.docker.com/_/postgres)

	1.2 Create Postgres instance in GCP CloudSQL(alternative)

2 Create Secret Manager

	2.1 Activate GCP Secret Manager.

	2.2 Create keys for all needed backend services.

		2.2.1 Backend-Postgres

		2.2.2 CloudAMQP

		2.2.3 Gemini-API

		2.2.4 SERPER-API

		2.2.5 Solid

		2.2.6 X-API-Key

3 Deploy Solid server in VM

	3.1 Install Docker: (https://docs.docker.com/engine/install/debian/)

		3.1.1 Add Docker's official GPG key:
		
			sudo apt update
			sudo apt install ca-certificates curl
			sudo install -m 0755 -d /etc/apt/keyrings
			sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
			sudo chmod a+r /etc/apt/keyrings/docker.asc

		3.1.2 Add the repository to Apt sources:
		
			sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
			Types: deb
			URIs: https://download.docker.com/linux/debian
			Suites: $(. /etc/os-release && echo "$VERSION_CODENAME")
			Components: stable
			Signed-By: /etc/apt/keyrings/docker.asc
			EOF

		3.1.3 Update and Install Docker
		
			sudo apt update
			sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

	3.2 Pull and run Solid server image

		3.2.1 Authenticate Docker to use Google Container Registry
		
			```bash
			gcloud auth configure-docker
			```

		3.2.2 Setup docker-compose.yml file (/opt/solid-crud/docker-compose.yml)
		
			```yaml
				services:
				solid-crud:
					image: us-central1-docker.pkg.dev/nossaia/solid-crud/solid-crud:alpha
					container_name: solid-crud
					restart: unless-stopped
					ports:
						- "80:80"
						- "443:443"
					volumes:
						- /etc/letsencrypt:/etc/letsencrypt
			```

		3.2.3 Set enviroment variables in docker-compose.override.yml (/opt/solid-crud/docker-compose.override.yml)
		
			```yaml
					environment:
						SECRET_VERSION: "projects/79811639884/secrets/Solid-Secrets/versions/1"
						DOMAIN_NAME: "solid.karrera.ai"
						TAXONOMY_SERVICE_HOST: "https://karrera-backend-79811639884.us-east1.run.app"
						ONTOLOGY_SERVICE_HOST: "https://workdna-ai-79811639884.us-east1.run.app"
						BIO_SERVICE_HOST: "https://biography-api-79811639884.us-east1.run.app"
						QUEUE_PUBLISHER_SERVICE_HOST: "https://queuepublisher-79811639884.us-east1.run.app"
			```


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
			-e NODE_OPTIONS="--max-old-space-size=4096" \
			-e CSS_ROOT_FILE_PATH=/data \
			-e CSS_CONFIG=config/karrera.json \
			-e CSS_BASE_URL=https://css.karrera.ai/ \
			-e CSS_HTTPS_KEY=/certificates/privkey.pem \
			-e CSS_HTTPS_CERT=/certificates/fullchain.pem \
			css-server:1.0.3
			
	4.8 Create karreraai WebID

	4.9 Configure Pod Data Backup

		4.9.1 Create Backup data folder

			mkdir /Backup-PodData

		4.9.2 Create Backup Bucket

		4.9.3 Allow Default GCP Service account to be Storage Admin

		4.9.4 Create script to Backup Pod Data and copy it to backup Bucket (/Backup-PodData/backup-poddata.sh)

			#!/bin/bash

			# Source and destination directories
			SRC="/PodData"
			DEST="/Backup-PodData"
			
			# Create destination directory if it doesn't exist
			mkdir -p "$DEST"
			
			# Generate date-based filename
			DATE=$(date +%Y-%m-%d)
			FILENAME="PodData-$DATE.tar.gz"
			
			# Create the tar.gz archive
			tar -czf "$DEST/$FILENAME" -C "$SRC" .
			
			# Copy file to Backup Bucket
			gsutil cp $DEST/$FILENAME gs://karrera-backup-bucket/CSS-Backup
			
			# Optional: print a message (useful for logs)
			echo "Backup created: $DEST/$FILENAME"

		4.9.5 Allow script to be executable

			chmod +x /Backup-PodData/backup-poddata.sh

		4.9.6 Insert command in root crontab to execute backup every day at 4:00AM

			sudo su
			cronta -e
			Insert line below:
				0 4 * * * docker stop css-server && /Backup-PodData/backup-poddata.sh && docker start css-server
		

5 Set Cloudrun CD for all micro services
	
  5.1 Deploy Karrera-backend(Replit-backend and Postgres-backend)
		
    5.1.1 Update secret manager API call
	
  5.2 Deploy Karrera-web
			
	5.2.1 Build Development
	
	Build in development mode
	npm run build:dev
	
	The build will:
	- Compile TypeScript
	- Process React
	- Minify code
	- Generate files in dist/public/
	
	5.2.2 Production Build
	
	Build in production mode
	npm run build:prod
	
	The build will:
	- Compile with production optimizations
	- Minify and optimize code
	- Generate optimized files in dist/public/
	
  5.3 Deploy Queue publisher

    5.3.1 Queue publisher deployment (using GCP Console)

		5.3.1.1 Navigate to Cloud Run
		- Go to Cloud Run and click Services.
		- Then click Deploy Container in top right.
		
		5.3.1.2 Continuous Deployment Setup
	    - Select Continuously deploy new revisions from a source repository.
    	- Click Set Up Cloud Build.
    	- Repository Provider: Select GitHub.
    	- Repository: Select QueuePublisher repo.
    	- Build Configuration: Choose Dockerfile.
		- Build Branch: Select $dev or $prod (accoridng to which version you are deploying).
		
		5.3.1.3 Service Settings
    	- Region: Select us-east1 for prod, us-central1 for dev.
    	- Authentication: Select Allow public access.
		- Billing: Select Request-based.
		- Scaling: Select Auto scaling, and set min = 1, max = 1. These values can change in the future.
		- Ingress: In theory, can be used only internally, but we can select All as well.
		
		5.3.1.4 Container Settings
	    - Go to Container, Networking, Security.
		- Port: 8000 (make sure port 8000 is exposed).
		- Select Containers

			5.3.1.4.1 Settings
			- Go to Settings.
			- Resources: 512MiB (Memory) and 1 CPU - for now, values can change as we go.
			- Revision Scaling: min = 1, max = 1.
			- Other settings leave as default values.

			5.3.1.4.2 Variables & Secrets
			- Go to Variables & Secrets.
			- Add the following environment variables (names: values):
				- VERSION_NAME= <Version of CloudAMQP server password google secrets>
				- SERVER_NAME= <Cloud AMQP server name>
				- VIRTUAL_HOST= <Cloud AMQP virtual host name>
				- HOST= <Cloud AMQP host address>
				- SERVER_PORT= <Cloud AMQP server port>
				- APP_VERSION= <Queue Publisher version - e.g. Dev>
				- APP_HOST= <Queue publisher google host server - e.g. CloudRun-us-east1>
				- SCRAPE_QUEUE=Scrape_web
				- SCRAPE_DLQ=scrape_web_dlq
				- ARTIFACT_QUEUE=Artifact_reader
				- ARTIFACT_DLQ=artifact_reader_dlq
				- CV_QUEUE=CV_reader
				- CV_DLQ=CV_reader_dlq
				- CHAT_QUEUE=Chat_reader
				- CHAT_DLQ=chat_reader_dlq
				- PI_QUEUE=PI_reader
				- PI_DLQ=PI_reader_dlq
				- MEMORY_QUEUE=Memory_creator
				- MEMORY_DLQ=memory_creator_dlq
				- GENERIC_ARTIFACT_QUEUE=Generic_artifact_reader
				- GENERIC_ARTIFACT_DLQ=generic_artifact_dlq
				
			5.3.1.5 Create
			- Click Create. Cloud Build will now trigger a deployment on every git push to the dev branch.
			- After this, look at the logs to see if everything is okay during the build.
			- This build will deploy the the QueuePublisher service into the app.
	
  5.4 Deploy WorkDNA
		
    5.4.1 Deploy ChromaDB on VM (Insert initial collections)

		5.4.1.1 Open the VM (in our case, css-server)

		5.4.1.2 Open port 8000

		5.4.1.3  Pull the image from docker
		docker pull chromadb/chroma:latest

		5.4.1.4 Run the image inside the VM
		docker run -d -v ./chroma-data:/data -p 8000:8000 --restart always chromadb/chroma 
		- PS: Give a name if you want to using --name name-of-server

		5.4.1.5 Update ChromaDB collections
		To do that, we need to have embedded all the values (capabilities, workdna sheets for paths, paths descriptions, etc).
		So, check the workdna-ai.md and sbert-chroma.md to know how to create collections and add the embeddings

		
    5.4.2 Create Bucket and Upload the Embedding Model

		5.4.2.1 Install Sentence Trasnformers.
		```bash
		pip install -U sentence-transformers
		```
		
		5.4.2.2 Download the embedding model to local machine
		We are using currently Qwen/Qwen3-Embedding-0.6B, so if we changed it, we would have to change the name and download the new one.
		```python
		from sentence_transformers import SentenceTransformer

		name_of_model = "Qwen/Qwen3-Embedding-0.6B"

		model = SentenceTransformer(name_of_model)
		model.save(name_of_model) ## This will save the whole model config to the local machine, under the folder with the name of the model
		```

		5.4.2.3 Navigate to Cloud Storage
		In the search bar at the top, type Buckets and select Cloud Storage > Buckets.
		
		5.4.2.4 Create and configure the Bucket
		- Click the + CREATE button at the top of the page.
		- Name your bucket (e.g., embedding-model) - names are public, so avoid sensitive names.
		- Location: Set location to Multi-Region (us) or to the specific Region (e.g., `us-central1` for prod).
		- Storage class: Select Standard.
		- Access control: Select Uniform.
		- Public Access Prevention: Ensure "Enforce public access prevention on this bucket" is checked.
		- Create and Finalize: Click CREATE. If prompted with a "Public access will be prevented" warning, click CONFIRM.

		5.4.2.5 Upload the folder to the bucket
		- After the bucket is created, click the name of the bucket.
		- In the Objects tab, Click Upload > Upload folder.
		- Select the folder create at step 5.4.2.2 in the dialog that appears, then click Open.
		OR, if preferred, one can use the gcloud storage cp command in command line:
		```bash
		gcloud storage cp FOLDER_PATH gs://DESTINATION_BUCKET_NAME
		```

	5.4.3 WorkDNA-AI deployment (using GCP Console)

		5.4.3.1 Navigate to Cloud Run
		- Go to Cloud Run and click Services.
		- Then click Deploy Container in top right.
		
		5.4.3.2 Continuous Deployment Setup
	    - Select Continuously deploy new revisions from a source repository.
    	- Click Set Up Cloud Build.
    	- Repository Provider: Select GitHub.
    	- Repository: Select WorkDNA-AI repo.
    	- Build Configuration: Choose Dockerfile.
		- Build Branch: Select $dev or $prod (accoridng to which version you are deploying).
		
		5.4.3.3: Service Settings
    	- Region: Select us-east1 for prod, us-central1 for dev.
    	- Authentication: Select Allow public access.
		- Billing: Select Request-based.
		- Scaling: Select Auto scaling, and set min = 1, max = 1.
		- Ingress: In theory, WorKDNA can be used only internally, but we can select All as well.
		
		5.4.3.4: Container Settings
	    - Go to Container, Networking, Security.
		- Port: 5005 (make sure port 5005 is exposed).
		- Select Containers

			5.4.3.4.1: Settings
			- Go to Settings.
			- Resources: 4 GiB (Memory) and 1 CPU - for now, values can change as we go.
			- Add Health Check:
				- Type: Select Startup Check.
				- Probe type: Select TCP.
				- Port: 5005.
				- Every 240s, default settings.
			- Revision Scaling: min = 1, max = 1.
			- Other settings leave as default values.

			5.4.3.4.2: Volumes (to mount the bucket to the container)
			- Go to Volumes.
			- Select Add Mount Volume.
			- Select Cloud Storage Bucket.
			- Select the storage volume from 5.4.2.
			- Specify the path where you want to mount the volume (i.e. qwen_models).
			- In Mount options, Enable implicit directions ON. 
			- Click Done.

			5.4.3.4.3: Variables & Secrets
			- Go to Variables & Secrets.
			- Add the following environment variables (names: values):
				- GEMINI_SECRET: <reference the url of the secret>
				- POSTGRES_PASSWORD_SECRET: <reference the url of the secret>
				- CHROMA_DB_HOST: <IP of the VM hosting the chroma>	
				- CHROMA_DB_PORT: <chromaDB port>
				- APP_VERSION: dev / prod
				- VERSION: <version of the service itself, like v1.0, v1.1>
				- APP_COMPONENT: work-dna-ontology-service	
				- POSTGRES_DB_NAME: <name of the Postgres DB>
				- GCS_MOUNT_ROOT: <path of the mounted bucket as we mentioned in 5.4.3.4.2>
			
			For now, we are referencing the secrets by pasting the url. We can switch it later to mounting the secret as well (TODO).

			5.4.3.5 Create
			- Click Create. Cloud Build will now trigger a deployment on every git push to the dev branch.
			- After this, look at the logs to see if everything is okay during the build.
			- This build will deploy the the WorkDNA-AI service and all associated services into the app.
	
  5.5 Deploy Biography API

  	5.5.1 Biography API deployment (using GCP Console)

		5.5.1.1 Navigate to Cloud Run
		- Go to Cloud Run and click Services.
		- Then click Deploy Container in top right.
		
		5.5.1.2 Continuous Deployment Setup
	    - Select Continuously deploy new revisions from a source repository.
    	- Click Set Up Cloud Build.
    	- Repository Provider: Select GitHub.
    	- Repository: Select Biography_API repo.
    	- Build Configuration: Choose Dockerfile.
		- Build Branch: Select $dev or $prod (accoridng to which version you are deploying).
		
		5.5.1.3 Service Settings
    	- Region: Select us-east1 for prod, us-central1 for dev.
    	- Authentication: Select Allow public access.
		- Billing: Select Request-based.
		- Scaling: Select Auto scaling, and set min = 1, max = 1. These values can change in the future.
		- Ingress: In theory, can be used only internally, but we can select All as well.
		
		5.5.1.4 Container Settings
	    - Go to Container, Networking, Security.
		- Port: 8000 (make sure port 8000 is exposed).
		- Select Containers

			5.5.1.4.1 Settings
			- Go to Settings.
			- Resources: 512MiB (Memory) and 1 CPU - for now, values can change as we go.
			- Revision Scaling: min = 1, max = 1.
			- Other settings leave as default values.

			5.5.1.4.2 Variables & Secrets
			- Go to Variables & Secrets.
			- Add the following environment variables (names: values):
				- GEMINI_API_KEY_VERSION_NAME= <Version of Gemini-Api-Key password google secrets>
				- GEMINI_MODEL_ID= <Gemini model used - e.g. gemini-2.5-flash>
				- SERVER_PORT= <Cloud AMQP server port>
				- APP_VERSION= <Biography_API version - e.g. Dev>
				- APP_HOST= <Queue publisher google host server - e.g. CloudRun-us-east1>
				
			5.5.1.5 Create
			- Click Create. Cloud Build will now trigger a deployment on every git push to the dev branch.
			- After this, look at the logs to see if everything is okay during the build.
			- This build will deploy the the Biography_API service into the app.

6 Set Cloudrun Worker Pool Services

    6.1 Deploy artifact-scrape-consumer in Worker Pool

		6.1.1 artifact-scrape-consumer deployment (using GCP Console)

			6.1.1.1 Navigate to Cloud Run
			- Go to Cloud Run and click Worker Pools.
			- Then click Deploy Container in top right.
			
			6.1.1.2 Worker Pool Setup
	    	- Select the container image URL, choosing the latest version from karrera-artifact-scrape-consumer inside karrera-consumers.
			
			6.1.1.3 Service Settings
	    	- Region: Select us-east1 for prod, us-central1 for dev.
			- Instances: Select 1 as the number of instances. The number may be changed in the future.
			
			6.1.1.4 Container Settings
		    - Go to Container, Networking, Security.
			- Select Containers
	
				6.1.1.4.1 Settings
				- Go to Settings.
				- Resources: 2Gib (Memory) and 1 CPU - for now, values can change as we go.
				- Other settings leave as default values.
	
				6.1.1.4.2 Variables & Secrets
				- Go to Variables & Secrets.
				- Add the following environment variables (names: values):
					- SERVER_VERSION_NAME= <Version of CloudAMQP server password google secrets>
					- SERVER_NAME= <Cloud AMQP server name>
					- VIRTUAL_HOST= <Cloud AMQP virtual host name>
					- HOST= <Cloud AMQP host address>
					- SERVER_PORT= <Cloud AMQP server port>
					- APP_VERSION= <artifact-scrape-consumer version - e.g. Dev>>
					- APP_HOST= <Queue publisher google host server - e.g. CloudRun-Worker-pools-us-central1>
					- ARTIFACT_QUEUE=Artifact_reader_DEV
					- ARTIFACT_DLQ=artifact_reader_dlq_DEV
					- POD_URL= <URL of the PODs, for dev or prod>
					- X_API_KEY_VERSION_NAME= <Version of X-API-Key password google secrets>
					- GEMINI_API_KEY_VERSION_NAME= <Version of Gemini-Api-Key password google secrets>
					- GEMINI_MODEL_ID= <Gemini model used - e.g. gemini-2.5-flash>
					- DNA_API_URL= <WorkDNA CloudRun API URL>
					- DNA_COMPETENCIES_API_ENDPOINT=/ontology/match_capabilities
					- DNA_OCCUPATIONS_API_ENDPOINT=/ontology/match_paths
					
				6.1.1.5 Create
				- Click Create. The Worker Pool service will be created.
				- After this, look at the logs to see if everything is okay during the build.
				- This build will deploy the the Artifact-Scrape-Consumer service into the app.
	

	6.2 Deploy chat-Consumer in Worker Pool
	
	6.3 Deploy scrape-consumer in Worker Pool
	
	6.4 Deploy CV-Consumer in Worker Pool
