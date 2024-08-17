# Helm Chart For Victoria Metrics Agent.

![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)  ![Version: 0.10.14](https://img.shields.io/badge/Version-0.10.14-informational?style=flat-square)
[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/victoriametrics)](https://artifacthub.io/packages/helm/victoriametrics/victoria-metrics-agent)
[![Slack](https://img.shields.io/badge/join%20slack-%23victoriametrics-brightgreen.svg)](https://slack.victoriametrics.com/)

Victoria Metrics Agent - collects metrics from various sources and stores them to VictoriaMetrics

## Prerequisites

* Install the follow packages: ``git``, ``kubectl``, ``helm``, ``helm-docs``. See this [tutorial](../../REQUIREMENTS.md).

## How to install

Access a Kubernetes cluster.

Add a chart helm repository with follow commands:

```console
helm repo add vm https://victoriametrics.github.io/helm-charts/

helm repo update
```

List versions of ``vm/victoria-metrics-agent`` chart available to installation:

```console
helm search repo vm/victoria-metrics-agent -l
```

Export default values of ``victoria-metrics-agent`` chart to file ``values.yaml``:

```console
helm show values vm/victoria-metrics-agent > values.yaml
```

Change the values according to the need of the environment in ``values.yaml`` file.

Test the installation with command:

```console
helm install vmagent vm/victoria-metrics-agent -f values.yaml -n NAMESPACE --debug --dry-run
```

Install chart with command:

```console
helm install vmagent vm/victoria-metrics-agent -f values.yaml -n NAMESPACE
```

Get the pods lists by running this commands:

```console
kubectl get pods -A | grep 'agent'
```

Get the application by running this command:

```console
helm list -f vmagent -n NAMESPACE
```

See the history of versions of ``vmagent`` application with command.

```console
helm history vmagent -n NAMESPACE
```

## How to uninstall

Remove application with command.

```console
helm uninstall vmagent -n NAMESPACE
```

## Documentation of Helm Chart

Install ``helm-docs`` following the instructions on this [tutorial](../../REQUIREMENTS.md).

Generate docs with ``helm-docs`` command.

```bash
cd charts/victoria-metrics-agent

helm-docs
```

The markdown generation is entirely go template driven. The tool parses metadata from charts and generates a number of sub-templates that can be referenced in a template file (by default ``README.md.gotmpl``). If no template file is provided, the tool has a default internal template that will generate a reasonably formatted README.

## Parameters

The following tables lists the configurable parameters of the chart and their default values.

Change the values according to the need of the environment in ``victoria-metrics-agent/values.yaml`` file.

<table>
	<thead>
		<th>Key</th>
		<th>Type</th>
		<th>Default</th>
		<th>Description</th>
	</thead>
	<tbody>
		<tr>
			<td>affinity</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.global.scrape_interval</td>
			<td>string</td>
			<td><pre lang="">
10s
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[0].job_name</td>
			<td>string</td>
			<td><pre lang="">
vmagent
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[0].static_configs[0].targets[0]</td>
			<td>string</td>
			<td><pre lang="">
localhost:8429
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[1].bearer_token_file</td>
			<td>string</td>
			<td><pre lang="">
/var/run/secrets/kubernetes.io/serviceaccount/token
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[1].job_name</td>
			<td>string</td>
			<td><pre lang="">
kubernetes-apiservers
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[1].kubernetes_sd_configs[0].role</td>
			<td>string</td>
			<td><pre lang="">
endpoints
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[1].relabel_configs[0].action</td>
			<td>string</td>
			<td><pre lang="">
keep
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[1].relabel_configs[0].regex</td>
			<td>string</td>
			<td><pre lang="">
default;kubernetes;https
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[1].relabel_configs[0].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_namespace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[1].relabel_configs[0].source_labels[1]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[1].relabel_configs[0].source_labels[2]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_endpoint_port_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[1].scheme</td>
			<td>string</td>
			<td><pre lang="">
https
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[1].tls_config.ca_file</td>
			<td>string</td>
			<td><pre lang="">
/var/run/secrets/kubernetes.io/serviceaccount/ca.crt
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[1].tls_config.insecure_skip_verify</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[2].bearer_token_file</td>
			<td>string</td>
			<td><pre lang="">
/var/run/secrets/kubernetes.io/serviceaccount/token
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[2].job_name</td>
			<td>string</td>
			<td><pre lang="">
kubernetes-nodes
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[2].kubernetes_sd_configs[0].role</td>
			<td>string</td>
			<td><pre lang="">
node
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[2].relabel_configs[0].action</td>
			<td>string</td>
			<td><pre lang="">
labelmap
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[2].relabel_configs[0].regex</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_node_label_(.+)
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[2].relabel_configs[1].replacement</td>
			<td>string</td>
			<td><pre lang="">
kubernetes.default.svc:443
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[2].relabel_configs[1].target_label</td>
			<td>string</td>
			<td><pre lang="">
__address__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[2].relabel_configs[2].regex</td>
			<td>string</td>
			<td><pre lang="">
(.+)
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[2].relabel_configs[2].replacement</td>
			<td>string</td>
			<td><pre lang="">
/api/v1/nodes/$1/proxy/metrics
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[2].relabel_configs[2].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_node_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[2].relabel_configs[2].target_label</td>
			<td>string</td>
			<td><pre lang="">
__metrics_path__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[2].scheme</td>
			<td>string</td>
			<td><pre lang="">
https
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[2].tls_config.ca_file</td>
			<td>string</td>
			<td><pre lang="">
/var/run/secrets/kubernetes.io/serviceaccount/ca.crt
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[2].tls_config.insecure_skip_verify</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[3].bearer_token_file</td>
			<td>string</td>
			<td><pre lang="">
/var/run/secrets/kubernetes.io/serviceaccount/token
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[3].honor_timestamps</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[3].job_name</td>
			<td>string</td>
			<td><pre lang="">
kubernetes-nodes-cadvisor
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[3].kubernetes_sd_configs[0].role</td>
			<td>string</td>
			<td><pre lang="">
node
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[3].relabel_configs[0].action</td>
			<td>string</td>
			<td><pre lang="">
labelmap
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[3].relabel_configs[0].regex</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_node_label_(.+)
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[3].relabel_configs[1].replacement</td>
			<td>string</td>
			<td><pre lang="">
kubernetes.default.svc:443
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[3].relabel_configs[1].target_label</td>
			<td>string</td>
			<td><pre lang="">
__address__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[3].relabel_configs[2].regex</td>
			<td>string</td>
			<td><pre lang="">
(.+)
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[3].relabel_configs[2].replacement</td>
			<td>string</td>
			<td><pre lang="">
/api/v1/nodes/$1/proxy/metrics/cadvisor
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[3].relabel_configs[2].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_node_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[3].relabel_configs[2].target_label</td>
			<td>string</td>
			<td><pre lang="">
__metrics_path__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[3].scheme</td>
			<td>string</td>
			<td><pre lang="">
https
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[3].tls_config.ca_file</td>
			<td>string</td>
			<td><pre lang="">
/var/run/secrets/kubernetes.io/serviceaccount/ca.crt
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[3].tls_config.insecure_skip_verify</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].job_name</td>
			<td>string</td>
			<td><pre lang="">
kubernetes-service-endpoints
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].kubernetes_sd_configs[0].role</td>
			<td>string</td>
			<td><pre lang="">
endpointslices
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[0].action</td>
			<td>string</td>
			<td><pre lang="">
drop
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[0].regex</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[0].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_container_init
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[10].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[10].target_label</td>
			<td>string</td>
			<td><pre lang="">
service
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[11].replacement</td>
			<td>string</td>
			<td><pre lang="">
${1}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[11].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[11].target_label</td>
			<td>string</td>
			<td><pre lang="">
job
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[12].action</td>
			<td>string</td>
			<td><pre lang="">
replace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[12].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_node_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[12].target_label</td>
			<td>string</td>
			<td><pre lang="">
node
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[1].action</td>
			<td>string</td>
			<td><pre lang="">
keep_if_equal
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[1].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_annotation_prometheus_io_port
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[1].source_labels[1]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_container_port_number
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[2].action</td>
			<td>string</td>
			<td><pre lang="">
keep
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[2].regex</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[2].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_annotation_prometheus_io_scrape
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[3].action</td>
			<td>string</td>
			<td><pre lang="">
replace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[3].regex</td>
			<td>string</td>
			<td><pre lang="">
(https?)
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[3].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_annotation_prometheus_io_scheme
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[3].target_label</td>
			<td>string</td>
			<td><pre lang="">
__scheme__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[4].action</td>
			<td>string</td>
			<td><pre lang="">
replace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[4].regex</td>
			<td>string</td>
			<td><pre lang="">
(.+)
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[4].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_annotation_prometheus_io_path
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[4].target_label</td>
			<td>string</td>
			<td><pre lang="">
__metrics_path__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[5].action</td>
			<td>string</td>
			<td><pre lang="">
replace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[5].regex</td>
			<td>string</td>
			<td><pre lang="">
([^:]+)(?::\d+)?;(\d+)
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[5].replacement</td>
			<td>string</td>
			<td><pre lang="">
$1:$2
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[5].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__address__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[5].source_labels[1]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_annotation_prometheus_io_port
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[5].target_label</td>
			<td>string</td>
			<td><pre lang="">
__address__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[6].action</td>
			<td>string</td>
			<td><pre lang="">
labelmap
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[6].regex</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_label_(.+)
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[7].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[7].target_label</td>
			<td>string</td>
			<td><pre lang="">
pod
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[8].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_container_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[8].target_label</td>
			<td>string</td>
			<td><pre lang="">
container
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[9].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_namespace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[4].relabel_configs[9].target_label</td>
			<td>string</td>
			<td><pre lang="">
namespace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].job_name</td>
			<td>string</td>
			<td><pre lang="">
