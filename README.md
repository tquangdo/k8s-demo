# k8s-demo 🐳

![Stars](https://img.shields.io/github/stars/tquangdo/k8s-demo?color=f05340)
![Issues](https://img.shields.io/github/issues/tquangdo/k8s-demo?color=f05340)
![Forks](https://img.shields.io/github/forks/tquangdo/k8s-demo?color=f05340)
[![Report an issue](https://img.shields.io/badge/Support-Issues-green)](https://github.com/tquangdo/k8s-demo/issues/new)

## reference
- [youtube1](https://www.youtube.com/watch?v=dyaEzaDS7NQ)
- [youtube2](https://www.youtube.com/watch?v=CX8AnwTW2Zs)
- [youtube3](https://www.youtube.com/watch?v=hl6qFk6WhUk)
- [youtube4](https://www.youtube.com/watch?v=s_o8dwzRlu4)

## CLI
1. ### see info
    ```shell
    kubectl get all/namespace/node/svc/pod/replicaset/deployment/secret< --all-namespaces>< -o wide>
    kubectl get configmap
    kubectl config view
    kubectl version --output=yaml
    kubectl cluster-info
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
    kubectl delete --all svc/pod/replicaset/deployment/secret --namespace=default
    ```

## youtube1
1. ### get all
    ```shell
    kubectl get all      
    ~~~~
    # 1/ pod
    NAME                                READY   STATUS    RESTARTS   AGE
    pod/yt1-metadata-5f9dc4d6bc-5vbgs   1/1     Running   0          8m43s
    pod/yt1-metadata-5f9dc4d6bc-g8xqp   1/1     Running   0          8m43s
    pod/yt1-metadata-5f9dc4d6bc-q4hjn   1/1     Running   0          8m43s

    # 2/ service
    NAME                  TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
    service/kubernetes    ClusterIP      10.96.0.1      <none>        443/TCP          18h
    service/yt1-service   LoadBalancer   10.104.114.3   localhost     8083:31932/TCP   29s

    # 3/ deployment
    NAME                           READY   UP-TO-DATE   AVAILABLE   AGE
    deployment.apps/yt1-metadata   3/3     3            3           8m43s

    # 4/ replicaset
    NAME                                      DESIRED   CURRENT   READY   AGE
    replicaset.apps/yt1-metadata-5f9dc4d6bc   3         3         3       8m43s
    ```
1. ### ssh to nginx container (in pod)
    ```shell
    kubectl exec -it yt1-metadata-5f9dc4d6bc-5vbgs -- bin/bash
    root@yt1-metadata-5f9dc4d6bc-5vbgs:/ ls
    #bin  boot  dev  docker-entrypoint.d  docker-entrypoint.sh  etc  home  lib  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
    ```
1. ### demo
    - access `localhost:8083`(in `yt1/service.yaml`) on browser will see HP of Nginx
    ![demo](screenshots/demo.png)

## youtube2
- run `kubectl apply -f yt2/deployment.yaml`
1. ### ERR
    - show 🔴 & search KW `False` will see errors
    ![ERR](screenshots/ERR.png)
1. ### OK > port forward
    - with extension, type `10001:80` will auto create this command:
    ```shell
    kubectl port-forward pods/hello-deployment-f694ff6c4-cm2qz 10001:80 -n default
    # Forwarding from 127.0.0.1:10001 -> 80
    # Forwarding from [::1]:10001 -> 80
    # Handling connection for 10001
    ```
    ![PortFWD](screenshots/PortFWD.png)
1. ### demo
    - access `localhost:10001` on browser will see `gcr.io/google-samples/hello-app:2.0`
    ![Demo2](screenshots/Demo2.png)

## youtube3
1. ### create deployment
    ```shell
    kubectl create deployment demo-nginx --image=nginx --replicas=1
    kubectl get deployment 
    # NAME         READY   UP-TO-DATE   AVAILABLE   AGE
    # demo-nginx   1/1     1            1           2m24s
    kubectl get svc        
    # NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
    # kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   36h
    ```
1. ### expose deployment
    ```shell
    kubectl expose deployment demo-nginx --port=80
    kubectl get svc                               
    # NAME         TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)   AGE
    # demo-nginx   ClusterIP   10.98.20.54   <none>        80/TCP    8s
    # kubernetes   ClusterIP   10.96.0.1     <none>        443/TCP   36h
    ```
1. ### port forward
    ```shell
    kubectl port-forward service/demo-nginx 17000:80
    # Forwarding from 127.0.0.1:17000 -> 80
    # Forwarding from [::1]:17000 -> 80
    # Handling connection for 17000
    ```
    - access `localhost:17000` on browser will see HP of Nginx

## youtube4
![yt4_1](screenshots/yt4_1.png)
-
![yt4_2](screenshots/yt4_2.png)

1. ### run 4 yaml files
    ```shell
    kubectl apply -f yt4/mongo-config.yaml
    kubectl apply -f yt4/mongo-secret.yaml
    kubectl apply -f yt4/mongo.yaml
    kubectl apply -f yt4/webapp.yaml
    ```
1. ### check result
    1. ### secret
        ```shell
        kubectl get secret
        #NAME           TYPE     DATA   AGE
        #mongo-secret   Opaque   2      3m37s
        ```
    1. ### configmap
        ```shell
        kubectl get configmap
        #NAME               DATA   AGE
        #mongo-config       1      4m
        ```
    1. ### service
        ```shell
        kubectl get svc                                   
        #NAME             TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
        #kubernetes       ClusterIP   10.96.0.1      <none>        443/TCP          39m
        #mongo-service    ClusterIP   10.111.82.5    <none>        27017/TCP        4m57s
        #webapp-service   NodePort    10.101.60.17   <none>        3000:30100/TCP   4m48s
        ```
    1. ### pod
        ```shell
        kubectl get pod      
        #NAME                                 READY   STATUS    RESTARTS   AGE
        #mongo-deployment-7d4d5c9f6c-9mzhh    1/1     Running   0          3m47s
        #webapp-deployment-649d7fb885-xw6mq   1/1     Running   0          3m38s
        kubectl logs webapp-deployment-649d7fb885-xw6mq -f
        #app listening on port 3000!
        ```
1. ### access on browser
![yt4_3](screenshots/yt4_3.png)
-
![yt4_4](screenshots/yt4_4.png)
