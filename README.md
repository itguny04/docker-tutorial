# Docker Tutorial

# Docker 설치
https://docs.docker.com/engine/install/
> Centos/RHEL
```
$ sudo yum install -y yum-utils

$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

$ sudo yum install docker-ce docker-ce-cli containerd.io    
```
> Ubuntu/Debian
```
$ sudo apt-get update
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
$ sudo apt-key fingerprint 0EBFCD88
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

> Ubuntu 20.04
```
$ sudo apt install docker.io
```

> 일반 유저에 docekr 권한 설정
```
$ sudo usermod -aG docker ubuntu
```

> docker 버전 확인
```
docker version
Client: Docker Engine - Community
 Version:           20.10.2
 API version:       1.41
 Go version:        go1.13.15
 Git commit:        2291f61
 Built:             Mon Dec 28 16:17:43 2020
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.2
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.13.15
  Git commit:       8891c58
  Built:            Mon Dec 28 16:15:19 2020
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.4.3
  GitCommit:        269548fa27e0089a8b8278fc4fc781d7f65a939b
 runc:
  Version:          1.0.0-rc92
  GitCommit:        ff819c7e9184c13b7c2607fe6c30ae19403a7aff
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```

> docker 서버 정보 확인
```
$ docker info
Client:
 Context:    default
 Debug Mode: false
 Plugins:
  app: Docker App (Docker Inc., v0.9.1-beta3)
  buildx: Build with BuildKit (Docker Inc., v0.5.1-docker)

Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 20.10.2
 Storage Driver: overlay2
  Backing Filesystem: extfs
  Supports d_type: true
  Native Overlay Diff: true
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 1
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local logentries splunk syslog
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 io.containerd.runtime.v1.linux runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 269548fa27e0089a8b8278fc4fc781d7f65a939b
 runc version: ff819c7e9184c13b7c2607fe6c30ae19403a7aff
 init version: de40ad0
 Security Options:
  apparmor
  seccomp
   Profile: default
 Kernel Version: 5.4.0-1029-aws
 Operating System: Ubuntu 20.04.1 LTS
 OSType: linux
 Architecture: x86_64
 CPUs: 1
 Total Memory: 978.6MiB
 Name: ip-172-31-5-91
 ID: LMEL:NKSC:CX3K:2BG5:GXPN:5IGG:LDIM:RWR3:3GFX:3EP5:IMU2:CYRD
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Registry: https://index.docker.io/v1/
 Labels:
 Experimental: false
 Insecure Registries:
  127.0.0.0/8
 Live Restore Enabled: false
 ```

# Docker 기본 명령어
```
$ docker help

Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Options:
      --config string      Location of client config files (default "/home/ubuntu/.docker")
  -c, --context string     Name of the context to use to connect to the daemon (overrides DOCKER_HOST env var and default context set with "docker context use")
  -D, --debug              Enable debug mode
  -H, --host list          Daemon socket(s) to connect to
  -l, --log-level string   Set the logging level ("debug"|"info"|"warn"|"error"|"fatal") (default "info")
      --tls                Use TLS; implied by --tlsverify
      --tlscacert string   Trust certs signed only by this CA (default "/home/ubuntu/.docker/ca.pem")
      --tlscert string     Path to TLS certificate file (default "/home/ubuntu/.docker/cert.pem")
      --tlskey string      Path to TLS key file (default "/home/ubuntu/.docker/key.pem")
      --tlsverify          Use TLS and verify the remote
  -v, --version            Print version information and quit