kubernetes-service-endpoints-slow
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].kubernetes_sd_configs[0].role</td>
			<td>string</td>
			<td><pre lang="">
endpointslices
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[0].action</td>
			<td>string</td>
			<td><pre lang="">
drop
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[0].regex</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[0].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_container_init
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[10].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[10].target_label</td>
			<td>string</td>
			<td><pre lang="">
service
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[11].replacement</td>
			<td>string</td>
			<td><pre lang="">
${1}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[11].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[11].target_label</td>
			<td>string</td>
			<td><pre lang="">
job
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[12].action</td>
			<td>string</td>
			<td><pre lang="">
replace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[12].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_node_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[12].target_label</td>
			<td>string</td>
			<td><pre lang="">
node
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[1].action</td>
			<td>string</td>
			<td><pre lang="">
keep_if_equal
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[1].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_annotation_prometheus_io_port
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[1].source_labels[1]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_container_port_number
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[2].action</td>
			<td>string</td>
			<td><pre lang="">
keep
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[2].regex</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[2].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_annotation_prometheus_io_scrape_slow
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[3].action</td>
			<td>string</td>
			<td><pre lang="">
replace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[3].regex</td>
			<td>string</td>
			<td><pre lang="">
(https?)
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[3].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_annotation_prometheus_io_scheme
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[3].target_label</td>
			<td>string</td>
			<td><pre lang="">
