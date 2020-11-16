## Terms

- _Docker_ is a platform that packages an application and all its dependencies together in the form of containers.
- _Dockerfile_ is a text document that contains all the commands that a user can call on the command line to assemble an image.
- _Docker image_ - a read-only template with instructions for creating a Docker container. It is a combination of file system and parameters.
- _Docker container_ - a runnable instance of docker image. A container is isolated from the host by default.
- _Docker Compose_ is a YAML file that contains details about the services, networks, and volumes for setting up the Docker application. It can be used to create separate containers, host them, and get them to communicate with each other. Each container will expose a port for communicating with other containers.
- _Docker Swarm_ is a technique to create and maintain a cluster of Docker engines. The Docker engines can be hosted on different nodes, and these nodes, which are in remote locations, form a cluster when connected in swarm mode.

## Commands

Common syntax `docker COMMAND SUBCOMMAND`

- download a docker image
  \*\* we can use pull command to get an image `docker pull [OPTIONS] [PATH/]IMAGE_NAME[:TAG]`

```
docker pull hello-world
docker pull hello-world:latest
```

If a registry is password protected, you should log in to it before pulling 'docker login REGISTRY_SERVER:REGISTRY_PORT'

\*\* create a container — when we create a container from an image, it downloads the image from the repository if it is not available in the host.

```
docker run hello-world
```

- `docker image ls` — list available images
- `docker image rm IMAGE_NAME`
- `docker image remove IMAGE_NAME` — remove an image
- `docker image inspect IMAGE_NAME` — inspect an image
- list containers
  - `docker container ls` - lis of running containers
  - `docker container ls -a` - list of all available containers
- `docker container run CONTAINER_NAME` — run a container
- `docker container start CONTAINER_NAME` — start a stopped container
- `docker container stop CONTAINER_NAME` — stop a running container
- `docker container rm CONTAINER_NAME` — remove a container

## Deploy a Spring Boot application

- create image file for application. Create new file `Dockerfile.txt`. Docker reads commands/instructions from "Dockerfile.txt" and builds the image. It is a simple text file with all the instructions required to build the image.

Example1:

```
FROM java:8
EXPOSE 8100
ADD /target/application-0.0.1-SNAPSHORT.jar my-docker-application.jar
ENTRYPOINT ["java","-jar","my-docker-application.jar"]
```

Details:

- `FROM java:8` means this is a Java application and will require all the Java libraries so it will pull all the Java-related libraries and add them to the container.
- `EXPOSE PORT_NUMBER` means that we would like to expose PORT_NUMBER to the outside world to access our application.
- template `ADD <source from where Docker should create the image> <destination>`
- ENTRYPOINT ["java", "-jar", "docker-application.jar"] will run the command as the entry point as this is a JAR and we need to run this JAR from within Docker.

Example2:

```
FROM java:8
VOLUME /tmp
ARG JAR_FILE
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
```

- build image via Docker `docker build -t my-docker-application`
  - with the concrete file 'docker build -f Dockerfile -t my-docker-application`
- check that an image is created `docker images`
- push this image to Docker `docker run -p 8100:8100 -t my-docker-application`
- check the running container `docker ps -a`

## Analyze Code Quality With Sonarqube and Docker

- Download Sonar from DockerHub

```
docker pull sonarqube
docker run -d --name sonarqube -p 9000:9000 sonarqube
```

