镜像的导出和导入 (offline)
==========================

导出镜像
-------

命令： ``docker image save <image-name> -o <file-name>``

示例：

.. code-block:: bash

    $ docker image ls
    REPOSITORY                                                        TAG               IMAGE ID       CREATED        SIZE
    phpstorm_helpers                                                  PS-212.5712.51    52009cf10d7b   2 days ago     1.56MB
    nginx                                                             latest            eeb9db34b331   2 weeks ago    134MB
    registry.cn-beijing.aliyuncs.com/yupao-base/hyperf-debian-php74   dev               3a7274e2d255   4 weeks ago    641MB
    busybox                                                           latest            b34806a1af7a   5 weeks ago    1.41MB
    classes/nginx                                                     1.21-alpine       59f53e4a8b9f   6 weeks ago    22MB
    classes/php                                                       7.1-fpm           3a8daea4f41e   6 weeks ago    525MB
    classes/hyperf                                                    latest            251a84f0f2fd   6 weeks ago    113MB
    moby/buildkit                                                     buildx-stable-1   cb9b18fdb708   8 weeks ago    134MB
    ubuntu                                                            latest            d5ca7a445605   3 months ago   65.6MB
    $ docker image save nginx:latest -o nginx.bak
    $ ll
    total 286880
    drwxr-xr-x  10 johnhe  staff        320  1 16 21:04 ./
    drwxr-xr-x   8 johnhe  staff        256  1 16 13:08 ../
    -rw-r--r--   1 johnhe  staff         13  1 16 00:10 .gitignore
    drwxr-xr-x   6 johnhe  staff        192  1 16 17:11 .idea/
    -rw-r--r--   1 johnhe  staff        638  1 16 00:49 Makefile
    drwxr-xr-x   5 johnhe  staff        160  1 16 00:51 build/
    -rw-r--r--   1 johnhe  staff        804  1 16 00:49 make.bat
    -rw-------   1 johnhe  staff  138865152  1 16 21:04 nginx.bak
    -rw-r--r--   1 johnhe  staff        641  1 16 00:10 requirements.txt
    drwxr-xr-x  12 johnhe  staff        384  1 16 15:45 source/


导入镜像
-------

命令： ``docker image load -i <file-name>``


.. code-block:: bash

    $ docker container ls
    CONTAINER ID   IMAGE                       COMMAND                  CREATED       STATUS        PORTS                                      NAMES
    32e273c0de17   nginx                       "/docker-entrypoint.…"   6 hours ago   Up 6 hours    80/tcp                                     fervent_robinson
    a42f90b43fd8   classes/nginx:1.21-alpine   "/docker-entrypoint.…"   3 days ago    Up 19 hours   0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp   nginx121
    9e0ae9623c69   classes/hyperf              "/bin/sh"                3 weeks ago   Up 2 days     0.0.0.0:9513->9513/tcp                     member-private
    33fbc40bef50   classes/hyperf              "/bin/sh"                4 weeks ago   Up 3 weeks    0.0.0.0:9505->9505/tcp                     hyperf-job_commom
    c8403acb95c5   classes/hyperf              "/bin/sh"                4 weeks ago   Up 11 days    0.0.0.0:9504->9504/tcp                     hyperf-job-business
    61d23490f60d   classes/hyperf              "/bin/sh"                4 weeks ago   Up 3 weeks    0.0.0.0:9511->9511/tcp                     hyperf-joblist
    9bf5d48892a9   classes/hyperf              "/bin/sh"                4 weeks ago   Up 3 weeks    0.0.0.0:9512->9512/tcp                     hyperf-backend
    b5d9eadd35cf   classes/php:7.1-fpm         "docker-php-entrypoi…"   4 weeks ago   Up 19 hours   9000/tcp                                   php71
    $ docker container rm -f 32
    32
    $ docker image rm nginx:latest
    Untagged: nginx:latest
    Untagged: nginx@sha256:0d17b565c37bcbd895e9d92315a05c1c3c9a29f762b011a10c54a66cd53c9b31
    Deleted: sha256:eeb9db34b33190cac170b27d857e9b23511d396a2609c1a54e93025634afed0a
    Deleted: sha256:329714c05b53967354e105142a5075c4dfa6814e2fdc54f5ca5e1b6a39108ebb
    Deleted: sha256:14f1624904f0aca21e1d64758ebccade9321ef49689556c01f12f54607d5354c
    Deleted: sha256:3d2d2b4995bda324283359b9f57e4c9e455e644b3636e3aae7890d607697bae0
    Deleted: sha256:bad387b6281671164a260a90feab91c0beb6650f43833fdcdac532865ea9f3c0
    Deleted: sha256:b5e4d1f1c443d3283d42d586edf903aab8bb5f23f7249e49fd87a169382ec87e
    Deleted: sha256:1c79be3b9cebb9838b5c607567cb18eb50cd94e39b20a6241ca7d2d53dcffc89
    $ docker image ls
    REPOSITORY                                                        TAG               IMAGE ID       CREATED        SIZE
    phpstorm_helpers                                                  PS-212.5712.51    52009cf10d7b   2 days ago     1.56MB
    registry.cn-beijing.aliyuncs.com/yupao-base/hyperf-debian-php74   dev               3a7274e2d255   4 weeks ago    641MB
    busybox                                                           latest            b34806a1af7a   5 weeks ago    1.41MB
    classes/nginx                                                     1.21-alpine       59f53e4a8b9f   6 weeks ago    22MB
    classes/php                                                       7.1-fpm           3a8daea4f41e   6 weeks ago    525MB
    classes/hyperf                                                    latest            251a84f0f2fd   6 weeks ago    113MB
    moby/buildkit                                                     buildx-stable-1   cb9b18fdb708   8 weeks ago    134MB
    ubuntu                                                            latest            d5ca7a445605   3 months ago   65.6MB
    $ ll
    total 286880
    drwxr-xr-x  10 johnhe  staff        320  1 16 21:04 ./
    drwxr-xr-x   8 johnhe  staff        256  1 16 13:08 ../
    -rw-r--r--   1 johnhe  staff         13  1 16 00:10 .gitignore
    drwxr-xr-x   6 johnhe  staff        192  1 16 17:11 .idea/
    -rw-r--r--   1 johnhe  staff        638  1 16 00:49 Makefile
    drwxr-xr-x   5 johnhe  staff        160  1 16 00:51 build/
    -rw-r--r--   1 johnhe  staff        804  1 16 00:49 make.bat
    -rw-------   1 johnhe  staff  138865152  1 16 21:04 nginx.bak
    -rw-r--r--   1 johnhe  staff        641  1 16 00:10 requirements.txt
    drwxr-xr-x  12 johnhe  staff        384  1 16 15:45 source/
    $ docker image load -i ./nginx.bak
    1c79be3b9ceb: Loading layer [==================================================>]  77.83MB/77.83MB
    c6652321c7b9: Loading layer [==================================================>]  60.98MB/60.98MB
    d00df4ca0725: Loading layer [==================================================>]  3.072kB/3.072kB
    eb5d612bd5e0: Loading layer [==================================================>]  4.096kB/4.096kB
    01792ec538b3: Loading layer [==================================================>]  3.584kB/3.584kB
    7bc89178e1bb: Loading layer [==================================================>]  7.168kB/7.168kB
    Loaded image: nginx:latest