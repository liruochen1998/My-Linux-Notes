# Shadowsocks

![Shadowsocks icon](https://en.wikipedia.org/wiki/File:Shadowsocks_logo.png)

## Shadowsocks
**Shadowsocks** is an open-source encrypted proxy project, widely used in mainland China to circumvent Internet censorship. It was created in 2012 by a Chinese programmer named "[clowwindy](https://web.archive.org/web/20120422191812/http://www.v2ex.com/t/32777)", and multiple implementations of the protocol have been made available since. 

Typically, the client software will open a socks5 proxy on the machine it is run, which internet traffic can then be directed towards, similarly to an SSH tunnel. Unlike an SSH tunnel, shadowsocks can also proxy UDP traffic.

## ShadowsocksR
**ShadowsocksR** is a fork of the original project, claimed to be superior in terms of security and stability. Upon release, it was found to violate the General Public License by not having the source code of the C# client available. It was also criticized for its solution to the alleged security issues in the source project. Both projects are currently under development.

## Setup
This only shows the utilization of **SSR**, recording the steps how I setup **SSR** in my VPS.

### login to your VPS
```
$ ssh -l root@ip-address
$ Enter password:
```
### install SSR
update `yum` first   

```
$ yum update -y
$ yum install unzip zip -y
$ yum install wget -y
```
download, unzip and install **SSR**

```
$ wget -N –no-check-certificate https://raw.githubusercontent.com/Moexin/Easy-SSR-Bash-Python-The-Final/master/ssr.zip
$ unzip ssr.zip
$ cd SSR*
$ bash install.sh
```
### install bbr to speed up

```
$ wget https://github.com/teddysun/across/raw/master/bbr.sh
chmod +x bbr.sh
$ ./bbr.sh
```

## Done!
When you want to start **SSR**, type `ssr` and you will see the user interface. 

![UI screenshot]()


