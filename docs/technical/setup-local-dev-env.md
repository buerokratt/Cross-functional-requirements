# Setting up local development environment

Creating a service principle
1. Sign in to your Azure Account through the Azure portal
2. Select `Azure Active Directory`
3. Select `App registrations`
4. Select `New registration`
5. Enter a suitable app name
6. Click `Register`

Creating a client secret for the service principle
1. In AAD select your service principle
2. On the left hand side select `Certificates and secrets`
3. Click `+ New client secret`
4. Copy and save the `value` - this will be need to authenticate

Giving permission to your service principle
1. On the Subscription page go to `Access Control (IAM)`
2. Select `Add role assignment`
3. Select `Contributor`
4. Select `select members` and search for the name of your recently created service principle
5. Select `Review + Assign`

Updating local credentials.tfvars file
1. Copy and rename the `credentials-template.tfvars` file and name it `credentials.tfvars`
2. Fill in the values using the following information from your previously created service principle
    - `client_id` = Object ID of the service principle
    - `client_secret` = The secret created for the service principle
    - `tenent_id` = Directory (tenent) ID of the service principle
    - `subscription_id` = Subscription ID of the subscription
 
Deploying the infrastructure locally
1. Ensure that you have `make` installed and are in the terraform directory
2. In the terminal run `make tf-deploy` - this will verify the terraform and deploy to your specified subscription