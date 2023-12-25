Задача 1: https://hub.docker.com/layers/sirm1ssalot/custom-nginx/1.0.0/images/sha256-bc1ce85465c763c97b560a96ceb1e2b3c45e4bbbd8c6026beac697268b0332b8?context=repo

Задача 2: 
[root@shd2 task1]# docker run -d -p 8080:80 --name SAA-custom-nginx-t2 sirm1ssalot/custom-nginx
7ff7fe513acd25f6961db209b6103e354fb7575d9ba4c73c27398720b585779b
[root@shd2 task1]# docker rename SAA-custom-nginx-t2 custom-nginx-t2
[root@shd2 task1]# date +"%d-%m-%Y %T.%N %Z" && sleep 0.150 && docker ps && ss -tlpn | grep 127.0.0.1:8080  && docker logs custom-nginx-t2 -n1 && docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html
25-12-2023 13:30:54.400893043 MSK
CONTAINER ID   IMAGE                      COMMAND                  CREATED          STATUS          PORTS                                   NAMES
7ff7fe513acd   sirm1ssalot/custom-nginx   "/docker-entrypoint.…"   30 seconds ago   Up 29 seconds   0.0.0.0:8080->80/tcp, :::8080->80/tcp   custom-nginx-t2
[root@shd2 task1]# curl 127.0.0.1:8080
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I will be DevOps Engineer!</h1>
</body>
</html>
[root@shd2 task1]#

Задача 3:
.3 Контейнер остановился, т.к. терминал получил команду завершения процесса.
.10 Во время работы внутри контейнера мы сменили порт, в который идет трансляция nginx, а т.к. при запуске контейнера мы назначили маппинг 8080:80, ни докер ни хостовая система не знают о том, что nginx будет показывать что то на другом порту.
.11 Для актуализации конфигурации требуется поменять настройки контейнера на хосте, в файлах hostconfig.json и config.v2.json, в них нужно указать требуемый маппинг портов, предварительно остановив контейнер и службу docker. После внесения изменений нужно включить службу и контейнер.

HISTORY
На машине:
216  docker attach custom-nginx-t2
  217  docker ps -a
  218  docker ps
  219  docker rm agitated_nash
  220  docker start custom-nginx-t2
  222  docker exec -it custom-nginx-t2 bash
  224  ss -tlpn | grep 127.0.0.1:8080
  225  docker port custom-nginx-t2
  226  curl http://127.0.0.1:8080
  227  docker ps
  228  vim /var/lib/docker/containers/7ff7fe513acd25f6961db209b6103e354fb7575d9ba4c73c27398720b585779b/hostconfig.json
  229  docker stop custom-nginx-t2
  230  docker start custom-nginx-t2
  231  curl http://127.0.0.1:8080
  232  docker port custom-nginx-t2
  233  vim /var/lib/docker/containers/7ff7fe513acd25f6961db209b6103e354fb7575d9ba4c73c27398720b585779b/hostconfig.json
  234  docker stop custom-nginx-t2
  235  vim /var/lib/docker/containers/7ff7fe513acd25f6961db209b6103e354fb7575d9ba4c73c27398720b585779b/hostconfig.json
  236  systemctl stop docker
  237  vim /var/lib/docker/containers/7ff7fe513acd25f6961db209b6103e354fb7575d9ba4c73c27398720b585779b/hostconfig.json
  238  systemctl restart docker
  239  docker start custom-nginx-t2
  240  docker port custom-nginx-t2
  241  docker ps
  242  vim /var/lib/docker/containers/7ff7fe513acd25f6961db209b6103e354fb7575d9ba4c73c27398720b585779b/hostconfig.json
  243  docker port custom-nginx-t2
  244  docker ps
  245  curl http://127.0.0.1:8080
  246  curl http://127.0.0.1:80
  247  curl http://127.0.0.1:81
  248  curl http://127.0.0.1:8080
  249  history
  250  docker exec -it custom-nginx-t2 bash
  251  date +"%d-%m-%Y %T.%N %Z" && sleep 0.150 && docker ps && ss -tlpn | grep 127.0.0.1:8080  && docker logs custom-nginx-t2 -n1 && docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html
  252  docker stop custom-nginx-t2
  253  systemctl stop docker
  254  vim /var/lib/docker/containers/7ff7fe513acd25f6961db209b6103e354fb7575d9ba4c73c27398720b585779b/hostconfig.json
  255  vim /var/lib/docker/containers/7ff7fe513acd25f6961db209b6103e354fb7575d9ba4c73c27398720b585779b/config.v2.json
  256  systemctl restart docker
  257  docker start custom-nginx-t2
  258  docker ps
  259  docker port custom-nginx-t2
  260  curl http://127.0.0.1:8080
265  docker rm -f custom-nginx-t2
В контейнере:
root@7ff7fe513acd:/usr/share/nginx/html# history
    1  apt-get vim
    2  sudo apt-get vim
    3  cat /etc/os-release
    4  apt-get vi
    5  apt-get --help
    6  apt-get install vim
    7  apt-get install vi
    8  apt-get install nano
    9  netstat -tlpn
   10  whoami
   11  apt install vim
   12  cat /etc/apt/sources.list
   13  ping deb.debian.org
   14  curl deb.debian.org
   15  apt install vim
   16  apt-get update
   17  apt-get install vim
   18  vim /etc/nginx/conf.d/default.conf
   19  nginx -s reload
   20  curl http://127.0.0.1:80 && curl http://127.0.0.1:81
   21  curl http://127.0.0.1:81
   22  exit
   23  systemctl status nginx
   24  service nginx status
   25  exit
   26  ss -tlpn
   27  exit
   28  history

Задача 4:
root@1f0d25306687:/data# ls
portal.file  portal2.file

Задача 5:
AppArmorProfile
Args [ nginx, -g, daemon off; ]
Config
AttachStderr true
AttachStdin false
AttachStdout true
Cmd [ nginx, -g, daemon off; ]
Domainname
Entrypoint [ /docker-entrypoint.sh ]
Env [ PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin, NGINX_VERSION=1.21.1, NJS_VERSION=0.6.1, PKG_RELEASE=1~buster ]
ExposedPorts { 80/tcp: [object Object] }
Hostname 35c9c56354be
Image 127.0.0.1:5000/custom-nginx
Labels { com.docker.compose.config-hash: fbb2a6303bfe36ad9081945cde52c6625ca50fc28b5fcb97e9d1fd60cb18aa4b, com.docker.compose.container-number: 1, com.docker.compose.depends_on: , com.docker.compose.image: sha256:1314bd85f85f7f8718403326da668afa8ef33133771935d65a1274389a423465, com.docker.compose.oneoff: False, com.docker.compose.project: pt-w-d, com.docker.compose.project.config_files: /data/compose/1/docker-compose.yml, com.docker.compose.project.working_dir: /data/compose/1, com.docker.compose.service: nginx, com.docker.compose.version: 2.20.2, maintainer: NGINX Docker Maintainers <docker-maint@nginx.com> }
OnBuild
OpenStdin false
StdinOnce false
StopSignal SIGQUIT
Tty false
User
Volumes
WorkingDir /usr/share/nginx/html
Created 2023-12-25T14:02:42.678178459Z
Driver overlay2



.6 После удаления файла docker-compose.yaml, docker compose находит контейнеры, принадлежащие другому проекту с тем же именем. 
