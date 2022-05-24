---
layout: default
title: Overview
parent: Automate Change
nav_order: 1
introduction: Bridge the gap between distributed DevOps/SRE teams and centralized ServiceNow platform owner teams by automatically generating Change Requests. Utilize data from your existing CI/CD tools against sophisticated change policies to accelerate your pipeline.
dataflow: /assets/images/automate_change_dataflow.png
---

# Overview
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC 
{:toc}

## Introduction

{{ page.introduction }}

## Dataflow

![Dataflow]({{ site.baseurl }}{{ page.dataflow }})

1. Create a *Work Item* in `Azure Boards` and note the *Work Item ID* (e.g. AB#14) and assign the item to a developer.
1. Make your *code* and *configuration changes* and commit your changes to `GitHub`.

  > NOTE: Makes sure to set the commit message to the `Work Item ID` relating the code change to the `Azure Boards` work item.

1. Trigger the `ADO Pipeline` to start the build and deployment of your changes. 
1. Service is built and the Docker image is published to `Docker Hub` ready for final deployment.
1. The `ADO Pipeline` pauses, and a Change Request is *automatically generated* in ServiceNow for approval.
1. The `Change Request` is reviewed in ServiceNow and approved after reviewing all the changes.
1. The `ADO Pipline` is released and the Docker image is deployed to the `Azure Kubernetes` environment

## Components


| Component | Description |
|-----------|-------------|
| [Azure DevOps Boards](https://azure.microsoft.com/en-us/services/devops/boards/) | Microsoft Azure Backlog tracking tool for your distributed teams.|
| [GitHub Source Control](https://github.com) | Leading Source Code hosting platform for Version Control & Collaboration for your distributed teams.|
| [Azure DevOps Pipelines](https://azure.microsoft.com/en-us/services/devops/pipelines/) | Microsoft Azure Pipelines used to continuously Build, Test, and Deploy to any Platform and Cloud.|
| [Docker Hub](https://hub.docker.com) | Leading Docker Public Registry for finding and sharing Docker Container Images with your distributed teams.|
|[ServiceNow DevOps Change Velocity]({{site.data.urls.devops_change_velocity}}) | ServiceNow Change Automation for your Cloud Native Source code.|
| [ServiceNow DevOps Config]({{site.data.urls.devops_change_config}}) | ServiceNow Change Automation for your Cloud Native Configurations & Properties.|
| [Azure Kubernetes](https://docs.microsoft.com/en-us/azure/aks/intro-kubernetes) | Microsoft Azure mananaged Kubernetes Cluster for your Cloud Native Workloads.|


## Next Steps

* Follow the [Guide]({{ site.baseurl }}/pages/automate_change/guide) to implement in your environment.