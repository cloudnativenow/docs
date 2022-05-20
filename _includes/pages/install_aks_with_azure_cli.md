### Install Azure Kubernetes with Azure CLI

Azure Kubernetes Service (AKS) simplifies deploying a managed Kubernetes cluster in Azure by offloading the operational overhead to Azure. As a hosted Kubernetes service, Azure handles critical tasks, like health monitoring and maintenance. Installation is as follows:

1. Start a Bash Shell

1. Login to Azure

    ```
    az login
    ```

1. Create Resource Group (See Example below)

    ```
    az group create -n "olympus" -l "eastus"
    ```

    > NOTE: In this example we are creating a resource group called `olympus` and
    using the `eastus` region. 

1. Get latest AKS Versions available for your region (See Example below)

    ```
    az aks get-versions -l "eastus" -o table
    ```

    > NOTE: We recommend avoiding *preview* releases for stability
     

1. Deploy AKS (See Example below)

    ```
    az aks create --resource-group "olympus" --name "olympus" --node-count 4 --kubernetes-version "1.21.9" --ssh-key-value $HOME/.ssh/olympus.pub --node-vm-size "Standard_DS2_v2" --node-osdisk-size 30 --enable-managed-identity
    ```
    > NOTE: In this example we are creating a 4 node AKS cluster called `olympus` in the 
    `eastus` region with 30 Gig Disks with our SSH key called `olympus`