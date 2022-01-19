Google Kubernetes Engine is Kubernetes as a managed service.

**Container** -
- The topmost layer's contents are lost when the container is no longer running.
- An application running in a container can only modify the topmost layer.

**Container Registry** is a single place for your team to manage Docker images, 
perform vulnerability analysis, and decide who can access what with fine-grained access control
**Cloud Build** is a managed service on Google Cloud Platform infrastructure that allows you to continuously build,
                    test and deploy containers.
    - gcloud builds submit --tag gcr.io/${GOOGLE_CLOUD_PROJECT}/quickstart-image .
- gcloud builds submit --config cloudbuild.yaml .

![Cloud Build](/Users/matolaga/Mathan/Git/GCP/src/main/resources/Cloud Build.png)
![Compute Options](/Users/matolaga/Mathan/Git/GCP/src/main/resources/Compute Options.png)

**Kube Components**
![Kube Components](/Users/matolaga/Mathan/Git/GCP/src/main/resources/Kube Components.png)
![Pod](/Users/matolaga/Mathan/Git/GCP/src/main/resources/Pod.png)
- namespaces provides a mechanism for isolating groups of resources within a single cluster.
- use namespaces at command level not inside yaml files for flexibility
- Deployment object would create a ReplicaSet object to manage the Pods. 
- Services provide load-balanced access to specified Pods. There are three primary types of Services:

    - ClusterIP: Exposes the service on an IP address that is only accessible from within this cluster. This is the default type.
    
    -  NodePort: Exposes the service on the IP address of each node in the cluster, at a specific port number.
    
    - LoadBalancer: Exposes the service externally, using a load balancing service provided by a cloud provider.
- In Google Kubernetes Engine, LoadBalancers give you access to a regional Network Load Balancing configuration by default.
  To get access to a global HTTP(S) Load Balancing configuration, you can use an Ingress object.

- A node pool is a group of nodes within a cluster that all have the same configuration. Node pools use a NodeConfig specification

**Kubernetes controller objects**:

- ReplicaSets  controller : ensures that a population of Pods, all identical to one another, are running at the same time

Deployments - let you create, update, roll back, and scale Pods, using ReplicaSets as needed to do so

Replication Controllers - perform a similar role to the combination of ReplicaSets and Deployments, but their use is no longer recommended.

StatefulSets - If you need to deploy applications that maintain local state, StatefulSet is a better option.
A StatefulSet is similar to a Deployment in that the Pods use the same container spec.

DaemonSets - DaemonSet ensures that a specific Pod is always running on all or some subset of the nodes. If new nodes are added,
DaemonSet will automatically set up Pods in those nodes with the required specification.

Jobs - creates one or more Pods required to run a task. When the task is completed, Job will then terminate all those Pods. Cronjob


**Kubectl** - Kubectl is a utility used by administrators to control Kubernetes clusters. 
You use it to communicate with the kube apiserver on your control-plane
![Kubectl](/Users/matolaga/Mathan/Git/GCP/src/main/resources/Kubectl.png)

- Kubernetes has three Object Types you should know about:

- Pods - runs one or more closely related containers
- Services - sets up networking in a Kubernetes cluster
- Deployment - Maintains a set of identical pods, ensuring that they have the correct config and that the right number of them exist.
- Pods:

    1. Runs a single set of containers
    2. Good for one-off dev purposes
    3. Rarely used directly in production
- Deployment:

    1. Runs a set of identical pods
    2. Monitors the state of each pod, updating as necessary
    3. Good for dev
    4. Good for production

- get, describe, logs, exec - action
- kubectl command(action) type(kube objects) name  flags
- kubectl get pods
- pod phases - pending, running, Succeeded, Failed, Unknown, Crashloopbackoff.
- container state- waitinhg, running, terminated.
- kubectl exec -it pod_name -- /bin/bash - pass terminals stdin to the container. Display the stdout in ur terminal. 
- gcloud container clusters create $my_cluster --num-nodes 3 --zone $my_zone --enable-ip-alias - to create kube cluster
- gcloud container clusters resize $my_cluster --zone $my_zone --num-nodes=4 - modify the nodes
- When issuing cluster commands, you typically must specify both the cluster name and the cluster location (region or zone).
- gcloud container clusters get-credentials $my_cluster --zone $my_zone - kubeconfig - cluster and current context info is stored in the /.kube/config
- kubectl config view to print the config contents
- kubectl config current-context - current context
- kubectl config get-contexts - to get all
- kubectl config use-context gke_${GOOGLE_CLOUD_PROJECT}_us-central1-a_standard-cluster-1 - to change context
- kubectl top nodes - to view resource across nodes.
- source <(kubectl completion bash) - to enable bash autocompletion - after this enter kubectl and press tab twice to see the 
list of possible commands
- Kubernetes introduces the abstraction of a Pod to group one or more related containers 
  as a single entity to be scheduled and deployed as a unit on the same node  
- kubectl create deployment --image nginx nginx-1 - deploy nginx as a Pod named nginx-1:
- To expose a Pod to clients outside the cluster requires a service
- kubectl expose pod $my_nginx_pod --port 80 --type LoadBalancer - creates a LoadBalancer service,
  which allows the nginx Pod to accessed from internet addresses outside of the cluster.
- kubectl get services - services in the cluster
-  preferred way of deploying Pods and other resources to Kubernetes is through configuration files,
   which are sometimes called manifest files.
- kubectl exec -it new-nginx /bin/bash - interactive bash shell in the  container:  
    -  If the Pod had several containers, you could specify one by name with the -c option.
