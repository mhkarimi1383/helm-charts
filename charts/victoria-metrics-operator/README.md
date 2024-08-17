# Helm Chart For Victoria Metrics Operator.

![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)  ![Version: 0.34.0](https://img.shields.io/badge/Version-0.34.0-informational?style=flat-square)
[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/victoriametrics)](https://artifacthub.io/packages/helm/victoriametrics/victoria-metrics-operator)

Victoria Metrics Operator

## Prerequisites

* Install the follow packages: ``git``, ``kubectl``, ``helm``, ``helm-docs``. See this [tutorial](../../REQUIREMENTS.md).
* PV support on underlying infrastructure.

## Upgrade guide

 During release an issue with helm CRD was discovered. So for upgrade from version less then 0.1.3 you have to two options:
 1) use helm management for CRD, enabled by default.
 2) use own management system, need to add variable: --set createCRD=false.

If you choose helm management, following steps must be done before upgrade:

1) define namespace and helm release name variables

```
export NAMESPACE=default
export RELEASE_NAME=operator
```

execute kubectl commands:

```
kubectl get crd  | grep victoriametrics.com | awk '{print $1 }' | xargs -i kubectl label crd {} app.kubernetes.io/managed-by=Helm --overwrite
kubectl get crd  | grep victoriametrics.com | awk '{print $1 }' | xargs -i kubectl annotate crd {} meta.helm.sh/release-namespace="$NAMESPACE" meta.helm.sh/release-name="$RELEASE_NAME"  --overwrite
```

run helm upgrade command.

## Chart Details

This chart will do the following:

* Rollout victoria metrics operator

## How to install

Access a Kubernetes cluster.

Add a chart helm repository with follow commands:

```console
helm repo add vm https://victoriametrics.github.io/helm-charts/

helm repo update
```

List versions of ``vm/victoria-metrics-operator`` chart available to installation:

```console
helm search repo vm/victoria-metrics-operator -l
```

Export default values of ``victoria-metrics-operator`` chart to file ``values.yaml``:

```console
helm show values vm/victoria-metrics-operator > values.yaml
```

Change the values according to the need of the environment in ``values.yaml`` file.

Test the installation with command:

```console
helm install vmoperator vm/victoria-metrics-operator -f values.yaml -n NAMESPACE --debug --dry-run
```

Install chart with command:

```console
helm install vmoperator vm/victoria-metrics-operator -f values.yaml -n NAMESPACE
```

Get the pods lists by running this commands:

```console
kubectl get pods -A | grep 'operator'
```

Get the application by running this command:

```console
helm list -f vmoperator -n NAMESPACE
```

See the history of versions of ``vmoperator`` application with command.

```console
helm history vmoperator -n NAMESPACE
```

## How to uninstall

Remove application with command.

```console
helm uninstall vmoperator -n NAMESPACE
```

## Validation webhook

  Its possible to use validation of created resources with operator. For now, you need cert-manager to easily certificate management https://cert-manager.io/docs/

```yaml
admissionWebhooks:
  enabled: true
  # what to do in case, when operator not available to validate request.
  certManager:
    # enables cert creation and injection by cert-manager
    enabled: true
```

## Documentation of Helm Chart

Install ``helm-docs`` following the instructions on this [tutorial](../../REQUIREMENTS.md).

Generate docs with ``helm-docs`` command.

```bash
cd charts/victoria-metrics-operator

helm-docs
```

The markdown generation is entirely go template driven. The tool parses metadata from charts and generates a number of sub-templates that can be referenced in a template file (by default ``README.md.gotmpl``). If no template file is provided, the tool has a default internal template that will generate a reasonably formatted README.

## Parameters

The following tables lists the configurable parameters of the chart and their default values.

Change the values according to the need of the environment in ``victoria-metrics-operator/values.yaml`` file.

<table>
	<thead>
		<th>Key</th>
		<th>Type</th>
		<th>Default</th>
		<th>Description</th>
	</thead>
	<tbody>
		<tr>
			<td>admissionWebhooks</td>
			<td>object</td>
			<td><pre lang="plaintext">
