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
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>

</pre>
