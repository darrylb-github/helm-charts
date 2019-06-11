# nodelocaldns

[nodelocaldns](https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/dns/nodelocaldns) is a Kubernetes daemonset for running node-local dns server for a more scalable Kubernetes cluster DNS.

## Prerequisites

Kubernetes 1.10+

## Installing the Chart

To install the chart with the release name `nodelocaldns`, run:

```bash
$ helm install --name nodelocaldns stable/nodelocaldns
```

After a few minutes, you should see nodelocaldns is running on every node in your cluster.

**Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```bash
helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following table lists the configurable parameters of the node-init chart and their default values.

|             Parameter       |            Description             |                    Default                |
|-----------------------------|------------------------------------|-------------------------------------------|
| `image.repository`          | The image repository to pull from  | `k8s.gcr.io/k8s-dns-node-cache`           |
| `image.tag`                 | The image tag to pull              | `1.15.0`                                  |
| `image.pullPolicy`          | Image pull policy                  | `IfNotPresent`                            |
| `image.pullSecrets`         | Image pull secrets                 |  `nil`                                    |
| `rbac.create`               | If true, create & use RBAC resources | `true`                                  |
| `rbac.serviceAccount`       | existing ServiceAccount to use (ignored if rbac.create=true) | `default`       |
| `name`              | Container name if Daemonset or Deployment | `node-cache`                      |
| `env`               | Additional environment variables   | `nil`                                   |
| `volumes`           | Additional volumes                 | `nil`                                   |
| `volumeMounts`      | Additional volumeMounts            | `nil`                                   |
| `resources.requests.cpu` | CPU resource requests         | `200m`                                    |
| `resources.limits.cpu` | CPU resource limits             | `200m`                                    |
| `resources.requests.memory` | Memory resource requests   | `256Mi`                                   |
| `resources.limits.memory` | Memory resource limits       | `256Mi`                                   |
| `securityContext`   | Allows you to overwrite the default securityContext applied to the container  | `{"privileged":true}`  |
| `livenessProbe`     | Overrides the default liveness probe | http port 5555                          |
| `podAnnotations`  | Annotations to add to the DaemonSet's Pods | `nil`                             |
| `tolerations`     | List of node taints to tolerate (requires Kubernetes >= 1.6) | `nil`           |
| `nodeSelector`    | Node selectors                     | `nil`                                     |
| `affinity`        | Node affinities                    | `nil`                                     |
| `useHostNetwork`  | If true, use the host's network. Must be enabled when e.g. the init script must be run before any network plugins are loaded, or e.g. it configures the host network interface. | `true`                                     |
| `useHostPID`.     | If true, use the host's PID namespace. Must be enabled when the init script invokes operations on processes in the host space.  | `nil`                               |
| `priorityClassName` | Which Priority Class to associate with the daemonset. Use `system-node-critical` if you want to be extra sure that the init script is run. | `nil`                  |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
helm install --name nodelocaldns \
  --set nodelocaldns.image=YOUR-IMAGE \
  stable/nodelocaldns
```

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
helm install --name nodelocaldns -f my-values.yaml stable/nodelocaldns
```

**Tip**: You can copy and customize the default [values.yaml](values.yaml)
