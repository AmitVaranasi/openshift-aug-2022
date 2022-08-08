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


## Docker Overview

- Docker comes two flavours
  1. Docker Community Edition - Docker CE ( OpenSource )
  2. Docker Enterprise Edition - Docker EE ( Licensed Software )
  
