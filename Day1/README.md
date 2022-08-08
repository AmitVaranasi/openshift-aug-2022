# Day 1

# Containerization

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

### Download mysql image
```
docker pull mysql:latest
```

Expected output
<pre>
jegan@dell-precision-7670:~$ docker pull mysql:latest
latest: Pulling from library/mysql
32c1bf40aba1: Pull complete 
3ac22f3a638d: Pull complete 
b1e7273ed05e: Pull complete 
20be45a0c6ab: Pull complete 
410a229693ff: Pull complete 
1ce71e3a9b88: Pull complete 
c93c823af05b: Pull complete 
c6752c4d09c7: Pull complete 
d7f2cfe3efcb: Pull complete 
916f32cb0394: Pull complete 
0d62a5f9a14f: Pull complete 
Digest: sha256:ce2ae3bd3e9f001435c4671cf073d1d5ae55d138b16927268474fc54ba09ed79
Status: Downloaded newer image for mysql:latest
docker.io/library/mysql:latest
</pre>


### Docker Image inspect
```
jegan@dell-precision-7670:~$ <b>docker image inspect mysql:latest</b>
```

Expected output
<pre>
jegan@dell-precision-7670:~$ <b>docker image inspect mysql:latest</b>
[
    {
        "Id": "sha256:7b94cda7ffc7c59b01668e63f48e0f4ee3d16b427cc0b846193b65db671e9fa2",
        "RepoTags": [
            "mysql:latest"
        ],
        "RepoDigests": [
            "mysql@sha256:ce2ae3bd3e9f001435c4671cf073d1d5ae55d138b16927268474fc54ba09ed79"
        ],
        "Parent": "",
        "Comment": "",
        "Created": "2022-08-04T01:26:12.412321537Z",
        "Container": "06aa065e5833ed2db46adef57d922bf876630ebad5b36499c2d41f2a859a2f2b",
        "ContainerConfig": {
            "Hostname": "06aa065e5833",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "3306/tcp": {},
                "33060/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "GOSU_VERSION=1.14",
                "MYSQL_MAJOR=8.0",
                "MYSQL_VERSION=8.0.30-1.el8",
                "MYSQL_SHELL_VERSION=8.0.30-1.el8"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "#(nop) ",
                "CMD [\"mysqld\"]"
            ],
            "Image": "sha256:4185be6baa43f58474725b6ffb5f1f6ed7e99a1fa99cc0bfd4ee830e3fc3d9aa",
            "Volumes": {
                "/var/lib/mysql": {}
            },
            "WorkingDir": "",
            "Entrypoint": [
                "docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {}
        },
        "DockerVersion": "20.10.12",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "3306/tcp": {},
                "33060/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "GOSU_VERSION=1.14",
                "MYSQL_MAJOR=8.0",
                "MYSQL_VERSION=8.0.30-1.el8",
                "MYSQL_SHELL_VERSION=8.0.30-1.el8"
            ],
            "Cmd": [
                "mysqld"
            ],
            "Image": "sha256:4185be6baa43f58474725b6ffb5f1f6ed7e99a1fa99cc0bfd4ee830e3fc3d9aa",
            "Volumes": {
                "/var/lib/mysql": {}
            },
            "WorkingDir": "",
            "Entrypoint": [
                "docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": null
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 445901586,
        "VirtualSize": 445901586,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/bb081b2eb6cc77ccc60bef1ca9ddac91645de67967cfced8e3a39168cffc9e03/diff:/var/lib/docker/overlay2/1dceef8fad3fae52aa33d94b2fd4c25d5a91cf14fd5bc343f8cd99fff9719034/diff:/var/lib/docker/overlay2/b5882a2e1e7531249e24e1125ba743cf5138e8859a7a4cff0780f53cc3bf72d7/diff:/var/lib/docker/overlay2/fb9f62f3761e8c945a0a9d1a8dfcf4ce486dbfb9fa67dfe913e36dd2aa42d67f/diff:/var/lib/docker/overlay2/b5567dff06ce54f97e2257258161ee73e2bda03ab0eb226d7e66cb06160f43a0/diff:/var/lib/docker/overlay2/9a8e0aa9c8f6101f1c5ae1e633e43d9d872647817a3319189c3fd91c06bffc12/diff:/var/lib/docker/overlay2/e122f798ae0f714e9c49e2f2e891125af7c85375059ccc07fd770aa9a9f91be9/diff:/var/lib/docker/overlay2/fc77880d13878818b1fb4bdcce8bb7eebffa620e8664cf3896afeda779ee42a4/diff:/var/lib/docker/overlay2/7415c2da12a1f8d29a00fffc1b41a29a69f4d34e211bd926dc48859d19f0cfba/diff:/var/lib/docker/overlay2/9bceb8a69d472e6f80e554b20f7facb59b8fcfda71cba071fc8fdcc1aed85b44/diff",
                "MergedDir": "/var/lib/docker/overlay2/a61aa68b2c09e95bc72fa940107a143ff68cd43e77df9878269944ad1575b345/merged",
                "UpperDir": "/var/lib/docker/overlay2/a61aa68b2c09e95bc72fa940107a143ff68cd43e77df9878269944ad1575b345/diff",
                "WorkDir": "/var/lib/docker/overlay2/a61aa68b2c09e95bc72fa940107a143ff68cd43e77df9878269944ad1575b345/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:cf4db719a36940c70d724cd9eaa2fccaf1f0174ba863ebb40f428eaf13da76cc",
                "sha256:727f87cfc4aa2010d7576783a7a5f639f5bbd866219e1e919bb6bed6ce65c43b",
                "sha256:23caed4272c6e7903e9a8d53d8b4b9df7caed8ee8fb0e69bbf8e5d4bae125aa1",
                "sha256:e909c98952f3ccf508fee1882e044dff330f75e4610410d3c3c0b946ec7e5e4a",
                "sha256:05a0857d35134cf4003357cf7191e67e663fea8a3ad1d3734414508a493ebf31",
                "sha256:3a84339241ba3150f0b6324d4431fa182707c8ae31e5e60c3e2f112ac669c888",
                "sha256:6fab872104e6b09e75652b07884d190388d27d66272cc78f8957debcad5f7335",
                "sha256:052d59c7ab867eb6c17153c2d0a64cbff1b66bc7bf6452da7a58434d9c71dd6c",
                "sha256:e8f119e9974013b4c47a4cef1bef29749d751e3eb92d46726a88cb8b4cf9e4e2",
                "sha256:c6b70a293f9b3f727669e5aeba8c7b16c43caebbb0058f6068e8b1ff543dfaef",
                "sha256:4df68c319ca5e844e67ceba086417d33f5428b5f3163e9894f96d942e5febe60"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"
        }
    }
]
</pre>

