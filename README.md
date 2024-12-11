To create a remote backend for Terraform in Azure, you can use Azure Storage to store the Terraform state files and Azure Cosmos DB or Azure Blob's native locking mechanism to manage state locking. Here's how to configure it using Azure Storage.

### Prerequisites:
1. Install Terraform on the local machine
`choco install -y terraform`
2. Install Azure CLI
https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-windows?tabs=azure-cli
3. Authenticate via Azure CLI
4. Clone this repo:
`git clone https://github.com/genzo1977/avd-test-env.git`
5. Change directory:
`cd .\avd-test-env\`
6. Log into Azure:
`az login`

### Steps to Initialize and Apply:
1. Run `terraform init` to initialize the backend.
2. Run `terraform plan` to see what you are about to apply
3. Run `terraform apply` to apply the infrastructure and store the state remotely.
4. Update Terraform provider block in your architecture directory with the below
```
  backend "azurerm" {
    resource_group_name  = "your-resource-group"
    storage_account_name = "yourstorageaccount"
    container_name       = "your-container"
    key                  = "terraform.tfstate"
  }
```
