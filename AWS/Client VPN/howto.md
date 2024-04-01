# AWS Client VPN using SSO login
### Requirements:
* Have SSO setup and working
* Have at least 1 user in IAM Identity Center

## Step 1:
Create application from IAM Identity Center ( not IAM )
* Goto **Applications**
* Add application
* Select "I have an application I want to set up"
* Select "SAML 2.0"
* Click "Next"
* Add name and description
* Download the metadata file
* Click Submit

## Step 2:
Create identity provider
* Goto IAM
* Click on "Identity providers"
* Add provider
* Select SAML
* Give a name
* Choose the metadata file downloaded from Step 1
* Click "Add provider"

## Step 3: 
Create selfsigned SHA-256 certificate 
* After created upload certificate to AWS Certificate manager

## Step 4:
Configure Client VPN
* Goto VPC
* On the left menu, click on Client VPN Endpoints
* Click on Create client vpn endpoint
* Fill out the name, description and CIDR
* Under "Authentication information"
  * Select the uploaded certificate on Step 3
  * Select "Use user-based authentication"
  * Select "Federated authentication"
  * Under "SAML provider ARN" select the provider created on Step 2 
  * Leave "Self-service SAML" empty
  * Select VPC for private network and security group for the VPN
  * Click "Create client VPN endpoint"

## Step 5:
Download configuration
* After endpoint is created, select the enpoint and click on "Download client configuration"

### Step 6:
Download client from: https://aws.amazon.com/vpn/client-vpn-download/

### Step 7:
Add profile to vpn client, click connect and follow SSO instructions.

Optionally can create limited client access to subnets using group or user id and subnet CIDR