__scheme__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[4].action</td>
			<td>string</td>
			<td><pre lang="">
replace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[4].regex</td>
			<td>string</td>
			<td><pre lang="">
(.+)
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[4].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_annotation_prometheus_io_path
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[4].target_label</td>
			<td>string</td>
			<td><pre lang="">
__metrics_path__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[5].action</td>
			<td>string</td>
			<td><pre lang="">
replace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[5].regex</td>
			<td>string</td>
			<td><pre lang="">
([^:]+)(?::\d+)?;(\d+)
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[5].replacement</td>
			<td>string</td>
			<td><pre lang="">
$1:$2
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[5].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__address__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[5].source_labels[1]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_annotation_prometheus_io_port
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[5].target_label</td>
			<td>string</td>
			<td><pre lang="">
__address__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[6].action</td>
			<td>string</td>
			<td><pre lang="">
labelmap
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[6].regex</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_label_(.+)
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[7].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[7].target_label</td>
			<td>string</td>
			<td><pre lang="">
pod
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[8].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_container_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[8].target_label</td>
			<td>string</td>
			<td><pre lang="">
container
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[9].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_namespace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].relabel_configs[9].target_label</td>
			<td>string</td>
			<td><pre lang="">
namespace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].scrape_interval</td>
			<td>string</td>
			<td><pre lang="">