- Download Sonar Scanner by using [link](https://docs.sonarqube.org/latest/analysis/scan/sonarscanner/)
- Unzip Sonar Scanner and Link the Sonarqube
  \*\* go to \$sonarscanner_install_dir/conf/sonar-scanner.properties and link the host and port on which your Sonar installation is running.
  F.e., if it is on localhost and port 9000 as mentioned in docker run then

```
sonar.host.url=http://localhost:9000
```

- Start Analyzing the Source Code
  the source code directory should be placed in the current folder and run the following command:
  `sonar-scanner -Dsonar.projectKey=<Project Name> -Dsonar.sources=<Project Src Directory>`

## Run databases via Docker

### Run Postgres as docker container

- download docker image

```
$ pull postgres:11
```

- run postgres container with database port and user password

```
$ docker run --name dev-postgres -p 5432:5432 -e POSTGRES_PASSWORD=postgres -d postgres:11
```

- create database 'dailyqa' for user 'postgres'

```
$ docker exec dev-postgres psql -U postgres -c "create database dailyqa" postgres
```

## Run Oracle as docker container

- login to Docker hub with your Docker account information with the below command

```
$ docker login
```

- Use the below command to install Oracle 12c image from Docker Hub.

```
$ docker run -d -p 1521:1521 --name OracleDB store/oracle/database-enterprise:12.2.0.1-slim
```

- to start and mount the database.

```
$ docker exec -it OracleDB bash -c "source /home/oracle/.bashrc; sqlplus /nolog"
```

- start working on DB

```
connect sys as sysdba;
-- Here enter the password as 'Oradoc_db1'
alter session set "_ORACLE_SCRIPT"=true;
create user dummy identified by dummy;
GRANT CONNECT, RESOURCE, DBA TO dummy;
--Now create a sample table.
create table Docker (id int,name varchar2(20));
--Start inserting values in to the table
```

- Below are the details of the installed database:

  - HostName: localhost (hostname will be System IP address if you installed in any Linux VM)

  - Port: 1521

  - UserName and Password: dummy

  - Service Name: ORCLCDB.localdomain

  - Use the below command to get the Service Name of the DB installed.

```
select value from v$parameter where name='service_names';
```

## Docker commands

- [Official docker images](https://github.com/docker-library/official-images/tree/master/library)


### Clean the system

- `docker image prune` to clean up just "dangling" images
- `docker image prune -a` which will remove all images you're not using.
- `docker system prune` will clean up everything
- `docker system df` to see space usage.

### Check setup

- `docker version`
- `docker info`
- `docker-machine version`

- `docker-machine ls`
- `docker-machine start`
- `docker-machine env default`
- `docker-compose version`

### docker container
- `set FORMAT="table {{.ID}}\t{{.Repository}}\t{{.Tag}}\t{{.Size}}"` to define variable with format
- `docker image list --format %FORMAT%`  to list the images with format
- `docker container ls` list running containers
- `docker container ls -a` list all containers
- `docker container ls -q/ --quiet ` list only container IDs
- `docker container run`
- `docker container run --publish 80:80 nginx`
- `docker container run --publish 80:80 --detach nginx`
- `docker container run --publish 80:80 --detach --name webhost nginx`
- `docker run --name mongo -d mongo`
- `docker container run -d -p 3306:3306 --name db -e MYSQL_RANDOM_ROOT_PASSWORD=yes MYSQL_RANDOM_ROOT_PASSWORD`
- `docker container run -d --name mysql -e MYSQL_RANDOM_ROOT_PASSWORD=true mysql`
- `docker container run -d --name webserver -p 8080:80 httpd`
- `docker container run -d --name proxy -p 80:80 nginx`
- `docker container run -it alpine bash`
- `docker container run -it alpine sh`
- `docker container run --rm -p 80:3000 dma1979/testing-node` - run own dma1979 image from repo
- `docker container start CONAINER_ID`
- `docker container start -ai CONAINER_ID`
- `docker container stop CONAINER_ID` or `docker stop CONAINER_ID` stop the container
- `docker stop $(docker ps -a -q)` remove all RUNNING containers
- `docker kill $(docker ps -q)` kill all RUNNING containers
- `docker container stop TAB COMPLETION`
- `docker container top CONTAINER_ID` info about running container(time, pid an etc.)
- `docker container top CONTAINER_NAME`
- `docker container rm C_ID C_ID2 C_ID3...` or `docker rm C_ID C_ID2 C_ID3...` remove containers
- `docker container rm -f C_ID C_ID2 C_ID3...` remove containers with 'FORCE'
- `docker container rm -f TAB COMPLETION`
- `docker rm $(docker ps -a -q)` remove all stopped containers
- `docker container logs CONTAINER_NAME`
- `docker container inspect CONTAINER_NAME`
- `docker container inspect --format '{{ .NetworkSettings.IPAddress }}' bridge`
- `docker container stats CONTAINER_NAME`
- `docker container run -it --name proxy nginx bash` with the shell inside container
- `docker container run -it --name ubuntu ubuntu`
- `docker container exec -it mysql bash`

### docker image

- `docker image ls` list image
- `docker rmi IMAGE_ID` remove image
- `docker rmi $(docker images -q)` remove all images
- `docker pull IMAGE_NAME`
- `docker pull alpine`
- `docker pull nginx`
- `docker pull nginx:1.11.9`
- `docker pull mongo`
- `docker image inspect nginx`
- `docker image push dma1979/nginx`
- `docker image push dma1979/nginx bretfisher/nginx:testing`
- `docker image push dma1979/nginx:testing`
- `docker image build -t customnginx .`
- `docker image build -t nginx-with-html .`
- `docker image tag nginx dma1979/nginx`
- `docker image tag nginx-with-html:latest dma1979/nginx-with-html:latest`

### networking

- `docker network ls`
- `docker network inspect bridge`
- `docker network create my_app_net`
- `docker container run -d --name new_nginx --network my_app_net nginx`
- `docker network inspect my_app_net`
- `docker network connect TAB COMPLETION`
- `docker container inspect TAB COMPLETION`
- `docker container disconnect TAB COMPLETION`

- `docker container exec -it my_nginx ping new_nginx`
- `docker container exec -it new_nginx ping my_nginx`

- `docker network create my_net`
- `docker container run -d --net my_net --net-alias search elasticsearch:2`
- `docker container run --rm -- net my_net alpine nslookup search`
- `docker container run --rm --net dude centos curl -s search:9200`

- `docker history nginx:latest`
- `docker history mysql`

### volumes
- `docker volume ls` list volumes
