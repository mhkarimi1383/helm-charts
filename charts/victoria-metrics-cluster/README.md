# Victoria Metrics Helm Chart for Cluster Version

![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)  ![Version: 0.11.23](https://img.shields.io/badge/Version-0.11.23-informational?style=flat-square)
[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/victoriametrics)](https://artifacthub.io/packages/helm/victoriametrics/victoria-metrics-cluster)
[![Slack](https://img.shields.io/badge/join%20slack-%23victoriametrics-brightgreen.svg)](https://slack.victoriametrics.com/)

Victoria Metrics Cluster version - high-performance, cost-effective and scalable TSDB, long-term remote storage for Prometheus

## Prerequisites

* Install the follow packages: ``git``, ``kubectl``, ``helm``, ``helm-docs``. See this [tutorial](../../REQUIREMENTS.md).

* PV support on underlying infrastructure

## Chart Details

Note: this chart installs VictoriaMetrics cluster components such as vminsert, vmselect and vmstorage. It doesn't create or configure metrics scraping. If you are looking for a chart to configure monitoring stack in cluster check out [victoria-metrics-k8s-stack chart](https://github.com/VictoriaMetrics/helm-charts/tree/master/charts/victoria-metrics-k8s-stack#helm-chart-for-victoria-metrics-kubernetes-monitoring-stack).

## How to install

Access a Kubernetes cluster.

Add a chart helm repository with follow commands:

```console
helm repo add vm https://victoriametrics.github.io/helm-charts/

helm repo update
```

List versions of ``vm/victoria-metrics-cluster`` chart available to installation:

```console
helm search repo vm/victoria-metrics-cluster -l
```

Export default values of ``victoria-metrics-cluster`` chart to file ``values.yaml``:

```console
helm show values vm/victoria-metrics-cluster > values.yaml
```

Change the values according to the need of the environment in ``values.yaml`` file.

Test the installation with command:

```console
helm install vmcluster vm/victoria-metrics-cluster -f values.yaml -n NAMESPACE --debug --dry-run
```

Install chart with command:

```console
helm install vmcluster vm/victoria-metrics-cluster -f values.yaml -n NAMESPACE
```

Get the pods lists by running this commands:

```console
kubectl get pods -A | grep 'vminsert\|vmselect\|vmstorage'
```

Get the application by running this command:

```console
helm list -f vmcluster -n NAMESPACE
```

See the history of versions of ``vmcluster`` application with command.

```console
helm history vmcluster -n NAMESPACE
```

## How to uninstall

Remove application with command.

```console
helm uninstall vmcluster -n NAMESPACE
```

## Documentation of Helm Chart

Install ``helm-docs`` following the instructions on this [tutorial](../../REQUIREMENTS.md).

Generate docs with ``helm-docs`` command.

```bash
cd charts/victoria-metrics-cluster

helm-docs
```

The markdown generation is entirely go template driven. The tool parses metadata from charts and generates a number of sub-templates that can be referenced in a template file (by default ``README.md.gotmpl``). If no template file is provided, the tool has a default internal template that will generate a reasonably formatted README.

## Parameters

The following tables lists the configurable parameters of the chart and their default values.

Change the values according to the need of the environment in ``victoria-metrics-cluster/values.yaml`` file.

<table>
	<thead>
		<th>Key</th>
		<th>Type</th>
		<th>Default</th>
		<th>Description</th>
	</thead>
	<tbody>
		<tr>
			<td>clusterDomainSuffix</td>
			<td>string</td>
			<td><pre lang="">
cluster.local
</pre>
</td>
			<td>k8s cluster domain suffix, uses for building storage pods' FQDN. Ref: [https://kubernetes.io/docs/tasks/administer-cluster/dns-custom-nameservers/](https://kubernetes.io/docs/tasks/administer-cluster/dns-custom-nameservers/)</td>
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
			<td>extraSecrets</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
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
			<td>printNotes</td>
			<td>bool</td>
			<td><pre lang="">
true
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
			<td>serviceAccount.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.affinity</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Pod affinity</td>
		</tr>
		<tr>
			<td>vminsert.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.automountServiceAccountToken</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.containerWorkingDir</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Container workdir</td>
		</tr>
		<tr>
			<td>vminsert.enabled</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td>Enable deployment of vminsert component. Deployment is used</td>
		</tr>
		<tr>
			<td>vminsert.env</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Additional environment variables (ex.: secret tokens, flags) https://docs.victoriametrics.com/#environment-variables</td>
		</tr>
		<tr>
			<td>vminsert.envFrom</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.extraArgs."envflag.enable"</td>
			<td>string</td>
			<td><pre lang="">
"true"
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.extraArgs."envflag.prefix"</td>
			<td>string</td>
			<td><pre lang="">
VM_
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.extraArgs.loggerFormat</td>
			<td>string</td>
			<td><pre lang="">
json
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.extraContainers</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.extraVolumeMounts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.extraVolumes</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.fullnameOverride</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Overrides the full name of vminsert component</td>
		</tr>
		<tr>
			<td>vminsert.horizontalPodAutoscaler.behavior</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Behavior settings for scaling by the HPA</td>
		</tr>
		<tr>
			<td>vminsert.horizontalPodAutoscaler.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Use HPA for vminsert component</td>
		</tr>
		<tr>
			<td>vminsert.horizontalPodAutoscaler.maxReplicas</td>
			<td>int</td>
			<td><pre lang="">
10
</pre>
</td>
			<td>Maximum replicas for HPA to use to to scale the vminsert component</td>
		</tr>
		<tr>
			<td>vminsert.horizontalPodAutoscaler.metrics</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Metric for HPA to use to scale the vminsert component</td>
		</tr>
		<tr>
			<td>vminsert.horizontalPodAutoscaler.minReplicas</td>
			<td>int</td>
			<td><pre lang="">
2
</pre>
</td>
			<td>Minimum replicas for HPA to use to scale the vminsert component</td>
		</tr>
		<tr>
			<td>vminsert.image.pullPolicy</td>
			<td>string</td>
			<td><pre lang="">
IfNotPresent
</pre>
</td>
			<td>Image pull policy</td>
		</tr>
		<tr>
			<td>vminsert.image.registry</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Image registry</td>
		</tr>
		<tr>
			<td>vminsert.image.repository</td>
			<td>string</td>
			<td><pre lang="">
victoriametrics/vminsert
</pre>
</td>
			<td>Image repository</td>
		</tr>
		<tr>
			<td>vminsert.image.tag</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Image tag override Chart.AppVersion    </td>
		</tr>
		<tr>
			<td>vminsert.image.variant</td>
			<td>string</td>
			<td><pre lang="">
cluster
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.ingress.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Ingress annotations</td>
		</tr>
		<tr>
			<td>vminsert.ingress.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Enable deployment of ingress for vminsert component</td>
		</tr>
		<tr>
			<td>vminsert.ingress.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.ingress.hosts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Array of host objects</td>
		</tr>
		<tr>
			<td>vminsert.ingress.pathType</td>
			<td>string</td>
			<td><pre lang="">
Prefix
</pre>
</td>
			<td>pathType is only for k8s >= 1.1=</td>
		</tr>
		<tr>
			<td>vminsert.ingress.tls</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Array of TLS objects</td>
		</tr>
		<tr>
			<td>vminsert.initContainers</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.name</td>
			<td>string</td>
			<td><pre lang="">
vminsert
</pre>
</td>
			<td>vminsert container name</td>
		</tr>
		<tr>
			<td>vminsert.nodeSelector</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Pod's node selector. Ref: [https://kubernetes.io/docs/user-guide/node-selection/](https://kubernetes.io/docs/user-guide/node-selection/)</td>
		</tr>
		<tr>
			<td>vminsert.podAnnotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Pod's annotations</td>
		</tr>
		<tr>
			<td>vminsert.podDisruptionBudget.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>See `kubectl explain poddisruptionbudget.spec` for more. Ref: [https://kubernetes.io/docs/tasks/run-application/configure-pdb/](https://kubernetes.io/docs/tasks/run-application/configure-pdb/)</td>
		</tr>
		<tr>
			<td>vminsert.podDisruptionBudget.labels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.podSecurityContext.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.ports.name</td>
			<td>string</td>
			<td><pre lang="">
http
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.priorityClassName</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Name of Priority Class</td>
		</tr>
		<tr>
			<td>vminsert.probe.liveness.failureThreshold</td>
			<td>int</td>
			<td><pre lang="">
3
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.probe.liveness.initialDelaySeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.probe.liveness.periodSeconds</td>
			<td>int</td>
			<td><pre lang="">
15
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.probe.liveness.tcpSocket.port</td>
			<td>string</td>
			<td><pre lang="">
'{{ dig "ports" "name" "http" (.app | dict) }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.probe.liveness.timeoutSeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.probe.readiness.failureThreshold</td>
			<td>int</td>
			<td><pre lang="">
3
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.probe.readiness.httpGet.path</td>
			<td>string</td>
			<td><pre lang="">
'{{ index .app.extraArgs "http.pathPrefix" | default "" | trimSuffix "/" }}/health'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.probe.readiness.httpGet.port</td>
			<td>string</td>
			<td><pre lang="">
'{{ dig "ports" "name" "http" (.app | dict) }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.probe.readiness.httpGet.scheme</td>
			<td>string</td>
			<td><pre lang="">
'{{ ternary "HTTPS" "HTTP" (.app.extraArgs.tls | default false) }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.probe.readiness.initialDelaySeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.probe.readiness.periodSeconds</td>
			<td>int</td>
			<td><pre lang="">
15
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.probe.readiness.timeoutSeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.probe.startup</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.replicaCount</td>
			<td>int</td>
			<td><pre lang="">
2
</pre>
</td>
			<td>Count of vminsert pods</td>
		</tr>
		<tr>
			<td>vminsert.resources</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Resource object</td>
		</tr>
		<tr>
			<td>vminsert.securityContext</td>
			<td>object</td>
			<td><pre lang="plaintext">
enabled: false
</pre>
</td>
			<td>Pod's security context. Ref: [https://kubernetes.io/docs/tasks/configure-pod-container/security-context/](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)</td>
		</tr>
		<tr>
			<td>vminsert.service.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service annotations</td>
		</tr>
		<tr>
			<td>vminsert.service.clusterIP</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Service ClusterIP</td>
		</tr>
		<tr>
			<td>vminsert.service.externalIPs</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Service External IPs. Ref: [https://kubernetes.io/docs/user-guide/services/#external-ips]( https://kubernetes.io/docs/user-guide/services/#external-ips)</td>
		</tr>
		<tr>
			<td>vminsert.service.extraPorts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Extra service ports</td>
		</tr>
		<tr>
			<td>vminsert.service.labels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service labels</td>
		</tr>
		<tr>
			<td>vminsert.service.loadBalancerIP</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Service load balancer IP</td>
		</tr>
		<tr>
			<td>vminsert.service.loadBalancerSourceRanges</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Load balancer source range</td>
		</tr>
		<tr>
			<td>vminsert.service.servicePort</td>
			<td>int</td>
			<td><pre lang="">
8480
</pre>
</td>
			<td>Service port</td>
		</tr>
		<tr>
			<td>vminsert.service.targetPort</td>
			<td>string</td>
			<td><pre lang="">
http
</pre>
</td>
			<td>Target port</td>
		</tr>
		<tr>
			<td>vminsert.service.type</td>
			<td>string</td>
			<td><pre lang="">
ClusterIP
</pre>
</td>
			<td>Service type</td>
		</tr>
		<tr>
			<td>vminsert.service.udp</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Make sure that service is not type "LoadBalancer", as it requires "MixedProtocolLBService" feature gate. ref: https://kubernetes.io/docs/reference/command-line-tools-reference/feature-gates/</td>
		</tr>
		<tr>
			<td>vminsert.serviceMonitor.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service Monitor annotations</td>
		</tr>
		<tr>
			<td>vminsert.serviceMonitor.basicAuth</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Basic auth params for Service Monitor</td>
		</tr>
		<tr>
			<td>vminsert.serviceMonitor.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Enable deployment of Service Monitor for vminsert component. This is Prometheus operator object</td>
		</tr>
		<tr>
			<td>vminsert.serviceMonitor.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service Monitor labels</td>
		</tr>
		<tr>
			<td>vminsert.serviceMonitor.metricRelabelings</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Service Monitor metricRelabelings</td>
		</tr>
		<tr>
			<td>vminsert.serviceMonitor.namespace</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Target namespace of ServiceMonitor manifest</td>
		</tr>
		<tr>
			<td>vminsert.serviceMonitor.relabelings</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Service Monitor relabelings</td>
		</tr>
		<tr>
			<td>vminsert.strategy</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vminsert.suppressStorageFQDNsRender</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Suppress rendering `--storageNode` FQDNs based on `vmstorage.replicaCount` value. If true suppress rendering `--storageNodes`, they can be re-defined in extraArgs</td>
		</tr>
		<tr>
			<td>vminsert.tolerations</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Array of tolerations object. Ref: [https://kubernetes.io/docs/concepts/configuration/assign-pod-node/](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/)</td>
		</tr>
		<tr>
			<td>vminsert.topologySpreadConstraints</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Pod topologySpreadConstraints</td>
		</tr>
		<tr>
			<td>vmselect.affinity</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Pod affinity</td>
		</tr>
		<tr>
			<td>vmselect.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.automountServiceAccountToken</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.cacheMountPath</td>
			<td>string</td>
			<td><pre lang="">
/cache
</pre>
</td>
			<td>Cache root folder</td>
		</tr>
		<tr>
			<td>vmselect.containerWorkingDir</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Container workdir</td>
		</tr>
		<tr>
			<td>vmselect.enabled</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td>Enable deployment of vmselect component. Can be deployed as Deployment(default) or StatefulSet</td>
		</tr>
		<tr>
			<td>vmselect.env</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Additional environment variables (ex.: secret tokens, flags) https://docs.victoriametrics.com/#environment-variables</td>
		</tr>
		<tr>
			<td>vmselect.envFrom</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.extraArgs."envflag.enable"</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.extraArgs."envflag.prefix"</td>
			<td>string</td>
			<td><pre lang="">
VM_
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.extraArgs.loggerFormat</td>
			<td>string</td>
			<td><pre lang="">
json
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.extraContainers</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.extraHostPathMounts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.extraVolumeMounts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.extraVolumes</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.fullnameOverride</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Overrides the full name of vmselect component</td>
		</tr>
		<tr>
			<td>vmselect.horizontalPodAutoscaler.behavior</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Behavior settings for scaling by the HPA</td>
		</tr>
		<tr>
			<td>vmselect.horizontalPodAutoscaler.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Use HPA for vmselect component</td>
		</tr>
		<tr>
			<td>vmselect.horizontalPodAutoscaler.maxReplicas</td>
			<td>int</td>
			<td><pre lang="">
10
</pre>
</td>
			<td>Maximum replicas for HPA to use to to scale the vmselect component</td>
		</tr>
		<tr>
			<td>vmselect.horizontalPodAutoscaler.metrics</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Metric for HPA to use to scale the vmselect component</td>
		</tr>
		<tr>
			<td>vmselect.horizontalPodAutoscaler.minReplicas</td>
			<td>int</td>
			<td><pre lang="">
2
</pre>
</td>
			<td>Minimum replicas for HPA to use to scale the vmselect component</td>
		</tr>
		<tr>
			<td>vmselect.image.pullPolicy</td>
			<td>string</td>
			<td><pre lang="">
IfNotPresent
</pre>
</td>
			<td>Image pull policy</td>
		</tr>
		<tr>
			<td>vmselect.image.registry</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Image registry</td>
		</tr>
		<tr>
			<td>vmselect.image.repository</td>
			<td>string</td>
			<td><pre lang="">
victoriametrics/vmselect
</pre>
</td>
			<td>Image repository</td>
		</tr>
		<tr>
			<td>vmselect.image.tag</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Image tag override Chart.AppVersion</td>
		</tr>
		<tr>
			<td>vmselect.image.variant</td>
			<td>string</td>
			<td><pre lang="">
cluster
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.ingress.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Ingress annotations</td>
		</tr>
		<tr>
			<td>vmselect.ingress.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Enable deployment of ingress for vmselect component</td>
		</tr>
		<tr>
			<td>vmselect.ingress.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.ingress.hosts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Array of host objects</td>
		</tr>
		<tr>
			<td>vmselect.ingress.pathType</td>
			<td>string</td>
			<td><pre lang="">
Prefix
</pre>
</td>
			<td>pathType is only for k8s >= 1.1=</td>
		</tr>
		<tr>
			<td>vmselect.ingress.tls</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Array of TLS objects</td>
		</tr>
		<tr>
			<td>vmselect.initContainers</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.name</td>
			<td>string</td>
			<td><pre lang="">
vmselect
</pre>
</td>
			<td>Vmselect container name</td>
		</tr>
		<tr>
			<td>vmselect.nodeSelector</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Pod's node selector. Ref: [https://kubernetes.io/docs/user-guide/node-selection/](https://kubernetes.io/docs/user-guide/node-selection/)</td>
		</tr>
		<tr>
			<td>vmselect.persistentVolume.accessModes</td>
			<td>list</td>
			<td><pre lang="plaintext">
- ReadWriteOnce
</pre>
</td>
			<td>Array of access mode. Must match those of existing PV or dynamic provisioner. Ref: [http://kubernetes.io/docs/user-guide/persistent-volumes/](http://kubernetes.io/docs/user-guide/persistent-volumes/)</td>
		</tr>
		<tr>
			<td>vmselect.persistentVolume.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Persistent volume annotations</td>
		</tr>
		<tr>
			<td>vmselect.persistentVolume.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Create/use Persistent Volume Claim for vmselect component. Empty dir if false. If true, vmselect will create/use a Persistent Volume Claim</td>
		</tr>
		<tr>
			<td>vmselect.persistentVolume.existingClaim</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Existing Claim name. Requires vmselect.persistentVolume.enabled: true. If defined, PVC must be created manually before volume will be bound</td>
		</tr>
		<tr>
			<td>vmselect.persistentVolume.labels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Persistent volume labels</td>
		</tr>
		<tr>
			<td>vmselect.persistentVolume.size</td>
			<td>string</td>
			<td><pre lang="">
2Gi
</pre>
</td>
			<td>Size of the volume. Better to set the same as resource limit memory property</td>
		</tr>
		<tr>
			<td>vmselect.persistentVolume.subPath</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Mount subpath</td>
		</tr>
		<tr>
			<td>vmselect.podAnnotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Pod's annotations</td>
		</tr>
		<tr>
			<td>vmselect.podDisruptionBudget.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>See `kubectl explain poddisruptionbudget.spec` for more. Ref: https://kubernetes.io/docs/tasks/run-application/configure-pdb/</td>
		</tr>
		<tr>
			<td>vmselect.podDisruptionBudget.labels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.podSecurityContext.enabled</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.ports.name</td>
			<td>string</td>
			<td><pre lang="">
http
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.priorityClassName</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Name of Priority Class</td>
		</tr>
		<tr>
			<td>vmselect.probe.liveness.failureThreshold</td>
			<td>int</td>
			<td><pre lang="">
3
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.probe.liveness.initialDelaySeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.probe.liveness.periodSeconds</td>
			<td>int</td>
			<td><pre lang="">
15
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.probe.liveness.tcpSocket.port</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.port" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.probe.liveness.timeoutSeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.probe.readiness.failureThreshold</td>
			<td>int</td>
			<td><pre lang="">
3
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.probe.readiness.httpGet.path</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.http.path" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.probe.readiness.httpGet.port</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.port" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.probe.readiness.httpGet.scheme</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.http.scheme" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.probe.readiness.initialDelaySeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.probe.readiness.periodSeconds</td>
			<td>int</td>
			<td><pre lang="">
15
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.probe.readiness.timeoutSeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.probe.startup</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.replicaCount</td>
			<td>int</td>
			<td><pre lang="">
2
</pre>
</td>
			<td>Count of vmselect pods</td>
		</tr>
		<tr>
			<td>vmselect.resources</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Resource object</td>
		</tr>
		<tr>
			<td>vmselect.securityContext</td>
			<td>object</td>
			<td><pre lang="plaintext">
enabled: true
</pre>
</td>
			<td>Pod's security context. Ref: [https://kubernetes.io/docs/tasks/configure-pod-container/security-context/](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/</td>
		</tr>
		<tr>
			<td>vmselect.service.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service annotations</td>
		</tr>
		<tr>
			<td>vmselect.service.clusterIP</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Service ClusterIP</td>
		</tr>
		<tr>
			<td>vmselect.service.externalIPs</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Service External IPs. Ref: [https://kubernetes.io/docs/user-guide/services/#external-ips](https://kubernetes.io/docs/user-guide/services/#external-ips)</td>
		</tr>
		<tr>
			<td>vmselect.service.extraPorts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Extra service ports</td>
		</tr>
		<tr>
			<td>vmselect.service.labels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service labels</td>
		</tr>
		<tr>
			<td>vmselect.service.loadBalancerIP</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Service load balacner IP</td>
		</tr>
		<tr>
			<td>vmselect.service.loadBalancerSourceRanges</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Load balancer source range</td>
		</tr>
		<tr>
			<td>vmselect.service.servicePort</td>
			<td>int</td>
			<td><pre lang="">
8481
</pre>
</td>
			<td>Service port</td>
		</tr>
		<tr>
			<td>vmselect.service.targetPort</td>
			<td>string</td>
			<td><pre lang="">
http
</pre>
</td>
			<td>Target port</td>
		</tr>
		<tr>
			<td>vmselect.service.type</td>
			<td>string</td>
			<td><pre lang="">
ClusterIP
</pre>
</td>
			<td>Service type</td>
		</tr>
		<tr>
			<td>vmselect.serviceMonitor.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service Monitor annotations</td>
		</tr>
		<tr>
			<td>vmselect.serviceMonitor.basicAuth</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Basic auth params for Service Monitor</td>
		</tr>
		<tr>
			<td>vmselect.serviceMonitor.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Enable deployment of Service Monitor for vmselect component. This is Prometheus operator object</td>
		</tr>
		<tr>
			<td>vmselect.serviceMonitor.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service Monitor labels</td>
		</tr>
		<tr>
			<td>vmselect.serviceMonitor.metricRelabelings</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Service Monitor metricRelabelings</td>
		</tr>
		<tr>
			<td>vmselect.serviceMonitor.namespace</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Target namespace of ServiceMonitor manifest</td>
		</tr>
		<tr>
			<td>vmselect.serviceMonitor.relabelings</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Service Monitor relabelings</td>
		</tr>
		<tr>
			<td>vmselect.statefulSet.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Deploy StatefulSet instead of Deployment for vmselect. Useful if you want to keep cache data.</td>
		</tr>
		<tr>
			<td>vmselect.statefulSet.podManagementPolicy</td>
			<td>string</td>
			<td><pre lang="">
OrderedReady
</pre>
</td>
			<td>Deploy order policy for StatefulSet pods</td>
		</tr>
		<tr>
			<td>vmselect.statefulSet.service.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Headless service annotations</td>
		</tr>
		<tr>
			<td>vmselect.statefulSet.service.labels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Headless service labels</td>
		</tr>
		<tr>
			<td>vmselect.statefulSet.service.servicePort</td>
			<td>int</td>
			<td><pre lang="">
8481
</pre>
</td>
			<td>Headless service port</td>
		</tr>
		<tr>
			<td>vmselect.strategy</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmselect.suppressStorageFQDNsRender</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Suppress rendering `--storageNode` FQDNs based on `vmstorage.replicaCount` value. If true suppress rendering `--storageNodes`, they can be re-defined in extraArgs</td>
		</tr>
		<tr>
			<td>vmselect.tolerations</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Array of tolerations object. Ref: [https://kubernetes.io/docs/concepts/configuration/assign-pod-node/](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/)</td>
		</tr>
		<tr>
			<td>vmselect.topologySpreadConstraints</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Pod topologySpreadConstraints</td>
		</tr>
		<tr>
			<td>vmstorage.affinity</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Pod affinity</td>
		</tr>
		<tr>
			<td>vmstorage.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.automountServiceAccountToken</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.containerWorkingDir</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Container workdir</td>
		</tr>
		<tr>
			<td>vmstorage.enabled</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td>Enable deployment of vmstorage component. StatefulSet is used</td>
		</tr>
		<tr>
			<td>vmstorage.env</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Additional environment variables (ex.: secret tokens, flags) https://docs.victoriametrics.com/#environment-variables</td>
		</tr>
		<tr>
			<td>vmstorage.envFrom</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.extraArgs."envflag.enable"</td>
			<td>string</td>
			<td><pre lang="">
"true"
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.extraArgs."envflag.prefix"</td>
			<td>string</td>
			<td><pre lang="">
VM_
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.extraArgs.loggerFormat</td>
			<td>string</td>
			<td><pre lang="">
json
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.extraContainers</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.extraHostPathMounts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.extraSecretMounts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.extraVolumeMounts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.extraVolumes</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.fullnameOverride</td>
			<td>string</td>
			<td><pre lang="">
null
</pre>
</td>
			<td>Overrides the full name of vmstorage component</td>
		</tr>
		<tr>
			<td>vmstorage.image.pullPolicy</td>
			<td>string</td>
			<td><pre lang="">
IfNotPresent
</pre>
</td>
			<td>Image pull policy</td>
		</tr>
		<tr>
			<td>vmstorage.image.registry</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Image registry</td>
		</tr>
		<tr>
			<td>vmstorage.image.repository</td>
			<td>string</td>
			<td><pre lang="">
victoriametrics/vmstorage
</pre>
</td>
			<td>Image repository</td>
		</tr>
		<tr>
			<td>vmstorage.image.tag</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Image tag override Chart.AppVersion</td>
		</tr>
		<tr>
			<td>vmstorage.image.variant</td>
			<td>string</td>
			<td><pre lang="">
cluster
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.initContainers</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.name</td>
			<td>string</td>
			<td><pre lang="">
vmstorage
</pre>
</td>
			<td>vmstorage container name</td>
		</tr>
		<tr>
			<td>vmstorage.nodeSelector</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Pod's node selector. Ref: [https://kubernetes.io/docs/user-guide/node-selection/](https://kubernetes.io/docs/user-guide/node-selection/)</td>
		</tr>
		<tr>
			<td>vmstorage.persistentVolume.accessModes</td>
			<td>list</td>
			<td><pre lang="plaintext">
- ReadWriteOnce
</pre>
</td>
			<td>Array of access modes. Must match those of existing PV or dynamic provisioner. Ref: [http://kubernetes.io/docs/user-guide/persistent-volumes/](http://kubernetes.io/docs/user-guide/persistent-volumes/)</td>
		</tr>
		<tr>
			<td>vmstorage.persistentVolume.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Persistent volume annotations</td>
		</tr>
		<tr>
			<td>vmstorage.persistentVolume.enabled</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td>Create/use Persistent Volume Claim for vmstorage component. Empty dir if false. If true,  vmstorage will create/use a Persistent Volume Claim</td>
		</tr>
		<tr>
			<td>vmstorage.persistentVolume.existingClaim</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Existing Claim name. Requires vmstorage.persistentVolume.enabled: true. If defined, PVC must be created manually before volume will be bound</td>
		</tr>
		<tr>
			<td>vmstorage.persistentVolume.labels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Persistent volume labels</td>
		</tr>
		<tr>
			<td>vmstorage.persistentVolume.mountPath</td>
			<td>string</td>
			<td><pre lang="">
/storage
</pre>
</td>
			<td>Data root path. Vmstorage data Persistent Volume mount root path</td>
		</tr>
		<tr>
			<td>vmstorage.persistentVolume.name</td>
			<td>string</td>
			<td><pre lang="">
vmstorage-volume
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.persistentVolume.size</td>
			<td>string</td>
			<td><pre lang="">
8Gi
</pre>
</td>
			<td>Size of the volume.</td>
		</tr>
		<tr>
			<td>vmstorage.persistentVolume.storageClass</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Storage class name. Will be empty if not setted</td>
		</tr>
		<tr>
			<td>vmstorage.persistentVolume.subPath</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Mount subpath</td>
		</tr>
		<tr>
			<td>vmstorage.podAnnotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Pod's annotations</td>
		</tr>
		<tr>
			<td>vmstorage.podDisruptionBudget</td>
			<td>object</td>
			<td><pre lang="plaintext">
enabled: false
labels: {}
</pre>
</td>
			<td>See `kubectl explain poddisruptionbudget.spec` for more. Ref: [https://kubernetes.io/docs/tasks/run-application/configure-pdb/](https://kubernetes.io/docs/tasks/run-application/configure-pdb/)</td>
		</tr>
		<tr>
			<td>vmstorage.podManagementPolicy</td>
			<td>string</td>
			<td><pre lang="">
OrderedReady
</pre>
</td>
			<td>Deploy order policy for StatefulSet pods</td>
		</tr>
		<tr>
			<td>vmstorage.podSecurityContext.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.ports.name</td>
			<td>string</td>
			<td><pre lang="">
http
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.priorityClassName</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Name of Priority Class</td>
		</tr>
		<tr>
			<td>vmstorage.probe.liveness.failureThreshold</td>
			<td>int</td>
			<td><pre lang="">
10
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.probe.liveness.initialDelaySeconds</td>
			<td>int</td>
			<td><pre lang="">
30
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.probe.liveness.periodSeconds</td>
			<td>int</td>
			<td><pre lang="">
30
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.probe.liveness.tcpSocket.port</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.port" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.probe.liveness.timeoutSeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.probe.readiness.failureThreshold</td>
			<td>int</td>
			<td><pre lang="">
3
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.probe.readiness.httpGet.path</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.http.path" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.probe.readiness.httpGet.port</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.port" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.probe.readiness.httpGet.scheme</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.http.scheme" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.probe.readiness.initialDelaySeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.probe.readiness.periodSeconds</td>
			<td>int</td>
			<td><pre lang="">
15
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.probe.readiness.timeoutSeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.probe.startup</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.replicaCount</td>
			<td>int</td>
			<td><pre lang="">
2
</pre>
</td>
			<td>Count of vmstorage pods</td>
		</tr>
		<tr>
			<td>vmstorage.resources</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Resource object. Ref: [https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)</td>
		</tr>
		<tr>
			<td>vmstorage.retentionPeriod</td>
			<td>int</td>
			<td><pre lang="">
1
</pre>
</td>
			<td>Data retention period. Supported values 1w, 1d, number without measurement means month, e.g. 2 = 2month</td>
		</tr>
		<tr>
			<td>vmstorage.securityContext</td>
			<td>object</td>
			<td><pre lang="plaintext">
enabled: false
</pre>
</td>
			<td>Pod's security context. Ref: [https://kubernetes.io/docs/tasks/configure-pod-container/security-context/](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)</td>
		</tr>
		<tr>
			<td>vmstorage.service.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service annotations</td>
		</tr>
		<tr>
			<td>vmstorage.service.extraPorts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Extra service ports</td>
		</tr>
		<tr>
			<td>vmstorage.service.labels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service labels</td>
		</tr>
		<tr>
			<td>vmstorage.service.servicePort</td>
			<td>int</td>
			<td><pre lang="">
8482
</pre>
</td>
			<td>Service port</td>
		</tr>
		<tr>
			<td>vmstorage.service.vminsertPort</td>
			<td>int</td>
			<td><pre lang="">
8400
</pre>
</td>
			<td>Port for accepting connections from vminsert</td>
		</tr>
		<tr>
			<td>vmstorage.service.vmselectPort</td>
			<td>int</td>
			<td><pre lang="">
8401
</pre>
</td>
			<td>Port for accepting connections from vmselect</td>
		</tr>
		<tr>
			<td>vmstorage.serviceMonitor.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service Monitor annotations</td>
		</tr>
		<tr>
			<td>vmstorage.serviceMonitor.basicAuth</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Basic auth params for Service Monitor</td>
		</tr>
		<tr>
			<td>vmstorage.serviceMonitor.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Enable deployment of Service Monitor for vmstorage component. This is Prometheus operator object</td>
		</tr>
		<tr>
			<td>vmstorage.serviceMonitor.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service Monitor labels</td>
		</tr>
		<tr>
			<td>vmstorage.serviceMonitor.metricRelabelings</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Service Monitor metricRelabelings</td>
		</tr>
		<tr>
			<td>vmstorage.serviceMonitor.namespace</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Target namespace of ServiceMonitor manifest</td>
		</tr>
		<tr>
			<td>vmstorage.serviceMonitor.relabelings</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Service Monitor relabelings</td>
		</tr>
		<tr>
			<td>vmstorage.terminationGracePeriodSeconds</td>
			<td>int</td>
			<td><pre lang="">
60
</pre>
</td>
			<td>Pod's termination grace period in seconds</td>
		</tr>
		<tr>
			<td>vmstorage.tolerations</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Array of tolerations object. Node tolerations for server scheduling to nodes with taints. Ref: [https://kubernetes.io/docs/concepts/configuration/assign-pod-node/](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/) #</td>
		</tr>
		<tr>
			<td>vmstorage.topologySpreadConstraints</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Pod topologySpreadConstraints</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.destination</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>backup destination at S3, GCS or local filesystem. Pod name will be included to path!</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.disableDaily</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>disable daily backups</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.disableHourly</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>disable hourly backups</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.disableMonthly</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>disable monthly backups</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.disableWeekly</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>disable weekly backups</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.enable</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>enable automatic creation of backup via vmbackupmanager. vmbackupmanager is part of Enterprise packages</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.env</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Additional environment variables (ex.: secret tokens, flags) https://docs.victoriametrics.com/#environment-variables</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.eula</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>should be true and means that you have the legal right to run a backup manager that can either be a signed contract or an email with confirmation to run the service in a trial period # https://victoriametrics.com/legal/esa/</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.extraArgs."envflag.enable"</td>
			<td>string</td>
			<td><pre lang="">
"true"
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.extraArgs."envflag.prefix"</td>
			<td>string</td>
			<td><pre lang="">
VM_
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.extraArgs.loggerFormat</td>
			<td>string</td>
			<td><pre lang="">
json
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.extraSecretMounts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.image.registry</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>vmbackupmanager image registry</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.image.repository</td>
			<td>string</td>
			<td><pre lang="">
victoriametrics/vmbackupmanager
</pre>
</td>
			<td>vmbackupmanager image repository</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.image.tag</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>vmbackupmanager image tag override Chart.AppVersion</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.image.variant</td>
			<td>string</td>
			<td><pre lang="">
cluster
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.probe.liveness.failureThreshold</td>
			<td>int</td>
			<td><pre lang="">
10
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.probe.liveness.initialDelaySeconds</td>
			<td>int</td>
			<td><pre lang="">
30
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.probe.liveness.periodSeconds</td>
			<td>int</td>
			<td><pre lang="">
30
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.probe.liveness.tcpSocket.port</td>
			<td>string</td>
			<td><pre lang="">
manager-http
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.probe.liveness.timeoutSeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.probe.readiness.failureThreshold</td>
			<td>int</td>
			<td><pre lang="">
3
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.probe.readiness.httpGet.path</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.http.path" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.probe.readiness.httpGet.port</td>
			<td>string</td>
			<td><pre lang="">
manager-http
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.probe.readiness.httpGet.scheme</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.http.scheme" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.probe.readiness.initialDelaySeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.probe.readiness.periodSeconds</td>
			<td>int</td>
			<td><pre lang="">
15
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.probe.readiness.timeoutSeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.probe.startup</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.resources</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.restore</td>
			<td>object</td>
			<td><pre lang="plaintext">
onStart:
    enabled: false
</pre>
</td>
			<td>Allows to enable restore options for pod. Read more: https://docs.victoriametrics.com/vmbackupmanager.html#restore-commands</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.retention</td>
			<td>object</td>
			<td><pre lang="plaintext">
keepLastDaily: 2
keepLastHourly: 2
keepLastMonthly: 2
keepLastWeekly: 2
</pre>
</td>
			<td>backups' retention settings</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.retention.keepLastDaily</td>
			<td>int</td>
			<td><pre lang="">
2
</pre>
</td>
			<td>keep last N daily backups. 0 means delete all existing daily backups. Specify -1 to turn off</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.retention.keepLastHourly</td>
			<td>int</td>
			<td><pre lang="">
2
</pre>
</td>
			<td>keep last N hourly backups. 0 means delete all existing hourly backups. Specify -1 to turn off</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.retention.keepLastMonthly</td>
			<td>int</td>
			<td><pre lang="">
2
</pre>
</td>
			<td>keep last N monthly backups. 0 means delete all existing monthly backups. Specify -1 to turn off</td>
		</tr>
		<tr>
			<td>vmstorage.vmbackupmanager.retention.keepLastWeekly</td>
			<td>int</td>
			<td><pre lang="">
2
</pre>
</td>
			<td>keep last N weekly backups. 0 means delete all existing weekly backups. Specify -1 to turn off</td>
		</tr>
	</tbody>
</table>

