# 프로젝트 개요 (Mission Summary)
본 프로젝트는 Linux CLI(터미널), Docker(컨테이너), Git/GitHub(버전 관리 및 협업)를 활용하여 재현 가능한 로컬 개발 환경을 구축하는 것을 목표로 한다.

주요 수행 내용은 다음과 같다:
- 터미널을 이용한 파일 및 디렉토리 생성, 관리 및 권한 설정
- Docker 설치 확인 및 컨테이너 실행 검증
- Dockerfile을 통한 커스텀 이미지 생성
- 웹 서버 실행 및 포트 매핑을 통한 외부 접근 확인
- 바인드 마운트 및 Docker Volume을 통한 데이터 관리 및 영속성 검증
- Git/GitHub를 이용한 버전 관리 및 원격 저장소 연동

# 실행 환경
- OS: macOS 15.7.4
- Shell: zsh
- Terminal: macOS Terminal | Apple_Terminal
- Docker:  28.5.2
- Git: 2.53.0

# 수행 항목 체크리스트
- [x] 터미널 파일/디렉토리 작업 수행
- [x] 파일 권한 변경 실습
- [x] Docker 설치 및 동작 확인
- [x] hello-world 컨테이너 실행
- [x] ubuntu 컨테이너 내부 명령 실행
- [x] Dockerfile 작성 및 이미지 빌드
- [x] 웹 서버 실행 및 포트 매핑 확인
- [x] 바인드 마운트 적용 및 반영 확인
- [x] Docker Volume 생성 및 영속성 검증

# 수행 로그

## 파일 및 디렉토리 생성 및 관리
```bash
inuseforstudies0516@c4r9s7 ~ % pwd
/Users/inuseforstudies0516
inuseforstudies0516@c4r9s7 ~ % ls -la
total 40
drwxr-x---+ 20 inuseforstudies0516  inuseforstudies0516   640 Apr  2 15:13 .
drwxr-xr-x   8 root                 admin                 256 Mar 31 17:03 ..
-r--------   1 inuseforstudies0516  inuseforstudies0516     7 Mar 31 17:03 .CFUserTextEncoding
-rw-r--r--@  1 inuseforstudies0516  inuseforstudies0516  8196 Apr  1 17:43 .DS_Store
drwx------+  2 inuseforstudies0516  inuseforstudies0516    64 Mar 31 17:04 .Trash
drwxr-xr-x   5 inuseforstudies0516  inuseforstudies0516   160 Mar 31 17:04 .docker
drwxr-xr-x  10 inuseforstudies0516  inuseforstudies0516   320 Apr  2 14:02 .orbstack
drwxr-xr-x   3 inuseforstudies0516  inuseforstudies0516    96 Mar 31 17:04 .ssh
drwxr-xr-x   3 inuseforstudies0516  inuseforstudies0516    96 Mar 31 17:04 .vscode
-rw-------   1 inuseforstudies0516  inuseforstudies0516     2 Mar 31 20:45 .zsh_history
drwx------  12 inuseforstudies0516  inuseforstudies0516   384 Apr  2 15:13 .zsh_sessions
drwx------+  3 inuseforstudies0516  inuseforstudies0516    96 Mar 31 17:03 Desktop
drwx------+  3 inuseforstudies0516  inuseforstudies0516    96 Mar 31 17:03 Documents
drwx------+  3 inuseforstudies0516  inuseforstudies0516    96 Mar 31 17:03 Downloads
drwx------@ 80 inuseforstudies0516  inuseforstudies0516  2560 Apr  1 14:25 Library
drwx------   4 inuseforstudies0516  inuseforstudies0516   128 Apr  1 13:59 Movies
drwx------+  3 inuseforstudies0516  inuseforstudies0516    96 Mar 31 17:03 Music
drwx------   4 inuseforstudies0516  inuseforstudies0516   160 Apr  2 14:02 OrbStack
drwx------+  4 inuseforstudies0516  inuseforstudies0516   128 Mar 31 17:03 Pictures
drwxr-xr-x+  4 inuseforstudies0516  inuseforstudies0516   128 Mar 31 17:03 Public
inuseforstudies0516@c4r9s7 ~ % mkdir project-1
inuseforstudies0516@c4r9s7 ~ % cd project-1
inuseforstudies0516@c4r9s7 project-1 % touch hello.txt
inuseforstudies0516@c4r9s7 project-1 % echo "안녕하세요" > hello.txt    
inuseforstudies0516@c4r9s7 project-1 % cat hello.txt
안녕하세요
inuseforstudies0516@c4r9s7 project-1 % cp hello.txt hello-copy.txt
inuseforstudies0516@c4r9s7 project-1 % mv hello-copy.txt hello-renamed.txt
inuseforstudies0516@c4r9s7 project-1 % rm hello-renamed.txt
inuseforstudies0516@c4r9s7 project-1 % ls -la
total 8
drwxr-xr-x   3 inuseforstudies0516  inuseforstudies0516   96 Apr  2 15:17 .
drwxr-x---+ 21 inuseforstudies0516  inuseforstudies0516  672 Apr  2 15:15 ..
-rw-r--r--   1 inuseforstudies0516  inuseforstudies0516   16 Apr  2 15:16 hello.txt
inuseforstudies0516@c4r9s7 project-1 % 
```

