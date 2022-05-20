### Deploy All Boutique Images using Helm Pipeline

The Boutique application consists of 12 Docker Images which need to be depoyed to your Azure Kubernetes using the provided `kubernetes-deploy-all` Helm Pipeline. Procedure is as follows:

1. Sign In to [Azure DevOps]({{site.data.urls.ado}})

1. Select the Boutique Project (e.g. `cassandra`) you configured earlier.

1. Navigate to `Pipelines > All` and create an `azure-pipelines` folder, if it does not exist.

1. Navigate to the `azure-pipelines` folder and press `Create Pipeline`

1. For the `Where is your code?` prompt, select `GitHub`

1. For the `Select a repository` prompt, select your GitHub Repository.

1. Press `Approve and Install`

1. Enter your GitHub password if prompted.

1. At the `Configure your pipeline` prompt, select `Existing Azure Pipelines YAML file`

1. At the `Select an existing YAML file` prompt, set fields as follows:

    | Field | Value |
    |-------|-------|
    | Branch  | `main` |
    | Path | `/azure-pipelines/kubernetes-deploy-all.yml` | 

1. Press `Continue` to review your pipeline YAML.

1. Create the following Pipeline Variables:

    | Name | Value | Keep this value secret | Let users override this value when running this pipeline | 
    |-------|-------|-------|-------|
    | SERVICE_NAMESPACE | `cassandra`| False | True | 
    | REPO_PREFIX  | YOUR DOCKER HUB ID  | False | True |

1. Using the `Run` Button, select `Save Pipeline`

1. Rename Pipeline as follows:

    | Field | Value |
    |-------|-------|
    | Name  |  `kubernetes-deploy-all` |
    | Select folder | `\azure-pipelines` | 

1. Press `Run Pipeline`

1. Review parameters and press `Run`