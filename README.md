# How-to-connect-optical-rotary-encoder-with-Arduino

![image](https://user-images.githubusercontent.com/19898602/136206124-bac6bf63-6d6e-41ad-b485-7ef627be32d6.png)


Hello guys in this post we’ll learn how we can connect optical rotary encoder with arduino microcontroller.
First we get some information about what is optical rotary encoder.



## VIDEO
You can watch this video or continue to read below post

https://youtu.be/Y6BjnfwfzKE

# What is Optical rotary encoder

![OPTICAL-ENCODER-1_1](https://user-images.githubusercontent.com/19898602/136203701-f90239bd-9f47-4078-ac9b-bff41ba6fbf3.gif)


Optical rotary encoder is a mechanical device having a rotating shaft inside of cylindrical housing, construction look same as motor.
A circular flat disc having two sets of slot on it.
Optical sensors are attached on either sides of this disc, transmitter set on one side and receiver set on one side.

So when slotted disc rotate in between sensor it cuts the optical sensor and signal is generated at receiver ends.

Receiver is further connected with a microcontroller to process generated signal,
in this way we can know how much shaft is rotate.


we can also determine the direction of rotation of shaft by comparing the signal polarity of two outputs. because two sets of slots are at some offset

Optical rotary encoder general have two outputs “A” & “B” .

Below is the image to understand how 400 pulse per revolution encoder generate pulse it gives total 1600 transition per revolution. 

it means it can give very high accuracy.



![image](https://user-images.githubusercontent.com/19898602/136203785-d8145f1b-e8c5-46c7-a64d-eca59db791b2.png)

# Types of Encoders


Generally there is Two types encoders

> INCREMENTAL ENCODER


> ABSOLUTE ENCODER


# Incremental Encoders


This types of encoders gives pulse as output which can be treated as a incremental signal.

because it doesn’t have any unique vale of any unique position means when power gets off to this encoder it lost its position reference and start with zero.

# Absolute Encoders


This types of encoders are more advanced then incremental encoders.

meanwhile they have magnetic disc in place of slotted disc, so it have unique value of each and every position so it can remember its potion also after power off.

In this post we are going to learn about Incremental encoders.


# Connection optical encoder with arduino

Here I am using orange make rotary encoder which have 400 pulse per revolution

Below you can see the wire details of encoder

WHITE : OUTPU – A

GREEN : OUTPUT – B

BLACK : GND

RED : +5V DC

SHIED : GND


![image](https://user-images.githubusercontent.com/19898602/136204112-d0db26e5-9128-42c8-a53e-8a03f4027310.png)


connect optical rotary encoder with arduino as per below

>  WHITE (OUT A) : PIN 3 (interrupter pin of arduino)


>  GREEN (OUT B) : PIN 2 (interrupter pin of arduino)


>  RED : 5V


>  BLACK : GND

Here we have to note that the output from encoder that is wire green and white must be only connected to interrupt pin of orduino.


otherwise arduino not able to record every pulse from encoder.


you can learn more about interrupt pin on google.

![image](https://user-images.githubusercontent.com/19898602/136204236-2f32d418-11da-400f-9295-89a652d06119.png)

Before moving fuurther I would like to tell you something about PCB

Yes PCB are the heart of the electronics based project usually we hesitate to try custom PCB and opt to homemade solutions

like breadboard or Zero PCB earlier I also was in the same boat, I hesitate to try custom PCB my belief was they are much expensive.

but then I came to know about [JLCPCB.COM](https://jlcpcb.com/IAT) and I was totally surprised how low price PCB's are they offering 

there PCB quality is best in market, now I always go with PCB for my project and [JLCPCB.COM](https://jlcpcb.com/IAT) is my trusted 

PCB manufacturer, you can also try there PCB service for more details you can visit their website [JLCPCB.COM](https://jlcpcb.com/IAT)
You can also try there new purple colour for PCB without any extra cost.
![image](https://user-images.githubusercontent.com/19898602/134336832-cb9953e9-02a6-4ff7-9d27-2caad10fe7c7.png)
![image](https://user-images.githubusercontent.com/19898602/130722577-c30b7b43-ea89-4847-9c6b-058f9fabeda3.png)![image](https://user-images.githubusercontent.com/19898602/130722585-b5268db1-5f17-428f-ba60-b823140f2a70.png)



```javascript

volatile long temp, counter = 0; //This variable will increase or decrease depending on the rotation of encoder
    
void setup() {
  Serial.begin (9600);

  pinMode(2, INPUT_PULLUP); // internal pullup input pin 2 
  
  pinMode(3, INPUT_PULLUP); // internalเป็น pullup input pin 3
   //Setting up interrupt
  //A rising pulse from encodenren activated ai0(). AttachInterrupt 0 is DigitalPin nr 2 on moust Arduino.
  attachInterrupt(0, ai0, RISING);
   
  //B rising pulse from encodenren activated ai1(). AttachInterrupt 1 is DigitalPin nr 3 on moust Arduino.
  attachInterrupt(1, ai1, RISING);
  }
   
  void loop() {
  // Send the value of counter
  if( counter != temp ){
  Serial.println (counter);
  temp = counter;
  }
  }
   
  void ai0() {
  // ai0 is activated if DigitalPin nr 2 is going from LOW to HIGH
  // Check pin 3 to determine the direction
  if(digitalRead(3)==LOW) {
  counter++;
  }else{
  counter--;
  }
  }
   
  void ai1() {
  // ai0 is activated if DigitalPin nr 3 is going from LOW to HIGH
  // Check with pin 2 to determine the direction
  if(digitalRead(2)==LOW) {
  counter--;
  }else{
  counter++;
  }
  }


```


After uploading code to arduino, open serial monitor

and rotate encoder shaft you can see the value increase if you rotate encoder in clock wise direction, 

and value decrease if you rotate in counter clockwise direction.

If value are showing reverse means giving -ve value for clockwise motion.

you can reverse the “GREEN” & “WHITE” wire.

By using encoder we have made a cool project please check out it here

This is all for this tutorial hope this tutorial may helpful for you.



