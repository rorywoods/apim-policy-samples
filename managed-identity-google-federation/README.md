## Use orkload Identity Federation to avoid a service account certificate
Making a service to service call to a GCP endpoint requires use of a service account. Instead of requiring a service account certificate, exchange a token from Entra ID for a Google Identity access token. 

This policy demonstrates using policy expressions to conduct the exchange.

### Configuration
1. Enable managed identity on the APIM instance
1. Create an app registration to represent the GCP resource in the local Entra tenant
1. Create a project, IAM Workload Identity pool and identity provider mapping in Google
1. Restrict the Workload Identity Federation allowed audience to the object ID of your application
1. Map the google.subject to the assertion.sub in the Workload Identity Federation
1. Optionally, you could also restrict this mapping to a subject to only allow APIM to request a token
1. Assign permissions to the Workload Pool IAM principal to the GCP target resource
1. Add an APIM named variable with name `app-registration-appid-uri` and value of the Application ID URI of the app registration
1. Add an APIM named variable with name `gcp-project-name` and value of the GCP project name
1. Add an APIM named variable with name `gcp-pool-id` and value of the GCP pool ID
1. Add an APIM named variable with name `gcp-provider-id` and value of the GCP identity provider ID