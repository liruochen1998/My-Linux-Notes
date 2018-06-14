# OwnCloud

![ENV](https://img.shields.io/badge/ENV-LAMP-blue.svg) ![php5](https://img.shields.io/badge/PHP-5-brightgreen.svg) ![MySQL](https://img.shields.io/badge/MySQL-5.7-green.svg) 


![owncloud_logo](https://github.com/liruochen1998/My-Linux-Notes/blob/master/content/application/pics/owncloud_logo.png)

**OwnCloud** is a suite of client–server software for creating file hosting services and using them. **ownCloud** is functionally very similar to the widely used **Dropbox**, with the primary functional difference being that the Server Edition of **ownCloud** is free and open-source, and thereby allowing anyone to install and operate it without charge on a private server. It also supports extensions that allow it to work like **Google Drive**, with online document editing, calendar and contact synchronization, and more. Its openness avoids enforced quotas on storage space or the number of connected clients, instead having hard limits defined only by the physical capabilities of the server.

There are also some similar substitutes to **ownCloud** such as **nextCloud**, etc.

## Setup

### Environment
You need `LAMP` environment prior to the **ownCloud** setup.

**Note:** Highly recommend `PHP5` instead of `PHP7`. (You need to add some modules of `PHP`, but `PHP7` doesn't work well)

### OwnCloud part
#### Download ownCloud
download **ownCloud** first:

	$ wget https://download.owncloud.org/community/owncloud-9.1.4.zip
	
unzip the package and move it to the directory under apache service:
	
	/usr/local/apache/htdocs/owncloud
	
#### Create database for ownCloud
start mySQL first:

	$ sudo mysql -u root -p
create a new database for **ownCloud**:

```	
MySQL [(none)]> CREATE DATABASE owncloud;
MySQL [(none)]> GRANT ALL ON owncloud.* to 'owncloud'@'localhost' IDENTIFIED BY 'liruochen1998';
MySQL [(none)]> FLUSH PRIVILEGES;
MySQL [(none)]> exit
```

#### Visit your ip-address and finish the setup
You will need to visit `ip-address:80/owncloud` in the browser and setup a new account for **ownCloud**. 
You will also need to connect this account with the MySQL database that you just created.

#### Done!
After create your account and link your server to a database, you are all set!

### Problem solving!
#### ownCloud
>can't write into "config" directory.  

**Solution:**  

```
$ chown –R apache:apache $owncloud_path  
$ chmod –R 777 $owncloud_path 
```
reference: [https://blog.csdn.net/xuhuiyue/article/details/73554909](https://blog.csdn.net/xuhuiyue/article/details/73554909)

>everyone can read your data, you need to modify xxx.

**Solution:**  
modify the permission of the directory:  
	$ chmod -R 770 $ownCloud_PATH

>can't read the modules: zip, gd, cURL, and intl modules.

**Solution:**  

* `zip` module: need `libzib` reliance
* `gd` module: need a lot of reliance prior to install
* `cURL` module: normal.
* `intl` module: very hard to install on `PHP7`, which is the reason that I recommend `PHP5`

Two ways to install these modules:  

1. In the directory `/usr/local/php/bin/`, you can use pecl to download and install easily.
  	
 ```		
 $ ./pecl search file-name  
 $ ./pecl install file-name
 ```
 After installation, you will get a directory that has your `xxx.so` or `xxx.dll`.  

2. In the folder that you unzip the `php5.tar.gz`, you can find a module folder `/root/php5/ext`. You will find all the modules(including what you installed or not installed)

```
$ cd /root/software/php-5.6.5/ext/gd
$ /usr/local/php/bin/phpize
$ ./configure --with-php-config=/usr/local/php/bin/php-config --with-png-dir --with-freetype-dir --with-jpeg-dir --with-gd
$ make
$ make install
```
After installation, you will get a directory that has your module installed.

Now, through either way can you get the directory of the installed module location, just add some configuration in `php.ini`.

In `/etc/php.ini`, you can find lines `;extension=`, add:  
`extension=$module_path_you_just_get` or `extension=xxx.so`.

**Note:** Everytime you modify `php.ini`, you'd better restart `apache`.

## Reference
useful:  
[https://www.cnblogs.com/zjhblogs/p/6004254.html](https://www.cnblogs.com/zjhblogs/p/6004254.html)  
[https://blog.csdn.net/cymen/article/details/72885545](https://blog.csdn.net/cymen/article/details/72885545)  
[https://www.orgleaf.com/135.html](https://www.orgleaf.com/135.html)  
normal:  
[http://blog.51cto.com/ccj168/2084441](http://blog.51cto.com/ccj168/2084441)  
[https://blog.csdn.net/rain_yunlx/article/details/79478985](https://blog.csdn.net/rain_yunlx/article/details/79478985)  
