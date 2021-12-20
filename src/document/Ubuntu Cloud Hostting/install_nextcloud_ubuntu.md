## การติดตั้งบน Ubuntu 20.04 LTS

**ข้อกำหนดเบื้องต้นสำหรับการติดตั้งด้วยตนเอง**

ไฟล์เก็บถาวร Nextcloud .tar มีโมดูล PHP ที่จำเป็นทั้งหมด ส่วนนี้แสดงรายการโมดูล PHP ที่จำเป็นและเป็นทางเลือกทั้งหมด ศึกษาคู่มือ PHPสำหรับข้อมูลเพิ่มเติมเกี่ยวกับโมดูล การแจกจ่าย Linux ของคุณควรมีแพ็คเกจสำหรับโมดูลที่จำเป็นทั้งหมด คุณสามารถตรวจสอบสถานะของโมดูลโดยการพิมพ์ `php -m | grep -i <module_name>` หากคุณได้รับผลลัพธ์แสดงว่ามีโมดูลอยู่

Required:
- PHP (7.3 or 7.4)
- PHP module ctype
- PHP module curl
- PHP module dom
- PHP module filter (only on Mageia and FreeBSD)
- PHP module GD
- PHP module hash (only on FreeBSD)
- PHP module iconv
- PHP module JSON
- PHP module libxml (Linux package libxml2 must be >=2.7.0)
- PHP module mbstring
- PHP module openssl
- PHP module posix
- PHP module session
- PHP module SimpleXML
- PHP module XMLReader
- PHP module XMLWriter
- PHP module zip
- PHP module zlib

คุณสามารถใช้แพ็คเกจ .deb เพื่อติดตั้งโมดูลที่จำเป็นและแนะนำสำหรับการติดตั้ง Nextcloud ทั่วไป โดยใช้ Apache และ MariaDB โดย run คำสั่งต่อไปนี้ในเทอร์มินัล :

~~~
sudo apt update
sudo apt install apache2 mariadb-server libapache2-mod-php7.4
sudo apt install php7.4-gd php7.4-mysql php7.4-curl php7.4-mbstring php7.4-intl
sudo apt install php7.4-gmp php7.4-bcmath php-imagick php7.4-xml php7.4-zip
~~~

