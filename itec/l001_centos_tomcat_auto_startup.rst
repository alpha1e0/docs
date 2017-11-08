.. centos配置，tomcat开机自启动


=================================
L001 - CentOS tomcat 开机自启动
=================================


:Version: v1.0
:Date: 2017-10-30
:Note: 转载请注明出处。

----


1 前言
========

CentOS 使用 **systemd** 管理，但截止 *CentOS 7* 仍然兼容 **init.d** （ *CentOS 8* 没有测试过）

因此，有两种方式设置 **tomcat** 自启动


2 systemd 方式自启动
======================

假设 **tomcat** 安装（解压）在目录 **/opt/apache-tomcat-8.5.23** 中

**step 1**

创建 PID 文件

>>> cd /opt/apache-tomcat-8.5.23
>>> touch tomcat.pid

**step 2**

创建 **setenv.sh** 文件

>>> vi /opt/apache-tomcat-8.5.23/bin/setenv.sh

添加如下内容 ::

    CATALINA_PID="/opt/apache-tomcat-8.5.23/tomcat.pid"
    JAVA_OPTS="-server -XX:PermSize=256M -XX:MaxPermSize=1024m -Xms512M -Xmx1024M -XX:MaxNewSize=256m"

其中 **JAVA_OPTS** 中按需要更改参数

**step 3**

添加 **tomcat.service** 服务描述文件

>>> vi /usr/lib/systemd/system/tomcat.service

添加如下内容 :: 

    [Unit]
    Description=Tomcat
    After=syslog.target network.target remote-fs.target nss-lookup.target   

    [Service]
    Type=forking
    Environment=JAVA_HOME=/opt/jdk1.8.0_144/jre
    PIDFile=/opt/apache-tomcat-8.5.23/tomcat.pid
    ExecStart=/opt/apache-tomcat-8.5.23/bin/startup.sh
    ExecReload=/bin/kill -s HUP $MAINPID
    ExecStop=/bin/kill -s QUIT $MAINPID
    PrivateTmp=true 

    [Install]
    WantedBy=multi-user.target


**step 4**

使用如下命令管理tomcat ::

    systemctl daemon-reload   # 初次创建tomcat.service后必须执行该命令一次
    systemctl enable tomcat   # 设置开机启动

在一切配置好之后就可以使用如下命令管理 **tomcat** 了 ::

    systemctl start|stop|restart tomcat
    systemctl status tomcat 



3 init.d 方式自启动
======================

**init.d** 方式比较简单，添加开机启动脚本即可

**step 1**

增加服务启动脚本

>>> vi /etc/rc.d/init.d/tomcat

添加如下内容 ::

    #!/bin/bash
    # chkconfig: 2345 10 90 
    # description: myservice ....
    # filename: /etc/rc.d/init.d/tomcat
    # description: Start up the Tomcat servlet engine.
    # chkconfig --add /etc/rc.d/init.d/tomcat
    # chkconfig tomcat on   

    if [ -f /etc/init.d/functions ]; then
        . /etc/init.d/functions
    elif [ -f /etc/rc.d/init.d/functions ]; then
        . /etc/rc.d/init.d/functions
    else
        echo -e "\atomcat: unable to locate functions lib. Cannot continue."
    exit -1
    fi  

    RETVAL=$?   

    CATALINA_HOME="/opt/apache-tomcat-8.5.23"     # 此处根据实际情况设置tomcat目录

    export JAVA_HOME="/opt/jdk1.8.0_144"          # 此处根据实际情况设置java路径
    export JRE_HOME="/opt/jdk1.8.0_144/jre"       # 此处根据实际情况设置jre路径

    case "$1" in
        start)
            if [ -f $CATALINA_HOME/bin/startup.sh ]; then
                echo $"Starting Tomcat"
                $CATALINA_HOME/bin/startup.sh
            fi
        ;;
        stop)
            if [ -f $CATALINA_HOME/bin/shutdown.sh ]; then
                echo $"Stopping Tomcat"
                $CATALINA_HOME/bin/shutdown.sh
            fi
        ;;
        *)
            echo $"Usage: $0 {start|stop}"
            exit 1
        ;;
    esac    

    exit $RETVAL

**step 2**

使用如下命令设置开机自启动

>>> chkconfig --add /etc/rc.d/init.d/tomcat

在一切配置好之后就可以使用如下命令管理 **tomcat** 了 ::

    service tomcat start|stop|restart

