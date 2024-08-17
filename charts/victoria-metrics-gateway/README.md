# Victoria Metrics Helm Chart for vmgateway

![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)  ![Version: 0.1.64](https://img.shields.io/badge/Version-0.1.64-informational?style=flat-square)
[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/victoriametrics)](https://artifacthub.io/packages/helm/victoriametrics/victoria-metrics-gateway)
[![Slack](https://img.shields.io/badge/join%20slack-%23victoriametrics-brightgreen.svg)](https://slack.victoriametrics.com/)

Victoria Metrics Gateway - Auth & Rate-Limitting proxy for Victoria Metrics

# Table of Content

* [Prerequisites](#prerequisites)
* [Chart Details](#chart-details)
* [How to Install](#how-to-install)
* [How to Uninstall](#how-to-uninstall)
* [How to use JWT signature verification](#how-to-use-jwt-signature-verification)
* [Documentation of Helm Chart](#documentation-of-helm-chart)

## Prerequisites

* Install the follow packages: ``git``, ``kubectl``, ``helm``, ``helm-docs``. See this [tutorial](../../REQUIREMENTS.md).
* PV support on underlying infrastructure

## Chart Details

This chart will do the following:

* Rollout victoria metrics gateway

## How to install

Access a Kubernetes cluster.

Add a chart helm repository with follow commands:

```console
helm repo add vm https://victoriametrics.github.io/helm-charts/

helm repo update
```

List versions of ``vm/victoria-metrics-gateway`` chart available to installation:

```console
helm search repo vm/victoria-metrics-gateway -l
```

Export default values of ``victoria-metrics-gateway`` chart to file ``values.yaml``:

```console
helm show values vm/victoria-metrics-gateway > values.yaml
```

Change the values according to the need of the environment in ``values.yaml`` file.

Test the installation with command:

```console
helm install vmgateway vm/victoria-metrics-gateway -f values.yaml -n NAMESPACE --debug --dry-run
```

Install chart with command:

```console
helm install vmgateway vm/victoria-metrics-gateway -f values.yaml -n NAMESPACE
```

Get the pods lists by running this commands:

```console
kubectl get pods -A | grep 'vmgateway'
```

Get the application by running this command:

```console
helm list -f vmgateway -n NAMESPACE
```

See the history of versions of ``vmgateway`` application with command.

```console
helm history vmgateway -n NAMESPACE
```

## How to uninstall

Remove application with command.

```console
helm uninstall vmgateway -n NAMESPACE
```

# How to use [JWT signature verification](https://docs.victoriametrics.com/vmgateway.html#jwt-signature-verification)

Kubernetes best-practice is to store sensitive configuration parts in secrets. For example, 2 keys will be stored as:
```yaml
apiVersion: v1
data:
  key: "<<KEY_DATA>>"
kind: Secret
metadata:
  name: key1
---
apiVersion: v1
data:
  key: "<<KEY_DATA>>"
kind: Secret
metadata:
  name: key2
```

In order to use those secrets it is needed to:
- mount secrets into pod
- provide flag pointing to secret on disk

Here is an example `values.yml` file configuration to achieve this:
```yaml
auth:
  enable: true

extraVolumes:
  - name: key1
    secret:
      secretName: key1
  - name: key2
    secret:
      secretName: key2

extraVolumeMounts:
  - name: key1
    mountPath: /key1
  - name: key2
    mountPath: /key2

extraArgs:
  envflag.enable: "true"
  envflag.prefix: VM_
  loggerFormat: json
  auth.publicKeyFiles: "/key1/key,/key2/key"
```
Note that in this configuration all secret keys will be mounted and accessible to pod.
Please, refer to [this](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.19/#secretvolumesource-v1-core) doc to see all available secret source options.

## Documentation of Helm Chart

Install ``helm-docs`` following the instructions on this [tutorial](../../REQUIREMENTS.md).

Generate docs with ``helm-docs`` command.

```bash
cd charts/victoria-metrics-gateway

helm-docs
```

The markdown generation is entirely go template driven. The tool parses metadata from charts and generates a number of sub-templates that can be referenced in a template file (by default ``README.md.gotmpl``). If no template file is provided, the tool has a default internal template that will generate a reasonably formatted README.

## Parameters

The following tables lists the configurable parameters of the chart and their default values.

Change the values according to the need of the environment in ``victoria-metrics-gateway/values.yaml`` file.

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
			<td>auth</td>
			<td>object</td>
			<td><pre lang="plaintext">
enable: false
</pre>
</td>
			<td>Access Control configuration. https://docs.victoriametrics.com/vmgateway.html#access-control</td>
		</tr>
		<tr>
			<td>auth.enable</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Enable/Disable access-control</td>
		</tr>
		<tr>
			<td>clusterMode</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Specify to True if the source for rate-limiting, reading and writing as a VictoriaMetrics Cluster. Must be true for rate limiting</td>
		</tr>
		<tr>
			<td>configMap</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Use existing configmap if specified otherwise .config values will be used. Ref: https://victoriametrics.github.io/vmgateway.html</td>
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
			<td>env</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Additional environment variables (ex.: secret tokens, flags) https://github.com/VictoriaMetrics/VictoriaMetrics#environment-variables</td>
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
			<td>should be true and means that you have the legal right to run a vmgateway that can either be a signed contract or an email with confirmation to run the service in a trial period https://victoriametrics.com/legal/esa/</td>
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
			<td>Victoria Metrics gateway Docker registry</td>
		</tr>
		<tr>
			<td>image.repository</td>
			<td>string</td>
			<td><pre lang="">
victoriametrics/vmgateway
</pre>
</td>
			<td>Victoria Metrics gateway Docker repository and image name</td>
		</tr>
		<tr>
			<td>image.tag</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Tag of Docker image override Chart.AppVersion</td>
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
			<td>NodeSelector configurations. Ref: https://kubernetes.io/docs/user-guide/node-selection/</td>
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
			<td>See `kubectl explain poddisruptionbudget.spec` for more. Ref: https://kubernetes.io/docs/tasks/run-application/configure-pdb/</td>
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
			<td>rateLimiter</td>
			<td>object</td>
			<td><pre lang="plaintext">
config: {}
datasource:
    url: ""
enable: false
</pre>
</td>
			<td>Rate limiter configuration. Docs https://docs.victoriametrics.com/vmgateway.html#rate-limiter</td>
		</tr>
		<tr>
			<td>rateLimiter.datasource.url</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Datasource VictoriaMetrics or vmselects. Required. Example http://victoroametrics:8428 or http://vmselect:8481/select/0/prometheus</td>
		</tr>
		<tr>
			<td>rateLimiter.enable</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Enable/Disable rate-limiting</td>
		</tr>
		<tr>
			<td>read.url</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Read endpoint without suffixes, victoriametrics or vmselect. Example http://victoroametrics:8428 or http://vmselect:8481</td>
		</tr>
		<tr>
			<td>replicaCount</td>
			<td>int</td>
			<td><pre lang="">
1
</pre>
</td>
			<td>Number of replicas of vmgateway</td>
		</tr>
		<tr>
			<td>resources</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>We usually recommend not to specify default resources and to leave this as a conscious choice for the user. This also increases chances charts run on environments with little resources, such as Minikube. If you do want to specify resources, uncomment the following lines, adjust them as necessary, and remove the curly braces after 'resources:'.</td>
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
true
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
8431
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
			<td>Annotations to add to the service account</td>
		</tr>
		<tr>
			<td>serviceAccount.create</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td>Specifies whether a service account should be created</td>
		</tr>
		<tr>
			<td>serviceAccount.name</td>
			<td>string</td>
			<td><pre lang="">
null
</pre>
</td>
			<td>The name of the service account to use. If not set and create is true, a name is generated using the fullname template</td>
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
			<td>tolerations</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Tolerations configurations. Ref: https://kubernetes.io/docs/concepts/configuration/assign-pod-node/</td>
		</tr>
		<tr>
			<td>write.url</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Write endpoint without suffixes, victoriametrics or vminsert. Example http://victoroametrics:8428 or http://vminsert:8480</td>
		</tr>
	</tbody>
</table>