caBundle: ""
certManager:
    enabled: false
    issuer: {}
enabled: false
enabledCRDValidation:
    vmagent: true
    vmalert: true
    vmalertmanager: true
    vmalertmanagerConfig: true
    vmauth: true
    vmcluster: true
    vmrule: true
    vmsingle: true
    vmuser: true
policy: Fail
</pre>
</td>
			<td>Configures resource validation</td>
		</tr>
		<tr>
			<td>admissionWebhooks.caBundle</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>with keys: tls.key, tls.crt, ca.crt</td>
		</tr>
		<tr>
			<td>admissionWebhooks.certManager.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Enables cert creation and injection by cert-manager.</td>
		</tr>
		<tr>
			<td>admissionWebhooks.certManager.issuer</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>If needed, provide own issuer. Operator will create self-signed if empty.</td>
		</tr>
		<tr>
			<td>admissionWebhooks.enabled</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Enables validation webhook.</td>
		</tr>
		<tr>
			<td>admissionWebhooks.policy</td>
			<td>string</td>
			<td><pre lang="">
Fail
</pre>
</td>
			<td>What to do in case, when operator not available to validate request.</td>
		</tr>
		<tr>
			<td>affinity</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Pod affinity</td>
		</tr>
		<tr>
			<td>annotations</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Annotations to be added to the all resources</td>
		</tr>
		<tr>
			<td>cleanupCRD</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Tells helm to clean up all the vm resources under this release's namespace when uninstalling</td>
		</tr>
		<tr>
			<td>cleanupImage.pullPolicy</td>
			<td>string</td>
			<td><pre lang="">
IfNotPresent
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>cleanupImage.repository</td>
			<td>string</td>
			<td><pre lang="">
bitnami/kubectl
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>createCRD</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td>with this option, if you remove this chart, all crd resources will be deleted with it.</td>
		</tr>
		<tr>
			<td>env</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>extra settings for the operator deployment. Full list <a href="https://docs.victoriametrics.com/operator/vars">here</a></td>
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
			<td>extraArgs</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>operator container additional commandline arguments</td>
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
			<td>extraLabels</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Labels to be added to the all resources</td>
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
			<td>Overrides the full name of server component</td>
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
			<td>image</td>
			<td>object</td>
			<td><pre lang="plaintext">
pullPolicy: IfNotPresent
registry: ""
repository: victoriametrics/operator
tag: ""
variant: ""
</pre>
</td>
			<td>operator image configuration</td>
		</tr>
		<tr>
			<td>image.pullPolicy</td>
			<td>string</td>
			<td><pre lang="">
IfNotPresent
</pre>
</td>
			<td>Image pull policy</td>
		</tr>
		<tr>
			<td>image.registry</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Image registry</td>
		</tr>
		<tr>
			<td>image.repository</td>
			<td>string</td>
			<td><pre lang="">
victoriametrics/operator
</pre>
</td>
			<td>Image repository</td>
		</tr>
		<tr>
			<td>image.tag</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>Image tag override Chart.AppVersion</td>
		</tr>
		<tr>
			<td>imagePullSecrets</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Secret to pull images</td>
		</tr>
		<tr>
			<td>logLevel</td>
			<td>string</td>
			<td><pre lang="">
info
</pre>
</td>
			<td>possible values: info and error.</td>
		</tr>
		<tr>
			<td>nameOverride</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>VM operatror deployment name override</td>
		</tr>
		<tr>
			<td>nodeSelector</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Pod's node selector. Details are <a href="https://kubernetes.io/docs/user-guide/node-selection/">here</a></td>
		</tr>
		<tr>
			<td>operator.disable_prometheus_converter</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>By default, operator converts prometheus-operator objects.</td>
		</tr>
		<tr>
			<td>operator.enable_converter_ownership</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Enables ownership reference for converted prometheus-operator objects, it will remove corresponding victoria-metrics objects in case of deletion prometheus one.</td>
		</tr>
		<tr>
			<td>operator.prometheus_converter_add_argocd_ignore_annotations</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Compare-options and sync-options for prometheus objects converted by operator for properly use with ArgoCD</td>
		</tr>
		<tr>
			<td>operator.useCustomConfigReloader</td>
			<td>bool</td>
			<td><pre lang="">
