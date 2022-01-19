容器的交互式模式
=====================


创建一个容器并进入交互式模式：``docker container run -it``

.. code-block:: bash

    $ docker container run -it ubuntu sh
    #
    #
    # pwd
    /
    # ls
    bin  boot  dev	etc  home  lib	media  mnt  opt  proc  root  run  sbin	srv  sys  tmp  usr  var
    # exit
    $ docker container ls -a
    CONTAINER ID   IMAGE                                                                 COMMAND                  CREATED          STATUS                      PORTS                                      NAMES
    396017d4da35   ubuntu                                                                "sh"                     50 seconds ago   Exited (0) 19 seconds ago                                              strange_hamilton
    772b00f9f296   52009cf10d7b                                                          "/bin/sh"                2 days ago       Created                                                                phpstorm_helpers_PS-212.5712.51
    a42f90b43fd8   classes/nginx:1.21-alpine                                             "/docker-entrypoint.…"   3 days ago       Up 13 hours                 0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp   nginx121
    9e0ae9623c69   classes/hyperf                                                        "/bin/sh"                3 weeks ago      Up 2 days                   0.0.0.0:9513->9513/tcp                     member-private
    167fe755673f   registry.cn-beijing.aliyuncs.com/yupao-base/hyperf-debian-php74:dev   "bash"                   4 weeks ago      Exited (137) 5 days ago                                                resume-service
    cbd033683783   registry.cn-beijing.aliyuncs.com/yupao-base/hyperf-debian-php74:dev   "bash"                   4 weeks ago      Exited (137) 5 days ago                                                common-service
    efc7fa3a3b70   registry.cn-beijing.aliyuncs.com/yupao-base/hyperf-debian-php74:dev   "bash"                   4 weeks ago      Exited (137) 5 days ago                                                yupao-api
    33fbc40bef50   classes/hyperf                                                        "/bin/sh"                4 weeks ago      Up 3 weeks                  0.0.0.0:9505->9505/tcp                     hyperf-job_commom
    c8403acb95c5   classes/hyperf                                                        "/bin/sh"                4 weeks ago      Up 11 days                  0.0.0.0:9504->9504/tcp                     hyperf-job-business
    61d23490f60d   classes/hyperf                                                        "/bin/sh"                4 weeks ago      Up 3 weeks                  0.0.0.0:9511->9511/tcp                     hyperf-joblist
    9bf5d48892a9   classes/hyperf                                                        "/bin/sh"                4 weeks ago      Up 3 weeks                  0.0.0.0:9512->9512/tcp                     hyperf-backend
    b5d9eadd35cf   classes/php:7.1-fpm                                                   "docker-php-entrypoi…"   4 weeks ago      Up 13 hours                 9000/tcp                                   php71

在一个已经运行的容器里执行一个额外的command：``docker container exec -it``


.. code-block:: bash

    $ docker container run -d -p 8080:80 nginx
    7153e591588f0d22f7d187b5d1b681aa342fea3864c8bceceb0ab73d0363c15b
    $ docker container ls
    CONTAINER ID   IMAGE                       COMMAND                  CREATED          STATUS          PORTS                                      NAMES
    7153e591588f   nginx                       "/docker-entrypoint.…"   14 seconds ago   Up 13 seconds   0.0.0.0:8080->80/tcp                       quirky_solomon
    a42f90b43fd8   classes/nginx:1.21-alpine   "/docker-entrypoint.…"   3 days ago       Up 13 hours     0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp   nginx121
    9e0ae9623c69   classes/hyperf              "/bin/sh"                3 weeks ago      Up 2 days       0.0.0.0:9513->9513/tcp                     member-private
    33fbc40bef50   classes/hyperf              "/bin/sh"                4 weeks ago      Up 3 weeks      0.0.0.0:9505->9505/tcp                     hyperf-job_commom
    c8403acb95c5   classes/hyperf              "/bin/sh"                4 weeks ago      Up 11 days      0.0.0.0:9504->9504/tcp                     hyperf-job-business
    61d23490f60d   classes/hyperf              "/bin/sh"                4 weeks ago      Up 3 weeks      0.0.0.0:9511->9511/tcp                     hyperf-joblist
    9bf5d48892a9   classes/hyperf              "/bin/sh"                4 weeks ago      Up 3 weeks      0.0.0.0:9512->9512/tcp                     hyperf-backend
    b5d9eadd35cf   classes/php:7.1-fpm         "docker-php-entrypoi…"   4 weeks ago      Up 13 hours     9000/tcp                                   php71
    $ docker exec -it 71 sh
    #
    #
    #
    # pwd
    /
    #
    # ls
    bin  boot  dev	docker-entrypoint.d  docker-entrypoint.sh  etc	home  lib  media  mnt  opt  proc  root	run  sbin  srv	sys  tmp  usr  var
    #
    # exit
    $ docker container ps
    CONTAINER ID   IMAGE                       COMMAND                  CREATED              STATUS              PORTS                                      NAMES
    7153e591588f   nginx                       "/docker-entrypoint.…"   About a minute ago   Up About a minute   0.0.0.0:8080->80/tcp                       quirky_solomon
    a42f90b43fd8   classes/nginx:1.21-alpine   "/docker-entrypoint.…"   3 days ago           Up 13 hours         0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp   nginx121
    9e0ae9623c69   classes/hyperf              "/bin/sh"                3 weeks ago          Up 2 days           0.0.0.0:9513->9513/tcp                     member-private
    33fbc40bef50   classes/hyperf              "/bin/sh"                4 weeks ago          Up 3 weeks          0.0.0.0:9505->9505/tcp                     hyperf-job_commom
    c8403acb95c5   classes/hyperf              "/bin/sh"                4 weeks ago          Up 11 days          0.0.0.0:9504->9504/tcp                     hyperf-job-business
    61d23490f60d   classes/hyperf              "/bin/sh"                4 weeks ago          Up 3 weeks          0.0.0.0:9511->9511/tcp                     hyperf-joblist
    9bf5d48892a9   classes/hyperf              "/bin/sh"                4 weeks ago          Up 3 weeks          0.0.0.0:9512->9512/tcp                     hyperf-backend
    b5d9eadd35cf   classes/php:7.1-fpm         "docker-php-entrypoi…"   4 weeks ago          Up 13 hours         9000/tcp                                   php71



