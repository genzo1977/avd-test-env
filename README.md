To create a remote backend for Terraform in Azure, you can use Azure Storage to store the Terraform state files and Azure Cosmos DB or Azure Blob's native locking mechanism to manage state locking. Here's how to configure it using Azure Storage.

### Prerequisites:
1. Install Terraform on the local machine
`choco install -y terraform`
2. Install Azure CLI
https://learn.microsoft.com/en-us/cli/azure/install-azure-cli-windows?tabs=azure-cli
3. Authenticate via Azure CLI

`az login --tenant xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx --verbose`

e.g.

`az login --tenant 4d4dcd44-f444-4444-b444-a44444ca4ced --verbose`

5. Restart VS Code.
6. If you get ` Error: Output refers to sensitive values`
change 
`sensitive = false`
to
`sensitive = true`

```
# Storage account access key
output "storage_account_primary_access_key" {
  value     = azurerm_storage_account.storage.primary_access_key
  sensitive = true
}
```


### Steps to Initialize and Apply:
1. Run `terraform init` to initialize the backend.
2. Run `terraform apply` to apply the infrastructure and store the state remotely.
3. Update Terraform provider block in your architecture directory with the below
```
  backend "azurerm" {
    resource_group_name  = "your-resource-group"
    storage_account_name = "yourstorageaccount"
    container_name       = "your-container"
    key                  = "terraform.tfstate"
  }
```
