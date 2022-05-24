---
layout: default
title: Overview
parent: Microservice Discovery
nav_order: 1
introduction: Leverage the Lightstep Service Graph Connector to automatically detect and map services and relationships from Traces. The Service Graph is an interactive mapping of all technical and business service dependencies. This feature allows users to easily understand how services combine to deliver customer-facing or business capabilities. View the health of the full service topology at a glance. During incident response, understand the full blast radius of an issue, zero in on the probable cause, and facilitate cross-team collaboration. This version also supports the ability to configure the ingestion of Lightstep Alerts through event management and automatically correlates events to hosts or application services.
dataflow: /assets/images/disco_microservices.png
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

1. Configure your Azure Kubernetes environment with the latest Service Graph compatible [OTEL Collector](https://github.com/lightstep/lightstep-partner-toolkit/pkgs/container/lightstep-partner-toolkit-collector).

1. Configure Lightstep to send dynamic trace based service diagrams to ServiceNow.

1. Configure ServiceNow to dynamically receive service maps from Lightstep.

1. Examine Services & Relationships in ServiceNow using Service Maps and Dependencies Views

## Components

| Component | Description |
|-----------|-------------|
| [ServiceNow Lightstep](https://lightstep.com/) | The ServiceNow cloud-native reliability platform.|
| [Lightstep Service Graph Connector](https://store.servicenow.com/sn_appstore_store.do#!/store/application/803c697f77f63010f1351bfaae5a99a6)  | Automatically import Lightstep Trace based service dependencies into ServiceNow | 
| [GitHub Source Control](https://github.com) | Leading Source Code hosting platform for Version Control & Collaboration for your distributed teams.|
| [Azure DevOps Pipelines](https://azure.microsoft.com/en-us/services/devops/pipelines/) | Microsoft Azure Pipelines used to continuously Build, Test, and Deploy to any Platform and Cloud.|
| [Azure Kubernetes](https://docs.microsoft.com/en-us/azure/aks/intro-kubernetes) | Microsoft Azure mananaged Kubernetes Cluster for your Cloud Native Workloads.|

## Next Steps

* Follow the [Guide]({{ site.baseurl }}/pages/microservice_disco/guide) to implement in your environment.