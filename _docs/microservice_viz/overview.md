---
layout: default
title: Overview
parent: Microservice Visibility
nav_order: 1
---

## Table of contents
{: .no_toc .text-delta }

1. TOC 
{:toc}

## Introduction

Increase the visibility of Cloud Native microservices in a single Workspace. Quickly register services in minutes via REST and onboard your distributed teams. Connect your services to telemetry via Webhook integration and resolve incidents faster with alert automation.

## Dataflow

![Dataflow]({{ site.baseurl }}/assets/images/visibility_dataflow.png)

1. Deploy Boutique Microservices App to the `Azure Kubernetes` environment.
1. Update the Boutique YAML File and verify all services and relationships are valid.
1. Make your edits and commit your changes to `GitHub`.
1. Trigger the `ADO Pipeline` to start registration of your services.
1. Services are registered in ServiceNow via the `Site Reliability Operations` REST API
1. Review the `Service Map` in ServiceNow using the `Site Reliability Operations` Workspace

## Components

| Component | Description |
|-----------|-------------|
| [Azure Kubernetes](https://docs.microsoft.com/en-us/azure/aks/intro-kubernetes) | Microsoft Azure mananaged Kubernetes Cluster for your Cloud Native Workloads.|
| [GitHub Source Control](https://github.com) | Leading Source Code hosting platform for Version Control & Collaboration for your distributed teams.|
| [Azure DevOps Pipelines](https://azure.microsoft.com/en-us/services/devops/pipelines/) | Microsoft Azure Pipelines used to continuously Build, Test, and Deploy to any Platform and Cloud.|
|[ServiceNow Site Reliability Operations (SRO)]({{site.data.urls.sro}}) | ServiceNow Site Reliability Operations (SRO) App |

## Next Steps

* Follow the [Guide](guide) to implement in your environment.

