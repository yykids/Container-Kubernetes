## Container > Kubernetes > 사용 가이드

## 클러스터
클러스터는 사용자의 Kubernetes를 구성하는 인스턴스들의 그룹입니다.

### 클러스터 생성
Kubernetes 서비스를 사용하려면 먼저 클러스터를 생성해야 합니다. **Container > Kubernetes** 서비스 페이지에서 **클러스터 생성** 버튼을 클릭하면 클러스터 생성 페이지가 나타납니다. 클러스터 생성에 필요한 항목은 다음과 같습니다.

| 항목 | 설명 |
| --- | --- |
| 클러스터 이름 | Kubernetes 클러스터의 이름, 20자 이내의 영문자와 숫자, '-', '.'로 구성 |
| 쿠버네티스 버전 | 사용할 Kubernetes 버전 |
| VPC | 클러스터에 연결할 VPC 네트워크 |
| 서브넷 | VPC에 정의된 서브넷 중 클러스터를 구성하는 인스턴스에 연결할 서브넷 |
| 이미지 | 클러스터를 구성하는 인스턴스에 사용할 이미지 |
| 가용성 영역 | 기본 노드 그룹 인스턴스를 생성할 영역 |
| 인스턴스 타입 | 기본 노드 그룹 인스턴스 사양 |
| 노드 수 | 기본 노드 그룹 인스턴스 수 |
| 키 페어 | 기본 노드 그룹 접근에 사용할 키 페어 |
| 블록 스토리지 타입 | 기본 노드 그룹 인스턴스의 블록 스토리지 종류 |
| 블록 스토리지 크기 | 기본 노드 그룹 인스턴스의 블록 스토리지 크기 |

필요한 정보를 입력하고 **클러스터 생성** 버튼을 클릭하면 클러스터 생성이 시작됩니다. 클러스터 목록에서 상태를 확인할 수 있습니다. 생성하는 데는 몇 분 정도 걸립니다.

> [참고]
> 클러스터를 생성하면 기본 노드 그룹이 생성됩니다. 기본 노드 그룹이 생성된 이후에는 노드 수를 변경할 수 없습니다. 추가 노드가 필요하면 노드 그룹을 새로 만들어야 합니다.


### 클러스터 조회
생성한 클러스터는 **Container > Kubernetes** 서비스 페이지에서 확인할 수 있습니다. 클러스터를 선택하면 하단에 클러스터 정보가 나타납니다.

| 항목 | 설명 |
| --- | --- |
| 클러스터 이름 | Kubernetes 클러스터의 이름과 ID |
| 노드 수 | 클러스터를 구성하는 모든 노드 인스턴스 수 |
| Kubernetes 버전 | 사용 중인 Kubernetes 버전 |
| VPC | 클러스터에 연결된 VPC 네트워크 |
| 서브넷 | 클러스터를 구성하는 노드 인스턴스에 연결된 서브넷 |
| API 엔드포인트 | 클러스터에 접근해 조작하기 위한 API 엔드포인트 URI |
| 설정 파일 | 클러스터에 접근해 조작하기 위해 필요한 설정 파일 다운로드 버튼 |

### 클러스터 삭제
삭제할 클러스터를 선택하고 **클러스터 삭제** 버튼을 클릭하면 삭제가 진행됩니다. 삭제하는 데는 몇 분 정도 걸립니다.

## 노드 그룹
노드 그룹은 Kubernetes를 구성하는 워커 노드 인스턴스들의 그룹입니다.

### 노드 그룹 조회
클러스터 목록에서 클러스터 이름을 클릭하면 노드 그룹 목록을 확인할 수 있습니다. 노드 그룹을 선택하면 하단에 노드 그룹 정보가 나타납니다.

* 기본 정보
**기본 정보** 탭에서는 다음과 정보를 확인할 수 있습니다.

| 항목 | 설명 |
| --- | --- |
| 노드 그룹 이름 | 노드 그룹 이름과 ID |
| 클러스터 이름 | 노드 그룹이 속한 클러스터의 이름과 ID |
| 쿠버네티스 버전 | 사용 중인 Kubernetes 버전 |
| 가용성 영역 | 노드 그룹 인스턴스가 생성된 영역 |
| 인스턴스 타입 | 노드 그룹 인스턴스 사양 |
| 이미지 타입 | 노드 그룹 인스턴스에 사용한 이미지 종류 |
| 블록 스토리지 크기 | 노드 그룹 인스턴스의 블록 스토리지 크기 |
| 생성일 | 노드 그룹이 생성된 시각 |
| 수정일 | 노드 그룹이 마지막으로 수정된 시각 |

