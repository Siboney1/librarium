---
title: "Kubernetes"
metaTitle: "Kubernetes with Spectro Cloud"
metaDescription: "Kubernetes pack in Spectro Cloud"
hiddenFromNav: true
isIntegration: true
category: ["kubernetes"]
logoUrl: "https://registry.spectrocloud.com/v1/k8s-dashboard/blobs/sha256:2de5d88b2573af42d4cc269dff75744c4174ce47cbbeed5445e51a2edd8b7429?type=image/png"
---

import Tabs from 'shared/components/ui/Tabs';
import WarningBox from 'shared/components/WarningBox';
import InfoBox from 'shared/components/InfoBox';
import PointsOfInterest from 'shared/components/common/PointOfInterest';
import Tooltip from "shared/components/ui/Tooltip";

# Kubernetes

This pack defines the properties that will be used by Spectro Cloud to bring up the Kubernetes cluster. Most of the Kubernetes hardening standards recommended by the Center for Internet Security is enabled by default.

<WarningBox>
Info: Only Kubernetes versions 1.19 and above is supported
</WarningBox>

## Supported Kubernetes versions

<InfoBox>

Versions supported in the latest [release](/release-notes/) are highlighted.

</InfoBox>

<Tabs>
 
<Tabs.TabPane tab="1.19.x" key="k8s_v1.19">

- **1.19.16**
- **1.19.15**
- **1.19.14**
- **1.19.13**
- **1.19.12**
- **1.19.11**
- **1.19.10**
- **1.19.9**
- **1.19.8**
- **1.19.7**
- **1.19.6**
- **1.19.5**
- **1.19.4**
- **1.19.3**

</Tabs.TabPane>

<Tabs.TabPane tab="1.20.x" key="k8s_v1.20">

- **1.20.12**
- **1.20.11**
- **1.20.10**
- **1.20.9**
- **1.20.8**
- **1.20.7**
- **1.20.6**
- **1.20.5**
- **1.20.4**
- **1.20.2**
- **1.20.1**
- **1.20.0**

</Tabs.TabPane>

<Tabs.TabPane tab="1.21.x" key="k8s_v1.21">

- **1.21.10**
- **1.21.6**
- **1.21.5**
- **1.21.4**
- **1.21.3**
- **1.21.2**
- **1.21.1**
- **1.21.0**

</Tabs.TabPane>

<Tabs.TabPane tab="1.22.x" key="k8s_v1.22">

- **1.22.11**
- **1.22.7**

</Tabs.TabPane>

<Tabs.TabPane tab="1.23.x" key="k8s_v1.23">

- **1.23.4**

</Tabs.TabPane>

</Tabs>

## Notable parameters

| Name                                      | Supported values | Default value                                                                                           | Description                                                                                                                       |
| ----------------------------------------- | ---------------- | ------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| pack.k8sHardening                         | True, False      | True                                                                                                    | Flag to decide if Kubernetes hardening should be applied.                                                                         |
|                                           |                  |                                                                                                         | When set to True, additional flags configured in `kubeadmconfig` will be honored and will be set to the corresponding components. |
|                                           |                  |                                                                                                         | When set to True, additional flags configured in kubeadmconfig will be honored and will be set to the corresponding components.   |
| pack.podCIDR                              | `192.168.0.0/16` | CIDR range for the pod networking. This should match the networking layer property `calicoNetworkCIDR`. | CIDR range for Pods in cluster                                                                                                    |
| pack.serviceClusterIpRange                | `10.96.0.0/12`   | CIDR range for the services. This should not overlap with any IP ranges assigned to nodes for pods.     | CIDR range for Services in the Cluster                                                                                            |
| kubeadmconfig.apiServer.extraArgs         |                  |                                                                                                         | List of additional apiServer flags to be set                                                                                      |
| kubeadmconfig.apiServer.extraVolumes      |                  |                                                                                                         | List of additional volumes to be mounted on apiServer                                                                             |
| kubeadmconfig.controllerManager.extraArgs |                  |                                                                                                         | List of additional ControllerManager flags to be set                                                                              |
| kubeadmconfig.scheduler.extraArgs         |                  |                                                                                                         | List of additional Kube Scheduler flags to be set                                                                                 |
| kubeadmconfig.files                       |                  |                                                                                                         | List of additional files to be copied over to the nodes                                                                           |
| kubeadmconfig.preKubeadmCommands          |                  |                                                                                                         | List of additional commands to be executed **before** kubeadm commands are run                                                    |
| kubeadmconfig.postKubeadmCommands         |                  |                                                                                                         | List of additional commands to be executed **after** kubeadm commands are run                                                     |

## Example Kubeadm config

```yaml
kubeadmconfig:
  apiServer:
    extraArgs:
      anonymous-auth: "true"
      insecure-port: "0"
      profiling: "false"
    extraVolumes:
      - name: audit-policy
        hostPath: /etc/kubernetes/audit-policy.yaml
        mountPath: /etc/kubernetes/audit-policy.yaml
        readOnly: true
        pathType: File
  controllerManager:
    extraArgs:
      profiling: "false"
      terminated-pod-gc-threshold: "25"
      use-service-account-credentials: "true"
  scheduler:
    extraArgs:
      profiling: "false"
  kubeletExtraArgs:
    read-only-port: "0"
    event-qps: "0"
    protect-kernel-defaults: "true"
  files:
    - path: hardening/audit-policy.yaml
      targetPath: /etc/kubernetes/audit-policy.yaml
      targetOwner: "root:root"
      targetPermissions: "0600"
  preKubeadmCommands:
    - 'echo "Executing preKubeadmCmds"'
  postKubeadmCommands:
    - 'echo "Executing postKubeadmCmds"'
```
