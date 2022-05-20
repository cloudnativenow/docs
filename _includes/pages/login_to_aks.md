1. Configure kubectl environment variable

    ```
    export KUBECONFIG=$HOME/.kube/config-aks
    ```

1. Set kubectl context for AKS (See Example below)

    ```
    kubectl config use-context olympus
    ```

1. Test AKS Cluster Connection

    ```
    kubectl cluster-info
    kubectl get nodes -A
    ```

    ![Boutique Frontend](/assets/images/kubectl_cluster_info.png)    