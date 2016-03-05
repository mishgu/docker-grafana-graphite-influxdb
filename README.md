# Install dokcer
When you want know if you have docker you need:

    $ docker -v
    Docker version 1.10.2, build c3959b1

If you don't have dokcer you need [Install Docker](https://docs.docker.com/engine/installation/linux/ubuntulinux/)
# Usage
Install image influxdb:
    $ docker pull msha/influxdb
    $ docker run -d -p 8083:8083 -p 8086:8086 --name influxdb msha/influxdb

