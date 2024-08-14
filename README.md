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
```
