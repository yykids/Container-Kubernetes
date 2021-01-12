## Container > Kubernetes > User Guide 

## Cluster
Cluster refers to a group of instances that comprise user's Kubernetes. 

### Creating Clusters
To enable Kubernetes, a cluster must be created. Go to **Container > Kubernetes** and click **Create Clusters** and a page of creating clusters opens. Following items are required to create a cluster: 

| Item | Description |
| --- | --- |
| Cluster Name | Kubernetes cluster names can only contain up to 20 lower-case alphabet letters, numbers, and "-". They must begin with a lower-case alphabet letter and end with a lower-case alphabet letter or a number|
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
| Node Group Name | The added node group names can only contain up to 20 lower-case alphabet letters, numbers, and "-". They must begin with a lower-case alphabet letter and end with a lower-case alphabet letter or a number |
| Instance Type | Specificiations of an instance for additional node group |
| Node Count | Number of instances for additional node group |
| Keypair | Keypair to access additional node group |
| Block Storage Type | Type of block storage of instance for additional node group |
| Block Storage Size | Size of block storage of instance for additional node group |

Enter information as required and click **Create Node Groups**, and a node group begins to be created. You may check status from the list of node groups. It takes about 5 minutes to create; more time may be required depending on the node group setting.  

### Deleting Node Groups 
Select a node group to delete from the list of node groups, and click **Delete Node Groups** and it is deleted. It takes about 5 minutes to delete a node group; more time may be required depending on the node group status. 


### Autoscaler

