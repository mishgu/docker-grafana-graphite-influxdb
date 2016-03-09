# Install dokcer
When you want know if you have docker you need:

    $ docker -v
    Docker version 1.10.2, build c3959b1

If you don't have dokcer you need [Install Docker](https://docs.docker.com/engine/installation/linux/ubuntulinux/)
# Usage
### **Install influxdb image :**

    $ docker pull msha/influxdb
    $ docker run -d -p 8083:8083 -p 8086:8086 --name influxdb -e PRE_CREATE_DB="graphite" msha/influxdb:0.9
    $ docker ps
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                            NAMES
    cd27bf330f15        msha/influxdb:0.9       "/run.sh"                46 minutes ago      Up 46 minutes       0.0.0.0:8083->8083/tcp, 0.0.0.0:8086->8086/tcp   influxdb
    
* `-d`: your container will run in “detached” mode, in the background
* `-p`: you assign self port for port container
* `--name`: you assign name to container for ease access to container
* `-e` : auto create database with name 'graphite'

### **Influxdb**
You can see influxdb on *http://localhost:8083/* if you don't connect to *http://localhost:8083/* you need to check:

    $ docker ps
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                            NAMES
    cd27bf330f15        msha/influxdb:0.9       "/run.sh"                46 minutes ago      Up 46 minutes       0.0.0.0:8083->8083/tcp, 0.0.0.0:8086->8086/tcp   influxdb
    
### **Install graphite image :**

    $ docker pull msha/graphite-api
    $ docker run -it --link influxdb:msha/influxdb -d -p 8081:8000 --name graphite msha/graphite-api
    $ docker ps
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                            NAMES
    5096e5312238        msha/graphite-api   "/bin/sh -c 'gunicorn"   41 seconds ago      Up 39 seconds       0.0.0.0:8081->8000/tcp                           graphite
    238f07d20a1b        msha/influxdb:0.9       "/run.sh"                7 minutes ago       Up 7 minutes        0.0.0.0:8083->8083/tcp, 0.0.0.0:8086->8086/tcp   influxdb
* `-it`: instructs Docker to allocate a pseudo-TTY connected to the container’s stdin
* `--link`: add link to another container

## Check connectivity container:

    $ docker exec graphite cat /etc/hosts
    127.0.0.1	localhost
    ...
    172.17.0.3	influxdb cd27bf330f15
    172.17.0.2	155c83f55857
    $ curl http://localhost:8081/metrics/index.json
    []
