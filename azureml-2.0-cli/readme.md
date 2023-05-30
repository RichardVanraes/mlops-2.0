# MLOps Pipelines

## Preparing

Make sure to install the Azure Machine Learning SDK for Python:

```bash
pip install azureml-sdk
```

Also install the Azure CLI for Windows, Linux or macOS:
    
https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest

az extension add -n ml

## Execute the first commands to setup your environment if needed

```bash
az login
az account set --subscription <subscription_id>
az group create --name <resource_group> --location <location>
az ml folder attach -w <workspace_name> -g <resource_group>
```

## Create the Azure Machine Learning Workspace (Can also be done through the Azure Portal)

```bash
az ml workspace create --workspace-name <workspace_name> --resource-group <resource_group> --location <location>
```

:::success
**QUESTION**
How to set the default workspace and resource group for the Azure CLI?

**ANSWER**
```bash

```

:::

## Create the Compute Target using the CLI
This can also be done through the Azure Portal, but for the sake of automation, we'll do it here.
We use an environment variable that will be set in GitHub Actions to determine the compute target name.

Change the values inside the compute.yml to override the defaults.

```bash
az ml compute create --file compute.yml
```

## Create the environments for the components

This will automatically fetch the conda file as well.

```bash
az ml environment create --file env-aml-pillow.yml
```

## Create the components

Execute these commands inside of the respective folder.
```bash
az ml component create --file dataprep.yml
```