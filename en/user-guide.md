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
노드 그룹은 Kubernetes를 구성하는 워커 노드 인스턴스들의 그룹입니다. A node group is comprised of worker node instances that comprise a Kubernetes. 

### 노드 그룹 조회 Querying Node Groups 
Click a cluster name on the list to find the list of node groups. Select a node group and the information shows at the bottom.  클러스터 목록에서 클러스터 이름을 클릭하면 노드 그룹 목록을 확인할 수 있습니다. 노드 그룹을 선택하면 하단에 노드 그룹 정보가 나타납니다.

* 기본 정보 Basic Information
On the **Basic Information** tab, check the following: 탭에서는 다음과 정보를 확인할 수 있습니다.

| Item |Description |
| --- | --- |
| Name of Node Group 노드 그룹 이름 | Name and ID of a node group 노드 그룹 이름과 ID |
| Name of Cluster클러스터 이름 | Name and ID of a cluster to which a node group is included 노드 그룹이 속한 클러스터의 이름과 ID |
| Kubernetes Version 쿠버네티스 버전 | Kubernetes version in service 사용 중인 Kubernetes 버전 |
| Availability Area가용성 영역 | Area in which a node group instance is created 노드 그룹 인스턴스가 생성된 영역 |
| Instance Type 인스턴스 타입 | Specifications of a node group instance 노드 그룹 인스턴스 사양 |
| Image Type이미지 타입 | Type of image for a node group instance 노드 그룹 인스턴스에 사용한 이미지 종류 |
| Size of Block Storage블록 스토리지 크기 | Size of block storage for a node group instance 노드 그룹 인스턴스의 블록 스토리지 크기 |
| Created Date 생성일 | Time when node group was created 노드 그룹이 생성된 시각 |
| Modified Date수정일 | Last time when node group was modified 노드 그룹이 마지막으로 수정된 시각 |

* 노드 목록 List of Nodes 
Find the list of instances comprising a node group from the **List of Nodes노드 목록** tab. 탭에서는 노드 그룹을 구성하는 인스턴스의 목록을 확인할 수 있습니다.

### 노드 그룹 생성 Creating Node Groups 
When a cluster is created, a default node group is created, but more node groups may be created depending on the needs. If higher specifications are required to run a container, or more worker node instances are required to scale out, node groups may be additionally created. Click **Create Node Groups** from the page of node group list, and the page of creating a node group shows up. Following items are required to create a node group:  클러스터를 생성하면 기본 노드 그룹이 생성되지만, 필요에 따라 추가 노드 그룹을 만들 수 있습니다. 기본 노드 그룹의 인스턴스보다 높은 사양의 컨테이너 구동 환경이 필요하거나, 스케일 아웃(scale out, 확장)을 위해 더 많은 워커 노드 인스턴스가 필요한 경우 추가 노드 그룹을 생성해 사용할 수 있습니다. 노드 그룹 목록 페이지에서 **노드 그룹 생성** 버튼을 클릭하면 노드 그룹 생성 페이지가 나타납니다. 노드 그룹 생성에 필요한 항목은 다음과 같습니다.

| Item항목 | Description설명 |
| --- | --- |
| Availability Area 가용성 영역 | Area to create instances comprising a cluster 클러스터를 구성하는 인스턴스를 생성할 영역 |
| Name of Node Group 노드 그룹 이름 | Name of additional node group, comprised of alphabets, numbers, '-', and '.'로 구성 |
| Type of Instance 인스턴스 타입 | Specificiations of an instance for additional node group 추가 노드 그룹 인스턴스 사양 |
| Number of Nodes 노드 수 | Number of instances for additional node group 추가 노드 그룹 인스턴스 수 |
| Keypair 키 페어 | Keypair to access additional node group 추가 노드 그룹 접근에 사용할 키 페어 |
| Type of Block Storage 블록 스토리지 타입 | Type of block storage of instance for additional node group 추가 노드 그룹 인스턴스의 블록 스토리지 종류 |
| Size of Block Storage 스토리지 크기 | Size of block storage of instance for additional node group 추가 노드 그룹 인스턴스의 블록 스토리지 크기 |

필요한 정보를 입력하고 **노드 그룹 생성** 버튼을 클릭하면 노드 그룹 생성이 시작됩니다. 노드 그룹 목록에서 상태를 확인할 수 있습니다. 노드 그룹 생성하는 데는 약 5분 정도 걸립니다. 노드 그룹 설정에 따라 더 오래 걸릴 수도 있습니다. Enter information as required and click **Create Node Groups**, and a node group begins to be created. You may check status from the list of node groups. It takes about 5 minutes to create; more time may be required depending on the node group setting.  