## 파일 및 디렉토리 권한 변경
```bash
inuseforstudies0516@c4r9s7 project-1 % ls -l hello.txt
-rw-r--r--  1 inuseforstudies0516  inuseforstudies0516  16 Apr  2 15:16 hello.txt
inuseforstudies0516@c4r9s7 project-1 % chmod 755 hello.txt
inuseforstudies0516@c4r9s7 project-1 % ls -l hello.txt
-rwxr-xr-x  1 inuseforstudies0516  inuseforstudies0516  16 Apr  2 15:16 hello.txt
inuseforstudies0516@c4r9s7 project-1 % ls -ld app
drwxr-xr-x  3 inuseforstudies0516  inuseforstudies0516  96 Apr  2 15:33 app
inuseforstudies0516@c4r9s7 project-1 % chmod 700 app 
inuseforstudies0516@c4r9s7 project-1 % ls -ld app
drwx------  3 inuseforstudies0516  inuseforstudies0516  96 Apr  2 15:33 app
inuseforstudies0516@c4r9s7 project-1 % chmod 755 app
inuseforstudies0516@c4r9s7 project-1 % ls -ld app
drwxr-xr-x  3 inuseforstudies0516  inuseforstudies0516  96 Apr  2 15:33 app
```

## Docker 설치 및 환경 확인
```bash
inuseforstudies0516@c4r9s7 project-1 % docker --version
Docker version 28.5.2, build ecc6942
inuseforstudies0516@c4r9s7 project-1 % docker info
Client:
 Version:    28.5.2
 Context:    orbstack
 Debug Mode: false
 Plugins:
  buildx: Docker Buildx (Docker Inc.)
    Version:  v0.29.1
    Path:     /Users/inuseforstudies0516/.docker/cli-plugins/docker-buildx
  compose: Docker Compose (Docker Inc.)
    Version:  v2.40.3
    Path:     /Users/inuseforstudies0516/.docker/cli-plugins/docker-compose
Server:
 Containers: 0
  Running: 0
  Paused: 0
  Stopped: 0
 Images: 0
 Server Version: 28.5.2
 Storage Driver: overlay2
  Backing Filesystem: btrfs
  Supports d_type: true
  Using metacopy: false
  Native Overlay Diff: true
  userxattr: false
 Logging Driver: json-file
 Cgroup Driver: cgroupfs
 Cgroup Version: 2
 Plugins:
  Volume: local
  Network: bridge host ipvlan macvlan null overlay
  Log: awslogs fluentd gcplogs gelf journald json-file local splunk syslog
 CDI spec directories:
  /etc/cdi
  /var/run/cdi
 Swarm: inactive
 Runtimes: io.containerd.runc.v2 runc
 Default Runtime: runc
 Init Binary: docker-init
 containerd version: 1c4457e00facac03ce1d75f7b6777a7a851e5c41
 runc version: d842d7719497cc3b774fd71620278ac9e17710e0
 init version: de40ad0
 Security Options:
  seccomp
   Profile: builtin
  cgroupns
 Kernel Version: 6.17.8-orbstack-00308-g8f9c941121b1
 Operating System: OrbStack
 OSType: linux
 Architecture: x86_64
 CPUs: 6
 Total Memory: 15.67GiB
 Name: orbstack
 ID: 1a58b121-66ac-42be-b4fa-1d6f57271301
 Docker Root Dir: /var/lib/docker
 Debug Mode: false
 Experimental: false
 Insecure Registries:
  ::1/128
  127.0.0.0/8
 Live Restore Enabled: false
 Product License: Community Engine
 Default Address Pools:
   Base: 192.168.97.0/24, Size: 24
   Base: 192.168.107.0/24, Size: 24
   Base: 192.168.117.0/24, Size: 24
   Base: 192.168.147.0/24, Size: 24
   Base: 192.168.148.0/24, Size: 24
   Base: 192.168.155.0/24, Size: 24
   Base: 192.168.156.0/24, Size: 24
   Base: 192.168.158.0/24, Size: 24
   Base: 192.168.163.0/24, Size: 24
   Base: 192.168.164.0/24, Size: 24
   Base: 192.168.165.0/24, Size: 24
   Base: 192.168.166.0/24, Size: 24
   Base: 192.168.167.0/24, Size: 24
   Base: 192.168.171.0/24, Size: 24
   Base: 192.168.172.0/24, Size: 24
   Base: 192.168.181.0/24, Size: 24
   Base: 192.168.183.0/24, Size: 24
   Base: 192.168.186.0/24, Size: 24
   Base: 192.168.207.0/24, Size: 24
   Base: 192.168.214.0/24, Size: 24
   Base: 192.168.215.0/24, Size: 24
   Base: 192.168.216.0/24, Size: 24
   Base: 192.168.223.0/24, Size: 24
   Base: 192.168.227.0/24, Size: 24
   Base: 192.168.228.0/24, Size: 24
   Base: 192.168.229.0/24, Size: 24
   Base: 192.168.237.0/24, Size: 24
   Base: 192.168.239.0/24, Size: 24
   Base: 192.168.242.0/24, Size: 24
   Base: 192.168.247.0/24, Size: 24
   Base: fd07:b51a:cc66:d000::/56, Size: 64
WARNING: DOCKER_INSECURE_NO_IPTABLES_RAW is set
```

