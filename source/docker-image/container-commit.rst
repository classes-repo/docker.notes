通过 commit 创建镜像
==========================


.. code-block::

    $ docker image ls
    REPOSITORY                                                        TAG               IMAGE ID       CREATED        SIZE
    <none>                                                            <none>            4ef00d7a9f89   5 hours ago    134MB
    phptemp                                                           latest            4e8744da8bbd   14 hours ago   411MB
    phpstorm_helpers                                                  PS-212.5712.51    52009cf10d7b   3 days ago     1.56MB
    nginx                                                             latest            eeb9db34b331   2 weeks ago    134MB
    registry.cn-beijing.aliyuncs.com/yupao-base/hyperf-debian-php74   dev               3a7274e2d255   4 weeks ago    641MB
    busybox                                                           latest            b34806a1af7a   5 weeks ago    1.41MB
    classes/nginx                                                     1.21-alpine       59f53e4a8b9f   6 weeks ago    22MB
    classes/php                                                       7.1-fpm           3a8daea4f41e   6 weeks ago    525MB
    classes/hyperf                                                    latest            251a84f0f2fd   7 weeks ago    113MB
    moby/buildkit                                                     buildx-stable-1   cb9b18fdb708   2 months ago   134MB
    ubuntu                                                            latest            d5ca7a445605   3 months ago   65.6MB
    $ docker run -d nginx:latest
    6921910155edd5b9ad5d6874c36c1656b537fd576b14165d8058dd6c0ffa441e
    $ docker container ls
    CONTAINER ID   IMAGE                           COMMAND                  CREATED          STATUS          PORTS                                      NAMES
    6921910155ed   nginx:latest                    "/docker-entrypoint.…"   15 seconds ago   Up 14 seconds   80/tcp                                     brave_allen
    39afd2530500   moby/buildkit:buildx-stable-1   "buildkitd"              15 hours ago     Up 58 minutes                                              buildx_buildkit_mybuilder0
    a42f90b43fd8   classes/nginx:1.21-alpine       "/docker-entrypoint.…"   4 days ago       Up 15 minutes   0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp   nginx121
    b5d9eadd35cf   classes/php:7.1-fpm             "docker-php-entrypoi…"   5 weeks ago      Up 15 minutes   9000/tcp                                   php71
    $ docker exec -it 69 bash
    root@6921910155ed:/# echo "<h1>This is commited image<h1/>" > /usr/share/nginx/html/index.html
    root@6921910155ed:/# exit
    exit
    $ docker ps -a
    CONTAINER ID   IMAGE                                                                 COMMAND                  CREATED              STATUS                     PORTS                                      NAMES
    6921910155ed   nginx:latest                                                          "/docker-entrypoint.…"   About a minute ago   Up About a minute          80/tcp                                     brave_allen
    39afd2530500   moby/buildkit:buildx-stable-1                                         "buildkitd"              15 hours ago         Up About an hour                                                      buildx_buildkit_mybuilder0
    a42f90b43fd8   classes/nginx:1.21-alpine                                             "/docker-entrypoint.…"   4 days ago           Up 16 minutes              0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp   nginx121
    9e0ae9623c69   classes/hyperf                                                        "/bin/sh"                4 weeks ago          Exited (137) 3 hours ago                                              member-private
    167fe755673f   registry.cn-beijing.aliyuncs.com/yupao-base/hyperf-debian-php74:dev   "bash"                   4 weeks ago          Exited (137) 3 hours ago                                              resume-service
    cbd033683783   registry.cn-beijing.aliyuncs.com/yupao-base/hyperf-debian-php74:dev   "bash"                   4 weeks ago          Exited (137) 3 hours ago                                              common-service
    efc7fa3a3b70   registry.cn-beijing.aliyuncs.com/yupao-base/hyperf-debian-php74:dev   "bash"                   4 weeks ago          Exited (137) 3 hours ago                                              yupao-api
    33fbc40bef50   classes/hyperf                                                        "/bin/sh"                4 weeks ago          Exited (137) 3 hours ago                                              hyperf-job_commom
    c8403acb95c5   classes/hyperf                                                        "/bin/sh"                4 weeks ago          Exited (137) 3 hours ago                                              hyperf-job-business
    61d23490f60d   classes/hyperf                                                        "/bin/sh"                4 weeks ago          Exited (137) 3 hours ago                                              hyperf-joblist
    9bf5d48892a9   classes/hyperf                                                        "/bin/sh"                4 weeks ago          Exited (137) 3 hours ago                                              hyperf-backend
    b5d9eadd35cf   classes/php:7.1-fpm                                                   "docker-php-entrypoi…"   5 weeks ago          Up 16 minutes              9000/tcp                                   php71
    $ docker commit
    "docker commit" requires at least 1 and at most 2 arguments.
    See 'docker commit --help'.
    
    Usage:  docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
    
    Create a new image from a container's changes
    $ docker commit 6921910155ed commit-image:latest
    sha256:e2cb9394f34f0523e5fc8f6c079e095c8c627dcba6e46b90bf760026d0a41c5a
    $ docker image ls
    REPOSITORY                                                        TAG               IMAGE ID       CREATED         SIZE
    commit-image                                                      latest            e2cb9394f34f   9 seconds ago   134MB
    <none>                                                            <none>            4ef00d7a9f89   5 hours ago     134MB
    phptemp                                                           latest            4e8744da8bbd   14 hours ago    411MB
    phpstorm_helpers                                                  PS-212.5712.51    52009cf10d7b   3 days ago      1.56MB
    nginx                                                             latest            eeb9db34b331   2 weeks ago     134MB
    registry.cn-beijing.aliyuncs.com/yupao-base/hyperf-debian-php74   dev               3a7274e2d255   4 weeks ago     641MB
    busybox                                                           latest            b34806a1af7a   5 weeks ago     1.41MB
    classes/nginx                                                     1.21-alpine       59f53e4a8b9f   6 weeks ago     22MB
    classes/php                                                       7.1-fpm           3a8daea4f41e   6 weeks ago     525MB
    classes/hyperf                                                    latest            251a84f0f2fd   7 weeks ago     113MB
    moby/buildkit                                                     buildx-stable-1   cb9b18fdb708   2 months ago    134MB
    ubuntu                                                            latest            d5ca7a445605   3 months ago    65.6MB
    $ docker container rm -f 6921910155ed
    6921910155ed
    $ docker container run -it -p 8900:80 commit-image:latest
    /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
    /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
    10-listen-on-ipv6-by-default.sh: info: IPv6 listen already enabled
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
    /docker-entrypoint.sh: Configuration complete; ready for start up
    2022/01/17 08:26:31 [notice] 1#1: using the "epoll" event method
    2022/01/17 08:26:31 [notice] 1#1: nginx/1.21.5
    2022/01/17 08:26:31 [notice] 1#1: built by gcc 10.2.1 20210110 (Debian 10.2.1-6)
    2022/01/17 08:26:31 [notice] 1#1: OS: Linux 5.10.47-linuxkit
    2022/01/17 08:26:31 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
    2022/01/17 08:26:31 [notice] 1#1: start worker processes
    2022/01/17 08:26:31 [notice] 1#1: start worker process 25
    2022/01/17 08:26:31 [notice] 1#1: start worker process 26
    2022/01/17 08:26:31 [notice] 1#1: start worker process 27
    2022/01/17 08:26:31 [notice] 1#1: start worker process 28
    2022/01/17 08:26:31 [notice] 25#25: signal 28 (SIGWINCH) received
    2022/01/17 08:26:31 [notice] 1#1: signal 28 (SIGWINCH) received
    2022/01/17 08:26:31 [notice] 28#28: signal 28 (SIGWINCH) received
    2022/01/17 08:26:31 [notice] 27#27: signal 28 (SIGWINCH) received
    2022/01/17 08:26:31 [notice] 26#26: signal 28 (SIGWINCH) received
    172.110.0.1 - - [17/Jan/2022:08:26:39 +0000] "GET / HTTP/1.1" 200 32 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36" "-"
    2022/01/17 08:26:39 [error] 25#25: *2 open() "/usr/share/nginx/html/favicon.ico" failed (2: No such file or directory), client: 172.110.0.1, server: localhost, request: "GET /favicon.ico HTTP/1.1", host: "127.0.0.1:8900", referrer: "http://127.0.0.1:8900/"
    172.110.0.1 - - [17/Jan/2022:08:26:39 +0000] "GET /favicon.ico HTTP/1.1" 404 555 "http://127.0.0.1:8900/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36" "-"