5m
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[5].scrape_timeout</td>
			<td>string</td>
			<td><pre lang="">
30s
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].job_name</td>
			<td>string</td>
			<td><pre lang="">
kubernetes-services
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].kubernetes_sd_configs[0].role</td>
			<td>string</td>
			<td><pre lang="">
service
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].metrics_path</td>
			<td>string</td>
			<td><pre lang="">
/probe
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].params.module[0]</td>
			<td>string</td>
			<td><pre lang="">
http_2xx
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].relabel_configs[0].action</td>
			<td>string</td>
			<td><pre lang="">
keep
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].relabel_configs[0].regex</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].relabel_configs[0].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_annotation_prometheus_io_probe
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].relabel_configs[1].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__address__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].relabel_configs[1].target_label</td>
			<td>string</td>
			<td><pre lang="">
__param_target
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].relabel_configs[2].replacement</td>
			<td>string</td>
			<td><pre lang="">
blackbox
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].relabel_configs[2].target_label</td>
			<td>string</td>
			<td><pre lang="">
__address__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].relabel_configs[3].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__param_target
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].relabel_configs[3].target_label</td>
			<td>string</td>
			<td><pre lang="">
instance
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].relabel_configs[4].action</td>
			<td>string</td>
			<td><pre lang="">
labelmap
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].relabel_configs[4].regex</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_label_(.+)
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].relabel_configs[5].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_namespace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].relabel_configs[5].target_label</td>
			<td>string</td>
			<td><pre lang="">
namespace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].relabel_configs[6].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_service_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[6].relabel_configs[6].target_label</td>
			<td>string</td>
			<td><pre lang="">
service
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].job_name</td>
			<td>string</td>
			<td><pre lang="">
kubernetes-pods
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].kubernetes_sd_configs[0].role</td>
			<td>string</td>
			<td><pre lang="">
pod
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[0].action</td>
			<td>string</td>
			<td><pre lang="">
drop
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[0].regex</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[0].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_container_init
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[1].action</td>
			<td>string</td>
			<td><pre lang="">
keep_if_equal
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[1].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_annotation_prometheus_io_port
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[1].source_labels[1]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_container_port_number
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[2].action</td>
			<td>string</td>
			<td><pre lang="">
keep
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[2].regex</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[2].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_annotation_prometheus_io_scrape
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[3].action</td>
			<td>string</td>
			<td><pre lang="">
replace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[3].regex</td>
			<td>string</td>
			<td><pre lang="">
(.+)
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[3].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_annotation_prometheus_io_path
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[3].target_label</td>
			<td>string</td>
			<td><pre lang="">
__metrics_path__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[4].action</td>
			<td>string</td>
			<td><pre lang="">
replace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[4].regex</td>
			<td>string</td>
			<td><pre lang="">
([^:]+)(?::\d+)?;(\d+)
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[4].replacement</td>
			<td>string</td>
			<td><pre lang="">
$1:$2
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[4].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__address__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[4].source_labels[1]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_annotation_prometheus_io_port
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[4].target_label</td>
			<td>string</td>
			<td><pre lang="">
__address__
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[5].action</td>
			<td>string</td>
			<td><pre lang="">
labelmap
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[5].regex</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_label_(.+)
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[6].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[6].target_label</td>
			<td>string</td>
			<td><pre lang="">
