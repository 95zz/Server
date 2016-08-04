# Mac Apache服务器搭建、Tomcat（http）服务器搭建、Tomcat（https）服务器搭建
## Apache服务器搭建

搭建步骤：

```
1: 输入sudo apachectl -k start，（输入电脑密码）这样Apache服务器就打开了
2: 浏览器在地址栏输入localhost或者127.0.0.1，界面出现 It Works！
3: 接下来需要将本地服务器的路径指向你的目录
在终端输入：cd /etc/apache2/进入Apache内部，
以系统级服务的身份输入sudo vim httpd.conf，（输入电脑密码）打开httpd.conf 配置文件，然后输入enter再次输入E对配置文件尽心编辑
4: 查找 DocumentRoot字符串,进行路径修改，将路径改为你存放文件的服务器目录（注意第五点）有三个地方需要修改，我已经改过了，同时注意在终端搜索DocumentRoot字符串不一定可以搜到，所以需要自己找，
三个地方分别如下：DocumentRoot "Users/jincieryi/LocalServer"
<Directory "/Users/jincieryi/LocalServerr">
<Directory "/Users/jincieryi/LocalServer">
    AllowOverride None
    Options None
    Require all granted
</Directory>
5: 存放文件的服务器目录一定在根目录下，与桌面、文稿同级，比如我存放文件的服务器目录为 LocalServer，那我就将它放在根目录，路径为：/Users/jincieryi/LocalServer，否则访问不成功

```

## Tomcat（http）服务器搭建

搭建步骤：

```
1: 下载Tomcat（地址:tomcat.apache.org），在左侧列表中选择适合的版本（这里选择 7.0.70），
随后在右侧Quick Navigation下点击7.0.70，之后在新页面点击“Core下的“zip“或者“tar.gz”都可以，完成下载
2: 解压Tomcat到目录：/Library 中，并把文件夹名由“apache-tomcat-7.0.70”改为“Tomcat” 
3: 打开终端，输入如下三条命令： 
第一步:sudo chmod 755 /Library/Tomcat/bin/*.sh 
按回车键之后会提示输入密码，请输入管理员密码。之后输入并回车
第二步:cd /Library/Tomcat/bin
第三步:sudo sh startup.sh 
若出现如下提示则表示安装并运行成功： 
Using CATALINA_BASE: /Library/Tomcat 
Using CATALINA_HOME: /Library/Tomcat 
Using CATALINA_TMPDIR: /Library/Tomcat/temp 
Using JRE_HOME: /System/Library/Frameworks/JavaVM.framework/Versions/CurrentJDK/Home 
4: 打开浏览器，输入 http://localhost:8080/ 
回车之后如果看到Apache Tomcat，表示已经成功运行Tomcat 
5: 在终端中输入命令 sudo sh /Library/Tomcat/bin/shutdown.sh 回车之后可以关闭Tomcat。 

```

## Tomcat（https）服务器搭建

搭建步骤：

```
1: Tomcat（http）服务器搭建搭建完成之后，进入/Library/Tomcat/conf
2: 打开server.xml
3: 将<Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
               替换成
               <Connector port="8443" protocol="org.apache.coyote.http11.Http11Protocol" SSLEnabled="true"
           enableLookups="false"
           acceptCount="100" disableUploadTimeout="true"
           maxThreads="150" scheme="https" secure="true"
           clientAuth="false" sslProtocol="TLS"
           keystoreFile="bin/.keystore"
           keystorePass="Pingan968" />
4: 将.keystore文件拷入到/Library/Tomcat/bin 文件夹下面
.keystore文件下载地址："https://github.com/indexjincieryi/Server/"
回车之后如果看到Apache Tomcat，表示已经成功运行Tomcat 
5: 配置完成后，需要重启重Tomcat服务器
6: 浏览器输入"https://localhost:8443"即可访问 https的服务器了

```


