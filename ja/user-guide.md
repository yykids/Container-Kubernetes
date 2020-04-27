## Container > Kubernetes > 사용 가이드

## kubectl 설치 및 설정
kubectl은 쿠버네티스가 제공하는 CLI tool로써 원격의 호스트에서 쿠버네티스 클러스터에 대한 조작이 가능하다. 이번 장에서는 호스트에 kubectl을 설치하고, 쿠버네티스 클러스터를 조작하는 방법에 대해 설명합니다.

### kubectl 설치
kubectl을 설치하는 과정을 설명합니다.

#### 파일 다운로드
kubectl은 단독 실행 파일 입니다. 그래서 특별한 설치 과정이 필요없고, 실행 파일을 다운로드 받아 사용할 수 있습니다. 운영체제 별 다운로드 받는 방법은 다음과 같습니다.

| 운영체제 | 다운로드 커맨드 |
| --- | --- |
| Linux | curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/linux/amd64/kubectl |
| MacOS | curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/darwin/amd64/kubectl |
| Windows | curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/windows/amd64/kubectl.exe |

그 외 설치 방법과 옵션 등 자세한 사항은 아래 링크를 참조하세요.
https://kubernetes.io/docs/tasks/tools/install-kubectl/

#### 퍼미션 변경
`curl`로 다운받은 파일은 기본적으로 실행권한이 주어지지 않습니다. 아래 커맨드로 다운로드 받은 `kubectl` 파일에 아래 실행 권한을 추가해 줍니다.
```
chmod +x kubectl
```

#### 위치 변경(선택)
어디에서나 `kubectl`을 실행할 수 있도록 `kubectl`을 적절한 위치로 옮겨줍니다.
```
mv kubectl /usr/local/bin/
```

혹은 현재 경로를 PATH 환경변수에 추가할 수도 있습니다.
```
export PATH=$PATH:$(pwd)
```


### kubectl 설정
kubectl의 설치만으로 클러스터에 접근할 수 없습니다. kubectl로 쿠버네티스 클러스터에 접근하기 위해서는 아래와 같은 설정이 필요합니다.

#### 설정 파일 다운로드
웹콘솔의 클러스터 조회 페이지로 이동하여 '설정 파일 다운로드' 버튼을 클릭하여 설정 파일을 다운로드 받습니다. 다운로드 받은 파일은 적절한 위치로 옮겨 kubectl 실행 시 참조할 수 있도록 준비합니다. 이 설정 파일을 흔히 kubeconfig라고 부릅니다.

(주의사항)
콘솔에서 다운받은 이 설정 파일은 클러스터에 대한 정보와 인증을 위한 토큰값 등이 포함되어 있습니다. 이 설정 파일이 있으면 해당 쿠버네티스 클러스터에 대한 권한을 갖게 됩니다. 따라서 이 파일을 절대로 분실하지 않도록 주의하시길 바랍니다.

#### 설정 파일을 kubectl에 적용
kubectl은 항상 kubeconfig 파일을 로드하여 동작합니다. 따라서 kubectl 실행 시 로드할 kubeconfig 파일을 지정해야 합니다. kubectl이 실행되면서 kubeconfig 파일의 위치를 찾는 방법은 다음과 같습니다.

##### KUBECONFIG 환경 변수
만약 `KUBECONFIG` 환경 변수에 kubeconfig 파일의 경로가 저장되어 있다면 kubectl은 이 파일을 사용합니다.
다음과 같이 `KUBECONFIG` 환경 변수를 설정할 수 있습니다.
```
export KUBECONFIG=다운받은파일경로
```

kubectl 실행 시 `KUBECONFIG` 환경 변수를 변수로 넘기는 방법도 있습니다.
```
KUBECONFIG=다운받은파일경로 kubectl get nodes
```

##### 기본 파일 위치
`KUBECONFIG` 환경변수가 설정되어 있지 않다면 kubectl은 `$HOME/.kube/config` 파일을 사용합니다. 물론, 파일이 존재하지 않는다면 사용하지 않습니다. 다운로드 받은 파일을 `$HOME/.kube/config` 파일에 복사해 사용할 수 있습니다.
```
cp -f 다운받은파일경로 ~/.kube/config`
kubectl get nodes
```

##### `--kubeconfig` 파라미터
kubectl 호출 시 `--kubeconfig` 파라미터로 kubeconfig를 지정할 수 있습니다.
```
kubectl --kubeconfig=다운받은파일경로 get nodes
```

#### 연결 확인
`kubectl version` 명령어로 정상 설정되었는지 확인합니다.

이 명령을 실행하면 두 가지 정보를 출력합니다. 클라이언트 정보는 kubectl 실행 바이너리의 버전 정보를 출력하고, 서버 정보는 쿠버네티스 클러스터에 적용되어 있는 쿠버네티스 정보를 출력합니다. 따라서 정상적으로 연결된 경우에만 서버 정보가 출력됩니다.

```
[~]# kubectl version
Client Version: version.Info{Major:"1", Minor:"15", GitVersion:"v1.15.7", GitCommit:"6c143d35bb11d74970e7bc0b6c45b6bfdffc0bd4", GitTreeState:"clean", BuildDate:"2019-12-11T12:42:56Z", GoVersion:"go1.12.12", Compiler:"gc", Platform:"darwin/amd64"}
Server Version: version.Info{Major:"1", Minor:"15", GitVersion:"v1.15.7", GitCommit:"6c143d35bb11d74970e7bc0b6c45b6bfdffc0bd4", GitTreeState:"clean", BuildDate:"2019-12-11T12:34:17Z", GoVersion:"go1.12.12", Compiler:"gc", Platform:"linux/amd64"}
[~]#
```





















## 로드밸런서 서비스 객체를 이용한 서비스 노출
pod는 쿠버네티스 클러스터 내부에 존재하고, CNI(Container Network Interface)에 의해 클러스터에 연결됩니다. 클러스터 외부에서 pod로의 네트워크 통신은 기본적으로 불가능한 상태로 만들어집니다. Pod에서 제공하는 서비스를 인터넷 혹은 클러스터 외부에 제공하기 위해서는 별도의 설정이 필요합니다. 이 문서에서는 쿠버네티스의 서비스 객체 중 로드밸런서 서비스 객체를 이용해 서비스를 외부에 노출하는 방법에 대해 설명합니다.

### 개념
쿠버네티스의 서비스 객체를 `LoadBalancer` 유형으로 생성하면 쿠버네티스 외부에 로드밸런서가 생성됩니다. 그리고 이 로드밸런서 서비스 객체와 외부 로드밸런서는 서로 매핑됩니다. 이 로드밸런서가 바로 "Network -> Load Balancer" 페이지에서 확인할 수 있는 로드밸런서 객체 입니다. 즉, 쿠버네티스의 로드밸런서 서비스 객체를 생성하면 로드밸런서가 생성되어 Pod의 서비스를 외부에 노출 할 수 있게 됩니다.

### 로드밸런서 서비스를 이용한 웹 서비스 노출
로드밸런서 서비스 객체를 이용해 Pod의 웹 서비스를 노출하는 방법에 대해 설명합니다.

#### 서비스를 위한 웹서버 pod 실행
먼저, 테스트를 위해 웹서버 pod를 실행합니다. 아래의 yaml 파일을 이용해 Deployment 객체를 생성할 수 있습니다.
```
[service-lb-test]# cat nginx.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
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
[service-lb-test]#
[service-lb-test]# kubectl apply -f nginx.yaml
deployment.apps/nginx-deployment created
[service-lb-test]#
```

pod가 생성되어 `Running` 상태가 된 것을 확인합니다.
```
[service-lb-test]# kubectl get pods -o wide
NAME                                READY   STATUS    RESTARTS   AGE     IP           NODE                                    NOMINATED NODE   READINESS GATES
nginx-deployment-7fd6966748-pvrzs   1/1     Running   0          4m13s   10.100.3.4   twtest3-added-iqugtvla3klc-node-0       <none>           <none>
nginx-deployment-7fd6966748-wv7rd   1/1     Running   0          4m13s   10.100.2.8   twtest3-default-w-pmxhlw3kwuph-node-0   <none>           <none>
nginx-deployment-7fd6966748-xd8lh   1/1     Running   0          4m13s   10.100.3.3   twtest3-added-iqugtvla3klc-node-0       <none>           <none>
[service-lb-test]#
```

만약 TOAST Container Registry에 저장한 이미지를 사용하고 싶다면 먼저 사용자 레지스트리에 로그인하기 위한 시크릿(secret)을 만들어야 합니다.
```
# kubectl create secret docker-registry regcred --docker-server={사용자 레지스트리 주소} --docker-username={Toast 계정 email 주소} --docker-password={서비스 Appkey 또는 통합 Appkey}
secret/regcred created

