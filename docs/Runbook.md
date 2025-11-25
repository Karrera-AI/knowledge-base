#Karrera Infra Runbook

*Set IAM permissions for default compute service account.

1 Deploy Postgres

2 Create Secret Manager

3 Deploy Solid server in VM

4 Deploy CSS server in VM

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