### 노드 그룹 삭제Deleting Node Groups 
노드 그룹 목록에서 삭제하려는 노드 그룹을 선택하고 **노드 그룹 삭제** 버튼을 클릭하면 삭제가 진행됩니다. 노드 그룹 삭제하는 데는 약 5분 정도 걸립니다. 노드 그룹의 상태에 따라 더 오래 걸릴 수도 있습니다. Select a node group to delete from the list of node groups, and click **Delete Node Groups** and it is deleted. It takes about 5 minutes to delete a node group; more time may be required depending on the node group status. 

## 클러스터 관리 Cluster Management
원격의 호스트에서 클러스터를 조작하고 관리하려면 Kubernetes가 제공하는 명령줄 도구(CLI)인 `kubectl`이 필요합니다. To operate and manage clusters from a remote host, 'kubectl', which is the command line tool (CLI) as provided by Kubernetes, is required.

### kubectl 설치 Installing kubectl
kubectl은 특별한 설치 과정 없이 실행 파일을 다운로드해 바로 사용할 수 있습니다. 운영체제별 다운로드 경로는 다음과 같습니다. For kubectl, execution files can be downloaded and enabled, with no need of special installation procedure. Each operating system provides the following download path: 

| OS 운영체제 | Download Command 다운로드 커맨드 |
| --- | --- |
| Linux | curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/linux/amd64/kubectl |
| MacOS | curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/darwin/amd64/kubectl |
| Windows | curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/windows/amd64/kubectl.exe |

For more details on installation and optional items, see 그 외 설치 방법과 옵션 등 자세한 사항은 [Install and Set Up kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) 문서를 참고하세요.

#### 권한 변경 Role Changes
By default, downloaded files are not allowed to execute. The execution role must be added. 다운로드한 파일은 기본적으로 실행 권한이 없습니다. 실행 권한을 추가해야 합니다.

```
$ chmod +x kubectl
```

#### 위치 변경 또는 경로 지정 Change Location or Specify Path 
Change location to the path specified for an environment variable so as to execute kubectl on any path, or add the path including kubectl to an environment variable.  어느 경로에서든 kubectl을 실행할 수 있도록 환경 변수에 지정된 경로로 옮기거나, kubectl이 있는 경로를 환경 변수에 추가합니다.

* 환경 변수에 지정된 경로로 위치 변경 Change Loation to Path Specified for Environment Variable 
```
$ sudo mv kubectl /usr/local/bin/
```

* 환경 변수에 경로 추가 Add Path to Environment Variable 
```
// kubectl이 있는 경로에서 실행
$ export PATH=$PATH:$(pwd)
```

### 설정 Configuration 
kubectl로 Kubernetes 클러스터에 접근하려면 클러스터 설정 파일(kubeconfig)이 필요합니다. TOAST 웹 콘솔에서 **Container > Kubernetes** 서비스 페이지를 열고 접근할 클러스터를 선택합니다. 하단 **기본 정보** 탭에서 **설정 파일** 항목의 **다운로드** 버튼을 클릭해 설정 파일을 다운로드합니다. 다운로드한 설정 파일은 원하는 위치로 옮겨 kubectl 실행 시 참조할 수 있도록 준비합니다. To access Kubernetes cluster with kubectl, cluster configuration file (kubeconfig) is required. On TOAST web console, open **Container > Kubernetes** and select a cluster to access. From **Basic Information**, click **Download** of **Configuration Files** to download a configuration file. Changed the downloaded configuration file to a location of choice to serve as reference for kubectl execution. 

> [Caution]
> TOAST 웹 콘솔에서 다운로드한 설정 파일은 클러스터 정보와 인증을 위한 토큰 등이 포함되어 있습니다. 설정 파일이 있으면 해당 Kubernetes 클러스터에 접근할 수 있는 권한을 갖게 됩니다. 설정 파일을 절대로 분실하지 않도록 주의하시기 바랍니다. A configuration file downloaded from TOAST web console includes cluster information and token for authentication. With the file, you're authorized to access corresponding Kubernetes clusters. Take cautions for not losing configuration files.   

kubectl은 실행할 때마다 클러스터 설정 파일이 필요합니다. 따라서 매번 `--kubeconfig` 옵션을 이용해 클러스터 설정 파일을 지정해야 합니다. 그러나 환경 변수에 클러스터 설정 파일 경로가 저장되어 있다면 매번 옵션을 지정하지 않아도 됩니다. kubectl requires a cluster configuration file every time it is executed, so a cluster configuration file must be specified by using the `--kubeconfig` option. However, 

```
$ export KUBECONFIG={Path of cluster configuration file클러스터 설정 파일 경로}
```

클러스터 설정 파일 경로를 환경 변수에 저장하고 싶지 않다면 kubectl의 기본 설정 파일인 `$HOME/.kube/config`로 복사해 사용할 수도 있습니다. 그러나 클러스터를 여러 개 운영한다면 환경 변숫값을 변경하는 방법이 편리합니다. You may copy cluster configuration file path to `$HOME/.kube/config`, which is the default configuration file of kubectl, if you don't want to save it to an environment variable. However, when there are many clusters, it is easier to change environment variables. 

