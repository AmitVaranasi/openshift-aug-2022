# Day 2 - OpenShift

## Container Runtime
Example
  - runc is a Container runtime used by Docker Container Engine
  - CRI-O is a Container runtime used by Podman Container Engine

## Container Orchestration Platform
- has cluster of servers
- servers are placed in cross-geo locations
- manages containerized applications
- provides High Availability (HA) to the deployed applictions
- High Availability
    - 24/7 ( 365 the application should be live with no downtime )
- supports built-in monitoring functionalities
- supports scaling up/down your applications on demand
- Examples
   - Docker SWARM ( natively developed the Docker Inc organization that developed Docker Engine )
   - Google Kubernetes
       - supports many different types of Container Runtime
       - any Container Runtime that implements/supports Open Container Interface (OCI) are supported
   - RedHat OpenShift
   - OKD(Origin) - Opensource variant of OpenShift
   - AWS ROSA ( Managed RedHat OpenShift in AWS )
   - Azure OpenShift ( Managed RedHat OpenShift in Azure )

## Azure OpenShift
- managed RedHat OpenShift cluster that works in Microsoft Azure cloud
- RedHat OpenShift installation is taken care by Azure
- Azure decides the hardware on which they are going deploy RedHat OpenShift
- Azure decides the Operating System that they are going to use in Master/Workers Nodes
- Azure decides what Load Balancer they are going to support
- Azure takes care of setting up Private Container Registry
- Azure takes care of security aspects of your RedHat Openshift
- Azure decides which version of Openshift will be deployed, patching the OS are taken care by Azure

## Orchestration Cluster
- it has many Servers with Operating System installed on those Servers
- the Servers are normally referred as Nodes
- Node are of two type
  1. Master Node
  2. Worker Node 
- Node can be a Physical Server or Virtual Machine or Cloud based ec2 instance
- Node whether it is of type Master or Worker has Container Runtime and Container Engine installed


## Google Kubernetes
- opensource Orchestration Platform
- supports
   - Docker
   - Podman
   - Any Container that supports OCI
- applications are deployed from Container Image
- applications can also deployed via declarative manifest files that refers pre-built Container Image
- Kubernetes support adding your own Custom Resources by defining Custom Resource Definitions(CRD)
- Through CRDs, one can extend Kubernetes API to support many new features
- a bunch of Controllers to monitor and self-heal applications
- also supports Creating and deploying your own Custom Controllers to manage your Custom Resource (CR)
- Kubernetes Operators is a collection of one of more Custom Resources with one or more Custom Controllers.
- Through Kubernetes Operators one can deploy complex application within Kubernetes

## RedHat Enterprise Linux Core OS (RHCOS)
- is an optimized Operating System that is owned by RedHat for RedHat OpenShift Orchestration Platform
- it comes with pre-installed CRI-O Container Runtime and Podman Container Engine
- each version of RHCOS supports different versions of CRI-O and Podman

## RedHat OpenShift
- RedHat's distribution of Kubernetes
- supports only CRI-O Container Runtime and Podman Container Engine
- Developed on top of Kubernetes with many additional features
- supports Private Container Registry out of the box unlike Kubernetes(we have setup private registry manually and configure k8s to use that registry)
- supports CI/CD out of the box
- supports setting up your own Private GitHub like version control within OpenShift
- Backed by RedHat, hence you can get Support around the globe
- It's possible to deploy application from source code ( java, nodjs source code ) - S2I
- It's possible to deploy application from Container Image
- It's possible to deploy application using Declarative script(manifest files) i.e YAML file
- RedHat OpenShift Master Nodes only supports RedHat Enterprise Linux Core OS Operating System(RHCOS)
- RedHat OpenShift Worker Nodes supports either RHEL or RHCOS

