查看容器日志
=====================

.. code-block:: bash

    $ docker container run -d -p 8080:80 nginx
    3fe9123c8d802c800ac1c134d93bd7170d9bd2289297f31b2a87215f37de21d0

``docker container logs <container ID>`` 查看已生成的日志
--------------------------------------------------------------

.. code-block:: bash

    $ docker container logs 3f
    /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
    /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
    10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
    10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
    /docker-entrypoint.sh: Configuration complete; ready for start up
    2022/01/16 06:01:19 [notice] 1#1: using the "epoll" event method
    2022/01/16 06:01:19 [notice] 1#1: nginx/1.21.5
    2022/01/16 06:01:19 [notice] 1#1: built by gcc 10.2.1 20210110 (Debian 10.2.1-6)
    2022/01/16 06:01:19 [notice] 1#1: OS: Linux 5.10.47-linuxkit
    2022/01/16 06:01:19 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
    2022/01/16 06:01:19 [notice] 1#1: start worker processes
    2022/01/16 06:01:19 [notice] 1#1: start worker process 32
    2022/01/16 06:01:19 [notice] 1#1: start worker process 33
    2022/01/16 06:01:19 [notice] 1#1: start worker process 34
    2022/01/16 06:01:19 [notice] 1#1: start worker process 35


``docker container logs -f <container ID>``  动态查看日志
-------------------------------------------------------------------------------

.. code-block:: bash

    $ docker container logs -f 3f
    /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
    /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
    10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
    10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
    /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
    /docker-entrypoint.sh: Configuration complete; ready for start up
    2022/01/16 06:01:19 [notice] 1#1: using the "epoll" event method
    2022/01/16 06:01:19 [notice] 1#1: nginx/1.21.5
    2022/01/16 06:01:19 [notice] 1#1: built by gcc 10.2.1 20210110 (Debian 10.2.1-6)
    2022/01/16 06:01:19 [notice] 1#1: OS: Linux 5.10.47-linuxkit
    2022/01/16 06:01:19 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
    2022/01/16 06:01:19 [notice] 1#1: start worker processes
    2022/01/16 06:01:19 [notice] 1#1: start worker process 32
    2022/01/16 06:01:19 [notice] 1#1: start worker process 33
    2022/01/16 06:01:19 [notice] 1#1: start worker process 34
    2022/01/16 06:01:19 [notice] 1#1: start worker process 35
    172.110.0.1 - - [16/Jan/2022:06:02:03 +0000] "GET / HTTP/1.1" 304 0 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/97.0.4692.71 Safari/537.36" "-"