* 노드 목록
**노드 목록** 탭에서는 노드 그룹을 구성하는 인스턴스의 목록을 확인할 수 있습니다.

### 노드 그룹 생성
클러스터를 생성하면 기본 노드 그룹이 생성되지만, 필요에 따라 추가 노드 그룹을 만들 수 있습니다. 기본 노드 그룹의 인스턴스보다 높은 사양의 컨테이너 구동 환경이 필요하거나, 스케일 아웃(scale out, 확장)을 위해 더 많은 워커 노드 인스턴스가 필요한 경우 추가 노드 그룹을 생성해 사용할 수 있습니다. 노드 그룹 목록 페이지에서 **노드 그룹 생성** 버튼을 클릭하면 노드 그룹 생성 페이지가 나타납니다. 노드 그룹 생성에 필요한 항목은 다음과 같습니다.

| 항목 | 설명 |
| --- | --- |
| 가용성 영역 | 클러스터를 구성하는 인스턴스를 생성할 영역 |
| 노드 그룹 이름 | 추가 노드 그룹 이름, 20자 이내의 영문자와 숫자, '-', '.'로 구성 |
| 인스턴스 타입 | 추가 노드 그룹 인스턴스 사양 |
| 노드 수 | 추가 노드 그룹 인스턴스 수 |
| 키 페어 | 추가 노드 그룹 접근에 사용할 키 페어 |
| 블록 스토리지 타입 | 추가 노드 그룹 인스턴스의 블록 스토리지 종류 |
| 블록 스토리지 크기 | 추가 노드 그룹 인스턴스의 블록 스토리지 크기 |

필요한 정보를 입력하고 **노드 그룹 생성** 버튼을 클릭하면 노드 그룹 생성이 시작됩니다. 노드 그룹 목록에서 상태를 확인할 수 있습니다. 노드 그룹 생성하는 데는 몇 분 정도 걸립니다.

### 노드 그룹 삭제
노드 그룹 목록에서 삭제하려는 노드 그룹을 선택하고 **노드 그룹 삭제** 버튼을 클릭하면 삭제가 진행됩니다. 노드 그룹 삭제하는 데는 몇 분 정도 걸립니다.

## 클러스터 관리
원격의 호스트에서 클러스터를 조작하고 관리하려면 Kubernetes가 제공하는 명령줄 도구(CLI)인 `kubectl`이 필요합니다.

### kubectl 설치
kubectl은 특별한 설치 과정 없이 실행 파일을 다운로드해 바로 사용할 수 있습니다. 운영체제별 다운로드 경로는 다음과 같습니다.

| 운영체제 | 다운로드 커맨드 |
| --- | --- |
| Linux | curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/linux/amd64/kubectl |
| MacOS | curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/darwin/amd64/kubectl |
| Windows | curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/windows/amd64/kubectl.exe |

그 외 설치 방법과 옵션 등 자세한 사항은 [Install and Set Up kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) 문서를 참고하세요.

#### 권한 변경
다운로드한 파일은 기본적으로 실행 권한이 없습니다. 실행 권한을 추가해야 합니다.

```
$ chmod +x kubectl
```

#### 위치 변경 또는 경로 지정
어느 경로에서든 kubectl을 실행할 수 있도록 환경 변수에 지정된 경로로 옮기거나, kubectl이 있는 경로를 환경 변수에 추가합니다.

* 환경 변수에 지정된 경로로 위치 변경
```
$ sudo mv kubectl /usr/local/bin/
```

* 환경 변수에 경로 추가
```
// kubectl이 있는 경로에서 실행
$ export PATH=$PATH:$(pwd)
```

### 설정
kubectl로 Kubernetes 클러스터에 접근하려면 클러스터 설정 파일(kubeconfig)이 필요합니다. TOAST 웹 콘솔에서 **Container > Kubernetes** 서비스 페이지를 열고 접근할 클러스터를 선택합니다. 하단 **기본 정보** 탭에서 **설정 파일** 항목의 **다운로드** 버튼을 클릭해 설정 파일을 다운로드합니다. 다운로드한 설정 파일은 원하는 위치로 옮겨 kubectl 실행 시 참조할 수 있도록 준비합니다.

