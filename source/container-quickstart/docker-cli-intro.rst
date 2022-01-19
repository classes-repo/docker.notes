Docker CLI 命令行介绍
=======================


Docker Version
------------------

Windows (Intel芯片)

.. code-block:: bash

    $ docker version
    Client: Docker Engine - Community
    Cloud integration: 1.0.12
    Version:           20.10.5
    API version:       1.41
    Go version:        go1.13.15
    Git commit:        55c4c88
    Built:             Tue Mar  2 20:14:53 2021
    OS/Arch:           windows/amd64
    Context:           default
    Experimental:      true

    Server: Docker Engine - Community
    Engine:
    Version:          20.10.5
    API version:      1.41 (minimum version 1.12)
    Go version:       go1.13.15
    Git commit:       363e9a8
    Built:            Tue Mar  2 20:15:47 2021
    OS/Arch:          linux/amd64
    Experimental:     false
    containerd:
    Version:          1.4.4
    GitCommit:        05f951a3781f4f2c1911b05e61c160e9c30eaa8e
    runc:
    Version:          1.0.0-rc93
    GitCommit:        12644e614e25b05da6fd08a38ffa0cfe1903fdec
    docker-init:
    Version:          0.19.0
    GitCommit:        de40ad0

Linux（Intel芯片）

.. code-block:: bash

    ￥ docker version
    Client: Docker Engine - Community
    Version:           20.10.0
    API version:       1.41
    Go version:        go1.13.15
    Git commit:        7287ab3
    Built:             Tue Dec  8 18:59:40 2020
    OS/Arch:           linux/amd64
    Context:           default
    Experimental:      true

    Server: Docker Engine - Community
    Engine:
    Version:          20.10.0
    API version:      1.41 (minimum version 1.12)
    Go version:       go1.13.15
    Git commit:       eeddea2
    Built:            Tue Dec  8 18:57:45 2020
    OS/Arch:          linux/amd64
    Experimental:     false
    containerd:
    Version:          1.4.3
    GitCommit:        269548fa27e0089a8b8278fc4fc781d7f65a939b
    runc:
    Version:          1.0.0-rc92
    GitCommit:        ff819c7e9184c13b7c2607fe6c30ae19403a7aff
    docker-init:
    Version:          0.19.0
    GitCommit:        de40ad0

Mac with Intel chip

.. code-block:: bash

    $ docker version
    Client: Docker Engine - Community
    Cloud integration: 1.0.9
    Version: 20.10.5
    API version: 1.41
    Go version: go1.13.15
    Git commit: 55c4c88
    Built: Tue Mar 2 20:13:00 2021
    OS/Arch: darwin/amd64
    Context: default
    Experimental: true

    Server: Docker Engine - Community
    Engine:
    Version: 20.10.5
    API version: 1.41 (minimum version 1.12)
    Go version: go1.13.15
    Git commit: 363e9a8
    Built: Tue Mar 2 20:15:47 2021
    OS/Arch: linux/amd64
    Experimental: false
    containerd:
    Version: 1.4.3
    GitCommit: 269548fa27e0089a8b8278fc4fc781d7f65a939b
    runc:
    Version: 1.0.0-rc92
    GitCommit: ff819c7e9184c13b7c2607fe6c30ae19403a7aff
    docker-init:
    Version: 0.19.0
    GitCommit: de40ad0

Mac with Apple silicon

.. code-block:: bash


     $ docker version
      Client:
       Cloud integration: v1.0.20
       Version:           20.10.10
       API version:       1.41
       Go version:        go1.16.9
       Git commit:        b485636
       Built:             Mon Oct 25 07:43:15 2021
       OS/Arch:           darwin/arm64
       Context:           default
       Experimental:      true

      Server: Docker Engine - Community
       Engine:
        Version:          20.10.10
        API version:      1.41 (minimum version 1.12)
        Go version:       go1.16.9
        Git commit:       e2f740d
        Built:            Mon Oct 25 07:41:10 2021
        OS/Arch:          linux/arm64
        Experimental:     false
       containerd:
        Version:          1.4.11
        GitCommit:        5b46e404f6b9f661a205e28d59c982d3634148f8
       runc:
        Version:          1.0.2
        GitCommit:        v1.0.2-0-g52b36a2
       docker-init:
        Version:          0.19.0
        GitCommit:        de40ad0

Docker Info
------------------

.. code-block:: bash

      $ docker info
      Client:
       Context:    default
       Debug Mode: false
       Plugins:
        buildx: Build with BuildKit (Docker Inc., v0.6.3)
        compose: Docker Compose (Docker Inc., v2.1.1)
        scan: Docker Scan (Docker Inc., 0.9.0)

      Server:
       Containers: 11
        Running: 7
        Paused: 0
        Stopped: 4
       Images: 12
       Server Version: 20.10.10
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
       Runtimes: io.containerd.runc.v2 io.containerd.runtime.v1.linux runc
       Default Runtime: runc
       Init Binary: docker-init
       containerd version: 5b46e404f6b9f661a205e28d59c982d3634148f8
       runc version: v1.0.2-0-g52b36a2
       init version: de40ad0
       Security Options:
        seccomp
         Profile: default
       Kernel Version: 5.10.47-linuxkit
       Operating System: Docker Desktop
       OSType: linux
       Architecture: aarch64
       CPUs: 4
       Total Memory: 1.942GiB
       Name: docker-desktop
       ID: O7QY:WXNI:DML7:ETYQ:XRSN:NUYN:735O:BOKY:VFXH:FRNY:PISD:KWZK
       Docker Root Dir: /var/lib/docker
       Debug Mode: false
       HTTP Proxy: http.docker.internal:3128
       HTTPS Proxy: http.docker.internal:3128
       Registry: https://index.docker.io/v1/
       Labels:
       Experimental: false
       Insecure Registries:
        127.0.0.0/8
       Registry Mirrors:
        https://6vmzhah3.mirror.aliyuncs.com/
        https://hub-mirror.c.163.com/
        https://mirror.baidubce.com/
       Live Restore Enabled: false

docker命令行的基本使用
-----------------------------

docker + 管理的对象（比如容器，镜像） + 具体操作（比如创建，启动，停止，删除）

例如

- ``docker image pull nginx`` 拉取一个叫nginx的docker image镜像
- ``docker container stop web`` 停止一个叫web的docker container容器