# kubectl get secrets
NAME                  TYPE                                  DATA   AGE
regcred               kubernetes.io/dockerconfigjson        1      30m
```

Deployment 생성을 위한 매니패스트 파일에 시크릿 정보를 추가하고, 이미지 경로를 수정하면 사용자 레지스트리에 저장된 이미지를 이용해 팟을 만들 수 있습니다.
```
# cat nginx.yaml
...
spec:
  ...
  template:
    ...
    spec:
      containers:
      - name: nginx
        image: {사용자 레지스트리 주소}/nginx:1.14.2
        ...
      imagePullSecrets:
      - name: regcred

```

> [참고]
> TOAST Container Registry 사용 방법은 [Container Registry 사용 가이드](/Container/Container%20Registry/ja/user-guide) 문서를 참조하세요.

#### 웹서버를 외부에 노출하기 위한 로드밸런서 서비스 객체 생성

쿠버네티스의 서비스 객체를 생성할 때 다음의 필드를 사용해 서비스 객체를 정의합니다.
* .metadata.name: 이 서비스 객체의 이름을 정의합니다.
* .spec
    * .selector: 이 서비스가 연결될 Pod를 결정합니다.
    * .ports: 로드밸런서에서 트래픽을 받아 pod에 전달할 인터페이스를 정의합니다.
        * .name: 이 가상포트에 이름을 정의합니다.
        * .protocol: 프로토콜 이름(예: TCP) 입니다.
        * .port: 서비스 객체의 외부에 노출할 포트번호 입니다.
        * .targetPort: 서비스 객체와 연결된 Pod가 노출할 포트번호 입니다.
    * .type: 로드밸런서 유형으로 생성하기 위해서는 `LoadBalancer`로 지정해야 합니다.

아래의 yaml 파일을 이용해 로드밸런서 서비스 객체를 생성할 수 있습니다. 이 로드밸런서 서비스 객체는 `.spec.selector` 필드에 의해 "app: nginx"라는 라벨이 붙은 Pod와 연동합니다. 또, `.spec.ports` 필드에 의해 TCP/8080으로 들어온 트래픽을 Pod의 TCP/80으로 전달합니다.

```
[service-lb-test]# cat service.yaml
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
[service-lb-test]#
[service-lb-test]# kubectl apply -f service.yaml
service/nginx-svc created
[service-lb-test]#
```

서비스 객체가 생성되면 `kubectl get service` 명령어로 서비스 객체 목록을 조회할 수 있습니다. 단, 로드밸런서 서비스 객체가 생성되더라도 클러스터 외부의 로드밸런서를 생성하고 연동하는데에는 약간의 시간이 필요합니다. 외부 로드밸런서와 연동하는 중에는 `EXTERNAL-IP` 컬럼에 다음과 같이 `<pending>`이라고 표시됩니다.
```
[service-lb-test]# kubectl get service
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
kubernetes   ClusterIP      10.254.0.1      <none>        443/TCP          51m
nginx-svc    LoadBalancer   10.254.134.18   <pending>     8080:30013/TCP   11s
[service-lb-test]#
```

잠시 시간이 지나면 `EXTERNAL-IP` 컬럼에 IP 주소가 설정된 것을 확인하실 수 있습니다. 이 IP 주소는 Floating IP 주소 입니다. 이 Floating IP 주소는 "Network -> Floating IP" 페이지에서 확인하실 수 있습니다.
```
[service-lb-test]# kubectl get service
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)          AGE
kubernetes   ClusterIP      10.254.0.1      <none>           443/TCP          54m
nginx-svc    LoadBalancer   10.254.134.18   133.186.154.30   8080:30013/TCP   3m13s
[service-lb-test]#
```

#### 인터넷을 통해 서비스 테스트
인터넷에 연결된 호스트에서 쿠버네티스 클러스터의 웹서버 Pod에 접속 테스트를 수행합니다. 로드밸런서의 Floating IP주소로 HTTP 요청을 보내 응답을 제대로 받아오는지 확인하는 것 입니다.

아래와 같이 Floating IP의 TCP/80으로 HTTP 요청을 보내면 다음과 같이 에러가 발생합니다. 서비스 객체가 TCP/8080을 열고 기다리기 때문에 TCP/80으로 보낸 요청은 연결에 실패하는 것입니다.
```
[service-lb-test]# curl http://133.186.154.30
curl: (7) Failed to connect to 133.186.154.30 port 80: Connection refused
[service-lb-test]#
```

아래와 같이 Floating IP의 TCP/8080으로 HTTP 요청을 보내면 정상 응답을 받습니다. TCP/8080으로 보내진 요청을 서비스 객체가 Pod으로 연결할 때 TCP/80으로 바꾸었기 때문에 Pod가 서비스하는 TCP/80으로 연결될 수 있는 것 입니다.
```
[service-lb-test]# curl http://133.186.154.30:8080
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
[service-lb-test]#
```










## nginx ingress controller 설치 및 사용 예제
이 장에서는 많이 사용되는 Ingress controller 중의 하나인 Nginx ingress controller를 클러스터에 설치하는 방법에 대해 설명합니다. 또 Ingress를 이용하여 서비스를 분기하는 방법에 대한 예제를 보여드립니다.

### Nginx Ingress Controller 설치 방법
이 장에서는 Nginx ingress controller를 설치하는 방법에 대해 기술합니다.
<br>
좀 더 자세한 사항은 아래 링크를 참고하세요.
- https://kubernetes.github.io/ingress-nginx/deploy/
- https://docs.nginx.com/nginx-ingress-controller/installation/installation-with-manifests/


#### 필요 리소스 설치
다음과 같이 Nginx ingress controller에 필요한 리소스를 생성합니다.
```
[nginx-ingress-test]# kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/nginx-0.30.0/deploy/static/mandatory.yaml
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
[nginx-ingress-test]#
```

#### LoadBalancer 생성
Ingress를 외부에 노출하기 위해서는 로드밸런서(LoadBalancer) 서비스 혹은 노드포트(NodePort) 서비스를 생성해야 합니다. 이 문서에서는 로드밸런서 서비스를 생성하여 Ingress를 외부에 노출하도록 합니다.

다음과 같이 HTTP와 HTTPS를 처리할 수 있는 로드밸런서 서비스 객체를 생성합니다.
```
[nginx-ingress-test]# cat ingress-nginx-lb.yaml
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

