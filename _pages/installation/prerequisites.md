---
layout: default
title: Prerequisites
parent: Installation
nav_order: 1
---

# Prerequisites
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC 
{:toc}

## Introduction

This site provides documentation, training, and other notes for implementing the Cloud Native Service Operations for ServiceNow Solutions. The instructions provided are geared towards developers and assume a basic level of competency and familiarity with the tools listed. Following is a list of prerequisite tools, configuration steps, and accesses needed before implementing the Cloud Native Service Operation solutions.

## Request a ServiceNow Instance

{% include pages/request_sn_instance.md %}

## Get some Accounts

{% include pages/get_github.md %}

{% include pages/get_azure.md %}

{% include pages/get_docker_hub.md %}

## Setup your Workstation

{% include pages/install_wsl_for_windows.md %}

{% include pages/create_ssh_key.md %}

{% include pages/install_azure_cli_with_wsl.md %}

{% include pages/install_azure_cli_with_brew.md %}

## Deploy Azure Kubernetes

{% include pages/install_aks_with_azure_cli.md %}

{% include pages/configure_kubectl_for_aks.md %}

## Configure your Projects

{% include pages/configure_github.md %}

{% include pages/configure_docker_hub.md %}

{% include pages/configure_ado_project.md %}

## Deploy Boutique

{% include pages/fork_boutique.md %}

{% include pages/build_all_boutique_images.md %}

{% include pages/create_boutique_namespace.md %}

{% include pages/deploy_all_boutique_images.md %}

{% include pages/check_boutique_deployment.md %}