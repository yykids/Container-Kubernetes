## Container > Kubernetes > User Guide 

## Cluster
Cluster refers to a group of instances that comprise user's Kubernetes. 

### Creating Clusters
To enable Kubernetes, a cluster must be created. Go to **Container > Kubernetes** and click **Create Clusters** and a page of creating clusters opens. Following items are required to create a cluster: 

| Item | Description |
| --- | --- |
| Cluster Name | Name of a Kubernetes cluster, to be comprised of less than 20 characters, including alphabets, numbers, '-', and '.'|
| Kubernetes Version | Kubernetes version to use |
| VPC | VPC network to be attached to clusters |
| Subnet | subnet, among those defined for VPC, to be associated with instances that comprise a cluster VPC |
| Image | Images for instances comprising a cluster |
| Availability Area | Area to create a default node group instance |
| Instance Type | Instance specifications for a default node group |
| Node Count | Number of instances for a default node group |
| Keypair | Keypair to access default node group |
| Block Storage Type | Type of block storage for a default node group instance |
| Block Storage Size | Size of block storage for a default node group instance |

Enter information as required and click **Create Clusters**, and a cluster begins to be created. You may check status from the list of clusters. It takes about 10 minutes to create; more time may be required depending on the cluster setting.  

> [Caution]
> With a cluster created, a default node group is created. After a default node group is created, the number of nodes cannot be modified. When you need more nodes, a new node group must be created. 


### Querying Clusters 
A newly created cluster can be found on **Container > Kubernetes**. Select a cluster and the information shows at the bottom. 

| Item | Description |
| --- | --- |
| Cluster Name | Name and ID of Kubernetes Cluster |
| Node Count | Number of instances of all nodes comprising a cluster |
| Kubernetes Veresion | Kubernetes version in service |
| VPC | VPC network attached to cluster |
| Subnet | Subnet associated to a node instance comprising a cluster |
| API Endpoint | URI of API endpoint to access cluster for opearation |
| Configuration File | Download button of configuration file required to access cluster for operation |

### Deleting Clusters 
Select a cluster to delete, and click **Delete Clusters** and it is deleted. It takes about 5 minutes to delete; more time may be required depending on the cluster status. 

## Node Group
A node group is comprised of worker node instances that comprise a Kubernetes. 

### Querying Node Groups 
Click a cluster name on the list to find the list of node groups. Select a node group and the information shows at the bottom.  

* Basic Information
On the **Basic Information** tab, check the following: 

| Item |Description |
| --- | --- |
| Node Group Name | Name and ID of a node group|
| Cluster Name | Name and ID of a cluster to which a node group is included |
| Kubernetes Version | Kubernetes version in service |
| Availability Area | Area in which a node group instance is created |
| Instance Type | Specifications of a node group instance |
| Image Type | Type of image for a node group instance |
| Block Storage Size | Size of block storage for a node group instance |
| Created Date | Time when node group was created |
| Modified Date | Last time when node group was modified |

* List of Nodes 
Find the list of instances comprising a node group from the **List of Nodes** tab. 

### Creating Node Groups 
Along with a new cluste, a default node group is created, but more node groups can be created depending on the needs. If higher specifications are required to run a container, or more worker node instances are required to scale out, node groups may be additionally created. Click **Create Node Groups** from the page of node group list, and the page of creating a node group shows up. Following items are required to create a node group:  

| Item | Description |
| --- | --- |
| Availability Area | Area to create instances comprising a cluster |
| Node Group Name | Name of additional node group, comprised of alphabets, numbers, '-', and '.' |
| Instance Type | Specificiations of an instance for additional node group |
| Node Count | Number of instances for additional node group |
| Keypair | Keypair to access additional node group |
| Block Storage Type | Type of block storage of instance for additional node group |
| Block Storage Size | Size of block storage of instance for additional node group |

Enter information as required and click **Create Node Groups**, and a node group begins to be created. You may check status from the list of node groups. It takes about 5 minutes to create; more time may be required depending on the node group setting.  

### Deleting Node Groups 
Select a node group to delete from the list of node groups, and click **Delete Node Groups** and it is deleted. It takes about 5 minutes to delete a node group; more time may be required depending on the node group status. 

## Cluster Management
To run and manage clusters from a remote host, 'kubectl', which is the command line tool (CLI) as provided by Kubernetes, is required.

### Installing kubectl
For kubectl, execution files can be downloaded and enabled, with no need of special installation procedure. Each operating system provides the following download path: 

| OS | Download Command |
| --- | --- |
| Linux | curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/linux/amd64/kubectl |
| MacOS | curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/darwin/amd64/kubectl |
| Windows | curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/windows/amd64/kubectl.exe |