[nginx-ingress-test]# kubectl apply -f ingress-nginx-lb.yaml
service/ingress-nginx created
[nginx-ingress-test]#
```

위에서 생성한 `ingress-nginx` 서비스가 제대로 생성되었는지 확인합니다. `EXTERNAL-IP` 필드에는 IP 주소가 설정되어 있음을 확인해야 합니다.
```
[nginx-ingress-test]# kubectl get svc -o wide -n ingress-nginx
NAME            TYPE           CLUSTER-IP     EXTERNAL-IP      PORT(S)                      AGE   SELECTOR
ingress-nginx   LoadBalancer   10.254.2.128   133.186.154.41   80:30820/TCP,443:30269/TCP   39s   app.kubernetes.io/name=ingress-nginx,app.kubernetes.io/part-of=ingress-nginx
[nginx-ingress-test]#
```

### 예제 1. URI 기반 서비스 분기 Ingress
이번 예제는 URI에 기반하여 서비스를 분기하는 예제 입니다.
![ingress-01.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/ingress-01.png)


#### Service 및 Pod 생성
다음과 같이 테스트를 위한 `tea-svc` 서비스와 `coffee-svc` 서비스를 생성합니다. `tea-svc` 서비스에는 `tea` pod이 연결되고, `coffee-svc` 서비스에는 `coffee`  pod가 연결됩니다.

```
[nginx-ingress-test]# cat cafe.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: coffee
spec:
  replicas: 2
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
  replicas: 3
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
[nginx-ingress-test]#
[nginx-ingress-test]# kubectl apply -f cafe.yaml
deployment.apps/coffee created
service/coffee-svc created
deployment.apps/tea created
service/tea-svc created
[nginx-ingress-test]#
```

생성된 Deployment, Service, Pods가 정상적으로 생성되었는지 확인합니다. 특히 Pods의 경우 `Running` 상태인 것을 확인하셔야 합니다.
```
[nginx-ingress-test]# kubectl get deploy,svc,pods
NAME                           READY   UP-TO-DATE   AVAILABLE   AGE
deployment.extensions/coffee   2/2     2            2           18s
deployment.extensions/tea      3/3     3            3           18s

NAME                 TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
service/coffee-svc   ClusterIP   10.254.51.117    <none>        80/TCP    18s
service/kubernetes   ClusterIP   10.254.0.1       <none>        443/TCP   29h
service/tea-svc      ClusterIP   10.254.210.170   <none>        80/TCP    18s

