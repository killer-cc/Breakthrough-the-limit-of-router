raspberry pi
==============

安裝 Apache PHP Mariadb Python3
------------------------------
	sudo apt install apache2 php php-mysql mariadb-server mariadb-client python3 -y

設定 MariaDB(自行設定)
------------------------------
	sudo mysql_secure_installation 

設定資料庫
------------------------------
	sudo mysql

### 建立資料庫
	create database proxy;
	use proxy;

### 設定專用帳號
	grant all privileges on proxy.* to 'proxy'@'localhost' identified by '[密碼]' with grant option;
	flush privileges;

### 建立table
	create table domains( domain VARCHAR(100) NOT NULL,PRIMARY KEY (domain));
	create table ips( ip VARCHAR(100) NOT NULL,PRIMARY KEY (ip));
		
### 設定完成，退出
	exit
		
設定網頁
------------------------------
	cd /var/www/html

### 取得權限
	sudo chmod 777 . -R

### 放置檔案
將[html的內容](https://github.com/killer-cc/Breakthrough-the-limit-of-router/tree/main/html/ "Title")使用任何SFTP軟體全部放到/var/www/html中

### 修改sql.php
	vim sql.php
將$password = 後面改成設定資料庫時的密碼

安裝V2RAY
------------------------------
	sudo su -c "bash <(curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh)"

設定 V2RAY
------------------------------
	sudo touch /usr/local/etc/v2ray/config.json.default

	sudo vim /usr/local/etc/v2ray/config.json.default

(内容查看[config.json.default](https://github.com/killer-cc/Breakthrough-the-limit-of-router/blob/main/v2ray-config/config.json.default/ "Title"))

自行查看[V2RAY](https://www.v2fly.org/config/overview.html/ "Title")設定Outbound，並自行架設外部伺服器

設定開機啓動python
------------------------------
	sudo vim /etc/rc.local
把啟動命令放到/etc/rc.d/rc.local檔

(内容查看<https://github.com/killer-cc/Breakthrough-the-limit-of-router/blob/main/v2ray-config/%E8%B7%AF%E5%BE%91.txt>)

	sudo chmod 744 /etc/rc.local

設定自動寄送IP到Email的程式
------------------------------
	vim /home/pi/mail.py

(内容查看[mail.py](https://github.com/killer-cc/Breakthrough-the-limit-of-router/blob/main/pi-home/mail.py/ "Title")) 

記得將Google帳號密碼還有接收的Email改成自己的(mail.py的8到13行)，並將低安全性應用程式存取權開啟

設定自動更新Routing規則的程式
------------------------------
	vim /home/pi/updateV2RAY.py

(内容查看[updateV2RAY.py](https://github.com/killer-cc/Breakthrough-the-limit-of-router/blob/main/pi-home/updateV2RAY.py/ "Title"))



使用方法
------------------------------
1. 瀏覽器打開 : **http://[raspberry_pi_IP]**
2. 選擇*Domain/IP*,輸入並保存
3. 電腦及手機使用Socks客戶端連接到 : **[raspberry_pi_IP]:1080**
4. 完成
