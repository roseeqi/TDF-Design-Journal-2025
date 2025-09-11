
# Sprint 1: Protocols Design Journal
TDF Design Journal fall 2025, IND
Rose Qi

##  1.1: microcontroller -> human
Process: 
- Install ESP32 board
- Upload files

<img width="686" height="495" alt="image" src="https://github.com/user-attachments/assets/cf0012d4-4993-4289-8e7f-78684cfe4750" />
<img width="498" height="118" alt="image" src="https://github.com/user-attachments/assets/1eb4e630-2d2c-4b2d-a239-0ade6c38f371" />

Challenges & Learning:
- When downloading the ESP32 driver, I first used the wrong link, but after finding the correct one, I was able to successfully download it and upload code onto the ESP32.
- When setting up the board, I had trouble connecting. I learned that when choosing the port, you can identify it by name; board ports usually starts with "usbserial"
- The upload speed needs to be set to 115200 from the tools menu.
  <img width="179" height="76" alt="image" src="https://github.com/user-attachments/assets/541dcd75-654e-437c-9ab0-82674289919d" />
- Added code: serial begin , serial delay to have it shows up on the serial moniter.

### 01_helloworld
<img width="660" height="580" alt="image" src="https://github.com/user-attachments/assets/b2348f91-dd37-4bb9-a2a5-8e52d996f679" />
### 02_helloworld_spell
<img width="529" height="473" alt="image" src="https://github.com/user-attachments/assets/d30b5fd6-d0f4-4790-94f5-1f51ceb9defc" />
### 03_altering_periodicity

### 04_make_it_blink
### 05_make_it_blink_outside
<img src="https://github.com/user-attachments/assets/abca07ad-1cf5-415d-8d9a-70da682e0dfc" width="200">
<img width="383" height="340" alt="image" src="https://github.com/user-attachments/assets/ef8b1cfc-ffe4-4004-b602-620646a09919" />



**challenges for design journal: **
- how can we employ singular data types (primitives) used for the serial monitor communication:  what do we need to change in the serial printing methods?
- arrays:  how can we use arrays in the serial printing methods via Serial.printf() ?


## 1.2 microcontroller -> microcontroller via hardware serial
Process
- Connected two esp32
- Load up sender/reciever

Challenges & Learning:
- Px and Tx 交叉connected enable information to be transmitted from one board to another
- Learned code: Serial1.begin(9600, SERIAL_8N1, RX, TX)
- Needed to match baud rates between sender and receiver.


Photo/video
caption
<img width="619" height="462" alt="image" src="https://github.com/user-attachments/assets/3dcd9db1-f32b-45ef-9147-c37836bb4f22" />

challenges for design journal:  
- **what is needed to add a third device?  What sorts of opportunities does it afford w/r/t communications?**

## 1.3 integration with sensor boards
Process
- Connected sensor board APDZS-9960 to ESP32.
- Read values and printed them to Serial Monitor.

Challenge & Learning:
- Reading fluctuated, I changed it slower by adding delay

Photo/video
caption

**integrate all prior steps into a creative exercise**


## 1.4 microcontroller -> microcontroller via OSC
Process
- Install OSC library
- Edit wifi name and password
- Get IP address using file, get partner's IP address and
- Change 8888,9999, and give partner my
- upload file and send 

Challenge & Learning:
- A const was mis written, needed to delet a const 
- Private network and other network - our expermentation is very stable, while situation will not be the same when using bigger network
- 8888.9999 needs to be the same inorder for the message to be sent

Photo/video
caption

**make it your own**
















