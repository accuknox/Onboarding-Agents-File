## 1. Shared Informer Agent Installation Guide

Description : This agent authenticates with your cluster and collects information regarding the entities like nodes, pods and namespaces.

```
Installation Commands Here
```

## 2. Data Protection and Anomaly Detection Installation Guide

Description : Trains a model based on container workload type. It constantly monitors the syscalls happening inside the container. After training, if the VAE sees syscalls happening in a way not seen in training phase, it will send high reconstruction error with detailed forensics information.

```
Installation Commands Here
```

## 3. Cilium Installation Guide

Description : This agent is used to apply Network Policies.

#### For managed environment (GKE):

Command to Extract the Cluster CIDR to enable native-routing
```
NATIVE_CIDR=$(gcloud container clusters describe $CLUSTER_NAME --zone $CLUSTER_ZONE --format 'value(clusterIpv4Cidr)')
```

Command to Setup Helm repository
```
helm repo add cilium https://helm.cilium.io/
```

Command to Deploy Cilium release via Helm
```
helm install cilium cilium/cilium --version 1.9.8 \ 
--namespace kube-system \ 
--set nodeinit.enabled=true \ 
--set nodeinit.reconfigureKubelet=true \ 
--set nodeinit.removeCbrBridge=true \ 
--set cni.binPath=/home/kubernetes/bin \ 
--set gke.enabled=true \ 
--set ipam.mode=kubernetes \ 
--set nativeRoutingCIDR=$NATIVE_CIDR
```



## 4. KubeArmor Installation Guide

Description : This agent is used to apply System Policies.

#### Deploy KubeArmor for GKE
```
kubectl apply -f https://raw.githubusercontent.com/kubearmor/KubeArmor/master/deployments/GKE/kubearmor.yaml
```

#### Deploy KubeArmor Host Policy
```
kubectl apply -f https://raw.githubusercontent.com/kubearmor/KubeArmor/master/pkg/KubeArmorHostPolicy/config/crd/bases/security.kubearmor.com_kubearmorhostpolicies.yaml
```

#### Deploy KubeArmor Policy
```
kubectl apply -f https://raw.githubusercontent.com/kubearmor/KubeArmor/master/pkg/KubeArmorPolicy/config/crd/bases/security.kubearmor.com_kubearmorpolicies.yaml
```


## 5. Node Event Feeder Installation Guide

Description : Feeder service deployment that collects feeds from KubeArmor and Cilium

```
Installation Commands Here
```
