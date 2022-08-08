# OpenShift

## Hypervisor
- general terminolgy used to refer the Virtualization Software
- heavy-weight virtualization technology
  - because each Virtual Machine requires dedicated hardware resources
     - CPU Cores
     - RAM
     - Storage (HDD)
- Virtualization
  - you can run many Operating Systems side by side on the same machine
  - i.e may OS can be active
  - Type 1 Virtualization
      - Servers & Workstations
      - This can be installed directory on bare-metal server without need for Operating System
  - Type 2 Virtualization
      - Laptops, Desktops and Workstations can use Type 2
      - This requires some Operating System as Host OS ( Windows, Unix, Mac, Linux )
      - Hypervisor can only be installed on top of some OS
      
  - VMWARE
     - VMWare Workstation ( Unix, Linux and Windows ) - Type 2 Virtualization Product
     - VMWare Fusion ( Mac OS-X ) - Type 2 Virtualization Product
     - VMWare Player ( Windows ) - Type 2 Virtualization Product - Free
     - VMWare vSphere/VCenter - Type 1 Virtualization Product ( Server Grade )
  - Oracle
     - VirtualBox ( Free )
  - RedHat
     - KVM ( opensource )
  - Microsoft
     - Hyper-V
  - Parallels ( Commercial - Mac OS-X )
- Benefits
  - Server consolidation

## Medium Blog - Most commonly used docker commands
<pre>
https://medium.com/@jegan_50867/docker-commands-ba19387383b4
</pre>


## Container Technology
- lightweight virtualization technology
  - because they don't require dedicated hardware resources
  - container running in the same Operating System technically share the H/W resources available on underlying OS
- application virtualization technology
- containers are application process not an Operating System
- containers run in their own namespace
- containers are originally a Linux Technology
- Linux Kernel
  - suppport two features
  - 1. Namespace ( Isolation of containers are supported )
  - 2. Control Groups ( CGroup) - should be apply hardware upper limit quota restrictions to containers

- Containers
  - has IP address
  - has file system
  - has Network Stack ( OSI Layers )
  - has Software defined Network Card (NIC)

## Container Runtimes
- runc Container runtime is used Docker Engine


## Container Image Building Tools
- buildah
- Skopio


## Container Engine
- it is user-friendly Container software that make use of container runtime and other tools to manage container images
- used by end-users like us
- it offers easy to use user-friendly commands
- examples
  1. Podman is a Container Engine
  2. Docker is also a Container Engine

## Docker Overview
- is a Container Engine
- Docker comes two flavours
  1. Docker Community Edition - Docker CE ( OpenSource )
  2. Docker Enterprise Edition - Docker EE ( Licensed Software )

## Docker Alternates
- LXC
- Containerd
- Podman

## Container Orchestration Platforms/Tools
- Docker SWARM
   - manages containerized applications that use Docker Container Engine
- Kubernetes
   - manages containerized application that supports any container runtime that implements CNI(Container Network Interface)
   - Google
   - Opensource
   - CLI
   - Web Dashboard - limited in functionality - not enterprise grade ( in-secured )
- RedHat OpenShift
   - developed on top of Google Kubernetes with many additional features
   - manages containerized application that supports CRI-O Container Runtime (Podman - Container Engine )
   - is RedHat's distribution of Kubernetes
   - CLI and Web-interface
 
- they many containerized applications
- High Availability of your applications are guaranteed
- inbuilt-monitoring features
- scale up/down your application instances depending on demand
- rolling update
   - upgrading your live application from one version to other without any down time