## Finding OpenShift version
```
oc version
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc version</b>
Client Version: 4.10.25
Server Version: 4.10.25
Kubernetes Version: v1.23.5+012e945
</pre>

## Listing OpenShift nodes
```
oc get nodes
kubectl get nodes
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc get nodes</b>
NAME                        STATUS   ROLES           AGE     VERSION
master-1.ocp.tektutor.org   Ready    master,worker   4h44m   v1.23.5+012e945
master-2.ocp.tektutor.org   Ready    master,worker   4h45m   v1.23.5+012e945
master-3.ocp.tektutor.org   Ready    master,worker   4h51m   v1.23.5+012e945
worker-1.ocp.tektutor.org   Ready    worker          4h30m   v1.23.5+012e945
worker-2.ocp.tektutor.org   Ready    worker          4h30m   v1.23.5+012e945
(jegan@tektutor.org)$ <b>kubectl get nodes</b>
NAME                        STATUS   ROLES           AGE     VERSION
master-1.ocp.tektutor.org   Ready    master,worker   4h44m   v1.23.5+012e945
master-2.ocp.tektutor.org   Ready    master,worker   4h45m   v1.23.5+012e945
master-3.ocp.tektutor.org   Ready    master,worker   4h51m   v1.23.5+012e945
worker-1.ocp.tektutor.org   Ready    worker          4h30m   v1.23.5+012e945
worker-2.ocp.tektutor.org   Ready    worker          4h30m   v1.23.5+012e945
</pre>


## Listing the OpenShift projects
Kubernetes namespace is referred as Project in OpenShift.  Technically, namespace and project are one and same.

```
oc get projects
```

<pre>
(jegan@tektutor.org)$ <b>oc get projects</b>
NAME                                               DISPLAY NAME   STATUS
default                                                           Active
kube-node-lease                                                   Active
kube-public                                                       Active
kube-system                                                       Active
openshift                                                         Active
openshift-apiserver                                               Active
openshift-apiserver-operator                                      Active
openshift-authentication                                          Active
openshift-authentication-operator                                 Active
openshift-cloud-controller-manager                                Active
openshift-cloud-controller-manager-operator                       Active
openshift-cloud-credential-operator                               Active
openshift-cloud-network-config-controller                         Active
openshift-cluster-csi-drivers                                     Active
openshift-cluster-machine-approver                                Active
openshift-cluster-node-tuning-operator                            Active
openshift-cluster-samples-operator                                Active
openshift-cluster-storage-operator                                Active
openshift-cluster-version                                         Active
openshift-config                                                  Active
openshift-config-managed                                          Active
openshift-config-operator                                         Active
openshift-console                                                 Active
openshift-console-operator                                        Active
openshift-console-user-settings                                   Active
openshift-controller-manager                                      Active
openshift-controller-manager-operator                             Active
openshift-dns                                                     Active
openshift-dns-operator                                            Active
openshift-etcd                                                    Active
openshift-etcd-operator                                           Active
openshift-host-network                                            Active
openshift-image-registry                                          Active
openshift-infra                                                   Active
openshift-ingress                                                 Active
openshift-ingress-canary                                          Active
openshift-ingress-operator                                        Active
openshift-insights                                                Active
openshift-kni-infra                                               Active
openshift-kube-apiserver                                          Active
openshift-kube-apiserver-operator                                 Active
openshift-kube-controller-manager                                 Active
openshift-kube-controller-manager-operator                        Active
openshift-kube-scheduler                                          Active
openshift-kube-scheduler-operator                                 Active
openshift-kube-storage-version-migrator                           Active
openshift-kube-storage-version-migrator-operator                  Active
openshift-machine-api                                             Active
openshift-machine-config-operator                                 Active
openshift-marketplace                                             Active
openshift-monitoring                                              Active
openshift-multus                                                  Active
openshift-network-diagnostics                                     Active
openshift-network-operator                                        Active
openshift-node                                                    Active
openshift-oauth-apiserver                                         Active
openshift-openstack-infra                                         Active
openshift-operator-lifecycle-manager                              Active
openshift-operators                                               Active
openshift-ovirt-infra                                             Active
openshift-sdn                                                     Active
openshift-service-ca                                              Active
openshift-service-ca-operator                                     Active
openshift-user-workload-monitoring                                Active
openshift-vsphere-infra                                           Active
</pre>

## Control Plane Components
Control Plane Components are there only in the Master Node.

1. API Server
2. etcd key/value datastore 
3. Scheduler
4. Controller Managers

### API Server
- implements all the Orchestration functionalities as REST API
- all the OpenShift components communicate only to API Server, they are not allowed to communicate with each other directly
- stores all cluster state and application state inside the etcd database
- API Server is the only components that is allowed to talk to etcd database
- anytime there is an update that is one in etcd database, it results in triggering an event
   - some new entry created in etcd
   - some existing entry is updated in etcd
   - some existing entry is deleted from etcd
