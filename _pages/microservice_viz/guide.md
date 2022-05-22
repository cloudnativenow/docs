---
layout: default
title: Guide
parent: Microservice Visibility
nav_order: 2
---

# Guide
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC 
{:toc}

## Prerequisites

{% include pages/install_sn_sro.md %}

## Verify Service Map
### Locate Service Map YAML File in GitHub

1. Browse to [GitHub]({{site.data.urls.github}})

1. Navigate to your GitHub Repository (e.g. `cassandra`)

1. Locate the `registration/boutique.json` file

### Review Service Map

1. Verify all `services` and `relationships` are valid

    ![Boutique Json]({{ site.baseurl }}/assets/images/boutique_json.png)

## Register Services

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
    | Path | `/azure-pipelines/register-services.yml` | 

1. Press `Continue` to review your pipeline YAML.

1. Create the following Pipeline Variables:

    | Name | Value | Keep this value secret | Let users override this value when running this pipeline | 
    |-------|-------|-------|-------|
    | NOW_USERNAME | YOUR SN USER ID | False | True | 
    | NOW_PASSWORD | YOUR SN PASSWORD | True | True |
    | NOW_SERVER | YOUR SERVICENOW URL | False | True |
    | SERVICE_MAP | `boutique` | False | True |

1. Using the `Run` Button, select `Save Pipeline`

1. Rename Pipeline as follows:

    | Field | Value |
    |-------|-------|
    | Name  |  `register-services` |
    | Select folder | `\azure-pipelines` | 

### Run Pipeline    

1. Press `Run Pipeline`

1. Review **Variables** and press `Run`

1. Monitor the Pipeline and make sure it runs successfully

    ![Register Services]({{ site.baseurl }}/assets/images/register_services_pipeline.png)

## Configure Site Reliability Operations
### Create new Teams

1. Navigate to **Site Reliability Operations > Site Teams > All Teams**

1. Create a Team called `Team Boutique` and add yourself as a member:

### Assign all Services to the new Team

1. Navigate to **Site Reliability Operations > Services > Unasigned Services**

1. Set the **Operational Status** for each Service to `Operational`

1. Set the **Support Group** for each Service to `Team Boutique`

### Review the Service Map

1. Navigate to **Site Reliability Operations > Site Reliability Ops Workspace**

1. Click on the **Services** Icon

1. Click on the **Boutique** Service

1. Clon on **Relationships** Tab

1. Review the _Boutique_ Service Map

    ![Boutique Service Map]({{ site.baseurl }}/assets/images/boutique_service_map.png)