For more details on installation and optional items, see documents of [Install and Set Up kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

#### Role Changes
By default, downloaded files are not allowed to execute. The execution role must be added. 

```
$ chmod +x kubectl
```

#### 위치 변경 또는 경로 지정 Change Location or Specify Paths 
Change location to the path specified for an environment variable so as to execute kubectl on any path, or add the path including kubectl to an environment variable.  

* Change Loation to Path Specified for Environment Variable 
```
$ sudo mv kubectl /usr/local/bin/
```

* Add Path to Environment Variable 
```
// Executed on the path including kubectl
$ export PATH=$PATH:$(pwd)
```

### Configuration 
To access Kubernetes cluster with kubectl, cluster configuration file (kubeconfig) is required. On TOAST web console, open **Container > Kubernetes** and select a cluster to access. From **Basic Information**, click **Download** of **Configuration Files** to download a configuration file. Change the downloaded configuration file to a location of choice to serve as reference for kubectl execution. 

> [Caution]
> A configuration file downloaded from TOAST web console includes cluster information and token for authentication. With the file, you're authorized to access corresponding Kubernetes clusters. Take cautions for not losing configuration files.   

kubectl requires a cluster configuration file every time it is executed, so a cluster configuration file must be specified by using the `--kubeconfig` option. However, if the environment variable includes specific path for a cluster configuration file, there is no need to specify each option. 

```
$ export KUBECONFIG={Path of cluster configuration file}
```

You may copy cluster configuration file path to `$HOME/.kube/config`, which is the default configuration file of kubectl, if you don't want to save it to an environment variable. However, when there are many clusters, it is easier to change environment variables. 

### Confirming Connection 
See if it is well set by the `kubectl version` command. If there's no problem, `Server Version` is printed.  

```
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"15", GitVersion:"v1.15.7", GitCommit:"6c143d35bb11d74970e7bc0b6c45b6bfdffc0bd4", GitTreeState:"clean", BuildDate:"2019-12-11T12:42:56Z", GoVersion:"go1.12.12", Compiler:"gc", Platform:"darwin/amd64"}
Server Version: version.Info{Major:"1", Minor:"15", GitVersion:"v1.15.7", GitCommit:"6c143d35bb11d74970e7bc0b6c45b6bfdffc0bd4", GitTreeState:"clean", BuildDate:"2019-12-11T12:34:17Z", GoVersion:"go1.12.12", Compiler:"gc", Platform:"linux/amd64"}
```

* Client Version: Version information of executed kubectl file 
* Server Version: Kubernetes version information comprising a cluster 

## LoadBalancer Service
Pod is a basic executio unit of a Kubernetes application and it is connected to a cluster network via CNI (Container Network Interface). Basically, access to pod is unavailble from cluster externals. To open up pod services outside of a cluster, a path to be made public must be created by using Kubernetes' `LoadBalancer` service object. 

### Creating Web Server Pods 
Write deployment object manifest file to execute the following two nginx pods and create an object. 

```yaml
# nginx.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

With deployment object created, pods defined at manifest are automatically created. 

```
$ kubectl apply -f nginx.yaml
deployment.apps/nginx-deployment created

$ kubectl get pods
NAME                                READY   STATUS    RESTARTS   AGE  
nginx-deployment-7fd6966748-pvrzs   1/1     Running   0          4m13s
nginx-deployment-7fd6966748-wv7rd   1/1     Running   0          4m13s
```

To use images saved at TOAST Container Registry, first create a secret to login to user registry. 

```
$ kubectl create secret docker-registry registry-credential --docker-server={user registry address} --docker-username={email address for Toast account} --docker-password={service or integrated Appkey}
secret/registry-credential created

$ kubectl get secrets
NAME                  TYPE                             DATA   AGE
registry-credential   kubernetes.io/dockerconfigjson   1      30m
```

By adding secret information to the deployment manifest file and changing the name of image, pods can be created by using images saved at user registry. 

```yaml
# nginx.yaml
...
spec:
  ...
  template:
    ...
    spec:
      containers:
      - name: nginx
        image: {user registry address}/nginx:1.14.2
        ...
      imagePullSecrets:
      - name: regcred

```

> [Note]
> Regarding how to use TOAST Container Registry, see [User Guide for Container Registry](/Container/Container%20Registry/en/user-guide).

### Creating LoadBalancer 
To define service object of Kubernetes, a manifest comprised of the following items is required: 

| Item | Description |
| --- | --- |
| metadata.name | Name of service object |
| spec.selector | Name of pod to be associated with service object |
| spec.ports | Interface setting to deliver incoming traffic from external load balancer to a pod |
| spec.ports.name | Name of interface |
| spec.ports.protocol | Protocol for an interface (e.g: TCP) |
| spec.ports.port | Port number to be made public out of service object |
| spec.ports.targetPort | Port number of a pod to be associated with service object |
| spec.type | Type of service object |

Service manifest is written like below. The LoadBalancer service object is associated with a pod labelled as `app: nginx`, following the defined name at **spec.selector**. And as **spec.ports** defines, traffic inflow via TCP/8080 is delivered to the TCP/80 port of the pod.  

```yaml
# service.yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-svc
  labels:
    app: nginx
spec:
  ports:
  - port: 8080
    targetPort: 80
    protocol: TCP
  selector:
    app: nginx
  type: LoadBalancer
```

When the LoadBalancer service object is created, it takes some time to create and associate a load balancer externally. Before associated with external load balancer, **EXTERNAL-IP** shows `<pending>`. 

```
$ kubectl apply -f service.yaml
service/nginx-svc created

$ kubectl get service
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
nginx-svc    LoadBalancer   10.254.134.18   <pending>     8080:30013/TCP   11s
```

When it is associated with external load balancer, **EXTERNAL-IP** shows IP, which refers to floating IP of external load balancer. 

```
$ kubectl get service
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)          AGE
nginx-svc    LoadBalancer   10.254.134.18   123.123.123.30   8080:30013/TCP   3m13s
```

> [Note]
> To find a load balancer that is created, visit **Network > Load Balancer**.
> Load balancer IP is a floating IP allowing external access. Check out from **Network > Floating IP**.


### Testing Service on Internet 
Send an HTTP request via floating IP associated with load balancer to see if the web server pod of a Kubernetes cluster responds. Since the TcP/8080 port of a service object is attached to TCP/80 port of a pod, request must be sent to the TCP/8080 port. If external load balancer, service object, and pod are well associated, the web server shall respond to nginx default page. 

```
$ curl http://123.123.123.30:8080
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```


## Ingress Controller 
Ingress Controller routes HTTP and HTTPS requests from cluster externals to internal services, in reference of the rules that are defined at ingress object so as to provide SSL/TSL closure and virtual hosting. For more details on Ingress Controller and Ingress, see [Ingress Controller](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/), [인그레스](https://kubernetes.io/docs/concepts/services-networking/ingress/).


### Installing NGINX Ingress Controller 
NGINX Ingress Controller is one of the most frequently used ingress controllers. For more details, see [NGINX Ingress Controller](https://kubernetes.github.io/ingress-nginx/)와 [NGINX Ingress Controller for Kubernetes](https://docs.nginx.com/nginx-ingress-controller/overview/).

NGINX Ingress Controller provides pre-defined manifest files to readily create resources in need. With this manifest, resources can be easily created when required. 

```
$ kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.30.0/deploy/static/mandatory.yaml
namespace/ingress-nginx created
configmap/nginx-configuration created
configmap/tcp-services created
configmap/udp-services created
serviceaccount/nginx-ingress-serviceaccount created
clusterrole.rbac.authorization.k8s.io/nginx-ingress-clusterrole created
role.rbac.authorization.k8s.io/nginx-ingress-role created
rolebinding.rbac.authorization.k8s.io/nginx-ingress-role-nisa-binding created
clusterrolebinding.rbac.authorization.k8s.io/nginx-ingress-clusterrole-nisa-binding created
deployment.apps/nginx-ingress-controller created
limitrange/ingress-nginx created
```

### Creating LoadBalancer 
Since ingress controller is also created as a pod, LoadBalancer or NodePort must be created to be made public. The LoadBalancer service manifest is defined to process HTTP and HTTPS like below: 

```yaml
# ingress-nginx-lb.yaml
apiVersion: v1
kind: Service
metadata:
  name: ingress-nginx
  namespace: ingress-nginx
  labels:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