pod
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[7].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_container_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[7].target_label</td>
			<td>string</td>
			<td><pre lang="">
container
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[8].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_namespace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[8].target_label</td>
			<td>string</td>
			<td><pre lang="">
namespace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[9].action</td>
			<td>string</td>
			<td><pre lang="">
replace
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[9].source_labels[0]</td>
			<td>string</td>
			<td><pre lang="">
__meta_kubernetes_pod_node_name
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>config.scrape_configs[7].relabel_configs[9].target_label</td>
			<td>string</td>
			<td><pre lang="">
node
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>configMap</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>containerWorkingDir</td>
			<td>string</td>
			<td><pre lang="">
/
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>deployment.enabled</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>deployment.strategy</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>env</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Additional environment variables (ex.: secret tokens, flags) https://docs.victoriametrics.com/#environment-variables</td>
		</tr>
		<tr>
			<td>envFrom</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>extraArgs."envflag.enable"</td>
			<td>string</td>
			<td><pre lang="">
"true"
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>extraArgs."envflag.prefix"</td>
			<td>string</td>
			<td><pre lang="">
VM_
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>extraArgs.loggerFormat</td>
			<td>string</td>
			<td><pre lang="">
json
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>extraContainers</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>extraHostPathMounts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>extraObjects</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>extraScrapeConfigs</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Extra scrape configs that will be appended to `config`</td>
		</tr>
		<tr>
			<td>extraVolumeMounts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>extraVolumes</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>fullnameOverride</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>global.compatibility.openshift.adaptSecurityContext</td>
			<td>string</td>
			<td><pre lang="">
auto
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>horizontalPodAutoscaling</td>
			<td>object</td>
			<td><pre lang="plaintext">
enabled: false
maxReplicas: 10
metrics: []
minReplicas: 1
</pre>
</td>
			<td>Horizontal Pod Autoscaling. Note that it is not intended to be used for vmagents which perform scraping. In order to scale scraping vmagents see: https://docs.victoriametrics.com/vmagent/#scraping-big-number-of-targets</td>
		</tr>
		<tr>
			<td>horizontalPodAutoscaling.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Use HPA for vmagent</td>
		</tr>
		<tr>
			<td>horizontalPodAutoscaling.maxReplicas</td>
			<td>int</td>
			<td><pre lang="">
10
</pre>
</td>
			<td>Maximum replicas for HPA to use to to scale vmagent</td>
		</tr>
		<tr>
			<td>horizontalPodAutoscaling.metrics</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Metric for HPA to use to scale vmagent</td>
		</tr>
		<tr>
			<td>horizontalPodAutoscaling.minReplicas</td>
			<td>int</td>
			<td><pre lang="">
1
</pre>
</td>
			<td>Minimum replicas for HPA to use to scale vmagent</td>
		</tr>
		<tr>
			<td>image.pullPolicy</td>
			<td>string</td>
			<td><pre lang="">
IfNotPresent
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>image.registry</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>image.repository</td>
			<td>string</td>
			<td><pre lang="">
victoriametrics/vmagent
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>image.tag</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>image.variant</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>imagePullSecrets</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>ingress.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>ingress.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>ingress.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>ingress.hosts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>ingress.pathType</td>
			<td>string</td>
			<td><pre lang="">
Prefix
</pre>
</td>
			<td>pathType is only for k8s >= 1.1=</td>
		</tr>
		<tr>
			<td>ingress.tls</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>initContainers</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>license</td>
			<td>object</td>
			<td><pre lang="plaintext">
key: ""
secret:
    key: ""
    name: ""
</pre>
</td>
			<td>Enterprise license key configuration for VictoriaMetrics enterprise. Required only for VictoriaMetrics enterprise. Documentation - https://docs.victoriametrics.com/enterprise.html, for more information, visit https://victoriametrics.com/products/enterprise/ . To request a trial license, go to https://victoriametrics.com/products/enterprise/trial/ Supported starting from VictoriaMetrics v1.94.0</td>
		</tr>
		<tr>
			<td>license.key</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>License key</td>
		</tr>
		<tr>
			<td>license.secret</td>
			<td>object</td>
			<td><pre lang="plaintext">
