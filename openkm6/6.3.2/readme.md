## OpenKM Community

Using the DMS/KM OpenKM open source community edition and tomcat bundled from the official OpenKM website on top of the ubuntu base image and java-jre. Best for using with a MySQL Server image as database backend and a NGINX Image as a reverse proxy. By default OpenKM uses a local database inside the container.

Whats included in this:
 - Ubuntu base image
 - OpenKM 6.3.2 Community (part of the bundle)
 - Tomcat 7.0.xx (part of the bundle)
 - packages: unzip, default-jre, wget

# Tags

```latest```, ```6.3.2``` OpenKM 6.3.2 Community with tomcat 7 (total 909.6MB)
	
# Container Structure

##### Simple schema 

```
Base Image -> Ubuntu
|
 \--- Tomcat Server 7
  \--- OpenKM applet
|--- default-jre, unzip, wget, apt...
```

##### Key folders

Tomcat server -> ```/opt/openkm/tomcat/```
Tomcat webapps -> ```/opt/openkm/tomcat/webapps/```
OpenKM deployment -> ```/opt/openkm/tomcat/webapps/OpenKM/```


##### Key files

```OpenKM.xml```; ```OpenKM.cfg``` -> ```/opt/openkm/tomcat/```
```OpenKM.war``` -> ```/opt/openkm/tomcat/webapps/OpenKM.war```
```web.xml``` -> ```/opt/openkm/tomcat/webapps/OpenKM/WEB-INF/web.xml```
```server.xml```; ```tomcat-users.cml```; ```web.xml```; ```log4j.properties```; ```logging.properties```; ```context.xml``` -> ```/opt/openkm/tomcat/conf/```

##### Default credentials

 - User: ```okmAdmin```
 - Password: ```admin```

# Useful commands for managing this container	

#### Start a new OpenKM6 container

##### Syntax
```sh
docker run -d (AS DEAMON) -p [HOSTIP]:HOSTPORT:CONTAINERPORT --restart="always" REPOSITORY/NAME:VERSION
```

##### Example
```sh
docker run -d -p 8000:8080 --restart="always" eduardomota/openkm6:latest
```


#### Share/mount host filesystem folder to OpenKM to container

##### Syntax
```sh
-v HOSTFILESYSTEMFOLDER:CONTAINERFOLDER
```

##### Example
```sh
docker run '...' -v "/apps/openkm/datashare":"/datashare"
```

#### Root access container while running

```sh
docker exec -it CONTAINERNAME bash
```
OR
```sh
docker exec -it CONTAINERNAME /bin/bash
```

#### Stop server

NOTE: stoping the PID 0 process with shutdown the container

```sh
/opt/openkm/tomcat/bin/catalina.sh stop
```

#### Force stop server

NOTE: stoping the PID 0 process with shutdown the container 

```sh
/opt/openkm/tomcat/bin/catalina.sh stop -force
```

#### Check configuration

NOTE: a misconfigured or crashing tomcat configuration will prevent container from starting.

Always check the configuration after changing tomcat settings or configs

```sh
/opt/openkm/tomcat/bin/catalina.sh configtest
```

#### Install nano text editor

```sh
apt-get install -y nano
```
