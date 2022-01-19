使用 buildx 构建多架构镜像
============================

Windows和Mac的桌面版Docker自带buildx命令，但是Linux环境下的Docker需要自行安装buildx （https://github.com/docker/buildx）

https://docs.docker.com/buildx/working-with-buildx/


登录dockerhub

.. code-block:: bash

    docker login


Dockerfile

.. code-block:: Dockerfile

    FROM ubuntu:latest
    CMD ["echo","hello docker!"]


构建

.. code-block:: bash

    $ docker buildx ls
    NAME/NODE       DRIVER/ENDPOINT STATUS  PLATFORMS
    desktop-linux   docker
      desktop-linux desktop-linux   running linux/arm64, linux/amd64, linux/riscv64, linux/ppc64le, linux/s390x, linux/386, linux/arm/v7, linux/arm/v6
    default *       docker
      default       default         running linux/arm64, linux/amd64, linux/riscv64, linux/ppc64le, linux/s390x, linux/386, linux/arm/v7, linux/arm/v6
    $ docker buildx create --name mybuilder --use
    mybuilder
    $ docker buildx ls
    NAME/NODE       DRIVER/ENDPOINT             STATUS   PLATFORMS
    mybuilder *     docker-container
      mybuilder0    unix:///var/run/docker.sock inactive
    desktop-linux   docker
      desktop-linux desktop-linux               running  linux/arm64, linux/amd64, linux/riscv64, linux/ppc64le, linux/s390x, linux/386, linux/arm/v7, linux/arm/v6
    default         docker
      default       default                     running  linux/arm64, linux/amd64, linux/riscv64, linux/ppc64le, linux/s390x, linux/386, linux/arm/v7, linux/arm/v6
    $ docker buildx build -t classes/test --platform linux/arm64,linux/amd64 --push .
    [+] Building 10.5s (12/12) FINISHED                                                                                                                                         
     => [internal] load build definition from Dockerfile                                                                                                                   0.0s
     => => transferring dockerfile: 215B                                                                                                                                   0.0s
     => [internal] load .dockerignore                                                                                                                                      0.0s
     => => transferring context: 2B                                                                                                                                        0.0s
     => [linux/amd64 internal] load metadata for docker.io/library/ubuntu:latest                                                                                           4.7s
     => [linux/arm64 internal] load metadata for docker.io/library/ubuntu:latest                                                                                           4.9s
     => [auth] library/ubuntu:pull token for registry-1.docker.io                                                                                                          0.0s
     => [auth] library/ubuntu:pull token for registry-1.docker.io                                                                                                          0.0s
     => [linux/amd64 1/1] FROM docker.io/library/ubuntu:latest@sha256:b5a61709a9a44284d88fb12e5c48db0409cfad5b69d4ff8224077c57302df9cf                                     0.0s
     => => resolve docker.io/library/ubuntu:latest@sha256:b5a61709a9a44284d88fb12e5c48db0409cfad5b69d4ff8224077c57302df9cf                                                 0.0s
     => [linux/arm64 1/1] FROM docker.io/library/ubuntu:latest@sha256:b5a61709a9a44284d88fb12e5c48db0409cfad5b69d4ff8224077c57302df9cf                                     0.0s
     => => resolve docker.io/library/ubuntu:latest@sha256:b5a61709a9a44284d88fb12e5c48db0409cfad5b69d4ff8224077c57302df9cf                                                 0.0s
     => exporting to image                                                                                                                                                 5.4s
     => => exporting layers                                                                                                                                                0.0s
     => => exporting manifest sha256:2e36872f7d5ae10593df1901bb63387ceee2f2ccbbe033173a6c47966cc7a81c                                                                      0.0s
     => => exporting config sha256:5c5af3b69f5e95672788c7caebe27a252cb4a7048249b6d07226dae7de6e2d5a                                                                        0.0s
     => => exporting manifest sha256:fd2a393219840b78c7bd3c6a7dc5a014a0555bc0206aeb0e9b2c5092e024ffca                                                                      0.0s
     => => exporting config sha256:a8180ae2c2e6c789cf162b607c32487178dd35e618c83d7a46cd581030f61a16                                                                        0.0s
     => => exporting manifest list sha256:f6bc67ac5962d016f8cc86c2f933543892a71e04a29bf3373fc2e42ad85519e8                                                                 0.0s
     => => pushing layers                                                                                                                                                  2.9s
     => => pushing manifest for docker.io/classes/test:latest@sha256:f6bc67ac5962d016f8cc86c2f933543892a71e04a29bf3373fc2e42ad85519e8                                      2.5s
     => [auth] classes/test:pull,push token for registry-1.docker.io                                                                                                       0.0s
     => [auth] classes/test:pull,push token for registry-1.docker.io                                                                                                       0.0s
     => [auth] classes/test:pull,push library/ubuntu:pull token for registry-1.docker.io                                                                                   0.0s
