# docker
Spring Boot + Docker   

# Windows安装
https://www.docker.com/  
https://docs.docker.com/desktop/setup/install/windows-install/   

# CentOS安装
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
把下载的image打包成jar文件，然后传输到本地，在本地执行下面的命令导入镜像image   
docker load -i openjdk-17-jdk-alpine.tar   
然后，就可以使用docker build命令构建镜像image，比如    
docker build -t spring-boot-demo .    
构建成功后就可以运行Docker容器：   
docker run -p 8080:8080 spring-boot-demo   
后面一个8080是容器的端口，前面一个8080是宿主机的端口，也就是浏览器访问的端口。    

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