NAME                          READY   STATUS    RESTARTS   AGE
pod/coffee-67c6f7c5fd-98vh5   1/1     Running   0          18s
pod/coffee-67c6f7c5fd-c58l2   1/1     Running   0          18s
pod/tea-7df475c6-dmxf6        1/1     Running   0          18s
pod/tea-7df475c6-gtlx5        1/1     Running   0          18s
pod/tea-7df475c6-lxqsx        1/1     Running   0          18s
[nginx-ingress-test]#
```

#### URI를 기반으로 서비스와 연결하는 Ingress 생성
다음과 같이 URI를 기반으로 서비스와 연결하는 Ingress를 생성합니다.
- URI `/tea` 로의 요청은 `tea-svc` 서비스에 연결
- URI `/coffee`로의 요청은 `coffee-svc` 서비스에 연결

```
[nginx-ingress-test]# cat cafe-ingress-uri.yaml
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
[nginx-ingress-test]#
[nginx-ingress-test]# kubectl apply -f cafe-ingress-uri.yaml
ingress.extensions/cafe-ingress-uri created
[nginx-ingress-test]#
```

생성된 ingress가 `ADDRESS`를 제대로 받아오는지 확인해야 합니다.
```
[nginx-ingress-test]# kubectl get ingress cafe-ingress-uri
NAME               HOSTS   ADDRESS   PORTS   AGE
cafe-ingress-uri   *                 80      20s
[nginx-ingress-test]#
[nginx-ingress-test]# kubectl get ingress cafe-ingress-uri
NAME               HOSTS   ADDRESS          PORTS   AGE
cafe-ingress-uri   *       133.186.154.44   80      88s
[nginx-ingress-test]#
```

#### HTTP Request 전송
외부 호스트에서 ingress의 `ADDRESS` 필드에 설정된 IP 주소로 HTTP request를 전송합니다.

##### 1. 정의되지 않은 URI
정의되지 않은 URI에 대한 요청은 `404 Not Found`를 리턴합니다.
```
[~]# curl http://133.186.154.44/
<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.17.8</center>
</body>
</html>
[~]#
[~]# curl http://133.186.154.44/invalid_uri
<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.17.8</center>
</body>
</html>
[~]#
```

##### 2. `/coffee` 요청
`/coffee`에 대한 요청은 "coffee service"에 전달되어 서비스 됩니다. 아래 실행 로그 중 `Server name`을 유심히 보시면, coffee service에 연결된 Pod이 라운드로빈으로 동작하고 있음을 확인하실 수 있습니다.

```
[~]# curl http://133.186.154.44/coffee
Server address: 10.100.3.48:8080
Server name: coffee-67c6f7c5fd-c58l2
Dat#e: 07/Apr/2020:08:24:27 +0000
URI: /coffee
Request ID: e831901e441303ad59fb02214c49d84a
[~]#
[~]# curl http://133.186.154.44/coffee
Server address: 10.100.2.23:8080
Server name: coffee-67c6f7c5fd-98vh5
Date: 07/Apr/2020:08:24:28 +0000
URI: /coffee
Request ID: e78427e68a1cd61ec633b9328359874e
[~]#
[~]# curl http://133.186.154.44/coffee
Server address: 10.100.3.48:8080
Server name: coffee-67c6f7c5fd-c58l2
Date: 07/Apr/2020:08:24:42 +0000
URI: /coffee
Request ID: cd5813933d6389032c18e5cfb5ad9df4
[~]#
```

##### 3. `/tea` 요청
`/tea`에 대한 요청은 "tea service"에 전달되어 서비스 됩니다. 아래 실행 로그 중 `Server name`을 유심히 보시면, "tea service"에 연결된 Pod이 라운드로빈으로 동작하고 있음을 확인하실 수 있습니다.

```
[~]# curl http://133.186.154.44/tea
Server address: 10.100.2.24:8080
Server name: tea-7df475c6-lxqsx
Date: 07/Apr/2020:08:25:03 +0000
URI: /tea
Request ID: 59303a5a5baa60802b463b1856c8ce8d
[~]#
[~]# curl http://133.186.154.44/tea
Server address: 10.100.3.50:8080
Server name: tea-7df475c6-dmxf6
Date: 07/Apr/2020:08:25:04 +0000
URI: /tea
Request ID: 81683a1d9e9a5ed46fed3f597958e9d3
[~]#
[~]# curl http://133.186.154.44/tea
Server address: 10.100.3.49:8080
Server name: tea-7df475c6-gtlx5
Date: 07/Apr/2020:08:25:05 +0000
URI: /tea
Request ID: 2b348f7615133ef1f99c2c4625260a68
[~]#
[~]# curl http://133.186.154.44/tea
Server address: 10.100.2.24:8080
Server name: tea-7df475c6-lxqsx
Date: 07/Apr/2020:08:25:10 +0000
URI: /tea
Request ID: 7d6a7c1858424400f481057a75e8a263
[~]#
```

#### 테스트 용 리소스 삭제
다음과 같이 테스트를 위해 생성한 리소스를 삭제할 수 있습니다.
```
[nginx-ingress-test]# kubectl delete -f cafe-ingress-uri.yaml
ingress.extensions "cafe-ingress-uri" deleted
[nginx-ingress-test]# kubectl delete -f cafe.yaml
deployment.apps "coffee" deleted
service "coffee-svc" deleted
deployment.apps "tea" deleted
service "tea-svc" deleted
[nginx-ingress-test]#
```

### 예제 2. 호스트 기반 서비스 분기 Ingress
이번 예제는 호스트 이름에 기반하여 서비스를 분기하는 예제 입니다.
![ingress-02.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/ingress-02.png)

#### Service 및 Pod 생성
예제1과 동일한 Service 및 Pod를 사용합니다.

#### 호스트를 기반으로 서비스와 연결하는 Ingress 생성
다음과 같이 URI를 기반으로 서비스와 연결하는 Ingress를 생성합니다.
- Host `tea.cafe.example.com`으로의 요청은 `tea-svc` 서비스에 연결
- Host `coffee.cafe.example.com`으로의 요청은 `tea-svc` 서비스에 연결

```
[nginx-ingress-test]# cat cafe-ingress-host.yaml
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
[nginx-ingress-test]#
[nginx-ingress-test]# kubectl apply -f cafe-ingress-host.yaml
ingress.extensions/cafe-ingress-host created
[nginx-ingress-test]#
```

생성된 ingress가 ADDRESS를 제대로 받아오는지 확인해야 합니다.
```
[nginx-ingress-test]# kubectl get ingress
NAME                HOSTS                                          ADDRESS   PORTS   AGE
cafe-ingress-host   tea.cafe.example.com,coffee.cafe.example.com             80      7s
[nginx-ingress-test]#
[nginx-ingress-test]#
[nginx-ingress-test]# kubectl get ingress
NAME                HOSTS                                          ADDRESS          PORTS   AGE
cafe-ingress-host   tea.cafe.example.com,coffee.cafe.example.com   133.186.154.44   80      4m29s
[nginx-ingress-test]#
```



#### HTTP Request 전송
외부 호스트에서 ingress의 ADDRESS에 설정된 IP 주소로 HTTP request를 전송합니다. 다만 호스트에 기반한 HTTP Request를 보내야 합니다.

(참고)
임의의 호스트 이름을 사용하여 테스트 하기 위해 `curl`의 `--resolve` 옵션을 사용합니다. `--resolve` 옵션은 `호스트이름:포트번호:IP주소`의 형식으로 입력합니다. 이는 "호스트이름"으로 보내는 "포트번호"에 대한 요청은 "IP주소"로 해석(resolve)하라는 의미 입니다.

##### 1. Unknown host
알려지지 않은 호스트에 대한 요청은 `404 Not Found`를 리턴합니다.
```
[~]# curl http://133.186.154.44
<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.17.8</center>
</body>
</html>
[~]#
[~]# curl --resolve test.example.com:80:133.186.154.44 http://test.example.com/
<html>
<head><title>404 Not Found</title></head>
<body>
<center><h1>404 Not Found</h1></center>
<hr><center>nginx/1.17.8</center>
</body>
</html>
[~]#
```

##### 2. `coffee.cafe.example.com`으로 요청
호스트 `coffee.cafe.example.com`에 대한 요청은 `coffee-svc` 서비스에 전달됩니다. 아래 실행 로그 중 `Server name`을 유심히 보시면, `coffee-svc` 서비스에 연결된 Pod이 라운드로빈으로 동작하고 있음을 확인하실 수 있습니다.

```
[~]# curl --resolve coffee.cafe.example.com:80:133.186.154.44 http://coffee.cafe.example.com/
Server address: 10.100.2.25:8080
Server name: coffee-67c6f7c5fd-2bbzf
Date: 07/Apr/2020:08:45:39 +0000
URI: /
Request ID: 29fd8a244b9f0a5ff5f35d1dc35edccf
[~]#
[~]# curl --resolve coffee.cafe.example.com:80:133.186.154.44 http://coffee.cafe.example.com/
Server address: 10.100.3.51:8080
Server name: coffee-67c6f7c5fd-j7zrr
Date: 07/Apr/2020:08:45:40 +0000
URI: /
Request ID: 54cae1d825fa8c3ffed6c03959507bb8
[~]#
[~]# curl --resolve coffee.cafe.example.com:80:133.186.154.44 http://coffee.cafe.example.com/
Server address: 10.100.2.25:8080
Server name: coffee-67c6f7c5fd-2bbzf
Date: 07/Apr/2020:08:45:41 +0000
URI: /
Request ID: f47cf9f4ee725fca440a7d50630cb25a
[~]#
```

##### 3. `tea.cafe.example.com`으로 요청
호스트 `tea.cafe.example.com`에 대한 요청은 `tea-svc` 서비스에 전달됩니다. 아래 실행 로그 중 `Server name`을 유심히 보시면, `tea-svc` 서비스에 연결된 Pod이 라운드로빈으로 동작하고 있음을 확인하실 수 있습니다.

```
[~]# curl --resolve tea.cafe.example.com:80:133.186.154.44 http://tea.cafe.example.com/
Server address: 10.100.3.52:8080
Server name: tea-7df475c6-q8mdx
Date: 07/Apr/2020:08:53:44 +0000
URI: /
Request ID: fe61c1589d3ab8ef4ca4507245251ef3
[~]#
[~]# curl --resolve tea.cafe.example.com:80:133.186.154.44 http://tea.cafe.example.com/
Server address: 10.100.3.53:8080
Server name: tea-7df475c6-llb6w
Date: 07/Apr/2020:08:53:46 +0000
URI: /
Request ID: cbca786ef9c0a11cd80d690f387f7286
[~]#
[~]# curl --resolve tea.cafe.example.com:80:133.186.154.44 http://tea.cafe.example.com/
Server address: 10.100.2.26:8080
Server name: tea-7df475c6-znz2n
Date: 07/Apr/2020:08:53:47 +0000
URI: /
Request ID: bd27447451135b112297640575d8449c
[~]#
[~]# curl --resolve tea.cafe.example.com:80:133.186.154.44 http://tea.cafe.example.com/
Server address: 10.100.3.52:8080
Server name: tea-7df475c6-q8mdx
Date: 07/Apr/2020:08:53:49 +0000
URI: /
Request ID: 58d26bdc750de30c0c4370bc1b641fd0
[~]#
```


#### 테스트 용 리소스 삭제
다음과 같이 테스트를 위해 생성한 리소스를 삭제할 수 있습니다.
```
[nginx-ingress-test]# kubectl delete -f cafe-ingress-host.yaml
ingress.extensions "cafe-ingress-host" deleted
[nginx-ingress-test]# kubectl delete -f cafe.yaml
deployment.apps "coffee" deleted
service "coffee-svc" deleted
deployment.apps "tea" deleted
service "tea-svc" deleted
[nginx-ingress-test]#
```






## 쿠버네티스 대시보드 활성화
이 장에서는 쿠버네티스 대시보드를 활성화하고 사용하는데 필요한 과정을 설명합니다.

<br>

쿠버네티스 대시보드에 대한 자세한 내용은 아래 링크를 참고해주세요.
https://kubernetes.io/ko/docs/tasks/access-application-cluster/web-ui-dashboard/

### 대시보드 권한 설정
대시보드 사용자에게 권한을 부여합니다. 이 예제에서는 모든 권한을 부여하도록 합니다.

```
[~]# kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
clusterrolebinding.rbac.authorization.k8s.io/kubernetes-dashboard created
[~]#
[~]# kubectl describe clusterrolebinding kubernetes-dashboard -n kube-system
Name:         kubernetes-dashboard
Labels:       <none>
Annotations:  <none>
Role:
  Kind:  ClusterRole
  Name:  cluster-admin
