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
