# Install dokcer
When you want know if you have docker you need:

    $ docker -v
    Docker version 1.10.2, build c3959b1

If you don't have dokcer you need [Install Docker](https://docs.docker.com/engine/installation/linux/ubuntulinux/)
# Usage
### **Install influxdb image :**

    $ docker pull msha/influxdb
    $ docker run -d -p 8083:8083 -p 8086:8086 --name influxdb msha/influxdb
    $ docker ps
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                            NAMES
    cd27bf330f15        msha/influxdb       "/run.sh"                46 minutes ago      Up 46 minutes       0.0.0.0:8083->8083/tcp, 0.0.0.0:8086->8086/tcp   influxdb
    
`-d`: your container will run in “detached” mode, in the background
`-p`: you assign self port for port container
`--name`: you assign name to container for ease access to container

Create 'graphite' database in influxdb:
![alt text](https://pp.vk.me/c630219/v630219008/27d74/TIeO3GbwMCI.jpg)
Review you database:
![alt text](https://pp.vk.me/c630219/v630219008/27d7e/q4kwFST4h5k.jpg)
If you don't connect to *http://localhost:8083/* you need to check:

    $ docker ps
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                            NAMES
    cd27bf330f15        msha/influxdb       "/run.sh"                46 minutes ago      Up 46 minutes       0.0.0.0:8083->8083/tcp, 0.0.0.0:8086->8086/tcp   influxdb
    
### **Install graphite image :**

    $ docker pull msha/graphite-api
    $ docker run -it --link influxdb:msha/influxdb -d -p 8081:8000 --name graphite msha/graphite-api
    $ docker ps
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                            NAMES
    5096e5312238        msha/graphite-api   "/bin/sh -c 'gunicorn"   41 seconds ago      Up 39 seconds       0.0.0.0:8081->8000/tcp                           graphite
    238f07d20a1b        msha/influxdb       "/run.sh"                7 minutes ago       Up 7 minutes        0.0.0.0:8083->8083/tcp, 0.0.0.0:8086->8086/tcp   influxdb
`-it`: instructs Docker to allocate a pseudo-TTY connected to the container’s stdin
`--link`: add link to another container

##Check connectivity container:

    $ docker exec graphite cat /etc/hosts
    127.0.0.1	localhost
    ...
    172.17.0.3	influxdb cd27bf330f15
    172.17.0.2	155c83f55857
    $ curl http://localhost:8081/metrics/index.json
    []
    
    

    