Subjects:
  Kind            Name                  Namespace
  ----            ----                  ---------
  ServiceAccount  kubernetes-dashboard  kube-system
[~]#
[~]# kubectl describe ClusterRole cluster-admin
Name:         cluster-admin
Labels:       kubernetes.io/bootstrapping=rbac-defaults
Annotations:  rbac.authorization.kubernetes.io/autoupdate: true
PolicyRule:
  Resources  Non-Resource URLs  Resource Names  Verbs
  ---------  -----------------  --------------  -----
  *.*        []                 []              [*]
             [*]                []              [*]
[~]#
```

### 서비스 노출
쿠버네티스 대시보드를 위해 `kubernetes-dashboard`라는 서비스 객체가 미리 생성되어 있습니다.
```
[~]# kubectl get svc kubernetes-dashboard -n kube-system
NAME                   TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
kubernetes-dashboard   ClusterIP   10.254.95.176   <none>        443/TCP   2d4h
[~]# kubectl describe svc kubernetes-dashboard -n kube-system
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
이 Service 객체는 `ClusterIP` type으로 생성되어 있어 사실상 이 자체로는 외부에 노출할 수 없습니다. 이 문서에서는 다음 두 가지 방법으로 쿠버네티스 대시보드 서비스를 외부에 노출하는 방법에 대해 설명합니다.
* 방법1. LoadBalancer를 이용해 서비스 노출
* 방법2. Ingress를 이용해 서비스 노출


#### 방법1. LoadBalancer를 이용해 서비스 노출
이번 절에서는 로드밸런서 서비스 객체를 이용해 쿠버네티스 대시보드를 외부에 노출하는 방법에 대해 설명합니다.

##### 개념
![dashboard-01.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/dashboard-01.png)
로드밸런서 서비스 객체를 생성하면 클러스터 외부에 로드밸런서가 생성되고, 이 로드밸런서와 서비스 객체가 연결됩니다. 로드밸런서의 IP 주소는 서비스 객체 조회 시 `EXTERNAL-IP` 필드로 표시됩니다. 외부에서는 이 IP 주소를 통해 클러스터 내부의 서비스를 접근할 수 있습니다.

##### 설정
미리 생성되어 있는 `kubernetes-dashboard`라는 서비스 객체의 유형은 `ClusterIP` 입니다. 이 서비스 객체의 유형을 `LoadBalancer`로 변경해야 합니다. `LoadBalancer`로 변경하기 위해서는 다음의 커맨드를 사용할 수 있습니다.
`kubectl -n kube-system patch svc/kubernetes-dashboard -p '{"spec":{"type":"LoadBalancer"}}'`

위의 커맨드를 실행하면 다음과 같은 메시지가 출력됩니다.
```
[~]# kubectl get svc -n kube-system
NAMESPACE       NAME                   TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)                      AGE
kube-system     heapster               ClusterIP      10.254.14.112    <none>           80/TCP                       2d23h
kube-system     kube-dns               ClusterIP      10.254.0.10      <none>           53/UDP,53/TCP,9153/TCP       2d23h
kube-system     kubernetes-dashboard   ClusterIP      10.254.95.176    <none>           443/TCP                      2d23h
[~]#
[~]# kubectl -n kube-system patch svc/kubernetes-dashboard -p '{"spec":{"type":"LoadBalancer"}}'
service/kubernetes-dashboard patched
[~]#
[~]# kubectl get svc -n kube-system
NAME                   TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)                  AGE
heapster               ClusterIP      10.254.14.112   <none>        80/TCP                   2d23h
kube-dns               ClusterIP      10.254.0.10     <none>        53/UDP,53/TCP,9153/TCP   2d23h
kubernetes-dashboard   LoadBalancer   10.254.95.176   <pending>     443:31669/TCP            2d23h
[~]#
```

서비스 객체가 `LoadBalancer`로 변경되면 잠시 후 `EXTERNAL-IP`가 설정됩니다.
```
[~]# kubectl get svc -n kube-system
NAME                   TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                  AGE
heapster               ClusterIP      10.254.14.112   <none>           80/TCP                   2d23h
kube-dns               ClusterIP      10.254.0.10     <none>           53/UDP,53/TCP,9153/TCP   2d23h
kubernetes-dashboard   LoadBalancer   10.254.95.176   133.186.154.81   443:30963/TCP            2d23h
[~]#
```

`EXTERNAL-IP`에 표시된 IP 주소는 외부에서 접근할 수 있는 공인 IP 주소로써 웹브라우져에서 IP 주소로 접속(https)하면 쿠버네티스 대시보드에 접속할 수 있습니다. 이 IP 주소는 TOAST 웹콘솔의 Floating IP 페이지에 표시됩니다. 웹브라우져에서 `https://EXTERNAL-IP`로 접속하면 쿠버네티스 대시보드가 표시되는 것을 확인할 수 있습니다.

(참고)
* 쿠버네티스 대시보드가 자동생성되는 임시 사설 인증서를 사용하기 때문에 웹브라우저의 종류와 보안 설정에 따라 안전하지 않은 페이지로 표시됩니다.
* 로그인을 위해 필요한 토큰값은 이 문서의 "쿠버네티스 대시보드 접속을 위한 토큰값 획득"을 참고하세요.

#### 방법2. Ingress를 이용해 서비스 노출
<span style="color:#e11d21">**만약 방법1을 수행한 상태라면 이 문서의 "참고. 방법1에서 실행한 내용 되돌리기" 항목을 먼저 수행하셔야 합니다.**</span>
이번 절에서는 Ingress를 이용해 쿠버네티스 대시보드를 외부에 노출하는 방법에 대해 설명합니다.

##### 개념
![dashboard-02.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/dashboard-02.png)
Ingress는 클러스터 내부의 여러 서비스들을 외부에 노출하기 위한 개념 입니다. 클러스터 내에 Ingress Controller가 존재하고, Ingress Controller는 설정된 Ingress 객체의 설정에 따라 트래픽을 라우팅 합니다.

<br>
자세한 내용은 아래 링크를 참고하세요.
https://kubernetes.io/ko/docs/concepts/services-networking/ingress/


##### 설정
1. Ingress controller를 설치합니다. 이 예제는 nginx ingress controller를 기준으로 작성되었습니다. Nginx ingress controller의 설치 방법은 "nginx ingress controller 설치 및 사용 예제"장을 참고해주세요.
2. 다음과 같이 `kubernetes-dashboard` 서비스를 위한 ingress 객체를 생성합니다.
```
[~]# cat ./kubernetes-dashboard-ingress-tls-passthrough.yaml
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
[~]#
[~]# kubectl apply -f kubernetes-dashboard-ingress-tls-passthrough.yaml
ingress.extensions/k8s-dashboard-ingress created
[~]#
```