key: ""
name: ""
</pre>
</td>
			<td>Use existing secret with license key</td>
		</tr>
		<tr>
			<td>license.secret.key</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Key in secret with license key</td>
		</tr>
		<tr>
			<td>license.secret.name</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Existing secret name</td>
		</tr>
		<tr>
			<td>multiTenantUrls</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>nameOverride</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>nodeSelector</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>persistence.accessModes[0]</td>
			<td>string</td>
			<td><pre lang="">
ReadWriteOnce
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>persistence.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>persistence.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>persistence.existingClaim</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>persistence.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>persistence.matchLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Bind Persistent Volume by labels. Must match all labels of targeted PV.</td>
		</tr>
		<tr>
			<td>persistence.size</td>
			<td>string</td>
			<td><pre lang="">
10Gi
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>podAnnotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>podDisruptionBudget.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>podDisruptionBudget.labels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>podLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>podSecurityContext.enabled</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>priorityClassName</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>priority class to be assigned to the pod(s)</td>
		</tr>
		<tr>
			<td>probe.liveness.initialDelaySeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>probe.liveness.periodSeconds</td>
			<td>int</td>
			<td><pre lang="">
15
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>probe.liveness.tcpSocket.port</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.port" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>probe.liveness.timeoutSeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>probe.readiness.httpGet.path</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.http.path" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>probe.readiness.httpGet.port</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.port" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>probe.readiness.httpGet.scheme</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.http.scheme" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>probe.readiness.initialDelaySeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>probe.readiness.periodSeconds</td>
			<td>int</td>
			<td><pre lang="">
15
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>probe.startup</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>rbac.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>rbac.create</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>rbac.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>rbac.namespaced</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>if true and `rbac.enabled`, will deploy a Role/Rolebinding instead of a ClusterRole/ClusterRoleBinding</td>
		</tr>
		<tr>
			<td>remoteWriteUrls</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>replicaCount</td>
			<td>int</td>
			<td><pre lang="">
1
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>resources</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>securityContext.enabled</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>service.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>service.clusterIP</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>service.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>service.externalIPs</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>service.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>service.loadBalancerIP</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>service.loadBalancerSourceRanges</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>service.servicePort</td>
			<td>int</td>
			<td><pre lang="">
8429
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>service.type</td>
			<td>string</td>
			<td><pre lang="">
ClusterIP
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>serviceAccount.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>serviceAccount.create</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>serviceAccount.name</td>
			<td>string</td>
			<td><pre lang="">
null
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>serviceMonitor.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service Monitor annotations</td>
		</tr>
		<tr>
			<td>serviceMonitor.basicAuth</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Basic auth params for Service Monitor</td>
		</tr>
		<tr>
			<td>serviceMonitor.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Enable deployment of Service Monitor for server component. This is Prometheus operator object</td>
		</tr>
		<tr>
			<td>serviceMonitor.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service Monitor labels</td>
		</tr>
		<tr>
			<td>serviceMonitor.metricRelabelings</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Service Monitor metricRelabelings</td>
		</tr>
		<tr>
			<td>serviceMonitor.relabelings</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Service Monitor relabelings</td>
		</tr>
		<tr>
			<td>statefulset.clusterMode</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>create cluster of vmagents. See https://docs.victoriametrics.com/vmagent.html#scraping-big-number-of-targets available since 1.77.2 version https://github.com/VictoriaMetrics/VictoriaMetrics/releases/tag/v1.77.2</td>
		</tr>
		<tr>
			<td>statefulset.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>statefulset.replicationFactor</td>
			<td>int</td>
			<td><pre lang="">
1
</pre>
</td>
			<td>replication factor for vmagent in cluster mode</td>
		</tr>
		<tr>
			<td>statefulset.updateStrategy</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>tolerations</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>topologySpreadConstraints</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
	</tbody>
</table>