## hello-world 컨테이너 실행
```bash
inuseforstudies0516@c4r9s7 project-1 % docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
4f55086f7dd0: Pull complete 
Digest: sha256:452a468a4bf985040037cb6d5392410206e47db9bf5b7278d281f94d1c2d0931
Status: Downloaded newer image for hello-world:latest
Hello from Docker!
This message shows that your installation appears to be working correctly.
To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash
Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/
For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

## Ubuntu 컨테이너 실행 및 내부 명령 수행
```bash
inuseforstudies0516@c4r9s7 project-1 % docker run -it ubuntu bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
817807f3c64e: Pull complete 
Digest: sha256:186072bba1b2f436cbb91ef2567abca677337cfc786c86e107d25b7072feef0c
Status: Downloaded newer image for ubuntu:latest
root@7fe8f9374a65:/# ls; echo "Inside a container" ; exit
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
Inside a container
exit
```

## Docker 이미지 및 컨테이너 상태 확인
```bash
inuseforstudies0516@c4r9s7 project-1 % docker images
REPOSITORY    TAG       IMAGE ID       CREATED       SIZE
hello-world   latest    e2ac70e7319a   9 days ago    10.1kB
ubuntu        latest    f794f40ddfff   5 weeks ago   78.1MB
inuseforstudies0516@c4r9s7 project-1 % docker ps -a
CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES
7fe8f9374a65   ubuntu        "bash"     5 minutes ago   Exited (0) 4 minutes ago             distracted_hodgkin
70b1eb37c37f   hello-world   "/hello"   7 minutes ago   Exited (0) 7 minutes ago             intelligent_jang
inuseforstudies0516@c4r9s7 project-1 % docker logs 7fe8f9374a65
root@7fe8f9374a65:/# ls; echo "Inside a container" ; exit
bin  boot  dev  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
Inside a container
exit
inuseforstudies0516@c4r9s7 project-1 % docker stats --no-stream
CONTAINER ID   NAME      CPU %     MEM USAGE / LIMIT   MEM %     NET I/O   BLOCK I/O   PIDS
```

## 프로젝트 구조 및 웹 서버 파일 작성
```bash
inuseforstudies0516@c4r9s7 project-1 % mkdir -p project-1/app
inuseforstudies0516@c4r9s7 project-1 % cd project-1
inuseforstudies0516@c4r9s7 project-1 % open .
```

```bash
app/index.html
<!DOCTYPE html>
<html>
  <head>
      <title>PROJECT 1</title>
  </head>
  <body>
      <h1>Docker 웹서버</h1>
      <p>포트 매핑 성공</p>
  </body>