spec:
  type: LoadBalancer
  selector:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
  ports:
    - name: http
      port: 80
      targetPort: 80
      protocol: TCP
    - name: https
      port: 443
      targetPort: 443
      protocol: TCP
  selector:
    app.kubernetes.io/name: ingress-nginx
    app.kubernetes.io/part-of: ingress-nginx
```

After service object is created, check if it is associated with an external load balancer. The **EXTERNAL-IP** field must include floating IP address setting. 

```
$ kubectl apply -f ingress-nginx-lb.yaml
service/ingress-nginx created

$ kubectl get svc -n ingress-nginx
NAME            TYPE           CLUSTER-IP     EXTERNAL-IP      PORT(S)                      AGE
ingress-nginx   LoadBalancer   10.254.2.128   123.123.123.41   80:30820/TCP,443:30269/TCP   39s
```

### Diverging Service on URI 
Ingress controller can diverge services based on URI. Below figure shows the structure of a simple example of service divergence based on URI. 

![ingress-01.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/ingress-01.png)

#### Create Services and Pods 
Manifest is created to create services and pods like below: Associate the `tea` pod to `tea-svc`, and the `coffee` pod to `coffee-svc`.

```yaml
# cafe.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: coffee
spec:
  replicas: 3
  selector:
    matchLabels:
      app: coffee
  template:
    metadata:
      labels:
        app: coffee
    spec:
      containers:
      - name: coffee
        image: nginxdemos/nginx-hello:plain-text
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: coffee-svc
spec:
  ports:
  - port: 80
    targetPort: 8080
    protocol: TCP
    name: http
  selector:
    app: coffee
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tea
spec:
  replicas: 2
  selector:
    matchLabels:
      app: tea
  template:
    metadata:
      labels:
        app: tea
    spec:
      containers:
      - name: tea
        image: nginxdemos/nginx-hello:plain-text
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: tea-svc
  labels:
