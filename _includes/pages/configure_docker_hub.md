### Configure Docker Hub

You will need a Docker Hub _Access Token_ to kickoff deployment processes from Azure DevOps Pipelines. Procedure is as follows:

1. Browse to [Docker Hub]({{site.data.urls.docker_hub}})

1. Navigate to **Your Profile > Account Settings > Security**

1. Press `New Access Token` and enter the following:

    | Field | Value |
    |-------|-------|
    | Description  | Any memorable string (e.g. `mytoken`) |
    | Scope | `Read, Write, Delete` |

1. Safeguard your `Access Token`