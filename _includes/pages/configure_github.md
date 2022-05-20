### Configure GitHub

You will need a Github _Personal Access Token_ (aka. PAT) to kickoff deployment processes from Azure DevOps Pipelines. You will also need to configure GitHub with your Personal SSH Key so you can pull code down to your workstation. Procedure is as follows:

1. Browse to [GitHub]({{site.data.urls.github}})

1. Navigate to **Your Profile > Settings > Developer Settings > Personal Access Tokens**

1. Press `Generate new token` and enter the following:

    | Field | Value |
    |-------|-------|
    | Note  | Any memorable string (e.g. `myrepo`) |
    | Expiration | `30 days` (or longer) | 
    | Scope | `repo:*` |

1. Safeguard your `Personal Access Token`

1. Navigate to **Your Profile > Settings > SSH and GPG keys**

1. Press `New SSK key` and enter the following:

    | Field | Value |
    |-------|-------|
    | Title  | Any memorable string (e.g. `mykey`) |
    | Key | Paste in YOUR PERSONAL SSH PUBLIC KEY | 

1. Press `Add SSH Key`