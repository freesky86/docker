# docker
Spring Boot + Docker   

# Windows环境
https://www.docker.com/  
https://docs.docker.com/desktop/setup/install/windows-install/   

# CentOS环境
安装docker   
sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin   
启动docker   
service docker start    
停止docker   
sudo systemctl stop docker.socket  
sudo systemctl stop docker.service   

# 检查docker
命令行   
docker version   
看到client和server两组信息，说明docker启动成功

# 常见问题
在mainland地区，由于网络问题，有些镜像image不能下载    
比如  
docker pull openjdk:17-jdk-alpine  
解决办法是找一台能连上 https://registry-1.docker.io 的电脑，执行上面的指令，下载image，然后执行   
docker save -o openjdk-17-jdk-alpine.tar openjdk:17-jdk-alpine   
把下载的image打包成tar文件，然后传输到本地，在本地执行下面的命令导入镜像image   
docker load -i openjdk-17-jdk-alpine.tar   
然后，就可以使用docker build命令构建镜像image，比如    
docker build -t spring-boot-demo .    
构建成功后就可以运行Docker容器：   
docker run -p 8080:8080 spring-boot-demo   
后面一个8080是容器的端口，前面一个8080是宿主机的端口，也就是浏览器访问的端口。    

如果想要后台执行，可以加上-d参数，比如    
docker run -d -p 8080:8080 spring-boot-demo  
-d 是--detach的缩写，表示​​以“分离模式”运行容器​​，即让容器在后台运行（类似守护进程的方式）
执行后会返回一个完整的容器ID，实际只需要使用前12位就可以了。

构建好的的镜像，如果想在别的电脑上运行，需要先打包，将构建好的Docker镜像导出为tar文件：    
docker save -o spring-boot-demo.tar spring-boot-demo    
或者   
docker save spring-boot-demo > spring-boot-demo.tar    
  
将spring-boot-demo.tar文件传输到别的电脑上，比如CentOS服务器。   
在CentOS服务器上加载Docker镜像：   
docker load -i spring-boot-demo.tar    
运行Docker容器：  
docker run -p 8080:8080 spring-boot-demo   
在CentOS服务器上访问 http://localhost:8080，或者在其他电脑上用CentOS的IP访问 http://<CentOS IP>:8080    

进入docker容器内部执行指令    
首先执行命令 docker ps 查看正在运行的容器    
然后执行命令 docker exec -it <Container ID/name> /bin/sh    
比如  
docker exec -it 2c9c5e4ada8b /bin/sh   
or    
docker exec -it bold_spence /bin/sh   
如果容器中安装了bash，可以把最后的 /bin/sh 换成 /bin/bash    
退出命令是exit  


