#Skill to have the Amazon Echo open/close the garage door.

When this is completed a person could create an IFTTT recipe using the iOS Location/Android Location, and the Maker channel to create some geofencing.


Physical things that are needed to duplicate this project:
* Amazon Echo
* Arduino Yun
* relay

You will also need a Nearbus account (It is easy to sign up and free)

Ok... So how does this work?
Alexa hears a command to "turn on the garage door".  The Echo sends this command to AWS Lambda that then sends a Restful url to Nearbus that turns on the Yun's Digital Pin 3 closing the relay that allows the garage door to open/close.

Not so bad.
So hear are the steps.

1.  You will need a Nearbus account.
    Go here and set up an account.
    http://nearbus.net/index.php
    Click on Device List and select the HELLO WORLD example or go here:
    http://nearbus.net/wiki/index.php?title=App_Note_1218_-_Hello_World

2.  This is where you will want to take out your arduino yun.
    If this is your first time working with arduino you will want to load the IDE on your PC.
    for that go here. 
    http://arduino.cc/en/Main/Software
    follow the Hello World example (http://nearbus.net/wiki/index.php?title=App_Note_1218_-_Hello_World)
    NOTE in the Hello World example you will download the nearbus lib and I could not get it to compile in the Arduino
    this is because the IDE did not like WProgram.h.  You will need to open the NearbusYun_v15.h file with an editor
    (I use Notepad++)  If you use Notepad++ you can go to Search and select Replace.  the enter WProgram.h in the "Find What" box and then Type Arduino.h in the "Replace with" box, and select replace and save.  Close out the Arduino IDE if you        have it open, and reopen the program again and it should now compile.

3.  So for now, you have an Arduino Yun that has the Hello World example sketch running on it.
    
    We need to know that nearbus can see the Yun.  Log into nearbus.net and select DEVICE LIST, and verify that the State is UP/Green.  If it is you are doing great.  If not, go back and try again.
    You will notice that when you are seeing your device on the nearbus site that there is a drop down menu below it.  Using the drop down menu select "EDIT DEVICE".  
    The window that opens up will need a small change.  UNCHECK CONFIGURED AS VMCU!  This will put it in TRNSP mode.  It will look Red in the Configure tab.  Do not worry about that.

4.  So now is the time to hook the YUN back up to the PC and open the arduino IDE for one more go. This is where you will want to open my sketch and modify your information into it and load on to the YUN.  
    you will want to modify here:
    line 29 char deviceId []    = "Nearbus DEVICE ID"  to your device id that nearbus has assigned. put your device ID between the ""
    line 30 char sharedSecret[] = "Shared Secret"  This can be found in the Edit Devices tab on nearbus.  This is not your PIN.  It is the 8 digit number in the Shared Secret space. 
    line 206 client.get ("http://nearbus.net/v1/api_transp/NB101000?user=nearbus_logon_name&pass=nearbus_logon_password&method=POST&reg00=0");

    You will want to place your nearbus device ID in place of NB101000, and put in your nearbus login name and password.
                                  
    Load sketch to YUN, and connect it to the internet.  Verify that device is in the UP state on the nearbus site.
    at this point open a window in your browser and enter this, but modified with your information 
    "http://nearbus.net/v1/api_transp/NB101000?user=nearbus_logon_name&pass=nearbus_logon_password&method=POST&reg00=1"
    notice the the last digit has been changed to a 1 make sure you do not forget that.
    
    Hit enter.  you should see the relay close for one second and then open.  Everytime this url is entered the relay should respond by closing for one second and opening.

5.  So if that URL is closing the relay, it is time to put that url into the Index file for the Alexa skill. "http://nearbus.net/v1/api_transp/NB101000?user=nearbus_logon_name&pass=nearbus_logon_password&method=POST&reg00=1"
    notice the the last digit has been changed to a 1 make sure you do not forget that.

    



