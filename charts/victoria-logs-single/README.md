# Victoria Logs Helm Chart for Single Version

 ![Version: 0.5.4](https://img.shields.io/badge/Version-0.5.4-informational?style=flat-square)
[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/victoriametrics)](https://artifacthub.io/packages/helm/victoriametrics/victoria-logs-single)
[![Slack](https://img.shields.io/badge/join%20slack-%23victoriametrics-brightgreen.svg)](https://slack.victoriametrics.com/)

Victoria Logs Single version - high-performance, cost-effective and scalable logs storage

## Prerequisites

* Install the follow packages: ``git``, ``kubectl``, ``helm``, ``helm-docs``. See this [tutorial](../../REQUIREMENTS.md).

* PV support on underlying infrastructure.

## Chart Details

This chart will do the following:

* Rollout Victoria Logs Single.
* (optional) Rollout [fluentbit](https://fluentbit.io/) to collect logs from pods.

Chart allows to configure logs collection from Kubernetes pods to VictoriaLogs.
In order to do that you need to enable fluentbit:
```yaml
fluent-bit:
  enabled: true
```
By default, fluentbit will forward logs to VictoriaLogs installation deployed by this chart.

## How to install

Access a Kubernetes cluster.

Add a chart helm repository with follow commands:

```console
helm repo add vm https://victoriametrics.github.io/helm-charts/

helm repo update
```

List versions of ``vm/victoria-logs-single`` chart available to installation:

```console
helm search repo vm/victoria-logs-single -l
```

Export default values of ``victoria-logs-single`` chart to file ``values.yaml``:

```console
helm show values vm/victoria-logs-single > values.yaml
```

Change the values according to the need of the environment in ``values.yaml`` file.

Test the installation with command:

```console
helm install vlsingle vm/victoria-logs-single -f values.yaml -n NAMESPACE --debug --dry-run
```

Install chart with command:

```console
helm install vlsingle vm/victoria-logs-single -f values.yaml -n NAMESPACE
```

Get the pods lists by running this commands:

```console
kubectl get pods -A | grep 'single'
```

Get the application by running this command:

```console
helm list -f vlsingle -n NAMESPACE
```

See the history of versions of ``vlsingle`` application with command.

```console
helm history vlsingle -n NAMESPACE
```

## How to uninstall

Remove application with command.

```console
helm uninstall vlsingle -n NAMESPACE
```

## Documentation of Helm Chart

Install ``helm-docs`` following the instructions on this [tutorial](../../REQUIREMENTS.md).

Generate docs with ``helm-docs`` command.

```bash
cd charts/victoria-logs-single

helm-docs
```

The markdown generation is entirely go template driven. The tool parses metadata from charts and generates a number of sub-templates that can be referenced in a template file (by default ``README.md.gotmpl``). If no template file is provided, the tool has a default internal template that will generate a reasonably formatted README.

## Parameters

The following tables lists the configurable parameters of the chart and their default values.

Change the values according to the need of the environment in ``victoria-logs-single/values.yaml`` file.

<table>
	<thead>
		<th>Key</th>
		<th>Type</th>
		<th>Default</th>
		<th>Description</th>
	</thead>
	<tbody>
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
			<td>fluent-bit.config.filters</td>
			<td>string</td>
			<td><pre lang="">
|
    [FILTER]
        Name kubernetes
        Match kube.*
        Merge_Log On
        Keep_Log On
        K8S-Logging.Parser On
        K8S-Logging.Exclude On
    [FILTER]
        Name                nest
        Match               *
        Wildcard            pod_name
        Operation lift
        Nested_under kubernetes
        Add_prefix   kubernetes_
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>fluent-bit.config.outputs</td>
			<td>string</td>
			<td><pre lang="">
|
    [OUTPUT]
        Name http
        Match kube.*
        Host {{ include "victoria-logs.server.fullname" . }}
        port 9428
        compress gzip
        uri /insert/jsonline?_stream_fields=stream,kubernetes_pod_name,kubernetes_container_name,kubernetes_namespace_name&_msg_field=log&_time_field=date
        format json_lines
        json_date_format iso8601
        header AccountID 0
        header ProjectID 0
</pre>
</td>
			<td>Note that Host must be replaced to match your VictoriaLogs service name Default format points to VictoriaLogs service.</td>
		</tr>
		<tr>
			<td>fluent-bit.daemonSetVolumeMounts[0].mountPath</td>
			<td>string</td>
			<td><pre lang="">
/var/log
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>fluent-bit.daemonSetVolumeMounts[0].name</td>
			<td>string</td>
			<td><pre lang="">
varlog
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>fluent-bit.daemonSetVolumeMounts[1].mountPath</td>
			<td>string</td>
			<td><pre lang="">
/var/lib/docker/containers
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>fluent-bit.daemonSetVolumeMounts[1].name</td>
			<td>string</td>
			<td><pre lang="">
varlibdockercontainers
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>fluent-bit.daemonSetVolumeMounts[1].readOnly</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>fluent-bit.daemonSetVolumes[0].hostPath.path</td>
			<td>string</td>
			<td><pre lang="">
/var/log
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>fluent-bit.daemonSetVolumes[0].name</td>
			<td>string</td>
			<td><pre lang="">
varlog
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>fluent-bit.daemonSetVolumes[1].hostPath.path</td>
			<td>string</td>
			<td><pre lang="">
/var/lib/docker/containers
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>fluent-bit.daemonSetVolumes[1].name</td>
			<td>string</td>
			<td><pre lang="">
varlibdockercontainers
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>fluent-bit.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Enable deployment of fluent-bit</td>
		</tr>
		<tr>
			<td>fluent-bit.resources</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
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
			<td>global.nameOverride</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>global.victoriaLogs.server.fullnameOverride</td>
			<td>string</td>
			<td><pre lang="">
null
</pre>
</td>
			<td>Overrides the full name of server component</td>
		</tr>
		<tr>
			<td>global.victoriaLogs.server.name</td>
			<td>string</td>
			<td><pre lang="">
server
</pre>
</td>
			<td>Server container name</td>
		</tr>
		<tr>
			<td>podDisruptionBudget.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>See `kubectl explain poddisruptionbudget.spec` for more. Ref: [https://kubernetes.io/docs/tasks/run-application/configure-pdb/](https://kubernetes.io/docs/tasks/run-application/configure-pdb/)</td>
		</tr>
		<tr>
			<td>podDisruptionBudget.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>printNotes</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td>Print chart notes</td>
		</tr>
		<tr>
			<td>server.affinity</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Pod affinity</td>
		</tr>
		<tr>
			<td>server.containerWorkingDir</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Container workdir</td>
		</tr>
		<tr>
			<td>server.enabled</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td>Enable deployment of server component. Deployed as StatefulSet</td>
		</tr>
		<tr>
			<td>server.env</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Additional environment variables (ex.: secret tokens, flags) https://github.com/VictoriaMetrics/VictoriaMetrics#environment-variables</td>
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
			<td></td>
		</tr>
		<tr>
			<td>server.extraHostPathMounts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Sts/Deploy additional labels</td>
		</tr>
		<tr>
			<td>server.extraVolumeMounts</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.extraVolumes</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.image.pullPolicy</td>
			<td>string</td>
			<td><pre lang="">
IfNotPresent
</pre>
</td>
			<td>Image pull policy</td>
		</tr>
		<tr>
			<td>server.image.registry</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Image registry</td>
		</tr>
		<tr>
			<td>server.image.repository</td>
			<td>string</td>
			<td><pre lang="">
victoriametrics/victoria-logs
</pre>
</td>
			<td>Image repository</td>
		</tr>
		<tr>
			<td>server.image.tag</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Image tag</td>
		</tr>
		<tr>
			<td>server.image.variant</td>
			<td>string</td>
			<td><pre lang="">
victorialogs
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.ingress.annotations</td>
			<td>string</td>
			<td><pre lang="">
null
</pre>
</td>
			<td>Ingress annotations</td>
		</tr>
		<tr>
			<td>server.ingress.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Enable deployment of ingress for server component</td>
		</tr>
		<tr>
			<td>server.ingress.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Ingress extra labels</td>
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
			<td>Array of TLS objects</td>
		</tr>
		<tr>
			<td>server.initContainers</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
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
			<td>Pod's node selector. Ref: [https://kubernetes.io/docs/user-guide/node-selection/](https://kubernetes.io/docs/user-guide/node-selection/)</td>
		</tr>
		<tr>
			<td>server.persistentVolume.accessModes</td>
			<td>list</td>
			<td><pre lang="plaintext">
- ReadWriteOnce
</pre>
</td>
			<td>Array of access modes. Must match those of existing PV or dynamic provisioner. Ref: [http://kubernetes.io/docs/user-guide/persistent-volumes/](http://kubernetes.io/docs/user-guide/persistent-volumes/)</td>
		</tr>
		<tr>
			<td>server.persistentVolume.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Persistant volume annotations</td>
		</tr>
		<tr>
			<td>server.persistentVolume.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Create/use Persistent Volume Claim for server component. Empty dir if false</td>
		</tr>
		<tr>
			<td>server.persistentVolume.existingClaim</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Existing Claim name. If defined, PVC must be created manually before volume will be bound</td>
		</tr>
		<tr>
			<td>server.persistentVolume.matchLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Bind Persistent Volume by labels. Must match all labels of targeted PV.</td>
		</tr>
		<tr>
			<td>server.persistentVolume.mountPath</td>
			<td>string</td>
			<td><pre lang="">
/storage
</pre>
</td>
			<td>Mount path. Server data Persistent Volume mount root path.</td>
		</tr>
		<tr>
			<td>server.persistentVolume.size</td>
			<td>string</td>
			<td><pre lang="">
3Gi
</pre>
</td>
			<td>Size of the volume. Should be calculated based on the logs you send and retention policy you set.</td>
		</tr>
		<tr>
			<td>server.persistentVolume.storageClass</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>StorageClass to use for persistent volume. Requires server.persistentVolume.enabled: true. If defined, PVC created automatically</td>
		</tr>
		<tr>
			<td>server.persistentVolume.subPath</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Mount subpath</td>
		</tr>
		<tr>
			<td>server.podAnnotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Pod's annotations</td>
		</tr>
		<tr>
			<td>server.podLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Pod's additional labels</td>
		</tr>
		<tr>
			<td>server.podManagementPolicy</td>
			<td>string</td>
			<td><pre lang="">
OrderedReady
</pre>
</td>
			<td>Pod's management policy</td>
		</tr>
		<tr>
			<td>server.podSecurityContext</td>
			<td>object</td>
			<td><pre lang="plaintext">
enabled: true
fsGroup: 2000
runAsNonRoot: true
runAsUser: 1000
</pre>
</td>
			<td>Pod's security context. Ref: [https://kubernetes.io/docs/tasks/configure-pod-container/security-context/](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/)</td>
		</tr>
		<tr>
			<td>server.priorityClassName</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Name of Priority Class</td>
		</tr>
		<tr>
			<td>server.probe.liveness.failureThreshold</td>
			<td>int</td>
			<td><pre lang="">
10
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.probe.liveness.initialDelaySeconds</td>
			<td>int</td>
			<td><pre lang="">
30
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.probe.liveness.periodSeconds</td>
			<td>int</td>
			<td><pre lang="">
30
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.probe.liveness.tcpSocket.port</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.port" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.probe.liveness.timeoutSeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.probe.readiness.failureThreshold</td>
			<td>int</td>
			<td><pre lang="">
3
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.probe.readiness.httpGet.path</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.http.path" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.probe.readiness.httpGet.port</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.port" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.probe.readiness.httpGet.scheme</td>
			<td>string</td>
			<td><pre lang="">
'{{ include "vm.probe.http.scheme" . }}'
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.probe.readiness.initialDelaySeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.probe.readiness.periodSeconds</td>
			<td>int</td>
			<td><pre lang="">
15
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.probe.readiness.timeoutSeconds</td>
			<td>int</td>
			<td><pre lang="">
5
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>server.probe.startup</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
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
			<td>Resource object. Ref: [http://kubernetes.io/docs/user-guide/compute-resources/](http://kubernetes.io/docs/user-guide/compute-resources/</td>
		</tr>
		<tr>
			<td>server.retentionPeriod</td>
			<td>int</td>
			<td><pre lang="">
1
</pre>
</td>
			<td>Data retention period in month</td>
		</tr>
		<tr>
			<td>server.securityContext</td>
			<td>object</td>
			<td><pre lang="plaintext">
allowPrivilegeEscalation: false
capabilities:
    drop:
        - ALL
enabled: true
readOnlyRootFilesystem: true
</pre>
</td>
			<td>Security context to be added to server pods</td>
		</tr>
		<tr>
			<td>server.service.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service annotations</td>
		</tr>
		<tr>
			<td>server.service.clusterIP</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Service ClusterIP</td>
		</tr>
		<tr>
			<td>server.service.externalIPs</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Service External IPs. Ref: [https://kubernetes.io/docs/user-guide/services/#external-ips]( https://kubernetes.io/docs/user-guide/services/#external-ips)</td>
		</tr>
		<tr>
			<td>server.service.labels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service labels</td>
		</tr>
		<tr>
			<td>server.service.loadBalancerIP</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Service load balacner IP</td>
		</tr>
		<tr>
			<td>server.service.loadBalancerSourceRanges</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Load balancer source range</td>
		</tr>
		<tr>
			<td>server.service.servicePort</td>
			<td>int</td>
			<td><pre lang="">
9428
</pre>
</td>
			<td>Service port</td>
		</tr>
		<tr>
			<td>server.service.type</td>
			<td>string</td>
			<td><pre lang="">
ClusterIP
</pre>
</td>
			<td>Service type</td>
		</tr>
		<tr>
			<td>server.serviceMonitor.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service Monitor annotations</td>
		</tr>
		<tr>
			<td>server.serviceMonitor.basicAuth</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Basic auth params for Service Monitor</td>
		</tr>
		<tr>
			<td>server.serviceMonitor.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Enable deployment of Service Monitor for server component. This is Prometheus operator object</td>
		</tr>
		<tr>
			<td>server.serviceMonitor.extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Service Monitor labels</td>
		</tr>
		<tr>
			<td>server.serviceMonitor.metricRelabelings</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Service Monitor metricRelabelings</td>
		</tr>
		<tr>
			<td>server.serviceMonitor.relabelings</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Service Monitor relabelings</td>
		</tr>
		<tr>
			<td>server.statefulSet.enabled</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td>Creates statefulset instead of deployment, useful when you want to keep the cache</td>
		</tr>
		<tr>
			<td>server.statefulSet.podManagementPolicy</td>
			<td>string</td>
			<td><pre lang="">
OrderedReady
</pre>
</td>
			<td>Deploy order policy for StatefulSet pods</td>
		</tr>
		<tr>
			<td>server.statefulSet.service.annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Headless service annotations</td>
		</tr>
		<tr>
			<td>server.statefulSet.service.labels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Headless service labels</td>
		</tr>
		<tr>
			<td>server.statefulSet.service.servicePort</td>
			<td>int</td>
			<td><pre lang="">
9428
</pre>
</td>
			<td>Headless service port</td>
		</tr>
		<tr>
			<td>server.terminationGracePeriodSeconds</td>
			<td>int</td>
			<td><pre lang="">
60
</pre>
</td>
			<td>Pod's termination grace period in seconds</td>
		</tr>
		<tr>
			<td>server.tolerations</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Node tolerations for server scheduling to nodes with taints. Ref: [https://kubernetes.io/docs/concepts/configuration/assign-pod-node/](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/)</td>
		</tr>
	</tbody>
</table>