3. 아래의 명령을 수행하여 nginx ingress controller에 연결된 `EXTERNAL-IP`를 확인합니다.

```
[~]# kubectl get service/ingress-nginx -n ingress-nginx
NAME            TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)                      AGE
ingress-nginx   LoadBalancer   10.254.211.113   133.186.154.29   80:32680/TCP,443:31631/TCP   19h
[~]#
```

4. 웹브라우져에서 `https://EXTERNAL-IP`로 접속합니다.

(참고)
* 쿠버네티스 대시보드가 자동생성되는 임시 사설 인증서를 사용하기 때문에 웹브라우저의 종류와 보안 설정에 따라 안전하지 않은 페이지로 표시됩니다.
* 로그인을 위해 필요한 토큰값은 이 문서의 "쿠버네티스 대시보드 접속을 위한 토큰값 획득"을 참고하세요.



### 쿠버네티스 대시보드 접속을 위한 토큰값 획득
쿠버네티스 대시보드에 접속하면 토큰을 입력해 로그인을 할 수 있습니다. 토큰값은 다음과 같이 `kubectl` 커맨드로 알아낼 수 있습니다.

```
[~]# SECRET_NAME=$(kubectl -n kube-system get secrets | grep "kubernetes-dashboard-token" | cut -f1 -d ' ')
[~]# kubectl describe secret $SECRET_NAME -n kube-system | grep -E '^token' | cut -f2 -d':' | tr -d " "
eyJh ...(중략) y3w
[~]#
```

출력된 토큰값을 브라우져의 토큰 입력창에 입력하면 첫번째 과정에서 권한을 부여받은 사용자로 로그인하게 됩니다.
![dashboard-03.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/dashboard-03.png)


### 참고. 방법1에서 실행한 내용 되돌리기
<span style="color:#e11d21">**(위의 방법1을 실행하지 않은 상태라면 아래 내용을 수행할 필요가 없습니다)**</span>
위의 방법1에서 `kubernetes-dashboard` Service 객체를 `LoadBalancer` type으로 변경했다면, 이 객체의 type을 다시 `ClusterIP` type으로 변경하거나 기존 객체를 삭제하고 `ClusterIP` type으로 다시 생성할 수 있습니다.

1. `kubectl edit svc/kubernetes-dashboard -n kube-system` 명령을 이용해 type을 변경(`vim`을 사용할 줄 아셔야 합니다)

다음의 명령을 수행하면 vim이 실행되고, `kubernetes-dashboard` service 객체를 수정할 수 있게 됩니다. 여기에서 다음과 같이 수정합니다.
- `spec.type`의 값을 `LoadBalancer`에서 `ClusterIP`로 변경합니다.
- `spec.ports.nodePort` 항목을 삭제합니다.
- 저장하고 vim에서 빠져나옵니다.

아래는 `kubectl edit` 명령이 실행된 상태이며 내용은 수정하지 않았습니다.
```
## Please edit the object below. Lines beginning with a '#' will be ignored,
## and an empty file will abort the edit. If an error occurs while saving this file will be
## reopened with the relevant failures.
##
apiVersion: v1
kind: Service
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"labels":{"k8s-app":"kubernetes-dashboard"},"name":"kubernetes-dashboard","namespace":"kube-system"},"spec":{"ports":[{"port":443,"protocol":"TCP","targetPort":8443}],"selector":{"k8s-app":"kubernetes-dashboard"},"type":"ClusterIP"}}
  creationTimestamp: "2020-04-09T03:01:51Z"
  labels:
    k8s-app: kubernetes-dashboard
  name: kubernetes-dashboard
  namespace: kube-system
  resourceVersion: "37563611"
  selfLink: /api/v1/namespaces/kube-system/services/kubernetes-dashboard
  uid: fc7cf9d3-af07-4b69-b7b4-fe3f7a7fb8cd
spec:
  clusterIP: 10.254.138.151
  externalTrafficPolicy: Cluster
  ports:
  - nodePort: 30473
    port: 443
    protocol: TCP
    targetPort: 8443
  selector:
    k8s-app: kubernetes-dashboard
  sessionAffinity: None
  type: LoadBalancer
status:
  loadBalancer:
    ingress:
    - ip: 133.186.154.41
```

아래는 위의 지침대로 수정한 상태 입니다.
```
## Please edit the object below. Lines beginning with a '#' will be ignored,
## and an empty file will abort the edit. If an error occurs while saving this file will be
## reopened with the relevant failures.
##
apiVersion: v1
kind: Service
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"labels":{"k8s-app":"kubernetes-dashboard"},"name":"kubernetes-dashboard","namespace":"kube-system"},"spec":{"ports":[{"port":443,"protocol":"TCP","targetPort":8443}],"selector":{"k8s-app":"kubernetes-dashboard"},"type":"ClusterIP"}}
  creationTimestamp: "2020-04-09T03:01:51Z"
  labels:
    k8s-app: kubernetes-dashboard
  name: kubernetes-dashboard
  namespace: kube-system
  resourceVersion: "37563611"
  selfLink: /api/v1/namespaces/kube-system/services/kubernetes-dashboard
  uid: fc7cf9d3-af07-4b69-b7b4-fe3f7a7fb8cd
spec:
  clusterIP: 10.254.138.151
  externalTrafficPolicy: Cluster
  ports:
  - port: 443
    protocol: TCP
    targetPort: 8443
  selector:
    k8s-app: kubernetes-dashboard
  sessionAffinity: None
  type: ClusterIP
status:
  loadBalancer:
    ingress:
    - ip: 133.186.154.41
```

이 상태에서 `:wq` 명령으로 저장하고 vim을 빠져나오면 다음과 같은 메시지가 출력됩니다.
```
[~]# kubectl edit svc/kubernetes-dashboard -n kube-system
service/kubernetes-dashboard edited
[~]#
```

service 객체를 조회해보면 type이 변경된 것을 확인하실 수 있습니다.
```
[~]# kubectl get svc -n kube-system
NAME                   TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                  AGE
heapster               ClusterIP   10.254.14.112    <none>        80/TCP                   3d
kube-dns               ClusterIP   10.254.0.10      <none>        53/UDP,53/TCP,9153/TCP   3d
kubernetes-dashboard   ClusterIP   10.254.138.151   <none>        443/TCP                  16m
[~]#
```

2. 삭제 후 재생성
아래와 같이 `kubernetes-dashboard` service 객체를 삭제합니다.
```
[~]# kubectl delete svc/kubernetes-dashboard -n kube-system
service "kubernetes-dashboard" deleted
[~]#
```

아래와 같이 `kubernetes-dashboard` service 객체를 다시 생성합니다.
```
[~]# cat kubernetes-dashboard-svc-cluster.yaml
apiVersion: v1
kind: Service
metadata:
  annotations:
  labels:
    k8s-app: kubernetes-dashboard
  name: kubernetes-dashboard
  namespace: kube-system
spec:
  type: ClusterIP
  ports:
  - port: 443
    protocol: TCP
    targetPort: 8443
  selector:
    k8s-app: kubernetes-dashboard
[~]#
[~]# kubectl apply -f kubernetes-dashboard-svc-cluster.yaml
service/kubernetes-dashboard created
[~]#
```

