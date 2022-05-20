### Create Boutique Application namespace

1. Start a Bash Shell

1. Configure kubectl environment variable

    ```
    export KUBECONFIG=$HOME/.kube/config-aks
    ```

1. Set kubectl context for AKS (See Example below)

    ```
    kubectl config use-context olympus
    ```

1. Create Boutique Application namespace (e.g. `cassandra`)

    ```
    kubectl create ns cassandra
    ```