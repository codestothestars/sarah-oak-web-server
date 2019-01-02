# Sarah Oak Web Server
The web server for the public website of Sarah Oak.

Serves the static assets published by [codestothestars/sarah-oak-web](https://github.com/codestothestars/sarah-oak-web) at [sarahoak.com](http://sarahoak.com).

This web server is implemented as an [Azure Function](https://azure.microsoft.com/en-us/services/functions).

## Development
### Dependencies
* [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest) (needed for local development environment setup)
* [Node.js](https://nodejs.org) 11.6.0 ([nvm](https://github.com/creationix/nvm) is recommended)

### Install
Once you've installed the above dependencies and cloned this repository, install NPM dependencies.

```shell
npm install
```

### Environment Setup
Even for local development, Azure Functions expect access to a storage account. Run the following shell commands to create a resource group and storage account...
```shell
az group create --name sarah-oak-web-server

az storage account create \
    --https-only \
    --kind StorageV2 \
    --name $storageAccountName \
    --resource-group sarah-oak-web-server \
    --sku Standard_LRS
```

...where `$storageAccountName` is a unique name for your storage account.

Retrieve the connection string for the storage account...

```shell
az storage account show-connection-string \
    --name $storageAccountName \
    --output tsv \
    --query connectionString \
    --resource-group sarah-oak-web-server
```

...then add it to your local settings.

```shell
npx func settings add AzureWebJobsStorage "$connectionString"
```

### Run
After setting up your development environment, start a local server to run the application.

```shell
npm start
```

### Branching Model
This project uses the following branching rules.
* `master` contains the current production state. Merge changes into `master` to trigger a production deployment. Development does not occur here.
* `develop` contains the current development state planned for the next release. Feature branches are created from here and merged back in when the feature is complete.
* Use a named feature branch for each feature in development. This is where all main development should occur.
* `release-*` branches are created from `develop` to prepare the next release. Perform final testing and version checking here, then merge into `master` to trigger a production deployment and back into `develop` to update development.
* `hotfix-*` branches are created from `master` to fix immediate production issues. Merge back into `master` to deploy to production and into `develop` to update the development version.

### IDE
The application can be developed in any IDE in conjunction with the dependencies and commands listed above. [Visual Studio Code](https://code.visualstudio.com) is a light, fully-featured IDE that integrates well with Node.js, but is not required.
