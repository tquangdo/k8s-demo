# k8s-demo 🐳

![Stars](https://img.shields.io/github/stars/tquangdo/k8s-demo?color=f05340)
![Issues](https://img.shields.io/github/issues/tquangdo/k8s-demo?color=f05340)
![Forks](https://img.shields.io/github/forks/tquangdo/k8s-demo?color=f05340)
[![Report an issue](https://img.shields.io/badge/Support-Issues-green)](https://github.com/tquangdo/k8s-demo/issues/new)

## reference
- [youtube1](https://www.youtube.com/watch?v=DvZVFQFjzsQ)

## CLI
1. ### see info
    ```shell
    kubectl get all/namespace/node/pod/service/replicaset/deployment
    kubectl config view
    kubectl version --output=yaml
    kubectl cluster-info
    ```

1. ### get all
    ```shell
    kubectl get all      
    ~~~~
    NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
    service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   16h
    ```
 
1. ### describe
    ```shell
    kubectl describe node/docker-desktop
    ~~~~
    Name:               docker-desktop
    Roles:              control-plane
    Labels:             beta.kubernetes.io/arch=arm64
    ...
    Conditions:
    Type             Status  LastHeartbeatTime                 LastTransitionTime                Reason                       Message
    ----             ------  -----------------                 ------------------                ------                       -------
    MemoryPressure   False   Mon, 20 Feb 2023 11:14:33 +0900   Sun, 19 Feb 2023 22:13:12 +0900   KubeletHasSufficientMemory   kubelet has sufficient memory available
    ...
    Addresses:
    InternalIP:  192.168.65.4
    ...
    Allocatable:
    cpu:                4
    ...
    memory:             3925304Ki
    pods:               110
    ```

1. ### deployment
    ```shell
    kubectl create deployment [name]
    ```

1. ### debug
    ```shell
    kubectl logs [pod name]
    kubectl exec -it [pod name] -- bin/bash
    ```

1. ### config file
    ```shell
    kubectl apply -f [file name]
    kubectl delete -f [file name]
    ```


![demo](screenshots/demo.png)
