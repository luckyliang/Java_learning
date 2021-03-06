# Tomcat环境配置

`Tomcat`下载

`Apacha Tomcat`[官网](https://tomcat.apache.org/)

Tomcat [9.0.34版本](https://tomcat.apache.org/download-90.cgi)

![image-20210306113415504](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306113415504.png)

## `Tomcat`环境变量配置

下载Tomcat软件包解压，然后配置tomcate环境变量

![image-20210306114428803](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306114428803.png)

配置path

![image-20210306114655231](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306114655231.png)

### 

## 启动和关闭Tomcat

- 方法一
  - 启动：`TOMCAT_HOME\bin\startup.bat`
  - 关闭：`TOMCAT_HOME\bin\stop.bat`
- 方法二：
  - 启动：`TOMCAT_HOME\bin\catalina.bat run`
  - 关闭：`TOMCAT_HOME\bin\catlina.bat stop`

**注意：Tomcat启动成功前提条件：配置好JAVA_HOME**

## `Tomcat`启动测试

用上面方式启动Tomcat，然后浏览器输入 http://localhost:8080

如果出现下图证明Tomcat配置成功

![image-20210306115838520](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306115838520.png)



## `IDEA`中集成`Tomcat`

1. 打开Settings，新建1个Tomcat Server

   ![image-20210306121451266](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306121451266.png)

   ![image-20210306121608990](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306121608990.png)

   ![image-20210306121629930](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306121629930.png)



## 关联Tomcat源码包（可选）

#### 方法一

1. `Ctrl+鼠标单击Tomcat`内置的类型或方法，比如HttpServlet

   ![image-20210306122158634](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306122158634.png)

2. 点击`Choose Sources`

   ![image-20210306122235130](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306122235130.png)

3. 选择Tomcat的源码包

   ![image-20210306122344159](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306122320934.png)

   ![image-20210306122419039](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306122419039.png)

#### 方法二

1. 打开`Project Structure`

   ![image-20210306122525297](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306122525297.png)

2. 右击`Tomcat`，选择`Edit`

   ![image-20210306122603313](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306122603313.png)

3. 点击第一个+号

   ![image-20210306122631635](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306122631635.png)

4. 选择Tomcat的源码包

   ![image-20210306122710874](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306122710874.png)

   ![image-20210306122725731](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306122725731.png)

   ![image-20210306122740533](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306122740533.png)

   ![image-20210306122752041](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306122752041.png)

   

## Tomcat控制台输出乱码问题

1. 打开`TOMCAT_HOME/conf/logging.properties`文件

   ![image-20210306123308182](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306123308182.png)

2. 将所有的UTF-8编码改为GBK编码

   ![image-20210306123421156](L:\devlop\java\上课笔记\项目环境搭建\src\image-20210306123421156.png)

## Tomcat部署项目的方式

1. 将web项目整个文件夹，放在`%TOMCAT_HOME%/webapps`目录中文件夹名作为`ContextPath`

2. 将web项目打包成war，放在`%TOMCAT_HOME/webapps`目录中，war文件名作为ContextPath

3. 在`%TOMCAT_HOME%/conf/server.xml`的Host标签中添加以下内容（ContextPath是path属性值）

   `<Context docBase="项目路径" path = "/xxx" />`

4. 在`%TOMCAT_HOME%/conf/Catalina/localhost`中新建一个xml文件，xml文件名作为ContextPath

   `<Context docBase = "项目路径" />`































