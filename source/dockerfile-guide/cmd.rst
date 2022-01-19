容器启动命令 CMD
==================

``CMD`` 可以用来设置容器启动时默认会执行的命令

- 容器启动时默认执行的命令
- 如果 ``docker container run`` 启动容器时指定了其它命令，则 ``CMD`` 命令会被忽略
- 如果定义了多个 ``CMD`` ，只有最后一个会被执行

默认进入 ``shell`` 是因为 ``busybox`` 镜像里面有定义 ``CMD``

.. code-block:: Dockerfile

    $ docker container run --rm -it busybox
    / # ls
    bin   dev   etc   home  proc  root  sys   tmp   usr   var
    / #
    / # exit
    $ docker image history busybox
    IMAGE          CREATED       CREATED BY                                      SIZE      COMMENT
    b34806a1af7a   5 weeks ago   /bin/sh -c #(nop)  CMD ["sh"]                   0B
    <missing>      5 weeks ago   /bin/sh -c #(nop) ADD file:c59658f01bda35a59…   1.41MB
     $

在 ``docker container run`` 的时候指定执行命令 ``ip a``，此时将覆盖默认执行的命令

.. code-block:: bash

     $ docker container run --rm -it busybox ip a
    1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue qlen 1000
        link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
        inet 127.0.0.1/8 scope host lo
           valid_lft forever preferred_lft forever
    2: tunl0@NONE: <NOARP> mtu 1480 qdisc noop qlen 1000
        link/ipip 0.0.0.0 brd 0.0.0.0
    3: ip6tnl0@NONE: <NOARP> mtu 1452 qdisc noop qlen 1000
        link/tunnel6 00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00 brd 00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00
    371: eth0@if372: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue
        link/ether 02:42:ac:6e:00:03 brd ff:ff:ff:ff:ff:ff
        inet 172.110.0.3/16 brd 172.110.255.255 scope global eth0
           valid_lft forever preferred_lft forever
     $

如果定义了多个 ``CMD`` ，只有最后一个会被执行

Dockerfile.busybox

.. code-block:: dockerfile

    FROM busybox:latest
    CMD ["echo","hello busybox!"]

.. code-block:: bash

    $ docker image build -t busybox.cmd -f Dockerfile.busybox .
    [+] Building 0.1s (5/5) FINISHED
     => [internal] load build definition from Dockerfile.busybox                                                                                                                                           0.0s
     => => transferring dockerfile: 100B                                                                                                                                                                   0.0s
     => [internal] load .dockerignore                                                                                                                                                                      0.0s
     => => transferring context: 2B                                                                                                                                                                        0.0s
     => [internal] load metadata for docker.io/library/busybox:latest                                                                                                                                      0.0s
     => [1/1] FROM docker.io/library/busybox:latest                                                                                                                                                        0.0s
     => exporting to image                                                                                                                                                                                 0.0s
     => => exporting layers                                                                                                                                                                                0.0s
     => => writing image sha256:d0952b19e4b0a48202d3788118830058763f6b6abbba58d2b2b7041bb9141e75                                                                                                           0.0s
     => => naming to docker.io/library/busybox.cmd
    $ docker image history busybox.cmd
    IMAGE          CREATED       CREATED BY                                      SIZE      COMMENT
    d0952b19e4b0   5 weeks ago   CMD ["echo" "hello busybox!"]                   0B        buildkit.dockerfile.v0
    <missing>      5 weeks ago   /bin/sh -c #(nop)  CMD ["sh"]                   0B
    <missing>      5 weeks ago   /bin/sh -c #(nop) ADD file:c59658f01bda35a59…   1.41MB
    $
    $ docker container run --rm -it busybox.cmd
    hello busybox!
