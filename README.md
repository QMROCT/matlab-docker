## [Docker](https://www.docker.io/) Image with [Matlab Compiler Runtime](http://www.mathworks.de/products/compiler/mcr/)

This image is used to inject code via SSH and execute Matlab scripts on medical images inside a shielded environment. It runs Ubuntu 12.04 and MCR 2013b.

### Usage

Replace `id_rsa.pub` with with your public key.

```bash
git clone https://github.com/QMROCT/matlab-docker
cd matlab-docker

docker build -t matlab-image .

docker run -d -P --name matlab-container matlab-image

PORT=`docker port matlab-container 22 | cut -d: -f2`
IP=`ifconfig docker0 | grep 'inet addr:' | cut -d: -f2 | awk '{print $1}'`
ssh root@$IP -p $PORT
```

### Thanks
This repo is based on [docker-matlab-mcr](https://github.com/colin-rhodes/docker-matlab-mcr).