Service 객체를 조회해보면 `kubernetes-dashboard` service 객체가 다시 생성된 것을 확인하실 수 있습니다.
```
[~]# kubectl get svc -n kube-system
NAME                   TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)                  AGE
heapster               ClusterIP   10.254.14.112    <none>        80/TCP                   3d
kube-dns               ClusterIP   10.254.0.10      <none>        53/UDP,53/TCP,9153/TCP   3d
kubernetes-dashboard   ClusterIP   10.254.223.159   <none>        443/TCP                  9s
[~]#
```




## Pod에 Persistent volume 연동
이 장에서는 쿠버네티스의 Persistent Volume(PV)과 Persistent Volume Claims(PVC)에 대한 개념에 대해 알아보고, Pod에 Persistent volume을 연동하는 방법에 대해 기술합니다.

<br>
좀 더 상세한 내용을 원하신다면 다음 링크를 참조하세요.
- https://kubernetes.io/docs/concepts/storage/persistent-volumes/

### 개념
#### 스토리지클래스
스토리지클래스(StorageClass)는 저장장치의 특성에 대한 표현한 개념 입니다. 일종의 저장장치에 대한 프로파일이라고 볼 수 있습니다. 다음과 같은 속성이 있습니다.

좀 더 자세한 사항은 아래 링크를 참조하세요.
- https://kubernetes.io/docs/concepts/storage/storage-classes/


#### Persistent Volume & Persisten Volume Claims
Persistent Volume(PV)는 저장장치 그 자체를 나타내는 개념입니다. PV는 물리 저장장치를 표현하는 쿠버네티스 리소스 입니다. 따라서 하나의 PV는 하나의 TOAST 블록스토리지 리소스와 매핑됩니다.

Persistent Volume Claims(PVC)는 PV에 대한 요구 입니다. 사용자가 어떤 저장장치를 사용하고 싶다는 요구사항을 보내는 것으로 생각할 수 있습니다. 이 요구사항에는 저장장치의 용량, 읽기/쓰기 모드 등 저장장치의 특성이 포함됩니다.  동적 프로비져닝(Provisioning)의 경우 스토리지클래스에 기반하여 동작합니다.

이렇게 저장장치와 저장장치에 대한 요구를 분리함으로써 사용자는 사용하고 싶은 저장장치에 대한 특성만 지정하고, 시스템에서는 그 요구사항에 맞는 저장장치 리소스를 할당함으로써 리소스의 사용과 관리를 분리할 수 있게 됩니다.


#### PV/PVC의 생명주기
PV/PVC는 아래와 같이 4단계의 생명주기를 갖습니다.

##### 1. Provisioning
저장장치를 확보하는 단계입니다. 저장장치를 확보하는 방법에는 정적인 방법과 동적인 방법이 있습니다.
###### 정적 provisioning
관리자가 직접 저장장치를 확보하고 이에 연결된 PV를 생성합니다.

###### 동적 provisioning
PVC와 매치되는 저장장치가 없는 경우, 클러스터가 자동으로 저장장치를 확보하고 이에 연결된 PV를 생성합니다.

##### 2. Binding
PV와 PVC를 바인드하는 단계입니다. PV와 PVC는 1:1로 매핑되며, PV의 provisioning 방법과는 무관합니다.

##### 3. Using
PV를 Pod에 마운트하여 저장장치로 사용할 수 있습니다.

##### 4. Reclaiming
사용을 마친 PV에 연결된 저장장치를 회수하는 단계 입니다. PV 별로 회수 방법을 지정해놓을 수 있습니다.
###### Delete
Delete 회수 방법은 PV가 삭제될 때 연결되어 있는 저장장치를 삭제합니다.

###### Retain
Retain 회수 방법은 PV가 삭제될 때 연결되어 있는 저장장치를 그대로 두는 것 입니다. 이 저장장치를 회수하기 위해서는 사용자가 직접 회수 처리를 해야 합니다.

###### Recycle
Recycle 회수 방법은 PV가 삭제되면서 자동으로 다시 사용할 수 있는 상태를 만드는 방법입니다. 이 방법은 deprecated 되었습니다.

### TOAST의 PV/PVC 관련 사항
TOAST에서 PV/PVC 기능 관련하여 다음과 같은 제약사항이 있습니다.
1. 스토리지 접근 모드는 `ReadWriteOnce`만 지원합니다.
2. 스토리지클래스의 `Provisioner`는 `kubernetes.io/cinder`으로 지정해야 합니다.


### 정적 Provisioning으로 PV를 확보하여 Pod 연동
이번 장에서는 정적 Provisioning 방법으로 PV를 확보하고, 이를 Pod에 연동해 사용하는 방법에 대해 설명합니다.

#### Step 1. 블록 스토리지 생성
웹콘솔의 블록 스토리지 화면에서 PV와 연동할 블록 스토리지를 생성합니다. 저장장치 타입과 용량 등을 적절히 입력합니다.
이후 PV 생성을 위해서는 이 스토리지의 ID를 알고 있어야 합니다. 웹콘솔에서 확인할 수 있습니다.
![pv-01.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/pv-01.png)

#### Step 2. StorageClass 생성
다음과 같이 스토리지클래스를 생성합니다.
```
➜  pv-test# cat storage_class.yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: sc-default
provisioner: kubernetes.io/cinder
➜  pv-test#
➜  pv-test# kubectl apply -f storage_class.yaml
storageclass.storage.k8s.io/sc-default created
➜  pv-test#
➜  pv-test# kubectl get sc
NAME         PROVISIONER            AGE
sc-default   kubernetes.io/cinder   8s
➜  pv-test#
```

#### Step 3. PV 생성
다음과 같이 생성해놓은 저장장치에 연결된 PV를 생성합니다.
```
➜  pv-test# cat pv-static.yaml
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
➜  pv-test#
➜  pv-test# kubectl apply -f pv-static.yaml
persistentvolume/pv-static-001 created
➜  pv-test#
➜  pv-test# kubectl get pv -o wide
NAME            CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS   REASON   AGE   VOLUMEMODE
pv-static-001   10Gi       RWO            Delete           Available           sc-default              7s    Filesystem
➜  pv-test#
```
PV 생성시 다음을 유의해야 합니다.
* `storageClassName`는 위에서 생성한 스토리지클래스이름을 지정합니다. 다른 스토리지클래스를 지정할 수도 있습니다.
* `accessModes`는 반드시 `ReadWriteOnce`로 지정해야 합니다.
* `presistentVolumeReclaimPolicy`는 `Delete` 혹은 `Retain`으로 설정할 수 있습니다.

#### Step 4. PVC 생성
다음과 같이 위에서 생성한 PV를 사용하도록 하는 PVC를 생성합니다.
```
➜  pv-test# cat pvc-static.yaml
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
➜  pv-test#
➜  pv-test# kubectl apply -f pvc-static.yaml
persistentvolumeclaim/pvc-static created
➜  pv-test#
➜  pv-test# kubectl get pvc -o wide
NAME         STATUS   VOLUME          CAPACITY   ACCESS MODES   STORAGECLASS   AGE   VOLUMEMODE
pvc-static   Bound    pv-static-001   10Gi       RWO            sc-default     7s    Filesystem
➜  pv-test#
```
PVC 생성 시 다음을 유의해야 합니다.
* `storageClassName`는 위에서 생성한 스토리지클래스 이름을 지정합니다. 다른 스토리지클래스를 지정할 수도 있습니다.
* `spec/volumeName`에는 위에서 생성한 PV의 이름을 지정해야 합니다.
* `accessModes`는 반드시 `ReadWriteOnce`로 지정해야 합니다.

