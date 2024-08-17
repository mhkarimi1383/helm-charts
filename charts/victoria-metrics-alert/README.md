# Helm Chart For Victoria Metrics Alert.

![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)  ![Version: 0.9.12](https://img.shields.io/badge/Version-0.9.12-informational?style=flat-square)
[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/victoriametrics)](https://artifacthub.io/packages/helm/victoriametrics/victoria-metrics-alert)
[![Slack](https://img.shields.io/badge/join%20slack-%23victoriametrics-brightgreen.svg)](https://slack.victoriametrics.com/)

Victoria Metrics Alert - executes a list of given MetricsQL expressions (rules) and sends alerts to Alert Manager.

## Prerequisites

* Install the follow packages: ``git``, ``kubectl``, ``helm``, ``helm-docs``. See this [tutorial](../../REQUIREMENTS.md).

## How to install

Access a Kubernetes cluster.

Add a chart helm repository with follow commands:

```console
helm repo add vm https://victoriametrics.github.io/helm-charts/

helm repo update
```

List versions of ``vm/victoria-metrics-alert`` chart available to installation:

```console
helm search repo vm/victoria-metrics-alert -l
```

Export default values of ``victoria-metrics-alert`` chart to file ``values.yaml``:

```console
helm show values vm/victoria-metrics-alert > values.yaml
```

Change the values according to the need of the environment in ``values.yaml`` file.

Test the installation with command:

```console
helm install vmalert vm/victoria-metrics-alert -f values.yaml -n NAMESPACE --debug --dry-run
```

Install chart with command:

```console
helm install vmalert vm/victoria-metrics-alert -f values.yaml -n NAMESPACE
```

Get the pods lists by running this commands:

```console
kubectl get pods -A | grep 'alert'
```

Get the application by running this command:

```console
helm list -f vmalert -n NAMESPACE
```

See the history of versions of ``vmalert`` application with command.

```console
helm history vmalert -n NAMESPACE
```

## HA configuration for Alertmanager

There is no option on this chart to set up Alertmanager with [HA mode](https://github.com/prometheus/alertmanager#high-availability).
To enable the HA configuration, you can use:
- [VictoriaMetrics Operator](https://docs.victoriametrics.com/operator/VictoriaMetrics-Operator.html)
- official [Alertmanager Helm chart](https://github.com/prometheus-community/helm-charts/tree/main/charts/alertmanager)

## How to uninstall

Remove application with command.

```console
helm uninstall vmalert -n NAMESPACE
```

## Documentation of Helm Chart

Install ``helm-docs`` following the instructions on this [tutorial](../../REQUIREMENTS.md).

Generate docs with ``helm-docs`` command.

```bash
cd charts/victoria-metrics-alert

helm-docs
```

The markdown generation is entirely go template driven. The tool parses metadata from charts and generates a number of sub-templates that can be referenced in a template file (by default ``README.md.gotmpl``). If no template file is provided, the tool has a default internal template that will generate a reasonably formatted README.

## Parameters

The following tables lists the configurable parameters of the chart and their default values.

Change the values according to the need of the environment in ``victoria-metrics-alert/values.yaml`` file.

<table>
	<thead>
		<th>Key</th>
		<th>Type</th>
		<th>Default</th>
		<th>Description</th>
	</thead>
	<tbody>
		<tr>
			<td>alertmanager.baseURL</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.baseURLPrefix</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.config.global.resolve_timeout</td>
			<td>string</td>
			<td><pre lang="">
5m
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.config.receivers[0].name</td>
			<td>string</td>
			<td><pre lang="">
devnull
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.config.route.group_by[0]</td>
			<td>string</td>
			<td><pre lang="">
alertname
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.config.route.group_interval</td>
			<td>string</td>
			<td><pre lang="">
10s
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.config.route.group_wait</td>
			<td>string</td>
			<td><pre lang="">
30s
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.config.route.receiver</td>
			<td>string</td>
			<td><pre lang="">
devnull
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.config.route.repeat_interval</td>
			<td>string</td>
			<td><pre lang="">
24h
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.configMap</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.emptyDir</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.envFrom</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.extraArgs</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.extraContainers</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.extraHostPathMounts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.extraVolumeMounts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.extraVolumes</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.image</td>
			<td>object</td>
			<td><pre lang="plaintext">
registry: ""
repository: prom/alertmanager
tag: v0.25.0
</pre>
</td>
			<td>alertmanager image configuration</td>
		</tr>
		<tr>
			<td>alertmanager.imagePullSecrets</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.ingress.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.ingress.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.ingress.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.ingress.hosts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.ingress.pathType</td>
			<td>string</td>
			<td><pre lang="">
Prefix
</pre>
</td>
			<td>pathType is only for k8s >= 1.1=</td>
		</tr>
		<tr>
			<td>alertmanager.ingress.tls</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.listenAddress</td>
			<td>string</td>
			<td><pre lang="">
0.0.0.0:9093
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.nodeSelector</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.persistentVolume.accessModes</td>
			<td>list</td>
			<td><pre lang="plaintext">
- ReadWriteOnce
</pre>
</td>
			<td>Array of access modes. Must match those of existing PV or dynamic provisioner. Details are <a href="http://kubernetes.io/docs/user-guide/persistent-volumes/">here</a></td>
		</tr>
		<tr>
			<td>alertmanager.persistentVolume.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Persistant volume annotations</td>
		</tr>
		<tr>
			<td>alertmanager.persistentVolume.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Create/use Persistent Volume Claim for alertmanager component. Empty dir if false</td>
		</tr>
		<tr>
			<td>alertmanager.persistentVolume.existingClaim</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Existing Claim name. If defined, PVC must be created manually before volume will be bound</td>
		</tr>
		<tr>
			<td>alertmanager.persistentVolume.mountPath</td>
			<td>string</td>
			<td><pre lang="">
/data
</pre>
</td>
			<td>Mount path. Alertmanager data Persistent Volume mount root path.</td>
		</tr>
		<tr>
			<td>alertmanager.persistentVolume.size</td>
			<td>string</td>
			<td><pre lang="">
50Mi
</pre>
</td>
			<td>Size of the volume. Better to set the same as resource limit memory property.</td>
		</tr>
		<tr>
			<td>alertmanager.persistentVolume.storageClass</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>StorageClass to use for persistent volume. Requires alertmanager.persistentVolume.enabled: true. If defined, PVC created automatically</td>
		</tr>
		<tr>
			<td>alertmanager.persistentVolume.subPath</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Mount subpath</td>
		</tr>
		<tr>
			<td>alertmanager.podMetadata.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.podMetadata.labels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.podSecurityContext.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.priorityClassName</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.probe.liveness</td>
			<td>object</td>
			<td><pre lang="plaintext">
httpGet:
    path: '{{ ternary "" .baseURLPrefix (empty .baseURLPrefix) }}/-/healthy'
    port: web
</pre>
</td>
			<td>liveness probe</td>
		</tr>
		<tr>
			<td>alertmanager.probe.readiness</td>
			<td>object</td>
			<td><pre lang="plaintext">
httpGet:
    path: '{{ ternary "" .baseURLPrefix (empty .baseURLPrefix) }}/-/ready'
    port: web
</pre>
</td>
			<td>readiness probe</td>
		</tr>
		<tr>
			<td>alertmanager.probe.startup</td>
			<td>object</td>
			<td><pre lang="plaintext">
httpGet:
    path: '{{ ternary "" .baseURLPrefix (empty .baseURLPrefix) }}/-/ready'
    port: web
</pre>
</td>
			<td>startup probe</td>
		</tr>
		<tr>
			<td>alertmanager.resources</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.retention</td>
			<td>string</td>
			<td><pre lang="">
120h
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.securityContext.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.service.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.service.port</td>
			<td>int</td>
			<td><pre lang="">
9093
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.service.type</td>
			<td>string</td>
			<td><pre lang="">
ClusterIP
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.templates</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>alertmanager.tolerations</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
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
			<td>Add extra specs dynamically to this chart</td>
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
			<td></td>
		</tr>
		<tr>
			<td>server.affinity</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.config.alerts.groups</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.configMap</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.datasource.basicAuth</td>
			<td>object</td>
			<td><pre lang="plaintext">
password: ""
username: ""
</pre>
</td>
			<td>Basic auth for datasource</td>
		</tr>
		<tr>
			<td>server.datasource.bearer.token</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Token with Bearer token. You can use one of token or tokenFile. You don't need to add "Bearer" prefix string</td>
		</tr>
		<tr>
			<td>server.datasource.bearer.tokenFile</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Token Auth file with Bearer token. You can use one of token or tokenFile</td>
		</tr>
		<tr>
			<td>server.datasource.url</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.enabled</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.env</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Additional environment variables (ex.: secret tokens, flags) https://docs.victoriametrics.com/#environment-variables</td>
		</tr>
		<tr>
			<td>server.envFrom</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.extraArgs."envflag.enable"</td>
			<td>string</td>
			<td><pre lang="">
"true"
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.extraArgs."envflag.prefix"</td>
			<td>string</td>
			<td><pre lang="">
VM_
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.extraArgs.loggerFormat</td>
			<td>string</td>
			<td><pre lang="">
json
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.extraContainers</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Additional containers to run in the same pod</td>
		</tr>
		<tr>
			<td>server.extraHostPathMounts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Additional hostPath mounts</td>
		</tr>
		<tr>
			<td>server.extraVolumeMounts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Extra Volume Mounts for the container</td>
		</tr>
		<tr>
			<td>server.extraVolumes</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Extra Volumes for the pod</td>
		</tr>
		<tr>
			<td>server.fullnameOverride</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.image</td>
			<td>object</td>
			<td><pre lang="plaintext">
pullPolicy: IfNotPresent
registry: ""
repository: victoriametrics/vmalert
tag: ""
variant: ""
</pre>
</td>
			<td>vmalert image configuration</td>
		</tr>
		<tr>
			<td>server.imagePullSecrets</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.ingress.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.ingress.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.ingress.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.ingress.hosts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.ingress.pathType</td>
			<td>string</td>
			<td><pre lang="">
Prefix
</pre>
</td>
			<td>pathType is only for k8s >= 1.1=</td>
		</tr>
		<tr>
			<td>server.ingress.tls</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.labels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.minReadySeconds</td>
			<td>int</td>
			<td><pre lang="">
0
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.name</td>
			<td>string</td>
			<td><pre lang="">
server
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.nameOverride</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.nodeSelector</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.notifier</td>
			<td>object</td>
			<td><pre lang="plaintext">
alertmanager:
    basicAuth:
        password: ""
        username: ""
    bearer:
        token: ""
        tokenFile: ""
    url: ""
</pre>
</td>
			<td>Notifier to use for alerts. Multiple notifiers can be enabled by using `notifiers` section</td>
		</tr>
		<tr>
			<td>server.notifier.alertmanager.basicAuth</td>
			<td>object</td>
			<td><pre lang="plaintext">
password: ""
username: ""
</pre>
</td>
			<td>Basic auth for alertmanager</td>
		</tr>
		<tr>
			<td>server.notifier.alertmanager.bearer.token</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Token with Bearer token. You can use one of token or tokenFile. You don't need to add "Bearer" prefix string</td>
		</tr>
		<tr>
			<td>server.notifier.alertmanager.bearer.tokenFile</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Token Auth file with Bearer token. You can use one of token or tokenFile</td>
		</tr>
		<tr>
			<td>server.notifiers</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Additional notifiers to use for alerts</td>
		</tr>
		<tr>
			<td>server.podAnnotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.podDisruptionBudget.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.podDisruptionBudget.labels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.podLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.podSecurityContext.enabled</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.priorityClassName</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.probe.liveness</td>
			<td>object</td>
			<td><pre lang="plaintext">
failureThreshold: 3
initialDelaySeconds: 5
periodSeconds: 15
tcpSocket:
    port: '{{ include "vm.probe.port" . }}'
timeoutSeconds: 5
</pre>
</td>
			<td>liveness probe</td>
		</tr>
		<tr>
			<td>server.probe.readiness</td>
			<td>object</td>
			<td><pre lang="plaintext">
failureThreshold: 3
httpGet:
    path: '{{ include "vm.probe.http.path" . }}'
    port: '{{ include "vm.probe.port" . }}'
    scheme: '{{ include "vm.probe.http.scheme" . }}'
initialDelaySeconds: 5
periodSeconds: 15
timeoutSeconds: 5
</pre>
</td>
			<td>readiness probe</td>
		</tr>
		<tr>
			<td>server.probe.startup</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>startup probe</td>
		</tr>
		<tr>
			<td>server.remote.read.basicAuth</td>
			<td>object</td>
			<td><pre lang="plaintext">
password: ""
username: ""
</pre>
</td>
			<td>Basic auth for remote read</td>
		</tr>
		<tr>
			<td>server.remote.read.bearer.token</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Token with Bearer token. You can use one of token or tokenFile. You don't need to add "Bearer" prefix string</td>
		</tr>
		<tr>
			<td>server.remote.read.bearer.tokenFile</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Token Auth file with Bearer token. You can use one of token or tokenFile</td>
		</tr>
		<tr>
			<td>server.remote.read.url</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.remote.write.basicAuth</td>
			<td>object</td>
			<td><pre lang="plaintext">
password: ""
username: ""
</pre>
</td>
			<td>Basic auth for remote write</td>
		</tr>
		<tr>
			<td>server.remote.write.bearer</td>
			<td>object</td>
			<td><pre lang="plaintext">
token: ""
tokenFile: ""
</pre>
</td>
			<td>Auth based on Bearer token for remote write</td>
		</tr>
		<tr>
			<td>server.remote.write.bearer.token</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Token with Bearer token. You can use one of token or tokenFile. You don't need to add "Bearer" prefix string</td>
		</tr>
		<tr>
			<td>server.remote.write.bearer.tokenFile</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Token Auth file with Bearer token. You can use one of token or tokenFile</td>
		</tr>
		<tr>
			<td>server.remote.write.url</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.replicaCount</td>
			<td>int</td>
			<td><pre lang="">
1
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.resources</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.securityContext.enabled</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.service.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.service.clusterIP</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.service.externalIPs</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.service.labels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.service.loadBalancerIP</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.service.loadBalancerSourceRanges</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.service.servicePort</td>
			<td>int</td>
			<td><pre lang="">
8880
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.service.type</td>
			<td>string</td>
			<td><pre lang="">
ClusterIP
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.strategy.rollingUpdate.maxSurge</td>
			<td>string</td>
			<td><pre lang="">
25%
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.strategy.rollingUpdate.maxUnavailable</td>
			<td>string</td>
			<td><pre lang="">
25%
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.strategy.type</td>
			<td>string</td>
			<td><pre lang="">
RollingUpdate
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.tolerations</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.verticalPodAutoscaler</td>
			<td>object</td>
			<td><pre lang="plaintext">
enabled: false
</pre>
</td>
			<td>Vertical Pod Autoscaler</td>
		</tr>
		<tr>
			<td>server.verticalPodAutoscaler.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Use VPA for vmalert</td>
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
			<td>serviceAccount.automountToken</td>
			<td>bool</td>
			<td><pre lang="">
true
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
	</tbody>
</table>