```

# Docker Tutorial 프로젝트 다운로드
```
$ git clone https://github.com/nationminu/docker-tutorial.git
$ cd docker-tutorial
```

# Docker Hub 검색
> dockerhub 에 있는 이미지를 검색. <BR>
> docker search <검색어>
```
$ docker search centos
NAME                               DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
centos                             The official build of CentOS.                   6385      [OK]
ansible/centos7-ansible            Ansible on Centos7                              132                  [OK]
consol/centos-xfce-vnc             Centos container with "headless" VNC session…   125                  [OK]
jdeathe/centos-ssh                 OpenSSH / Supervisor / EPEL/IUS/SCL Repos - …   117                  [OK]
```

# Docker 이미지로 가져오기
> docker pull <이미지이름>:<이미지태그>
```
$ docker pull centos:7
7: Pulling from library/centos
2d473b07cdd5: Pull complete
Digest: sha256:0f4ec88e21daf75124b8a9e5ca03c37a5e937e0e108a255d890492430789b60e
Status: Downloaded newer image for centos:7
docker.io/library/centos:7
```

# Docker 이미지 목록 확인
> docker images / docker image ls
```
$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
centos       7         8652b9f0cb4c   2 months ago   204MB
```
# Docker 이미지 삭제
> docker rmi <이미지이름>:<이미지태그> / docker image 그 <이미지이름>:<이미지태그>
```
$ docker image rm centos:7
Untagged: centos:7
Untagged: centos@sha256:0f4ec88e21daf75124b8a9e5ca03c37a5e937e0e108a255d890492430789b60e
Deleted: sha256:8652b9f0cb4c0599575e5a003f5906876e10c1ceb2ab9fe1786712dac14a50cf
Deleted: sha256:174f5685490326fc0a1c0f5570b8663732189b327007e47ff13d2ca59673db02

$ docker image ls
REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```

# Docker 이미지로 컨테이너 기동하기
## CentOS 실행하기 #1
> docker run <옵션> <이미지이름>:<이미지태그> <컨테이너 내부에서 실행하는 커맨드> <br>
> 로컬에 이미지가 없을 경우 자동으로 dockerhub에서 pulling
```
$ docker run --name hello centos:7 echo "HELLO"
HELLO
```
> usage : <BR>
> -d : 백그라운드로 실행<BR>
> -v : 볼륨 마운트 ex> -v "local_volume:docker_inside_volue"<BR>
> -p : 포트 바인딩 ex> -p "80:80"<BR>
> --name : 컨테이너 이름 지정 ex> --name hello<BR>
> -it : 이미지 내부로 접속(interactive terminal)


## CentOS 실행하기 #2
> interactive terminal 접속
```
docker run --name hello -it centos:7
[root@73cbfe2e0917 /]# echo "HELLO"
HELLO
[root@73cbfe2e0917 /]#
```
> 컨테이너 이름이 이미 존재하면 실행되지 않음.

# docker 컨테이너 확인
> docker ps / docker container ls [-a : 종료된 컨테이너까지 확인]
```
$ docker ps -a
CONTAINER ID   IMAGE      COMMAND       CREATED              STATUS                            PORTS     NAMES
73cbfe2e0917   centos:7   "/bin/bash"   About a minute ago   Exited (127) About a minute ago             hello
```

# docker 컨테이너 삭제
> docker rm <NAME/ID> , docker container rm <NAME/ID>
```
$ docker ps -a
CONTAINER ID   IMAGE      COMMAND       CREATED              STATUS                            PORTS     NAMES
73cbfe2e0917   centos:7   "/bin/bash"   About a minute ago   Exited (127) About a minute ago             hello

$ docker container rm hello
hello

$ docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

# nginx tutorial
> 컨테이너 실행 조건 : <BR>
> 1. dockerhub 에서 nginx:latest docker 이미지를 실행 <BR>
> 2. 프로젝트 내부의 ./nginx/html/ 소스를 nginx 컨테이너 "/var/www/html" 디렉토리로 마운트한다.<BR>
> 3. nginx의 80 포트를 로컬에서 바인딩해서 80 포트로 접속할수 있게 한다 <BR>
> 4. 컨테이너 이름은 nginx 로 설정한다 <br>
> 5. 컨테이너는 백그라운드로 실행한다.
---
```
curl http://localhost
```


# Docker 이미지 빌드하기
> docker build -t <이미지이름>:<이미지태그> <디렉토리경로> -f <Dockerfile이름>

## Dockerfile 만들기
```
From 
```