### 연결 확인 Confirming Connection 
See if it is well set by the `kubectl version` command. If there's no problem, 명령어로 정상 설정되었는지 확인합니다. 문제가 없다면 `Server Version`이 is printed.  출력됩니다.

```
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"15", GitVersion:"v1.15.7", GitCommit:"6c143d35bb11d74970e7bc0b6c45b6bfdffc0bd4", GitTreeState:"clean", BuildDate:"2019-12-11T12:42:56Z", GoVersion:"go1.12.12", Compiler:"gc", Platform:"darwin/amd64"}
Server Version: version.Info{Major:"1", Minor:"15", GitVersion:"v1.15.7", GitCommit:"6c143d35bb11d74970e7bc0b6c45b6bfdffc0bd4", GitTreeState:"clean", BuildDate:"2019-12-11T12:34:17Z", GoVersion:"go1.12.12", Compiler:"gc", Platform:"linux/amd64"}
```

* Client Version: 실행한 kubectl 파일의 버전 정보 Version information of executed kubectl file 
* Server Version: 클러스터를 구성하고 있는 Kubernetes 버전 정보 Kubernetes version information comprising a cluster 

## LoadBalancer 서비스
Kubernetes 애플리케이션의 기본 실행 단위인 파드(pod)는 CNI(Container Network Interface)로 클러스터 네트워크에 연결됩니다. 기본적으로 클러스터 외부에서 파드로는 접근할 수 없습니다. 파드의 서비스를 클러스터 외부에 공개하려면 Kubernetes의 `LoadBalancer` 서비스(Service) 객체(object)를 이용해 외부에 공개할 경로를 만들어야 합니다. LoadBalancer 서비스 객체를 만들면 클러스터 외부에 TOAST Load Balancer가 생성되어 서비스 객체와 연결됩니다. Pod is a basic executio unit of a Kubernetes application and it is connected to a cluster network via CNI (Container Network Interface). Basically, access to pod is unavailble from cluster externals. To open up pod services outside of a cluster, a path to be made public must be create by using Kubernetes' `LoadBalancer` 서비스(Service) 객체(object). 

### 웹 서버 파드 생성 Creating Web Server Pods 
다음과 같이 2개의 nginx 파드를 실행하는 디플로이먼트(deployment) 객체 매니페스트 파일을 작성하고 객체를 생성합니다. Write deployment object manifest file to execute the following two nginx pods and create an object. 

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

디플로이먼트 객체를 생성하면 매니페스트에 정의한 파드가 자동으로 생성됩니다. With a deployment object created, pods defined at manifest are automatically created. 

```
$ kubectl apply -f nginx.yaml
deployment.apps/nginx-deployment created

$ kubectl get pods
NAME                                READY   STATUS    RESTARTS   AGE  
nginx-deployment-7fd6966748-pvrzs   1/1     Running   0          4m13s
nginx-deployment-7fd6966748-wv7rd   1/1     Running   0          4m13s
```

만약 TOAST Container Registry에 저장한 이미지를 사용하고 싶다면 먼저 사용자 레지스트리에 로그인하기 위한 시크릿(secret)을 만들어야 합니다. To use images saved at TOAST Container Registry, first create a secret to login user registry. 

```
$ kubectl create secret docker-registry registry-credential --docker-server={user registry address} --docker-username={email address for Toast account} --docker-password={service or integrated Appkey}
secret/registry-credential created

$ kubectl get secrets
NAME                  TYPE                             DATA   AGE
registry-credential   kubernetes.io/dockerconfigjson   1      30m
```

디플로이먼트 매니페스트 파일에 시크릿 정보를 추가하고, 이미지 이름을 변경하면 사용자 레지스트리에 저장된 이미지를 이용해 파드를 만들 수 있습니다. By adding secret information to the deployment manifest file and changing the name of image, pods can be created by using images saved at user registry. 

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
> Regarding how to use TOAST Container Registry, see 사용 방법은 [User Guide for Container Registry](/Container/Container%20Registry/en/user-guide) 문서를 참고하세요.

### Creating LoadBalancer 서비스 생성
To define a service object of Kubernetes, a manifest comprised of the following items is required: 의 서비스 객체를 정의하려면 다음과 같은 항목으로 구성된 매니페스트가 필요합니다.