</html>
```

```bash
Dockerfile

FROM nginx:alpine
COPY app/index.html /usr/share/nginx/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

## Docker 이미지 빌드
```bash
inuseforstudies0516@c4r9s7 project-1 % docker build -t project-1-webserver .
[+] Building 11.9s (7/7) FINISHED                                                                   docker:orbstack
 => [internal] load build definition from Dockerfile                                                           0.2s
 => => transferring dockerfile: 152B                                                                           0.0s
 => [internal] load metadata for docker.io/library/nginx:alpine                                                6.3s
 => [internal] load .dockerignore                                                                              0.2s
 => => transferring context: 2B                                                                                0.0s
 => [internal] load build context                                                                              0.2s
 => => transferring context: 242B                                                                              0.0s
 => [1/2] FROM docker.io/library/nginx:alpine@sha256:e7257f1ef28ba17cf7c248cb8ccf6f0c6e0228ab9c315c152f9c203c  4.4s
 => => resolve docker.io/library/nginx:alpine@sha256:e7257f1ef28ba17cf7c248cb8ccf6f0c6e0228ab9c315c152f9c203c  0.2s
 => => sha256:91d1c9c22f2c631288354fadb2decc448ce151d7a197c167b206588e09dcd50a 626B / 626B                     0.7s
 => => sha256:e7257f1ef28ba17cf7c248cb8ccf6f0c6e0228ab9c315c152f9c203cd34cf6d1 10.33kB / 10.33kB               0.0s
 => => sha256:7e89aa6cabfc80f566b1b77b981f4bb98413bd2d513ca9a30f63fe58b4af6903 2.50kB / 2.50kB                 0.0s
 => => sha256:d5030d429039a823bef4164df2fad7a0defb8d00c98c1136aec06701871197c2 12.32kB / 12.32kB               0.0s
 => => sha256:589002ba0eaed121a1dbf42f6648f29e5be55d5c8a6ee0f8eaa0285cc21ac153 3.86MB / 3.86MB                 1.3s
 => => sha256:8892f80f46a05d59a4cde3bcbb1dd26ed2441d4214870a4a7b318eaa476a0a54 1.87MB / 1.87MB                 1.0s
 => => sha256:cf1159c696ee2a72b85634360dbada071db61bceaad253db7fda65c45a58414c 953B / 953B                     1.3s
 => => sha256:3f4ad4352d4f91018e2b4910b9db24c08e70192c3b75d0d6fff0120c838aa0bb 402B / 402B                     1.9s
 => => extracting sha256:589002ba0eaed121a1dbf42f6648f29e5be55d5c8a6ee0f8eaa0285cc21ac153                      0.1s
 => => sha256:c2bd5ab177271dd59f19a46c214b1327f5c428cd075437ec0155ae71d0cdadc1 1.21kB / 1.21kB                 1.8s
 => => extracting sha256:8892f80f46a05d59a4cde3bcbb1dd26ed2441d4214870a4a7b318eaa476a0a54                      0.1s
 => => sha256:4d9d41f3822d171ccc5f2cdfd75ad846ac4c7ed1cd36fb998fe2c0ce4501647b 1.40kB / 1.40kB                 1.9s
 => => extracting sha256:91d1c9c22f2c631288354fadb2decc448ce151d7a197c167b206588e09dcd50a                      0.0s
 => => extracting sha256:cf1159c696ee2a72b85634360dbada071db61bceaad253db7fda65c45a58414c                      0.0s
 => => extracting sha256:3f4ad4352d4f91018e2b4910b9db24c08e70192c3b75d0d6fff0120c838aa0bb                      0.0s
 => => sha256:3370263bc02adcf5c4f51831d2bf1d54dbf9a6a80b0bf32c5c9b9400630eaa08 20.25MB / 20.25MB               2.8s
 => => extracting sha256:c2bd5ab177271dd59f19a46c214b1327f5c428cd075437ec0155ae71d0cdadc1                      0.0s
 => => extracting sha256:4d9d41f3822d171ccc5f2cdfd75ad846ac4c7ed1cd36fb998fe2c0ce4501647b                      0.0s
 => => extracting sha256:3370263bc02adcf5c4f51831d2bf1d54dbf9a6a80b0bf32c5c9b9400630eaa08                      0.4s
 => [2/2] COPY app/index.html /usr/share/nginx/html/index.html                                                 0.2s
 => exporting to image                                                                                         0.2s
 => => exporting layers                                                                                        0.1s
 => => writing image sha256:d5d5dd82bfa73a1751b594c3e1d62ec56f1cae2abe155b1bc478ab8d9eb02413                   0.0s
 => => naming to docker.io/library/project-1-webserver     

inuseforstudies0516@c4r9s7 project-1 % docker images
REPOSITORY            TAG       IMAGE ID       CREATED              SIZE
project-1-webserver   latest    d5d5dd82bfa7   About a minute ago   62.2MB
hello-world           latest    e2ac70e7319a   9 days ago           10.1kB
ubuntu                latest    f794f40ddfff   5 weeks ago          78.1MB
```

