### Install Azure CLI for macOS

The Azure command-line interface (Azure CLI) is a set of commands used to create and manage Azure resources. The Azure CLI is available across Azure services and is designed to get you working quickly with Azure, with an emphasis on automation. If you have a MacOS Workstation, the installation is as follows:

1. Start a Bash Shell

1. Install the Azure CLI

    ```
    brew update && brew install azure-cli
    ```

    > NOTE: For more detailed instructions consult the [Microsoft Azure CLL Docs for macOS](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli-macos)

1. Test Login

    ```
    az login
    ```