The autoscaler feature automatically adjusts the number of nodes in a node group if it runs out of available resources to schedule pods or if its node usage rate drops below a certain threshold. The autoscaler feature can be individually added to node groups which then work independently from each other. This function is based on Kubernetes Project official feature, cluster-autoscaler. For more information, please visit [here] (https://github.com/kubernetes/autoscaler/tree/master/cluster-autoscaler).

> [Note]
> The version of the cluster-autoscaler applied to the Kubernetes service is 1.19.0.

#### Glossary

Terms used in relation to the autoscaler and their meanings are as follows:

| Term       | Meaning                        |
| ---------- | ------------------------------ |
| Scale Up   | To increase a number of nodes. |
| Scale Down | To decrease a number of nodes. |

> [Caution]
> If worker nodes are working in an environment with no Internet connection, autoscaler container images must be manually added to the worker nodes. This task is applied to the following targets:
> 
> * Pangyo region: Node groups created before November 24, 2020
> * Pyeongchon region: Node groups created before November 19, 2020
> 
> Autoscaler container images are in the following directory:
> * `k8s.gcr.io/autoscaling/cluster-autoscaler:v1.19.0`
> 

#### Autoscaler Settings

Autoscaler can be added per node group and it works independently from each other. Autoscaler can be set up in various ways, as listed below:

* Set up on the default node groups upon creating a cluster.
* Set up on additional node groups upon adding the node groups.
* Set up on the existing node groups.

Activating the autoscaler enables the following options:

| Setting                  | Meaning                                                      | Effective Range | Default | Unit   |
| ------------------------ | ------------------------------------------------------------ | --------------- | ------- | ------ |
| Min. Node Qty            | The minimum number of nodes that can be scaled down          | 1-10             | 1       | unit   |
| Max. Node Qty            | The maximum number of nodes that can be scaled up            | 1 -10            | 10       | unit   |
| Scale Down               | Enable/disable node scale-down                               | Enable/disable  | Enable  | -      |
| Resource Usage Threshold | The default for resource usage threshold, which is the reference point for a scale down | 1-100           | 50      | %      |
| Threshold Duration       | The resource usage duration at or below the threshold for the nodes to be scaled down | 1-1,440         | 10      | minute |
| Post Scale-up Delay      | The delay it takes to start to monitor for scale-down targets after scaling up | 1-1,440         | 10      | minute |

> [Caution]
> Nodes cannot be manually added to or deleted from node groups on which autoscaler is enabled.

#### Scale-up/down Conditions

Scales up if all of the following conditions are met:

* There are no available nodes to schedule pods.
* The current number of nodes is below the maximum limit.

Scales down if all of the following conditions are met:

* Nodes use resources below the threshold for the set critical area duration.
* The current number of nodes exceeds the minimum limit.

If some nodes contain at least one pod that meets the following conditions, then they will be excluded from the list of nodes to be scaled down:

* Pods restricted by "PodDisruptionBudget"
* Pods in the "kube-system" namespace
* Pods that were not started by control objects such as "deployment" or "replicaset"
* Pods that cannot be moved to other nodes because of the restrictions such as "node selector"

For more information on the conditions for scale-up/down, visit [Cluster Autoscaler FAQ] (https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md).

#### Operation Example

Let's check how the autoscaler work through the following example:

##### 1. Enabling Autoscaler

Enables autoscaling on the default node group of the cluster you want. For this example, the number of nodes for the default group has been set to 1 and autoscaler settings are configured as follows:

| Setting                  | Setting Value |
| ------------------------ | ------------- |
| Min. Node Qty            | 1             |
| Max. Node Qty            | 5             |
| Scale Down               | Enable        |
| Resource Usage Threshold | 50            |
| Threshold Duration       | 3             |
| Post Scale-up Delay      | 5             |

##### 2. Distributing Pods
   Distribute pods with the following manifest:

> [Caution]
> Just like this manifest, all manifests must have a container resource request defined on them.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 15
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
        resources:
          requests:
            cpu: "100m"
```

Because the total amount of CPU resources for the requested pods is bigger than the resources that a single node can handle, some of the pods are left behind in the "pending" status, as shown below. In this case, the nodes will scale up.

```
# kubectl get pods
NAME                               READY   STATUS    RESTARTS   AGE
nginx-deployment-756fd4cdf-5gftm   1/1     Running   0          34s
nginx-deployment-756fd4cdf-64gtv   0/1     Pending   0          34s
nginx-deployment-756fd4cdf-7bsst   0/1     Pending   0          34s
nginx-deployment-756fd4cdf-8892p   1/1     Running   0          34s
nginx-deployment-756fd4cdf-8k4cc   1/1     Running   0          34s
nginx-deployment-756fd4cdf-cprp7   0/1     Pending   0          34s
nginx-deployment-756fd4cdf-cvs97   1/1     Running   0          34s
nginx-deployment-756fd4cdf-h7ftk   1/1     Running   0          34s
nginx-deployment-756fd4cdf-hv2fz   0/1     Pending   0          34s
nginx-deployment-756fd4cdf-j789l   0/1     Pending   0          34s
nginx-deployment-756fd4cdf-jrkfj   0/1     Pending   0          34s
nginx-deployment-756fd4cdf-m887q   0/1     Pending   0          34s
nginx-deployment-756fd4cdf-pvnfc   0/1     Pending   0          34s
nginx-deployment-756fd4cdf-wrj8b   1/1     Running   0          34s
nginx-deployment-756fd4cdf-x7ns5   0/1     Pending   0          34s
```

##### 3. Checking Node Scale-up
   The following is the node list before scale-up:

```
# kubectl get nodes
NAME                                            STATUS   ROLES    AGE   VERSION
autoscaler-test-default-w-ohw5ab5wpzug-node-0   Ready    <none>   45m   v1.17.6
```

After 5-10 minutes, the nodes will be scaled up as shown below:

```
# kubectl get nodes
NAME                                            STATUS   ROLES    AGE   VERSION
autoscaler-test-default-w-ohw5ab5wpzug-node-0   Ready    <none>   48m   v1.17.6
autoscaler-test-default-w-ohw5ab5wpzug-node-1   Ready    <none>   77s   v1.17.6
autoscaler-test-default-w-ohw5ab5wpzug-node-2   Ready    <none>   78s   v1.17.6
```

The hitherto "pending" pods are now normally scheduled after the scale-up.

```
# kubectl --kubeconfig ~/Downloads/autoscaler-test_kubeconfig.yaml get pods -o wide
NAME                               READY   STATUS    RESTARTS   AGE     IP            NODE                                            NOMINATED NODE   READINESS GATES
nginx-deployment-756fd4cdf-5gftm   1/1     Running   0          4m29s   10.100.8.13   autoscaler-test-default-w-ohw5ab5wpzug-node-0   <none>           <none>
nginx-deployment-756fd4cdf-64gtv   1/1     Running   0          4m29s   10.100.22.5   autoscaler-test-default-w-ohw5ab5wpzug-node-1   <none>           <none>
nginx-deployment-756fd4cdf-7bsst   1/1     Running   0          4m29s   10.100.22.4   autoscaler-test-default-w-ohw5ab5wpzug-node-1   <none>           <none>
nginx-deployment-756fd4cdf-8892p   1/1     Running   0          4m29s   10.100.8.10   autoscaler-test-default-w-ohw5ab5wpzug-node-0   <none>           <none>
nginx-deployment-756fd4cdf-8k4cc   1/1     Running   0          4m29s   10.100.8.12   autoscaler-test-default-w-ohw5ab5wpzug-node-0   <none>           <none>
nginx-deployment-756fd4cdf-cprp7   1/1     Running   0          4m29s   10.100.12.7   autoscaler-test-default-w-ohw5ab5wpzug-node-2   <none>           <none>
nginx-deployment-756fd4cdf-cvs97   1/1     Running   0          4m29s   10.100.8.14   autoscaler-test-default-w-ohw5ab5wpzug-node-0   <none>           <none>
nginx-deployment-756fd4cdf-h7ftk   1/1     Running   0          4m29s   10.100.8.11   autoscaler-test-default-w-ohw5ab5wpzug-node-0   <none>           <none>
nginx-deployment-756fd4cdf-hv2fz   1/1     Running   0          4m29s   10.100.12.5   autoscaler-test-default-w-ohw5ab5wpzug-node-2   <none>           <none>
nginx-deployment-756fd4cdf-j789l   1/1     Running   0          4m29s   10.100.22.6   autoscaler-test-default-w-ohw5ab5wpzug-node-1   <none>           <none>
nginx-deployment-756fd4cdf-jrkfj   1/1     Running   0          4m29s   10.100.12.4   autoscaler-test-default-w-ohw5ab5wpzug-node-2   <none>           <none>
nginx-deployment-756fd4cdf-m887q   1/1     Running   0          4m29s   10.100.22.3   autoscaler-test-default-w-ohw5ab5wpzug-node-1   <none>           <none>
nginx-deployment-756fd4cdf-pvnfc   1/1     Running   0          4m29s   10.100.12.6   autoscaler-test-default-w-ohw5ab5wpzug-node-2   <none>           <none>
nginx-deployment-756fd4cdf-wrj8b   1/1     Running   0          4m29s   10.100.8.15   autoscaler-test-default-w-ohw5ab5wpzug-node-0   <none>           <none>
nginx-deployment-756fd4cdf-x7ns5   1/1     Running   0          4m29s   10.100.12.3   autoscaler-test-default-w-ohw5ab5wpzug-node-2   <none>           <none>
```

You can check scale-up events with the following command:

```
# kubectl get events --field-selector reason="TriggeredScaleUp"
LAST SEEN   TYPE     REASON             OBJECT                                 MESSAGE
4m          Normal   TriggeredScaleUp   pod/nginx-deployment-756fd4cdf-64gtv   pod triggered scale-up: [{default-worker-bf5999ab 1->3 (max: 5)}]
4m          Normal   TriggeredScaleUp   pod/nginx-deployment-756fd4cdf-7bsst   pod triggered scale-up: [{default-worker-bf5999ab 1->3 (max: 5)}]
...
```


##### 4. Checking Node Scale-down after Deleting Pods
   Delete distributed deployments to delete the distributed pods.

```
# kubectl get pods
NAME                               READY   STATUS        RESTARTS   AGE
nginx-deployment-756fd4cdf-5gftm   0/1     Terminating   0          20m
nginx-deployment-756fd4cdf-64gtv   0/1     Terminating   0          20m
nginx-deployment-756fd4cdf-7bsst   0/1     Terminating   0          20m
nginx-deployment-756fd4cdf-8892p   0/1     Terminating   0          20m
nginx-deployment-756fd4cdf-8k4cc   0/1     Terminating   0          20m
nginx-deployment-756fd4cdf-cprp7   0/1     Terminating   0          20m
nginx-deployment-756fd4cdf-h7ftk   0/1     Terminating   0          20m
nginx-deployment-756fd4cdf-hv2fz   0/1     Terminating   0          20m
nginx-deployment-756fd4cdf-j789l   0/1     Terminating   0          20m
nginx-deployment-756fd4cdf-jrkfj   0/1     Terminating   0          20m
nginx-deployment-756fd4cdf-m887q   0/1     Terminating   0          20m
nginx-deployment-756fd4cdf-pvnfc   0/1     Terminating   0          20m
nginx-deployment-756fd4cdf-wrj8b   0/1     Terminating   0          20m
nginx-deployment-756fd4cdf-x7ns5   0/1     Terminating   0          20m
#
# kubectl get pods
No resources found in default namespace.
#
```

After a while, you can see nodes are scaled down to 1. The time it takes to scale down may vary depending on your settings.

```
# kubectl get nodes
NAME                                            STATUS   ROLES    AGE   VERSION
autoscaler-test-default-w-ohw5ab5wpzug-node-0   Ready    <none>   71m   v1.17.6
```

You can check scale-down events with the following command:

```
# kubectl get events --field-selector reason="ScaleDown"
LAST SEEN   TYPE     REASON      OBJECT                                               MESSAGE
13m         Normal   ScaleDown   node/autoscaler-test-default-w-ohw5ab5wpzug-node-1   node removed by cluster autoscaler
13m         Normal   ScaleDown   node/autoscaler-test-default-w-ohw5ab5wpzug-node-2   node removed by cluster autoscaler
```

You can check the status of each node group's autoscaler through "configmap/cluster-autoscaler-status." Configmaps are created ind different namespaces for different node groups. The following is the naming convention for each node group namespace created by the autoscaler:

* Format: nhn-ng-{node group name}
* Enter a node group name in {node group name}.
* The default node group name is "default-worker."

For example, the status of the default node group's autoscaler can be viewed as below. To understand what you can learn from this information, visit [here] (https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md).

```
# kubectl get configmap/cluster-autoscaler-status -n nhn-ng-default-worker -o yaml
apiVersion: v1
data:
  status: |+
    Cluster-autoscaler status at 2020-11-03 12:39:12.190150095 +0000 UTC:
    Cluster-wide:
      Health:      Healthy (ready=1 unready=0 notStarted=0 longNotStarted=0 registered=1 longUnregistered=0)
                   LastProbeTime:      2020-11-03 12:39:12.185954244 +0000 UTC m=+43.664545435
                   LastTransitionTime: 2020-11-03 12:38:41.705407217 +0000 UTC m=+13.183998415
      ScaleUp:     NoActivity (ready=1 registered=1)
                   LastProbeTime:      2020-11-03 12:39:12.185954244 +0000 UTC m=+43.664545435
                   LastTransitionTime: 2020-11-03 12:38:41.705407217 +0000 UTC m=+13.183998415
      ScaleDown:   NoCandidates (candidates=0)
                   LastProbeTime:      2020-11-03 12:39:12.185954244 +0000 UTC m=+43.664545435
                   LastTransitionTime: 2020-11-03 12:38:41.705407217 +0000 UTC m=+13.183998415
    NodeGroups:
      Name:        default-worker-f9a9ee5e
      Health:      Healthy (ready=1 unready=0 notStarted=0 longNotStarted=0 registered=1 longUnregistered=0 cloudProviderTarget=1 (minSize=1, maxSize=5))
                   LastProbeTime:      2020-11-03 12:39:12.185954244 +0000 UTC m=+43.664545435
                   LastTransitionTime: 2020-11-03 12:38:41.705407217 +0000 UTC m=+13.183998415
      ScaleUp:     NoActivity (ready=1 cloudProviderTarget=1)
                   LastProbeTime:      2020-11-03 12:39:12.185954244 +0000 UTC m=+43.664545435
                   LastTransitionTime: 2020-11-03 12:38:41.705407217 +0000 UTC m=+13.183998415
      ScaleDown:   NoCandidates (candidates=0)
                   LastProbeTime:      2020-11-03 12:39:12.185954244 +0000 UTC m=+43.664545435
                   LastTransitionTime: 2020-11-03 12:38:41.705407217 +0000 UTC m=+13.183998415
kind: ConfigMap
metadata:
  annotations:
    cluster-autoscaler.kubernetes.io/last-updated: 2020-11-03 12:39:12.190150095 +0000
      UTC
  creationTimestamp: "2020-11-03T12:38:28Z"
  name: cluster-autoscaler-status
  namespace: nhn-ng-default-worker
  resourceVersion: "1610"
  selfLink: /api/v1/namespaces/nhn-ng-default-worker/configmaps/cluster-autoscaler-status
  uid: e72bd1a2-a56f-41b4-92ee-d11600386558
```

> [Note]
> As for the status information, the "Cluster-wide" section has the same information as "NodeGroups."

#### Example of an action working with HPA (HorizontalPodAutoscale)
Horizontal Pod Autoscaler (HPA) observes resource usage, such as CPU usage, to auto-scale the number of pods of ReplicationController, Deployment, ReplicaSet, and StatefulSet. As the number of pods is adjusted, there could be too many or too few resources available in the node. At this moment, utilize the Autoscaler function to increase or decrease the number of nodes. In this example, we will see how HPA and Autoscaler can work together to deal with this issue. For more information on HPA, see [Horizontal Pod Autoscaler](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/). 

##### 1. Enabling Autoscaler
Enable Autoscaler as shown in the above example.

##### 2. Configuring HPA
Deploy a container that creates CPU load for a certain amount of time after receiving a web request. The, expose the service. The following is taken from the "php-apache.yaml" file.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: php-apache
spec:
  selector:
    matchLabels:
      run: php-apache
  replicas: 1
  template:
    metadata:
      labels:
        run: php-apache
    spec:
      containers:
      - name: php-apache
        image: k8s.gcr.io/hpa-example
        ports:
        - containerPort: 80
        resources:
          limits:
            cpu: 500m
          requests:
            cpu: 200m
---
apiVersion: v1
kind: Service
metadata:
  name: php-apache
  labels:
    run: php-apache
spec:
  ports:
  - port: 80
  selector:
    run: php-apache
```

```
# kubectl apply -f php-apache.yaml
deployment.apps/php-apache created
service/php-apache created
```

Now, set up HPA. For the php-apache deployment object just created in the previous step, set as follows: min pod count = 1, max pod count = 30, target CPU load = 50%.

```
# kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=30
horizontalpodautoscaler.autoscaling/php-apache autoscaled
```

If you look up the state of HPA, you can see the settings and the current state. Since no web request that causes CPU load has been sent yet, CPU load is still at 0%.

```
# kubectl get hpa
NAME         REFERENCE               TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
php-apache   Deployment/php-apache   0%/50%    1         30        1          80s
```

##### 3. Authorizing Load
Now run the pod that triggers load in the new terminal. This pod sends web requests without stopping. You can stop this requesting action with 'Ctrl+C.'

```
# kubectl run -i --tty load-generator --rm --image=busybox --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://php-apache; done"
If you don't see a command prompt, try pressing enter.
OK!OK!OK!OK!OK!OK!OK!
```

Using the 'kubectl top nodes' command, you can see the current resource usage of the node. You can observe the increase in CPU load as time goes after running the pod that causes load.

```
# kubectl top nodes
NAME                                            CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%
autoscaler-test-default-w-ohw5ab5wpzug-node-0   66m          6%     1010Mi          58%
(A moment later)
# kubectl top nodes
NAME                                            CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%
autoscaler-test-default-w-ohw5ab5wpzug-node-0   574m         57%    1013Mi          58%
```

If you look up the status of HPA, you can see the increase in CPU load and the resultant increase in REPLICAS (number of pods).

```
# kubectl get hpa
NAME         REFERENCE               TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
php-apache   Deployment/php-apache   250%/50%   1         30        5          2m44s
```

##### 4. Checking the Operation of Autoscaler
If you look up pods, due to the increase in the number of pods, you can see some pods are running as they are scheduled to 'node-0,' but some are still pending

```
# kubectl get pods -o wide
NAME                          READY   STATUS    RESTARTS   AGE     IP            NODE                                            NOMINATED NODE   READINESS GATES
load-generator                1/1     Running   0          2m      10.100.8.39   autoscaler-test-default-w-ohw5ab5wpzug-node-0   <none>           <none>
php-apache-79544c9bd9-6f7nm   0/1     Pending   0          65s     <none>        <none>                                          <none>           <none>
php-apache-79544c9bd9-82xkn   1/1     Running   0          80s     10.100.8.41   autoscaler-test-default-w-ohw5ab5wpzug-node-0   <none>           <none>
php-apache-79544c9bd9-cjj9q   0/1     Pending   0          80s     <none>        <none>                                          <none>           <none>
php-apache-79544c9bd9-k6nnt   1/1     Running   0          4m27s   10.100.8.38   autoscaler-test-default-w-ohw5ab5wpzug-node-0   <none>           <none>
php-apache-79544c9bd9-mplnn   0/1     Pending   0          19s     <none>        <none>                                          <none>           <none>
php-apache-79544c9bd9-t2knw   1/1     Running   0          80s     10.100.8.40   autoscaler-test-default-w-ohw5ab5wpzug-node-0   <none>           <none>
```

This situation of not being able to schedule pods is the node extension condition for Autoscaler. If you look up the state information provided by Cluster Autoscaler pod, you can see that ScaleUp is in InProgress state.

```
# kubectl get cm/cluster-autoscaler-status -n nhn-ng-default-worker -o yaml
apiVersion: v1
data:
  status: |+
    Cluster-autoscaler status at 2020-11-24 13:00:40.210137143 +0000 UTC:
    Cluster-wide:
      Health:      Healthy (ready=1 unready=0 notStarted=0 longNotStarted=0 registered=1 longUnregistered=0)
                   LastProbeTime:      2020-11-24 13:00:39.930763305 +0000 UTC m=+1246178.729396969
                   LastTransitionTime: 2020-11-10 02:51:14.353177175 +0000 UTC m=+13.151810823
      ScaleUp:     InProgress (ready=1 registered=1)
                   LastProbeTime:      2020-11-24 13:00:39.930763305 +0000 UTC m=+1246178.729396969
                   LastTransitionTime: 2020-11-24 12:58:34.83642035 +0000 UTC m=+1246053.635054003
      ScaleDown:   NoCandidates (candidates=0)
                   LastProbeTime:      2020-11-24 13:00:39.930763305 +0000 UTC m=+1246178.729396969
                   LastTransitionTime: 2020-11-20 01:42:32.287146552 +0000 UTC m=+859891.085780205
    NodeGroups:
      Name:        default-worker-bf5999ab
      Health:      Healthy (ready=1 unready=0 notStarted=0 longNotStarted=0 registered=1 longUnregistered=0 cloudProviderTarget=2 (minSize=1, maxSize=3))
                   LastProbeTime:      2020-11-24 13:00:39.930763305 +0000 UTC m=+1246178.729396969
                   LastTransitionTime: 2020-11-10 02:51:14.353177175 +0000 UTC m=+13.151810823
      ScaleUp:     InProgress (ready=1 cloudProviderTarget=2)
                   LastProbeTime:      2020-11-24 13:00:39.930763305 +0000 UTC m=+1246178.729396969
                   LastTransitionTime: 2020-11-24 12:58:34.83642035 +0000 UTC m=+1246053.635054003
      ScaleDown:   NoCandidates (candidates=0)
                   LastProbeTime:      2020-11-24 13:00:39.930763305 +0000 UTC m=+1246178.729396969
                   LastTransitionTime: 2020-11-20 01:42:32.287146552 +0000 UTC m=+859891.085780205
...
```

After a while, you can see another node (node-8) has been added.

```
# kubectl get nodes
NAME                                            STATUS     ROLES    AGE   VERSION
autoscaler-test-default-w-ohw5ab5wpzug-node-0   Ready      <none>   22d   v1.17.6
autoscaler-test-default-w-ohw5ab5wpzug-node-8   Ready      <none>   90s   v1.17.6
```

You can see all pods that were in Pending state are properly scheduled and now in the Running state.

```
# kubectl get pods -o wide
NAME                          READY   STATUS    RESTARTS   AGE     IP            NODE                                            NOMINATED NODE   READINESS GATES
load-generator                1/1     Running   0          5m32s   10.100.8.39   autoscaler-test-default-w-ohw5ab5wpzug-node-0   <none>           <none>
php-apache-79544c9bd9-6f7nm   1/1     Running   0          4m37s   10.100.42.3   autoscaler-test-default-w-ohw5ab5wpzug-node-8   <none>           <none>
php-apache-79544c9bd9-82xkn   1/1     Running   0          4m52s   10.100.8.41   autoscaler-test-default-w-ohw5ab5wpzug-node-0   <none>           <none>
php-apache-79544c9bd9-cjj9q   1/1     Running   0          4m52s   10.100.42.5   autoscaler-test-default-w-ohw5ab5wpzug-node-8   <none>           <none>
php-apache-79544c9bd9-k6nnt   1/1     Running   0          7m59s   10.100.8.38   autoscaler-test-default-w-ohw5ab5wpzug-node-0   <none>           <none>
php-apache-79544c9bd9-mplnn   1/1     Running   0          3m51s   10.100.42.4   autoscaler-test-default-w-ohw5ab5wpzug-node-8   <none>           <none>
php-apache-79544c9bd9-t2knw   1/1     Running   0          4m52s   10.100.8.40   autoscaler-test-default-w-ohw5ab5wpzug-node-0   <none>           <none>
```

If you press `Ctrl+C` to stop the pod (`load-generator`) that was executed for load, load will decrease after a while. The lower the load, the lower the CPU usage occupied by the pod, which in return decrease the number of pods.

```
# kubectl get hpa
NAME         REFERENCE               TARGETS   MINPODS   MAXPODS   REPLICAS   AGE
php-apache   Deployment/php-apache   0%/50%    1         30        1          31m
```

As the number of pods decreases, the resource usage of the node also decreases, which results in the reduction in nodes. You can see the newly added node-8 has been reduced.

```
# kubectl get nodes
NAME                                            STATUS   ROLES    AGE   VERSION
autoscaler-test-default-w-ohw5ab5wpzug-node-0   Ready    <none>   22d   v1.17.6
```

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

#### Change Roles
By default, downloaded files are not allowed to execute. The execution role must be added. 

```
$ chmod +x kubectl
```

#### Change Location or Specify Paths 
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

### CertificateSigningRequest (CSR)

Using Certificate API of Kubernetes, you can request and issue the X.509 certificate for a Kubernetes API client . CSR resource lets you request certificate and decide to accept/reject the request. For more information, see the [Certificate Signing Requests](https://kubernetes.io/docs/reference/access-authn-authz/certificate-signing-requests/).

#### CSR Request and Issue Approval Example
First of all, create a private key. For more information on certificate creation, see the [Certificates] (https://kubernetes.io/docs/concepts/cluster-administration/certificates/) document.

```
# openssl genrsa -out dev-user1.key 2048
Generating RSA private key, 2048 bit long modulus
...........................................................................+++++
..................+++++
e is 65537 (0x010001)
# openssl req -new -key dev-user1.key -subj "/CN=dev-user1" -out dev-user1.csr
```

Create a CSR resource that includes created private key information and request certificate issuance.

```
# BASE64_CSR=$(cat dev-user1.csr | base64 | tr -d '\n')
# cat <<EOF > csr.yaml -
apiVersion: certificates.k8s.io/v1beta1
kind: CertificateSigningRequest
metadata:
  name: dev-user1
spec:
  groups:
  - system:authenticated
  request: ${BASE64_CSR}
  usages:
  - digital signature
  - key encipherment
  - server auth
  - client auth
EOF
# kubectl apply -f csr.yaml
certificatesigningrequest.certificates.k8s.io/dev-user1 created
```

The registered CSR is in `Pending` state. This state indicates waiting for issuance approval or rejection.

```
# kubectl get csr
NAME        AGE   REQUESTOR          CONDITION
dev-user1   6s    system:unsecured   Pending
```

Approves this certificate issuance request.

```
# kubectl certificate approve dev-user1
certificatesigningrequest.certificates.k8s.io/dev-user1 approved
```

If you check the CSR again, you can see that it has been changed to the `Approved,Issued` state.
```
# kubectl get csr
NAME        AGE    REQUESTOR          CONDITION
dev-user1   114s   system:unsecured   Approved,Issued
```

You can look up the certificate as below. The certificate is a value for the Certificate field under Status.

```
# kubectl get csr/dev-user1 -o yaml
apiVersion: certificates.k8s.io/v1beta1
kind: CertificateSigningRequest
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"certificates.k8s.io/v1beta1","kind":"CertificateSigningRequest","metadata":{"annotations":{},"name":"dev-user1"},"spec":{"groups":["system:authenticated"],"request":"LS0tLS... (omitted)","usages":["digital signature","key encipherment","server auth","client auth"]}}
  creationTimestamp: "2020-12-07T06:32:53Z"
  name: dev-user1
  resourceVersion: "3202"
  selfLink: /apis/certificates.k8s.io/v1beta1/certificatesigningrequests/dev-user1
  uid: b22477eb-0abc-4fc4-8a79-f6516751a940
spec:
  groups:
  - system:masters
  - system:authenticated
  request: LS0tLS... (omitted)
  usages:
  - digital signature
  - key encipherment
  - server auth
  - client auth
  username: system:unsecured
status:
  certificate: LS0tLS... (omitted)
  conditions:
  - lastUpdateTime: "2020-12-07T06:34:43Z"
    message: This CSR was approved by kubectl certificate approve.
    reason: KubectlApprove
    type: Approved
```

> [Caution]
> This function is provided only when the time of cluster creation falls within the following period:
> 
> * Pangyo region: Cluster created as of December 29, 2020
> * Pyeongchon region: Cluster created as of December 24, 2020

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
Ingress Controller routes HTTP and HTTPS requests from cluster externals to internal services, in reference of the rules that are defined at ingress object so as to provide SSL/TSL closure and virtual hosting. For more details on Ingress Controller and Ingress, see [Ingress Controller](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/), [Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/).


### Installing NGINX Ingress Controller 
NGINX Ingress Controller is one of the most frequently used ingress controllers. For more details, see [NGINX Ingress Controller](https://kubernetes.github.io/ingress-nginx/) and [NGINX Ingress Controller for Kubernetes](https://docs.nginx.com/nginx-ingress-controller/overview/).

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

Request for `/coffee` as endpoint is sent to the `coffee-svc` service so as the `coffee` pod can respond. From the **Server Name**, you can see that `coffee` pods take turns to respond in the round-robin technique. 

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

Once the type of service object is changed into `LoadBalancer`, TOAST Load Balancer is created out of the cluster, which is associated with load balancer and service object. By querying service object associated with the load balanacer, IP of the load balancer shows at **EXTERNAL-IP**. See [LoadBalancer Service](/Container/Kubernetes/en/user-guide/#loadbalancer) for the description of service objects of the `LoadBalancer` type.  

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

With PV and PVC, user can define the attributes of a volume of choice, while the system seperates the use of resources from management by assigning volume resources for each user requirement.  

### Life Cycle of PV/PVC 
PV and PVC support the four-phase life cycle. 

* Provisioning
User can secure volume on his own to provision PV (static provisioning), or apply [Storage Class](https://kubernetes.io/docs/concepts/storage/storage-classes/) to dynamically provision PV (dynamic provisioning). 

* Binding
Bind PV to PVC 1:1. With dynamic provisioning, binding is also automatically executed along with PV provisioning. 

* Using
Mount PV to a pod to make it enabled.  

* Reclaiming
Volume is reclaimed after it is used up, in three methods: Delete, Retain, or Recycle. 

| Method | Description |
| --- | --- |
| Delete | PV is deleted along with its attached volumes. |
| Retain | PV is deleted but its attached volumes are not: volumes can be deleted or reused by user. |
| Recycle | PV is deleted and its attached volumes are made to be reused without being deleted. This method has been deprecated. |


### Static Provisioning 

To enable static provisioning, user must have the block storage prepared. Go to **Storage > Block Storage** on TOAST web console, and click **Create Block Storages** to create block storages to be attached to PV. See Block Stroage Guide for [Creating Block Storages](/Storage/Block%20Storage/en/console-guide/#_2).  

To provision PV, ID of a block storage is required. Select a block storage from the list of block storages on **Storage > Block Storage**. Check ID on the **Information** tab at the bottom of the block storage name. 

> [Caution]
> Block storage must be on the same availability area with the node group instance to run pods; otherwise, attachement is unavailable. 

Create manifest for storage class. To enable TOAST Block Storage, **provisioner** must be configured with `kubernetes.io/cinder`. 

```yaml
# storage_class.yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: sc-default
provisioner: kubernetes.io/cinder
```

Create storage class and confirm.  

```
$ kubectl apply -f storage_class.yaml
storageclass.storage.k8s.io/sc-default created

$ kubectl get sc
NAME         PROVISIONER            AGE
sc-default   kubernetes.io/cinder   8s
```

Write PV manifest to be attached to block storage. Enter storage class name for **spec.storageClassName**. To enable TOAST Block Storage, **spec.accessModes** must be configured with 'ReadWriteOnce'. Choose 'Delete' or 'Retain' for **spec.presistentVolumeReclaimPolicy**.

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

Create PV and confirm. 

```
$ kubectl apply -f pv-static.yaml
persistentvolume/pv-static-001 created

$ kubectl get pv -o wide
NAME            CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS   REASON   AGE   VOLUMEMODE
pv-static-001   10Gi       RWO            Delete           Available           sc-default              7s    Filesystem
```

Write PVC manifest to use created PV. PV name must be specified for **spec.volumeName**.  Set other items same as pv manifest. 

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

Create PVC and confirm. 

```
$ kubectl apply -f pvc-static.yaml
persistentvolumeclaim/pvc-static created

$ kubectl get pvc -o wide
NAME         STATUS   VOLUME          CAPACITY   ACCESS MODES   STORAGECLASS   AGE   VOLUMEMODE
pvc-static   Bound    pv-static-001   10Gi       RWO            sc-default     7s    Filesystem
```

After PVC is created, query PV status, and you can find PVC name specified for **CLAIM** and **STATUS** changed into 'Bound'. 

```
$ kubectl get pv -o wide
NAME            CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS   CLAIM                STORAGECLASS   REASON   AGE   VOLUMEMODE
pv-static-001   10Gi       RWO            Delete           Bound    default/pvc-static   sc-default              79s   Filesystem
```


### Dynamic Provisioning 

With Dynamic Provisioning, block storage is automatically created in reference of attributes defined at storage class. You may speify the type of TOAST Block Storages for **parameters.type** of the storage class manifest. If not specified, it is configured with HDD type.  

| Type | Configured Value |
| --- | --- |
| HDD | General HDD |
| SSD | General SSD |

Block storage must be on the same availability area of the node group to be allowed for attachment. You may specify the availability area to create a block storage for **parameters.availability** of the storage class manifest. Check the availability area of a node group to be attached from the list of node groups.  

> [Caution]
> Without availability area specified for the storage class manifest, a block storage is created at a random availability area. It is a must to specify availability area, becuase, if a block storage is located at a different availability area from its node group, it may not be properly attached.  

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

There is no need to create PV for dynamic provisioning; therefore, pvc manifest does not require the setting of **spec.volumeName**. 

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

With PVC provisioning, PV is automatically created. At the same time, block storage attached to the PV is also automatically created, and you can check it from the list of block storages on the **Storage > Block Storage** page of TOAST web console. 

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

> [Caution]
> A block storage created by dynamic provisioning cannot be deleted from the web console. It is not automatically deleted along with a cluster being deleted. Therefore, before a cluster is deleted, PVC must be deleted first; otherwise, you may be charged for pvc usage. The reclaimPolicy of PVC created by dynamic provisioning is configured with 'Delete' by default, by which deleting PVC only causes the deletion of PV and block storage as well.  


### Mounting PVC to Pods 

To mount PVC to a pod, mount information must be defined at the pod manifest. Enter pvc name to use for `spec.volumes.persistenVolumeClame.claimName`; enter paths to mount for `spec.containers.volumeMounts.mountPath`.

In the example as blow, pvc created with dynamic provisioning is mounted to `/usr/share/nginx/html` of the pod. 

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

Create a pod and see if block storage is mounted. 

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

You can also check block storage attachement from **Storage > Block Storage** on TOAST web console. 
