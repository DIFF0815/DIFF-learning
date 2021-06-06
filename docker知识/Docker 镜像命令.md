#### Docker镜像列表地址

https://hub.docker.com/search?q=&type=image

#### Docker命令文档查看

https://docs.docker.com/engine/reference/run/

#### Docker 镜像命令

```shell
docker --version
docker --help
docker xx --help

docker images # 查看本地所有镜像
docker images -a # 同上
docker images -q # 查看本地镜像的IMAGE ID

docker search image-name # 搜索远程镜像信息 
docker search image-name --filter-STARS=3000 # 搜索stars 数在3000以上的镜像数量

docker pull   image-name[:tag] # 下载镜像
# 示例
docker pull mysql:5.7
docker pull docker.io/library/mysql:5.7 # 同上

docker rmi -f fce289e99eb9(镜像ID) # 删除指定镜像

docker rmi -f fce289e99eb9(镜像ID) cb46a5704478(镜像ID) # 删除多个镜像
```

![image-20210603010417387](/Users/artist/Library/Application Support/typora-user-images/image-20210603010417387.png)

#### 容器命令

##### 有了镜像才可以创建容器

```shell
docker pull centos
```

##### 新建容器并启动

```shell
docker run [可选参数] image
# 参数说明
--name="Name" 容器名字 tomcat tomcat02，用来区分容器
-d						后台方式运行
-it						使用交互式方式运行，进入容器查看内容
-p						指定容器的端口 -p 8080:8080
	-p 主机端口:容器端口
	-p ip:主机端口:容器端口
	-p 容器端口
	容器端口
-P						随机指定端口(大写)
```

##### 启动并进入centos容器

```shell
➜  ~ docker run -it centos /bin/bash
```

![image-20210604204716581](/Users/artist/Library/Application Support/typora-user-images/image-20210604204716581.png)



##### 查看正在运行的容器

```shell
docker ps    查看增值运行的容器
docker ps -a 查看正在运行的容器 + 曾经运行过的容器
docker ps -n=? 查看最近创建的容器，后面加数字
docker ps -q   只显示容器编号
```

#### 退出容器

```shell
exit 直接停止并退出容器
ctrl + p + q 容器不停止退出
```

##### 删除容器

```shell
docker rm + 容器ID						 删除指定的容器(运行中的不能删除，强制删除 加上 -f)
docker rm -f $(docker ps -aq) 递归删除按照命令查询出的记录
docker ps -a -q|xargs docker rm 同上
```

##### 启动和停止容器的操作

```shell
docker start 容器ID
docker restart 容器ID
docker stop 容器ID 
```

##### 常用其他命令

后台启动容器

```shell
docker run -d centos
# 如果后台执行程序 但是没有对应的前台 后台程序会自动停止
```

查看日期

```shell
docker logs -tf --tail number 容器ID

# 自己编写一段shell 脚本 创建一些日志
docker run -d centos /bin/sh -c "while true;do echo helloworld;sleep 1;done"

# 停止容器
docker stop container-id
```

查看容器中进程信息

```shell
docker top container-id
```

查看镜像的元数据