## 웹 서버 실행 및 포트 매핑 확인
```bash
inuseforstudies0516@c4r9s7 project-1 % docker run -d -p 8080:80 --name test-server project-1-webserver
a6f13fc3372bbe8e46dd07359f33c984284bacdf2d0906d03b9fd7ef82940ece
inuseforstudies0516@c4r9s7 project-1 % docker ps
CONTAINER ID   IMAGE                 COMMAND                  CREATED         STATUS         PORTS                                     NAMES
a6f13fc3372b   project-1-webserver   "/docker-entrypoint.…"   6 seconds ago   Up 5 seconds   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp   test-server
inuseforstudies0516@c4r9s7 project-1 % curl http://localhost:8080
<!DOCTYPE html>
<html>
   <head>
       <title>PROJECT 1</title>
   </head>
   <body>
       <h1>Docker 웹서버</h1>
       <p>포트 매핑 성공</p>
   </body>
</html>%
```

```bash
inuseforstudies0516@c4r9s7 project-1 % docker rm -f test-server
test-server
inuseforstudies0516@c4r9s7 project-1 % docker build -t project-1-webserver .
[+] Building 2.5s (7/7) FINISHED                                                                    docker:orbstack
 => [internal] load build definition from Dockerfile                                                           0.1s
 => => transferring dockerfile: 152B                                                                           0.0s
 => [internal] load metadata for docker.io/library/nginx:alpine                                                1.6s
 => [internal] load .dockerignore                                                                              0.1s
 => => transferring context: 2B                                                                                0.0s
 => [internal] load build context                                                                              0.1s
 => => transferring context: 269B                                                                              0.0s
 => CACHED [1/2] FROM docker.io/library/nginx:alpine@sha256:e7257f1ef28ba17cf7c248cb8ccf6f0c6e0228ab9c315c152  0.0s
 => [2/2] COPY app/index.html /usr/share/nginx/html/index.html                                                 0.2s
 => exporting to image                                                                                         0.2s
 => => exporting layers                                                                                        0.1s
 => => writing image sha256:7114711b2ac6e0692ebacae4711bc438fe4fe0f96b815b88104c7b07abdbafc6                   0.0s
 => => naming to docker.io/library/project-1-webserver                                                         0.0s
inuseforstudies0516@c4r9s7 project-1 % docker run -d -p 8080:80 --name test-server project-1-webserver
39bc60ddc5282220060d707edd6b427c8104764fe594e53c47e42b890e83ad26
```