> [주의]
> TOAST 웹 콘솔에서 다운로드한 설정 파일은 클러스터 정보와 인증을 위한 토큰 등이 포함되어 있습니다. 설정 파일이 있으면 해당 Kubernetes 클러스터에 접근할 수 있는 권한을 갖게 됩니다. 설정 파일을 절대로 분실하지 않도록 주의하시기 바랍니다.

kubectl은 실행할 때마다 클러스터 설정 파일이 필요합니다. 따라서 매번 `--kubeconfig` 옵션을 이용해 클러스터 설정 파일을 지정해야 합니다. 그러나 환경 변수에 클러스터 설정 파일 경로가 저장되어 있다면 매번 옵션을 지정하지 않아도 됩니다.

```
$ export KUBECONFIG={클러스터 설정 파일 경로}
```

클러스터 설정 파일 경로를 환경 변수에 저장하고 싶지 않다면 kubectl의 기본 설정 파일인 `$HOME/.kube/config`로 복사해 사용할 수도 있습니다. 그러나 클러스터를 여러 개 운영한다면 환경 변숫값을 변경하는 방법이 편리합니다.

### 연결 확인
`kubectl version` 명령어로 정상 설정되었는지 확인합니다. 문제가 없다면 `Server Version`이 출력됩니다.

```
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"15", GitVersion:"v1.15.7", GitCommit:"6c143d35bb11d74970e7bc0b6c45b6bfdffc0bd4", GitTreeState:"clean", BuildDate:"2019-12-11T12:42:56Z", GoVersion:"go1.12.12", Compiler:"gc", Platform:"darwin/amd64"}
Server Version: version.Info{Major:"1", Minor:"15", GitVersion:"v1.15.7", GitCommit:"6c143d35bb11d74970e7bc0b6c45b6bfdffc0bd4", GitTreeState:"clean", BuildDate:"2019-12-11T12:34:17Z", GoVersion:"go1.12.12", Compiler:"gc", Platform:"linux/amd64"}
```

* Client Version: 실행한 kubectl 파일의 버전 정보
* Server Version: 클러스터를 구성하고 있는 Kubernetes 버전 정보

## LoadBalancer 서비스
Kubernetes 애플리케이션의 기본 실행 단위인 파드(pod)는 CNI(Container Network Interface)로 클러스터 네트워크에 연결됩니다. 기본적으로 클러스터 외부에서 파드로는 접근할 수 없습니다. 파드의 서비스를 클러스터 외부에 공개하려면 Kubernetes의 `LoadBalancer` 서비스(Service) 객체(object)를 이용해 외부에 공개할 경로를 만들어야 합니다. LoadBalancer 서비스 객체를 만들면 클러스터 외부에 TOAST Load Balancer가 생성되어 서비스 객체와 연결됩니다.

### 웹 서버 파드 생성
다음과 같이 2개의 nginx 파드를 실행하는 디플로이먼트(deployment) 객체 매니페스트 파일을 작성하고 객체를 생성합니다.

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

디플로이먼트 객체를 생성하면 매니페스트에 정의한 파드가 자동으로 생성됩니다.

```
$ kubectl apply -f nginx.yaml
deployment.apps/nginx-deployment created

$ kubectl get pods
NAME                                READY   STATUS    RESTARTS   AGE  
nginx-deployment-7fd6966748-pvrzs   1/1     Running   0          4m13s
nginx-deployment-7fd6966748-wv7rd   1/1     Running   0          4m13s
```

만약 TOAST Container Registry에 저장한 이미지를 사용하고 싶다면 먼저 사용자 레지스트리에 로그인하기 위한 시크릿(secret)을 만들어야 합니다.

```
$ kubectl create secret docker-registry registry-credential --docker-server={사용자 레지스트리 주소} --docker-username={Toast 계정 email 주소} --docker-password={서비스 Appkey 또는 통합 Appkey}
secret/registry-credential created

$ kubectl get secrets
NAME                  TYPE                             DATA   AGE
registry-credential   kubernetes.io/dockerconfigjson   1      30m
```

디플로이먼트 매니페스트 파일에 시크릿 정보를 추가하고, 이미지 이름을 변경하면 사용자 레지스트리에 저장된 이미지를 이용해 파드를 만들 수 있습니다.

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
        image: {사용자 레지스트리 주소}/nginx:1.14.2
        ...
      imagePullSecrets:
      - name: regcred