```shell
➜  ~ docker inspect 4c3c5692bc41     
[
    {
        "Id": "4c3c5692bc416ed0b7101324d8cd724d26371dbd2deace22a14308f88cd52b1d",
        "Created": "2020-09-24T03:20:41.805323079Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            "-g",
            "daemon off;"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 4294,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2021-06-04T12:43:19.883539341Z",
            "FinishedAt": "2021-06-04T12:42:39.464205372Z"
        },
        "Image": "sha256:e43dc4185a80f780d6a5a0fd0831a2ef859a332b690ef6e0e250b51ccd4bbe64",
        "ResolvConfPath": "/var/lib/docker/containers/4c3c5692bc416ed0b7101324d8cd724d26371dbd2deace22a14308f88cd52b1d/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/4c3c5692bc416ed0b7101324d8cd724d26371dbd2deace22a14308f88cd52b1d/hostname",
        "HostsPath": "/var/lib/docker/containers/4c3c5692bc416ed0b7101324d8cd724d26371dbd2deace22a14308f88cd52b1d/hosts",
        "LogPath": "/var/lib/docker/containers/4c3c5692bc416ed0b7101324d8cd724d26371dbd2deace22a14308f88cd52b1d/4c3c5692bc416ed0b7101324d8cd724d26371dbd2deace22a14308f88cd52b1d-json.log",
        "Name": "/nginx",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": [
                "/Users/artist/Program/docker/dnmp/services/nginx/nginx.conf:/etc/nginx/nginx.conf:ro",
                "/Users/artist/Program/docker/dnmp/services/nginx/conf.d:/etc/nginx/conf.d:rw",
                "/Users/artist/Program/docker/dnmp/services/nginx/ssl:/ssl:rw",
                "/Users/artist/Program/docker/dnmp/services/nginx/fastcgi-php.conf:/etc/nginx/fastcgi-php.conf:ro",
                "/Users/artist/Program/docker/dnmp/www:/www:rw",
                "/Users/artist/Program/docker/dnmp/services/nginx/fastcgi_params:/etc/nginx/fastcgi_params:ro",
                "/Users/artist/Program/docker/dnmp/logs/nginx:/var/log/nginx:rw"
            ],
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "dnmp_default",
            "PortBindings": {
                "443/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "443"
                    }
                ],
                "80/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "80"
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "always",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": [],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "shareable",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": null,
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": null,
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/b5d0dcf3c36169bdff61cfcb5459267b0bee126e5ce904915fec94d77f8dd662-init/diff:/var/lib/docker/overlay2/b1e11a4c30416660fbdf26aeaa73e3e751cf22ffe151c8f29cf6b3f07f55147b/diff:/var/lib/docker/overlay2/f04f30a3846357c966f69a295340be5bb8e8a715b85d52421590082464f9d46c/diff:/var/lib/docker/overlay2/9153a3abc75838310bc87d1f5e6a8ac2621922599e0b26de6f2b74ad7fc33617/diff:/var/lib/docker/overlay2/79d1b577050821b809a7f116429d8b144e459c3a71087c72afbfde1f3af98fe8/diff:/var/lib/docker/overlay2/a821726a7c1abcc46d658af409515b527143a871d3e53739a30be78710cbc3ab/diff:/var/lib/docker/overlay2/727a9dbc277fac47598598bce808bc5a241c992c77e215125bccb790ba154cc5/diff:/var/lib/docker/overlay2/eda142aed85fdd619645050fb49a1bc291f36893d8f82501ce099b157234efaa/diff",
                "MergedDir": "/var/lib/docker/overlay2/b5d0dcf3c36169bdff61cfcb5459267b0bee126e5ce904915fec94d77f8dd662/merged",
                "UpperDir": "/var/lib/docker/overlay2/b5d0dcf3c36169bdff61cfcb5459267b0bee126e5ce904915fec94d77f8dd662/diff",
                "WorkDir": "/var/lib/docker/overlay2/b5d0dcf3c36169bdff61cfcb5459267b0bee126e5ce904915fec94d77f8dd662/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [
            {
                "Type": "bind",
                "Source": "/Users/artist/Program/docker/dnmp/services/nginx/nginx.conf",
                "Destination": "/etc/nginx/nginx.conf",
                "Mode": "ro",
                "RW": false,
                "Propagation": "rprivate"
            },
            {
                "Type": "bind",
                "Source": "/Users/artist/Program/docker/dnmp/services/nginx/ssl",
                "Destination": "/ssl",
                "Mode": "rw",
                "RW": true,
                "Propagation": "rprivate"
            },
            {
                "Type": "bind",
                "Source": "/Users/artist/Program/docker/dnmp/logs/nginx",
                "Destination": "/var/log/nginx",
                "Mode": "rw",
                "RW": true,
                "Propagation": "rprivate"
            },
            {
                "Type": "bind",
                "Source": "/Users/artist/Program/docker/dnmp/www",
                "Destination": "/www",
                "Mode": "rw",
                "RW": true,
                "Propagation": "rprivate"
            },
            {
                "Type": "bind",
                "Source": "/Users/artist/Program/docker/dnmp/services/nginx/conf.d",
                "Destination": "/etc/nginx/conf.d",
                "Mode": "rw",
                "RW": true,
                "Propagation": "rprivate"
            },
            {
                "Type": "bind",
                "Source": "/Users/artist/Program/docker/dnmp/services/nginx/fastcgi-php.conf",
                "Destination": "/etc/nginx/fastcgi-php.conf",
                "Mode": "ro",
                "RW": false,
                "Propagation": "rprivate"
            },
            {
                "Type": "bind",
                "Source": "/Users/artist/Program/docker/dnmp/services/nginx/fastcgi_params",
                "Destination": "/etc/nginx/fastcgi_params",
                "Mode": "ro",
                "RW": false,
                "Propagation": "rprivate"
            }
        ],
        "Config": {
            "Hostname": "4c3c5692bc41",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "443/tcp": {},
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "TZ=Asia/Shanghai",
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.19.1",
                "NJS_VERSION=0.4.2",
                "PKG_RELEASE=1",
                "INSTALL_APPS=,,"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "dnmp_nginx",
            "Volumes": {
                "/etc/nginx/conf.d": {},
                "/etc/nginx/fastcgi-php.conf": {},
                "/etc/nginx/fastcgi_params": {},
                "/etc/nginx/nginx.conf": {},
                "/ssl": {},
                "/var/log/nginx": {},
                "/www": {}
            },
            "WorkingDir": "/www",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "com.docker.compose.config-hash": "9b72166d20825ff1ff549898c6f3e76f46e2f1d1795597f47a63012d26904a24",
                "com.docker.compose.container-number": "1",
                "com.docker.compose.oneoff": "False",
                "com.docker.compose.project": "dnmp",
                "com.docker.compose.project.config_files": "docker-compose.yml",
                "com.docker.compose.project.working_dir": "/Users/artist/Program/docker/dnmp",
                "com.docker.compose.service": "nginx",
                "com.docker.compose.version": "1.25.4",
                "maintainer": "NGINX Docker Maintainers \u003cdocker-maint@nginx.com\u003e"
            },
            "StopSignal": "SIGTERM"
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "b7cef707cfe8c83a80c2a481e8ab5076b49df7b1fa810e3a595bbc2bf6eb6d35",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "443/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "443"
                    },
                    {
                        "HostIp": "::",
                        "HostPort": "443"
                    }
                ],
                "80/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "80"
                    },
                    {
                        "HostIp": "::",
                        "HostPort": "80"
                    }
                ]
            },
            "SandboxKey": "/var/run/docker/netns/b7cef707cfe8",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "",
            "Gateway": "",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "",
            "IPPrefixLen": 0,
            "IPv6Gateway": "",
            "MacAddress": "",
            "Networks": {
                "dnmp_default": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": [
                        "4c3c5692bc41",
                        "nginx"
                    ],
                    "NetworkID": "94db6d10d9314e003c55d2f369c2644b24c005a0a719f39777f786e7c48065b9",
                    "EndpointID": "9accb22f21162b288e902d323fa79b0fad8263321df3480f0a794465c3129ad2",
                    "Gateway": "172.21.0.1",
                    "IPAddress": "172.21.0.4",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:15:00:04",
                    "DriverOpts": null
                }
            }
        }
    }
]

```

