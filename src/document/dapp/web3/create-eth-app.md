## create-eth-app

ที่มา : https://github.com/paulrberg/create-eth-app

ขั้นตอนการติดตั้ง : https://github.com/GridsETH2/MyMemoCreateEthApp

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
