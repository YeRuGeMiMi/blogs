# Ubuntu Server搭建java web环境

## 搭建环境

### jdk

#### 下载

+ http://download.oracle.com/otn-pub/java/jdk/7u79-b15/jdk-7u79-linux-x64.tar.gz

#### 安装
1. 解压下载包

  `tar -zvxf jdk-7u79-linux-i586.tar.gz`

2. 移动jdk到/usr/local/

  `sudo mv jdk-7u79-linux-i586/ /usr/local/java`

3. 用vi打开profile文件

  `sudo vi /etc/profile`

4. 在profile末尾加上环境变量配置
  ```
  export JAVA_HOME=/usr/local/java
  export JRE_HOME=$JAVA_HOME/jre
  export CLASSPATH=.:$CLASSPATH:$JAVA_HOME/lib:$JRE_HOME/lib
  export PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
  ```
5. 使配置生效

  `source /etc/profile`

6. 使用`java -version`查看环境变量jdk是否配置成功

  ```
  java version "1.7.0_79"
  Java(TM) SE Runtime Environment (build 1.7.0_79-b15)
  Java HotSpot(TM) Client VM (build 24.79-b02, mixed mode)
  ```

### mysql

#### 安装
`sudo apt-get install mysql-server`

安装过程中，需要输入两次root用户密码。

#### 创建数据库
1. 用root用户登录数据库

  `mysql -u root -p`

  输入密码后即可登录数据库。

2. 创建**u_test**数据库

  `CREATE DTABASE u_test DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;`

3. 导入数据库备份

  `use u_test;`

  `source 数据库备份文件`

### Tomcat

#### 下载
http://mirrors.hust.edu.cn/apache/tomcat/tomcat-7/v7.0.62/bin/apache-tomcat-7.0.62.tar.gz

#### 安装
1. 解压下载包

  `tar -zvxf apache-tomcat-7.0.62.tar.gz`

2. 移动tomcat文件夹到/usr/local

  `sudo mv apache-tomcat-7.0.62 /usr/local/tomcat7`

3. profile增加配置

  `sudo vi /etc/profile`

  文件末尾加上

  `export CATALINA_HOME=/usr/local/tomcat7`

4. 使配置生效

  `source /etc/profile`

5. 修改catalina.sh

  在`# OS specific support. $var _must_ be set to either true or false.`之前加上**CATALINA_HOME**以及**JAVA_HOME**:
  ```
  CATALINA_HOME=/usr/local/tomcat7
  JAVA_HOME=/usr/local/java
  ```
6. 将catalina.sh设置为服务

  `sudo cp bin/catalina.sh /etc/init.d/tomcat7`

7. 让tomcat开机启动

  `sudo update-rc.d -f tomcat defaults`

## 部署
将打包好的war包文件，拷贝到**tomcat**的**webapps**目录下，重启**tomcat**即可。