**_บันทึก :_** _ในการติดตั้ง `apache2 mariadb-server` จะใช้วิธี [ติดตั้ง LAMP บน Ubuntu 20.04](https://ubunlog.com/en/lamp-install-apache-mariadb-php-ubuntu-20-04/)_

## @Home

Check Version PHP
~~~
$ php -v

Command 'php' not found, but can be installed with:

sudo apt install php7.4-cli
~~~
Check Version Apache2
~~~
$ apache2 -v

Command 'apache2' not found, but can be installed with:

sudo apt install apache2-bin
~~~
Check Version MySQL
~~~
devg@devg-system:~$ mysql --version

Command 'mysql' not found, but can be installed with:

sudo apt install mysql-client-core-8.0     # version 8.0.27-0ubuntu0.20.04.1, or
sudo apt install mariadb-client-core-10.3  # version 1:10.3.32-0ubuntu0.20.04.1
~~~

**Install** `tasksel`

~~~
$ sudo apt install tasksel
~~~

**Install** `lamp-server`
~~~
$ sudo tasksel install lamp-server
~~~
Check Status Apache2
~~~
$ service apache2 status

● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor prese>
     Active: active (running) since Mon 2021-12-20 23:41:46 +07; 1min 52s ago
       Docs: https://httpd.apache.org/docs/2.4/
   Main PID: 20996 (apache2)
      Tasks: 6 (limit: 9444)
     Memory: 10.0M
     CGroup: /system.slice/apache2.service
             ├─20996 /usr/sbin/apache2 -k start
             ├─21001 /usr/sbin/apache2 -k start
             ├─21002 /usr/sbin/apache2 -k start
             ├─21003 /usr/sbin/apache2 -k start
             ├─21004 /usr/sbin/apache2 -k start
             └─21005 /usr/sbin/apache2 -k start

ธ.ค. 20 23:41:45 devg-system systemd[1]: Starting The Apache HTTP Server...
ธ.ค. 20 23:41:46 devg-system apachectl[20995]: AH00558: apache2: Could not reli>
ธ.ค. 20 23:41:46 devg-system systemd[1]: Started The Apache HTTP Server.
lines 1-18/18 (END)
~~~
Status = `Active: active (running)`

**_Note_** _For Restart Server Apache2 `service apache2 restart`_

Check Version Apache2
~~~
$ apache2 -v

Server version: Apache/2.4.41 (Ubuntu)
Server built:   2021-10-14T16:24:43
~~~
เรียกใช้คำสั่งต่อไปนี้เพื่อเปิดพอร์ต TCP 80
~~~
$ sudo iptables -I INPUT -p tcp --dport 80 -j ACCEPT
~~~
ตอนนี้เราต้องตั้งค่า www-data (ผู้ใช้ Apache) เป็นเจ้าของ รูทเอกสาร (หรือที่รู้จักในชื่อเว็บรูท) โดยค่าเริ่มต้น จะเป็นเจ้าของโดยผู้ใช้รูท
~~~
$ sudo chown www-data:www-data /var/www/html/ -R
~~~
โดยค่าเริ่มต้น Apache จะใช้ชื่อโฮสต์ของระบบเป็น ServerName หากชื่อโฮสต์ของระบบไม่สามารถแก้ไข ได้ใน DNS คุณอาจเห็นข้อผิดพลาดต่อไปนี้หลังจากรันคำสั่ง `sudo apache2ctl -t`
~~~
AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 127.0.0.1. Set the 'ServerName' directive globally to suppress this message
~~~
or
~~~
AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 2001:fb1:c4:8333:28a5:aee1:6a73:a4a9. Set the 'ServerName' directive globally to suppress this message
Syntax OK
~~~
เพื่อแก้ปัญหานี้ เราสามารถตั้งค่าโกลบอล ServerName ใน Apache โดยใช้ตัวแก้ไขข้อความบรรทัดคำสั่ง Nano เพื่อสร้างไฟล์การกำหนดค่าใหม่
~~~
$ sudo nano /etc/apache2/conf-available/servername.conf
~~~
เพิ่มบรรทัดต่อไปนี้ในไฟล์นี้
~~~
ServerName localhost
~~~
กด Ctrl+O จากนั้นกด Enter เพื่อยืนยัน Ctrl+X เพื่อออก จากนั้นเปิดใช้งานไฟล์กำหนดค่านี้
~~~
$ sudo a2enconf servername.conf

Enabling conf servername.
To activate the new configuration, you need to run:
  systemctl reload apache2
~~~
โหลด Apache ใหม่เพื่อให้การเปลี่ยนแปลงมีผล
~~~
$ sudo systemctl reload apache2
~~~
ตอนนี้ ถ้าคุณเรียกใช้ `sudo apache2ctl -t` อีกครั้ง คุณจะไม่เห็นข้อความแสดงข้อผิดพลาดด้านบน
~~~
$ sudo apache2ctl -t

Syntax OK
~~~
**Install MariaDB Database Server**

~~~
$ sudo apt install mariadb-client-core-10.3
~~~
so
~~~
$ sudo apt install mariadb-server mariadb-client
~~~



mysqld would have been started with the following arguments:
--user=mysql --pid-file=/run/mysqld/mysqld.pid --socket=/run/mysqld/mysqld.sock --basedir=/usr --datadir=/var/lib/mysql --tmpdir=/tmp --lc-messages-dir=/usr/share/mysql --bind-address=127.0.0.1 --query_cache_size=16M --log_error=/var/log/mysql/error.log --expire_logs_days=10 --character-set-server=utf8mb4 --collation-server=utf8mb4_general_ci 





















**Install** `phpmyadmin`
~~~
$ sudo apt install phpmyadmin
~~~
**Program with show ui : Package configuration**

- Package configuration : `[ ] apache2` and `<Ok>`

- Configure database for phpmyadmin with dbconfig-common? : `<Yes>` 

- MySQL application password for phpmyadmin : Password Ethereum2.0

**Check Status MySQL**

คุณสามารถใช้คำสั่ง mysqladmin เพื่อดูว่า mysql กำลังทำงานอยู่หรือไม่
~~~
$ mysqladmin -u root -p status
~~~

