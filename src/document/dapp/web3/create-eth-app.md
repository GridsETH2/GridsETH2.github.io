## create-eth-app

**ที่มา** : https://github.com/paulrberg/create-eth-app

**ขั้นตอนการติดตั้ง** : https://github.com/GridsETH2/MyMemoCreateEthApp

**เพิ่มเติม** : ติดตั้ง font-awesome จาก [cdnjs.com](https://cdnjs.com/libraries/font-awesome)

copy cdn ไปวางที่ `file ~/../ethw3dapp.project/packages/react-app/public/index.html` line 28
~~~javascript
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" />
~~~
## การพัฒนา

install @material-ui ในโฟลเดอร์โครงการด้วยคำสั่ง :
~~~
npm install @mui/material
~~~
import โมดูล material ที่ไฟล์ `../ethw3dapp.project/packages/react-app/src/App.js`
~~~javascript
import Button from '@material-ui/core/Button';
~~~
ในส่วนของ `<Header>` ทดสอบเพิ่ม `Button` ด้วย
~~~javascript
      <Button variant="contained" color="secondary" href="#contained-buttons">
        Link
      </Button>
~~~
ตอนนี้สีของ `Button` จะไม่เปลี่ยนแปลง ผมแก้ไขโดยเข้าไปแก้ใน `componancd/index.js`
~~~javascript
export const WaButton = styled.button`
~~~
กลับไปที่ไฟล์ `../ethw3dapp.project/packages/react-app/src/App.js` แก้ไขบันทัด `import { Body, Button, Header, Image, Link } from "./components";` ดังนี้
~~~javascript
import { Body, WaButton, Header, Image, Link } from "./components";
~~~
และใน `return ()` แก้ไขจาก `Button` เป็น `WaButton`
~~~javascript
return (
    <WaButton>
        ...
    </WaButton>
  );
~~~

### Create Component Navbar

ที่ `~/Documents/ExampleProject/EthW3dApp/ethw3dapp` ติดตั้ง `react-router-dom` ด้วยคำสั่ง
~~~
$ npm i react-router-dom
~~~

สร้างโฟลเดอร์ `[Nav]` ที่ `~/Documents/ExampleProject/EthW3dApp/ethw3dapp.project/packages/react-app/src/components/` 

ในโฟลเดอร์ `[Nav]` สร้างไฟล์ 2 ไฟล์ชื่อ `Navbar.js` และ `Navitems` จากนั้น Coding ตามนี้
- **[Navbar.js]()**
- **[Navitems]()**




