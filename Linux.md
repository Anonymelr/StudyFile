# 	Linux

### 一、文件目录类

#### 1.1 pwd指令

- 基本语法

  pwd	（功能：显示当前工作目录的绝对路径）

  ```shell
  pwd	#打印当前工作目录的绝对路径
  ```

  

#### 1.2 ls 指令

- 基本语法

  ls  [选项]  [目录或者是文件]  （功能：查看当前目录下的所有文件）

- 常用选项

  -a  :  显示当前目录所有的文件和目录，包含**隐藏的**

  -l   :  以列表的形式显示信息

  ```shell
  ls 			#查看当前目录的所有文件
  ls -l		#以列表的形式查看当前目录的所有文件
  ls -al		#查看当前目录的所有文件，包含隐藏文件
  ```



#### 1.3 cd 指令

- 基本语法

  cd  [参数]  （功能：切换到指定目录）

- 常用参数

  **绝对路径和相对路径**

  cd  :  回到家目录

  cd ..  :  回到上一级目录

  ```shell
  cd /apps		#进入	/apps 目录下
  cd ~			#返回根目录
  cd ..			#返回上一级目录
  ```

  

#### 1.4 mkdir 指令

- 基本用法

  mkdir  [选项]  要创建的目录	（功能：创建一个目录）

- 选项

  -p  :  创建多级目录

  ```shell
  mkdir /home/dog				#在home目录下创建dog目录（文件）
  mkdir -p /home/dog/hello	#在home目录下创建dog目录（文件）及再在dog目录下创建hello目录（文件）
  ```

  

#### 1.5 rmdir 指令

- 基本用法

  rmdir [选项] 要删除的空目录  （功能：删除**空目录**）

  ```shell
  rmdir /home/dog		#删除home目录下创建dog空目录（文件）
  ```



#### 1.6 touch 指令

- 基本语法

  touch 文件名称 （功能：创建空文件夹）

  ```shell
  touch hello.txt		#创建hello.txt文件夹
  ```

  

#### 1.7 cp指令

- 基本语法

  cp [选项] 源文件 目的地址 （功能：复制文件到指定位置）

- 常用选项

  -r  :  递归复制整个文件夹

  ```shell
  cp hello.txt bbb/		#将hello.txt 复制到 bbb/目录下
  cp -r hello/ bbb/		#将hello及里面的所有文件 都复制到 bbb/目录下
  \cp -r hello/ bbb/  	#强制覆盖
  ```

  

#### 1.8 rm 指令

- 基本语法

  rm [选项] 要删除的文件或者目录 （功能：删除文件）

- 常用选项

  -r  :   递归删除整个文件

  -f  :   强制删除不提示

  ```shell
  rm -rf hello	#删除
  ```

  

#### 1.9 mv 指令

- 基本语法

  mv oldFileName newFileName	（功能：重命名）

  mv fileName /app	（功能：移动文件）

  ```shell
  mv hello hello1		#重命名
  mv hello /app		#将 hello 移动到 /app 目录下
  ```

  

#### 1.10 cat 指令

- 基本语法

  cat [选项] 要查看的文件	（功能：以只读的方式打开文件）

- 选项

  -n  :  显示行号

  ```shell
  cat hello.txt			#以只读的方式查看文件
  cat -n hello.txt		#以只读的方式查看文件，并在每一行的前面显示行数
  ```

- 常用方法

  ```shell
  cat -n hell0.txt | more	#分页查看，点击空格页到下一页
  ```

  

#### 1.11 more 指令

- 按Space键：显示文本的下一屏内容。
- 按Enter键：只显示文本的下一行内容。
- 按斜线符`|`：接着输入一个模式，可以在文本中寻找下一个相匹配的模式。
- 按H键：显示帮助屏，该屏上有相关的帮助信息。
- 按B键：显示上一屏内容。
- 按Q键：退出more命令。



#### 1.12 less 指令

- 基本语法

  less [选项] 要查看的文件 	（功能：分页查看文件，速度比more快，适合查看大型文件）

  **用PageUp键向上翻页，用PageDown键向下翻页。要退出less程序，应按Q键。**



