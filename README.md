Warning: Test and validate this code to ensure it works for your needs. No warranty, guarantees are given. 

# Particle_SMS_Send_Read
This code will let you read incoming messages, process the commands from them and respond with a SMS confirmation.

## What Devices and Software does it work with?
    1. Particle Electron www.particle.io
    2. Particle Electron Firmware version 0.6.1 (as tested)
    3. Ublox module as integrated on the Particle Electron 2016-2017 model. 

## Thank you to:
1. ScruffR for providing the SMS send commands
    https://community.particle.io/u/scruffr/summary

2. Robynjayqueerie SMS library for uCommand.cpp and uCommand.h components and some other main file read SMS aspects.
    https://github.com/robynjayqueerie/electron-atcommand-library

3. Developer_BT for pointing me in the rirght direction for this project.
  https://community.particle.io/u/developer_bt/summary

## Overview:
  Send a SMS to the Particle device in the below format:
  <userCode>,<command>,<command_option>
  
  **Examples commands : 
  1. Turn D7 on
    1234,on
  2. Turn D7 off
    1234,off
  3. Change my passcode default of 1234 to 9999
    1234,newcode,9999
  4. Change the 'alert number' to a new number
    9999,newnumber,+61400000000
    
## Before Flashing to your device
Remember to change the 3 user specified variables toward the top of the readsms.ino file before flashing to your device
    
   1. STARTUP(cellular_credentials_set("telstra.extranet", "", "", NULL));  
   2. String alertNumber = "+614xxxxxxxx";  
   3. String userCode = "1234"; 

## What would I do, if given more time? Or.. love for someone else to branch fixes for?? ;)
    
   1. Test SMS lengths and impacts of sending long messages over two SMS's to the device
   2. Swap out all String references for char
   3. Swap if statements for 'case' to make it a bit cleaner
   4. Include more error processing and checking
   5. Investigate the impact of using > STARTUP(cellular_sms_received_handler_set(smsRecvCheck, NULL, NULL)); --instead of say an interrupt >     attachInterrupt(RI_UC, smsRecvCheck, CHANGE);
   6. Add in some more robust SMS rate limiting to prevent the device being kicked off the SMS/3G network for spamming or getting stuck in a loop somehow where it sends too many SMS's. Good to have as a precaution. 
   7. Add in the save to non-volatile memory for userCode and alertNumber so changes saved are not lost on reboot.