```

> [참고]
> TOAST Container Registry 사용 방법은 [Container Registry 사용 가이드](/Container/Container%20Registry/ko/user-guide) 문서를 참고하세요.

### LoadBalancer 서비스 생성
Kubernetes의 서비스 객체를 정의하려면 다음과 같은 항목으로 구성된 매니페스트가 필요합니다.

| 항목 | 설명 |
| --- | --- |
| metadata.name | 서비스 객체의 이름 |
| spec.selector | 서비스 객체와 연결할 파드 이름 |
| spec.ports | 외부 로드 밸런서에서 들어오는 트래픽을 파드에 전달할 인터페이스 설정 |
| spec.ports.name | 인터페이스 이름 |
| spec.ports.protocol | 인터페이스에서 사용할 프로토콜(예: TCP) |
| spec.ports.port | 서비스 객체 외부에 공개할 포트 번호 |
| spec.ports.targetPort | 서비스 객체와 연결할 파드의 포트 번호 |
| spec.type | 서비스 객체 유형 |

다음과 같이 서비스 매니페스트를 작성합니다. 이 LoadBalancer 서비스 객체는 **spec.selector**에 정의된 이름에 따라 `app: nginx` 레이블이 붙은 파드와 연결됩니다. 그리고 **spec.ports**에 정의된 대로 TCP/8080 포트로 들어온 트래픽을 파드의 TCP/80 포트로 전달합니다.

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

LoadBalancer 서비스 객체를 생성하면 클러스터 외부에 로드 밸런서를 만들고 연결하기까지 약간의 시간이 필요합니다. 외부 로드 밸런서와 연결되기 전에는 **EXTERNAL-IP** 항목이 `<pending>`으로 표시됩니다.

```
$ kubectl apply -f service.yaml
service/nginx-svc created

$ kubectl get service
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
nginx-svc    LoadBalancer   10.254.134.18   <pending>     8080:30013/TCP   11s
```

외부 로드 밸런서와 연결되면 **EXTERNAL-IP** 항목에 IP가 표시됩니다. 이 IP는 외부 로드 밸런서의 플로팅 IP입니다.

```
$ kubectl get service
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)          AGE
nginx-svc    LoadBalancer   10.254.134.18   123.123.123.30   8080:30013/TCP   3m13s
```

> [참고]
> 생성된 로드 밸런서는 **Network > Load Balancer** 페이지에서 확인할 수 있습니다.
> 로드 밸런서의 IP는 외부에서 접근할 수 있는 플로팅 IP입니다. **Network > Floating IP** 페이지에서 확인할 수 있습니다.


### 인터넷을 통한 서비스 테스트
로드 밸런서에 부착한 플로팅 IP로 HTTP 요청을 보내 Kubernetes 클러스터의 웹 서버 파드가 응답하는지 확인합니다. 서비스 객체의 TCP/8080 포트를 파드의 TCP/80 포트와 연결하도록 설정했기 때문에 TCP/8080 포트로 요청을 보내야 합니다. 외부 로드 밸런서와 서비스 객체, 파드가 잘 연결되었다면 웹 서버는 nginx 기본 페이지를 응답합니다.

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


## 인그레스 컨트롤러
인그레스 컨트롤러(ingress controller)는 인그레스(Ingress) 객체에 정의된 규칙을 참조하여 클러스터 외부에서 내부 서비스로 HTTP와 HTTPS 요청을 라우팅하고 SSL/TSL 종료, 가상 호스팅 등을 제공합니다. 인그레스 컨트롤러와 인그레스에 대한 자세한 내용은 [인그레스 컨트롤러](https://kubernetes.io/ko/docs/concepts/services-networking/ingress-controllers/), [인그레스](https://kubernetes.io/ko/docs/concepts/services-networking/ingress/) 문서를 참고하세요.


### NGINX Ingress Controller 설치
NGINX Ingress Controller는 많이 사용되는 인그레스 컨트롤러 중 하나입니다. 자세한 내용은 [NGINX Ingress Controller](https://kubernetes.github.io/ingress-nginx/)와 [NGINX Ingress Controller for Kubernetes](https://docs.nginx.com/nginx-ingress-controller/overview/) 문서를 참고하세요.

NGINX Ingress Controller는 필요한 자원을 바로 생성할 수 있도록 미리 정의한 매니페스트 파일을 제공합니다. 이 매니페스트를 이용하면 쉽게 필요한 자원을 생성할 수 있습니다.

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

### LoadBalancer 서비스 생성
인그레스 컨트롤러 역시 파드로 생성되기 때문에 외부에 공개하기 위해서는 LoadBalancer 서비스 또는 NodePort 서비스를 만들어야 합니다. 다음과 같이 HTTP와 HTTPS를 처리할 수 있는 LoadBalancer 서비스 매니페스트를 정의합니다.

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

서비스 객체를 생성하고 외부 로드 밸런서가 연결되어 있는지 확인합니다. **EXTERNAL-IP** 필드에는 플로팅 IP 주소가 설정되어 있어야 합니다.

```
$ kubectl apply -f ingress-nginx-lb.yaml
service/ingress-nginx created