#### 1.13 > 指令 和 >>指令

- 介绍

  ```
  > 输出重定向
  >> 追加
  ```

  ```shell
  ls -l > a.txt	#将ls显示的内容覆盖写入a.txt
  ls -l >> a.txt	#将ls显示的内容追加到a.txt的末尾
  ```

  

#### 1.14 head 指令

- 基本语法

  head [选项] 文件	（功能：查看文件的前10行）

- 常用选项

  -n  :  行数

  ```shell
  head hello.txt			#查看文件的前10行
  head -n 5 hello.txt		#查看文件的前5行
  ```

  

#### 1.15 tail指令

- 基本语法

  tail [选项] 文件	（功能：查看文件的后10行）

- 常用选项

  -n  :  行数

  -f  :  实时查看

  ```shell
  tail hello.txt			#查看文件的后10行
  tail -n 5 hello.txt		#查看文件的后5行
  tail -f hello.txt		#实时查看文件
  ```

  

#### 1.16 vim编辑器

##### 1.16.1 正常模式

- vim 打开一个文件，默认进入的就是正常模式

##### 1.16.2 编辑模式

- 在此模式，程序员可以输入内容
- 按	i	/	a	/	o	/	r	进入编辑模式
- 按   Esc    即可退出编辑模式

##### 1.16.3 命令行模式

- 在此模式，可以提供相关指令，完成读取、存盘、替换、离开vim等操作



#### 1.17 ln 指令

- 基本语法

  ln -s  [原文件或目录] [软链接名]	（功能：给原文件创建一个软链接）

  ```shell
  ln -s /root linkToRoot	#给/root目录创建一个linkToRoot软链接
  ```

  **删除软链接时，不要带“/”否则提示设备忙**



#### 1.18 history 指令

- 基本语法

  histroy	（功能：查看已经执行过的指令）

  ```shell
  history		#显示历史执行过的指令
  history 10  #显示最近执行过的指令
  ```



### 二、搜索查找类

#### 2.1 find 指令

- 基本语法

  find  [搜索范围]  [选项]  [参数]

- 常用选项

  -name	按指定文件名查询

  -user	查找所有属于指定用户名的所有文件

  -size	按指定文件大小查找文件

  ```shell
  find /home -name hello.txt 		#在home目录下查找名字为hello.txt的文件
  find /opt -user root			#在opt目录下查找所属用户是root的所有文件
  find / -size +20M(-20M)			#在/目录下查找文件大于20M的所有文件
  ```

  

#### 2.2 grep指令

- 基本语法

  grep [选项] 查找内容 源文件

- 常用选项

  -n 	显示匹配行及行号

  -i	  忽略字母大小写

  ```shell
  cat hello.txt | grep yes		#显示hello.txt文件中所有的yes
  cat hello.txt | grep -n yes		#显示hello.txt文件中所有的yes及行号
  ```

  

### 三、压缩及解压缩指令

#### 3.1 gzip/gunzip指令

- 基本语法

  gzip 文件			（功能：压缩文件）

  gunzip 文件.gz	（功能：解压文件）

  ```shell
  gzip hello.txt			#将hello.txt压缩，压缩后hello.txt不会存在
  gunzip hello.txt.gz		#解压hello.txt
  ```

  

#### 3.2 zip/unzip 指令

- 基本语法

  zip [选项]  文件.zip			（功能：压缩文件）

  unzip [选项]   文件.zip	（功能：解压文件）

- zip常用选项

  -r   递归压缩

- unzip常用选项

  -d<目录>	指定解压后文件的存放目录

  ```shell
  zip -r mypackage.zip /home		#将home 整个文件夹都压缩到 mypackage.zip
  unzip -d /opt/tmp mypackage.zip #将 mypackage.zip 解压到 /opt/tmp 目录下
  ```

  

#### 3.3 tar 指令

- 基本语法

  tar  [选项]  XXX.tar.gz 打包的内容

