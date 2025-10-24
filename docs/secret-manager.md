# Secret Manager user guide

## Python

```py title="secret_manager.py" linenums="1"
# Import the Secret Manager client library.
from google.cloud import secretmanager

# Name of the secret version.
version_name = "SECRET_VERSION_NAME"

# Create the Secret Manager client.
client = secretmanager.SecretManagerServiceClient()

response = client.access_secret_version(request={"name": version_name})
payload = response.payload.data.decode("UTF-8")

return payload
```


## Javascript


```js title="secret_manager.js" linenums="1" hl_lines="2-4"
// Import the Secret Manager client and instantiate it:
const {SecretManagerServiceClient} = require('@google-cloud/secret-manager');
const client = new SecretManagerServiceClient();

const verionName = "VERSION_NAME"

async function AccessSecret() {
    // Access the secret.
  const [accessResponse] = await client.accessSecretVersion({
    name: verionName,
  });

  const responsePayload = accessResponse.payload.data.toString('utf8');
  console.info(`Payload: ${responsePayload}`);
}

AccessSecret();
```


## Go

```go title="secret_manager.js" linenums="1" hl_lines="2-4"
package main

import (
	"context"
	"fmt"
	"log"

	secretmanager "cloud.google.com/go/secretmanager/apiv1"
	"cloud.google.com/go/secretmanager/apiv1/secretmanagerpb"
)

func main() {
    // Create the client.
	ctx := context.Background()
	client, err := secretmanager.NewClient(ctx)
	if err != nil {
		log.Fatalf("failed to setup client: %v", err)
	}
	defer client.Close()

    // Build the request.
	accessRequest := &secretmanagerpb.AccessSecretVersionRequest{
		Name: version.Name,
	}

	// Call the API.
	result, err := client.AccessSecretVersion(ctx, accessRequest)
	if err != nil {
		log.Fatalf("failed to access secret version: %v", err)
	}

    log.Printf("Plaintext: %s", result.Payload.Data)
}

```