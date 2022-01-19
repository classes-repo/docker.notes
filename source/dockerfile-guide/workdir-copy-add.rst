文件复制和目录操作
==================

往镜像里复制文件有两种方式，``COPY`` 和 ``ADD``，两者都可以把本地文件复制到镜像里，如果目标目录不存在，则会自动创建。
但 ``ADD`` 比 ``COPY`` 高级一点的地方就是，如果复制的是一个 ``tar.gz`` 等压缩文件时， ``ADD`` 会帮助我们自动去解压缩文件。

COPY
-----------------

index.html

.. code-block:: html

    <h1>
    hello docker
    <h1/>

Dockerfile

.. code-block:: dockerfile

    FROM nginx:alpine
    COPY index.html /usr/share/nginx/html

.. code-block:: bash

    $ ll
    total 16
    -rw-r--r--  1 johnhe  staff    57B  1 17 21:41 Dockerfile
    -rw-r--r--  1 johnhe  staff    24B  1 17 21:37 index.html
    $ docker image build -t dockerfile_copy .
    [+] Building 9.0s (7/7) FINISHED
     => [internal] load build definition from Dockerfile                                                                                                                                                   0.0s
     => => transferring dockerfile: 99B                                                                                                                                                                    0.0s
     => [internal] load .dockerignore                                                                                                                                                                      0.0s
     => => transferring context: 2B                                                                                                                                                                        0.0s
     => [internal] load metadata for docker.io/library/nginx:alpine                                                                                                                                        1.6s
     => [internal] load build context                                                                                                                                                                      0.0s
     => => transferring context: 61B                                                                                                                                                                       0.0s
     => [1/2] FROM docker.io/library/nginx:alpine@sha256:eb05700fe7baa6890b74278e39b66b2ed1326831f9ec3ed4bdc6361a4ac2f333                                                                                  7.2s
     => => resolve docker.io/library/nginx:alpine@sha256:eb05700fe7baa6890b74278e39b66b2ed1326831f9ec3ed4bdc6361a4ac2f333                                                                                  0.0s
     => => sha256:eb05700fe7baa6890b74278e39b66b2ed1326831f9ec3ed4bdc6361a4ac2f333 1.65kB / 1.65kB                                                                                                         0.0s
     => => sha256:e08a7adafd859e875957b027d89dfcbbe8cce7a5525ad88460c23a91febbfdac 8.91kB / 8.91kB                                                                                                         0.0s
     => => sha256:45812000e2a590aee6a5147486e6c0724ae526c7560ed1b37c429ddc578be151 602B / 602B                                                                                                             0.7s
     => => sha256:c2723ca2deddabe85020b61946d6a143b3f661b0f3a2092ccb9d32837877ae13 1.57kB / 1.57kB                                                                                                         0.0s
     => => sha256:9b3977197b4f2147bdd31e1271f811319dcd5c2fc595f14e81f5351ab6275b99 2.72MB / 2.72MB                                                                                                         1.4s
     => => sha256:11e00b6b0b40aaa8729e7f541235821bac980d36becf1206d92be51fc4446ad7 7.25MB / 7.25MB                                                                                                         6.7s
     => => sha256:2e3e03d70957cbfd7b9fefa47a4c5064a9aad7b9c3a56376ef2642a367c4fa63 895B / 895B                                                                                                             1.0s
     => => sha256:bb56ce0340f07d3b22628c285ab10577273e2d06b7ff7ab2df9d1319c2c8053e 668B / 668B                                                                                                             1.4s
     => => extracting sha256:9b3977197b4f2147bdd31e1271f811319dcd5c2fc595f14e81f5351ab6275b99                                                                                                              0.1s
     => => sha256:a313facfd18da1644e1d4a4d3691d27481ca47ee3bddeacc8ecc4b8e947dfd24 1.40kB / 1.40kB                                                                                                         1.7s
     => => extracting sha256:11e00b6b0b40aaa8729e7f541235821bac980d36becf1206d92be51fc4446ad7                                                                                                              0.2s
     => => extracting sha256:45812000e2a590aee6a5147486e6c0724ae526c7560ed1b37c429ddc578be151                                                                                                              0.0s
     => => extracting sha256:2e3e03d70957cbfd7b9fefa47a4c5064a9aad7b9c3a56376ef2642a367c4fa63                                                                                                              0.0s
     => => extracting sha256:bb56ce0340f07d3b22628c285ab10577273e2d06b7ff7ab2df9d1319c2c8053e                                                                                                              0.0s
     => => extracting sha256:a313facfd18da1644e1d4a4d3691d27481ca47ee3bddeacc8ecc4b8e947dfd24                                                                                                              0.0s
     => [2/2] COPY index.html /usr/share/nginx/html/                                                                                                                                                       0.1s
    FROM nginx:alpine
     => exporting to image                                                                                                                                                                                 0.0s
     => => exporting layers                                                                                                                                                                                0.0s
     => => writing image sha256:ffac89dfb72074a47ba7b40d6e3e9e90fce2519f4a2f47af0b7462c6ec148f59                                                                                                           0.0s
     => => naming to docker.io/library/dockerfile_copy                                                                                                                                                     0.0s
    $ docker image ls
    REPOSITORY                                                        TAG               IMAGE ID       CREATED         SIZE
    dockerfile_copy                                                   latest            ffac89dfb720   7 seconds ago   22.1MB
    commit-image                                                      latest            e2cb9394f34f   5 hours ago     134MB
    phptemp                                                           latest            4e8744da8bbd   20 hours ago    411MB
    phpstorm_helpers                                                  PS-212.5712.51    52009cf10d7b   3 days ago      1.56MB
    nginx                                                             latest            eeb9db34b331   2 weeks ago     134MB
    registry.cn-beijing.aliyuncs.com/yupao-base/hyperf-debian-php74   dev               3a7274e2d255   4 weeks ago     641MB
    busybox                                                           latest            b34806a1af7a   5 weeks ago     1.41MB
    classes/nginx                                                     1.21-alpine       59f53e4a8b9f   6 weeks ago     22MB
    classes/php                                                       7.1-fpm           3a8daea4f41e   6 weeks ago     525MB
    classes/hyperf                                                    latest            251a84f0f2fd   7 weeks ago     113MB
    moby/buildkit                                                     buildx-stable-1   cb9b18fdb708   2 months ago    134MB
    ubuntu                                                            latest            d5ca7a445605   3 months ago    65.6MB
    $ docker container run -it dockerfile_copy sh
    / # cd /usr/share/nginx/html/
    /usr/share/nginx/html # ls
    50x.html    index.html
    /usr/share/nginx/html # cat index.html
    <h1>
    hello docker
    <h1/>