- 常用选项

  -c	产生.tar打包文件

  -v 	显示详细信息

  -f	指定压缩后的文件名

  -z	打包同时压缩

  -x	解包.tar文件

  ```shell
  tar -zcvf a.tar.gz a1.txt a2.txt  #将a1.txt和a2.txt一起压缩到a.tar.gz
  tar -zcvf myhome.tar.gz /home/		#将home及目录下所有文件一起压缩到myhome.tar.gz
  tar -zxvf a.tar.gz				#将a.tar.gz解压到当前目录
  tar -zxvf myhome.tar.gz /opt/	#将myhome.tar.gz解压到opt目录下（前提opt目录必须存在，否则会报错）
  ```

  

### 四、磁盘分区及挂载

#### 4.1 df 指令

- 基本语法

  df 	（功能：查看系统整体磁盘的使用情况）

  ```shell
  df -lh 	#以列表的形式（单位是G）查看系统整体磁盘的使用情况
  ```

  

#### 4.2 du 指令

- 基本语法

  du [选项] 目录	（功能：查询指定目录的磁盘占用情况）

- 常用选项

  -s   指定目录占用大小汇总

  -h  带计量单位

  -a  含文件

  --max-depth=1  子目录深度

  -c  列出明细的同时，增加汇总值

  ```shell
  du -ach --max-depth=1 /apps		#查询apps目录下的所有文件占用情况
  ```

  

#### 4.3 实用指令

```shell
ls -l /home | grep "^-" | wc -l		#统计/home文件夹下面的文件数量
ls -l /home | grep "^d" | wc -l		#统计/home文件夹下面的目录数量
ls -lR /home | grep "^-" | wc -l	#统计/home文件夹下面的文件数量包括子文件夹下的
ls -lR /home | grep "^d" | wc -l	#统计/home文件夹下面的目录数量包括子文件夹下的

lsof | grep deleted					#查找被删除但是未释放空间的文件
```



### 五、进程管理

#### 5.1 ps 指令

- 基本语法

  ps  [选项] 

- 常用选项

  -a	显示当前终端的所有进程信息

  -u	以用户的格式显示进程信息

  -x	显示后台进程运行的参数

  ```shell
  ps -aux | more 	#分页查看当前所有的进程信息
  
  ps -aux | grep XXX  #以XXX为条件查看进程信息
  ```

  -e	显示所有进程

  -f	全格式

  ```shell
  ps -ef					#以全格式查看所有的进程信息
  	
  ps -ef | grep XXX		#以XXX为条件查看进程信息
  ```

- 常用方法

  ```shell
  ps -mq 21749 -o THREAD,tid	#查看21749进程下线程的内存消耗情况
  
  jstack 3899 > /home/a.txt   #将该线程的全部堆栈信息放入临时文件a.txt里面（注意此时线程号是 十六进制）
  ```

  

#### 5.2 kill 指令

- 基本语法

  kill  [选项]  进程号	（功能：通过进程号杀死进程）

- 常用选项

  -9  表示强迫进程立即停止

  ```shell
  kill -9 4002  #终止 4002 进程
  ```

  

#### 5.3 service 指令

- 基本语法

  service 服务名  [start/stop/restart/status]	（功能：开启/关闭/重启/查看 服务）



#### 5.4 top 指令

- 基本语法

  top [选项]

- 常用选项

  -d 秒数	指定top命令每隔几秒更新一下，默认3秒

  -i			  不显示任何僵死或闲置的jinc

  -p			 通过指定监控PID仅仅监控某个进程的状态

  ```shell
  输入 top，再输入 u 回车 再输入 用户名		#监控特定用户
  输入 top，再输入 k 回车 在输入 进程号		#杀死进程
  ```

  

### 六、防火墙及端口

#### 6.1 查看已开放的端口

- 基础命令

  ```shell
  #第一种方法
  firewall-cmd --list-all
  #第二种方法
  firewall-cmd --zone=public --list-ports
  ```

  ```shell
  #第一种结果：
  public
    target: default
    icmp-block-inversion: no
    interfaces:
    sources:
    services: ssh dhcpv6-client http
    ports: 7410/tcp 7750/tcp 7620/tcp 7630/tcp 7640/tcp 7610/tcp 7660/tcp 9240/tcp 9290/tcp 9410/tcp 9510/tcp 8000/tcp 10050/tcp 8848/tcp 3306/tcp 9710/tcp 8081/tcp 9620/tcp
    protocols:
    masquerade: no
    forward-ports:
    source-ports:
    icmp-blocks:
    rich rules:
  #第二种结果：
  7410/tcp 7750/tcp 7620/tcp 7630/tcp 7640/tcp 7610/tcp 7660/tcp 9240/tcp 9290/tcp 9410/tcp 9510/tcp 8000/tcp 10050/tcp 8848/tcp 3306/tcp 9710/tcp 8081/tcp 9620/tcp
  ```

