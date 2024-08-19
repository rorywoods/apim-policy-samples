## Use of Google Service Account from APIM
Making a service to service call to a GCP endpoint requires use of a service account. GCP CLI and SDKs care for this authentication flow. Services running in GCP can use workload identity federation to carry a service account identity.

When the need arise to call a GCP service endpoint from Azure API Management we must care for the OAuth flow manually. As of August 2024, Credential Manager does not support the jwt-bearer token flow that is required by GCP. Nor does it support a client credential flow with a certificate.

This policy demonstrates using policy expressions to concatenate a jwt, sign it, make a request for an access token and cache the token for further use until the token expires.

### Configuration
1. Create a Service Account in GCP IAM with the proper permissions on the target resource
1. Add a P12 key to the service account
1. Change the extension of the resulting file that is downloaded from p12 to pfx
1. Upload the pfx to the Certificates store of the APIM instance
1. Add the thumbprint of the certificate to a named value with the name `google-service-account-certificate-thumbprint`
1. Add the email address of the  GCP service account to a named value with the key `google-service-account-email-address`
1. Add the scope(s) to include in the jwt to a named value with the name `google-service-account-scopes`


References:  
https://stackoverflow.com/questions/68721061/how-can-i-sign-a-jwt-with-rsa-sha256-in-an-azure-api-management-policy-expressio  

https://developers.google.com/identity/protocols/oauth2/service-account#httprest