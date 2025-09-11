
# Sprint 1: Protocols Design Journal

##  1.1: microcontroller -> human
Process: 
- Install ESP32 board
- Upload files

Challenges & Learning:
- When downloading the Esp 32 driver, I encountered problem with using the wrong link, then with the correct link, I was able to successfully download and upload codes onto ESP 32
- When setting us the board, I had trouble with connecting and I learned that when choosing port, can tell from th ename of port, boards are usually named wtarting with usb
- The bit rate needs to change according to the board to 115200 from the tools colum\
- Added code: serial begin , serial delay to have it shows up on the serial moniter.


Photo/video
caption
### 01_helloworld
### 02_helloworld_spell
### 03_altering_periodicity
### 04_make_it_blink
### 05_make_it_blink_outside
<img width="341" height="498" alt="image" src="https://github.com/user-attachments/assets/abca07ad-1cf5-415d-8d9a-70da682e0dfc" />


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
















