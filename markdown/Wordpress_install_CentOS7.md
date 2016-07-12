#How To Install Wordpress On CentOS 7
##Attention
首先我默认你已经安装了LAMP架构了，如果没有安装请先安装LAMP

##第一步，为Wordpress新建一个数据库和用户

我们进入`MySQL`的管理界面
<pre><code>mysql -u root -p</code></pre>
当然你需要输入密码才能进入，当你输入密码之后
<pre><code>CREATE DATABASE wordpress;

CREATE USER wordpressuser@localhost IDENTIFIED BY 'password';

GRANT ALL PRIVILEGES ON wordpress.* TO wordpressuser@localhost IDENTIFIED BY 'password';

FLUSH PRIVILEGES;

exit</code></pre>
这里我们的`wordpressuser`和`password`是用户名和密码，根据你的喜好请自行设置
##第二步，安装Wordpress
输入以下代码，我们在根目录下载了Wordpress安装包解压，然后复制到相关目录
<pre><code>sudo yum install php-gd

sudo service httpd restart

cd ~

wget http://wordpress.org/latest.tar.gz

tar xzvf latest.tar.gz

sudo rsync -avP ~/wordpress/ /var/www/html/

mkdir /var/www/html/wp-content/uploads

sudo chown -R apache:apache /var/www/html/*</code></pre>
##第三步，配置Wordpress
我们进入Wordpress安装目录
<pre><code>cd /var/www/html</code></pre>
然后拷贝配置文件
<pre><code>cp wp-config-sample.php wp-config.php</code></pre>
然后编辑配置文件
<pre><code>vi wp-config.php</code></pre>
将配置文件部分内容更改为如下形式，然后保存退出
<pre><code>// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'wordpress');

/** MySQL database username */
define('DB_USER', 'wordpressuser');

/** MySQL database password */
define('DB_PASSWORD', 'password');</code></pre>
##第四步，完成安装Wordpress
我们又要访问服务器IP端口了
<pre><code>	http://server_domain_name_or_IP</code></pre>
然后你会看到如下图片
![wordpress_web_install](https://raw.githubusercontent.com/lvchengli/lvchengli.github.io/master/markdown/img/wordpress_web_install.png)

然后你填入信息然后`Continue`,然后跟住图形界面进行各项设置，完成安装之后就可以愉快地使用了





