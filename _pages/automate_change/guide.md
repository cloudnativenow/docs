---
layout: default
title: Guide
parent: Automate Change
nav_order: 2
---

# Guide
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC 
{:toc}

## Prerequisites

{% include pages/install_sn_devops_change.md %}

{% include pages/install_sn_devops_config.md %}

## Configure ADO Backlog
### Create Some ADO Work Items

1. Sign In to [Azure DevOps]({{site.data.urls.ado}})

1. Select the Boutique Project (e.g. `cassandra`) you configured earlier.

1. Navigate to `Boards` and create a couple of `Work Items`

    ![Work Items]({{ site.baseurl }}/assets/images/ado_work_items.png)

    >NOTE: As a best coding practice, developers should set the Git commit message to one of these Work Items relating the code change to the Azure Boards work item.

### Connect GitHub with Azure Boards

1. Sign In to [Azure DevOps]({{site.data.urls.ado}})

1. Select the Boutique Project (e.g. `cassandra`) you configured earlier.

1. Navigate to `Project Settings > Boards > GitHub connections` and press the `Connect your GitHub account` button.

1. Enter your GitHub password if prompted.

1. Select the GitHub organization that you want to connect to Azure Boards (e.g. YOUR GITHUB USER ID)

1. Select the GitHub repository you want to use with your Azure Boards. (e.g. YOUR GITHUB USER ID/cassandra)

1. Press the `Approve, Install & Authorize` Button

    ![GitHub Connection]({{ site.baseurl }}/assets/images/ado_github_connection.png)

