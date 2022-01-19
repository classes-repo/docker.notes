镜像的查看和删除
=================

.. code-block:: bash


    $ docker image

    Usage:  docker image COMMAND

    Manage images

    Commands:
    build       Build an image from a Dockerfile
    history     Show the history of an image
    import      Import the contents from a tarball to create a filesystem image
    inspect     Display detailed information on one or more images
    load        Load an image from a tar archive or STDIN
    ls          List images
    prune       Remove unused images
    pull        Pull an image or a repository from a registry
    push        Push an image or a repository to a registry
    rm          Remove one or more images
    save        Save one or more images to a tar archive (streamed to STDOUT by default)
    tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE

    Run 'docker image COMMAND --help' for more information on a command.



镜像的拉取Pull Image
----------------------

默认从Docker Hub拉取，如果不指定版本，会拉取最新版

.. code-block:: bash

    $ docker pull nginx
    Using default tag: latest
    latest: Pulling from library/nginx
    69692152171a: Pull complete
    49f7d34d62c1: Pull complete
    5f97dc5d71ab: Pull complete
    cfcd0711b93a: Pull complete
    be6172d7651b: Pull complete
    de9813870342: Pull complete
    Digest: sha256:df13abe416e37eb3db4722840dd479b00ba193ac6606e7902331dcea50f4f1f2
    Status: Downloaded newer image for nginx:latest
    docker.io/library/nginx:latest

指定版本

.. code-block:: bash

    $ docker pull nginx:1.20.0
    1.20.0: Pulling from library/nginx
    69692152171a: Already exists
    965615a5cec8: Pull complete
    b141b026b9ce: Pull complete
    8d70dc384fb3: Pull complete
    525e372d6dee: Pull complete
    Digest: sha256:ea4560b87ff03479670d15df426f7d02e30cb6340dcd3004cdfc048d6a1d54b4
    Status: Downloaded newer image for nginx:1.20.0
    docker.io/library/nginx:1.20.0

从Quay上拉取镜像


.. code-block:: bash

    $ docker pull quay.io/bitnami/nginx
    Using default tag: latest
    latest: Pulling from bitnami/nginx
    2e6370f1e2d3: Pull complete
    2d464c695e97: Pull complete
    83eb3b1671f4: Pull complete
    364c139450f9: Pull complete
    dc453d5ae92e: Pull complete
    09bd59934b83: Pull complete
    8d2bd62eedfb: Pull complete
    8ac060ae1ede: Pull complete
    c7c9bc2f4f9d: Pull complete
    6dd7098b85fa: Pull complete
    894a70299d18: Pull complete
    Digest: sha256:d143befa04e503472603190da62db157383797d281fb04e6a72c85b48e0b3239
    Status: Downloaded newer image for quay.io/bitnami/nginx:latest
    quay.io/bitnami/nginx:latest


镜像的查看
---------------

.. code-block:: bash

    $ docker image ls
    REPOSITORY              TAG       IMAGE ID       CREATED       SIZE
    quay.io/bitnami/nginx   latest    0922eabe1625   6 hours ago   89.3MB
    nginx                   1.20.0    7ab27dbbfbdf   10 days ago   133MB
    nginx


查看镜像详细信息
-----------------