false
</pre>
</td>
			<td>Enables custom config-reloader, bundled with operator. It should reduce  vmagent and vmauth config sync-time and make it predictable.</td>
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
			<td>podSecurityContext</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td></td>
		</tr>
		<tr>
			<td>probe.liveness</td>
			<td>object</td>
			<td><pre lang="plaintext">
failureThreshold: 3
initialDelaySeconds: 5
periodSeconds: 15
tcpSocket:
    port: probe
timeoutSeconds: 5
</pre>
</td>
			<td>Liveness probe</td>
		</tr>
		<tr>
			<td>probe.readiness</td>
			<td>object</td>
			<td><pre lang="plaintext">
failureThreshold: 3
httpGet:
    path: '{{ include "vm.probe.http.path" . }}'
    port: probe
    scheme: '{{ include "vm.probe.http.scheme" . }}'
initialDelaySeconds: 5
periodSeconds: 15
timeoutSeconds: 5
</pre>
</td>
			<td>Readiness probe</td>
		</tr>
		<tr>
			<td>probe.startup</td>
			<td>object</td>
			<td><pre lang="plaintext">
{}
</pre>
</td>
			<td>Startup probe</td>
		</tr>
		<tr>
			<td>rbac.aggregatedClusterRoles</td>
			<td>object</td>
			<td><pre lang="plaintext">
enabled: true
labels:
    admin:
        rbac.authorization.k8s.io/aggregate-to-admin: "true"
    view:
        rbac.authorization.k8s.io/aggregate-to-view: "true"
</pre>
</td>
			<td>create aggregated clusterRoles for CRD readonly and admin permissions</td>
		</tr>
		<tr>
			<td>rbac.aggregatedClusterRoles.labels</td>
			<td>object</td>
			<td><pre lang="plaintext">
admin:
    rbac.authorization.k8s.io/aggregate-to-admin: "true"
view:
    rbac.authorization.k8s.io/aggregate-to-view: "true"
</pre>
</td>
			<td>labels attached to according clusterRole</td>
		</tr>
		<tr>
			<td>rbac.create</td>
			<td>bool</td>
			<td><pre lang="">
true
</pre>
</td>
			<td>Specifies whether the RBAC resources should be created</td>
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
			<td>Resource object</td>
		</tr>
		<tr>
			<td>securityContext</td>
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
			<td>Specifies whether a service account should be created</td>
		</tr>
		<tr>
			<td>serviceAccount.name</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td>The name of the service account to use. If not set and create is true, a name is generated using the fullname template</td>
		</tr>
		<tr>
			<td>serviceMonitor</td>
			<td>object</td>
			<td><pre lang="plaintext">
annotations: {}
enabled: false
extraLabels: {}
relabelings: []
</pre>
</td>
			<td>configures monitoring with serviceScrape. VMServiceScrape must be pre-installed</td>
		</tr>
		<tr>
			<td>tolerations</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Array of tolerations object. Spec is <a href="https://kubernetes.io/docs/concepts/configuration/assign-pod-node/">here</a></td>
		</tr>
		<tr>
			<td>topologySpreadConstraints</td>
			<td>list</td>
			<td><pre lang="plaintext">
[]
</pre>
</td>
			<td>Pod Topology Spread Constraints. Spec is <a href="https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/">here</a></td>
		</tr>
		<tr>
			<td>watchNamespace</td>
			<td>string</td>
			<td><pre lang="">
""
</pre>
</td>
			<td></td>
		</tr>
	</tbody>
</table>

