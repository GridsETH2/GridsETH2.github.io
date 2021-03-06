## ความต้องการของระบบ

**เซิร์ฟเวอร์** เพื่อประสิทธิภาพ ความเสถียร และการทำงานที่ดีที่สุด เราได้จัดทำเอกสารคำแนะนำบางประการสำหรับการรันเซิร์ฟเวอร์ Nextcloud 

| แพลตฟอร์ม    	| ตัวเลือก                                       	|
|-------------	|----------------------------------------------	|
| ระบบปฏิบัติการ 	| - Ubuntu 20.04 LTS                           	|
| ฐานข้อมูล     	| - MySQL 8.0+ หรือ MariaDB 10.2/10.3/10.4/10.5 	|
| เว็บเซิร์ฟเวอร์ 	| - Apache 2.4 พร้อม mod_php หรือ php-fpm        	|
| PHP Runtime 	| - 8.0                                        	|         

**หน่วยความจำ** ข้อกำหนดด้านหน่วยความจำสำหรับการรันเซิร์ฟเวอร์ Nextcloud นั้นแตกต่างกันอย่างมาก ขึ้นอยู่กับจำนวนผู้ใช้ แอพ ไฟล์ และปริมาณกิจกรรมของเซิร์ฟเวอร์

Nextcloud ความต้องการขั้นต่ำของ RAM คือ 128MB และเราขอแนะนำขั้นต่ำของ RAM => 512MB

**ข้อกำหนดฐานข้อมูลสำหรับ MySQL/MariaDB**

ปัจจุบันจำเป็นต้องมีสิ่งต่อไปนี้หากคุณใช้งาน Nextcloud ร่วมกับฐานข้อมูล MySQL/MariaDB:

- เอ็นจิ้นการจัดเก็บ InnoDB (ไม่รองรับ MyISAM)
- ระดับการแยกธุรกรรม "READ COMMITED"
- ปิดการใช้งานหรือ BINLOG_FORMAT = ROW กำหนดค่าการบันทึกไบนารี (ดู: https://dev.mysql.com/doc/refman/5.7/en/binary-log-formats.html )
- สำหรับการสนับสนุน Emoji (UTF8 4 ไบต์)

**ไคลเอนต์เดสก์ท็อป**

- Windows 7+
- macOS Lion (10.7)+ (64 บิตเท่านั้น)
- Linux (CentOS 6.5+, Ubuntu 14.04+, Fedora 21+, openSUSE 13, SUSE Linux Enterprise 11 SP3+, Debian 8 (Jessie)+, Red Hat Enterprise Linux 7)

**แอพมือถือ**

เราขอแนะนำอย่างยิ่งให้ใช้ระบบปฏิบัติการมือถือเวอร์ชันล่าสุดเพื่อรับประสบการณ์ที่สมบูรณ์และเสถียรที่สุดจากแอพมือถือของเรา

- iOS 11.x+
- Android 4.x+

**_บันทึก :_** _แอป Nextcloud Talk ที่แยกต่างหากต้องใช้ iOS 10.x+ หรือ Android 5.x+_

**เว็บเบราว์เซอร์**

เพื่อประสบการณ์การใช้งานเว็บอินเทอร์เฟซ Nextcloud ที่ดีที่สุด เราขอแนะนำให้คุณใช้เบราว์เซอร์เวอร์ชันล่าสุดและเวอร์ชันที่รองรับจากรายการนี้ หรือเบราว์เซอร์ที่อิงตามสิ่งต่อไปนี้

- Microsoft Edge
- Mozilla Firefox
- Google Chrome /Chromium
- แอปเปิ้ลซาฟารี

**_บันทึก :_** _หากคุณต้องการใช้ Nextcloud Talk คุณควรใช้ Mozilla Firefox 52+ หรือ Google Chrome /Chromium 49+ เพื่อสัมผัสประสบการณ์เต็มรูปแบบกับแฮงเอาท์วิดีโอและการแชร์หน้าจอ Google Chrome/Chromium ต้องการปลั๊กอินเพิ่มเติมสำหรับการแชร์หน้าจอ_
