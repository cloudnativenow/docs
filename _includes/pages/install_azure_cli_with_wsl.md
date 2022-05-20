### Install Azure CLI for WSL Ubuntu

The Azure command-line interface (Azure CLI) is a set of commands used to create and manage Azure resources. The Azure CLI is available across Azure services and is designed to get you working quickly with Azure, with an emphasis on automation. If you have a Windows Workstation with WSL Ubuntu, the installation is as follows:

1. Start a Bash Shell

1. Get Updates

    ```
    sudo apt-get update
    sudo apt-get install ca-certificates curl apt-transport-https lsb-release gnupg
    ```

1. Download and install the Microsoft signing key

    ```
    curl -sL https://packages.microsoft.com/keys/microsoft.asc \
    | gpg --dearmor \
    | sudo tee /etc/apt/trusted.gpg.d/microsoft.gpg > /dev/null
    ```

1. Add the Azure CLI software repository

    ```
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" \
    | sudo tee /etc/apt/sources.list.d/azure-cli.list    
    ```

1. Install the Azure CLI

    ```
    sudo apt-get update
    sudo apt-get install azure-cli
    ```

    > NOTE: For more detailed instructions consult the [Microsoft Azure CLL Docs for WSL on Ubuntu](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-linux?pivots=apt)

1. Test Login

    ```
    az login
    ```