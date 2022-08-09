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
