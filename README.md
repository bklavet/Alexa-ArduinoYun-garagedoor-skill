#Skill to have the Amazon Echo open/close the garage door.


Physical things that are needed to duplicate this project:
* Amazon Echo
* Arduino Yun https://www.amazon.com/Arduino-A000008-ATmega32u4-Microcontroller-Board/dp/B00MBCGWQQ/ref=sr_1_1?ie=UTF8&qid=1473784222&sr=8-1&keywords=arduino+yun
* relay https://www.amazon.com/SainSmart-101-70-100-2-Channel-Relay-Module/dp/B0057OC6D8/ref=sr_1_1?ie=UTF8&qid=1473784175&sr=8-1&keywords=SainSmart+2-Channel+Relay+Module

Ok... So how does this work?
This will help you build an alexa skill that will control an arduino yun using a rest service through Nearbus.
Nearbus is free and allows for the arduino to work without the need for port forwarding, and providing some security.
http://www.nearbus.net/ 

The flow of the skill is as follows...
# ALEXA---->AWS Lambda--->Nearbus--->Arduino Yun

In this example we are going to close and open a relay, but this could be modified for multiple garage doors,
or a number of arduino projects.  It should be noted that Nearbus has several different downloads available 
for multiple arduino boards, but I have a yun... so that is what this documentation is going to reflect.

Something to note:
I had to modify the NearBusYun_v15.h it wouldn't compile so I changed WProgram.h to Arduino.h
My changes have been saved to this github, but if you want to go directly through nearbus.  be prepared to make the same change.

# For the Arduino Yun

If this is your first rodeo with the Arduino Yun, or Arduino in general, this should be a good project to do
But you will want the Arduino IDE loaded on a computer 
Here's a link to get the Arduino IDE https://www.arduino.cc/en/Main/Software
Once you have that loaded you will need to add two libraries to the Arduino Libraries used by the Arduino IDE,
they have been provided on this github and can be found in the Arduino Yun Stuff folder.
FlexiTimer2
NearBusYun_v15

After all this has been done, hook your arduino yun to your computer with micro usb cord and get familiar with how to 
connect to your board with the IDE.  
If you need help: https://www.arduino.cc/en/Guide/ArduinoYun 

Open the yun_garage_2_template sketch.  It should load and be ready for you to edit with your information that you will soon have.

# NearBus setup
http://www.nearbus.net/ 
you will want to sign up and setup a login.
Select the New Device tab
you will see a number of parameters and values that need entry.  Not all of them are necessary here are the important ones
Device Name = What ever you want i used "Arduino"
Shared Secret= 8 digit char/number example "12345678" This will be used in the Arduino template sketch
PIN = 4 digit pin I put one in, but I am not sure if it is needed or not
Device Identifier = this will be provided and will be needed in the arduino sketch
Unclick Configured as VCMU

click "Setup"

# Back to the Arduino Yun

So open the sketch yun_garage_2_template sketch
towards the top you will see a section titled Agent Configuration Parameters
 char deviceId []  = ""; enter in your Device Identifier you got from NearBus between the quotes with no spaces.
 char sharedSecret[] ="" enter in your shared secret you got from NearBus between the quotes with no spaces.
 
 Scroll down to the section that says Example 2 - Digital Output
 you will see a line that says client.get("http://nearbus.net/v1/api_transp......)
 edit the http request with you Device Identifier, your username you use to log into nearbus, and password you use to log on to nearbus.
 
 What is happening in the sketch is the Yun is waiting to receive a command to close the relay, when it recieves this,
 it closes the relay for 1 second and then opens the relay.  Then the Arduino Yun sends a reset command back to Nearbus
 so everything goes back to the way it was.  This allows us to set up a skill with the echo that will give us 
 the same result of a closed relay for one second regardless of external influences (like people manually operating
 the garage door.
 
 Load this sketch to the arduino and set up your relay to digital pin 3 
 connect the arduino Yun to your internet connect via Wifi or ethernet
 log into Nearbus and check your device list the state should be Green and say up, if it does try this.
 open a browser and enter http://nearbus.net/v1/api_transp/NB10xxxx?user=xxxxxxx&pass=xxxxxxx&method=POST&reg00=1
 Make sure you update it with your information and hit enter.  
 
 the relay on the arduino should close for one second and then open.
 If it does, Great!  now we can build an alexa skill to control this with our voice!
 
# Alexa Skill Setup
coming soon! 

