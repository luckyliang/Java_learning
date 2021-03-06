# Maven

## Maven配置

### Maven环境变量配置

[Apache Maven](https://maven.apache.org/) 主要用于自动化构建和管理Java项目，基于项目对象模型（POM, Project Object Model）的概念

**下载地址：**https://maven.apache.org/download.cgi

![image-20210306130500017](.\src\image-20210306130500017.png)

**必须配置好`JAVA_HOME`**，`Maven`对JDK版本要求：http://maven.apache.org/docs/history.html

**添加`MAVEN_HOME\bin` 到 `PATH`中**

![image-20210306131238430](.\src\image-20210306131238430.png)

### 初始化配置

#### 修改仓库位置

在`%MAVEN_HOME%/conf/settings.xml`的<settings>标签中添加1个<localRepository>标签

```xml
  <!-- 修改本地仓库位置 -->
  <localRepository>
  	E:\Program Files\apache-maven-localRepository\.m2\repository
  </localRepository>
```



#### 提高仓库下载速度

在`%MAVEN_HOME%/conf/settings.xml`的<mirrors>标签中添加1个<mirror>标签

```xml
     <mirror>
      <id>aliyun</id>
      <mirrorOf>central</mirrorOf>
      <name>aliyun</name>
      <url>https://maven.aliyun.com/repository/public</url>
    </mirror>
```

#### 修改Maven项目的JDK版本

推荐使用第三种方法一劳永逸

1. ##### 方法一

   在pom.xml中添加属性（每个Maven项目都要添加）

   ```xml
       <properties>
           <maven.compiler.source>14</maven.compiler.source>
           <maven.compiler.target>14</maven.compiler.target>
           <maven.compiler.compilerVersion>14</maven.compiler.compilerVersion>
       </properties>
   ```

2. 方法二

   在pom.xml中添加插件（每个Maven项目都要添加）

   ```xml
   <build>
       <plugins>
       	<!-- 修改Maven项目对应Java的JDK版本 -->
           <plugin>
               <groupId>org.apache.maven.plugins</groupId>
               <artifactId>maven-compiler-plugin</artifactId>
               <configuration>
                       <source>1.8</source>
                       <target>1.8</target>
               </configuration>
           </plugin>
       </plugins>
   </build>
   ```

3. 在`%MAVEN_HOME%/conf/settings.xml`的<profiles>标签添加<profile>

   这是一种一劳永逸的办法，不需要去修改每一个Maven项目的`pom.xml`

   ```xml
   <profile>
     <id>jdk-1.8</id>
     <activation>
       <jdk>1.8</jdk>
       <activeByDefaul>true</activeByDefaul>
     </activation>
     <properties>
     	<maven.complier.source>1.8</maven.complier.source>
     	<maven.complier.target>1.8</maven.complier.target>
     	<maven.complier.complierVersion>1.8</maven.complier.complierVersion>
     </properties>
   
   </profile>
   ```

## 新建Maven项目

### 命令行新建Maven项目

一般使用Idea直接创建Maven项目吧

- 方法一

  在命令行输入：`mvn archetype：generate`，会让我们选择项目类型

  默认值是7，`maven-archetype-quickstart`，是一个普通`java`项目，如果希望使用默认值，直接敲回车即可

  如果希望创建一个`web`项目，应该输入10，`maven-archetype-webapp`

  ![image-20210306160318311](.\src\image-20210306160318311.png)

  输入`groupId、artifactId、version、package`

  如果希望`version、package`使用默认值，直接敲回车即可

  ![image-20210306160421432](.\src\image-20210306160421432.png)

  最后输入y表示确认，项目就创建完毕了

  ![image-20210306160522549](.\src\image-20210306160522549.png)

  

- 在命令行输入

  ```java
  mvn archetype:generate -DgroupId=com.lc.maven -DartifactId=helloworld -Dversion=1.0-RELEASE -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-quickstart
  ```

- IDEA导入`maven`项目

  选择`pom.xml`进行导入

IDEA新建Maven项目（Web项目）t

推荐使用第二种方式

- 方法一

  使用`archetype`

  ![image-20210306161151684](.\src\image-20210306161151684.png)

  设置项目信息

  ![image-20210306161229755](.\src\image-20210306161229755.png)

  ![image-20210306161258733](.\src\image-20210306161258733.png)

​		

- 方法二（推荐）

  不勾选`Create from archetype`

  ![image-20210306161529179](.\src\image-20210306161529179.png)

  ![image-20210306161551145](.\src\image-20210306161551145.png)

  

  `pom.xml`配置

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <project xmlns="http://maven.apache.org/POM/4.0.0"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
      <!-- 模型版本 -->
      <modelVersion>4.0.0</modelVersion>
  
      <!-- 项目信息 -->
      <groupId>com.lc</groupId>
      <artifactId>crm</artifactId>
      <version>1.0.0</version>
      <!--打包方式 -->
      <packaging>war</packaging>
      <!-- 文件编码 -->
      <properties>
          <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
      </properties>
      <!-- 依赖 -->
      <dependencies>
          <dependency>
              <groupId>javax.servlet</groupId>
              <artifactId>javax.servlet-api</artifactId>
              <version>4.0.1</version>
          </dependency>
          <dependency>
              <groupId>javax.servlet</groupId>
              <artifactId>jstl</artifactId>
              <version>1.2</version>
          </dependency>
      </dependencies>
      <!-- 构建信息 -->
      <build>
          <!-- 打包后的文件名 -->
          <plugins>
              <!-- 修改Maven项目的JDK版本 -->
              <plugin>
                  <groupId>org.apache.maven.plugins</groupId>
                  <artifactId>maven-compiler-plugin</artifactId>
                  <configuration>
                      <source>1.8</source>
                      <target>1.8</target>
                  </configuration>
              </plugin>
          </plugins>
      </build>
  </project>
  ```

  对项目进行`Reimport`

  ![image-20210306162319725](.\src\image-20210306162319725.png)

  打开`Project structure，添加web.xml`

  ![image-20210306162418148](.\src\image-20210306162418148.png)

  将web.xml放到src/main/webapp/WEB-INF目录

  ![image-20210306162629274](.\src\image-20210306162629274.png)

  ![image-20210306162701587](.\src\image-20210306162701587.png)

## Maven配置Tomcat

1. 使用独立安装的`Tomcat9`

   在`%TOMCAT_HOME%/conf/tomcat-users.xml` 中添加用户

   ```xml
     <role rolename="manager-gui"/>
     <role rolename="manager-script"/>
     <user username="root" password="root" roles="manager-gui,manager-script"/>
   ```

   在`%MAVEN_HOME%/conf/settings.xml`的<servers>中添加<server>

   ```xml
    <server>
     <id>tomcat9</id>
     <username>root</username>
     <password>root</password>
   </server>
   ```

   集成`tomcat7-maven-plugin`

   ```xml
   <plugin>
       <groupId>org.apache.tomcat.maven</groupId>
       <artifactId>tomcat7-maven-plugin</artifactId>
       <version>2.2</version>
       <configuration>
           <path>/context_path</path>
           <update>true</update>
           <server>tomcat9</server>
           <port>8080</port>
           <uriEncoding>UTF-8</uriEncoding>
       </configuration>
   </plugin>
   ```

   启动本地的`tomcat9`，通过`tomcat7-maven-plugin`的命令部署项目到`tomcat9`

   ```java
   mvn tomcat7:deploy
   或者
   mvn tomcat7:redeploy
   ```

   

2. 集成`tomcat7-maven-plugin`

   使用`Maven`内置的`Tomcat`（目前`Maven`内置的`Tomcat为Tomcat7`）

   ```xml
   <!-- 集成tomcat7-maven-plugin -->
   <plugin>
       <groupId>org.apache.tomcat.maven</groupId>
       <artifactId>tomcat7-maven-plugin</artifactId>
       <version>2.2</version>
       <configuration>
           <path>/context_path</path>
           <port>8080</port>
           <uriEncoding>UTF-8</uriEncoding>
       </configuration>
   </plugin>
   <!-- 为了避免jar包冲突，修改servlet的scope为provided -->
   <dependency>
       <groupId>javax.servlet</groupId>
       <artifactId>javax.servlet-api</artifactId>
       <version>4.0.1</version>
       <scope>provided</scope>
   </dependency>
   ```

## Maven项目的常见目录

Maven使用“约定优于配置” 的思想（Convention over Configuration）

![image-20210306141133612](.\src\image-20210306141133612.png)

## pom.xml

[pom.xml](http://maven.apache.org/pom.html)是Maven项目的核心配置文件，根元素是project，project的常用子元素如下所示

|     元素     |                             描述                             |
| :----------: | :----------------------------------------------------------: |
| modelVersion |           pom的版本，目前都使用4.0.0，是必要的元素           |
|   groupId    |         组织名称，一般用域名的倒写，比如com.lc.hello         |
|  artifactId  |                           项目名称                           |
|   version    |     项目版本号，比如1.0.0、3.0、1.0-SNAPSHOT、1.0-RELESE     |
|  packaging   | 打包方式，比如pom、jar（默认值）、maven-plugin、ejb、war、ear、rar |
|  properties  |                   属性信息，比如文本编码等                   |
| dependencies |                           依赖信息                           |
|    build     |                   构建信息，比如插件配置等                   |

`groupId、artifactId、version`，组成一个Maven坐标，能够确定唯一的一个项目

## 常见问题解决

### 解决文件编码的警告

![image-20210306172800300](.\src\image-20210306172800300.png)

在pom.xml中添加

```xml
<!-- 文件编码 -->
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
```

### 解决IDEA控制台输出乱码

![image-20210306173027829](.\src\image-20210306173027829.png)

`Setting -> Build ， Execution，Deployment -> Build Tools -> Maven -> Runner`

`在VM Options中添加 -Dfile.encoding=GBK`

![image-20210306173050165](.\src\image-20210306173050165.png)

## 生成Runnable Jar



## 构建生命周期

![image-20210306144400330](.\src\image-20210306144400330.png)

- 构建生命周期，描述了构建的过程。`Maven`内置了3个构建生命周期
  - `clean`（清理）
  - `default`（默认，重点关注）
  - `site`（站点）
- 构建生命周期由`phase`（阶段）组成
  - `phase`可以跟`plugin goal`（插件目标）绑定
  - `plugin goal`代表1个特定的任务
  - 一旦某个`phase`被执行，就会执行器绑定的所有`goal`
- 通过命令mvn插件：`help`可以查看插件包含的所有`goal`
  - 比如`mvn archetype:help`

## default生命周期

`default`生命周期由下表中的phase组成

|  phase   |                             描述                             |
| :------: | :----------------------------------------------------------: |
| validate |             确认项目正确并且所有必要的信息均可用             |
| compile  |                 编译项目的源代码（src/main）                 |
|   test   |  使用合适的单元测试框架编译后的源代码（src/main、src/test）  |
| package  |     获取编译后的代码，并将其打包为可分发的格式，例如jar      |
|  verify  |       对集成测试的结果进行任何检查，以确保符合质量标准       |
| install  |   将软件包安装到本地储存库中，以作为本地其他项目中的依赖项   |
|  deploy  | 在构建环境中完成后，将最终软件包复制到远程储存库中，以便与其他开发人员和项目共享 |

使用命令`mvn package`就会按顺序执行`validate`、`compile`、`test`、`package`阶段

## 常用命令

|          命令           |            描述            |
| :---------------------: | :------------------------: |
| mvn archetype：generate |       创建Maven项目        |
|        mvn clean        |         清除target         |
|    mvn clean package    | 先执行clean，在执行package |

仓库查询

https://search.maven.org/

https://mvnrepository.com/

## dependency中scope的取值

- compile：默认。编译依赖关系在**所有类路径中均可用**，此外，这些依赖项会传递到相关项目
- provided：**仅在编译和测试类路径上可用**，并且不可传递。希望JDK或容器在运行时提供它
- runtime：依赖关系不是编译所需的，而是运行所必须的。他在运行时和测试类路径中，但不在编译类路径中
- test：依赖关系对于正常使用该应用程序不是必须的，并且在**测试编译和执行阶段可用**。他不是可传递的
- system：必须显示提供jar的位置（可以通过systemPath标签指定），不会去Maven仓库中查找













