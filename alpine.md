# docker Alpine & dotnet container

```bash
docker pull microsoft/dotnet:2.2-runtime-deps-alpine3.8
# first time create a container and open a shell
docker run -it --name alpy3 microsoft/dotnet:2.2-runtime-deps-alpine3.8 /bin/sh
# afterwards start the container and open a shell
docker start -i alpy3
```

# configure docker container via shell and apk add

Start the container and open a terminal

```sh
docker start -i alpy3
```

On the containerized image

```sh
hostname
ls
apk add npm
apk add vim
apk add git
pwd
cd .
pwd
ls -a
ls usr/bin/node
ls usr/lib/node_modules/
npm
cd root/
mkdir myapp
cd myapp/
npm init
touch
touch server.js
vim server.js
# console.log('an npm server/');;
npm start
cd ../
git clone https://github.com/rjminchuk/bbsuite.git
```

# dockerfile for alpine & dotnet core 2.1

A dockerfile for bootstrapping a docker image.

`consoleapp/dockerfile.alpine`

```
FROM microsoft/dotnet:2.1-runtime-alpine3.7

#############################################################
# my code below

RUN mkdir -p /root/src/app/docker-console
WORKDIR /root/src/app/docker-console

COPY ./app/alpine ./
ENTRYPOINT ["dotnet", "docker-console.dll"]
# CMD ["-c"]

RUN echo "finished docker build"
```

# Creating a custome docker image with a docker file

```bash
cd ~/source/dotnet-console
dotnet publish -c Release -o app/alpine -r alpine.3.7-x64
docker build -t alpine-console -f dockerfile.alpine .
# docker rm alpine-container 
docker run -it --name alpine-container alpine-console /bin/sh
docker start alpine-container
```