### Creating your first container
```
docker run hello-world:latest
```

Expected output
<pre>
jegan@dell-precision-7670:~$ <b>docker run hello-world:latest</b>
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
2db29710123e: Pull complete 
Digest: sha256:53f1bbee2f52c39e41682ee1d388285290c5c8a76cc92b42687eecf38e0af3f0
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
</pre>

## Listing the currently running containers
```
docker ps
```

## Listing all the containers 
```
docker ps -a
```

Expected output
<pre>
jegan@dell-precision-7670:~$ <b>docker ps -a</b>
CONTAINER ID   IMAGE                COMMAND    CREATED              STATUS                          PORTS     NAMES
7fb6b5c4f204   hello-world:latest   "/hello"   About a minute ago   Exited (0) About a minute ago             awesome_goldstine
</pre>

## Renaming a conatainer
```
docker rename <old-contianer-name> <new-container-name>
```

Expected output
<pre>
egan@dell-precision-7670:~$ <b>docker rename awesome_goldstine c1</b>
jegan@dell-precision-7670:~$ <b>docker ps</b>
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
jegan@dell-precision-7670:~$ <b>docker ps -a</b>
CONTAINER ID   IMAGE                COMMAND    CREATED         STATUS                     PORTS     NAMES
7fb6b5c4f204   hello-world:latest   "/hello"   7 minutes ago   Exited (0) 7 minutes ago             c1
</pre>

## Creating a container in interactive fashion
```
docker run -it --name ubuntu1 --hostname ubuntu1 ubuntu:16.04 /bin/bash
```

Expected output
<pre>
jegan@dell-precision-7670:~$ <b>docker run -it --name ubuntu1 --hostname ubuntu1 ubuntu:16.04 /bin/bash</b>
root@ubuntu1:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@ubuntu1:/# <b>hostname</b>
ubuntu1
root@ubuntu1:/# <b>hostname -i</b>
172.17.0.2
root@ubuntu1:/# <b>exit</b>
</pre>

## Starting a exited container
```
docker start ubuntu1
```

Expected output
<pre>
jegan@dell-precision-7670:~$ docker ps -a
CONTAINER ID   IMAGE                COMMAND       CREATED              STATUS                      PORTS     NAMES
af4568a9883d   ubuntu:16.04         "/bin/bash"   About a minute ago   Exited (0) 6 seconds ago              ubuntu1
4a4a0356cd89   ubuntu:16.04         "/bin/bash"   2 minutes ago        Exited (0) 2 minutes ago              brave_northcutt
7fb6b5c4f204   hello-world:latest   "/hello"      19 minutes ago       Exited (0) 19 minutes ago             c1
jegan@dell-precision-7670:~$ docker start ubuntu1
ubuntu1
jegan@dell-precision-7670:~$ docker ps
CONTAINER ID   IMAGE          COMMAND       CREATED              STATUS        PORTS     NAMES
af4568a9883d   ubuntu:16.04   "/bin/bash"   About a minute ago   Up 1 second             ubuntu1
</pre>

## Getting inside a running container
```
docker exec -it ubuntu1 bash
```

Expected output
<pre>
jegan@dell-precision-7670:~$ docker exec -it ubuntu1 bash
root@ubuntu1:/# ls
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@ubuntu1:/# exit
exit
jegan@dell-precision-7670:~$ docker ps
CONTAINER ID   IMAGE          COMMAND       CREATED         STATUS         PORTS     NAMES
af4568a9883d   ubuntu:16.04   "/bin/bash"   6 minutes ago   Up 5 minutes             ubuntu1
</pre>

## Starting and Stopping containers
Expected output
<pre>
jegan@dell-precision-7670:~$ docker ps
CONTAINER ID   IMAGE          COMMAND       CREATED         STATUS         PORTS     NAMES
af4568a9883d   ubuntu:16.04   "/bin/bash"   6 minutes ago   Up 5 minutes             ubuntu1
jegan@dell-precision-7670:~$ docker stop ubuntu1
ubuntu1
jegan@dell-precision-7670:~$ docker start af45
af45
jegan@dell-precision-7670:~$ docker ps
CONTAINER ID   IMAGE          COMMAND       CREATED          STATUS         PORTS     NAMES
af4568a9883d   ubuntu:16.04   "/bin/bash"   10 minutes ago   Up 6 seconds             ubuntu1
jegan@dell-precision-7670:~$ docker stop af4
af4
jegan@dell-precision-7670:~$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
</pre>


## Creating a container in background mode
```
docker run -d --name web1 --hostname web1 nginx:latest
```

Expected output
<pre>
jegan@dell-precision-7670:~$ docker run -d --name web1 --hostname web1 nginx:latest 
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
1efc276f4ff9: Pull complete 
baf2da91597d: Pull complete 
05396a986fd3: Pull complete 
6a17c8e7063d: Pull complete 
27e0d286aeab: Pull complete 
b1349eea8fc5: Pull complete 
Digest: sha256:ecc068890de55a75f1a32cc8063e79f90f0b043d70c5fcf28f1713395a4b3d49
Status: Downloaded newer image for nginx:latest
eb3e23fdb20893913da2c3c1817afcc9a47cd5160ebf2287d08aadcac44669f2
jegan@dell-precision-7670:~$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS     NAMES
eb3e23fdb208   nginx:latest   "/docker-entrypoint.…"   24 seconds ago   Up 23 seconds   80/tcp    web1
</pre>

## Finding detailed information about a container
```
docker inspect web1
```