ADD
-----------------

index.html

.. code-block:: html

    <h1>
    hello docker
    <h1/>

Dockerfile

.. code-block:: dockerfile

    FROM nginx:alpine
    ADD index.html.tar.gz /usr/share/nginx/html

.. code-block:: bash

    $ ls
    Dockerfile        index.html        index.html.tar.gz
    $ rm -rf index.html
    $ docker image build -t dockerfile_add .
    [+] Building 15.6s (7/7) FINISHED
     => [internal] load build definition from Dockerfile                                                                                                                                                   0.0s
     => => transferring dockerfile: 105B                                                                                                                                                                   0.0s
     => [internal] load .dockerignore                                                                                                                                                                      0.0s
     => => transferring context: 2B                                                                                                                                                                        0.0s
     => [internal] load metadata for docker.io/library/nginx:alpine                                                                                                                                       15.4s
     => [internal] load build context                                                                                                                                                                      0.0s
     => => transferring context: 190B                                                                                                                                                                      0.0s
    FROM nginx:alpine
    WORKDIR /usr/share/nginx/html/
     => CACHED [1/2] FROM docker.io/library/nginx:alpine@sha256:eb05700fe7baa6890b74278e39b66b2ed1326831f9ec3ed4bdc6361a4ac2f333                                                                           0.0s
    FROM nginx:alpine
     => [2/2] ADD index.html.tar.gz /usr/share/nginx/html/                                                                                                                                                 0.1s
     => exporting to image                                                                                                                                                                                 0.0s
     => => exporting layers                                                                                                                                                                                0.0s
     => => writing image sha256:30fa94d1335e6da4c36f72ff94a68cbe4c63e3fb7a0b62eb2ce4b485faf1b4a4                                                                                                           0.0s
     => => naming to docker.io/library/dockerfile_add                                                                                                                                                      0.0s
    $ docker image ls
    REPOSITORY                                                        TAG               IMAGE ID       CREATED         SIZE
    dockerfile_add                                                    latest            30fa94d1335e   9 seconds ago   22.1MB
    dockerfile_copy                                                   latest            ffac89dfb720   8 minutes ago   22.1MB
    commit-image                                                      latest            e2cb9394f34f   5 hours ago     134MB
    phptemp                                                           latest            4e8744da8bbd   20 hours ago    411MB
    phpstorm_helpers                                                  PS-212.5712.51    52009cf10d7b   3 days ago      1.56MB
    nginx                                                             latest            eeb9db34b331   2 weeks ago     134MB
    registry.cn-beijing.aliyuncs.com/yupao-base/hyperf-debian-php74   dev               3a7274e2d255   4 weeks ago     641MB
    busybox                                                           latest            b34806a1af7a   5 weeks ago     1.41MB
    classes/nginx                                                     1.21-alpine       59f53e4a8b9f   6 weeks ago     22MB
    classes/php                                                       7.1-fpm           3a8daea4f41e   6 weeks ago     525MB
    classes/hyperf                                                    latest            251a84f0f2fd   7 weeks ago     113MB
    moby/buildkit                                                     buildx-stable-1   cb9b18fdb708   2 months ago    134MB
    ubuntu                                                            latest            d5ca7a445605   3 months ago    65.6MB
    $ docker container run -it dockerfile_add sh
    / # cd /usr/share/nginx/html/
    /usr/share/nginx/html # ls
    50x.html    index.html
    /usr/share/nginx/html # cat index.html
    <h1>
    hello docker
    <h1/>

