---
layout: default
title: Guide
parent: Microservice Discovery
nav_order: 2
---

# Guide
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC 
{:toc}



## Prerequisites

### Microservice Observability

Implement the [Microservice Observability]({{ site.baseurl }}/pages/microservice_obs/overview) Solution.

{% include pages/install_sn_sgc.md %}

## Configure Lightstep

### Create Lightstep Stream

1. Browse to [Lightstep App]({{site.data.urls.lightstep_app}})

1. Select your Project (e.g. dev, prod, or other)

1. Navigate to **Streams**

1. Create a _Stream_ (e.g. `mystream`)

1. Click on your Stream

1. Note and safeguard your Stream ID from the URL as shown below:

    ![Stream ID]({{ site.baseurl }}/assets/images/stream_id.png)

### Get Lightstep Information

1. Browse to [Lightstep App]({{site.data.urls.lightstep_app}})

1. Select your Project (e.g. dev, prod, or other)

1. Navigate to **Settings**

1. Note and safeguard your `Organization` and your `Project` identifiers.

1. Navigate to **Settings > Access Tokens**

1. Safeguard your `Access Token`

1. Navigate to **Account > Account Settings > API Keys**

1. Create and safeguard an _API Key_ as follows:

    | Field | Value |
    |-------|-------|
    | Description  | Any memorable description (e.g. `srecon22`) |
    | Role | `Member` |

## Update the OTEL Collector to use the Service Graph compatible version

### Update the Lightstep configmap

1. Start a Bash Shell

{% include pages/login_to_aks.md %}

1. Set Lightstep Access Token Environment Variable

    ```bash
    export LS_ACCESS_TOKEN=YOUR LIGHTSTEP ACCESS TOKEN
    export LS_STREAM_ID=YOUR LIGHTSTEP STREAM ID
    export LS_API_KEY=YOUR LIGHTSTEP API KEY
    export LS_ORG_ID=YOUR LIGHTSTEP ORG ID
    export LS_PROJECT_ID=YOUR LIGHTSTEP PROJECT ID
    ```

1. Update the Lightstep configmap

    ```yaml
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
          lightstep-streams/mystream: 
            organization: "${LS_ORG_ID}" 
            project: "${LS_PROJECT_ID}" 
            api_key: "${LS_API_KEY}"
            window_size: 5m 
            stream_id: "${LS_STREAM_ID}"
        processors:
          resourcedetection/azure:
            detectors: [env, azure]
            timeout: 2s
            override: false
        exporters:
          otlp:
            endpoint: ingest.lightstep.com:443
            headers: 
              "lightstep-access-token": "${LS_ACCESS_TOKEN}"
          logging:
            loglevel: debug
          service: 
            scraper: 
              endpoint: 0.0.0.0:55688 
        service:
          pipelines:
            traces:
              receivers: [otlp]
              processors: [resourcedetection/azure]
              exporters: [logging,otlp]
            traces/sgc:
              receivers: [lightstep-streams/mystream]
              processors: []
              exporters: [logging,service]
    EOF
    ```

### Update Helm Chart

1. Sign In to [GitHub]({{site.data.urls.github}})

1. Select the Boutique Project (e.g. `cassandra`) you configured earlier.

1. Locate the `helm/templates/kubernetes-manifests.yaml` file

1. Locate the Deployment section for the `otelcollector`

1. Un-Comment the `image` section as follows:

    ```yaml
    # image: otel/opentelemetry-collector-contrib:0.49.0 
    image: ghcr.io/lightstep/lightstep-partner-toolkit-collector:latest
    ```

1. Expose Port `55688`

    ```yaml
    ports:
      - containerPort: 55688 # Add this entry
    ```

1. Locate the Service section for the `otelcollector`

1. Expose Port `55688`

    ```yaml
    # Add this section
    - name: "55688"
      port: 55688
      targetPort: 55688
    ```

1. Locate the Service section for the `otelcollector-external`  

1. Un-Comment the Service as follows:

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: otelcollector-external
    spec:
      type: LoadBalancer
      selector:
        app: otelcollector
      ports:
      - name: "55688"
        port: 55688
        targetPort: 55688
    ```

1. Commit changes

## Deploy Helm Chart

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
### Check OTEL Collector Deployment

1. Start a Bash Shell

1. Start a Bash Shell

{% include pages/login_to_aks.md %}

1. Retrieve the `otelcollector-external` service EXTERNAL-IP

    ```
    kubectl get service otelcollector-external -n cassandra
    ```

1. Browse to the `http://EXTERNAL-IP:55688` to view the OTEL Collector JSON

    ![Otel Json]({{ site.baseurl }}/assets/images/otel_json.png)

## Configure the Lightstep Service Graph Connector

1. Login to your SN Instance as Administrator

1. Navigate to the **SG Connector for Observability Lightstep > Setup**

1. Configure the **Setup > Set your Organization and Project** Task fields as follows:

    | Field | Value |
    |-------|-------|
    | u_lightstep_project  | YOUR LIGHTSTEP PROJECT ID |
    | u_lightstep_organization | YOUR LIGHTSTEP ORG ID |

1. Configure the **Setup > Set your API Key** Task fields as follows:

    | Field | Value |
    |-------|-------|
    | Name  | Some memorable name (e.g. `srecon22`) |
    | srecon22 | YOUR LIGHTSTEP API KEY |

1. Configure the **Setup > Configure OpenTelemetry** Task fields as follows:

    | Field | Value |
    |-------|-------|
    | Host  | YOUR OTEL COLLECTOR EXTERNAL-IP |
    | Override default port | `55688` |   
    | Protocol | `http` | 

1. Configure the **Setup > Test the Connection** to test connection.

1. Configure the **Setup > Set up Scheduled Import Jobs** Task fields as follows:

    ![Lightstep Jobs]({{ site.baseurl }}/assets/images/lightstep_jobs.png)

    >NOTE: Set all Jobs `Active=True`

1. Navigate to the **SG Connector for Observability Lightstep > Scheduled Data Imports**

1. Select the `SG-OpenTelemetry Resources Scheduled Import` Job. 

1. Manually trigger the Job by pressing the `Execute Now` buton.

## View Services & Relationships

1. Login to your SN Instance as Administrator

1. Navigate to the **SG Connector for Observability Lightstep > Lightstep Services**

1. Click on `View map` for your Lightstep Project (e.g. `LS-servicenow-dev-e95fa366`)

    ![SGC Services 1`]({{ site.baseurl }}/assets/images/sgc_services_1.png)

1. Right-Click on the `LS-frontend` service and select `Open in Dependency Views`.

    ![SGC Services 2`]({{ site.baseurl }}/assets/images/sgc_services_2.png)