$ kubectl get svc -n ingress-nginx
NAME            TYPE           CLUSTER-IP     EXTERNAL-IP      PORT(S)                      AGE
ingress-nginx   LoadBalancer   10.254.2.128   123.123.123.41   80:30820/TCP,443:30269/TCP   39s
```

### URI 기반 서비스 분기

![ingress-01.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/ingress-01.png)

#### 서비스와 파드 생성
다음과 같이 서비스와 파드를 생성하기 위한 매니페스트를 작성합니다. `tea-svc` 서비스에는 `tea` 파드를 연결하고, `coffee-svc` 서비스에는 `coffee` 파드를 연결합니다.

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

매니페스트를 적용하고 디플로이먼트, 서비스, 파드가 생성되었는지 확인합니다. 파드는 **Running** 상태여야 합니다.

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

#### 인그레스(Ingress) 생성
요청 경로에 따라 서비스를 연결하는 인그레스 매니페스트를 작성합니다. 엔드포인트가 `/tea`인 요청은 `tea-svc` 서비스에 연결하고 `/coffee`인 요청은 `coffee-svc` 서비스에 연결합니다.

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

인그레스를 생성하고 잠시 후 확인했을 때 **ADDRESS** 필드에 IP가 설정되어 있어야 합니다.

```
$ kubectl apply -f cafe-ingress-uri.yaml
ingress.extensions/cafe-ingress-uri created

$ kubectl get ingress cafe-ingress-uri
NAME               HOSTS   ADDRESS          PORTS   AGE
cafe-ingress-uri   *       123.123.123.44   80      88s
```

#### HTTP 요청 전송
외부 호스트에서 ingress의 **ADDRESS** 필드에 설정된 IP 주소로 HTTP 요청을 전송해 인그레스가 올바르게 설정되었는지 확인합니다.

엔드포인트 `/coffee`에 대한 요청은 `coffee-svc` 서비스에 전달되어 `coffee` 파드가 응답합니다. 응답의 **Server name** 항목을 보면 `coffee` 파드들이 라운드-로빈 방식으로 번갈아 응답하는 것을 확인할 수 있습니다.

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

마찬가지로 엔드포인트 `/tea`에 대한 요청은 `tea-svc` 서비스에  전달되어 `tea` 파드가 응답합니다.

```
$ curl http://123.123.123.44/tea
Server address: 10.100.2.24:8080
Server name: tea-7df475c6-lxqsx
Date: 07/Apr/2020:08:25:03 +0000
URI: /tea
Request ID: 59303a5a5baa60802b463b1856c8ce8d
```

정의되지 않은 URI로 요청을 보내면 인그레스 컨트롤러가 `404 Not Found`를 응답합니다.

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

#### 리소스 삭제
테스트에 사용한 자원들은 생성할 때 사용한 매니페스트를 이용해 삭제할 수 있습니다.

```
$ kubectl delete -f cafe-ingress-uri.yaml
ingress.extensions "cafe-ingress-uri" deleted

$ kubectl delete -f cafe.yaml
deployment.apps "coffee" deleted
service "coffee-svc" deleted
deployment.apps "tea" deleted
service "tea-svc" deleted
```

### 호스트 기반 서비스 분기

![ingress-02.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/ingress-02.png)

#### 서비스와 파드 생성
[URI 기반 서비스 분기](/Container/Kubernetes/ko/user-guide/#uri)와 동일한 매니페스트를 이용해 서비스와 파드를 생성합니다.

#### 인그레스 생성
호스트 이름에 따라 서비스를 연결하는 인그레스 매니페스트를 작성합니다. `tea.cafe.example.com` 호스트로 들어온 요청은 `tea-svc` 서비스에 연결하고 `coffee.cafe.example.com` 호스트로 들어온 요청은 `coffee-svc` 서비스에 연결합니다.

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

인그레스를 생성하고 잠시 후 확인했을 때 **ADDRESS** 필드에 IP가 설정되어 있어야 합니다.

```
$ kubectl apply -f cafe-ingress-host.yaml
ingress.extensions/cafe-ingress-host created