PVC 생성 후 PV의 상태를 조회해보면 `Status`가 `Available`에서 `Bound`로 변경된 것을 확인하실 수 있습니다.
```
➜  pv-test# kubectl get pv -o wide
NAME            CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                STORAGECLASS   REASON   AGE   VOLUMEMODE
pv-static-001   10Gi       RWO            Delete           Bound    default/pvc-static   sc-default              79s   Filesystem
➜  pv-test#
```

#### Step 5. Pod 연동
다음과 같이 PVC로 요청한 저장장치를 마운트하는 pod를 생성합니다.
```
➜  pv-test# cat pod-static-pvc.yaml
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
➜  pv-test#
➜  pv-test# kubectl apply -f pod-static-pvc.yaml
pod/nginx-with-static-pv created
➜  pv-test#
➜  pv-test# kubectl get pods
NAME                   READY   STATUS    RESTARTS   AGE
nginx-with-static-pv   1/1     Running   0          50s
➜  pv-test#
```

Pod 생성 시 다음을 유의해야 합니다.
* `spec/volumes/persistenVolumeClame/claimName`에 위에서 생성한 PVC의 이름을 입력해야 합니다.
* `spec/containers/volumeMounts`에 마운트 정보를 적절히 설정해야 합니다.

Pod에 PVC로 획득한 저장장치가 제대로 마운트되어 있는지 확인합니다. 이 예제에서는 획득한 저장장치를 `/usr/share/nginx/html` 디렉터리에 마운트 했습니다.
```
➜  pv-test# kubectl exec -ti nginx-with-static-pv -- df -h
Filesystem      Size  Used Avail Use% Mounted on
overlay          20G  2.9G   16G  16% /
tmpfs            64M     0   64M   0% /dev
tmpfs           920M     0  920M   0% /sys/fs/cgroup
/dev/vda1        20G  2.9G   16G  16% /etc/hosts
shm              64M     0   64M   0% /dev/shm
/dev/vdc        9.8G   23M  9.7G   1% /usr/share/nginx/html
tmpfs           920M   12K  920M   1% /run/secrets/kubernetes.io/serviceaccount
tmpfs           920M     0  920M   0% /proc/acpi
tmpfs           920M     0  920M   0% /proc/scsi
tmpfs           920M     0  920M   0% /sys/firmware
➜  pv-test#
```

이제 블록 스토리지의 연결정보에도 관련 내용이 표시되는 것을 확인할 수 있습니다.

#### Step 6. 테스트 리소스 삭제
다음과 같이 pod를 삭제합니다.
```
➜  pv-test# kubectl delete pod/nginx-with-static-pv
pod "nginx-with-static-pv" deleted
➜  pv-test#
➜  pv-test# kubectl get pods
No resources found.
➜  pv-test#
```

다음과 같이 PVC를 삭제합니다.
```
➜  pv-test# kubectl delete persistentvolumeclaim/pvc-static
persistentvolumeclaim "pvc-static" deleted
➜  pv-test#
```

이 예제에서는 PV의 `reclaimPolicy`를 `Delete`로 설정해두었기 때문에 PVC가 삭제되면 연결된 PV도 삭제되고, PV와 연결된 블록 스토리지까지 삭제됩니다.
만약, PV의 `reclaimPolicy`를 `Retain`으로 설정했다면 PVC가 삭제될 때 PV가 삭제되지 않습니다. 이후 PV를 삭제하더라도 블록스토리지까지 삭제되지 않습니다. PV 삭제 시 블록스토리지까지 삭제하려면 PV의 `reclaimPolicy`를 `Delete`로 변경해야 합니다.


### 동적 Provisioning으로 PV를 확보하여 Pod 연동

#### Step 1. 스토리지클래스 생성
정적 Provisioning의 스토리지클래스 생성 과정과 동일합니다.

#### Step 2. PVC 생성
다음과 같이 동적 provisioning을 수행하는 PVC를 생성합니다. PVC 생성 시 `volumeName` 필드가 없는 것을 유의하세요.
```
➜  pv-test# cat pvc-dynamic.yaml
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
  storageClassName: sc-default
➜  pv-test#
➜  pv-test# kubectl apply -f pvc-dynamic.yaml
persistentvolumeclaim/pvc-dynamic created
➜  pv-test#
```

PVC만 생성했지만 PV가 자동으로 생성된 것을 확인할 수 있습니다.
```
➜  pv-test# kubectl get sc,pv,pvc
NAME                                     PROVISIONER            AGE
storageclass.storage.k8s.io/sc-default   kubernetes.io/cinder   10m

NAME                                                        CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                 STORAGECLASS   REASON   AGE
persistentvolume/pvc-c63da3f9-dfcb-4cae-a9a9-67137994febc   10Gi       RWO            Delete           Bound    default/pvc-dynamic   sc-default              16s

NAME                                STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
persistentvolumeclaim/pvc-dynamic   Bound    pvc-c63da3f9-dfcb-4cae-a9a9-67137994febc   10Gi       RWO            sc-default     17s
➜  pv-test#
```

자동으로 생성된 블록 스토리지는 웹콘솔에서 확인할 수 있습니다.
![pv-02.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/pv-02.png)


#### Step 3. Pod 연동
다음과 같이 PVC로 요청한 저장장치를 마운트하는 pod를 생성합니다.
```
➜  pv-test# cat pod-dynamic-pvc.yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-with-dynamic-pvc
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
        claimName: pvc-dynamic
➜  pv-test#
➜  pv-test# kubectl apply -f pod-dynamic-pvc.yaml
pod/nginx-with-dynamic-pvc created
➜  pv-test#
```

다음과 같이 마운트 된 것을 확인할 수 있습니다.
```
➜  pv-test# kubectl exec -ti nginx-with-dynamic-pvc -- df -h
Filesystem      Size  Used Avail Use% Mounted on
overlay          20G  2.9G   16G  16% /
tmpfs            64M     0   64M   0% /dev
tmpfs           920M     0  920M   0% /sys/fs/cgroup
/dev/vda1        20G  2.9G   16G  16% /etc/hosts
shm              64M     0   64M   0% /dev/shm
/dev/vdc        9.8G   37M  9.7G   1% /usr/share/nginx/html
tmpfs           920M   12K  920M   1% /run/secrets/kubernetes.io/serviceaccount
tmpfs           920M     0  920M   0% /proc/acpi
tmpfs           920M     0  920M   0% /proc/scsi
tmpfs           920M     0  920M   0% /sys/firmware
➜  pv-test#
```

#### Step 4. 테스트 리소스 삭제
정적 Provisioning의 스토리지클래스 생성 과정과 동일합니다. `reclaimPolicy`가 `Delete`이기 때문에 PVC를 삭제하면 PV도 삭제되고, PV가 삭제되면 블록 스토리지도 삭제됩니다.

#### 주의사항
* 동적 Provisioning에 의해 생성된 블록 스토리지는 다음의 특성이 있습니다.
    * 연결된 PV가 삭제되면 자동으로 삭제됩니다.
    * 웹콘솔의 블록 스토리지 페이지에서 삭제가 불가능 합니다.
    * 클러스터 삭제 시 자동으로 삭제되지 않습니다.
        * 따라서 클러스터 삭제 전에 관련 PVC 및 PV를 미리 삭제해야 합니다.