- Controllers register themselves to certain types of events
- Based on the events the Controller act

### Scheduler
- is aware of only API Server
- Scheduler won't directly communicate to etcd datastore or other OpenShift components
- Scheduler is the one which is responsible to identify a health node where application Pods can be deployed
- Scheduler then send the scheduling recommendations to API Server via REST call

### etcd
- key/value database
- cluster state and application states are stored in this

### Controllers
- Controller provide High Availability
- They help in deploying and managing appliction
- Scale up/down
- Rolling update

### OpenShift resources
- Deployment (K8s resource)
- ReplicaSet (K8s resource)
- Pod (K8s resource)
- Job (K8s resource)
- DaemonSet (K8s resource)
- StatefulSet (K8s resource)
- Build ( OpenShift resource - Custom Resource added by OpenShift )
- ImageStream ( OpenShift resource  - Custom Resource added by OpenShift ) 
- DeploymentConfig ( OpenShift resource - Custom Resource added by OpenShift )

### Deployment command looks like this
```
oc create deployment nginx --image=bitnami/nginx:latest --replicas=3
```

### Deployment
- This is a JSON/YAML definition which is stored in etcd database
- The deployment is managed by Deployment Controller
- when we applications, they are deployed as Deployment with Kubernetes/OpenShift
- Deployment Controller creates ReplicaSet, which is then managed by ReplicaSet Controller
- Deployment has one or more ReplicaSet(s)

### ReplicaSet
- This is a JSON/YAML definition which is stored in etcd database
- The ReplicaSet is managed by ReplicaSet Controller
- ReplicaSet capture details like
    - How many Pod instances are desired?
- ReplicaSet Controller reads the ReplicaSet definition and learns the desired Pod instance count
- ReplicaSet Controller creates so many Pod definition as indicated in the ReplicaSet
- ReplicaSet Controller ensures the desired Pod count matches with the actual Pod count, whenever a Pod crashes, it is the responsibility of ReplicaSet Controller to ensure the desired and actual Pods are equal
- ReplicaSet has one or more Pods

### Pod
- is a collection of one or more Containers
- IP address is assigned on the Pod level not on the Container level
- If two containers are in the same Pod, there will be sharing IP Address of the Pod
- within container, application are deployment ( tomcat,mysql, nginx these are applications )
- recommended best practice,only one application should be there in a Pod
- Pods are scheduled by Scheduler onto some Node
- every Pod has a Network Stack and Network Interface Card (NIC)

### Kubelet
- is a daemon service that interacts with the Container Runtime on the current node/server where kubelet is running
- kubelet downloads the required container image and creates the Pod containers
- kubelet frequently reports the status of Pod container status to the API server
- kubelet also monitors the health of POds running on the node and ensures they are healthy
- kubelet will there on every node ( master and worker nodes )

### kube-proxy
- is a Pod that runs one instance per node (both master and worker nodes)
- provides load-balancing a group of similar Pods

### Core DNS
- is a Pod that runs usually on master nodes but in some installation, it might even run on worker node
- Core DNS offers Service Discovery i.e application will be connect to group of Pods by Service name

### Kubectl
- is a client tool used to create and manage deployments and services in Kubernetes
- it also works in OpenShift
- it make REST call to API Server

### OC
- is a client tool used to create and manage Openshift resources in OpenShift
- it makes REST call to API Server

## Creating a project
In the below command, replace 'jegan' with your name.  The project name must be all lowercase.
```
oc new-project jegan
```

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc new-project jegan</b>
Now using project "jegan" on server "https://api.ocp.tektutor.org:6443".

You can add applications to this project with the 'new-app' command. For example, try:

    oc new-app rails-postgresql-example

to build a new example application in Ruby. Or use kubectl to deploy a simple Kubernetes application:

    kubectl create deployment hello-node --image=k8s.gcr.io/e2e-test-images/agnhost:2.33 -- /agnhost serve-hostname
</pre>

## Finding the current active project 
```
oc project
```
Expected output
<pre>
(jegan@tektutor.org)$ <b>oc project</b>
Using project "jegan" on server "https://api.ocp.tektutor.org:6443".
</pre>

