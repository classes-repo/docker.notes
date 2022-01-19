Container Mode 容器运行的各种模式
=====================================


Attached
-------

.. code-block:: bash

    $ docker container run -p 8080:80 nginx
    Unable to find image 'nginx:latest' locally
    latest: Pulling from library/nginx
    927a35006d93: Pull complete
    fc3910c70f9c: Pull complete
    e11bfbf9fd54: Pull complete
    fbb8b547daa2: Pull complete
    0f1992aeebd8: Pull complete
    f929dacee378: Pull complete
    Digest: sha256:0d17b565c37bcbd895e9d92315a05c1c3c9a29f762b011a10c54a66cd53c9b31
    Status: Downloaded newer image for nginx:latest
    /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
    /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
    10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
    10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
    /docker-entrypoint.sh: Configuration complete; ready for start up
    2022/01/16 05:40:29 [notice] 1#1: using the "epoll" event method
    2022/01/16 05:40:29 [notice] 1#1: nginx/1.21.5
    2022/01/16 05:40:29 [notice] 1#1: built by gcc 10.2.1 20210110 (Debian 10.2.1-6)
    2022/01/16 05:40:29 [notice] 1#1: OS: Linux 5.10.47-linuxkit
    2022/01/16 05:40:29 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
    2022/01/16 05:40:29 [notice] 1#1: start worker processes
    2022/01/16 05:40:29 [notice] 1#1: start worker process 32
    2022/01/16 05:40:29 [notice] 1#1: start worker process 33
    2022/01/16 05:40:29 [notice] 1#1: start worker process 34
    2022/01/16 05:40:29 [notice] 1#1: start worker process 35
    172.110.0.1 - - [16/Jan/2022:05:41:05 +0000] "GET / HTTP/1.1" 200 615 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36" "-"
    2022/01/16 05:41:05 [error] 32#32: *2 open() "/usr/share/nginx/html/favicon.ico" failed (2: No such file or directory), client: 172.110.0.1, server: localhost, request: "GET /favicon.ico HTTP/1.1", host: "127.0.0.1:8080", referrer: "http://127.0.0.1:8080/"
    172.110.0.1 - - [16/Jan/2022:05:41:05 +0000] "GET /favicon.ico HTTP/1.1" 404 555 "http://127.0.0.1:8080/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36" "-"

Detached
-------

.. code-block:: bash

    $ docker container run -d -p 8080:80 nginx
    41b6ba35ef7d3e6ace80a3fc6b073f2331a6e1e85388773999dbf50ba6cef3cd

Detached to Attached
-------

.. code-block:: bash

    $ docker ps -a
    CONTAINER ID   IMAGE                                                                 COMMAND                  CREATED         STATUS                    PORTS                                      NAMES
    41b6ba35ef7d   nginx                                                                 "/docker-entrypoint.…"   4 minutes ago   Up 4 minutes              0.0.0.0:8080->80/tcp                       kind_kalam
    772b00f9f296   52009cf10d7b                                                          "/bin/sh"                2 days ago      Created                                                              phpstorm_helpers_PS-212.5712.51
    a42f90b43fd8   classes/nginx:1.21-alpine                                             "/docker-entrypoint.…"   3 days ago      Up 12 hours               0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp   nginx121
    9e0ae9623c69   classes/hyperf                                                        "/bin/sh"                3 weeks ago     Up 2 days                 0.0.0.0:9513->9513/tcp                     member-private
    167fe755673f   registry.cn-beijing.aliyuncs.com/yupao-base/hyperf-debian-php74:dev   "bash"                   4 weeks ago     Exited (137) 5 days ago                                              resume-service
    cbd033683783   registry.cn-beijing.aliyuncs.com/yupao-base/hyperf-debian-php74:dev   "bash"                   4 weeks ago     Exited (137) 5 days ago                                              common-service
    efc7fa3a3b70   registry.cn-beijing.aliyuncs.com/yupao-base/hyperf-debian-php74:dev   "bash"                   4 weeks ago     Exited (137) 5 days ago                                              yupao-api
    33fbc40bef50   classes/hyperf                                                        "/bin/sh"                4 weeks ago     Up 3 weeks                0.0.0.0:9505->9505/tcp                     hyperf-job_commom
    c8403acb95c5   classes/hyperf                                                        "/bin/sh"                4 weeks ago     Up 10 days                0.0.0.0:9504->9504/tcp                     hyperf-job-business
    61d23490f60d   classes/hyperf                                                        "/bin/sh"                4 weeks ago     Up 3 weeks                0.0.0.0:9511->9511/tcp                     hyperf-joblist
    9bf5d48892a9   classes/hyperf                                                        "/bin/sh"                4 weeks ago     Up 3 weeks                0.0.0.0:9512->9512/tcp                     hyperf-backend
    b5d9eadd35cf   classes/php:7.1-fpm                                                   "docker-php-entrypoi…"   4 weeks ago     Up 12 hours               9000/tcp                                   php71
    $docker attach 41
    172.110.0.1 - - [16/Jan/2022:05:49:06 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36" "-"