##### 进入当前正在运行的容器

```shell
# 方式一
docker exec -it container-id /bin/bash # 开启一个新的终端

➜  ~ docker exec -it 6458c15be991 /bin/bash            
[root@6458c15be991 /]# ps -ef   
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 13:52 ?        00:00:00 /bin/sh -c while true;do echo hello world;sleep 1;done
root        67     0  0 13:53 pts/0    00:00:00 /bin/bash
root        91     1  0 13:53 ?        00:00:00 /usr/bin/coreutils --coreutils-prog-shebang=sleep /usr/bin/sleep 1
root        92    67  0 13:53 pts/0    00:00:00 ps -ef


# 方式二
docker attach container-id # 进入当前正在执行的终端
```

##### 从容器内拷贝文件到主机

```shell
docker cp 6458c15be991:/home/123.java ~/Word
```



#### 安装并使用nginx

```shell
docker run -d --name nginx01 -p 3344:80 nginx
```

![image-20210605180839083](/Users/artist/Library/Application Support/typora-user-images/image-20210605180839083.png)

##### 再次进入nginx容器

每个容器都相当于一个独立且隔离的的linux环境

```shell
➜  ~ docker exec -it nginx01 /bin/bash            
root@a23517e4cc38:/# whereis nginx
nginx: /usr/sbin/nginx /usr/lib/nginx /etc/nginx /usr/share/nginx
```

