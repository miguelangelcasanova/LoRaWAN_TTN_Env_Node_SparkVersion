# LoRaWAN_TTN_Env_Node_SparkVersion

Description : 
 - A low power BME280 based enviromental datalogger node for the ThingsNetwork with deepsleep support and variable interval using a LMIC ABP. Compatible with https://github.com/ph2lb/LoRaWAN_TTN_Env 
 
Revision : 
 - 2017-nov-2  1.1 changed BME280 library to SparkFun BME280 library (safes 200 byte flash and 12 bytes ram)
 - 2017-jul-17 1.0 first "beta" 
 
Hardware used : 
 - Arduino Pro-Mini 3.3V 
 - RFM95W
 - BME280 sensor.
 
Software and libraries used : 
 - LMIC https://github.com/matthijskooijman/arduino-lmic 
 - LowPower library https://github.com/rocketscream/Low-Power
 - MiniCore loader  https://forum.arduino.cc/index.php?topic=412070 https://github.com/MCUdude/MiniCore 
   To use a brownout detection of 1.8V.
 - special adcvcc library from Charles (see : https://www.thethingsnetwork.org/forum/t/full-arduino-mini-lorawan-and-1-3ua-sleep-mode/8059/32?u=lex_ph2lb )
 - SparkFun BME280 library https://github.com/sparkfun/SparkFun_BME280_Arduino_Library/
 
For licenses of the used libraries, check the links above.
 
 
Aditional note : 

I use a HTTP integration on the TTN with the decoder / payload function below.  :
   
    function Decoder(bytes, port) 
    {
      var retValue =   { 
        bytes: bytes
      };
      
      retValue.batt = bytes[0] / 10.0;
      if (retValue.batt === 0)
         delete retValue.batt; 
     
      if (bytes.length >= 2)
      {
        retValue.humidity = bytes[1];
        if (retValue.humidity === 0)
          delete retValue.humidity; 
      } 
      if (bytes.length >= 3)
      {
        retValue.temperature = (((bytes[2] << 8) | bytes[3]) / 10.0) - 40.0;
      } 
      if (bytes.length >= 5)
      { 
        retValue.pressure = ((bytes[4] << 8) | bytes[5]); 
        if (retValue.pressure === 0)
          delete retValue.pressure; 
      }
       
      return retValue; 
    } 