$ kubectl get ingress
NAME                HOSTS                                          ADDRESS          PORTS   AGE
cafe-ingress-host   tea.cafe.example.com,coffee.cafe.example.com   123.123.123.44   80      4m29s
```

#### HTTP Request 전송
외부 호스트에서 인그레스의 ADDRESS에 설정된 IP로 HTTP 요청을 전송합니다. 다만 호스트 이름을 이용해 서비스를 분기하도록 인그레스를 구성했기 때문에 호스트 이름을 이용해 요청을 전송해야 합니다.

> [참고]
> 임의의 호스트 이름을 사용하여 테스트하려면 curl의 --resolve 옵션을 사용합니다. --resolve 옵션은 `{호스트 이름}:{포트 번호}:{IP}` 형식으로 입력합니다. 이는 {호스트 이름}으로 보내는 {포트번호}에 대한 요청을 {IP}로 해석(resolve)하라는 의미입니다.
> `/etc/host` 파일을 열어 `{IP} {호스트 이름}` 형식으로 추가할 수도 있습니다.

호스트 `coffee.cafe.example.com`로 요청을 전송하면 `coffee-svc` 서비스에 전달되어 `coffee` 파드가 응답합니다.

```
$ curl --resolve coffee.cafe.example.com:80:123.123.123.44 http://coffee.cafe.example.com/
Server address: 10.100.2.25:8080
Server name: coffee-67c6f7c5fd-2bbzf
Date: 07/Apr/2020:08:45:39 +0000
URI: /
Request ID: 29fd8a244b9f0a5ff5f35d1dc35edccf
```

호스트 `tea.cafe.example.com`로 요청을 전송하면 `tea-svc` 서비스에 전달되어 `tea` 파드가 응답합니다.

```
$ curl --resolve tea.cafe.example.com:80:123.123.123.44 http://tea.cafe.example.com/
Server address: 10.100.3.52:8080
Server name: tea-7df475c6-q8mdx
Date: 07/Apr/2020:08:53:44 +0000
URI: /
Request ID: fe61c1589d3ab8ef4ca4507245251ef3
```

알려지지 않은 호스트로 요청을 보내면 인그레스 컨트롤러가 `404 Not Found`를 응답합니다.

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

## Kubernetes 대시보드
TOAST Kubernetes 서비스는 기본 웹 UI 대시보드(dashboard)를 제공합니다. Kubernetes 대시보드에 대한 자세한 내용은 [웹 UI (대시보드)](https://kubernetes.io/ko/docs/tasks/access-application-cluster/web-ui-dashboard/) 문서를 참고하세요.

### 대시보드 권한 설정
대시보드를 사용하려면 사용자에게 접근 권한을 부여해야 합니다. 역할 기반 엑세스 제어에 대한 자세한 내용은 [Using RBAC Authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)을 참고하세요.

다음 명령은 사용자에게 모든 권한을 가진 클러스터 관리자 역할을 부여합니다.

```
$ kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
clusterrolebinding.rbac.authorization.k8s.io/kubernetes-dashboard created

$ kubectl describe clusterrolebinding kubernetes-dashboard -n kube-system
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

$ kubectl describe ClusterRole cluster-admin
Name:         cluster-admin
Labels:       kubernetes.io/bootstrapping=rbac-defaults
Annotations:  rbac.authorization.kubernetes.io/autoupdate: true
PolicyRule:
  Resources  Non-Resource URLs  Resource Names  Verbs
  ---------  -----------------  --------------  -----
  *.*        []                 []              [*]
             [*]                []              [*]
```

### 대시보드 서비스 공개
사용자 Kubernetes에는 대시보드를 공개하기 위한 `kubernetes-dashboard` 서비스 객체가 미리 생성되어 있습니다.

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

그러나 `kubernetes-dashboard` 서비스 객체는 ClusterIP 유형이기 때문에 아직 클러스터 외부에 공개되어 있지 않습니다. 대시보드를 외부 공개하려면 서비스 객체를 LoadBalancer 유형으로 변경하거나 인그레스 컨트롤러와 인그레스 객체를 생성해야 합니다.

#### LoadBalancer 서비스 객체로 변경

![dashboard-01.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/dashboard-01.png)

`LoadBalancer` 유형으로 서비스 객체를 변경하면 클러스터 외부에 TOAST Load Balancer가 생성되고, 외부 로드 밸런서와 서비스 객체가 연결됩니다. 서비스 객체를 조회했을 때 **EXTERNAL-IP** 필드에 로드 밸런서의 IP가 표시됩니다. `LoadBalancer` 유형의 서비스 객체에 대한 설명은 [LoadBalancer 서비스](/Container/Kubernetes/ko/user-guide/#loadbalancer)를 참고하세요.

웹 브라우저에서 `https://{EXTERNAL-IP}`로 접속하면 Kubernetes 대시보드 페이지가 로딩됩니다. 로그인을 위해 필요한 토큰은 [대시보드 엑세스 토큰](/Container/Kubernetes/ko/user-guide/#_24)을 참고하세요.

