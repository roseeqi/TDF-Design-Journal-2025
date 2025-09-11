# Sprint 1: Protocols Design Journal
TDF Design Journal fall 2025, IND
Rose Qi

##  1.1: microcontroller -> human
Process: 
- Install ESP32 board
- Upload files


Challenges & Learning:
- When downloading the ESP32 driver, I first used the wrong link, but after finding the correct one, I was able to successfully download it and upload code onto the ESP32.
- When setting up the board, I had trouble connecting. I learned that when choosing the port, you can identify it by name; board ports usually starts with "usbserial"

  <img width="300" height="495" alt="image" src="https://github.com/user-attachments/assets/cf0012d4-4993-4289-8e7f-78684cfe4750" />
- The upload speed needs to be set to 115200 from the tools menu.

  <img width="300" height="100" alt="image" src="https://github.com/user-attachments/assets/1eb4e630-2d2c-4b2d-a239-0ade6c38f371" />
- Added code: serial begin , serial delay to have it shows up on the serial moniter.

  <img width="179" height="100" alt="image" src="https://github.com/user-attachments/assets/541dcd75-654e-437c-9ab0-82674289919d" />

#### 01_helloworld
<img width="600" height="657" alt="image" src="https://github.com/user-attachments/assets/883e1c91-12de-4c4a-81eb-dac115a222d0" />

#### 02_helloworld_spell
<img width="600" height="636" alt="image" src="https://github.com/user-attachments/assets/7b2a63fb-e7cf-4a23-8b52-edfa3455fda6" />

#### 03_altering_periodicity
<img width="600" height="399" alt="image" src="https://github.com/user-attachments/assets/c17bfbbd-f2bb-429c-b814-bebcc9fc6d34" />

#### 04_make_it_blink
https://github.com/user-attachments/assets/54140ec6-176b-479f-b9b5-64d7857ca25e

#### 05_make_it_blink_outside
https://github.com/user-attachments/assets/528a8cc0-91f4-4546-9cb8-7a349695462a

<img src="https://github.com/user-attachments/assets/abca07ad-1cf5-415d-8d9a-70da682e0dfc" width="200">
<img width="383" height="300" alt="image" src="https://github.com/user-attachments/assets/ef8b1cfc-ffe4-4004-b602-620646a09919" />

#### Challenge Questions
- how can we employ singular data types (primitives) used for the serial monitor communication:  what do we need to change in the serial printing methods?

  For singular data types, change the format specifier in Serial.printf() to match the type.
- arrays:  how can we use arrays in the serial printing methods via Serial.printf() ?

  For arrays, loop through and print each element.


## 1.2 microcontroller -> microcontroller via hardware serial
Process
- Connected two esp32
- Load up sender/reciever

Challenges & Learning:
- Px and Tx were cross-connected to enable data transmission between boards.
- Learned code: Serial1.begin(9600, SERIAL_8N1, RX, TX)
- Needed to match baud rates between sender and receiver.

<img width="600" height="736" alt="image" src="https://github.com/user-attachments/assets/4fd9e702-efbe-47ef-9d3b-31bb85fa136f" />
Connected and transmitting successfully 

<img width="200" height="462" alt="image" src="https://github.com/user-attachments/assets/3dcd9db1-f32b-45ef-9147-c37836bb4f22" /> <img width="415" height="250" alt="image" src="https://github.com/user-attachments/assets/f0dcf942-fc44-4ffa-9c18-c83488f9e726" />

#### Challenges Question:  
- what is needed to add a third device?  What sorts of opportunities does it afford w/r/t communications?
  Adding a third device requires extra connections and additional Rx and Tx pins. It creates opportunities for multi-node communication, such as broadcasts

## 1.3 integration with sensor boards
Process
- Connected sensor board APDZS-9960 to ESP32.
- Read values and printed them to serial monitor.

Challenge & Learning:


- Reading fluctuated, I changed it slower by adding delay
  
https://github.com/user-attachments/assets/380ff0c4-13a3-431b-95d4-dcad1fd9eddd

Board APDZS-9960 recognizing color

https://github.com/user-attachments/assets/b1d105fb-26df-42d9-80dd-f9fbab584800

Board APDZS-9960 recognizing gesture


https://github.com/user-attachments/assets/9183fec2-6f2d-4416-960e-2362b9696021

Board APDZS-9960 recognizing proximity


https://github.com/user-attachments/assets/22624717-e717-4290-8a4e-09c645a530cc

Board APDZS-9960 with accelgyro

#### Integration: Brightness & distance reactive LEDs
This sketch used an APDS-9960 color sensor and an ultrasonic distance sensor. The APDS-9960 color sensor decides which LED is active. Green LED turns on under bright light, and red LED in dim light. The ultrasonic sensor measures distance, and the closer the object is, the faster the active LED blinks. 

https://github.com/user-attachments/assets/9c7fd7a4-c57a-496c-92cd-e5e6569889ab




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
<img width="1352" height="755" alt="image" src="https://github.com/user-attachments/assets/cd16ed3f-0404-4b56-8405-7d2e8bd34e52" />
















