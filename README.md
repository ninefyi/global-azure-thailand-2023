# Azure Global Thailand 2023
## MongoDB Atlas, GitHub Codespace, Azure App Service, Azure Developer CLI
## Template [link](https://github.com/azure-samples/todo-nodejs-mongo)

## Install the Azure Developer CLI
- [Azure Developer CLI](https://learn.microsoft.com/en-us/azure/developer/azure-developer-cli/install-azd)
- Run command `sudo curl -fsSL https://aka.ms/install-azd.sh | bash`
- Run command `azd auth login`

## Install the Azure CLI
- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
- Run command `sudo curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash`
- Run command `az login --use-device-code`

## Initial template
- Run command: `azd init --template todo-nodejs-mongo`
- Change version of nodejs infra/app/api.bicep to 16-lts

## Run below command
- `azd up`
- create vnet network
```bash
az network vnet create \
--name vnet-demo \
--resource-group rg-demo \
--address-prefix 10.0.0.0/16 \
--subnet-name subnet-demo \
--subnet-prefixes 10.0.0.0/24
```
- run command
```bash
az network vnet subnet update --resource-group rg-demo --vnet-name vnet-demo --name subnet-demo --disable-private-endpoint-network-policies true
```
- create a private endpoint on MongoDB Atlas (you need to upgrade the plan at least M10)
- API app service - app vnet integrate [link](https://learn.microsoft.com/en-us/azure/app-service/configure-vnet-integration-enable)
- update connection string on azure key vault
- restarted api app service

## Remove all services
- Run command: `azd down`
- Terminate MongoDB Atlas cluster