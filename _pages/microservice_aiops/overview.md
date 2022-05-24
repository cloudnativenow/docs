---
layout: default
title: Overview
parent: Predict & Prevent Incidents
nav_order: 1
introduction: Use Health Log Analytics (HLA) to predict IT issues before they affect your users. The application helps you solve problems faster by collecting, understanding, and correlating machine-generated log data in real time. It detects anomalies from your application logs and discovers any deviation from normal behavior as it happens and alerts you of possible issues.
dataflow: /assets/images/aiops.png
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

1. Configure your Azure Kubernetes environment with [Fluent Bit](https://fluentbit.io) to collect all cluster logs and send them to [Azure Log Analytics](https://docs.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-tutorial).

1. Configure your ServiceNow instance to collect logs from Azure Log Analytics using [Health Log Analytics]({{site.data.urls.hla}})

1. Use Health Log Analytics to predict and prevent Incidents.

## Components

| Component | Description |
|-----------|-------------|
| [Health Log Analytics]({{site.data.urls.hla}}) | The ServiceNow Health Log Analytics collects logs streaming into your ServiceNow instance from endpoints or data lakes, such as Splunk, Elasticsearch or Azure Log Analytics and detects anomalies using AI & Machine Learning |
| [Fluent Bit](https://fluentbit.io) | Fluent Bit is a super fast, lightweight, and highly scalable logging and metrics processor and it is the preferred log forwarding solution for cloud and containerized environments |
| [Azure Log Analytics](https://docs.microsoft.com/en-us/azure/azure-monitor/logs/log-analytics-tutorial)  | Log Analytics is a tool in the Azure portal to edit and run log queries from data collected by Azure Monitor Logs and interactively analyze their results | 
| [Azure Kubernetes](https://docs.microsoft.com/en-us/azure/aks/intro-kubernetes) | Microsoft Azure mananaged Kubernetes Cluster for your Cloud Native Workloads.|

## Next Steps

* Follow the Guide to implement in your environment.