# DevOps-Project-kubernetes-tomcat-session-replication

![image](https://github.com/user-attachments/assets/cb191728-541f-4417-a1a3-d03e9a69e0f1)

This project explains tomcat based session replication in Kubernetes. To achieve this I have used redission based session replication. 
```
I have added below section in context.xml as shown in the screeshot below.


    <Manager className="org.redisson.tomcat.RedissonSessionManager"
    configPath="${catalina.base}/redisson.yaml"
    readMode="REDIS" updateMode="DEFAULT" broadcastSessionEvents="false"
    keyPrefix="" />
```
![image](https://github.com/user-attachments/assets/a3811a20-bcaf-40ce-8649-56d62e466e9b)

I have downloaded the jar file **redisson-all-3.22.0.jar** and **redisson-tomcat-8-3.22.0.jar** from the link https://repo1.maven.org/maven2/org/redisson/redisson-all/3.22.0/redisson-all-3.22.0.jar and https://repo1.maven.org/maven2/org/redisson/redisson-tomcat-8/3.22.0/redisson-tomcat-8-3.22.0.jar. Download these two jar files to the lib directory. You can refer the **Dockerfile** as shown in the screenshot below.
```
FROM tomcat:8-jdk11-openjdk 

MAINTAINER "DevOps Team"

ADD https://repo1.maven.org/maven2/org/redisson/redisson-all/3.22.0/redisson-all-3.22.0.jar /usr/local/tomcat/lib/
ADD https://repo1.maven.org/maven2/org/redisson/redisson-tomcat-8/3.22.0/redisson-tomcat-8-3.22.0.jar /usr/local/tomcat/lib/

COPY ./pasco/context.xml /usr/local/tomcat/conf/
COPY ./pasco/redisson.yaml /usr/local/tomcat/

COPY target/ROOT.war /usr/local/tomcat/webapps
```
For Jenkins you should install the plugins 1. SonarQube Scanner 2. Nexus Artifact Uploader and 3. Pipeline Utility Steps as shown in the screenshot below.

![image](https://github.com/user-attachments/assets/049257d8-c588-489f-884e-867783b2f421)

After adding the Jenkins Slave node the screenshot is as shown below.
![image](https://github.com/user-attachments/assets/2438f217-8e88-4a23-9f81-c06edc31279f)

commands to add swap space of 512 MB is given below
```
fallocate -l 512M /swapfile
chmod 600 /swapfile
sudo mkswap /swapfile
cat /etc/fstab

/swapfile swap swap defaults 0 0


swapon /swapfile
free -mh

```
![image](https://github.com/user-attachments/assets/fde8cb3b-fd0a-45db-9463-20194028e5c2)

The screenshot of Jenkins Job is as shown below.
![image](https://github.com/user-attachments/assets/9a1c8797-120b-4421-9b2b-5cc9ff60ce08)

The screenshots of SonarQube, Nexus Artifactory, ArgoCD and Route53 record set entry after successfully running the Jenkins Job is as shown in the screenshot below.
![image](https://github.com/user-attachments/assets/6e66087b-f55f-4208-aa66-168e80680327)
![image](https://github.com/user-attachments/assets/06f851a1-09c0-48ad-aeca-78f23b70ebe8)
![image](https://github.com/user-attachments/assets/927bcf0d-65f4-4c27-b0d2-d0a36da3f05b)
![image](https://github.com/user-attachments/assets/9ff02794-88a1-4a9a-b9fe-43bf7cf4da11)

The Session Id shown in the below screenshot reflects the session replication.
![image](https://github.com/user-attachments/assets/b2a97bce-a5e3-445a-a21b-f4b0051b0928)
![image](https://github.com/user-attachments/assets/3cfb3e84-074d-420b-be93-03212fd7571b)


<br><br/>
<br><br/>
<br><br/>
<br><br/>
<br><br/>
```
Source Code:-  https://github.com/singhritesh85/kubernetes-tomcat-session-replication.git
```
<br><br/>
<br><br/>
<br><br/>
<br><br/>
<br><br/>
```
Reference:-  https://github.com/AndriyKalashnykov/tomcat-root-war.git
             https://redisson.org/articles/redis-based-tomcat-session-management.html
             https://github.com/mahendra-shinde/tomcat7-redisson-session.git
             https://github.com/bitnami/charts.git
```
