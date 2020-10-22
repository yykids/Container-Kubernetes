## Container > Kubernetes > 使用ガイド

## クラスター
クラスターは、ユーザーのKubernetesを構成するインスタンスのグループです。

### クラスター作成
Kubernetesサービスを使用するには、まずクラスターを作成する必要があります。**Container > Kubernetes**サービスページで**クラスター作成**ボタンを押すと、クラスター作成ページが表示されます。クラスターの作成に必要な項目は次のとおりです。

| 項目 | 説明 |
| --- | --- |
| クラスター名 | Kubernetesクラスターの名前。20文字以内の英数字、(-)、(.)で構成 |
| Kubernetesのバージョン | 使用するKubernetesのバージョン |
| VPC | クラスターに接続するVPCネットワーク |
| サブネット | VPCに定義されたサブネットのうち、クラスターを構成するインスタンスに接続するサブネット |
| イメージ | クラスターを構成するインスタンスに使用するイメージ |
| アベイラビリティゾーン | 基本ノードグループインスタンスを作成する領域 |
| インスタンスタイプ | 基本ノードグループインスタンスの仕様 |
| ノード数 | 基本ノードグループインスタンスの数 |
| キーペア | 基本ノードグループアクセスに使用するキーペア |
| ブロックストレージタイプ | 基本ノードグループインスタンスのブロックストレージの種類 |
| ブロックストレージサイズ | 基本ノードグループインスタンスのブロックストレージサイズ |

必要な情報を入力し、**クラスター作成**ボタンを押すと、クラスターの作成が始まります。クラスターリストで状態を確認できます。作成には約10分かかります。クラスターの設定によっては、さらに時間がかかる場合もあります。

> [参考]
> クラスターを作成すると、基本ノードグループが作成されます。基本ノードグループが作成された後は、ノード数を変更できません。追加ノードが必要な場合は、ノードグループを新たに作成する必要があります。


### クラスター照会
作成したクラスターは**Container > Kubernetes**サービスページで確認できます。クラスターを選択すると、下部にクラスター情報が表示されます。

| 項目 | 説明 |
| --- | --- |
| クラスター名 | Kubernetesクラスターの名前とID |
| ノード数 | クラスターを構成するすべてのノードインスタンス数 |
| Kubernetesバージョン | 使用中のKubernetesバージョン |
| VPC | クラスターに接続したVPCネットワーク |
| サブネット | クラスターを構成するノードインスタンスに接続したサブネット |
| APIエンドポイント | クラスターにアクセスして操作するためのAPIエンドポイントURI |
| 設定ファイル | クラスターにアクセスして操作するために必要な設定ファイルのダウンロードボタン |

### クラスター削除
削除するクラスターを選択し、**クラスター削除**ボタンを押すと削除が行われます。削除には約5分かかります。クラスターの状態によっては、さらに時間がかかる場合もあります。

## ノードグループ
ノードグループはKubernetesを構成するワーカーノードインスタンスのグループです。

### ノードグループ照会
クラスターリストからクラスター名を押すと、ノードグループリストを確認できます。ノードグループを選択すると、下部にノードグループ情報が表示されます。

* 基本情報
**基本情報**タブでは、次のような情報を確認できます。

| 項目 | 説明 |
| --- | --- |
| ノードグループ名 | ノードグループ名とID |
| クラスター名 | ノードグループが属しているクラスターの名前とID |
| Kubernetesバージョン | 使用中のKubernetesバージョン |
| アベイラビリティゾーン | ノードグループインスタンスが作成された領域 |
| インスタンスタイプ | ノードグループインスタンスの仕様 |
| イメージタイプ | ノードグループインスタンスに使用したイメージの種類 |
| ブロックストレージサイズ | ノードグループインスタンスのブロックストレージサイズ |
| 作成日 | ノードグループが作成された日時 |
| 修正日 | ノードグループが最後に修正された日時 |

* ノードリスト
**ノードリスト**タブでは、ノードグループを構成するインスタンスのリストを確認できます。

### ノードグループ作成
クラスターを作成すると、基本ノードグループが作成されますが、必要に応じて追加ノードグループを作成できます。基本ノードグループのインスタンスより高い仕様のコンテナ起動環境が必要な場合や、スケールアウト(scale out、拡張)のためにさらに多くのワーカーノードインスタンスが必要な場合は、追加ノードグループを作成して使用できます。ノードグループリストページで**ノードグループ作成**ボタンを押すと、ノードグループ作成ページが表示されます。ノードグループの作成に必要な項目は次のとおりです。

| 項目 | 説明 |
| --- | --- |
| アベイラビリティゾーン | クラスターを構成するインスタンスを作成する領域 |
| ノードグループ名 | 追加ノードグループ名、20文字以内の英数字、(-)、(.)で構成 |
| インスタンスタイプ | 追加ノードグループのインスタンス仕様 |
| ノード数 | 追加ノードグループインスタンス数 |
| キーペア | 追加ノードグループアクセスに使用するキーペア |
| ブロックストレージタイプ | 追加ノードグループインスタンスのブロックストレージ種類 |
| ブロックストレージサイズ | 追加ノードグループインスタンスのブロックストレージサイズ |