## 바인드 마운트 적용 및 실시간 반영 확인
```bash
inuseforstudies0516@c4r9s7 project-1 % docker run -d -p 8081:80 \
  -v $(pwd)/app:/usr/share/nginx/html \
  --name test-server-mount project-1-webserver
303bb300614a7ab982dd217aac2326015286bdc4b765ae0140ddbb6cb9f1b9ce
inuseforstudies0516@c4r9s7 project-1 % 

http://localhost:8081/

echo "<h1>수정됨! 바인드 마운트 성공!</h1>" > app/index.html
```

## Docker Volume 생성 및 데이터 영속성 검증
```bash
inuseforstudies0516@c4r9s7 project-1 % docker volume create web-content
web-content
inuseforstudies0516@c4r9s7 project-1 % docker volume ls
DRIVER    VOLUME NAME
local     web-content
inuseforstudies0516@c4r9s7 project-1 % docker run -d -p 8082:80 \
  -v web-content:/usr/share/nginx/html \
  --name project-1-volume project-1-webserver
6fc972fbce3e7761a7d693e879038833a0ac5744c832e8b857218659bb50bf71
inuseforstudies0516@c4r9s7 project-1 % docker exec project-1-volume  sh -c \
  "echo '<h1>볼륨 테스트\!</h1>' > /usr/share/nginx/html/volume-test.html"
inuseforstudies0516@c4r9s7 project-1 % docker exec project-1-volume ls /usr/share/nginx/html/
50x.html
index.html
volume-test.html

inuseforstudies0516@c4r9s7 project-1 % docker exec project-1-volume sh -c "echo '<html><head><meta charset=\"UTF-8\"></head><body><h1>볼륨 테스트\!</h1></body></html>' > /usr/share/nginx/html/volume-test.html"
```

```bash
inuseforstudies0516@c4r9s7 project-1 % docker stop project-1-volume
project-1-volume
inuseforstudies0516@c4r9s7 project-1 % docker rm project-1-volume
project-1-volume
inuseforstudies0516@c4r9s7 project-1 % docker run -d -p 8083:80 \
  -v web-content:/usr/share/nginx/html \
  --name project-1-volume2 project-1-webserver
fc04a3d89f3173ebd283559bfa53c0e2cb93801ab39069de6e0d403ac6efc5c2
inuseforstudies0516@c4r9s7 project-1 % docker exec project-1-volume2 ls /usr/share/nginx/html/
50x.html
index.html
volume-test.html
```