Expected output
<pre>
jegan@dell-precision-7670:~$ docker inspect web1
[
    {
        "Id": "eb3e23fdb20893913da2c3c1817afcc9a47cd5160ebf2287d08aadcac44669f2",
        "Created": "2022-08-08T09:47:07.303477315Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            "-g",
            "daemon off;"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 67675,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2022-08-08T09:47:07.761413365Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:b692a91e4e1582db97076184dae0b2f4a7a86b68c4fe6f91affa50ae06369bf5",
        "ResolvConfPath": "/var/lib/docker/containers/eb3e23fdb20893913da2c3c1817afcc9a47cd5160ebf2287d08aadcac44669f2/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/eb3e23fdb20893913da2c3c1817afcc9a47cd5160ebf2287d08aadcac44669f2/hostname",
        "HostsPath": "/var/lib/docker/containers/eb3e23fdb20893913da2c3c1817afcc9a47cd5160ebf2287d08aadcac44669f2/hosts",
        "LogPath": "/var/lib/docker/containers/eb3e23fdb20893913da2c3c1817afcc9a47cd5160ebf2287d08aadcac44669f2/eb3e23fdb20893913da2c3c1817afcc9a47cd5160ebf2287d08aadcac44669f2-json.log",
        "Name": "/web1",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "docker-default",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "host",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/ef0aa1912aa64b2df3c86e2dd7968648e0dab07d62202e261e031047d8986266-init/diff:/var/lib/docker/overlay2/5402cc115786dffaaaa93c8eece071f3bc677a34f85beb1664bc57c5a861b69f/diff:/var/lib/docker/overlay2/96b3fb4c67add269bb933cd37e890ffbf877efc1ee43e53ec92066d8f323afbf/diff:/var/lib/docker/overlay2/4b79ff4b1bae970dbdb7010af2ca5b943393b203a7623bcec1ed5cada5e68e0e/diff:/var/lib/docker/overlay2/6de0d8783a2d79ed69cdc2c41ef2fae4ab53361c36c72c85f980669f377ff7a9/diff:/var/lib/docker/overlay2/60f21d8864c1984464b914a78d21304f2bd7e33b36a45ffbdff17ae81e1390b3/diff:/var/lib/docker/overlay2/bcdac2552c4e019642342ca2c81df10ad4e9e94b9b4bd5a717bb17b6f24376bb/diff",
                "MergedDir": "/var/lib/docker/overlay2/ef0aa1912aa64b2df3c86e2dd7968648e0dab07d62202e261e031047d8986266/merged",
                "UpperDir": "/var/lib/docker/overlay2/ef0aa1912aa64b2df3c86e2dd7968648e0dab07d62202e261e031047d8986266/diff",
                "WorkDir": "/var/lib/docker/overlay2/ef0aa1912aa64b2df3c86e2dd7968648e0dab07d62202e261e031047d8986266/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "web1",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.23.1",
                "NJS_VERSION=0.7.6",
                "PKG_RELEASE=1~bullseye"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "nginx:latest",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGQUIT"
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "bd769865225f821b6f053373b00ad130c635eafa2feb1813dee315669de35685",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "80/tcp": null
            },
            "SandboxKey": "/var/run/docker/netns/bd769865225f",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "30c763c82cb4c159e65cfb0e4f8fed5adf74c74bfb5e78f30ca8b1360aa83d8e",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "d7fce2dc7dda8e69598b45a367b49bdebac6f5ecd97a9f2f84f81955d7e56d3a",
                    "EndpointID": "30c763c82cb4c159e65cfb0e4f8fed5adf74c74bfb5e78f30ca8b1360aa83d8e",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]
</pre>


## Accessing the nginx web1 container web page
<pre>
jegan@dell-precision-7670:~$ docker inspect web1 | grep IPA
            "SecondaryIPAddresses": null,
            "IPAddress": "172.17.0.2",
                    "IPAMConfig": null,
                    "IPAddress": "172.17.0.2",
jegan@dell-precision-7670:~$ curl 172.17.0.2
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>jegan@dell-precision-7670:~$ docker run -d --name web2 --hostname web2 nginx:latest
59eeb34bca86d636cfa34c6de270c44efab9ac31bd6c2d72804d326e97f7a2fe
jegan@dell-precision-7670:~$ docker run -d --name web3 --hostname web3 nginx:latest
a2af8503d2807e4dc0c4e0b715f124f910785d35bd7bd4ced4444a580b1ed92d
jegan@dell-precision-7670:~$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS     NAMES
a2af8503d280   nginx:latest   "/docker-entrypoint.…"   2 seconds ago    Up 1 second     80/tcp    web3
59eeb34bca86   nginx:latest   "/docker-entrypoint.…"   10 seconds ago   Up 9 seconds    80/tcp    web2
eb3e23fdb208   nginx:latest   "/docker-entrypoint.…"   13 minutes ago   Up 13 minutes   80/tcp    web1
jegan@dell-precision-7670:~$ docker inspect -f {{.NetworkSettings.IPAddress}} web1
172.17.0.2
jegan@dell-precision-7670:~$ docker inspect -f {{.NetworkSettings.IPAddress}} web2
172.17.0.3
jegan@dell-precision-7670:~$ docker inspect -f {{.NetworkSettings.IPAddress}} web3
172.17.0.4
jegan@dell-precision-7670:~$ curl 172.17.0.3
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
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
</pre>

