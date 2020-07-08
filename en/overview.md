## Container > Kubernetes > Overview
This document briefly describes what Kubernetes is about, as well as TOAST Kubernetes in particular. 여기에서는 Kubernetes(쿠버네티스)가 무엇인지 간략히 알아보고, TOAST에서 제공하는 Kubernetes 서비스를 살펴봅니다.

## Kubernetes
Kubernetes is an open-source platform which manages contianerized workload and services. Following features are available: 는 컨테이너화된 워크로드와 서비스를 관리할 수 있는 오픈소스 플랫폼입니다. Kubernetes는 다음과 같은 기능을 제공합니다.

* 서비스 디스커버리와 로드 밸런싱 Service discovery and load balancing 
* 스토리지 오케스트레이션 Storage orchestration 
* 자동화된 롤아웃과 롤백 Automated rollouts and rollbacks 
* 자동화된 빈 패킹(bin packing) Automated bin packing 
* 자동화된 복구(self-healing) Self-healing
* 시크릿과 구성 관리 Secret and configuration management 

자세한 내용은 아래 Kubernetes 문서를 참고하시기 바랍니다. For more details, see the following documents on Kubernetes:  

* [What is Kubernetes쿠버네티스란 무엇인가?](https://kubernetes.io/docs/concepts/overview/what-is-kubernetes/)

## Kubernetes 클러스터 Cluster 
A Kubernetes cluster is a computer cluster 클러스터는 서로 연결되어 하나의 유닛처럼 동작하는 컴퓨터 클러스터입니다. Kubernetes가 제공하는 기능은 클러스터 단위로 동작하며, 클러스터 단위로 설정할 수 있습니다. Kubernetes provides cluster-based features

### 구성 Configuration 
A Kubernetes cluster consists of a master and nodes.  클러스터는 마스터와 노드로 구성됩니다.

#### 마스터 Master 
마스터는 클러스터 관리를 담당합니다. 애플리케이션을 스케줄링하거나 스케일링, 업데이트하는 등 클러스터 내의 모든 활동을 관리합니다. 일반적으로 마스터의 구성 요소들은 별도의 머신(가상 머신 혹은 물리 머신)에서 구동됩니다. 고가용성 보장을 위해 한 클러스터에 다수의 마스터를 구성할 수도 있습니다. Master is in charge of cluster management. All activites of a cluster, such as application scheduling, scaling, or updating are managed. Master components, in general, run on seperate machines (virtual or physical machine). To ensure high availability, a cluster can be composed of many masters. 

#### 노드 Nodes
노드는 사용자의 애플리케이션이 구동되는 워커 머신입니다. 하나의 클러스터에는 다수의 노드가 존재할 수 있습니다. 노드는 마스터와 연결해야 동작됩니다. 마스터의 애플리케이션 구동, 정지 등의 명령에 따라 그대로 수행합니다. A node is a worker machine where user's application runs. One cluster may contain many nodes, which can run when connected to the master node. 


## TOAST Kubernetes
TOAST Kubernetes 서비스는 클라우드에서 Kubernetes를 올바르고 안전하게 구동할 수 있게 Kubernetes 클러스터를 생성하고 관리할 수 있는 서비스입니다. 사용자는 웹 콘솔을 이용해 TOAST에 꼭 맞는 Kubernetes 클러스터를 만들고 관리할 수 있습니다. 안전하고 효율적으로 운영할 수 있게 마스터는 TOAST에서 관리하고, 사용자는 노드와 서비스, Pod(파드) 등을 관리합니다. TOAST Kubernetes creates and manages Kubernetes clusters so as to properly and safely run Kubernetes in the cloud. Users can create and manage Kubernetes clusters that fits right for TOAST on the web console. 

TOAST Kubernetes 서비스의 주요 기능은 다음과 같습니다. TOAST Kubernetes provides the following features: 

* TOAST에 꼭맞는 Kubernetes 클러스터 생성과 관리 Creating and Managing Kubernetes just right for TOAST
    * TOAST의 기반 서비스와 연동 Integrate with TOAST infrastructure services
    * 로드 밸런서를 이용한 서비스 공개 Open services on load balancer 
    * 블록 스토리지와 연동한 퍼시스턴트 볼륨(Persistent Volume, PV) 지원 Support persistent volume (PV) by integrating with block storage

* 고가용성을 보장하는 마스터 관리 Managing Master to Ensure High Availability 

* 웹 콘솔을 이용한 쉬운 조작 Easy Operations on Web Console 
    * 클러스터 생성, 삭제, 조회 Create, delete, and query clusters
    * 노드 그룹 생성, 삭제, 조회 Create, delete, and query node groups
    * kubectl 설정 지원 Support kubectl configuration 