spec:
  ports:
  - port: 80
    targetPort: 8080
    protocol: TCP
    name: http
  selector:
    app: tea
```

Apply manifest, and see if deployment, service, and pod is created. The pod must be **Running**. 

```
$ kubectl apply -f cafe.yaml
deployment.apps/coffee created
service/coffee-svc created
deployment.apps/tea created
service/tea-svc created

$ kubectl get deploy,svc,pods
NAME                           READY   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/coffee   3/3     3            3           18s
deployment.extensions/tea      2/2     2            2           18s

NAME                 TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
service/coffee-svc   ClusterIP   10.254.51.117    <none>        80/TCP    18s
service/tea-svc      ClusterIP   10.254.210.170   <none>        80/TCP    18s

NAME                          READY   STATUS    RESTARTS   AGE
pod/coffee-67c6f7c5fd-98vh5   1/1     Running   0          18s
pod/coffee-67c6f7c5fd-c58l2   1/1     Running   0          18s
pod/coffee-67c6f7c5fd-dmxf6   1/1     Running   0          18s
pod/tea-7df475c6-gtlx5        1/1     Running   0          18s
pod/tea-7df475c6-lxqsx        1/1     Running   0          18s
```

#### Create Ingress
According to the request path, ingress manifest is created for service connection. A request with `/tea` as endpoint is connected to the `tea-svc` service, while `/coffee` is connected to the the `coffee-svc` service. 

```yaml
# cafe-ingress-uri.yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: cafe-ingress-uri
spec:
  rules:
  - http:
      paths:
      - path: /tea
        backend:
          serviceName: tea-svc
          servicePort: 80
      - path: /coffee
        backend:
          serviceName: coffee-svc
          servicePort: 80
```

In a while after ingress is created, IP must be configured at the **ADDRESS** field.  

```
$ kubectl apply -f cafe-ingress-uri.yaml
ingress.extensions/cafe-ingress-uri created

$ kubectl get ingress cafe-ingress-uri
NAME               HOSTS   ADDRESS          PORTS   AGE
cafe-ingress-uri   *       123.123.123.44   80      88s
```

#### Send HTTP Requests 
Send HTTP request to the IP address set for **ADDRESS** of ingress for an external host, to check if the ingress has been properly set. 

Request for `/coffee` as endpoint is sent to the `coffee-svc` service so as the `coffee` pod can respond. From the **Server name**, you can see that `coffee` pods take turns to respond in the round-robin technique. 

```
$ curl http://123.123.123.44/coffee
Server address: 10.100.3.48:8080
Server name: coffee-67c6f7c5fd-c58l2
Dat#e: 07/Apr/2020:08:24:27 +0000
URI: /coffee
Request ID: e831901e441303ad59fb02214c49d84a

$ curl http://123.123.123.44/coffee
Server address: 10.100.2.23:8080
Server name: coffee-67c6f7c5fd-98vh5
Date: 07/Apr/2020:08:24:28 +0000
URI: /coffee
Request ID: e78427e68a1cd61ec633b9328359874e
```

Likewise, request for `/tea` as endpoint is delivered to the `tea-svc` service so as the `tea` can respond.   

```
$ curl http://123.123.123.44/tea
Server address: 10.100.2.24:8080
Server name: tea-7df475c6-lxqsx
Date: 07/Apr/2020:08:25:03 +0000
URI: /tea
Request ID: 59303a5a5baa60802b463b1856c8ce8d
```

When a request is sent to undefined URI, the ingress controller sends `404 Not Found` as response.  

```
$ curl http://123.123.123.44/
<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.17.8</center>
</body>
</html>
```

#### Delete Resources
Resources for testing can be deleted with used manifest.  

```
$ kubectl delete -f cafe-ingress-uri.yaml
ingress.extensions "cafe-ingress-uri" deleted

$ kubectl delete -f cafe.yaml
deployment.apps "coffee" deleted
service "coffee-svc" deleted
deployment.apps "tea" deleted
service "tea-svc" deleted
```

### Service Divergence on Host 
Ingress controller can diverge services based on the host name. Below figure shows the structure of a simple example of service divergence based on the host name. 

![ingress-02.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/ingress-02.png)

#### Create Services and Pods 
Create services and pods by using the same manifest as [URI-based Service Divergence](/Container/Kubernetes/en/user-guide/#uri). 

#### Create Ingress 
Write the ingress manifest connecting services based on the host name. Incoming request via the `tea.cafe.example.com` host is connected to the `tea-svc` service, while request via the `coffee.cafe.example.com` host is connected to the `coffee-svc` service.      

```yaml
# cafe-ingress-host.yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: cafe-ingress-host
spec:
  rules:
  - host: tea.cafe.example.com
    http:
      paths:
      - path: /
        backend:
          serviceName: tea-svc
          servicePort: 80
  - host: coffee.cafe.example.com
    http:
      paths:
      - path: /
        backend:
          serviceName: coffee-svc
          servicePort: 80
