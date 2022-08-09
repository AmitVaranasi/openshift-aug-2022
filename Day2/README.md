# Day 2 - OpenShift

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

## Google Kubernetes
- opensource Orchestration Platform
- supports
   - Docker
   - Podman
   - Any Container that supports OCI


## RedHat OpenShift
- RedHat's distribution of Kubernetes
- Developed on top of Kubernetes with many additional features
- supports Private Container Registry out of the box unlike Kubernetes(we have setup private registry manually and configure k8s to use that registry)
- supports CI/CD out of the box
