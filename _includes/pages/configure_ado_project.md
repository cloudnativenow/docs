### Configure Azure DevOps Project

You can create connections from Azure Pipelines to external and remote services for executing tasks in a job. Your Azure DevOps Pipelines will need to connect to GitHub to retrieve source code and also connect to Kubernetes to deploy Docker images from Docker Hub. Procedure is as follows:

1. Sign In to [Azure DevOps]({{site.data.urls.ado}})

1. Create a _new project_ as follows:

    | Field | Value |
    |-------|-------|
    | Project name  | Any memorable name (e.g. `cassandra`) |
    | Visibility | Public |

1. Navigate to **Project Settings > Pipelines > Service Connections**

1. Create a _new service connection_ for GitHub as follows:

    | Field | Value |
    |-------|-------|
    | Service or connection type | `GitHub` |
    | Authentication method | `Personal Access Token` |
    | Personal Access Token | YOUR GITHUB PERSONAL ACCESS TOKEN |
    | Service connection name | `github` |
    | Grant access permission to all pipelines | `True` |

1. Create a _new service connection_ for Kubernetes as follows:

    | Field | Value |
    |-------|-------|
    | Service or connection type | `Kubernetes` |
    | Authentication method | `Azure Subscription` |
    | Azure Subscription | YOUR AZURE SUBSCRIPTION ID |
    | Cluster | YOUR AKS CLUSTER NAME (e.g. `olympus`) |
    | Namespace | `default` |
    | Use cluster admin credentials | `True` |
    | Service connection name | `olympus` |
    | Grant access permission to all pipelines | `True` |