- kubectl port-forward new-nginx 10081:80 port forwarding from Cloud Shell to the nginx Pod (from port 10081 of the Cloud Shell VM
  to port 80 of the nginx container)    
- kubernetes verrsio upgrade - If the version you are upgrading to is more than 1 minor version away
  from the current version. You may have to do this step in stages.  
    - I will upgrade from 1.14.10 to 1.15.11 first, then I will upgrade from 1.15.11 to my most recent version (1.16.9).
    - You must now upgrade the nodes of your cluster to the same version as the control plane.
- The status ImagePullBackOff means that a container could not start because Kubernetes could not pull a container image
  (for reasons such as invalid image name, or pulling from a private registry without imagePullSecret).
  The BackOff part indicates that Kubernetes will keep trying to pull the image, with an increasing back-off delay.   
    
**deployment** - Deployments describe a desired state of Pods.
- A deployment is responsible for keeping a set of pods running
- yaml file submitted -kube control pane - deployment controller - replicat set is created.
- A ReplicaSet is a controller that ensures that a certain number of Pod replicas are running at any given time. 
- ways to create depoyment - yaml(declarative), using kubectl run cmnd(imperative), using console
- creation of a Kubernetes object called horizontal pod Autoscaler. This object performs the actual scaling 
  to match the target CPU utilization. Keep in mind that we're not scaling the cluster as a whole, just a particular
  deployment within that cluster
- stateless apps are suited for deployment.

**Updating Deployment**
- kubectl apply -f new file or kubectl set command to update, kubectl edit command, gcp console
- deployment updated it launches a new ReplicaSet and creates a new set of Pods in a controlled fashion
  new Pods are launched in a new ReplicaSet. Next, all Pods are deleted from the old ReplicaSet
  a rolling update strategy also known as a rampt strategy.updates her slowly release, which ensures the availability of the application
  but takes time.
- The Horizontal Pod Autoscaler automatically scales the number of Pods in a replication controller,
  deployment, replica set or stateful set based on observed CPU utilizatio  
- **Rolling update Strategy** 
    - Max unavailable and Max search fields control how the pods are updated.
- **Blue-Green Deployments** 
  - A blue green deployment strategy is useful when you want to deploy a new version of an application,
    and also ensure that application services remain available while the deployment is updated
  - kube services are switched to the newer versions after its deployed
- **Canary Deployments**    
   - The Canary method is another update strategy based on the blue green method,
     but traffic is gradually shifted to the new version 
   - adv - minimize the access resource usage during the updates  
- kubectl scale --replicas=5 deployment nginx-deployment
- deployment's rollout is triggered if and only if the deployment's Pod template is changed. 
- To roll back an object's rollout, you can use the kubectl rollout undo
- Services can be configured as ClusterIP, NodePort or LoadBalancer types
- sessionAffinity field to ClientIP in the specification of the service if you need a client's first request to determine
  which Pod will be used for all subsequent connections.
  
**Job**
- A Job is a Kubernetes object, like a deployment. A Job creates one or more Pods to run a specific task reliably
- task is completed, it will terminate the Pod 
- **Parallel Jobs** - set using parallelism
- CronJobs are meant for performing regular scheduled actions such as backups, report generation, and so on.
- kubectl get jobs

**Pod N/W**
- Addresss are assigned from VPC

**Scaling**
- The cluster autoscaler is a Kubernetes tool that increases or decreases the size of a Kubernetes cluster (by adding or removing nodes),
  based on the presence of pending pods and node utilization metrics.
- kubectl autoscale deployment web --max 4 --min 1 --cpu-percent 1  
- kubectl get hpa  
- kubectl scale deployment loadgen --replicas 0
  
- Taints apply to nodes, while affinity rules apply to Pods.

- Helm - open source package manager to org kube obje in packages.
![Helm_Arch](/Users/matolaga/Mathan/Git/GCP/src/main/resources/Heml Arch.png)

**Services**
- services give pods a stable IP address and name that remains the same through updates, upgrades, scalability changes, and even pod failures.
-  When you create a service, that service issued a static virtual IP address from the pool of IP addresses
   that the cluster reserves for services. 
-  The virtual IP is durable. It is published to all nodes in the cluster. 
-  It doesn't change even if all the pods behind it change. In GKE, this range is automatically managed for you,
   and by default, contains over 4,000 addresses per cluster.
   
Several ways to find a service in GKE
- ENV variables
- Kube DNS
    - DNS is preinstalled in Google Kubernetes engine.
    -  Kubernetes DNS server watches the api server for the creation of new services when a new services
       created cubed DNS automatically creates a set of DNS records for it
- Istio - open platform platform indepen service mesh
  - Available as plugin in gke
  

**Types of Services**
1. ClusterIP. Exposes a service which is only accessible from within the cluster. spec.clusterIp:spec.ports[*].port
2. NodePort. Exposes a service via a static port on each node’s IP.<NodeIP>:spec.ports[*].nodePort spec.clusterIp:spec.ports[*].port
3. LoadBalancer. Exposes the service via the cloud provider’s load balancer. spec.loadBalancerIp:spec.ports[*].port <NodeIP>:spec.ports[*].nodePort spec.clusterIp:spec.ports[*].port


**Ingress**
- Ingress object defines rules for routing HTTP(S) traffic to applications running in a cluster.
- An Ingress object is associated with one or more Service objects, each of which is associated with a set of Pods.
- When you create an Ingress object, the GKE Ingress controller creates a Google Cloud HTTP(S) Load Balancer 