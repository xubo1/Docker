+ 准备好docker运行环境
+ 上传data-sharing-project-1.0-SNAPSHOT.jar包
+ 创建Dockerfile文件
```
FROM java:8

ADD ./data-sharing-project-1.0-SNAPSHOT.jar project/data-sharing-project-1.0-SNAPSHOT.jar

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN echo "Asia/shanghai" >> /etc/timezone

EXPOSE 9001
ENTRYPOINT ["java","-jar","project/data-sharing-project-1.0-SNAPSHOT.jar"]
```
+ 在Dockerfile的当前目录执行
```
docker build -t data-share:1.0.0-SNAPSHOT .
```
+ 执行docker images看是否创建成功
![微信截图_20200508155612.png](http://ww1.sinaimg.cn/large/005QyRUkgy1gel3ju1pn5j30vn012a9w.jpg)

+ 启动镜像
```
docker run -it 镜像id/bin/bash
```
+ 启动成功
![微信截图_20200508160259.png](http://ww1.sinaimg.cn/large/005QyRUkgy1gel3q5wemuj31gq0k7diq.jpg)

+ 将镜像打包成压缩包
```
docker save -o data-share.tar.gz data-share:1.0.0-SNAPSHOT
```
+ 将镜像压缩包传到新环境时，导入镜像需要以下命令
```
docker load -i data-share.tar.gz
```