.. code-block:: bash

    $ docker image inspect nginx
    [
        {
            "Id": "sha256:eeb9db34b33190cac170b27d857e9b23511d396a2609c1a54e93025634afed0a",
            "RepoTags": [
                "nginx:latest"
            ],
            "RepoDigests": [
                "nginx@sha256:0d17b565c37bcbd895e9d92315a05c1c3c9a29f762b011a10c54a66cd53c9b31"
            ],
            "Parent": "",
            "Comment": "",
            "Created": "2021-12-29T18:45:32.26799474Z",
            "Container": "28117e6cd07462919e64874c17cec15a453e5b3d99b088f04a12a7640c27c280",
            "ContainerConfig": {
                "Hostname": "28117e6cd074",
                "Domainname": "",
                "User": "",
                "AttachStdin": false,
                "AttachStdout": false,
                "AttachStderr": false,
                "ExposedPorts": {
                    "80/tcp": {}
                },
                "Tty": false,
                "OpenStdin": false,
                "StdinOnce": false,
                "Env": [
                    "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                    "NGINX_VERSION=1.21.5",
                    "NJS_VERSION=0.7.1",
                    "PKG_RELEASE=1~bullseye"
                ],
                "Cmd": [
                    "/bin/sh",
                    "-c",
                    "#(nop) ",
                    "CMD [\"nginx\" \"-g\" \"daemon off;\"]"
                ],
                "Image": "sha256:86f0ad4f760522a77d5d2748709f102fba21b448831ba769d6b5bee6bc8b15e7",
                "Volumes": null,
                "WorkingDir": "",
                "Entrypoint": [
                    "/docker-entrypoint.sh"
                ],
                "OnBuild": null,
                "Labels": {
                    "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
                },
                "StopSignal": "SIGQUIT"
            },
            "DockerVersion": "20.10.7",
            "Author": "",
            "Config": {
                "Hostname": "",
                "Domainname": "",
                "User": "",
                "AttachStdin": false,
                "AttachStdout": false,
                "AttachStderr": false,
                "ExposedPorts": {
                    "80/tcp": {}
                },
                "Tty": false,
                "OpenStdin": false,
                "StdinOnce": false,
                "Env": [
                    "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                    "NGINX_VERSION=1.21.5",
                    "NJS_VERSION=0.7.1",
                    "PKG_RELEASE=1~bullseye"
                ],
                "Cmd": [
                    "nginx",
                    "-g",
                    "daemon off;"
                ],
                "Image": "sha256:86f0ad4f760522a77d5d2748709f102fba21b448831ba769d6b5bee6bc8b15e7",
                "Volumes": null,
                "WorkingDir": "",
                "Entrypoint": [
                    "/docker-entrypoint.sh"
                ],
                "OnBuild": null,
                "Labels": {
                    "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
                },
                "StopSignal": "SIGQUIT"
            },
            "Architecture": "arm64",
            "Variant": "v8",
            "Os": "linux",
            "Size": 134458357,
            "VirtualSize": 134458357,
            "GraphDriver": {
                "Data": {
                    "LowerDir": "/var/lib/docker/overlay2/71a67ccad5c06d21b6cea4a4c6777b15e9d148c6f6469a21d3baaa6d7a93d281/diff:/var/lib/docker/overlay2/26c759131dbeb5d5559105872fe79e736207d7dd23c9309604d855ac49e9c146/diff:/var/lib/docker/overlay2/c5c43a3607987b6a8015b7354f984e76b36c58bb8c0549510fd88296c7c2d1e7/diff:/var/lib/docker/overlay2/31700a64f48f76459ac9d8b30adf7a891f50d554bbb2e3b3f7123513a4a37cca/diff:/var/lib/docker/overlay2/60712eaea34d50ded405060c2dc49a0fc840272a657fe3463c40b8f5db1519dd/diff",
                    "MergedDir": "/var/lib/docker/overlay2/c7786f0dd2b59b645efc5d4e132fd2145b35a4f9c6d463dc460f56e40ffc1917/merged",
                    "UpperDir": "/var/lib/docker/overlay2/c7786f0dd2b59b645efc5d4e132fd2145b35a4f9c6d463dc460f56e40ffc1917/diff",
                    "WorkDir": "/var/lib/docker/overlay2/c7786f0dd2b59b645efc5d4e132fd2145b35a4f9c6d463dc460f56e40ffc1917/work"
                },
                "Name": "overlay2"
            },
            "RootFS": {
                "Type": "layers",
                "Layers": [
                    "sha256:1c79be3b9cebb9838b5c607567cb18eb50cd94e39b20a6241ca7d2d53dcffc89",
                    "sha256:c6652321c7b9deb69994b5490710e7ab52a38f5171eddbe6f4d47fb9ea928929",
                    "sha256:d00df4ca0725daf0ad547fcc9c731ed877d7b898559703ffe94e35de77ebd455",
                    "sha256:eb5d612bd5e0648b5dd9680101b778787652f435ac73db4b5e559b868392a314",
                    "sha256:01792ec538b3b8d67d341ad7b079beec9b289feb8a1e618b3fcfe2bb0c206a2b",
                    "sha256:7bc89178e1bbe5212cc907f798b0f3bb3e07c71083390703e04486012d398a4f"
                ]
            },
            "Metadata": {
                "LastTagTime": "0001-01-01T00:00:00Z"
            }
        }
    ]                latest    f0b8a9a54136   10 days ago   133MB


镜像的删除
------------------

.. code-block:: bash

    $ docker image rm 0922eabe1625
    Untagged: quay.io/bitnami/nginx:latest
    Untagged: quay.io/bitnami/nginx@sha256:d143befa04e503472603190da62db157383797d281fb04e6a72c85b48e0b3239
    Deleted: sha256:0922eabe16250e2f4711146e31b7aac0e547f52daa6cf01c9d00cf64d49c68c8
    Deleted: sha256:5eee4ed0f6b242e2c6e4f4066c7aca26bf9b3b021b511b56a0dadd52610606bd
    Deleted: sha256:472a75325eda417558f9100ff8b4a97f4a5e8586a14eb9c8fc12f944b26a21f8
    Deleted: sha256:cdcb5872f8a64a0b5839711fcd2a87ba05795e5bf6a70ba9510b8066cdd25e76
    Deleted: sha256:e0f1b7345a521469bbeb7ec53ef98227bd38c87efa19855c5ba0db0ac25c8e83
    Deleted: sha256:11b9c2261cfc687fba8d300b83434854cc01e91a2f8b1c21dadd937e59290c99
    Deleted: sha256:4819311ec2867ad82d017253500be1148fc335ad13b6c1eb6875154da582fcf2
    Deleted: sha256:784480add553b8e8d5ee1bbd229ed8be92099e5fb61009ed7398b93d5705a560
    Deleted: sha256:e0c520d1a43832d5d2b1028e3f57047f9d9f71078c0187f4bb05e6a6a572993d
    Deleted: sha256:94d5b1d6c9e31de42ce58b8ce51eb6fb5292ec889a6d95763ad2905330b92762
    Deleted: sha256:95deba55c490bbb8de44551d3e6a89704758c93ba8503a593cb7c07dfbae0058
    Deleted: sha256:1ad1d903ef1def850cd44e2010b46542196e5f91e53317dbdb2c1eedfc2d770c
