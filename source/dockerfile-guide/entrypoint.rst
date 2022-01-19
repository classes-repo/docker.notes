容器启动命令 ENTRYPOINT
=========================


``ENTRYPOINT`` 也可以设置容器启动时要执行的命令，但是和 ``CMD`` 是有区别的

- ``CMD`` 设置的命令，可以在 ``docker container run`` 时传入其它命令，覆盖掉 ``CMD`` 的命令，但是 ``ENTRYPOINT`` 所设置的命令是一定会被执行的
- ``ENTRYPOINT`` 和 ``CMD`` 可以联合使用，``ENTRYPOINT`` 设置执行的命令，``CMD`` 传递参数

准备三个 ``Dockerfile`` 分别构建三个镜像 ``demo-cmd`` 、 ``demo-entrypoint`` 和 ``demo-both``

.. code-block:: Dockerfile

    FROM ubuntu:latest
    CMD ["echo", "hello docker"]

.. code-block:: Dockerfile

    FROM ubuntu:latest
    ENTRYPOINT ["echo", "hello docker"]

.. code-block:: Dockerfile

    FROM ubuntu:latest
    ENTRYPOINT ["echo"]
    CMD []

.. code-block:: bash

    $ docker image ls
    REPOSITORY                                                        TAG                    IMAGE ID       CREATED        SIZE
    demo-cmd                                                          latest                 0088ab49beec   3 months ago   65.6MB
    demo-both                                                         latest                 b5cb092c67ea   3 months ago   65.6MB

CMD
____________________


对于 ``demo-cmd`` 的镜像，如果执行创建容器，不指定运行时的命令，则会默认执行 ``CMD`` 所定义的命令，打印出 ``hello docker``

.. code-block:: bash

    $ docker container run -it --rm demo-cmd
    hello docker

当 ``docker container run`` 的时候指定命令，则该命令会覆盖掉 ``CMD`` 的命令，如：

.. code-block:: bash

    $ docker container run -it --rm demo-cmd echo "hello world"
    hello world

ENTRYPOINT
____________________

但是 ``ENTRYPOINT`` 所定义的命令则无法覆盖，一定会执行

.. code-block:: bash

    $ docker container run -it --rm demo-entrypoint
    hello docker
    $ docker container run -it --rm demo-entrypoint echo "hello world"
    hello docker echo hello world

ENTRYPOINT & CMD
____________________

.. code-block:: bash

    $ docker run -it --rm demo-both

    $ docker run -it --rm demo-both hello docker
    hello docker
    $ docker run -it --rm demo-both hello everyone
    hello everyone