​			

#### 6.2 防火墙开放端口：（开放端口后需重载防火墙）

- 基础命令

  ```shell
  #开放 3306 端口
  firewall-cmd --zone=public --add-port=3306/tcp --permanent
  #防火墙重载
  firewall-cmd --reload
  ```

- 命令含义：

  –zone #作用域

  –add-port=80/tcp #添加端口，格式为：端口/通讯协议

  –permanent #永久生效，没有此参数重启后失效



#### 6.3 firewalld的基本使用

- 基本命令

  ```shell
  #启动
  systemctl start firewalld
  #关闭
  systemctl stop firewalld
  #查看状态
  systemctl status firewalld
  #开机禁用
  systemctl disable firewalld
  #开机启用
  systemctl enable firewalld
  #查看版本： 
  firewall-cmd --version
  #查看帮助： 
  firewall-cmd --help
  #显示状态： 
  firewall-cmd --state
  ```



### 七、常用脚本

#### 7.1 启动 jar 的sh脚本

- **模板：**

```shell
#!/bin/sh
## java env
export JAVA_HOME=/data/washserver/jdk1.8.0_121
export JRE_HOME=$JAVA_HOME/jre

#临时目录配置
TMP_HOME=/data/washserver/advertiuses/tmp
API_NAME=advertiuses
JAR_NAME=$API_NAME\.jar
#PID  代表是PID文件
PID=$API_NAME\.pid

#使用说明，用来提示输入参数
usage() {
    echo "Usage: sh 执行脚本.sh [start|stop|restart|status|deploy]"
    exit 1
}

#检查程序是否在运行
is_exist(){
  pid=`ps -ef|grep $JAR_NAME|grep -v grep|awk '{print $2}' `
  #如果不存在返回1，存在返回0
  if [ -z "${pid}" ]; then
   return 1
  else
    return 0
  fi
}

#启动方法
start(){
  is_exist
  if [ $? -eq "0" ]; then
    echo ">>> ${JAR_NAME} is already running PID=${pid} <<<"
  else
    nohup $JRE_HOME/bin/java -Xms256m -Xmx512m -Djava.io.tmpdir=$TMP_HOME  -jar $JAR_NAME >/dev/null 2>&1 &
    echo $! > $PID
    echo ">>> start $JAR_NAME successed PID=$! <<<"
   fi
  }

#停止方法
stop(){
  #is_exist
  pidf=$(cat $PID)
  #echo "$pidf"
  echo ">>> api PID = $pidf begin kill $pidf <<<"
  kill $pidf
  rm -rf $PID
  rm -rf $TMP_HOME/*
  sleep 2
  is_exist
  if [ $? -eq "0" ]; then
    echo ">>> api 2 PID = $pid begin kill -9 $pid  <<<"
    kill -9  $pid
    sleep 2
    echo ">>> $JAR_NAME process stopped <<<"
  else
    echo ">>> ${JAR_NAME} is not running <<<"
  fi
}

#输出运行状态
status(){
  is_exist
  if [ $? -eq "0" ]; then
    echo ">>> ${JAR_NAME} is running PID is ${pid} <<<"
  else
    echo ">>> ${JAR_NAME} is not running <<<"
  fi
}

#重启
restart(){
  stop
  start
}

# 部署服务
deploy(){
        # backup
        mv /apps/advertiuses/advertiuses.jar \
        /apps/advertiuses/backup/advertiuses-$(date +%Y%m%d).jar

        # install
        mv /apps/advertiuses/install/advertiuses.jar \
        /apps/advertiuses

        # start
        restart
}

#根据输入参数，选择执行对应方法，不输入则执行使用说明
case "$1" in
  "start")
    start
    ;;
  "stop")
    stop
    ;;
  "status")
    status
    ;;
  "restart")
    restart
    ;;
   "deploy")
    deploy
    ;;
  *)
    usage
    ;;
esac
exit 0
```



