[Docker tutorial for implementation](https://docs.docker.com/get-started/02_our_app/)
[How Docker containers work](https://docs.microsoft.com/en-us/learn/modules/intro-to-docker-containers/4-how-docker-containers-work)
![](https://i.imgur.com/dhpRPro.png)







## Storage configuration
- when the app in a container needs to store data
    - always consider containers as temporary
    - Container make use of two options to persist data
        1. **Volume (official recommend)**
        2. bind mounts: 隨機找尋一個空間進行儲存 (不會特別針對這塊進行優化)
        3. tmpfs mount: 暫時寫在memory
        
![](https://i.imgur.com/UdmAPtM.png)

### Volume
- **stored on the host filesystem** at a specific folder location (volume data isn't meant to be updated by the host)
    - choose a folder that the data isn't going to be modified by non-Docker processes
    - **```docker volume create```**: create volumes as part of the container creation process. Docker will create the volume if it doesn't exist when you try to mount the volume into a container the first time
    - Multiple containers can simultaneously use the same volumes. Volume don't get removed automatically when a container stops using the volume.

### Bind mounts
- conceptually the same as a volume, however, instead of using a specific folder, you can mount any file or folder on the host.
- **updated by the host and used by both the container and host**
- Although Bind mounts are more performant, volume are considered the preferred data storage strategy


## Network configuration
- Docker provides three pre-configured network configurations
    - **Bridge**: **default configuration** applied to containers when launched without specifying any additional network configuration (internal & private, also isolates the container network from the Docker host network)
    - **Host**: enable you to run the container on the host network directly. This configuration effectively removes the isolation between the host and the container at a network level. (**Container can only use ports not already used by the host**)
    - **none**: to disable networking for containers, use the none network option
- **Host network configuration isn't supported for both Windows and macOS desktops**

### Bridge
- Each container in the bridge network is assigned an IP address and subnet mask (主機名稱預設為container名稱)
- Containers connected to the default bridge network are allowed to access other bridge connected containers by IP address. The bridge network doesn't allow communication between containers using hostnames.
- Defualt: docker doesn't publish any container ports. You should mapping between the container ports and the Docker hos ports
```shell=
# 用主機上 8080 IP mapping 到 client browsing port 80
--publish 8080:80
```


## Benefit to use Docker containers

- Developers can focus on developing software and the operations team on the deployment and management of the software.
- Containers are ideal candidates for continuous integration and speed up the time from build to production
- Cloud deployments: deploy Docker containers to Azure Container Instances, Azure App Service, and Azure Kubernetes

## When not to use Docker containers
### Security and virtualization
- Containers provide a level of isolation. However, containers share a single host OS kernel, which can be a single point of attack. 
- Considering security aspects, we need to take configure such as storage and networks into account. For example, all containers will use the bridge network by default and can access each other via IP address. In such case, VM is more suitable.

### Service monitoring
- Managing the applications and containers are more complicated that traditional VM deployments. More detailed information about  services inside the container is harder to monitor.
- ```docker stats``` return information for the container such as percentage CPU usage, memory usage, I/O written to dist, network data (only for data streaming). However, no aggreggation is done as the data isn't stored.