.. note::
   因此在 ``COPY`` 和 ``ADD`` 指令中选择的时候，可以遵循这样的原则，所有的文件复制均使用 ``COPY`` 指令，仅在需要自动解压缩的场合使用 ``ADD``

WORKDIR
-----------------

``WORKDIR`` 用于切换操作目录，表示后面的操作都是基于切换后的目录进行

Dockerfile

.. code-block:: dockerfile

    FROM nginx:alpine
    WORKDIR /usr/share/nginx/html
    ADD index.html.tar.gz ./

.. code-block:: bash

    $ docker image build -t dockerfile_workdir .
    [+] Building 15.6s (8/8) FINISHED
     => [internal] load build definition from Dockerfile                                                                                                                                                   0.0s
     => => transferring dockerfile: 116B                                                                                                                                                                   0.0s
     => [internal] load .dockerignore                                                                                                                                                                      0.0s
     => => transferring context: 2B                                                                                                                                                                        0.0s
     => [internal] load metadata for docker.io/library/nginx:alpine                                                                                                                                       15.4s
     => [internal] load build context                                                                                                                                                                      0.0s
     => => transferring context: 39B                                                                                                                                                                       0.0s
     => [1/3] FROM docker.io/library/nginx:alpine@sha256:eb05700fe7baa6890b74278e39b66b2ed1326831f9ec3ed4bdc6361a4ac2f333                                                                                  0.0s
     => CACHED [2/3] WORKDIR /usr/share/nginx/html/                                                                                                                                                        0.0s
     => [3/3] ADD index.html.tar.gz ./                                                                                                                                                                     0.1s
     => exporting to image                                                                                                                                                                                 0.0s
     => => exporting layers                                                                                                                                                                                0.0s
     => => writing image sha256:ecd42c0f5fa848959a18eba86beb85b40eaf67f2e455811add359808d62b6c1e                                                                                                           0.0s
     => => naming to docker.io/library/dockerfile_workdir                                                                                                                                                  0.0s
    $ docker image ls
    REPOSITORY                                                        TAG               IMAGE ID       CREATED              SIZE
    dockerfile_workdir                                                latest            ecd42c0f5fa8   About a minute ago   22.1MB
    dockerfile_add                                                    latest            30fa94d1335e   10 minutes ago       22.1MB
    dockerfile_copy                                                   latest            ffac89dfb720   18 minutes ago       22.1MB
    commit-image                                                      latest            e2cb9394f34f   6 hours ago          134MB
    phptemp                                                           latest            4e8744da8bbd   20 hours ago         411MB
    phpstorm_helpers                                                  PS-212.5712.51    52009cf10d7b   3 days ago           1.56MB
    nginx                                                             latest            eeb9db34b331   2 weeks ago          134MB
    registry.cn-beijing.aliyuncs.com/yupao-base/hyperf-debian-php74   dev               3a7274e2d255   4 weeks ago          641MB
    busybox                                                           latest            b34806a1af7a   5 weeks ago          1.41MB
    classes/nginx                                                     1.21-alpine       59f53e4a8b9f   6 weeks ago          22MB
    classes/php                                                       7.1-fpm           3a8daea4f41e   6 weeks ago          525MB
    classes/hyperf                                                    latest            251a84f0f2fd   7 weeks ago          113MB
    moby/buildkit                                                     buildx-stable-1   cb9b18fdb708   2 months ago         134MB
    ubuntu                                                            latest            d5ca7a445605   3 months ago         65.6MB
    $ docker container run -it dockerfile_workdir sh
    /usr/share/nginx/html # ls
    50x.html    index.html
    /usr/share/nginx/html # cat index.html
    <h1>
    hello docker
    <h1/>
    $ docker image history dockerfile_workdir
    IMAGE          CREATED          CREATED BY                                      SIZE      COMMENT
    ecd42c0f5fa8   8 minutes ago    ADD index.html.tar.gz ./ # buildkit             24B       buildkit.dockerfile.v0
    <missing>      10 minutes ago   WORKDIR /usr/share/nginx/html/                  0B        buildkit.dockerfile.v0
    <missing>      2 weeks ago      /bin/sh -c #(nop)  CMD ["nginx" "-g" "daemon…   0B
    <missing>      2 weeks ago      /bin/sh -c #(nop)  STOPSIGNAL SIGQUIT           0B
    <missing>      2 weeks ago      /bin/sh -c #(nop)  EXPOSE 80                    0B
    <missing>      2 weeks ago      /bin/sh -c #(nop)  ENTRYPOINT ["/docker-entr…   0B
    <missing>      2 weeks ago      /bin/sh -c #(nop) COPY file:09a214a3e07c919a…   4.61kB
    <missing>      2 weeks ago      /bin/sh -c #(nop) COPY file:0fd5fca330dcd6a7…   1.04kB
    <missing>      2 weeks ago      /bin/sh -c #(nop) COPY file:0b866ff3fc1ef5b0…   1.96kB
    <missing>      2 weeks ago      /bin/sh -c #(nop) COPY file:65504f71f5855ca0…   1.2kB
    <missing>      2 weeks ago      /bin/sh -c set -x     && addgroup -g 101 -S …   16.7MB
    <missing>      2 weeks ago      /bin/sh -c #(nop)  ENV PKG_RELEASE=1            0B
    <missing>      2 weeks ago      /bin/sh -c #(nop)  ENV NJS_VERSION=0.7.1        0B
    <missing>      2 weeks ago      /bin/sh -c #(nop)  ENV NGINX_VERSION=1.21.5     0B
    <missing>      2 weeks ago      /bin/sh -c #(nop)  LABEL maintainer=NGINX Do…   0B
    <missing>      7 weeks ago      /bin/sh -c #(nop)  CMD ["/bin/sh"]              0B
    <missing>      7 weeks ago      /bin/sh -c #(nop) ADD file:df538113122843069…   5.33MB