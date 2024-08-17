# Victoria Metrics Helm Chart for vmanomaly

![Version: 1.4.1](https://img.shields.io/badge/Version-1.4.1-informational?style=flat-square)
[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/victoriametrics)](https://artifacthub.io/packages/helm/victoriametrics/victoria-metrics-anomaly)
[![Slack](https://img.shields.io/badge/join%20slack-%23victoriametrics-brightgreen.svg)](https://slack.victoriametrics.com/)
[![GitHub license](https://img.shields.io/github/license/VictoriaMetrics/VictoriaMetrics.svg)](https://github.com/VictoriaMetrics/helm-charts/blob/master/LICENSE)
![Twitter Follow](https://img.shields.io/twitter/follow/VictoriaMetrics?style=social)
![Subreddit subscribers](https://img.shields.io/reddit/subreddit-subscribers/VictoriaMetrics?style=social)

Victoria Metrics Anomaly Detection - a service that continuously scans Victoria Metrics time series and detects unexpected changes within data patterns in real-time.

## Prerequisites

* Install the follow packages: ``git``, ``kubectl``, ``helm``, ``helm-docs``. See this [tutorial](../../REQUIREMENTS.md).

* PV support on underlying infrastructure

## Chart Details

This chart will do the following:

* Rollout victoria metrics anomaly

## How to install

Access a Kubernetes cluster.

Add a chart helm repository with follow commands:

```console
helm repo add vm https://victoriametrics.github.io/helm-charts/

helm repo update
```

List versions of ``vm/victoria-metrics-anomaly`` chart available to installation:

```console
helm search repo vm/victoria-metrics-anomaly -l
```

Export default values of ``victoria-metrics-anomaly`` chart to file ``values.yaml``:

```console
helm show values vm/victoria-metrics-anomaly > values.yaml
```

Change the values according to the need of the environment in ``values.yaml`` file.

Test the installation with command:

```console
helm install vmanomaly vm/victoria-metrics-anomaly -f values.yaml -n NAMESPACE --debug --dry-run
```

Install chart with command:

```console
helm install vmanomaly vm/victoria-metrics-anomaly -f values.yaml -n NAMESPACE
```

Get the pods lists by running this commands:

```console
kubectl get pods -A | grep 'vmanomaly'
```

Get the application by running this command:

```console
helm list -f vmanomaly -n NAMESPACE
```

See the history of versions of ``vmanomaly`` application with command.

```console
helm history vmanomaly -n NAMESPACE
```

## How to uninstall

Remove application with command.

```console
helm uninstall vmanomaly -n NAMESPACE
```

## Documentation of Helm Chart

Install ``helm-docs`` following the instructions on this [tutorial](../../REQUIREMENTS.md).

Generate docs with ``helm-docs`` command.

```bash
cd charts/victoria-metrics-anomaly

helm-docs
```

The markdown generation is entirely go template driven. The tool parses metadata from charts and generates a number of sub-templates that can be referenced in a template file (by default ``README.md.gotmpl``). If no template file is provided, the tool has a default internal template that will generate a reasonably formatted README.

## Parameters

The following tables lists the configurable parameters of the chart and their default values.

For more `vmanomaly` config parameters see https://docs.victoriametrics.com/anomaly-detection/components

Change the values according to the need of the environment in ``victoria-metrics-anomaly/values.yaml`` file.

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
			<td>Affinity configurations</td>
		</tr>
		<tr>
			<td>annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Annotations to be added to the deployment</td>
		</tr>
		<tr>
			<td>config</td>
			<td>object</td>
			<td><pre lang="plaintext">
models: {}
preset: ""
reader:
    class: vm
    datasource_url: ""
    queries: {}
    sampling_period: 1m
    tenant_id: ""
schedulers: {}
writer:
    class: vm
    datasource_url: ""
    tenant_id: ""
</pre>
</td>
			<td>Full <a href="https://docs.victoriametrics.com/anomaly-detection/components/">vmanomaly config section</a></td>
		</tr>
		<tr>
			<td>config.models</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td><a href="https://docs.victoriametrics.com/anomaly-detection/components/models/">Models section</a></td>
		</tr>
		<tr>
			<td>config.preset</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Whether to use preset configuration. If not empty, preset name should be specified.</td>
		</tr>
		<tr>
			<td>config.reader</td>
			<td>object</td>
			<td><pre lang="plaintext">
class: vm
datasource_url: ""
queries: {}
sampling_period: 1m
tenant_id: ""
</pre>
</td>
			<td><a href="https://docs.victoriametrics.com/anomaly-detection/components/reader/">Reader section</a></td>
		</tr>
		<tr>
			<td>config.reader.class</td>
			<td>string</td>
			<td><pre lang="">
vm
</pre>
</td>
			<td>Name of the class needed to enable reading from VictoriaMetrics or Prometheus. VmReader is the default option, if not specified.</td>
		</tr>
		<tr>
			<td>config.reader.datasource_url</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Datasource URL address. Required for example <code>http://single-victoria-metrics-single-server.default.svc.cluster.local:8428</code> or <code>http://cluster-victoria-metrics-cluster-vminsert.default.svc.cluster.local:8480/insert/</code></td>
		</tr>
		<tr>
			<td>config.reader.queries</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Required. PromQL/MetricsQL query to select data in format: QUERY_ALIAS: "QUERY". As accepted by "/query_range?query=%s". See https://docs.victoriametrics.com/anomaly-detection/components/reader/#per-query-parameters for more details.</td>
		</tr>
		<tr>
			<td>config.reader.sampling_period</td>
			<td>string</td>
			<td><pre lang="">
1m
</pre>
</td>
			<td>Frequency of the points returned. Will be converted to <code>/query_range?step=%s</code> param (in seconds). <bold>Required</bold> since 1.9.0.</td>
		</tr>
		<tr>
			<td>config.reader.tenant_id</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>For VictoriaMetrics Cluster version only, tenants are identified by accountID or accountID:projectID. See VictoriaMetrics Cluster multitenancy docs</td>
		</tr>
		<tr>
			<td>config.schedulers</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td><a href="https://docs.victoriametrics.com/anomaly-detection/components/scheduler/">Scheduler section</a></td>
		</tr>
		<tr>
			<td>config.writer</td>
			<td>object</td>
			<td><pre lang="plaintext">
class: vm
datasource_url: ""
tenant_id: ""
</pre>
</td>
			<td><a href="https://docs.victoriametrics.com/anomaly-detection/components/writer/">Writer section</a></td>
		</tr>
		<tr>
			<td>config.writer.class</td>
			<td>string</td>
			<td><pre lang="">
vm
</pre>
</td>
			<td>Name of the class needed to enable writing to VictoriaMetrics or Prometheus. VmWriter is the default option, if not specified.</td>
		</tr>
		<tr>
			<td>config.writer.datasource_url</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Datasource URL address. Required for example <code>http://single-victoria-metrics-single-server.default.svc.cluster.local:8428</code> or <code>http://cluster-victoria-metrics-cluster-vminsert.default.svc.cluster.local:8480/insert/</code></td>
		</tr>
		<tr>
			<td>config.writer.tenant_id</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>For VictoriaMetrics Cluster version only, tenants are identified by accountID or accountID:projectID. See VictoriaMetrics Cluster multitenancy docs</td>
		</tr>
		<tr>
			<td>containerWorkingDir</td>
			<td>string</td>
			<td><pre lang="">
/vmanomaly
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
			<td>Additional environment variables (ex.: secret tokens, flags)</td>
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
			<td>eula</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>should be true and means that you have the legal right to run a vmanomaly that can either be a signed contract or an email with confirmation to run the service in a trial period https://victoriametrics.com/legal/esa/</td>
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
			<td>Additional hostPath mounts</td>
		</tr>
		<tr>
			<td>extraVolumeMounts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Extra Volume Mounts for the container</td>
		</tr>
		<tr>
			<td>extraVolumes</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Extra Volumes for the pod</td>
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
			<td>global.image.registry</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>global.imagePullSecrets</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>image.pullPolicy</td>
			<td>string</td>
			<td><pre lang="">
IfNotPresent
</pre>
</td>
			<td>Pull policy of Docker image</td>
		</tr>
		<tr>
			<td>image.registry</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Victoria Metrics anomaly Docker registry</td>
		</tr>
		<tr>
			<td>image.repository</td>
			<td>string</td>
			<td><pre lang="">
victoriametrics/vmanomaly
</pre>
</td>
			<td>Victoria Metrics anomaly Docker repository and image name</td>
		</tr>
		<tr>
			<td>image.tag</td>
			<td>string</td>
			<td><pre lang="">
v1.15.4
</pre>
</td>
			<td>Tag of Docker image</td>
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
			<td>license</td>
			<td>object</td>
			<td><pre lang="plaintext">
key: ""
secret:
    key: ""
    name: ""
</pre>
</td>
			<td>License key configuration for vmanomaly. See <a href="https://docs.victoriametrics.com/vmanomaly.html#licensing">docs</a> Required starting from v1.5.0.</td>
		</tr>
		<tr>
			<td>license.key</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>License key for vmanomaly</td>
		</tr>
		<tr>
			<td>license.secret</td>
			<td>object</td>
			<td><pre lang="plaintext">
key: ""
name: ""
</pre>
</td>
			<td>Use existing secret with license key for vmanomaly</td>
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
			<td>NodeSelector configurations. Details are <a href="https://kubernetes.io/docs/user-guide/node-selection/">here</a></td>
		</tr>
		<tr>
			<td>persistentVolume</td>
			<td>object</td>
			<td><pre lang="plaintext">
accessModes:
    - ReadWriteOnce
annotations: {}
enabled: false
existingClaim: ""
matchLabels: {}
size: 1Gi
storageClass: ""
</pre>
</td>
			<td>Persistence to store models on disk. Available starting from v1.13.0</td>
		</tr>
		<tr>
			<td>persistentVolume.accessModes</td>
			<td>list</td>
			<td><pre lang="plaintext">
- ReadWriteOnce
</pre>
</td>
			<td>Array of access modes. Must match those of existing PV or dynamic provisioner. Details are <a href="http://kubernetes.io/docs/user-guide/persistent-volumes/">here</a></td>
		</tr>
		<tr>
			<td>persistentVolume.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Persistant volume annotations</td>
		</tr>
		<tr>
			<td>persistentVolume.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Create/use Persistent Volume Claim for models dump.</td>
		</tr>
		<tr>
			<td>persistentVolume.existingClaim</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Existing Claim name. If defined, PVC must be created manually before volume will be bound</td>
		</tr>
		<tr>
			<td>persistentVolume.matchLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Bind Persistent Volume by labels. Must match all labels of targeted PV.</td>
		</tr>
		<tr>
			<td>persistentVolume.size</td>
			<td>string</td>
			<td><pre lang="">
1Gi
</pre>
</td>
			<td>Size of the volume. Should be calculated based on the metrics you send and retention policy you set.</td>
		</tr>
		<tr>
			<td>persistentVolume.storageClass</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>StorageClass to use for persistent volume. Requires server.persistentVolume.enabled: true. If defined, PVC created automatically</td>
		</tr>
		<tr>
			<td>podAnnotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Annotations to be added to pod</td>
		</tr>
		<tr>
			<td>podDisruptionBudget</td>
			<td>object</td>
			<td><pre lang="plaintext">
enabled: false
labels: {}
</pre>
</td>
			<td>See <code>kubectl explain poddisruptionbudget.spec</code> for more. Details are <a href="https://kubernetes.io/docs/tasks/run-application/configure-pdb/">here</a></td>
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
			<td>securityContext.runAsGroup</td>
			<td>int</td>
			<td><pre lang="">
1000
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>securityContext.runAsNonRoot</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>securityContext.runAsUser</td>
			<td>int</td>
			<td><pre lang="">
1000
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
			<td></td>
		</tr>
		<tr>
			<td>serviceMonitor.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>serviceMonitor.extraLabels</td>
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
			<td>Tolerations configurations. Details are <a href="https://kubernetes.io/docs/concepts/configuration/assign-pod-node/">here</a></td>
		</tr>
	</tbody>
</table>