必要な情報を入力し、**ノードグループ作成**ボタンを押すと、ノードグループの作成が始まります。ノードグループリストで状態を確認できます。ノードグループの作成には約5分かかります。ノードグループの設定によっては、さらに時間がかかる場合もあります。

### ノードグループ削除
ノードグループリストから削除するノードグループを選択し、**ノードグループ削除**ボタンを押すと、削除が行われます。ノードグループの削除には約5分かかります。ノードグループの状態によっては、さらに時間がかかる場合もあります。

### GPUノードグループ使用 
KubernetesでGPU基盤ワークロードの実行が必要な場合、 GPUインスタンスで構成されたノードグループを作成できます。
クラスターまたはノードグループ作成プロセスでインスタンスタイプを選択する時、 `g2`タイプを選択するとGPUノードグループを作成できます。

> [参考]
> TOAST GPUインスタンスで提供されるGPUはNVIDIA系です。 ([使用可能なGPUの仕様を確認](/Compute/GPU%20Instance/ja/overview/#gpu))
> NVIDIA GPUを利用するために必要なKubernetesのnvidia-device-pluginは、GPUノードグループの作成時に自動的にインストールされます。

作成されたGPUノードの基本的な設定のヘルスチェックおよび簡単な動作テストは次のような方法を利用できます。

#### ノード水準のヘルスチェック
GPUノードに接続した後、`nvidia-smi`コマンドを実行します。
次のような内容が出力されればGPU driverが正常に動作しているということです。

```
$ nvidia-smi
Mon Jul 27 14:38:07 2020
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 418.152.00   Driver Version: 418.152.00   CUDA Version: 10.1     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  Tesla T4            Off  | 00000000:00:05.0 Off |                    0 |
| N/A   30C    P8     9W /  70W |      0MiB / 15079MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+

+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+ 
```

#### Kubernetes水準のヘルスチェック
`kubectl`コマンドを使用してクラスター水準で使用可能なGPUリソース情報を確認します。
以下は各ノードで使用可能なGPUコアの個数を出力するコマンドおよび実行結果です。

```
$ kubectl get nodes -A -o custom-columns='NAME:.metadata.name,GPU Allocatable:.status.allocatable.nvidia\.com/gpu,GPU Capacity:.status.capacity.nvidia\.com/gpu'
NAME                                       GPU Allocatable   GPU Capacity
my-cluster-default-w-vdqxpwisjjsk-node-1   1                 1
```

#### GPUテストのためのサンプルワークロード実行
Kubernetesクラスターに属すGPUノードはCPUとメモリの他に`nvidia.com/gpu`という名前のリソースを提供します。
GPUを使用したい場合は`nvidia.com/gpu`リソースを割り当てられるように、下記のサンプルファイルのように入力してください。

* resnet.yaml
```
apiVersion: v1
kind: Pod
metadata:
  name: resnet-gpu-pod
spec:
  imagePullSecrets:
    - name: nvcr.dgxkey
  containers:
    - name: resnet
      image: nvcr.io/nvidia/tensorflow:18.07-py3
      command: ["mpiexec"]
      args: ["--allow-run-as-root", "--bind-to", "socket", "-np", "1", "python", "/opt/tensorflow/nvidia-examples/cnn/resnet.py", "--layers=50", "--precision=fp16", "--batch_size=64", "--num_iter=90"]
      resources:
        limits:
          nvidia.com/gpu: 1
``` 

上記のファイルを実行すると次のような結果を確認できます。

```
$ kubectl create -f resnet.yaml
pod/resnet-gpu-pod created

$ kubectl get pods resnet-gpu-pod
NAME             READY   STATUS    RESTARTS   AGE
resnet-gpu-pod   0/1     Running   0          17s 

$ kubectl logs resnet-gpu-pod -n default -f
PY 3.5.2 (default, Nov 23 2017, 16:37:01)
[GCC 5.4.0 20160609]
TF 1.8.0
Script arguments:
  --layers 50
  --display_every 10
  --iter_unit epoch
  --batch_size 64
  --num_iter 100
  --precision fp16
Training
WARNING:tensorflow:Using temporary folder as model directory: /tmp/tmpjw90ypze
2020-07-31 00:57:23.020712: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:898] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2020-07-31 00:57:23.023190: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1356] Found device 0 with properties:
name: Tesla T4 major: 7 minor: 5 memoryClockRate(GHz): 1.59
pciBusID: 0000:00:05.0
totalMemory: 14.73GiB freeMemory: 14.62GiB
2020-07-31 00:57:23.023226: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1435] Adding visible gpu devices: 0
2020-07-31 00:57:23.846680: I tensorflow/core/common_runtime/gpu/gpu_device.cc:923] Device interconnect StreamExecutor with strength 1 edge matrix:
2020-07-31 00:57:23.846743: I tensorflow/core/common_runtime/gpu/gpu_device.cc:929]      0
2020-07-31 00:57:23.846753: I tensorflow/core/common_runtime/gpu/gpu_device.cc:942] 0:   N
2020-07-31 00:57:23.847023: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1053] Created TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:0 with 14151 MB memory) -> physical GPU (device: 0, name: Tesla T4, pci bus id: 0000:00:05.0, compute capability: 7.5)
  Step Epoch Img/sec   Loss  LR
     1   1.0     3.1  7.936  8.907 2.00000
    10  10.0    68.3  1.989  2.961 1.65620
    20  20.0   214.0  0.002  0.978 1.31220
    30  30.0   213.8  0.008  0.979 1.00820
    40  40.0   210.8  0.095  1.063 0.74420
    50  50.0   211.9  0.261  1.231 0.52020
    60  60.0   211.6  0.104  1.078 0.33620
    70  70.0   211.3  0.340  1.317 0.19220
    80  80.0   206.7  0.168  1.148 0.08820
    90  90.0   210.4  0.092  1.073 0.02420
   100 100.0   210.4  0.001  0.982 0.00020
```

> [参考]
> GPUが必要ないワークロードがGPUノードに割り当てられることを防ぎたい場合は[TaintおよびTolerationの概要](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/)を参照してください。


## クラスター管理
遠隔のホストからクラスターを操作し、管理するには、Kubernetesが提供するコマンドラインツール(CLI)、`kubectl`が必要です。

### kubectlインストール
kubectlは、インストール不要で、実行ファイルをダウンロードしてすぐに使用できます。各OSのダウンロードパスは次のとおりです。

| OS | ダウンロードコマンド |
| --- | --- |
| Linux | curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/linux/amd64/kubectl |
| MacOS | curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/darwin/amd64/kubectl |
| Windows | curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.15.7/bin/windows/amd64/kubectl.exe |

その他、インストール方法とオプションなどの詳細は、[Install and Set Up kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)文書を参照してください。

#### 権限変更
ダウンロードしたファイルは基本的に実行権限がありません。実行権限を追加する必要があります。

```
$ chmod +x kubectl
```

#### 位置変更またはパス指定
どのパスからでもkubectlを実行できるように環境変数に指定されたパスに移すか、kubectlがあるパスを環境変数に追加します。

* 環境変数に指定したパスへ移動
```
$ sudo mv kubectl /usr/local/bin/
```

* 環境変数にパスを追加
```
// kubectlがあるパスで実行
$ export PATH=$PATH:$(pwd)
```

### 設定
kubectlでKubernetesクラスターにアクセスするには、クラスター設定ファイル(kubeconfig)が必要です。TOAST Webコンソールで**Container > Kubernetes**サービスページを開き、アクセスするクラスターを選択します。下部、**基本情報**タブで**設定ファイル**項目の**ダウンロード**ボタンを押して設定ファイルをダウンロードします。ダウンロードした設定ファイルは、任意の位置へ移動させ、kubectl実行時に参照できるように準備します。

> [注意]
> TOAST Webコンソールからダウンロードした設定ファイルは、クラスター情報と認証のためのトークンなどが含まれています。設定ファイルがある場合は該当Kubernetesクラスターにアクセスできる権限を持ちます。設定ファイルを絶対に紛失しないように注意してください。

kubectlは実行するたびにクラスター設定ファイルが必要です。したがって、毎回`--kubeconfig`オプションを利用してクラスター設定ファイルを指定する必要があります。しかし、環境変数にクラスター設定ファイルパスが保存されている場合は、毎回オプションを指定する必要はありません。

```
$ export KUBECONFIG={クラスター設定ファイルパス}
```

クラスター設定ファイルのパスを環境変数に保存したくない場合は、kubectlの基本設定ファイル、`$HOME/.kube/config`にコピーして使用することもできます。しかし、クラスターを複数運用する場合は、環境変数の値を変更する方法が便利です。

### 接続確認
`kubectl version`コマンドで、正常に設定できているかを確認します。問題がなければ`Server Version`が出力されます。

```
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"15", GitVersion:"v1.15.7", GitCommit:"6c143d35bb11d74970e7bc0b6c45b6bfdffc0bd4", GitTreeState:"clean", BuildDate:"2019-12-11T12:42:56Z", GoVersion:"go1.12.12", Compiler:"gc", Platform:"darwin/amd64"}
Server Version: version.Info{Major:"1", Minor:"15", GitVersion:"v1.15.7", GitCommit:"6c143d35bb11d74970e7bc0b6c45b6bfdffc0bd4", GitTreeState:"clean", BuildDate:"2019-12-11T12:34:17Z", GoVersion:"go1.12.12", Compiler:"gc", Platform:"linux/amd64"}
```

* Client Version：実行したkubectlファイルのバージョン情報
* Server Version：クラスターを構成しているKubernetesのバージョン情報

## LoadBalancerサービス
Kubernetesアプリケーションの基本実行単位Podは、CNI(Container Network Interface)でクラスターネットワークに接続されます。基本的にクラスターの外部からPodにはアクセスできません。Podのサービスをクラスターの外部に公開するにはKubernetesの`LoadBalancer`サービス(Service)オブジェクト(object)を利用して外部に公開するパスを作成する必要があります。LoadBalancerサービスオブジェクトを作成すると、クラスターの外部にTOAST Load Balancerが作成され、サービスオブジェクトと接続されます。

### WebサーバーPod作成
次のように2個のnginx Podを実行するデフォルトデプロイメント(deployment)オブジェクトマニフェストファイルを作成し、オブジェクトを作成します。

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

デプロイメントオブジェクトを作成すると、マニフェストに定義したPodが自動的に作成されます。

```
$ kubectl apply -f nginx.yaml
deployment.apps/nginx-deployment created

$ kubectl get pods
NAME                                READY   STATUS    RESTARTS   AGE  
nginx-deployment-7fd6966748-pvrzs   1/1     Running   0          4m13s
nginx-deployment-7fd6966748-wv7rd   1/1     Running   0          4m13s
```

TOAST Container Registryに保存したイメージを使用したい場合は、先にユーザーレジストリにログインするためのシークレット(secret)を作成する必要があります。

```
$ kubectl create secret docker-registry registry-credential --docker-server={ユーザーレジストリアドレス} --docker-username={Toastアカウントemailアドレス} --docker-password={サービスAppkeyまたは統合Appkey}
secret/registry-credential created

$ kubectl get secrets
NAME                  TYPE                             DATA   AGE
registry-credential   kubernetes.io/dockerconfigjson   1      30m
```

デプロイメントマニフェストファイルにシークレット情報を追加し、イメージ名を変更すると、ユーザーレジストリに保存されたイメージを利用してPodを作成できます。

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
        image: {ユーザーレジストリアドレス}/nginx:1.14.2
        ...
      imagePullSecrets:
      - name: regcred

```

> [参考]
> TOAST Container Registryの使用方法は[Container Registry使用ガイド](/Container/Container%20Registry/ja/user-guide)文書を参照してください。

### LoadBalancerサービスの作成
Kubernetesのサービスオブジェクトを定義するには、次の項目で構成されたマニフェストが必要です。

| 項目 | 説明 |
| --- | --- |
| metadata.name | サービスオブジェクトの名前 |
| spec.selector | サービスオブジェクトと接続するPodの名前 |
| spec.ports | 外部ロードバランサーから流入するトラフィックをPodに伝達するインターフェイス設定 |
| spec.ports.name | インターフェイス名 |
| spec.ports.protocol | インターフェイスで使用するプロトコル(例：TCP) |
| spec.ports.port | サービスオブジェクトの外部に公開するポート番号 |
| spec.ports.targetPort | サービスオブジェクトと接続するPodのポート番号 |
| spec.type | サービスオブジェクトタイプ |

次のようにサービスマニフェストを作成します。このLoadBalancerサービスオブジェクトは**spec.selector**に定義された名前に応じて`app: nginx`ラベルがついたPodと接続されます。そして**spec.ports**に定義されたとおりにTCP/8080ポートに流入するトラフィックをPodのTCP/80ポートへ伝達します。

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

LoadBalancerサービスオブジェクトを作成すると、クラスターの外部にロードバランサーを作成して接続するまで、若干の時間が必要です。外部ロードバランサーと接続されるまで**EXTERNAL-IP**項目が`<pending>`と表示されます。

```
$ kubectl apply -f service.yaml
service/nginx-svc created

$ kubectl get service
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
nginx-svc    LoadBalancer   10.254.134.18   <pending>     8080:30013/TCP   11s
```

外部ロードバランサーと接続すると、**EXTERNAL-IP**項目にIPが表示されます。このIPは外部ロードバランサーのFloating IPです。

```
$ kubectl get service
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)          AGE
nginx-svc    LoadBalancer   10.254.134.18   123.123.123.30   8080:30013/TCP   3m13s
```

> [参考]
> 作成されたロードバランサーは、**Network > Load Balancer**ページで確認できます。
> ロードバランサーのIPは、外部からアクセスできるFloating IPです。**Network > Floating IP**ページで確認できます。


### インターネットによるサービステスト
ロードバランサーに設定されたFloating IPにHTTPリクエストを送ってKubernetesクラスターのWebサーバーPodが応答するかを確認します。サービスオブジェクトのTCP/8080ポートをPodのTCP/80ポートと接続するように設定したため、TCP/8080ポートにリクエストを送る必要があります。外部ロードバランサーとサービスオブジェクト、Podが正常に接続されていれば、Webサーバーはnginx基本ページをレスポンスします。

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


## イングレスコントローラー
イングレスコントローラー(ingress controller)は、イングレス(Ingress)オブジェクトに定義されたルールを参照してクラスター外部から内部サービスへHTTPとHTTPSリクエストをルーティングしてSSL/TSL終了、仮想ホスティングなどを提供します。イングレスコントローラーとイングレスの詳細な内容は[イングレスコントローラー](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/), [イングレス](https://kubernetes.io/docs/concepts/services-networking/ingress/)文書を参照してください。


### NGINX Ingress Controllerのインストール
NGINX Ingress Controllerは、数多く使用されているイングレスコントローラーの中の1つです。詳細は[NGINX Ingress Controller](https://kubernetes.github.io/ingress-nginx/)と[NGINX Ingress Controller for Kubernetes](https://docs.nginx.com/nginx-ingress-controller/overview/)文書を参照してください。

NGINX Ingress Controllerは、必要なリソースをすぐに作成できるように、あらかじめ定義したマニフェストファイルを提供します。このマニフェストを利用すると、簡単に必要なリソースを作成できます。

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

### LoadBalancerサービス作成
イングレスコントローラーは、Podに作成されるため、外部に公開するにはLoadBalancerサービスまたはNodePortサービスを作成する必要があります。次のようにHTTPとHTTPSを処理できるLoadBalancerサービスマニフェストを定義します。

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

サービスオブジェクトを作成し、外部ロードバランサーが接続されているかを確認します。**EXTERNAL-IP**フィールドにはFloating IPアドレスが設定されている必要があります。

```
$ kubectl apply -f ingress-nginx-lb.yaml
service/ingress-nginx created

$ kubectl get svc -n ingress-nginx
NAME            TYPE           CLUSTER-IP     EXTERNAL-IP      PORT(S)                      AGE
ingress-nginx   LoadBalancer   10.254.2.128   123.123.123.41   80:30820/TCP,443:30269/TCP   39s
```

### URIを元にサービス分岐
イングレスコントローラーは、URIを元にサービスを分岐できます。下記の図はURIを元にサービスを分岐する簡単な例です。

![ingress-01.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/ingress-01.png)

#### サービスとPodの作成
次のようにサービスとPodを作成するためのマニフェストを作成します。`tea-svc`サービスには`tea`Podを接続し、`coffee-svc`サービスには`coffee`Podを接続します。

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

マニフェストを適用し、デプロイメント、サービス、Podが作成されているかを確認します。Podは**Running**状態になっている必要があります。

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

#### イングレス(Ingress)作成
リクエストパスに応じてサービスを接続するイングレスマニフェストを作成します。エンドポイントが`/tea`のリクエストは`tea-svc`サービスに接続し、`/coffee`のリクエストは`coffee-svc`サービスに接続します。

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

イングレスを作成した後、**ADDRESS**フィールドにIPが設定されている必要があります。

```
$ kubectl apply -f cafe-ingress-uri.yaml
ingress.extensions/cafe-ingress-uri created

$ kubectl get ingress cafe-ingress-uri
NAME               HOSTS   ADDRESS          PORTS   AGE
cafe-ingress-uri   *       123.123.123.44   80      88s
```

#### HTTPリクエスト転送
外部ホストから、ingressの**ADDRESS**フィールドに設定されたIPアドレスにHTTPリクエストを転送し、イングレスが正しく設定されたかを確認します。

エンドポイント`/coffee`に対するリクエストは`coffee-svc`サービスに伝達され、`coffee` Podがレスポンスします。レスポンスの**Server name**項目を見ると`coffee`Podがラウンド-ロビン方式で交互にレスポンスすることを確認できます。

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

同様に、エンドポイント`/tea`に対するリクエストは`tea-svc`サービスに伝達され、`tea`Podがレスポンスします。

```
$ curl http://123.123.123.44/tea
Server address: 10.100.2.24:8080
Server name: tea-7df475c6-lxqsx
Date: 07/Apr/2020:08:25:03 +0000
URI: /tea
Request ID: 59303a5a5baa60802b463b1856c8ce8d
```

定義されていないURIにリクエストを送ると、イングレスコントローラーが`404 Not Found`をレスポンスします。

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

#### リソース削除
テストに使用したリソースは、作成する時に使用したマニフェストを利用して削除できます。

```
$ kubectl delete -f cafe-ingress-uri.yaml
ingress.extensions "cafe-ingress-uri" deleted

$ kubectl delete -f cafe.yaml
deployment.apps "coffee" deleted
service "coffee-svc" deleted
deployment.apps "tea" deleted
service "tea-svc" deleted
```

### ホストを元にサービス分岐
イングレスコントローラーは、ホスト名を元にサービスを分岐できます。下の図はホスト名を元にサービスを分岐する簡単な例です。

![ingress-02.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/ingress-02.png)

#### サービスとPod作成
[URIを元にサービス分岐](/Container/Kubernetes/ja/user-guide/#uri)と同じマニフェストを利用してサービスとPodを作成します。

#### イングレス作成
ホスト名に応じてサービスを接続するイングレスマニフェストを作成します。`tea.cafe.example.com`ホストに入ったリクエストは`tea-svc`サービスに接続し、`coffee.cafe.example.com`ホストに入ったリクエストは`coffee-svc`サービスに接続します。

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

イングレスを作成した後、**ADDRESS**フィールドにIPが設定されている必要があります。

```
$ kubectl apply -f cafe-ingress-host.yaml
ingress.extensions/cafe-ingress-host created

$ kubectl get ingress
NAME                HOSTS                                          ADDRESS          PORTS   AGE
cafe-ingress-host   tea.cafe.example.com,coffee.cafe.example.com   123.123.123.44   80      4m29s
```

#### HTTP Request転送
外部ホストから、イングレスのADDRESSに設定されたIPへHTTPリクエストを転送します。ただし、ホスト名を利用してサービスを分岐するようにイングレスを構成したため、ホスト名を利用してリクエストを送る必要があります。

> [参考]
> 任意のホスト名を使用してテストするにはcurlの--resolveオプションを使用します。--resolveオプションは`{ホスト名}:{ポート番号}:{IP}`形式で入力します。これは{ホスト名}に送る{ポート番号}に対するリクエストを{IP}で解釈(resolve)するという意味です。
> `/etc/host`ファイルを開き、`{IP} {ホスト名}`形式で追加することもできます。

ホスト`coffee.cafe.example.com`へリクエストを送ると、`coffee-svc`サービスに伝達され、`coffee`Podがレスポンスします。

```
$ curl --resolve coffee.cafe.example.com:80:123.123.123.44 http://coffee.cafe.example.com/
Server address: 10.100.2.25:8080
Server name: coffee-67c6f7c5fd-2bbzf
Date: 07/Apr/2020:08:45:39 +0000
URI: /
Request ID: 29fd8a244b9f0a5ff5f35d1dc35edccf
```

ホスト`tea.cafe.example.com`へリクエストを送ると、`tea-svc`サービスに伝達され、`tea`Podがレスポンスします。

```
$ curl --resolve tea.cafe.example.com:80:123.123.123.44 http://tea.cafe.example.com/
Server address: 10.100.3.52:8080
Server name: tea-7df475c6-q8mdx
Date: 07/Apr/2020:08:53:44 +0000
URI: /
Request ID: fe61c1589d3ab8ef4ca4507245251ef3
```

不明なホストへリクエストを送ると、イングレスコントローラーが`404 Not Found`をレスポンスします。

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

## Kubernetesダッシュボード
TOAST Kubernetesサービスは、基本Web UIダッシュボード(dashboard)を提供します。Kubernetesダッシュボードの詳細は、[Web UI (ダッシュボード)](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/)文書を参照してください。

### ダッシュボードサービス公開
ユーザーKubernetesにはダッシュボードを公開するための`kubernetes-dashboard`サービスオブジェクトがあらかじめ作成されています。

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

しかし、`kubernetes-dashboard`サービスオブジェクトはClusterIPタイプのため、まだクラスターの外部に公開されていません。ダッシュボードを外部へ公開するには、サービスオブジェクトをLoadBalancerタイプに変更するか、イングレスコントローラーとイングレスオブジェクトを作成する必要があります。

#### LoadBalancerサービスオブジェクトに変更

サービスオブジェクトを`LoadBalancer`タイプに変更すると、クラスターの外部にTOAST Load Balancerが作成され、ロードバランサー、サービスオブジェクトと接続されます。ロードバランサーと接続したサービスオブジェクトを照会すると、**EXTERNAL-IP**フィールドにロードバランサーのIPが表示されます。`LoadBalancer`タイプのサービスオブジェクトの詳細は[LoadBalancerサービス](/Container/Kubernetes/ja/user-guide/#loadbalancer)を参照してください。下の図は`LoadBalancer`タイプのサービスを利用してダッシュボードを外部に公開する構造を表しています。

![dashboard-01.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/dashboard-01.png)

次のように、`kubernetes-dashboard`サービスオブジェクトのタイプを`LoadBalancer`に変更します。

```
$ kubectl -n kube-system patch svc/kubernetes-dashboard -p '{"spec":{"type":"LoadBalancer"}}'
service/kubernetes-dashboard patched
```

`kubernetes-dashboard`サービスオブジェクトが`LoadBalancer`タイプに変更した後、しばらくすると**EXTERNAL-IP**フィールドでロードバランサーのIPを確認できます。

```
$ kubectl get svc -n kube-system
NAME                   TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                  AGE
...
kubernetes-dashboard   LoadBalancer   10.254.95.176   123.123.123.81   443:30963/TCP            2d23h
```

> [参考]
> 作成されたロードバランサーは、**Network > Load Balancer**ページで確認できます。
> ロードバランサーのIPは、外部からアクセスできるFloating IPです。**Network > Floating IP**ページで確認できます。

Webブラウザで`https://{EXTERNAL-IP}`に接続すると、Kubernetesダッシュボードページがローディングされます。ログインするために必要なトークンは[ダッシュボードアクセストークン](/Container/Kubernetes/ja/user-guide/#_23)を参照してください。

> [参考]
> Kubernetesダッシュボードは、自動作成されるプライベート証明書を使用するため、Webブラウザの種類とセキュリティ設定によっては安全ではないページと表示される場合があります。

#### イングレス(Ingress)を利用したサービス公開

イングレスは、クラスター内部の複数のサービスにアクセスするためのルーティングを提供するネットワークオブジェクトです。イングレスオブジェクトの設定はイングレスコントローラーで起動します。`kubernetes-dashboard`サービスオブジェクトは、イングレスを通して公開できます。イングレスとイングレスコントローラーの詳細は[イングレスコントローラー](/Container/Kubernetes/ja/user-guide/#_16)を参照してください。下の図はイングレスを通してダッシュボードを外部に公開する構造を表しています。

![dashboard-02.png](http://static.toastoven.net/prod_infrastructure/container/kubernetes/dashboard-02.png)

[NGINX Ingress Controllerインストール](/Container/Kubernetes/ja/user-guide/#nginx-ingress-controller)を参照して`NGINX Ingress Controller`をインストールし、`LoadBalancer`タイプのサービスを作成します。そして、次のようにイングレスオブジェクトを作成するためのマニフェストを作成します。

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

マニフェストを適用してイングレスを作成し、`ingress-nginx`サービスオブジェクトの**EXTERNAL-IP**フィールドを確認します。

```
$ kubectl apply -f kubernetes-dashboard-ingress-tls-passthrough.yaml
ingress.extensions/k8s-dashboard-ingress created

$ kubectl get service/ingress-nginx -n ingress-nginx
NAME            TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)                      AGE
ingress-nginx   LoadBalancer   10.254.211.113   123.123.123.29   80:32680/TCP,443:31631/TCP   19h
```

Webブラウザで`https://{EXTERNAL-IP}`に接続すると、Kubernetesダッシュボードページがローディングされます。ログインするために必要なトークンは[ダッシュボードアクセストークン](/Container/Kubernetes/ja/user-guide/#_23)を参照してください。

### ダッシュボードアクセストークン
Kubernetesダッシュボードにログインするにはトークンが必要です。トークンは次のコマンドで取得できます。

```
# SECRET_NAME=$(kubectl -n kube-system get secrets | grep "kubernetes-dashboard-token" | cut -f1 -d ' ')

$ kubectl describe secret $SECRET_NAME -n kube-system | grep -E '^token' | cut -f2 -d':' | tr -d " "
eyJhbGc...-QmXA
```

出力されたトークンをブラウザのトークン入力ウィンドウに入力すると、クラスター管理者権限を付与されたユーザーとしてログインできます。


## パシステントボリューム
パシステントボリューム(Persistent Volume、PV)は物理保存装置(volume)を表現するKubernetesのリソースです。1つのPVは1つのTOAST Block Storageと接続されます。詳細は[パシステントボリューム](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)文書を参照してください。

PVをPodに接続して使用するには、パシステントボリュームクレーム(Persistent Volume Claims、PVC)オブジェクトが必要です。PVCは容量、読み取り/書き込みモードなど、ボリュームの要求事項を定義します。

PVとPVCで、ユーザーは使用したいボリュームのプロパティを定義し、システムはユーザーの要求事項通りにボリュームリソースを割り当てる方式で、リソースの使用と管理を分離します。

### PV/PVCのライフサイクル
PVとPVCは4段階のライフサイクル(life cycle)に従います。

* プロビジョニング(provisioning)
ユーザーが直接ボリュームを確保してPVを作成(static provisioning)したり、[ストレージクラス](https://kubernetes.io/docs/concepts/storage/storage-classes/)を使用して動的に作成(dynamic provisioning)できます。

* バインディング(binding)
PVとPVCを1:1でバインディングします。動的プロビジョニングでPVを作成した場合、バインディングも自動的に実行されます。

* 使用(using)
PVをPodにマウントして使用します。

* 返却(reclaiming)
使用を終えたボリュームを回収します。回収方法は削除(Delete)、保存(Retain)、再使用(Recycle)があります。

| 方法 | 説明 |
| --- | --- |
| 削除(Delete) | PVを削除する時、接続されたボリュームを一緒に削除します。|
| 保存(Retain) | PVを削除する時、接続されたボリュームを削除しません。ボリュームはユーザーが直接削除または、再使用できます。|
| 再使用(Recycle) | PVを削除する時、接続されたボリュームを削除せず、再使用できる状態にします。この方法は使用を中断(deprecated)しています。|


### 静的プロビジョニング

静的プロビジョニング(static provisioning)は、ユーザーが直接ブロックストレージを準備する必要があります。TOAST Webコンソールの**Storage > Block Storage**サービスページで**ブロックストレージ作成**ボタンを押して、PVと接続するブロックストレージを作成します。ブロックストレージガイドの[ブロックストレージ作成](/Storage/Block%20Storage/ja/console-guide/#_2)を参照してください。

PVを作成するにはブロックストレージのIDが必要です。**Storage > Block Storage**サービスページのブロックストレージリストから使用するブロックストレージを選択します。下部**情報**タブのブロックストレージ名項目でIDを確認できます。

> [注意]
> ブロックストレージと、Podを起動するノードグループインスタンスのアベイラビリティゾーンは、同じにする必要があります。アベイラビリティゾーンが異なると接続できません。

ストレージクラスマニフェストを作成します。TOAST Block Storageを使用するには**provisioner**を必ず`kubernetes.io/cinder`に設定する必要があります。

```yaml
# storage_class.yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: sc-default
provisioner: kubernetes.io/cinder
```

ストレージクラスを作成し、確認します。

```
$ kubectl apply -f storage_class.yaml
storageclass.storage.k8s.io/sc-default created

$ kubectl get sc
NAME         PROVISIONER            AGE
sc-default   kubernetes.io/cinder   8s
```

ブロックストレージと、接続するPVマニフェストを作成します。**spec.storageClassName**にはストレージクラス名を入力します。TOAST Block Storageを使用するには**spec.accessModes**は`ReadWriteOnce`に設定する必要があります。**spec.presistentVolumeReclaimPolicy**は`Delete`または`Retain`に設定できます。

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

PVを作成し、確認します。

```
$ kubectl apply -f pv-static.yaml
persistentvolume/pv-static-001 created

$ kubectl get pv -o wide
NAME            CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS   REASON   AGE   VOLUMEMODE
pv-static-001   10Gi       RWO            Delete           Available           sc-default              7s    Filesystem
```

作成したPVを使用するためのPVCマニフェストを作成します。**spec.volumeName**にはPVの名前を指定する必要があります。他の項目はPVマニフェストの内容と同じように設定します。

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

PVCを作成し、確認します。

```
$ kubectl apply -f pvc-static.yaml
persistentvolumeclaim/pvc-static created

$ kubectl get pvc -o wide
NAME         STATUS   VOLUME          CAPACITY   ACCESS MODES   STORAGECLASS   AGE   VOLUMEMODE
pvc-static   Bound    pv-static-001   10Gi       RWO            sc-default     7s    Filesystem
```

PVCを作成した後、PVの状態を照会すると、**CLAIM**項目にPVC名が指定され、**STATUS**項目が`Bound`に変更されていることを確認できます。

```
$ kubectl get pv -o wide
NAME            CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                STORAGECLASS   REASON   AGE   VOLUMEMODE
pv-static-001   10Gi       RWO            Delete           Bound    default/pvc-static   sc-default              79s   Filesystem
```


### 動的プロビジョニング

動的プロビジョニング(dynamic provisioning)は、ストレージクラスに定義されたプロパティを参照して自動的にブロックストレージを作成します。ストレージクラスマニフェストの**parameters.type**にTOAST Block Storageタイプを指定できます。指定しない場合は、HDDタイプに設定されます。

| タイプ | 設定値 |
| --- | --- |
| HDD | General HDD |
| SSD | General SSD |

ブロックストレージはノードグループと同じアベイラビリティゾーン(availability zone)に作成すると接続できます。ストレージクラスマニフェストの**parameters.availability**に、ブロックストレージを作成するアベイラビリティゾーンを指定できます。接続するノードグループのアベイラビリティゾーンは、ノードグループリストで確認できます。

> [注意]
> ストレージクラスマニフェストにアベイラビリティゾーンを指定しない場合、任意のアベイラビリティゾーンにブロックストレージを作成します。ブロックストレージがノードグループと異なるアベイラビリティゾーンに作成されると接続ができない場合があるため、アベイラビリティゾーンを指定する必要があります。

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

動的プロビジョニングは、PVを作成する必要がありません。したがってPVCマニフェストには**spec.volumeName**を設定しません。

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

PVCを作成すると、PVが自動的に作成されます。PVに接続されたブロックストレージも自動的に作成され、TOAST Webコンソール**Storage > Block Storage**サービスページのブロックストレージリストで確認できます。

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

> [注意]
> 動的プロビジョニングで作成されたブロックストレージは、Webコンソールで削除できません。また、クラスターを削除する時、自動的に削除されません。したがって、クラスターを削除する前にPVCを全て削除する必要があります。PVCを削除しないでクラスターを削除すると、課金される場合があります。動的プロビジョニングを作成したPVCのreclaimPolicyは基本的に`Delete`が設定されているため、PVCを削除すればPVとブロックストレージが削除されます。


### PodにPVCマウント

PodにPVCをマウントするには、Podマニフェストにマウント情報を定義する必要があります。`spec.volumes.persistenVolumeClame.claimName`に使用するPVC名を入力します。そして`spec.containers.volumeMounts.mountPath`にマウントするパスを入力します。

下記の例は、静的プロビジョニングで作成したPVCをPodの`/usr/share/nginx/html`にマウントします。

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

Podを作成し、ブロックストレージがマウントされているかを確認します。

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

TOAST Webコンソール**Storage > Block Storage**サービスページでも、ブロックストレージの接続情報を確認できます。