| Item | Description |
| --- | --- |
| metadata.name | Name of service object 서비스 객체의 이름 |
| spec.selector | Name of pod to be associated with service object 서비스 객체와 연결할 파드 이름 |
| spec.ports | Interface setting to deliver incoming traffic from external load balancer to a pod 외부 로드 밸런서에서 들어오는 트래픽을 파드에 전달할 인터페이스 설정 |
| spec.ports.name | Name of interface 인터페이스 이름 |
| spec.ports.protocol | Protocol for an interface 인터페이스에서 사용할 프로토콜(e.g: TCP) |
| spec.ports.port | Port number to go public out of service object 서비스 객체 외부에 공개할 포트 번호 |
| spec.ports.targetPort | Port number of a pod to be associated with service object 서비스 객체와 연결할 파드의 포트 번호 |
| spec.type | Type of service object 서비스 객체 유형 |

Service manifest is written like below. 다음과 같이 서비스 매니페스트를 작성합니다. The LoadBalancer service object is associated with a pod labelled as `app: nginx`, following the defined name at **spec.selector**. 서비스 객체는 **spec.selector**에 정의된 이름에 따라 `app: nginx` 레이블이 붙은 파드와 연결됩니다. 그리고 **spec.ports**에 정의된 대로 TCP/8080 포트로 들어온 트래픽을 파드의 TCP/80 포트로 전달합니다. And as **spec.ports** defines, traffic inflow via TCP/8080 is delivered to the TCP/80 port of the pod.  

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

LoadBalancer 서비스 객체를 생성하면 클러스터 외부에 로드 밸런서를 만들고 연결하기까지 약간의 시간이 필요합니다. 외부 로드 밸런서와 연결되기 전에는 **EXTERNAL-IP** 항목이 `<pending>`으로 표시됩니다. When the LoadBalancer service object is created, it takes some time to create and associate a load balancer externally. Before associated with external load balancer, **EXTERNAL-IP** shows `<pending>`. 

```
$ kubectl apply -f service.yaml
service/nginx-svc created

$ kubectl get service
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
nginx-svc    LoadBalancer   10.254.134.18   <pending>     8080:30013/TCP   11s
```

When it is associated with external load balancer, 외부 로드 밸런서와 연결되면 **EXTERNAL-IP** shows IP, which refers to floating IP of external load balancer. 항목에 IP가 표시됩니다. 이 IP는 외부 로드 밸런서의 플로팅 IP입니다.

```
$ kubectl get service
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)          AGE
nginx-svc    LoadBalancer   10.254.134.18   123.123.123.30   8080:30013/TCP   3m13s
```

> [Note]
> To find a load balancer that is created, visit 생성된 로드 밸런서는 **Network > Load Balancer** 페이지에서 확인할 수 있습니다.
> Load balancer IP is a floating IP allowing external access. Check out from 로드 밸런서의 IP는 외부에서 접근할 수 있는 플로팅 IP입니다. **Network > Floating IP** 페이지에서 확인할 수 있습니다.


### 인터넷을 통한 서비스 테스트 Testing Service on Internet 
로드 밸런서에 부착한 플로팅 IP로 HTTP 요청을 보내 Kubernetes 클러스터의 웹 서버 파드가 응답하는지 확인합니다. 서비스 객체의 TCP/8080 포트를 파드의 TCP/80 포트와 연결하도록 설정했기 때문에 TCP/8080 포트로 요청을 보내야 합니다. 외부 로드 밸런서와 서비스 객체, 파드가 잘 연결되었다면 웹 서버는 nginx 기본 페이지를 응답합니다. Send an HTTP request via floating IP associated with load balancer to see if the web server pod of a Kubernetes cluster responds. Since the TcP/8080 port of a service object is attached to TCP/80 port of a pod, request must be sent to the TCP/8080 port. If external load balancer, service object, and pod are well associated, the web server shall respond to nginx default page. 

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


