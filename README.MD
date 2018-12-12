# terraform-example-for-bitbucket-pipelines

An example of infrastructure as code that provisions Azure infrastructure using Terraform through Bitbucket Pipelines.

When executed by Bitbucket Pipelines the Terraform script in this repo creates an Ubuntu VM on Azure.

## Requirements

- You need an Azure subscription.
- Create a service principle for Authentication: [https://www.terraform.io/docs/providers/azurerm/authenticating_via_service_principal.html](https://www.terraform.io/docs/providers/azurerm/authenticating_via_service_principal.html).
- You need an Azure storage account and container to store Terraform state: [https://docs.microsoft.com/en-us/azure/terraform/terraform-create-k8s-cluster-with-tf-and-aks#set-up-azure-storage-to-store-terraform-state](https://docs.microsoft.com/en-us/azure/terraform/terraform-create-k8s-cluster-with-tf-and-aks#set-up-azure-storage-to-store-terraform-state)

## Important files

- bitbucket-pipelines.yml - Bitbucket Pipelines configuration file that defines the build process for this repo.
- scripts/infrastructure - Directory that contains Terraform scripts to create VM on Azure.

## Setup instructions

- Create a repo in Bitbucket.
- Enable Pipelines throught the Bitbucket settings for the repo.
- You can view/modified the configuration for Pipelines in the file bitbucket-pipelines.yml.
- For authentiation with your service principle you need to set the following [environment variables in Bitbucket](https://confluence.atlassian.com/bitbucket/variables-in-pipelines-794502608.html)
    - ARM_SUBSCRIPTION_ID
    - ARM_CLIENT_ID
    - ARM_CLIENT_SECRET 
    - ARM_TENANT_ID
    - For more details on these environment variables please see [the Terraform docs for the Azure provider](https://www.terraform.io/docs/providers/azurerm/index.html#argument-reference).
- For storing Terraform state in Azure storage set these environment variables in Bitbucket:
    - TF_BACKEND_RES_GROUP
    - TF_BACKEND_STORAGE_ACC
    - TF_BACKEND_CONTAINER
    - TF_BACKEND_KEY
- Commit this code to your repo and push it to Bitbucket. 

After pushing to Bitbucket your build should execute.
You can check recent builds in Bitbucket under the Pipelines section. Here you can see if the build succeeded or failed.
If it failed you can check the console to find out why.

After a successful build you will have provisioned an Ubuntu VM in Azure.


## Resources

- https://www.nicksantamaria.net/post/self-deploying-site-hugo-terraform-bitbucket-pipelines/
- https://www.terraform.io/docs/providers/azurerm/index.html#argument-reference
- https://www.terraform.io/docs/providers/azurerm/authenticating_via_service_principal.html

### Using Azure storage to maintain Terraform state

- https://medium.com/@trstringer/use-azure-blob-storage-for-remote-terraform-state-5f809b95215a
- http://www.mikaelkrief.com/terraform-remote-backend-azure/
- http://teknews.cloud/terraform-remote-state-with-azure-storage/
- http://www.blueshift.dk/blog/terraform-remote-state-azure