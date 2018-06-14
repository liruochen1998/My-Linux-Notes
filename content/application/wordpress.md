# WordPress

![wordpress icon](https://github.com/liruochen1998/My-Linux-Notes/blob/master/content/application/pics/wordpress_logo.png)  
**WordPress** is a free and open-source content management system based on PHP and MySQL. To function, **WordPress** has to be installed on a web server, which would either be part of an Internet hosting service or a network host in its own right.

## Setup

### LAMP part

This is the preparation before setting up **WordPress**, you will need `LAMP` environment in your VPS.

#### Install the reliance environments and applications

	$ yum install -y httpd php php-fpm mysql mysql-server php-mysql

#### Start these applications

```
$ service httpd start
$ service mysqld start  
$ service php-fpm start 
```
#### Check point
visit your ip in the browser, you may see something like your `php` info.

#### MySQL setup
you will need a database to store all the data of your wordpress.

**Note:** Check my other documents, especially `LAMP` setup for further information. It is better if you set up `LAMP` before moving on.

### WordPress part
#### Download WordPress
	$wget http://wordpress.org/latest.tar.gz
#### Make a directory for your WordPress
	$ mkdir /var/blog
You also need to add permission to this directory:  
	
	$ chown –R apache:apache /var/blog
#### Configuration
You will need to configure in the `httpd.conf` file.
	
	$ vi /etc/httpd/conf/httpd.conf
or
	
	$ vi /etc/httpd/httpd.conf
depends on your situation.

add:

```
<VirtualHost *:80>  
    ServerName 域名  
    DocumentRoot "/var/blog/wordpress"  
    <Directory "/var/blog/wordpress">  
        Options Indexes FollowSymLinks  
        AllowOverride None        
        Order deny,allow  
        Allow from all  
    </Directory>  
    ErrorLog logs/blog-error.log  
    CustomLog logs/blog-access.log common  
  
</VirtualHost>  
```
#### Restart Apache and visit your ip-address
Restart Apache and visit your ip-address, you will see **WordPress** UI. Now, start the further setup there.
A very important file is `wp-config.php`.
Directory:

	/var/blog/wordpress/wp-config.php


## References
very useful:
[https://blog.csdn.net/webyzx/article/details/78666344](https://blog.csdn.net/webyzx/article/details/78666344)    
aliyun about MySQL:
[https://help.aliyun.com/document_detail/50774.html?spm=a2c4g.11186623.6.766.LgY4mw](https://help.aliyun.com/document_detail/50774.html?spm=a2c4g.11186623.6.766.LgY4mw)


	

