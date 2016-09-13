#Skill to have the Amazon Echo open/close the garage door.


Physical things that are needed to duplicate this project:
* Amazon Echo
* Arduino Yun
* relay

Ok... So how does this work?
This will help you build an alexa skill that will control an arduino yun using a rest service through Nearbus.
Nearbus is free and allows for the arduino to work without the need for port forwarding, and providing some security.

ALEXA---->AWS Lambda--->Nearbus--->Arduino Yun

In this example we are going to close and open a relay, but this could be modified for multiple garage doors,
or a number of arduino projects.  It should be noted that Nearbus has several different downloads available 
for multiple arduino boards, but I have a yun... so that is what this documentation is going to reflect.

# For Custom Slot Setup walkthrough
coming soon!
# For the Arduino Yun
coming soon!
need to comment on WProgram.h needing to be changed to Arduino.h in Nearbus lib to load.
	
As for the arduino yun,  you will want to get familiar with the arduino IDE software and load the sketch alexaBridgeexample to the yun.  This is a quick and ugly hack on the Bridge example.
In the sketch, the Yun is looking for a command coming from the web, when it recognizes it, it changes the pin status.  There is no Security on this, so keep that in mind with what you use this for.

When this is done, you should be able to have alexa set the digital pin 3 to low and cause the relay to close for one second and then open.	
If you want to test the arduino yun from your lan you can enter this into your browser
# your lan ip/arduino/digital/13/1               this should light pin13 
# your lan ip/arduino/digital/13/0               should turn it off.
	