## 인그레스 컨트롤러 Ingress Controller 
Ingress Controller routes HTTP and HTTPS requests from cluster externals to internal services, in reference of the rules that are defined at ingress object so as to provide SSL/TSL closure and virtual hosting. For more details on Ingress Controller and Ingress, see 인그레스 컨트롤러(ingress controller)는 인그레스(Ingress) 객체에 정의된 규칙을 참조하여 클러스터 외부에서 내부 서비스로 HTTP와 HTTPS 요청을 라우팅하고 SSL/TSL 종료, 가상 호스팅 등을 제공합니다. 인그레스 컨트롤러와 인그레스에 대한 자세한 내용은 [Ingress Controller](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/), [인그레스](https://kubernetes.io/docs/concepts/services-networking/ingress/) 문서를 참고하세요.


### NGINX Ingress Controller 설치 Installing NGINX Ingress Controller 
NGINX Ingress Controller is one of the most frequently used ingress controllers. For more details, see 는 많이 사용되는 인그레스 컨트롤러 중 하나입니다. 자세한 내용은 [NGINX Ingress Controller](https://kubernetes.github.io/ingress-nginx/)와 [NGINX Ingress Controller for Kubernetes](https://docs.nginx.com/nginx-ingress-controller/overview/) 문서를 참고하세요.

NGINX Ingress Controller provides pre-defined manifest files to readily create resources in need. With this manifest, resources can be easily created when required. 는 필요한 자원을 바로 생성할 수 있도록 미리 정의한 매니페스트 파일을 제공합니다. 이 매니페스트를 이용하면 쉽게 필요한 자원을 생성할 수 있습니다.

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

### LoadBalancer 서비스 생성 Creating LoadBalancer 
인그레스 컨트롤러 역시 파드로 생성되기 때문에 외부에 공개하기 위해서는 LoadBalancer 서비스 또는 NodePort 서비스를 만들어야 합니다. 다음과 같이 HTTP와 HTTPS를 처리할 수 있는 LoadBalancer 서비스 매니페스트를 정의합니다. Since ingress controller is created as a pod, LoadBalancer or NodePort must be created to be made public. The LoadBalancer service manifest is defined to process HTTP and HTTPS like below: 

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

After service object is created, check if it is associated with an external load balancer. The 서비스 객체를 생성하고 외부 로드 밸런서가 연결되어 있는지 확인합니다. **EXTERNAL-IP** field must include floating IP address setting. 필드에는 플로팅 IP 주소가 설정되어 있어야 합니다.

```
$ kubectl apply -f ingress-nginx-lb.yaml
service/ingress-nginx created

$ kubectl get svc -n ingress-nginx
NAME            TYPE           CLUSTER-IP     EXTERNAL-IP      PORT(S)                      AGE
ingress-nginx   LoadBalancer   10.254.2.128   123.123.123.41   80:30820/TCP,443:30269/TCP   39s
```

### URI 기반 서비스 분기 Diverging Service on URI 
인그레스 컨트롤러는 URI를 기반으로 서비스를 분기할 수 있습니다. 아래 그림은 URI를 기반으로 서비스를 분기하는 간단한 예제의 구조를 나타냅니다. Ingress controller can diverge services based on URI. Below figure shows the structure of a simple example of service divergence based on URI. 

![ingress-01.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/ingress-01.png)

#### 서비스와 파드 생성 Create Services and Pods 
Manifest is created to create services and pods like below:다음과 같이 서비스와 파드를 생성하기 위한 매니페스트를 작성합니다. Associate the `tea-svc` 서비스에는 `tea` pod to `tea-svc`, and 파드를 연결하고, `coffee-svc` 서비스에는 the `coffee` pod for `coffee-svc`. 파드를 연결합니다.

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

Apply manifest, and see if deployment, service, and pod is created. The pod must be **Running**. 매니페스트를 적용하고 디플로이먼트, 서비스, 파드가 생성되었는지 확인합니다. 파드는 **Running** 상태여야 합니다.

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

#### 인그레스(Ingress) 생성 Create Ingress
According to the request path, ingress manifest is created for service connection. A request with `/tea` as endpoint is connected to the `tea-svc` service, while `/coffee` is connected to the the `coffee-svc` service. 요청 경로에 따라 서비스를 연결하는 인그레스 매니페스트를 작성합니다. 엔드포인트가 `/tea`인 요청은 `tea-svc` 서비스에 연결하고 `/coffee`인 요청은 `coffee-svc` 서비스에 연결합니다.

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

인그레스를 생성하고 잠시 후 확인했을 때 **ADDRESS** 필드에 IP가 설정되어 있어야 합니다. In a while after ingress is created, IP must be configured at the **ADDRESS** field.  

```
$ kubectl apply -f cafe-ingress-uri.yaml
ingress.extensions/cafe-ingress-uri created

$ kubectl get ingress cafe-ingress-uri
NAME               HOSTS   ADDRESS          PORTS   AGE
cafe-ingress-uri   *       123.123.123.44   80      88s
```

#### HTTP 요청 전송 Send HTTP Requests 
Send HTTP request to the IP address set for **ADDRESS** of ingress for an external host, to check if the ingress has been properly set. 외부 호스트에서 ingress의 **ADDRESS** 필드에 설정된 IP 주소로 HTTP 요청을 전송해 인그레스가 올바르게 설정되었는지 확인합니다.

Request for 엔드포인트 `/coffee` as endpoint is sent to the 에 대한 요청은 `coffee-svc` service so as the 서비스에 전달되어 `coffee` pod can respond. From the  파드가 응답합니다. 응답의 **Server name**, you can see that  항목을 보면 `coffee` pods take turns to respond in the round-robin technique. 파드들이 라운드-로빈 방식으로 번갈아 응답하는 것을 확인할 수 있습니다.

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

Likewise, request for `/tea` as endpoint is delivered to the `tea-svc` service so as the `tea` can respond.   마찬가지로 엔드포인트 `/tea`에 대한 요청은 `tea-svc` 서비스에  전달되어 `tea` 파드가 응답합니다.

```
$ curl http://123.123.123.44/tea
Server address: 10.100.2.24:8080
Server name: tea-7df475c6-lxqsx
Date: 07/Apr/2020:08:25:03 +0000
URI: /tea
Request ID: 59303a5a5baa60802b463b1856c8ce8d
```

When a request is sent to undefined URI, the ingress controller sends `404 Not Found` as response.  정의되지 않은 URI로 요청을 보내면 인그레스 컨트롤러가 `404 Not Found`를 응답합니다.

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

#### 리소스 삭제 Delete Resources
Resources for testing can be deleted with used manifest.  테스트에 사용한 자원들은 생성할 때 사용한 매니페스트를 이용해 삭제할 수 있습니다.

```
$ kubectl delete -f cafe-ingress-uri.yaml
ingress.extensions "cafe-ingress-uri" deleted

$ kubectl delete -f cafe.yaml
deployment.apps "coffee" deleted
service "coffee-svc" deleted
deployment.apps "tea" deleted
service "tea-svc" deleted
```

### 호스트 기반 서비스 분기 Diverge Services on Host 
Ingress controller can diverge services based on the host name. Below figure shows the structure of a simple example of service divergence based on the host name. 인그레스 컨트롤러는 호스트 이름을 기반으로 서비스를 분기할 수 있습니다. 아래 그림은 호스트 이름을 기반으로 서비스를 분기하는 간단한 예제의 구조를 나타냅니다.

![ingress-02.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/ingress-02.png)

#### 서비스와 파드 생성 Create Services and Pods 
[URI 기반 서비스 분기](/Container/Kubernetes/en/user-guide/#uri)와 동일한 매니페스트를 이용해 서비스와 파드를 생성합니다. Create services and pods by using the same manifest as [URI 기반 서비스 분기](/Container/Kubernetes/en/user-guide/#uri). 

#### 인그레스 생성 Create Ingress 
호스트 이름에 따라 서비스를 연결하는 인그레스 매니페스트를 작성합니다. `tea.cafe.example.com` 호스트로 들어온 요청은 `tea-svc` 서비스에 연결하고 `coffee.cafe.example.com` 호스트로 들어온 요청은 `coffee-svc` 서비스에 연결합니다. Write the ingress manifest connecting services based on the host name. Incoming request via the `tea.cafe.example.com` host is connected to the `tea-svc` service, while request via the `coffee.cafe.example.com` host is connected to the `coffee-svc` service.      

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

인그레스를 생성하고 잠시 후 확인했을 때 **ADDRESS** 필드에 IP가 설정되어 있어야 합니다. In a while after ingress is created, IP must be configured at the **ADDRESS** field. 

```
$ kubectl apply -f cafe-ingress-host.yaml
ingress.extensions/cafe-ingress-host created

$ kubectl get ingress
NAME                HOSTS                                          ADDRESS          PORTS   AGE
cafe-ingress-host   tea.cafe.example.com,coffee.cafe.example.com   123.123.123.44   80      4m29s
```

#### Send HTTP Request 전송 
외부 호스트에서 인그레스의 ADDRESS에 설정된 IP로 HTTP 요청을 전송합니다. 다만 호스트 이름을 이용해 서비스를 분기하도록 인그레스를 구성했기 때문에 호스트 이름을 이용해 요청을 전송해야 합니다. HTTP request is sent from external host to IP configured at the ADDRESS of the ingress controller. Nevertheless, such request must be sent by using host name, since service divergence is based on the host name by configuration.

> [Note 참고]
> 임의의 호스트 이름을 사용하여 테스트하려면 curl의 --resolve 옵션을 사용합니다. --resolve 옵션은 `{호스트 이름}:{포트 번호}:{IP}` 형식으로 입력합니다. 이는 {호스트 이름}으로 보내는 {포트번호}에 대한 요청을 {IP}로 해석(resolve)하라는 의미입니다. To test with a random host name, use the --resolve option of curl: enter the --resolve option in the `{Host Name}:{Port Number}:{IP}`format. This means to resolve a request for {Port Number} to be sent to {Host Name} as {IP}. 
> `/etc/host` 파일을 열어 `{IP} {호스트 이름}` 형식으로 추가할 수도 있습니다. You may open up the `/etc/host` file and add `{IP} {Host Name}`. 

호스트 `coffee.cafe.example.com`로 요청을 전송하면 `coffee-svc` 서비스에 전달되어 `coffee` 파드가 응답합니다. When a request is sent to the `coffee.cafe.example.com` host, it is delivered to`coffee-svc` so that the `coffee` pod can respond.

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

When it is requested to an unknown host, the ingress controller sends `404 Not Found` as response.  알려지지 않은 호스트로 요청을 보내면 인그레스 컨트롤러가 `404 Not Found`를 응답합니다.

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

## Kubernetes 대시보드 Dashboard 
TOAST Kubernetes 서비스는 기본 웹 UI 대시보드(dashboard)를 제공합니다. Kubernetes 대시보드에 대한 자세한 내용은 [웹 UI (대시보드)](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/) 문서를 참고하세요. TOAST Kubernetes provides default web UI dashboard. For more details on Kubernetes Dashboard, see documents at [Web UI (Dashboard)](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/). 

### 대시보드 서비스 공개 Opening Dashboard Services
사용자 Kubernetes에는 대시보드를 공개하기 위한 `kubernetes-dashboard` 서비스 객체가 미리 생성되어 있습니다. User Kubernetes has the `kubernetes-dashboard` service object which has been already created to open dashboard. 

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

그러나 `kubernetes-dashboard` 서비스 객체는 ClusterIP 유형이기 때문에 아직 클러스터 외부에 공개되어 있지 않습니다. 대시보드를 외부 공개하려면 서비스 객체를 LoadBalancer 유형으로 변경하거나 인그레스 컨트롤러와 인그레스 객체를 생성해야 합니다. However, the `kubernetes-dashboard` object belongs to ClusterIP type and is not open out of the cluster. To open up dashboard externally, the service object type must be changed into LoadBalancer, or ingress controller and ingress object must be created.  

#### LoadBalancer 서비스 객체로 변경 Change into LoadBalancer 

`LoadBalancer` 유형으로 서비스 객체를 변경하면 클러스터 외부에 TOAST Load Balancer가 생성되고, 로드 밸런서와 서비스 객체와 연결됩니다. 로드 밸런서와 연결된 서비스 객체를 조회하면 **EXTERNAL-IP** 필드에 로드 밸런서의 IP가 표시됩니다. `LoadBalancer` 유형의 서비스 객체에 대한 설명은 [LoadBalancer 서비스](/Container/Kubernetes/en/user-guide/#loadbalancer)를 참고하세요. 아래 그림은 `LoadBalancer` 유형의 서비스를 이용해 대시보드를 외부에 공개하는 구조를 나타냅니다. Once the type of service object is changed into `LoadBalancer`, TOAST Load Balancer is created out of the cluster, which is associated with load balancer and service object. By querying service object associated with the load balanacer, IP of the load balancer shows at **EXTERNAL-IP**

![dashboard-01.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/dashboard-01.png)

다음과 같이 `kubernetes-dashboard` 서비스 객체의 유형을 `LoadBalancer`로 변경합니다. Change the type of the `kubernetes-dashboard` service object to `LoadBalancer`, like below:  

```
$ kubectl -n kube-system patch svc/kubernetes-dashboard -p '{"spec":{"type":"LoadBalancer"}}'
service/kubernetes-dashboard patched
```

`kubernetes-dashboard` 서비스 객체가 `LoadBalancer` 유형으로 변경되면 잠시 후 **EXTERNAL-IP** 필드에서 로드 밸런서 IP를 확인할 수 있습니다. After the service object `kubernetes-dashboard` is changed to the `LoadBalancer` type, you can check load balancer IP from the **EXTERNAL-IP**  field.  

```
$ kubectl get svc -n kube-system
NAME                   TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                  AGE
...
kubernetes-dashboard   LoadBalancer   10.254.95.176   123.123.123.81   443:30963/TCP            2d23h
```

> [Note참고]
> Find newly created load balancer on the  생성된 로드 밸런서는 **Network > Load Balancer** page. 페이지에서 확인할 수 있습니다.
> Load balancer IP is a floating IP which is externally accessible. Find it on the 로드 밸런서의 IP는 외부에서 접근할 수 있는 플로팅 IP입니다. **Network > Floating IP** 페이지에서 확인할 수 있습니다.

웹 브라우저에서 `https://{EXTERNAL-IP}`로 접속하면 Kubernetes 대시보드 페이지가 로딩됩니다. 로그인을 위해 필요한 토큰은 [대시보드 엑세스 토큰](/Container/Kubernetes/en/user-guide/#_23)을 참고하세요. Access `https://{EXTERNAL-IP}` on the web browser to load the Kubernetes dashboard page. Tokens required for login are available at [Dashboard Access Token](/Container/Kubernetes/en/user-guide/#_23).

> [Note]
> Since Kubernetes dashboard is based on a private certificate that is automatically created, the page may be displayed as unsafe, depending on the web browser or security setting.  대시보드는 자동 생성되는 사설 인증서를 사용하기 때문에 웹 브라우저의 종류와 보안 설정에 따라 안전하지 않은 페이지로 표시될 수 있습니다.

#### 인그레스(Ingress)를 이용한 서비스 공개 Open Services with Ingress 

인그레스는 클러스터 내부의 여러 서비스들로 접근하기 위한 라우팅을 제공하는 네트워크 객체입니다. 인그레스 객체의 설정은 인그래스 컨트롤러로 구동됩니다. `kubernetes-dashboard` 서비스 객체를 인그레스를 통해 공개할 수 있습니다. 인그레스와 인그레스 컨트롤러에 대한 설명은 [인그레스 컨트롤러](/Container/Kubernetes/en/user-guide/#_16)를 참고하세요. 아래 그림은 인그레스를 통해 대시보드를 외부에 공개하는 구조를 나타냅니다.Ingress refers to the network object providing routing to access many services within a cluster. The setting of an ingress object runs by ingress controller. The `kubernetes-dashboard` service object can go public through ingress. See [Ingress Controller](/Container/Kubernetes/en/user-guide/#_16) regarding description on ingress and ingress controller. Below figure shows the structure of making dashboard public through ingress.
![dashboard-02.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/dashboard-02.png)

[Install NGINX Ingress Controller 설치](/Container/Kubernetes/en/user-guide/#nginx-ingress-controller)를 참고해 `NGINX Ingress Controller`를 설치하고 `LoadBalancer` 유형의 서비스를 생성합니다. 그리고 다음과 같이 인그레스 객체 생성을 위한 매니페스트를 작성합니다. Install `NGINX Ingress Controller` in reference of the [Install NGINX Ingress Controller](/Container/Kubernetes/en/user-guide/#nginx-ingress-controller) and create service of the `LoadBalancer` type. Write manifest to create an ingress object, like below: 

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

매니페스트를 적용해 인그레스를 생성하고 `ingress-nginx` 서비스 객체의 **EXTERNAL-IP** 필드를 확인합니다. Apply the manifest to create ingress, and check **EXTERNAL-IP** of the `ingress-nginx` service object. 

```
$ kubectl apply -f kubernetes-dashboard-ingress-tls-passthrough.yaml
ingress.extensions/k8s-dashboard-ingress created

$ kubectl get service/ingress-nginx -n ingress-nginx
NAME            TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)                      AGE
ingress-nginx   LoadBalancer   10.254.211.113   123.123.123.29   80:32680/TCP,443:31631/TCP   19h
```

웹 브라우저에서 `https://{EXTERNAL-IP}`로 접속하면 Kubernetes 대시보드 페이지가 로딩됩니다. 로그인을 위해 필요한 토큰은 [대시보드 엑세스 토큰](/Container/Kubernetes/en/user-guide/#_23)을 참고하세요. Access `https://{EXTERNAL-IP}` on the web browser and the Kubernetes dashboard page is loaded. See [Dashboard Access Token](/Container/Kubernetes/en/user-guide/#_23) for tokens required for login. 

### 대시보드 엑세스 토큰 Dashboard Access Token 
Kubernetes 대시보드에 로그인하려면 토큰이 필요합니다. 토큰은 다음 명령으로 얻을 수 있습니다. Token is required to login Kubernetes dashboard. Get tokens with the following command: 

```
# SECRET_NAME=$(kubectl -n kube-system get secrets | grep "kubernetes-dashboard-token" | cut -f1 -d ' ')

$ kubectl describe secret $SECRET_NAME -n kube-system | grep -E '^token' | cut -f2 -d':' | tr -d " "
eyJhbGc...-QmXA
```

출력된 토큰을 브라우저의 토큰 입력 창에 입력하면 클러스터 관리자 권한을 부여받은 사용자로 로그인할 수 있습니다. Enter printed token on the browser, and you can login as user with the administrator role. 


## 퍼시스턴트 볼륨 Persistent Volume 
퍼시스턴트 볼륨(Persistent Volume, PV)는 물리 저장 장치(volume)를 표현하는 Kubernetes의 자원입니다. 하나의 PV는 하나의 TOAST Block Storage와 연결됩니다. 자세한 내용은 [퍼시스턴트 볼륨](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) 문서를 참고하세요. Persistent Volume or PV is a Kubernetes resource representing physical storage volume. One PV is attached to one TOAST Block Storage. For more details, see [Persistent Volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/). 

PV를 파드에 연결해 사용하려면 퍼시스턴트 볼륨 클레임(Persistent Volume Claims, PVC) 객체가 필요합니다. PVC는 용량, 읽기/쓰기 모드 등 필요한 볼륨의 요구 사항을 정의합니다. Persistent Volume Claims, PVC is required to attach PV to pods. PVC defines necessary volume requirements, including volume and read/write modes. 

PV와 PVC로 사용자는 사용하고 싶은 볼륨의 속성을 정의하고, 시스템은 사용자의 요구 사항에 맞는 볼륨 리소스를 할당하는 방식으로 자원의 사용과 관리를 분리합니다. PV and PVC users 

### PV/PVC의 생명 주기 Life Cycle of PV/PVC 
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
