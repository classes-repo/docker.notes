构建参数和环境变量 (ARG vs ENV)
===============================

``ARG`` 和 ``ENV`` 是经常容易被混淆的两个Dockerfile的语法，都可以用来设置一个“变量”。 但实际上两者有很多的不同。

ENV
-----

Dockerfile.env

.. code-block:: Dockerfile

    FROM php:7.1-fpm

    ENV REDIS_VERSION=5.2.0

    RUN pecl install redis-${REDIS_VERSION} && docker-php-ext-enable redis && \
        cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini && \
        #
        # Clean up
        apt-get clean &&  \
        apt-get autoclean &&  \
        apt-get --purge -y autoremove &&  \
        rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


ARG
-----

Dockerfile.arg

.. code-block:: Dockerfile

    FROM php:7.1-fpm

    ARG REDIS_VERSION=5.2.0

    RUN pecl install redis-${REDIS_VERSION} && docker-php-ext-enable redis && \
        cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini && \
        #
        # Clean up
        apt-get clean &&  \
        apt-get autoclean &&  \
        apt-get --purge -y autoremove &&  \
        rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ARG & ENV 联合使用
-----

Dockerfile.arg.env

.. code-block:: Dockerfile

    FROM php:7.1-fpm

    ARG REDIS_V=5.2.0
    ENV REDIS_VERSION=${REDIS_V}

    RUN pecl install redis-${REDIS_VERSION} && docker-php-ext-enable redis && \
        cp /usr/local/etc/php/php.ini-production /usr/local/etc/php/php.ini && \
        #
        # Clean up
        apt-get clean &&  \
        apt-get autoclean &&  \
        apt-get --purge -y autoremove &&  \
        rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

区别
-------

.. image:: ../_static/dockerfile-guide/docker_environment_build_args.png
    :alt: docker-image
    

ARG 可以在镜像build的时候动态修改value, 通过 ``--build-arg``

.. code-block:: bash
    
    $ docker image build -f .\Dockerfile.arg -t php.arg --build-arg REDIS_VERSION=5.1.0 .

ENV 设置的变量可以在镜像中保持，并存在于容器中的环境变量里