### 八、Linux服务器环境配置

#### 8.1 安装指令包

- 安装 vim

  ```shell
  yum install -y vim*
  ```

- 安装上传下载工具包rz及sz

  ```shell
  yum install -y lrzsz
  ```

  

#### 8.2  安装JDK

- tar.gz 包安装方式

  - 上传 tar 包：使用 rz 命令，最好放在/usr/java包中

    ```shell
    mkdir /usr/local/java 	#在usr文件下创建java文件夹
    cd /usr/local/java		#进入/usr/java目录下
    rz						#上传tar包
    ```

  - 解压 tar 包

    ```shell
    tar -zxvf  jdk包			#解压jdk包
    ```

  - 配置环境变量

    ```shell
    vi /etc/profile			#打开系统配置文件
    #在文件末尾添加如下配置
    export JAVA_HOME=/usr/local/java/解压后的jdk包名
    export PATH=$PATH:$JAVA_HOME/bin
    ```

  - 重新加载配置文件

    ```shell
    source /etc/profile
    ```

  - 测试

    ```shell
    java -version 		#在任何一个地方即可使用java命令	
    ```

  

#### 8.3  安装Tomcat 

- 上传 tar 包

  ```shell
  mkdir /usr/local/tomcat 	#在usr文件下创建tomcat文件夹
  cd /usr/local/tomcat		#进入/usr/tomcat目录下
  rz							#上传tar包
  ```

- 解压 tar 包

  ```shell
  tar -zxvf  tomcat包		#解压tomcat包
  ```

- 启动 tomcat 服务

  ```shell
  ./startup.sh		#启动服务
  ```

- 在windows访问tomcat

  ```shell
  #访问前要关闭防火墙或者开放对应的端口号
  http://192.168.1.1:8080/
  ```

- 关闭 tomcat 服务

  ```shell
  ./shutdown.sh		#关闭服务
  ```

- 修改 tomcat 的端口号

  ```shell
  vim server.xml  	#修改里面的端口号即可
  ```

  

#### 8.4 安装MySQL

- centos7下进行环境准备

  ```shell
  #卸载默认安装的mariadb
  rpm -qa | grep mariadb 	#查看是否安装了mariadb
  rpm -e --nodeps mariadb.x86_64  #卸载mariadb
  ```

- 在线安装

  ```shell
  #添加官方的yum源创建并编辑mysql-community.repo文件
  vi /etc/yum.repos.d/mysql-community.repo
  
  #粘贴以下内容到源文件
  # Enable to use MySQL 5.7
  [mysql57-community]
  name=MySQL 5.7 Community Server
  baseurl=http://repo.mysql.com/yum/mysql-5.7-community/el/6/$basearch/
  enabled=1
  gpgcheck=1
  gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
  
  #安装mysql
  sudo yum install mysql-community-server
  ```

- 启动 mysql

  ```shell
  #启动mysql命令
  sudo systemctl start mysqld.service
  #查看mysql服务
  sudo systemctl status mysqld.service
  #查看版本信息
  mysql -version
  ```

- 设置用户密码

  ```shell
  #查看服务启动随机生成的密码（5.7版本以后）
  sudo grep 'temporary password' /var/log/mysqld.log
  #使用生成的临时密码登录
  mysql -uroot -p		#然后输入临时密码
  #修改密码（MyNewPass4!改为自己密码）
  ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass4!';
  ```

- 开启远程连接

  ```shell
  #先登录mysql，使用mysql库
  use mysql
  #添加远程登录用户
  GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '密码' WITH GRANT OPTION;
  #刷新权限
  flush privileges;
  
  #远程连接前，关闭防火墙或者开放端口号3306
  #开放 3306 端口
  firewall-cmd --zone=public --add-port=3306/tcp --permanent
  #防火墙重载
  firewall-cmd --reload
  ```

  

