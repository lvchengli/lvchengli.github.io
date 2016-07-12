#How To Install Linux, Apache, MySQL, PHP (LAMP) stack On CentOS 7
##LAMP ---> Linux + Apache + MySQL + PHP
###安装apache
我们在CentOS上面安装程序需要用到 `yum install xxx` 进行安装，首先我们输入以下代码
<pre><code>sudo yum install httpd</code></pre>
使用sudo可能要输入root密码，然后
<pre><code>sudo systemctl start httpd.service</code></pre>
然后可以在浏览器输入服务器的IP访问
<pre><code>http://your_server_IP_address/</code></pre>
在服务器上可以看到如下图
![default_apache](https://raw.githubusercontent.com/lvchengli/lvchengli.github.io/master/markdown/img/default_apache.png)
之后，你需要让apache随服务器开机启动，然后输入
<pre><code>sudo systemctl enable httpd.service</code></pre>
###安装MySQL (MariaDB)
下面第一行下载MariaDB，第二行打开MariaDB数据库，第三行设置密码
<pre><code>sudo yum install mariadb-server mariadb
sudo systemctl start mariadb
sudo mysql_secure_installation
</code></pre>
输入第三行代码然后`enter`之后，会提示输入当前的密码，但是我们刚安装了MariaDB，所以初始密码为空，所以直接`enter`，然后提示是否设置一个root密码，然后输入Y，然后跟着指令设置密码
<pre><code>Enter current password for root (enter for none):
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MariaDB
root user without the proper authorization.

New password: password
Re-enter new password: password
Password updated successfully!
Reloading privilege tables..
 ... Success!</code></pre>
设置完密码之后，我们连续按enter键进行默认设置，这里的细节我们不用管，最后一件事情就是让数据库随服务器启动
<pre><code>sudo systemctl enable mariadb.service</code></pre>
###安装PHP
首先我们安装一些相关程序
<pre><code>sudo yum install php php-mysql php-fpm php-cli</code></pre>
###测试PHP环境
在CentOS中，我们的目录是在 `/var/www/html/` ，我们在目录下新建一个文件
<pre><code>sudo vi /var/www/html/info.php</code></pre>
然后在`vim`界面内输入以下内容然后保存退出
<pre><code>&lt;?php phpinfo(); ?&gt;</code></pre>
在vim界面内按`i`可以进行编辑操作，然后按`Esc`之后，再输入`:wq`可以保存退出
如果服务器开启了防火墙我们需要关闭以下，不过默认是没有防火墙的
<pre><code>sudo firewall-cmd --permanent --zone=public --add-service=http 
sudo firewall-cmd --permanent --zone=public --add-service=https
sudo firewall-cmd --reload</code></pre>
然后我们现在访问这个`info.php`文件
<pre><code>http://your_server_IP_address/info.php</code></pre>
然后我们可以看到如下图，证明环境搭建成功
![default_php](https://raw.githubusercontent.com/lvchengli/lvchengli.github.io/master/markdown/img/default_php.png)
如果这里没有出现这个图，证明出现了问题，建议你`Google一下`