```

In a while after ingress is created, IP must be configured at the **ADDRESS** field. 

```
$ kubectl apply -f cafe-ingress-host.yaml
ingress.extensions/cafe-ingress-host created

$ kubectl get ingress
NAME                HOSTS                                          ADDRESS          PORTS   AGE
cafe-ingress-host   tea.cafe.example.com,coffee.cafe.example.com   123.123.123.44   80      4m29s
```

#### Send HTTP Requests 
HTTP request is sent from external host to IP configured at the ADDRESS of the ingress controller. Nevertheless, such request must be sent by using host name, since service divergence is based on the host name by configuration.

> [Note]
> To test with a random host name, use the --resolve option of curl: enter the --resolve option in the `{Host Name}:{Port Number}:{IP}`format. This means to resolve a request for {Port Number} to be sent to {Host Name} as {IP}. 
> You may open up the `/etc/host` file and add `{IP} {Host Name}`. 

When a request is sent to the `coffee.cafe.example.com` host, it is delivered to`coffee-svc` so that the `coffee` pod can respond.

```
$ curl --resolve coffee.cafe.example.com:80:123.123.123.44 http://coffee.cafe.example.com/
Server address: 10.100.2.25:8080
Server name: coffee-67c6f7c5fd-2bbzf
Date: 07/Apr/2020:08:45:39 +0000
URI: /
Request ID: 29fd8a244b9f0a5ff5f35d1dc35edccf
```

When a request is sent to the `tea.cafe.example.com` host, it is delivered to `tea-svc` so that the `tea` pod can respond. 

```
$ curl --resolve tea.cafe.example.com:80:123.123.123.44 http://tea.cafe.example.com/
Server address: 10.100.3.52:8080
Server name: tea-7df475c6-q8mdx
Date: 07/Apr/2020:08:53:44 +0000
URI: /
Request ID: fe61c1589d3ab8ef4ca4507245251ef3
```

When it is requested to an unknown host, the ingress controller sends `404 Not Found` as response.  

```
$ curl http://123.123.123.44
<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.17.8</center>
</body>
</html>

$ curl --resolve test.example.com:80:123.123.123.44 http://test.example.com/
<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.17.8</center>
</body>
</html>
```

## Kubernetes Dashboard 
TOAST Kubernetes provides default web UI dashboard. For more details on Kubernetes Dashboard, see documents at [Web UI (Dashboard)](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/). 

### Opening Dashboard Services
User Kubernetes has the `kubernetes-dashboard` service object which has been already created to publicly open dashboard. 

```
$ kubectl get svc kubernetes-dashboard -n kube-system
NAME                   TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
kubernetes-dashboard   ClusterIP   10.254.95.176   <none>        443/TCP   2d4h