1. At this point, all commits in Git using the Azure Boards Work Item notation (e.g. AB#123) will be propagated to the relevant Work Item.

    >NOTE: For more information on linking Git commits to Azure Boards see the [Azure Devops Documentation](https://docs.microsoft.com/en-us/azure/devops/boards/github/link-to-from-github?view=azure-devops#use-ab-mention-to-link-from-github-to-azure-boards-work-items)

## Configure ServiceNow DevOps Change


### Configure DevOps Performance Analytics Jobs

1. Login to your NOW Instance as Administrator

1. Navigate to **Performance Analytics > Data Collector > Jobs**

1. Search for Jobs where **Name** = `*DevOps`

    ![PA Jobs]({{ site.baseurl }}/assets/images/pa_jobs.png)

1. For each Job, set the fields as follows:

    | Field | Value |
    |-------|-------|
    | Active | `true` |
    | Run as | `System Administrator` |

    >NOTE: You will have to switch application scope from `Global` to `DevOps Data Model` or `DevOps Insights` accordingly to make changes to _Jobs_.

### Configure Application Services Change Group

1. Login to your NOW Instance as Administrator

1. Navigate to **Configuration > Application Services**

1. For all Application Services under change control, set the **Change Group** field to the relevant group (e.g. `Team Boutique`)

    ![Change Group]({{ site.baseurl }}/assets/images/change_group_assignment.png)

### Create ServiceNow DevOps App

1. Login to your NOW Instance as Administrator

1. Navigate to **DevOps > Create App**

1. Create an App as follows:

    | Field | Value |
    |-------|-------|
    | Application Name | `Boutique App` |

### Create ServiceNow DevOps Admin User

1. Login to your NOW Instance as Administrator

1. Navigate to **User Administration > Users**

1. Create an admin user as follows:

    | Field | Value |
    |-------|-------|
    | Username | YOUR DEVOPS ADMIN USER NAME (e.g. `devops`) |
    | Password | YOUR DEVOPS ADMIN USER PASSWORD |
    | Roles | `admin` |

1. Press **Submit** Button

### Create ServiceNow DevOps Admin Credential

1. Login to your NOW Instance as Administrator

1. Navigate to **Connections & Credentials > Credentials**

1. Create a _Basic Auth Credential_ as follows:

    | Field | Value |
    |-------|-------|
    | Name | YOUR DEVOPS ADMIN USER CREDENTIAL NAME (e.g. `devops`) |
    | User Name | YOUR DEVOPS ADMIN USER NAME (e.g. `devops`) |
    | Password | YOUR DEVOPS ADMIN USER PASSWORD |

1. Press **Submit** Buttom

### Configure ServiceNow DevOps Integration User

1. Login to your NOW Instance as Administrator

1. Navigate to **User Administration > Users**

1. Locate the User ID: `devops.integration.user`

1. Update User as follows:

    | Field | Value |
    |-------|-------|
    | Password | YOUR DEVOPS INTEGRATION USER PASSWORD |

1. Press **Update** Button

### Create ServiceNow DevOps Connection

1. Login to your NOW Instance as Administrator

1. Navigate to **Connections & Credentials > Connections & Credentials Aliases**

1. Click on the **CreateDevOpsTool** alias

1. Under the **Connections** Tab create a new Connection

1. Create a _New Connection & Credential Alias_ as follows:

    | Field | Value |
    |-------|-------|
    | Name | YOUR SERVICENOW CONNECTION NAME(e.g. `devops`) |
    | Credential | YOUR DEVOPS ADMIN USER CREDENTIAL NAME (e.g. `devops`) 
    | Connection URL | YOUR SERVICENOW URL (e.g. `https://srecon22.service-now.com`) | 

1. Press **Submit** Button

### Create DevOps GitHub Tool

1. Login to your NOW Instance as Administrator

1. Navigate to **DevOps > Tools > Create New**

    | Field | Value |
    |-------|-------|
    | Name | YOUR ADO TOOL NAME (e.g. `MyGitHub`) |
    | Tool Integration | `GitHub` | 
    | Tool Url |  GITHUB API URL (e.g. `https://api.github.com`) |
    | Credential Type | `Basic Auth` |
    | Tool Username | YOUR GITHUB ID |
    | Tool Password / Access Token | YOUR GITHUB PAT |

1. Press **Submit** Button

1. Press **Discover** Button

1. Select **Repositories** Tab

1. Select the _cassandra_ repository

1. Set **Track file changes** = `True`

1. Press the **Configure** Button and configure as follows:

    | Field | Value |
    |-------|-------|
    | Integration User | `DevOps Integration User` |
    | Integration user password | YOUR DEVOPS INTEGRATION USER PASSWORD | 

1. Press **Send** Button

    >NOTE: The provided Tool URL and credentials will be used to create a Webhook from the Git Repo to ServiceNow.

### Create DevOps ADO Tool

1. Login to your NOW Instance as Administrator

1. Navigate to **DevOps > Tools > Create New**

    | Field | Value |
    |-------|-------|
    | Name | YOUR ADO TOOL NAME (e.g. `MyAdo`) |
    | Tool Integration | `Azure DevOps` | 
    | Tool Url |  YOUR ADO ORG URL (e.g. `https://dev.azure.com/YOURORG/YOURREPO`) |
    | Tool Username | YOUR ADO TOKEN NAME |
    | Tool Password / Access Token | YOUR ADO TOKEN VALUE |    

1. Press **Submit** Button

1. Press **Discover** Button

1. Select **Repositories** Tab

1. Select the _cassandra_ repository

1. Set the **Track** field to `true`

1. Press the **Configure** Button and configure as follows:

    | Field | Value |
    |-------|-------|
    | Integration User | `DevOps Integration User` |
    | Integration user password | YOUR INTEGRATION USER PASSWORD| 

1. Press **Send** Button

    >NOTE: The provided Tool URL and credentials will be used to create 2 Service Connections in Azure DevOps

1. Select **Pipelines** Tab

1. For all Pipelines, set the **App** field to `Boutique App`

1. For all Pipelines, set the **Track** field to `true`

    ![DevOps Pipelines]({{ site.baseurl }}/assets/images/devops_pipelines.png)

### Check Service Connections

1. Sign In to [Azure DevOps]({{site.data.urls.ado}})

1. Select the Boutique Project (e.g. `cassandra`) you configured earlier.

1. Navigate to `Project Settings` and press the `Service Connections` button.

1. Locate the 2 ServiceNow Service Connections you created earlier from ServiceNow.

    ![Service Connections]({{ site.baseurl }}/assets/images/ado_service_connections.png)

### Configure Pipeline

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
    | Path | `/azure-pipelines/kubernetes-deploy.yml` | 

1. Press `Continue` to review your pipeline YAML.

1. Un-Comment the `DevOps_Change` Stage and set all occurences of `connectedServiceName` to your ServiceNow Service Connection name.

    ![Uncomment Pipeline]({{ site.baseurl }}/assets/images/uncomment_pipeline.png)

1. Create the following Pipeline Variables:

    | Name | Value | Keep this value secret | Let users override this value when running this pipeline | 
    |-------|-------|-------|-------|
    | REPO_USERNAME | YOUR DOCKER HUB ID | False | True | 
    | REPO_PAT | YOUR DOCKER PAT | True | True |
    | REPO_PREFIX | YOUR DOCKER HUB ID  | False | True |
    | SERVICE_NAME |  YOUR SERVICE NAME (e.g. `frontend`) | False | True | 
    | SERVICE_NAMESPACE | `cassandra`| False | True |

1. Using the `Run` Button, select `Save Pipeline`

## Approve Code Change

### Make a Code Change

1. Sign In to [GitHub]({{site.data.urls.github}})

1. Select the Boutique Project (e.g. `cassandra`) you configured earlier.

1. Locate the `src/adservice/src/main/java/hipstershop/AdService.java` file

1. Update the `createAdsMap` method for any product to display different discount text as follows:

    ![Code Change]({{ site.baseurl }}/assets/images/code_change.png)

1. Commit changes using the Azure Boards Work Item notation (e.g. AB#123)

    ![Code Change]({{ site.baseurl }}/assets/images/commit_code.png)

### Trigger the Azure DevOps Pipeline

1. Sign In to [Azure DevOps]({{site.data.urls.ado}})

1. Select the Boutique Project (e.g. `cassandra`) you configured earlier.

1. Navigate to `Pipelines > All` and select the `azure-pipelines` folder.

1. Run the `kubernetes-deploy` Pipeline and set parameters as follows:

    | Parameter | Value |
    |-----------|-------|
    | SERVICE_NAME  | `adservice` |

1. Notice that the pipeline has been paused, pending change control approval.

    ![Paused Pipeline]({{ site.baseurl }}/assets/images/paused_pipeline.png)

### Approve Change in ServiceNow

1. Login to your NOW Instance as Administrator

1. Navigate to **DevOps > Orchestrate > Pipeline Change Requests**

    ![Change Request]({{ site.baseurl }}/assets/images/change_request.png)

1. Select Change and review all relevant items.

    ![Change Detail]({{ site.baseurl }}/assets/images/change_request_detail.png)

1. Click on the `Approvers` Tab

1. Hover over **Approver** and right-click `Approve` the item.

1. Press the **Implement** Button

    >NOTE: Notice how the Azure DevOps Pipeline has been un-paused.

1. Browse to the EXTERNAL-IP to view the Boutique Application and look for the updated AdService discount text.

    ![Discounted Watches]({{ site.baseurl }}/assets/images/discounted_watches.png)
