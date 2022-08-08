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

## Docker Commands

### Finding details about your docker installation
```
docker info
```

Expected output
<pre>
jegan@dell-precision-7670:~$ <b>docker info</b>
Client:
 Context:    default
 Debug Mode: false
 Plugins:
  app: Docker App (Docker Inc., v0.9.1-beta3)
  buildx: Docker Buildx (Docker Inc., v0.8.2-docker)
  compose: Docker Compose (Docker Inc., v2.6.0)
  scan: Docker Scan (Docker Inc., v0.17.0)

Server:
 Containers: 3
  Running: 3
  Paused: 0
  Stopped: 0
 Images: 24
 Server Version: 20.10.17
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 1
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: runc io.containerd.runc.v2 io.containerd.runtime.v1.linux
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 10c12954828e7c7c9b6e0ea9b0c02b01407d3ae1
 runc version: v1.1.2-0-ga916309
 init version: de40ad0
 Security Options:
  apparmor
  seccomp
   Profile: default
 Kernel Version: 5.14.0-1046-oem
 Operating System: Ubuntu 20.04.4 LTS
 OSType: linux
 Architecture: x86_64
 CPUs: 24
 Total Memory: 62.5GiB
 Name: dell-precision-7670
 ID: QVBR:HPEI:FOHH:UC3T:GJLO:63XP:Y6HJ:FUYM:X2XW:7IXK:SX3V:Y4NR
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false
</pre>

### Listing Docker Image from the Local Docker Registry
```
docker images
```