## Git 초기 설정 및 원격 저장소 연동
```bash
inuseforstudies0516@c4r9s7 project-1 % git config --global user.name "********" 
inuseforstudies0516@c4r9s7 project-1 % git config --global user.email "********@gmail.com"
inuseforstudies0516@c4r9s7 project-1 % git config --global init.defaultBranch main
inuseforstudies0516@c4r9s7 project-1 % git init
Initialized empty Git repository in /Users/inuseforstudies0516/project-1/project-1/.git/
inuseforstudies0516@c4r9s7 project-1 % git add .
inuseforstudies0516@c4r9s7 project-1 % git commit -m "PROJECT 1: 개발 워크스테이션 구축"
[main (root-commit) b3482cc] PROJECT 1: 개발 워크스테이션 구축
 3 files changed, 15 insertions(+)
 create mode 100644 .DS_Store
 create mode 100644 Dockerfile
 create mode 100644 app/index.html
inuseforstudies0516@c4r9s7 project-1 % git config --list
credential.helper=osxkeychain
user.name=********
user.email=********@gmail.com
init.defaultbranch=main
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
core.ignorecase=true
core.precomposeunicode=true
inuseforstudies0516@c4r9s7 project-1 % git remote add origin https://github.com/********/project-1.git
inuseforstudies0516@c4r9s7 project-1 % git push -u origin main
Username for 'https://github.com': ********
Password for 'https://********@github.com': 
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 6 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (6/6), 875 bytes | 875.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/********/project-1.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

## Docker Compose 실행 및 관리
```bash
inuseforstudies0516@c4r9s7 project-1 % docker compose up -d 
WARN[0000] /Users/inuseforstudies0516/project-1/project-1/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
[+] Running 2/2
 ✔ Network project-1_default        Created                                                                  0.1s 
 ✔ Container project-1-webserver-1  Started                                                                  0.4s 
inuseforstudies0516@c4r9s7 project-1 % docker compose ps
WARN[0000] /Users/inuseforstudies0516/project-1/project-1/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
NAME                    IMAGE                 COMMAND                  SERVICE     CREATED          STATUS          PORTS
project-1-webserver-1   project-1-webserver   "/docker-entrypoint.…"   webserver   19 seconds ago   Up 18 seconds   0.0.0.0:8090->80/tcp, [::]:8090->80/tcp
inuseforstudies0516@c4r9s7 project-1 % docker compose logs
WARN[0000] /Users/inuseforstudies0516/project-1/project-1/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
webserver-1  | /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
webserver-1  | /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
webserver-1  | /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
webserver-1  | 10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
webserver-1  | 10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
webserver-1  | /docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
webserver-1  | /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
webserver-1  | /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
webserver-1  | /docker-entrypoint.sh: Configuration complete; ready for start up
webserver-1  | 2026/04/02 08:44:21 [notice] 1#1: using the "epoll" event method
webserver-1  | 2026/04/02 08:44:21 [notice] 1#1: nginx/1.29.7
webserver-1  | 2026/04/02 08:44:21 [notice] 1#1: built by gcc 15.2.0 (Alpine 15.2.0) 
webserver-1  | 2026/04/02 08:44:21 [notice] 1#1: OS: Linux 6.17.8-orbstack-00308-g8f9c941121b1
webserver-1  | 2026/04/02 08:44:21 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 20480:1048576
webserver-1  | 2026/04/02 08:44:21 [notice] 1#1: start worker processes
webserver-1  | 2026/04/02 08:44:21 [notice] 1#1: start worker process 30
webserver-1  | 2026/04/02 08:44:21 [notice] 1#1: start worker process 31
webserver-1  | 2026/04/02 08:44:21 [notice] 1#1: start worker process 32
webserver-1  | 2026/04/02 08:44:21 [notice] 1#1: start worker process 33
webserver-1  | 2026/04/02 08:44:21 [notice] 1#1: start worker process 34
webserver-1  | 2026/04/02 08:44:21 [notice] 1#1: start worker process 35
inuseforstudies0516@c4r9s7 project-1 % docker compose down
WARN[0000] /Users/inuseforstudies0516/project-1/project-1/docker-compose.yml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
[+] Running 2/2
 ✔ Container project-1-webserver-1  Removed                                                                  0.3s 
 ✔ Network project-1_default        Removed 

inuseforstudies0516@c4r9s7 project-1 % git add .
inuseforstudies0516@c4r9s7 project-1 % git commit -m "Added docker-compose configuration"
[main 4f7bc7d] Added docker-compose configuration
 1 file changed, 8 insertions(+)
 create mode 100644 docker-compose.yml
inuseforstudies0516@c4r9s7 project-1 % git push origin main
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 6 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 407 bytes | 407.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/********/project-1.git
   b3482cc..4f7bc7d  main -> main
```




