---
title: Docker tutorial
layout: default
category: lessons
tags: [intro, docker, tutorial, beginner]
---

本文记录小组学习内容

以一句话概括为什么要学习

    A little knowledge is a dangerous thing

##词汇发音纠正

IT部分词汇生僻，充分展现了程序员的宅本质，导致发音困难，由于口音等问题不同人又有不同读法，如果不查字典而凭空猜测很容易产生错误，而且很难自己发觉和改正。本周纠正几个工作中常用词的发音，今后的工作中也将持续及时发现和改正这方面错误。

对于不确定的读音，也可以在youtube上搜索prononciation来收听真人发音

    Chassis: [ˈʃæsi] 最后的s是不发音的，除了服务器机架的意思外，汽车，飞机，电视等的底架都是这个词
    Cache： [kæʃ] 音同$的cash
    Putty: [ˈpʌti] 面团，腻子等

##Docker入门

Docker和容器不是新的技术，bsd的jail和solaris的zone都是类似的概念，作为系统上的虚拟化技术，相对于虚拟机最大的优点就是使用host os内核而减少了一层guest os的虚拟化负担，因而可以实现更高的效率以及秒级的启动。

而docker的成功另一方面在于生态圈的完善，用户可以方便的上传和下载docker hub上的镜像。

###docker底层技术(isolation)

    namespace
        pid: processes
        net: networks
        ipc: inter-process communication
        mnt: mnt points
        uts: kernel and versions
    cgroups(control groups)
        isolation, allow and limit resources for containner

###安装
    
docker需要linux内核，多数主流64位linux系统都支持docker，对于windows和mac，可以使用boot2docker来创建一个虚拟机使用docker

###使用

docker有server和client, 首先启动docker服务

可以使用<http://www.docker.com/tryit>的tutorial来了解命令的基本使用

