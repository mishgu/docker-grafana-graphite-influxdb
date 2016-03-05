# Install dokcer
When you want know if you have docker you need:

    $ docker -v
    Docker version 1.10.2, build c3959b1

If you don't have dokcer you need [Install Docker](https://docs.docker.com/engine/installation/linux/ubuntulinux/)
# Usage
Install influxdb image :

    $ docker pull msha/influxdb
    $ docker run -d -p 8083:8083 -p 8086:8086 --name influxdb msha/influxdb
    $ docker ps
   
CONTAINER ID   IMAGE         COMMAND    CREATED        STATUS         PORTS                                         NAMES
cd27bf330f15   msha/influxdb "/run.sh"  2 minutes ago  Up 2 minutes   0.0.0.0:8083->8083/tcp, 0.0.0.0:8086->8086/tcp   influxdb
Install 
