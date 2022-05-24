---
layout: default
title: Guide
parent: Microservice Observability
nav_order: 2
---

# Guide
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC 
{:toc}

## Prerequisites

{% include pages/get_lightstep.md %}


## Instrument Code

### Get Lightstep Access Token

1. Browse to [Lightstep App]({{site.data.urls.lightstep_app}})

1. Select your Project (e.g. dev, prod, or other)

1. Navigate to **Settings > Access Tokens**

1. Safeguard your `Access Token`

### Create Lightstep configmap

1. Start a Bash Shell

{% include pages/login_to_aks.md %}

1. Set Lightstep Access Token Environment Variable

    ```
    export LS_ACCESS_TOKEN=YOUR LIGHTSTEP ACCESS TOKEN
    ```

1. Create Lightstep configmap

    ```
    kubectl apply -n cassandra -f - <<EOF
    kind: ConfigMap
    apiVersion: v1
    metadata:
      name: lightstep-configmap
    data:
      collector-config: |
        receivers:
          otlp:
            protocols:
              grpc:
              http:
        exporters:
          otlp:
            endpoint: ingest.lightstep.com:443
            headers: 
              "lightstep-access-token": "${LS_ACCESS_TOKEN}"
          logging:
            loglevel: debug
        service:
          pipelines:
            traces:
              receivers: [otlp]
              processors: []
              exporters: [logging,otlp]             
    EOF
    ```

### Enable Instrumentation

1. Sign In to [GitHub]({{site.data.urls.github}})

1. Select the Boutique Project (e.g. `cassandra`) you configured earlier.

1. Locate the `helm/templates/kubernetes-manifests.yaml` file

1. Un-Comment the Deployment section for the `otelcollector`

1. Un-Comment the `image` section as follows:

    ```yaml
    image: otel/opentelemetry-collector-contrib:0.49.0 
    # image: ghcr.io/lightstep/lightstep-partner-toolkit-collector:latest
    ```

1. Un-Comment the Service section for the `otelcollector`

1. Un-Comment the `#Lightstep Instrumentation` sections for all the services to expose the `OTEL_EXPORTER_OTLP_TRACES_ENDPOINT` and `OTEL_RESOURCE_ATTRIBUTES` to Lightstep as follows:

    ```yaml
    # Lightstep Instrumentation
    - name: OTEL_EXPORTER_OTLP_TRACES_ENDPOINT
      value: "http://otelcollector:4317"
    - name: OTEL_RESOURCE_ATTRIBUTES
      value: "service.name=productcatalogservice,service.version=1.0.0"
    ```

1. Commit changes

## Deploy Instrumented Application

### Re-Deploy Application using Helm Pipeline

After the Lightstep instrumentation, we need to re-deploy the 10 Boutique application Pods along with the new Lightstep OTEL collector Pod to your Azure Kubernetes using the same provided `kubernetes-deploy-all` Helm Pipeline. Procedure is as follows:

1. Sign In to [Azure DevOps]({{site.data.urls.ado}})

1. Select the Boutique Project (e.g. `cassandra`) you configured earlier.

1. Navigate to `Pipelines > All > azure-pipelines`

1. Select the `kubernetes-deploy-all` Pipeline

1. Press `Run Pipeline`

1. Review **Variables** and press `Run` as follows:

    | Name | Value | Keep this value secret | Let users override this value when running this pipeline | 
    |-------|-------|-------|-------|
    | SERVICE_NAMESPACE | `cassandra`| False | True | 
    | REPO_PREFIX  | YOUR DOCKER HUB ID  | False | True |

1. Press `Run` 

1. Monitor the Pipeline and make sure it runs successfully

### Monitor Services

1. Browse to [Lightstep App]({{site.data.urls.lightstep_app}})

1. Select your Project (e.g. dev, prod, or other)

1. Navigate to the **Service Directory**, and you should see all 10 services emitting traces

    ![Lightstep Directory]({{ site.baseurl }}/assets/images/lightstep_directory.png)

1. Navigate the **Explorer** and query for non-health check operations, and sort by descending _Duration_ as follows:

    ```
    operation NOT IN ("/_healthz", "/grpc.health.v1.Health/Check", "grpc.grpc.health.v1.Health/Check", "grpc.health.v1.Health/Check", "PING")
    ```
    
    ![Lightstep Directory]({{ site.baseurl }}/assets/images/lightstep_explorer.png)

1. Click on one of the longer span durations to examine where the transaction is spending the most time as follows:

    ![Lightstep Directory]({{ site.baseurl }}/assets/images/lightstep_trace.png)

1. Navigate back to the **Explorer** and examine the live _Service Diagram_ detected by Lightstep from the Traces as follows:

    ![Lightstep Service Diagram]({{ site.baseurl }}/assets/images/lightstep_service_diagram.png)