> [참고]
> 생성된 로드 밸런서는 **Network > Load Balancer** 페이지에서 확인할 수 있습니다.
> 로드 밸런서의 IP는 외부에서 접근할 수 있는 플로팅 IP입니다. **Network > Floating IP** 페이지에서 확인할 수 있습니다.

다음과 같이 `kubernetes-dashboard` 서비스 객체의 유형을 `LoadBalancer`로 변경합니다.

```
$ kubectl -n kube-system patch svc/kubernetes-dashboard -p '{"spec":{"type":"LoadBalancer"}}'
service/kubernetes-dashboard patched
```

`kubernetes-dashboard` 서비스 객체가 `LoadBalancer` 유형으로 변경되면 잠시 후 **EXTERNAL-IP** 필드에서 로드 밸런서 IP를 확인할 수 있습니다.

```
$ kubectl get svc -n kube-system
NAME                   TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                  AGE
...
kubernetes-dashboard   LoadBalancer   10.254.95.176   123.123.123.81   443:30963/TCP            2d23h
```

> [참고]
> Kubernetes 대시보드는 자동 생성되는 사설 인증서를 사용하기 때문에 웹 브라우저의 종류와 보안 설정에 따라 안전하지 않은 페이지로 표시될 수 있습니다.

#### 인그레스(Ingress)를 이용한 서비스 공개

![dashboard-02.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/dashboard-02.png)