关闭容器

```shell
➜  ~ docker stop a23517e4cc38            
a23517e4cc38
➜  ~ curl localhost:3344  
curl: (7) Failed to connect to localhost port 3344: Connection refused
```

#### 容器数据卷

##### 什么是容器数据卷

docker的理念回顾

将应用和环境打包成一个镜像！

如果数据都在容器中，那么我们把容器删除，数据就会丢失！需求：要把数据进行持久化！

MySQL，容器删了，删库跑路！需求：数据可以存储在本地！

容器之间可以有个数据共享的技术！Docker容器中产生的数据，同步到本地！

这就是卷技术！目录的挂载，将我们容器内的目录，挂载到宿主机上面！

```shell
docker run -it -v /Users/artist/Word/docker:/home centos /bin/bash
docker run -it -v 宿主机目录:容器内目录 镜像名称 终端
```

此时，宿主机与容器内目录开始进行同步

#### 实战MySQL

```shell
# 1 获取mysql
docker pull mysql:5.7
# 2 启动mysql
docker run -it -p 3310:3306 -v /Users/artist/Word/docker/mysql/conf:/etc/mysql/conf.d -v /Users/artist/Word/docker/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 --name mysql01 mysql:5.7
```

#### 具名挂载和匿名挂载

```shell
# 匿名挂载
-v 容器内路径
docker run -d -P(大写，随机指定端口) -v /etc/nginx(只写容器内目录) nginx

# 查看所有的volume的情况
docker volume ls

# 下面就匿名挂载，在-v后只写了容器内的路径，没有写容器外的路径
```

![image-20210606163943419](/Users/artist/Library/Application Support/typora-user-images/image-20210606163943419.png)

```shell
# 具名挂载
docker run -it -v juming-centos:/home --name centos-01 centos /bin/bash
docker volume ls
# print
# local     juming-centos

docker volume inspect juming-centos
# print 

```



##### 区分匿名挂载、域名挂载以及指定路径挂载

```shell
-v 容器内路径 #匿名挂载
-v 卷名:容器内路径 #具名挂载
-v /宿主机路径:/容器内路径 # 指定路径挂载
```

##### 拓展

```shell
docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx:ro nginx
docker run -d -P --name nginx02 -v juming-nginx:/etc/nginx:rw nginx
# 通过 -v 容器内路径:ro rw  改变读写权限
ro readonly  表示只读
rw readwrite 表示读写
# 一旦设置了容器权限，容器对我们挂载出来的内容是有限定的
# ro 只要看到ro 就说明这个路径只能通过宿主机来操作，容器内是无法操作的
```



#### 初识Dockfile

Dockerfile 就是用来构建docker镜像的构建文件