运行客户端命令docker查看可用选项

    # docker
    Usage: docker [OPTIONS] COMMAND [arg...]

    A self-sufficient runtime for linux containers.

    Options:
      --api-enable-cors=false                Enable CORS headers in the remote API
      -b, --bridge=""                        Attach containers to a pre-existing network bridge
                                               use 'none' to disable container networking
      --bip=""                               Use this CIDR notation address for the network bridge's IP, not compatible with -b
      -D, --debug=false                      Enable debug mode
      -d, --daemon=false                     Enable daemon mode
      --dns=[]                               Force Docker to use specific DNS servers
      --dns-search=[]                        Force Docker to use specific DNS search domains
      -e, --exec-driver="native"             Force the Docker runtime to use a specific exec driver
      --fixed-cidr=""                        IPv4 subnet for fixed IPs (e.g. 10.20.0.0/16)
                                               this subnet must be nested in the bridge subnet (which is defined by -b or --bip)
      --fixed-cidr-v6=""                     IPv6 subnet for fixed IPs (e.g.: 2001:a02b/48)
      -G, --group="docker"                   Group to assign the unix socket specified by -H when running in daemon mode
                                               use '' (the empty string) to disable setting of a group
      -g, --graph="/var/lib/docker"          Path to use as the root of the Docker runtime
      -H, --host=[]                          The socket(s) to bind to in daemon mode or connect to in client mode, specified using one or more tcp://host:port, unix:///path/to/socket, fd://* or fd://socketfd.
      -h, --help=false                       Print usage
      --icc=true                             Allow unrestricted inter-container and Docker daemon host communication
      --insecure-registry=[]                 Enable insecure communication with specified registries (no certificate verification for HTTPS and enable HTTP fallback) (e.g., localhost:5000 or 10.20.0.0/16)
      --ip=0.0.0.0                           Default IP address to use when binding container ports
      --ip-forward=true                      Enable net.ipv4.ip_forward and IPv6 forwarding if --fixed-cidr-v6 is defined. IPv6 forwarding may interfere with your existing IPv6 configuration when using Router Advertisement.
      --ip-masq=true                         Enable IP masquerading for bridge's IP range
      --iptables=true                        Enable Docker's addition of iptables rules
      --ipv6=false                           Enable IPv6 networking
      -l, --log-level="info"                 Set the logging level (debug, info, warn, error, fatal)
      --label=[]                             Set key=value labels to the daemon (displayed in `docker info`)
      --mtu=0                                Set the containers network MTU
                                               if no value is provided: default to the default route MTU or 1500 if no default route is available
      -p, --pidfile="/var/run/docker.pid"    Path to use for daemon PID file
      --registry-mirror=[]                   Specify a preferred Docker registry mirror
      -s, --storage-driver=""                Force the Docker runtime to use a specific storage driver
      --selinux-enabled=false                Enable selinux support. SELinux does not presently support the BTRFS storage driver
      --storage-opt=[]                       Set storage driver options
      --tls=false                            Use TLS; implied by --tlsverify flag
      --tlscacert="/root/.docker/ca.pem"     Trust only remotes providing a certificate signed by the CA given here
      --tlscert="/root/.docker/cert.pem"     Path to TLS certificate file
      --tlskey="/root/.docker/key.pem"       Path to TLS key file
      --tlsverify=false                      Use TLS and verify the remote (daemon: verify client, client: verify daemon)
      -v, --version=false                    Print version information and quit

    Commands:
        attach    Attach to a running container
        build     Build an image from a Dockerfile
        commit    Create a new image from a container's changes
        cp        Copy files/folders from a container's filesystem to the host path
        create    Create a new container
        diff      Inspect changes on a container's filesystem
        events    Get real time events from the server
        exec      Run a command in a running container
        export    Stream the contents of a container as a tar archive
        history   Show the history of an image
        images    List images
        import    Create a new filesystem image from the contents of a tarball
        info      Display system-wide information
        inspect   Return low-level information on a container or image
        kill      Kill a running container
        load      Load an image from a tar archive
        login     Register or log in to a Docker registry server
        logout    Log out from a Docker registry server
        logs      Fetch the logs of a container
        port      Lookup the public-facing port that is NAT-ed to PRIVATE_PORT
        pause     Pause all processes within a container
        ps        List containers
        pull      Pull an image or a repository from a Docker registry server
        push      Push an image or a repository to a Docker registry server
        rename    Rename an existing container
        restart   Restart a running container
        rm        Remove one or more containers
        rmi       Remove one or more images
        run       Run a command in a new container
        save      Save an image to a tar archive
        search    Search for an image on the Docker Hub
        start     Start a stopped container
        stats     Display a live stream of one or more containers' resource usage statistics
        stop      Stop a running container
        tag       Tag an image into a repository
        top       Lookup the running processes of a container
        unpause   Unpause a paused container
        version   Show the Docker version information
        wait      Block until a container stops, then print its exit code

    Run 'docker COMMAND --help' for more information on a command.

docker version查看版本

    # docker version
    Client version: 1.5.0
    Client API version: 1.17
    Go version (client): go1.3.3
    Git commit (client): a8a31ef/1.5.0
    OS/Arch (client): linux/amd64
    Server version: 1.5.0
    Server API version: 1.17
    Go version (server): go1.3.3
    Git commit (server): a8a31ef/1.5.0

docker search oracle在docker hub上搜索容器

    #docker search oracle
    NAME                                      DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
    oraclelinux                               Oracle Linux is an open-source operating s...   32        [OK]
    ...

docker pull oraclelinux:6.6下载

docker run -h tutorial1 --name=tutorial1 oraclelinux:6.6  echo "hello world"

-h指定hostname， --name指定容器名字

docker ps, docker ps -a, docker ps -l

docker ps只显示running的容器，-a显示所有，-l显示最后一个

docker top, docker info, docker inspect查看状态，具体使用参照手册

docker rm, docker rmi 删除容器和删除镜像

对于要保存的修改可以使用docker commit，要放到docker hub上可以docker push（相对于pull）

##其他

docker的其他使用将在以后继续介绍，包括dockerfile的使用，docker容器间网络连接等

可以参考docker网站文档

推荐Docker Hands on: Deploy, Administer Docker Platform学习docker的使用