인그레스는 클러스터 내부의 여러 서비스들로 접근하기 위한 라우팅을 제공하는 네트워크 객체입니다. 인그레스 객체의 설정은 인그래스 컨트롤러로 구동됩니다. 인그레스와 인그레스 컨트롤러에 대한 설명은 [인그레스 컨트롤러](/Container/Kubernetes/ko/user-guide/#_16)를 참고하세요.

[NGINX Ingress Controller 설치](/Container/Kubernetes/ko/user-guide/#nginx-ingress-controller)를 참고해 `NGINX Ingress Controller`를 설치하고 `LoadBalancer` 유형의 서비스를 생성합니다. 그리고 다음과 같이 인그레스 객체 생성을 위한 매니페스트를 작성합니다.

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

매니페스트를 적용해 인그레스를 생성하고 `ingress-nginx` 서비스 객체의 **EXTERNAL-IP** 필드를 확인합니다. 웹 브라우저에서 `https://{EXTERNAL-IP}`로 접속하면 Kubernetes 대시보드 페이지가 로딩됩니다. 로그인을 위해 필요한 토큰은 [대시보드 엑세스 토큰](/Container/Kubernetes/ko/user-guide/#_24)을 참고하세요.

```
$ kubectl apply -f kubernetes-dashboard-ingress-tls-passthrough.yaml
ingress.extensions/k8s-dashboard-ingress created

$ kubectl get service/ingress-nginx -n ingress-nginx
NAME            TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)                      AGE
ingress-nginx   LoadBalancer   10.254.211.113   123.123.123.29   80:32680/TCP,443:31631/TCP   19h
```

### 대시보드 엑세스 토큰
Kubernetes 대시보드에 로그인하려면 토큰이 필요합니다. 토큰은 다음 명령으로 얻을 수 있습니다.

```
# SECRET_NAME=$(kubectl -n kube-system get secrets | grep "kubernetes-dashboard-token" | cut -f1 -d ' ')

$ kubectl describe secret $SECRET_NAME -n kube-system | grep -E '^token' | cut -f2 -d':' | tr -d " "
eyJhbGc...-QmXA
```

출력된 토큰을 브라우저의 토큰 입력 창에 입력하면 클러스터 관리자 권한을 부여받은 사용자로 로그인할 수 있습니다.


## 퍼시스턴트 볼륨
퍼시스턴트 볼륨(Persistent Volume, PV)는 물리 저장 장치(volume)를 표현하는 Kubernetes의 자원입니다. 하나의 PV는 하나의 TOAST Block Storage와 연결됩니다. 자세한 내용은 [퍼시스턴트 볼륨](https://kubernetes.io/ko/docs/concepts/storage/persistent-volumes/) 문서를 참고하세요.

PV를 파드에 연결해 사용하려면 퍼시스턴트 볼륨 클레임(Persistent Volume Claims, PVC) 객체가 필요합니다. PVC는 용량, 읽기/쓰기 모드 등 필요한 볼륨의 요구 사항을 정의합니다.

PV와 PVC로 사용자는 사용하고 싶은 볼륨의 속성을 정의하고, 시스템은 사용자의 요구 사항에 맞는 볼륨 리소스를 할당하는 방식으로 자원의 사용과 관리를 분리합니다.

### PV/PVC의 생명 주기
PV와 PVC는 4단계의 생명 주기(life cycle)를 따릅니다.

* 프로비저닝(provisioning)
사용자가 직접 볼륨을 확보하고 PV를 생성(static provisioning)하거나 [스토리지 클래스](https://kubernetes.io/ko/docs/concepts/storage/storage-classes/)를 사용해 동적으로 생성(dynamic provisioning)할 수 있습니다.

* 바인딩(binding)
PV와 PVC를 1:1로 바인딩합니다. 동적 프로비저닝으로 PV를 생성했다면 바인딩도 자동으로 수행됩니다.

* 사용(using)
PV를 파드에 마운트해 사용합니다.

* 반환(reclaiming)
사용을 마친 볼륨을 회수합니다. 회수 방법은 삭제(Delete), 보존(Retain), 재사용(Recycle)이 있습니다.

| 방법 | 설명 |
| --- | --- |
| 삭제(Delete) | PV를 삭제할 때 연결된 볼륨을 함께 삭제합니다. |
| 보존(Retain) | PV를 삭제할 때 연결된 볼륨을 삭제하지 않습니다. 볼륨은 사용자가 직접 삭제하거나 재사용 할 수 있습니다. |
| 재사용(Recycle) | PV를 삭제할 때 연결된 볼륨을 삭제하지 않고 재사용할 수 있는 상태로 만듭니다. 이 방법은 사용 중단(deprecated) 되었습니다. |


### 정적 프로비저닝

정적 프로비저닝(static provisioning)은 사용자가 직접 블록 스토리지를 준비해야 합니다. TOAST 웹 콘솔의 **Storage > Block Storage** 서비스 페이지에서 **블록 스토리지 생성** 버튼을 클릭해 PV와 연결할 블록 스토리지를 생성합니다. 블록 스토리지 가이드의 [블록 스토리지 생성](/Storage/Block%20Storage/ko/console-guide/#_2)을 참고하세요.

PV를 생성하려면 블록 스토리지의 ID가 필요합니다. **Storage > Block Storage** 서비스 페이지의 블록 스토리지 목록에서 사용할 블록 스토리지를 선택합니다. 하단 **정보** 탭의 블록 스토리지 이름 항목에서 ID를 확인할 수 있습니다.  

> [주의]
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


### 동적 프로비저닝

동적 프로비저닝(dynamic provisioning)은 스토리지 클래스에 정의된 속성을 참조하여 자동으로 블록 스토리지를 생성합니다. 스토리지 클래스 매니페스트의 **parameters.type**에 TOAST Block Storage 유형을 지정할 수 있습니다. 지정하지 않으면 HDD 유형으로 설정됩니다.

| 타입 | 설정값 |
| --- | --- |
| HDD | General HDD |
| SSD | General SSD |

블록 스토리지는 노드 그룹과 같은 가용성 영역(availability zone)에 만들어야 연결할 수 있습니다. 스토리지 클래스 매니페스트의 **parameters.availability**에 블록 스토리지를 생성할 가용성 영역을 지정할 수 있습니다. 연결할 노드 그룹의 가용성 영역은 노드 그룹 목록에서 확인할 수 있습니다.

> [주의]
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

> [주의]
> 동적 프로비저닝으로 생성된 블록 스토리지는 웹 콘솔에서 삭제할 수 없습니다. 또한 클러스터를 삭제할 때 자동으로 삭제되지 않습니다. 따라서 클러스터를 삭제하기 전에 PVC를 모두 삭제해야 합니다. PVC를 삭제하지 않고 클러스터를 삭제하면 과금이 될 수 있습니다. 동적 프로비저닝을 생성된 PVC의 reclaimPolicy는 기본적으로 `Delete`로 설정되기 때문에 PVC만 삭제해도 PV와 블록 스토리지가 삭제됩니다.


### 파드에 PVC 마운트

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