$ kubectl describe svc kubernetes-dashboard -n kube-system
Name:              kubernetes-dashboard
Namespace:         kube-system
Labels:            k8s-app=kubernetes-dashboard
Annotations:       kubectl.kubernetes.io/last-applied-configuration:
                     {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"labels":{"k8s-app":"kubernetes-dashboard"},"name":"kubernetes-dashboard"...
Selector:          k8s-app=kubernetes-dashboard
Type:              ClusterIP
IP:                10.254.95.176
Port:              <unset>  443/TCP
TargetPort:        8443/TCP
Endpoints:         10.100.2.3:8443
Session Affinity:  None
Events:
...
```

However, the `kubernetes-dashboard` object belongs to ClusterIP type and is not open out of the cluster. To open up dashboard externally, the service object type must be changed into LoadBalancer, or ingress controller and ingress object must be created.  

#### Change into LoadBalancer 

Once the type of service object is changed into `LoadBalancer`, TOAST Load Balancer is created out of the cluster, which is associated with load balancer and service object. By querying service object associated with the load balanacer, IP of the load balancer shows at **EXTERNAL-IP**. See [LoadBalancer 서비스](/Container/Kubernetes/en/user-guide/#loadbalancer) for the description of service objects of the `LoadBalancer` type.  

![dashboard-01.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/dashboard-01.png)

Change the type of the `kubernetes-dashboard` service object to `LoadBalancer`, like below:  

```
$ kubectl -n kube-system patch svc/kubernetes-dashboard -p '{"spec":{"type":"LoadBalancer"}}'
service/kubernetes-dashboard patched
```

After the type of service object `kubernetes-dashboard` is changed to `LoadBalancer`, you can check load balancer IP from the **EXTERNAL-IP**  field.  

```
$ kubectl get svc -n kube-system
NAME                   TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                  AGE
...
kubernetes-dashboard   LoadBalancer   10.254.95.176   123.123.123.81   443:30963/TCP            2d23h
```

> [Note]
> Find newly created load balancer on the **Network > Load Balancer** page. 
> Load balancer IP is a floating IP which is externally accessible. Find it on **Network > Floating IP**.

Access `https://{EXTERNAL-IP}` on the web browser to load the Kubernetes dashboard page. Tokens required for login are available at [Dashboard Access Token](/Container/Kubernetes/en/user-guide/#_23).

> [Note]
> Since Kubernetes dashboard is based on a private certificate that is automatically created, the page may be displayed as unsafe, depending on the web browser or security setting.  

#### Open Services with Ingress 

Ingress refers to the network object providing routing to access many services within a cluster. The setting of an ingress object runs by ingress controller. The `kubernetes-dashboard` service object can go public through ingress. See [Ingress Controller](/Container/Kubernetes/en/user-guide/#_16) regarding description on ingress and ingress controller. Below figure shows the structure of making dashboard public through ingress.
![dashboard-02.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/dashboard-02.png)

Install `NGINX Ingress Controller` in reference of the [Install NGINX Ingress Controller](/Container/Kubernetes/en/user-guide/#nginx-ingress-controller) and create service of the `LoadBalancer` type. Write manifest to create an ingress object, like below: 

```yaml
# kubernetes-dashboard-ingress-tls-passthrough.yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: k8s-dashboard-ingress
  namespace: kube-system
  annotations:
    ingress.kubernetes.io/ssl-passthrough: "true"
    kubernetes.io/ingress.allow-http: "false"
    kubernetes.io/ingress.class: nginx
    nginx.ingress.kubernetes.io/backend-protocol: HTTPS
    nginx.ingress.kubernetes.io/proxy-body-size: 100M
    nginx.ingress.kubernetes.io/rewrite-target: /
    nginx.org/ssl-backend: kubernetes-dashboard
spec:
  rules:
  - http:
      paths:
      - backend:
          serviceName: kubernetes-dashboard
          servicePort: 443
        path: /
  tls:
  - secretName: kubernetes-dashboard-certs
```

Apply manifest to create ingress, and check **EXTERNAL-IP** of the `ingress-nginx` service object. 

```
$ kubectl apply -f kubernetes-dashboard-ingress-tls-passthrough.yaml
ingress.extensions/k8s-dashboard-ingress created

$ kubectl get service/ingress-nginx -n ingress-nginx
NAME            TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)                      AGE
ingress-nginx   LoadBalancer   10.254.211.113   123.123.123.29   80:32680/TCP,443:31631/TCP   19h
```

Access `https://{EXTERNAL-IP}` on the web browser, and the Kubernetes dashboard page is loaded. See [Dashboard Access Token](/Container/Kubernetes/en/user-guide/#_23) for tokens required for login. 

### Dashboard Access Token 
Token is required to login Kubernetes dashboard. Get tokens with the following command: 

```
# SECRET_NAME=$(kubectl -n kube-system get secrets | grep "kubernetes-dashboard-token" | cut -f1 -d ' ')

$ kubectl describe secret $SECRET_NAME -n kube-system | grep -E '^token' | cut -f2 -d':' | tr -d " "
eyJhbGc...-QmXA
```

Enter printed token on the browser, and you can login as user with the administrator role. 


## Persistent Volume 
Persistent Volume or PV is a Kubernetes resource representing physical storage volume. One PV is attached to one TOAST Block Storage. For more details, see [Persistent Volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/). 

Persistent Volume Claims, or PVC is required to attach PV to pods. PVC defines necessary volume requirements, including volume and read/write modes. 

PV와 PVC로 사용자는 사용하고 싶은 볼륨의 속성을 정의하고, 시스템은 사용자의 요구 사항에 맞는 볼륨 리소스를 할당하는 방식으로 자원의 사용과 관리를 분리합니다. PV and PVC users 

### Life Cycle of PV/PVC 
PV와 PVC는 4단계의 생명 주기(life cycle)를 따릅니다.

* 프로비저닝(provisioning)
사용자가 직접 볼륨을 확보하고 PV를 생성(static provisioning)하거나 [스토리지 클래스](https://kubernetes.io/docs/concepts/storage/storage-classes/)를 사용해 동적으로 생성(dynamic provisioning)할 수 있습니다.

* 바인딩(binding)
PV와 PVC를 1:1로 바인딩합니다. 동적 프로비저닝으로 PV를 생성했다면 바인딩도 자동으로 수행됩니다.

* 사용(using)
PV를 파드에 마운트해 사용합니다.

* 반환(reclaiming)
사용을 마친 볼륨을 회수합니다. 회수 방법은 삭제(Delete), 보존(Retain), 재사용(Recycle)이 있습니다.

| Method | Description |
| --- | --- |
| 삭제(Delete) | PV를 삭제할 때 연결된 볼륨을 함께 삭제합니다. |
| 보존(Retain) | PV를 삭제할 때 연결된 볼륨을 삭제하지 않습니다. 볼륨은 사용자가 직접 삭제하거나 재사용 할 수 있습니다. |
| 재사용(Recycle) | PV를 삭제할 때 연결된 볼륨을 삭제하지 않고 재사용할 수 있는 상태로 만듭니다. 이 방법은 사용 중단(deprecated) 되었습니다. |


### 정적 프로비저닝 Static Provisioning 

정적 프로비저닝(static provisioning)은 사용자가 직접 블록 스토리지를 준비해야 합니다. TOAST 웹 콘솔의 **Storage > Block Storage** 서비스 페이지에서 **블록 스토리지 생성** 버튼을 클릭해 PV와 연결할 블록 스토리지를 생성합니다. 블록 스토리지 가이드의 [블록 스토리지 생성](/Storage/Block%20Storage/en/console-guide/#_2)을 참고하세요.

PV를 생성하려면 블록 스토리지의 ID가 필요합니다. **Storage > Block Storage** 서비스 페이지의 블록 스토리지 목록에서 사용할 블록 스토리지를 선택합니다. 하단 **정보** 탭의 블록 스토리지 이름 항목에서 ID를 확인할 수 있습니다.

> [Caution]
> 블록 스토리지와 파드를 구동할 노드 그룹 인스턴스의 가용성 영역이 같아야 합니다. 가용성 영역이 다르면 연결할 수 없습니다. 

스토리지 클래스 매니페스트를 작성합니다. TOAST Block Storage를 사용하려면 **provisioner**를 반드시 `kubernetes.io/cinder`로 설정해야 합니다.

```yaml
# storage_class.yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: sc-default
provisioner: kubernetes.io/cinder
```

스토리지 클래스를 생성하고 확인합니다.

```
$ kubectl apply -f storage_class.yaml
storageclass.storage.k8s.io/sc-default created

$ kubectl get sc
NAME         PROVISIONER            AGE
sc-default   kubernetes.io/cinder   8s
```

블록 스토리지와 연결할 PV 매니페스트를 작성합니다. **spec.storageClassName**에는 스토리지 클래스 이름을 입력합니다. TOAST Block Storage를 사용하려면 **spec.accessModes**는 반드시 `ReadWriteOnce`로 설정해야 합니다. **spec.presistentVolumeReclaimPolicy**는 `Delete` 또는 `Retain`으로 설정할 수 있습니다.

```yaml
# pv-static.yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-static-001
spec:
  capacity:
    storage: 10Gi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Delete
  storageClassName: sc-default
  cinder:
    fsType: "ext3"
    volumeID: "e6f95191-d58b-40c3-a191-9984ce7532e5"
```

PV를 생성하고 확인합니다.

```
$ kubectl apply -f pv-static.yaml
persistentvolume/pv-static-001 created

$ kubectl get pv -o wide
NAME            CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS   REASON   AGE   VOLUMEMODE
pv-static-001   10Gi       RWO            Delete           Available           sc-default              7s    Filesystem
```

생성한 PV를 사용하기 위한 PVC 매니페스트를 작성합니다. **spec.volumeName**에는 PV의 이름을 지정해야 합니다. 다른 항목들은 PV 매니페스트의 내용과 동일하게 설정합니다.

```yaml
# pvc-static.yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-static
  namespace: default
spec:
  volumeName: pv-static-001
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
  storageClassName: sc-default
```

PVC를 생성하고 확인합니다.

```
$ kubectl apply -f pvc-static.yaml
persistentvolumeclaim/pvc-static created

$ kubectl get pvc -o wide
NAME         STATUS   VOLUME          CAPACITY   ACCESS MODES   STORAGECLASS   AGE   VOLUMEMODE
pvc-static   Bound    pv-static-001   10Gi       RWO            sc-default     7s    Filesystem
```

PVC를 생성한 다음 PV의 상태를 조회해보면 **CLAIM** 항목에 PVC 이름이 지정되고, **STATUS** 항목이 `Bound`로 변경된 것을 확인할 수 있습니다.

```
$ kubectl get pv -o wide
NAME            CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                STORAGECLASS   REASON   AGE   VOLUMEMODE
pv-static-001   10Gi       RWO            Delete           Bound    default/pvc-static   sc-default              79s   Filesystem
```


### 동적 프로비저닝 Dynamic Provisioning 

동적 프로비저닝(dynamic provisioning)은 스토리지 클래스에 정의된 속성을 참조하여 자동으로 블록 스토리지를 생성합니다. 스토리지 클래스 매니페스트의 **parameters.type**에 TOAST Block Storage 유형을 지정할 수 있습니다. 지정하지 않으면 HDD 유형으로 설정됩니다.

| 타입 | 설정값 |
| --- | --- |
| HDD | General HDD |
| SSD | General SSD |

블록 스토리지는 노드 그룹과 같은 가용성 영역(availability zone)에 만들어야 연결할 수 있습니다. 스토리지 클래스 매니페스트의 **parameters.availability**에 블록 스토리지를 생성할 가용성 영역을 지정할 수 있습니다. 연결할 노드 그룹의 가용성 영역은 노드 그룹 목록에서 확인할 수 있습니다.

> [Caution 주의]
> 스토리지 클래스 매니페스트에 가용성 영역을 지정하지 않으면 임의의 가용성 영역에 블록 스토리지를 만듭니다. 블록 스토리지가 노드 그룹과 다른 가용성 영역에 생성되면 연결하지 못할 수 있으니 반드시 가용성 영역을 지정해야 합니다.

```yaml
# storage_class.yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: sc-ssd
provisioner: kubernetes.io/cinder
parameters:
  type: General SSD
  availability: kr-pub-a
```

동적 프로비저닝은 PV를 생성할 필요가 없습니다. 따라서 PVC 매니페스트에는 **spec.volumeName**를 설정하지 않습니다.

```yaml
# pvc-dynamic.yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-dynamic
  namespace: default
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
  storageClassName: sc-ssd
```

PVC를 생성하면 PV가 자동으로 생성됩니다. PV에 연결된 블록 스토리지도 자동으로 생성되며 TOAST 웹 콘솔 **Storage > Block Storage** 서비스 페이지의 블록 스토리지 목록에서 확인할 수 있습니다.

```
$ kubectl apply -f pvc-dynamic.yaml
persistentvolumeclaim/pvc-dynamic created

$ kubectl get sc,pv,pvc
NAME                                     PROVISIONER            AGE
storageclass.storage.k8s.io/sc-default   kubernetes.io/cinder   10m

NAME                                                        CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                 STORAGECLASS   REASON   AGE
persistentvolume/pvc-c63da3f9-dfcb-4cae-a9a9-67137994febc   10Gi       RWO            Delete           Bound    default/pvc-dynamic   sc-default              16s

NAME                                STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
persistentvolumeclaim/pvc-dynamic   Bound    pvc-c63da3f9-dfcb-4cae-a9a9-67137994febc   10Gi       RWO            sc-default     17s
```

> [Caution 주의]
> 동적 프로비저닝으로 생성된 블록 스토리지는 웹 콘솔에서 삭제할 수 없습니다. 또한 클러스터를 삭제할 때 자동으로 삭제되지 않습니다. 따라서 클러스터를 삭제하기 전에 PVC를 모두 삭제해야 합니다. PVC를 삭제하지 않고 클러스터를 삭제하면 과금이 될 수 있습니다. 동적 프로비저닝을 생성된 PVC의 reclaimPolicy는 기본적으로 `Delete`로 설정되기 때문에 PVC만 삭제해도 PV와 블록 스토리지가 삭제됩니다.


### 파드에 PVC 마운트 Mounting PVC to Pods 

파드에 PVC를 마운트하려면 파드 매니페스트에 마운트 정보를 정의해야 합니다. `spec.volumes.persistenVolumeClame.claimName`에 사용할 PVC 이름을 입력합니다. 그리고 `spec.containers.volumeMounts.mountPath`에 마운트할 경로를 입력합니다.

아래 예제는 정적 프로비저닝으로 생성한 PVC를 파드의 `/usr/share/nginx/html`에 마운트합니다.

```yaml
# pod-pvc.yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-with-static-pv
spec:
  containers:
    - name: web
      image: nginx
      ports:
        - name: web
          containerPort: 80
          hostPort: 8082
          protocol: TCP
      volumeMounts:
        - name: html-volume
          mountPath: "/usr/share/nginx/html"
  volumes:
    - name: html-volume
      persistentVolumeClaim:
        claimName: pvc-static
```

파드를 생성하고 블록 스토리지가 마운트되어 있는지 확인합니다.

```
$ kubectl apply -f pod-static-pvc.yaml
pod/nginx-with-static-pv created

$ kubectl get pods
NAME                   READY   STATUS    RESTARTS   AGE
nginx-with-static-pv   1/1     Running   0          50s

$ kubectl exec -ti nginx-with-static-pv -- df -h
Filesystem      Size  Used Avail Use% Mounted on
...
/dev/vdc        9.8G   23M  9.7G   1% /usr/share/nginx/html
...
```

TOAST 웹 콘솔 **Storage > Block Storage** 서비스 페이지에서도 블록 스토리지의 연결 정보를 확인할 수 있습니다.
