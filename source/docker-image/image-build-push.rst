docker build
====================

说明 [#f0]_
---------------------

.. code-block:: bash

    docker build [OPTIONS] PATH | URL | -


该命令主要用于从 ``dockerfile`` 来构建镜像，``dockerfile`` 可以来自本地文件路径、远程资源和标准输出

范例
---------------------

Build with PATH
****************

.. code-block:: bash

    $ ls
    Dockerfile
    $ docker build .
    [+] Building 0.3s (6/6) FINISHED
     => [internal] load build definition from Dockerfile                                                                                                                                                   0.0s
     => => transferring dockerfile: 119B                                                                                                                                                                   0.0s
     => [internal] load .dockerignore                                                                                                                                                                      0.0s
     => => transferring context: 2B                                                                                                                                                                        0.0s
     => [internal] load metadata for docker.io/library/nginx:latest                                                                                                                                        0.0s
     => [1/2] FROM docker.io/library/nginx:latest                                                                                                                                                          0.0s
     => [2/2] RUN echo "hello docker" > /usr/share/nginx/html/index.html                                                                                                                                   0.2s
     => exporting to image                                                                                                                                                                                 0.0s
     => => exporting layers                                                                                                                                                                                0.0s
     => => writing image sha256:4ef00d7a9f8970353482652c945eab18e72920527a1dabfae03ca7bce7b7173d                                                                                                           0.0s
    $ docker image ls
    REPOSITORY                                                        TAG               IMAGE ID       CREATED          SIZE
    <none>                                                            <none>            4ef00d7a9f89   25 seconds ago   134MB

Build with URL
****************

.. code-block:: bash

    docker build github.com/creack/docker-firefox

Build with -
****************

.. code-block:: bash

    docker build - < Dockerfile

.. code-block:: bash

    docker build - < context.tar.gz

参考资料
--------

.. [#f0] https://docs.docker.com/engine/reference/builder/#usage