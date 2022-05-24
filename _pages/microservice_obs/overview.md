---
layout: default
title: Overview
parent: Microservice Observability
nav_order: 1
introduction: Cloud Native Service Operations Teams can quickly analyze performance and behavior for complex microservice stacks using Lightstep Telemetry Data (Traces, Metrics & Logs) to  reduce outages and increase systems reliability. Understand and resolve complex issues across any number of services and reveal hidden dependencies to help diagnose and pinpoint exactly Where, Why, and How incidents occur.
dataflow: /assets/images/lightstep_obs.png
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

1. Instrument your services with Open Telemetry. For polyglot applications you can use the respective [Open Telemetry SDK's](https://opentelemetry.io/docs/instrumentation/) to instrument your code. 

  > NOTE: For your convenience we have allready instrumented all services for you.

1. Review the instrumentation *code* and *configuration changes* and commit your changes to `GitHub`.

1. Trigger the `ADO Pipeline` to start the build and deployment of your changes. 

1. Services are built and the Docker images are deployed to the `Azure Kubernetes` environment

1. Use the `ServiceNow Lightstep` app to examine your **Service Directory** and start monitoring.

1. Examine your **Latency Histograms**, review your **Service Diagrams** and spot long running transactions that are slowing down your system.


## Components

| Component | Description |
|-----------|-------------|
| [ServiceNow Lightstep](https://lightstep.com/) | The ServiceNow cloud-native reliability platform.|
| [GitHub Source Control](https://github.com) | Leading Source Code hosting platform for Version Control & Collaboration for your distributed teams.|
| [Azure DevOps Pipelines](https://azure.microsoft.com/en-us/services/devops/pipelines/) | Microsoft Azure Pipelines used to continuously Build, Test, and Deploy to any Platform and Cloud.|
| [Azure Kubernetes](https://docs.microsoft.com/en-us/azure/aks/intro-kubernetes) | Microsoft Azure mananaged Kubernetes Cluster for your Cloud Native Workloads.|

## Next Steps

* Follow the [Guide]({{ site.baseurl }}/pages/microservice_obs/guide) to implement in your environment.