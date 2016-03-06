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
Create 'graphite' database in influxdb:
![alt text](https://pp.vk.me/c630219/v630219008/27d74/TIeO3GbwMCI.jpg)
Review you database:
![alt text](https://pp.vk.me/c630219/v630219008/27d7e/q4kwFST4h5k.jpg)
If you don't connect to *http://localhost:8083/* you need to check:

    $ docker ps
    CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                            NAMES
    cd27bf330f15        msha/influxdb       "/run.sh"                46 minutes ago      Up 46 minutes       0.0.0.0:8083->8083/tcp, 0.0.0.0:8086->8086/tcp   influxdb
    
### **Install graphite image :**