## Inspecting Network in Docker
<pre>
jegan@dell-precision-7670:~$ ifconfig
docker0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet6 fe80::42:33ff:fe5a:f98f  prefixlen 64  scopeid 0x20<link>
        ether 02:42:33:5a:f9:8f  txqueuelen 0  (Ethernet)
        RX packets 19  bytes 2662 (2.6 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 167  bytes 25477 (25.4 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

enp0s31f6: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether 08:92:04:3e:f8:c3  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        device interrupt 19  memory 0x96100000-96120000  

enx4ee6c01ee064: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.20.10.5  netmask 255.255.255.240  broadcast 172.20.10.15
        inet6 fe80::ae04:231c:8d57:a547  prefixlen 64  scopeid 0x20<link>
        inet6 2401:4900:234c:76de:84e0:88d0:e72a:40ec  prefixlen 64  scopeid 0x0<global>
        inet6 2401:4900:234c:76de:38cb:592e:c8d8:d1c8  prefixlen 64  scopeid 0x0<global>
        ether 4e:e6:c0:1e:e0:64  txqueuelen 1000  (Ethernet)
        RX packets 108926  bytes 77907206 (77.9 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 178139  bytes 45110718 (45.1 MB)
        TX errors 1  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 400988124  bytes 79685246606 (79.6 GB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 400988124  bytes 79685246606 (79.6 GB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth6a74f11: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::8c96:baff:fe8b:21ab  prefixlen 64  scopeid 0x20<link>
        ether 8e:96:ba:8b:21:ab  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 55  bytes 8513 (8.5 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth9e16802: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::2c22:18ff:fead:ca21  prefixlen 64  scopeid 0x20<link>
        ether 2e:22:18:ad:ca:21  txqueuelen 0  (Ethernet)
        RX packets 7  bytes 1275 (1.2 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 71  bytes 10287 (10.2 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

vethc23d13d: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::5c67:f8ff:fe90:c5de  prefixlen 64  scopeid 0x20<link>
        ether 5e:67:f8:90:c5:de  txqueuelen 0  (Ethernet)
        RX packets 12  bytes 1653 (1.6 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 126  bytes 19279 (19.2 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

virbr0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 192.168.122.1  netmask 255.255.255.0  broadcast 192.168.122.255
        ether 52:54:00:79:0a:83  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlp0s20f3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.104  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::e3a5:c91c:4313:30b9  prefixlen 64  scopeid 0x20<link>
        ether a0:80:69:39:18:9f  txqueuelen 1000  (Ethernet)
        RX packets 1447396  bytes 1144891537 (1.1 GB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1774551  bytes 833241643 (833.2 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

jegan@dell-precision-7670:~$ docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
d7fce2dc7dda   bridge    bridge    local
5787a5e22bc5   host      host      local
da0bf7e46cb4   none      null      local
jegan@dell-precision-7670:~$ docker network inspect bridge
[
    {
        "Name": "bridge",
        "Id": "d7fce2dc7dda8e69598b45a367b49bdebac6f5ecd97a9f2f84f81955d7e56d3a",
        "Created": "2022-08-08T08:04:30.914133428+05:30",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": [
                {
                    "Subnet": "172.17.0.0/16",
                    "Gateway": "172.17.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "59eeb34bca86d636cfa34c6de270c44efab9ac31bd6c2d72804d326e97f7a2fe": {
                "Name": "web2",
                "EndpointID": "f71df1e5dd40da8601d0729c3bb3e5bc30803ced9c0f99fe9863aca12b38d8bc",
                "MacAddress": "02:42:ac:11:00:03",
                "IPv4Address": "172.17.0.3/16",
                "IPv6Address": ""
            },
            "a2af8503d2807e4dc0c4e0b715f124f910785d35bd7bd4ced4444a580b1ed92d": {
                "Name": "web3",
                "EndpointID": "0511ddcbbc1ac925b35040670a9d0bc9400a51ee027de51f17a7a6d582bc5030",
                "MacAddress": "02:42:ac:11:00:04",
                "IPv4Address": "172.17.0.4/16",
                "IPv6Address": ""
            },
            "eb3e23fdb20893913da2c3c1817afcc9a47cd5160ebf2287d08aadcac44669f2": {
                "Name": "web1",
                "EndpointID": "30c763c82cb4c159e65cfb0e4f8fed5adf74c74bfb5e78f30ca8b1360aa83d8e",
                "MacAddress": "02:42:ac:11:00:02",
                "IPv4Address": "172.17.0.2/16",
                "IPv6Address": ""
            }
        },
        "Options": {
            "com.docker.network.bridge.default_bridge": "true",
            "com.docker.network.bridge.enable_icc": "true",
            "com.docker.network.bridge.enable_ip_masquerade": "true",
            "com.docker.network.bridge.host_binding_ipv4": "0.0.0.0",
            "com.docker.network.bridge.name": "docker0",
            "com.docker.network.driver.mtu": "1500"
        },
        "Labels": {}
    }
]
</pre>

## Creating a custom network and adding a container to your private network
<pre>
jegan@dell-precision-7670:~$ docker network create my-net-3 --subnet 192.168.100.0/24
4b90a70702c8edb740af6c051a0ee6d390b45501bcbbc7c9b7ee88b0d70cd32d
jegan@dell-precision-7670:~$ docker network ls
NETWORK ID     NAME       DRIVER    SCOPE
d7fce2dc7dda   bridge     bridge    local
5787a5e22bc5   host       host      local
e1424119e2ec   my-net-1   bridge    local
5319369b37d3   my-net-2   bridge    local
4b90a70702c8   my-net-3   bridge    local
da0bf7e46cb4   none       null      local
jegan@dell-precision-7670:~$ ifconfig
br-4b90a70702c8: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 192.168.100.1  netmask 255.255.255.0  broadcast 192.168.100.255
        ether 02:42:b5:df:ba:37  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

br-5319369b37d3: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.19.0.1  netmask 255.255.0.0  broadcast 172.19.255.255
        ether 02:42:68:40:72:f1  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

br-e1424119e2ec: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.18.0.1  netmask 255.255.0.0  broadcast 172.18.255.255
        ether 02:42:be:08:71:07  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

docker0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet6 fe80::42:33ff:fe5a:f98f  prefixlen 64  scopeid 0x20<link>
        ether 02:42:33:5a:f9:8f  txqueuelen 0  (Ethernet)
        RX packets 19  bytes 2662 (2.6 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 210  bytes 32848 (32.8 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

enp0s31f6: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether 08:92:04:3e:f8:c3  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        device interrupt 19  memory 0x96100000-96120000  

enx4ee6c01ee064: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.20.10.5  netmask 255.255.255.240  broadcast 172.20.10.15
        inet6 fe80::ae04:231c:8d57:a547  prefixlen 64  scopeid 0x20<link>
        inet6 2401:4900:234c:76de:84e0:88d0:e72a:40ec  prefixlen 64  scopeid 0x0<global>
        inet6 2401:4900:234c:76de:38cb:592e:c8d8:d1c8  prefixlen 64  scopeid 0x0<global>
        ether 4e:e6:c0:1e:e0:64  txqueuelen 1000  (Ethernet)
        RX packets 124401  bytes 80801356 (80.8 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 252860  bytes 67078354 (67.0 MB)
        TX errors 1  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 401155000  bytes 79701241633 (79.7 GB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 401155000  bytes 79701241633 (79.7 GB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth6a74f11: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::8c96:baff:fe8b:21ab  prefixlen 64  scopeid 0x20<link>
        ether 8e:96:ba:8b:21:ab  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 100  bytes 16157 (16.1 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth9e16802: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::2c22:18ff:fead:ca21  prefixlen 64  scopeid 0x20<link>
        ether 2e:22:18:ad:ca:21  txqueuelen 0  (Ethernet)
        RX packets 7  bytes 1275 (1.2 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 116  bytes 17931 (17.9 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

vethc23d13d: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::5c67:f8ff:fe90:c5de  prefixlen 64  scopeid 0x20<link>
        ether 5e:67:f8:90:c5:de  txqueuelen 0  (Ethernet)
        RX packets 12  bytes 1653 (1.6 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 169  bytes 26650 (26.6 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

virbr0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 192.168.122.1  netmask 255.255.255.0  broadcast 192.168.122.255
        ether 52:54:00:79:0a:83  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlp0s20f3: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.1.104  netmask 255.255.255.0  broadcast 192.168.1.255
        inet6 fe80::e3a5:c91c:4313:30b9  prefixlen 64  scopeid 0x20<link>
        ether a0:80:69:39:18:9f  txqueuelen 1000  (Ethernet)
        RX packets 1447979  bytes 1144958145 (1.1 GB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 1775183  bytes 833312722 (833.3 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

jegan@dell-precision-7670:~$ docker run -dit --name c1 --hostname c1 ubuntu:16.04 /bin/bash
docker: Error response from daemon: Conflict. The container name "/c1" is already in use by container "7fb6b5c4f20464120725d73e1bc6932f2138bc74863298a3ebddffe2004bd918". You have to remove (or rename) that container to be able to reuse that name.
See 'docker run --help'.
jegan@dell-precision-7670:~$ docker run -dit --name c2 --hostname c2 --network=my-net-3 ubuntu:16.04 /bin/bash
7d491f19487886cf49618b5224638bdadc7dceb9501257b520cee0ec93e8eeee
jegan@dell-precision-7670:~$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS     NAMES
7d491f194878   ubuntu:16.04   "/bin/bash"              3 seconds ago    Up 2 seconds              c2
a2af8503d280   nginx:latest   "/docker-entrypoint.…"   17 minutes ago   Up 17 minutes   80/tcp    web3
59eeb34bca86   nginx:latest   "/docker-entrypoint.…"   17 minutes ago   Up 17 minutes   80/tcp    web2
eb3e23fdb208   nginx:latest   "/docker-entrypoint.…"   31 minutes ago   Up 31 minutes   80/tcp    web1
jegan@dell-precision-7670:~$ docker inspect -f {{.NetworkSettings.IPAddress}} c2

jegan@dell-precision-7670:~$ docker inspect c2 | grep IPA
            "SecondaryIPAddresses": null,
            "IPAddress": "",
                    "IPAMConfig": null,
                    "IPAddress": "192.168.100.2",


### ⛹️‍♂️ Lab - Creating a LoadBalancer using nginx image
```
docker run -d --name web1 --hostname web1 nginx:latest
docker run -d --name web2 --hostname web2 nginx:latest
docker run -d --name web3 --hostname web3 nginx:latest

docker run -d --name lb --hostname lb -p 80:80 nginx:latest

docker ps
```

Expected output
<pre>
jegan@dell-precision-7670:~$ docker run -d --name web1 --hostname web1 nginx:latest
2b22ed87b8749ee715a90de068a34b2eb47077cfee340e9cb3012dcde0c25822
jegan@dell-precision-7670:~$ docker run -d --name web2 --hostname web2 nginx:latest
98d61adfb0bdb18322ab55e1c454d70ff8f31dc03529c553d597e5f65dfcfc5c
jegan@dell-precision-7670:~$ docker run -d --name web3 --hostname web3 nginx:latest
e1ba3ee3ca7fd60a96bb7fe8d6cc82ccbe879889e1d93e6c7dbbb3f9d7a96075
jegan@dell-precision-7670:~$ docker run -d --name lb --hostname lb -p 80:80 nginx:latest
a46601633de84c6e327f4d9dd2a4c9902d0475915034b21602b1f6659d2fefd4
jegan@dell-precision-7670:~$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS              PORTS                               NAMES
a46601633de8   nginx:latest   "/docker-entrypoint.…"   2 seconds ago        Up 1 second         0.0.0.0:80->80/tcp, :::80->80/tcp   lb
e1ba3ee3ca7f   nginx:latest   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp                              web3
98d61adfb0bd   nginx:latest   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp                              web2
2b22ed87b874   nginx:latest   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp                              web1

</pre>
</pre>


## Configure Load Balancer Container to route the traffic to any one of the container ie web1 or web2 or web3
<pre>
jegan@dell-precision-7670:~$ docker run -d --name web1 --hostname web1 nginx:latest
2b22ed87b8749ee715a90de068a34b2eb47077cfee340e9cb3012dcde0c25822
jegan@dell-precision-7670:~$ docker run -d --name web2 --hostname web2 nginx:latest
98d61adfb0bdb18322ab55e1c454d70ff8f31dc03529c553d597e5f65dfcfc5c
jegan@dell-precision-7670:~$ docker run -d --name web3 --hostname web3 nginx:latest
e1ba3ee3ca7fd60a96bb7fe8d6cc82ccbe879889e1d93e6c7dbbb3f9d7a96075
jegan@dell-precision-7670:~$ docker run -d --name lb --hostname lb -p 80:80 nginx:latest
a46601633de84c6e327f4d9dd2a4c9902d0475915034b21602b1f6659d2fefd4
jegan@dell-precision-7670:~$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED              STATUS              PORTS                               NAMES
a46601633de8   nginx:latest   "/docker-entrypoint.…"   2 seconds ago        Up 1 second         0.0.0.0:80->80/tcp, :::80->80/tcp   lb
e1ba3ee3ca7f   nginx:latest   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp                              web3
98d61adfb0bd   nginx:latest   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp                              web2
2b22ed87b874   nginx:latest   "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp                              web1
jegan@dell-precision-7670:~$ docker exec -it lb bash
root@lb:/# cd /etc/nginx
root@lb:/etc/nginx# ls
conf.d	fastcgi_params	mime.types  modules  nginx.conf  scgi_params  uwsgi_params
root@lb:/etc/nginx# vim
bash: vim: command not found
root@lb:/etc/nginx# vim
bash: vim: command not found
root@lb:/etc/nginx# vi
bash: vi: command not found
root@lb:/etc/nginx# more nginx.conf

user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}
root@lb:/etc/nginx# 
root@lb:/etc/nginx# 
root@lb:/etc/nginx# 
root@lb:/etc/nginx# 
root@lb:/etc/nginx# 
root@lb:/etc/nginx# 
root@lb:/etc/nginx# 
root@lb:/etc/nginx# 
root@lb:/etc/nginx# ls
conf.d	fastcgi_params	mime.types  modules  nginx.conf  scgi_params  uwsgi_params
root@lb:/etc/nginx# pwd
/etc/nginx
root@lb:/etc/nginx# exit
exit
jegan@dell-precision-7670:~$ cd devops-aug-2022/
jegan@dell-precision-7670:~/devops-aug-2022$ cd ..
jegan@dell-precision-7670:~$ cd openshift-aug-2022/
jegan@dell-precision-7670:~/openshift-aug-2022$ cd Day1
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker cp lb:/etc/nginx/nginx.conf .
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ ls
nginx.conf  README.md
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ vim nginx.conf 
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker inspect web1|grep IPA
            "SecondaryIPAddresses": null,
            "IPAddress": "172.17.0.2",
                    "IPAMConfig": null,
                    "IPAddress": "172.17.0.2",
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker inspect web2|grep IPA
            "SecondaryIPAddresses": null,
            "IPAddress": "172.17.0.3",
                    "IPAMConfig": null,
                    "IPAddress": "172.17.0.3",
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker inspect web3|grep IPA
            "SecondaryIPAddresses": null,
            "IPAddress": "172.17.0.4",
                    "IPAMConfig": null,
                    "IPAddress": "172.17.0.4",
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ vim nginx.conf 
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ ls
nginx.conf  README.md
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker cp nginx.conf lb:/etc/nginx/nginx.conf
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker restart lb
lb
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                               NAMES
a46601633de8   nginx:latest   "/docker-entrypoint.…"   9 minutes ago    Up 1 second     0.0.0.0:80->80/tcp, :::80->80/tcp   lb
e1ba3ee3ca7f   nginx:latest   "/docker-entrypoint.…"   10 minutes ago   Up 10 minutes   80/tcp                              web3
98d61adfb0bd   nginx:latest   "/docker-entrypoint.…"   10 minutes ago   Up 10 minutes   80/tcp                              web2
2b22ed87b874   nginx:latest   "/docker-entrypoint.…"   10 minutes ago   Up 10 minutes   80/tcp                              web1
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ echo "Server 1" > index.html
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker exec -it web1 bash
root@web1:/# cd /etc/nginx
root@web1:/etc/nginx# ls
conf.d	fastcgi_params	mime.types  modules  nginx.conf  scgi_params  uwsgi_params
root@web1:/etc/nginx# more nginx.conf

user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}
root@web1:/etc/nginx# 
root@web1:/etc/nginx# 
root@web1:/etc/nginx# cd conf.d/
root@web1:/etc/nginx/conf.d# ls
default.conf
root@web1:/etc/nginx/conf.d# ls -l
total 4
-rw-r--r-- 1 root root 1093 Aug  8 10:35 default.conf
root@web1:/etc/nginx/conf.d# more default.conf 
server {
    listen       80;
    listen  [::]:80;
    server_name  localhost;

    #access_log  /var/log/nginx/host.access.log  main;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }

    #error_page  404              /404.html;

    # redirect server error pages to the static page /50x.html
    #
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }

    # proxy the PHP scripts to Apache listening on 127.0.0.1:80
    #
    #location ~ \.php$ {
    #    proxy_pass   http://127.0.0.1;
    #}

    # pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
root@web1:/etc/nginx/conf.d# cat /usr/share/nginx/html/index.html 
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
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
root@web1:/etc/nginx/conf.d# exit
exit
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ ls
index.html  nginx.conf  README.md
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ cat index.html 
Server 1
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker cp index.html web1:/usr/share/nginx/html/index.html
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ echo "Server 2" > index.html
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker cp index.html web2:/usr/share/nginx/html/index.html
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ echo "Server 3" > index.html
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker cp index.html web3:/usr/share/nginx/html/index.html
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ curl localhost
Server 1
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ curl localhost
Server 1
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ curl localhost
Server 1

</pre>


## The updated Nginx load balancer configuration file should look like below
<pre>
user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}

http {
    upstream backend {
        server 172.17.0.2:80;
        server 172.17.0.3:80;
        server 172.17.0.4:80;
    }

    server {
        location / {
            proxy_pass http://backend;
        }
    }
}
</pre>


## Storing mysql db records in a external storage using Volume Mounting
<pre>
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker run -d --name db --hostname db -e MYSQL_ROOT_PASSWORD=root mysql:latest
19dd70ba784c84e221eeb864850e41c82a1b16acc8975710157db073a512b4b9
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS             PORTS                               NAMES
19dd70ba784c   mysql:latest   "docker-entrypoint.s…"   4 seconds ago   Up 3 seconds       3306/tcp, 33060/tcp                 db
a46601633de8   nginx:latest   "/docker-entrypoint.…"   2 hours ago     Up About an hour   0.0.0.0:80->80/tcp, :::80->80/tcp   lb
e1ba3ee3ca7f   nginx:latest   "/docker-entrypoint.…"   2 hours ago     Up 2 hours         80/tcp                              web3
98d61adfb0bd   nginx:latest   "/docker-entrypoint.…"   2 hours ago     Up 2 hours         80/tcp                              web2
2b22ed87b874   nginx:latest   "/docker-entrypoint.…"   2 hours ago     Up 2 hours         80/tcp                              web1
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker exec -it db bash
bash-4.4# ls
bin   dev			  entrypoint.sh  home  lib64  mnt  proc  run   srv  tmp  var
boot  docker-entrypoint-initdb.d  etc		 lib   media  opt  root  sbin  sys  usr
bash-4.4# mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.30 MySQL Community Server - GPL

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.00 sec)

mysql> CREATE DATABASE tektutor;
Query OK, 1 row affected (0.00 sec)

mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| tektutor           |
+--------------------+
5 rows in set (0.00 sec)

mysql> USE tektutor;
Database changed
mysql> CREATE TABLE training ( id int, name varchar(60), duration varchar(60));
Query OK, 0 rows affected (0.03 sec)

mysql> SHOW TABLES;
+--------------------+
| Tables_in_tektutor |
+--------------------+
| training           |
+--------------------+
1 row in set (0.00 sec)

mysql> INSERT INTO training VALUES ( 1, "Advanced C++ Programming", "5 Days" );
Query OK, 1 row affected (0.01 sec)

mysql> INSERT INTO training VALUES ( 2, "Game Programming using Qt and QML", "5 Days" );
Query OK, 1 row affected (0.01 sec)

mysql> SELECT * FROM training;
+------+-----------------------------------+----------+
| id   | name                              | duration |
+------+-----------------------------------+----------+
|    1 | Advanced C++ Programming          | 5 Days   |
|    2 | Game Programming using Qt and QML | 5 Days   |
+------+-----------------------------------+----------+
2 rows in set (0.00 sec)

mysql> exit
Bye
bash-4.4# exit
exit
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker stop db
db
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED       STATUS             PORTS                               NAMES
a46601633de8   nginx:latest   "/docker-entrypoint.…"   2 hours ago   Up About an hour   0.0.0.0:80->80/tcp, :::80->80/tcp   lb
e1ba3ee3ca7f   nginx:latest   "/docker-entrypoint.…"   2 hours ago   Up 2 hours         80/tcp                              web3
98d61adfb0bd   nginx:latest   "/docker-entrypoint.…"   2 hours ago   Up 2 hours         80/tcp                              web2
2b22ed87b874   nginx:latest   "/docker-entrypoint.…"   2 hours ago   Up 2 hours         80/tcp                              web1
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker start db
db
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS             PORTS                               NAMES
19dd70ba784c   mysql:latest   "docker-entrypoint.s…"   3 minutes ago   Up 2 seconds       3306/tcp, 33060/tcp                 db
a46601633de8   nginx:latest   "/docker-entrypoint.…"   2 hours ago     Up About an hour   0.0.0.0:80->80/tcp, :::80->80/tcp   lb
e1ba3ee3ca7f   nginx:latest   "/docker-entrypoint.…"   2 hours ago     Up 2 hours         80/tcp                              web3
98d61adfb0bd   nginx:latest   "/docker-entrypoint.…"   2 hours ago     Up 2 hours         80/tcp                              web2
2b22ed87b874   nginx:latest   "/docker-entrypoint.…"   2 hours ago     Up 2 hours         80/tcp                              web1
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker exec -it db bash
bash-4.4# mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.30 MySQL Community Server - GPL

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| tektutor           |
+--------------------+
5 rows in set (0.01 sec)

mysql> USE tektutor;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> SHOW TABLES;
+--------------------+
| Tables_in_tektutor |
+--------------------+
| training           |
+--------------------+
1 row in set (0.01 sec)

mysql> SELECT * 
    -> FROM training;
+------+-----------------------------------+----------+
| id   | name                              | duration |
+------+-----------------------------------+----------+
|    1 | Advanced C++ Programming          | 5 Days   |
|    2 | Game Programming using Qt and QML | 5 Days   |
+------+-----------------------------------+----------+
2 rows in set (0.00 sec)

mysql> exit
Bye
bash-4.4# exit
exit
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker rm -f db
db
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker run -d --name db --hostname db -e MYSQL_ROOT_PASSWORD=root mysql:latest
3239cfacc983b592d93a4af5257e857ade5c6b1565427fafdd3e9d5468390eb6
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker exec -it db bash
bash-4.4# mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.30 MySQL Community Server - GPL

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.01 sec)

mysql> exit
Bye
bash-4.4# exit
exit
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker rm -f db
db
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ mkdir -p /tmp/mysql
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ ls -l /tmp/mysql
total 0
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ ls -lha /tmp/mysql
total 8.0K
drwxrwxr-x  2 jegan jegan 4.0K Aug  8 17:43 .
drwxrwxrwt 22 root  root  4.0K Aug  8 17:43 ..
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ set -o vi
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker run -d --name db --hostname db -v /tmp/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root mysql:latest
2f1ef9a5424168ca8a5de16ef6f9cd865e81e399b0bf9cb390e93cd7a84038fb
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS             PORTS                               NAMES
2f1ef9a54241   mysql:latest   "docker-entrypoint.s…"   3 seconds ago   Up 3 seconds       3306/tcp, 33060/tcp                 db
a46601633de8   nginx:latest   "/docker-entrypoint.…"   2 hours ago     Up About an hour   0.0.0.0:80->80/tcp, :::80->80/tcp   lb
e1ba3ee3ca7f   nginx:latest   "/docker-entrypoint.…"   2 hours ago     Up 2 hours         80/tcp                              web3
98d61adfb0bd   nginx:latest   "/docker-entrypoint.…"   2 hours ago     Up 2 hours         80/tcp                              web2
2b22ed87b874   nginx:latest   "/docker-entrypoint.…"   2 hours ago     Up 2 hours         80/tcp                              web1
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker exec -it db bash
bash-4.4# mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.30 MySQL Community Server - GPL

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> CREATE DATABASE tektutor;
Query OK, 1 row affected (0.01 sec)

mysql> USE tektutor;
Database changed
mysql> CREATE TABLE training ( id int, name varchar(50), duration varchar(50) );
Query OK, 0 rows affected (0.03 sec)

mysql> INSERT INTO training VALUES ( 1, "Microservices", "5 Days" );
Query OK, 1 row affected (0.02 sec)

mysql> select * from training;
+------+---------------+----------+
| id   | name          | duration |
+------+---------------+----------+
|    1 | Microservices | 5 Days   |
+------+---------------+----------+
1 row in set (0.00 sec)

mysql> exit
Bye
bash-4.4# exit
exit
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker rm -f db
db
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker ps -a
CONTAINER ID   IMAGE          COMMAND                  CREATED       STATUS       PORTS                               NAMES
a46601633de8   nginx:latest   "/docker-entrypoint.…"   2 hours ago   Up 2 hours   0.0.0.0:80->80/tcp, :::80->80/tcp   lb
e1ba3ee3ca7f   nginx:latest   "/docker-entrypoint.…"   2 hours ago   Up 2 hours   80/tcp                              web3
98d61adfb0bd   nginx:latest   "/docker-entrypoint.…"   2 hours ago   Up 2 hours   80/tcp                              web2
2b22ed87b874   nginx:latest   "/docker-entrypoint.…"   2 hours ago   Up 2 hours   80/tcp                              web1
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker run -d --name db --hostname db -v /tmp/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root mysql:latest
836943c501667a9126ab87819aa90dc191c8b98fe65569eb8544023344346c9d
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ docker exec -it db sh
sh-4.4# mysql -u root -p
Enter password: 
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.30 MySQL Community Server - GPL

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
| tektutor           |
+--------------------+
5 rows in set (0.00 sec)

mysql> USE tektutor;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> SHOW TABLES;
+--------------------+
| Tables_in_tektutor |
+--------------------+
| training           |
+--------------------+
1 row in set (0.00 sec)

mysql> SELECT * FROM training;
+------+---------------+----------+
| id   | name          | duration |
+------+---------------+----------+
|    1 | Microservices | 5 Days   |
+------+---------------+----------+
1 row in set (0.00 sec)

mysql> ^C
mysql> exit
Bye
sh-4.4# df -h
Filesystem      Size  Used Avail Use% Mounted on
overlay         930G   31G  852G   4% /
tmpfs            64M     0   64M   0% /dev
tmpfs            32G     0   32G   0% /sys/fs/cgroup
shm              64M     0   64M   0% /dev/shm
/dev/nvme0n1p3  930G   31G  852G   4% /etc/hosts
tmpfs            32G     0   32G   0% /proc/asound
tmpfs            32G     0   32G   0% /proc/acpi
tmpfs            32G     0   32G   0% /proc/scsi
tmpfs            32G     0   32G   0% /sys/firmware
sh-4.4# exit
exit
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev             32G     0   32G   0% /dev
tmpfs           6.3G  3.1M  6.3G   1% /run
/dev/nvme0n1p3  930G   31G  852G   4% /
tmpfs            32G  136M   32G   1% /dev/shm
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs            32G     0   32G   0% /sys/fs/cgroup
/dev/loop0      128K  128K     0 100% /snap/bare/5
/dev/loop1      114M  114M     0 100% /snap/core/13425
/dev/loop3       55M   55M     0 100% /snap/core18/1754
/dev/loop2      219M  219M     0 100% /snap/gnome-3-34-1804/77
/dev/loop4       62M   62M     0 100% /snap/core20/1587
/dev/loop7       50M   50M     0 100% /snap/snap-store/433
/dev/loop5      243M  243M     0 100% /snap/gnome-3-34-1804/27
/dev/loop8      401M  401M     0 100% /snap/gnome-3-38-2004/112
/dev/loop6       55M   55M     0 100% /snap/snap-store/558
/dev/loop10     142M  142M     0 100% /snap/chromium/2051
/dev/loop9       56M   56M     0 100% /snap/core18/2538
/dev/loop11      63M   63M     0 100% /snap/gtk-common-themes/1506
/dev/loop14      92M   92M     0 100% /snap/gtk-common-themes/1535
/dev/loop12     222M  222M     0 100% /snap/code/102
/dev/loop13     134M  134M     0 100% /snap/chromium/2036
/dev/nvme0n1p1  861M   46M  816M   6% /boot/efi
tmpfs           6.3G   64K  6.3G   1% /run/user/1001
/dev/loop15     224M  224M     0 100% /snap/code/103
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ sudo su -
[sudo] password for jegan: 
root@dell-precision-7670:~# cd /var/lib/docker
root@dell-precision-7670:/var/lib/docker# ls
buildkit  containers  image  network  overlay2  plugins  runtimes  swarm  tmp  trust  volumes
root@dell-precision-7670:/var/lib/docker# cd volumes/
root@dell-precision-7670:/var/lib/docker/volumes# ls
17e0ff685078422080e74a3dc76f834980211ba9dec889a4aa5c6220e78b8f66  backingFsBlockDev
801a2e2e7cb0734ce0d534026563640ffc9d614e33e586a34704cd6e8a661f3d  metadata.db
809fd2709821011a787178ec6f08985fa884f601f39733193add2124bfd370c5
root@dell-precision-7670:/var/lib/docker/volumes# docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                               NAMES
836943c50166   mysql:latest   "docker-entrypoint.s…"   2 minutes ago   Up 2 minutes   3306/tcp, 33060/tcp                 db
a46601633de8   nginx:latest   "/docker-entrypoint.…"   2 hours ago     Up 2 hours     0.0.0.0:80->80/tcp, :::80->80/tcp   lb
e1ba3ee3ca7f   nginx:latest   "/docker-entrypoint.…"   2 hours ago     Up 2 hours     80/tcp                              web3
98d61adfb0bd   nginx:latest   "/docker-entrypoint.…"   2 hours ago     Up 2 hours     80/tcp                              web2
2b22ed87b874   nginx:latest   "/docker-entrypoint.…"   2 hours ago     Up 2 hours     80/tcp                              web1
root@dell-precision-7670:/var/lib/docker/volumes# cd 17e0ff685078422080e74a3dc76f834980211ba9dec889a4aa5c6220e78b8f66/
root@dell-precision-7670:/var/lib/docker/volumes/17e0ff685078422080e74a3dc76f834980211ba9dec889a4aa5c6220e78b8f66# ls
_data
root@dell-precision-7670:/var/lib/docker/volumes/17e0ff685078422080e74a3dc76f834980211ba9dec889a4aa5c6220e78b8f66# cd _data/
root@dell-precision-7670:/var/lib/docker/volumes/17e0ff685078422080e74a3dc76f834980211ba9dec889a4aa5c6220e78b8f66/_data# ls
 auto.cnf        binlog.index      client-key.pem       ibdata1         mysql                private_key.pem   sys
 binlog.000001   ca-key.pem       '#ib_16384_0.dblwr'   ibtmp1          mysql.ibd            public_key.pem    tektutor
 binlog.000002   ca.pem           '#ib_16384_1.dblwr'  '#innodb_redo'   mysql.sock           server-cert.pem   undo_001
 binlog.000003   client-cert.pem   ib_buffer_pool      '#innodb_temp'   performance_schema   server-key.pem    undo_002
root@dell-precision-7670:/var/lib/docker/volumes/17e0ff685078422080e74a3dc76f834980211ba9dec889a4aa5c6220e78b8f66/_data# ^C
root@dell-precision-7670:/var/lib/docker/volumes/17e0ff685078422080e74a3dc76f834980211ba9dec889a4aa5c6220e78b8f66/_data# exit
logout
jegan@dell-precision-7670:~/openshift-aug-2022/Day1$ ls -l /tmp/mysql
total 99680
-rw-r----- 1 systemd-coredump systemd-coredump       56 Aug  8 17:44  auto.cnf
-rw-r----- 1 systemd-coredump systemd-coredump  3025278 Aug  8 17:44  binlog.000001
-rw-r----- 1 systemd-coredump systemd-coredump      918 Aug  8 17:46  binlog.000002
-rw-r----- 1 systemd-coredump systemd-coredump      157 Aug  8 17:46  binlog.000003
-rw-r----- 1 systemd-coredump systemd-coredump       48 Aug  8 17:46  binlog.index
-rw------- 1 systemd-coredump systemd-coredump     1680 Aug  8 17:44  ca-key.pem
-rw-r--r-- 1 systemd-coredump systemd-coredump     1112 Aug  8 17:44  ca.pem
-rw-r--r-- 1 systemd-coredump systemd-coredump     1112 Aug  8 17:44  client-cert.pem
-rw------- 1 systemd-coredump systemd-coredump     1680 Aug  8 17:44  client-key.pem
-rw-r----- 1 systemd-coredump systemd-coredump   196608 Aug  8 17:48 '#ib_16384_0.dblwr'
-rw-r----- 1 systemd-coredump systemd-coredump  8585216 Aug  8 17:44 '#ib_16384_1.dblwr'
-rw-r----- 1 systemd-coredump systemd-coredump     5660 Aug  8 17:44  ib_buffer_pool
-rw-r----- 1 systemd-coredump systemd-coredump 12582912 Aug  8 17:46  ibdata1
-rw-r----- 1 systemd-coredump systemd-coredump 12582912 Aug  8 17:46  ibtmp1
drwxr-x--- 2 systemd-coredump systemd-coredump     4096 Aug  8 17:46 '#innodb_redo'
drwxr-x--- 2 systemd-coredump systemd-coredump     4096 Aug  8 17:46 '#innodb_temp'
drwxr-x--- 2 systemd-coredump systemd-coredump     4096 Aug  8 17:44  mysql
-rw-r----- 1 systemd-coredump systemd-coredump 31457280 Aug  8 17:46  mysql.ibd
lrwxrwxrwx 1 systemd-coredump systemd-coredump       27 Aug  8 17:46  mysql.sock -> /var/run/mysqld/mysqld.sock
drwxr-x--- 2 systemd-coredump systemd-coredump     4096 Aug  8 17:44  performance_schema
-rw------- 1 systemd-coredump systemd-coredump     1676 Aug  8 17:44  private_key.pem
-rw-r--r-- 1 systemd-coredump systemd-coredump      452 Aug  8 17:44  public_key.pem
-rw-r--r-- 1 systemd-coredump systemd-coredump     1112 Aug  8 17:44  server-cert.pem
-rw------- 1 systemd-coredump systemd-coredump     1676 Aug  8 17:44  server-key.pem
drwxr-x--- 2 systemd-coredump systemd-coredump     4096 Aug  8 17:44  sys
drwxr-x--- 2 systemd-coredump systemd-coredump     4096 Aug  8 17:45  tektutor
-rw-r----- 1 systemd-coredump systemd-coredump 16777216 Aug  8 17:48  undo_001
-rw-r----- 1 systemd-coredump systemd-coredump 16777216 Aug  8 17:48  undo_002

</pre>
