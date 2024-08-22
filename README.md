Rebuild{Robotics} - https://wwww.rebuildrobotics.fi
# CombatBot_BeetleESP32C3_DCMotors_BLE_Android_V.1.1.2

Designed for 150-450 g combat robots controlled with Android smartphone/tablet via bluetoothLE. Controlling is done with Rebuild{Robotics} Bot Controller Android app.
In this version driving motors are controlled with HR8833 or TB6612FNG DC motor driver using PWM signal. Other version is available for motors drivers using PPM signal.
Script and controller can be also used to control basic Arduino based bots with servo.

  *****
  FEATURES:
  *****
  - High accuracy tank steering with center brake.
  - Channel mixing between ch1(fwd/bwd) and ch2(left/right) channels.
  - Motor rotation inverting and trim.
  - Support for single servo or brushless motor controlled by ESC as weapon motor.
  - 1-2S LiPo battery voltage monitoring.
  - Failsafe (Stops all functions when disconnected from controller).
  - Customizable AI slot (ch4, void runAI).
  - Buildin semiautomatic support in Custom AI slot for flippers using DFRobot VL6180X ToF Distance Ranging Sensor (Work in progress).
  - Bot name, weapon/servo presets, drive motor directions and trim levels can be updated straight from controller.
  - Necessary presets are stored in Eeprom.
  - Signal and variable debugging through serial monitor and led.
  - Onboard led indicates error-, standby-, bluetooth- and weapon statuses as followed:
      - Blink, dim/slow     =   Standby
      - Blink, bright/fast  =   Script weapon parameter error
      - Solid, dim          =   Bluetooth connected
      - Solid, bright       =   Weapon signal active

  *****
  HARDWARE:
  *****
  - DFRobot - Beetle ESP32-C3 (https://www.dfrobot.com/product-2566.html)
  - DFRobot - Fermion: HR8833 Thumbnail Sized DC Motor Driver 2x1.5A or TB6612FNG 2x1.2A DC Motor Driver (https://www.dfrobot.com/product-1492.html, https://www.dfrobot.com/product-1704.html)
  - DFRobot - Fermion: VL6180X ToF Distance Ranging Sensor (5-100mm) (https://www.dfrobot.com/product-2287.html) (Optional)
  - 5V BEC to convert battery voltage for boards and servo if needed (Included in ESP32-C3 CombatBot Expansion Board)
  - Rebuild Robotics - ESP32-C3 CombatBot Expansion Board
  - Rebuild Robotics - TinySwitch
  - Rebuild Robotics - TinyLED
  - 6V 600 > RPM Geared N10/N20 DC motors
  - Servo for flipper or brushless motor for spinning weapon
  - 2S 180-450mAh LiPo battery
  - 22 AWG Wires
  - BT2.0 Connector pair (Replace battery JST with BT2.0 male connector. Remember to prevent battery shortcut!)

  Rebuild Robotics products are coming for sale laterwards in upcoming webshop: https://wwww.rebuildrobotics.fi . At this moment you can ask them from me selling as private person.

  *****  
  OUTPUTS:
  *****
  - 2 PWM + 2 digital outputs for motor driver.
  - 1 Servo PPM output for weapon ESC or servo.
  - If using Bidirectional signal with ESC, it has to be enabled from ESC separately.
  
  *****
  ARDUINO IDE BOARD MANAGER & LIBRARIES:
  *****
  Tested stable versions:
    - Board:                  esp32 by Espressif Systems 2.0.13   Install from Arduino IDE
    - Weapon (PPM):           ESP32_New_ISR_Servo 1.4.0           Install from Arduino IDE
   
  Presets needed in Arduino IDE for serial monitoring and uploading script:
    - Tools > Board: > esp32 > DFRobot Beetle ESP32-C3
    - Tools > USB CDC On Boot > Enabled
    - Tools > Upload Speed > 115200
    - Tools > Erase All Flash Before Sketch Upload > Enabled = Erases all bot presets from Eeprom / Disabled = Keeps bot presets in memory.
 
  *****
  SAFETY:
  *****
  - Combat robotics is fun and extremely educating but dangerous hobby, always think safety first!
  - Script includes failsafe function to prevent up accidents. Function shuts down drive- and weapon motors when controllers signal is lost.
    This is same kind of option than good RC receivers have and it's required in combat robotics.
  - Remember to set pins correctly, if they are not set right script and failsafe won't work properly!
  - Do not keep battery connected at the same time when USB is connected into powersource!
  - Accidentally motor spins will happen when ESP is powered, script is uploading or wrong board or library version is installed!
    Motor spins at startup can be prevented by using pull-up/pull down resistors or our designed ESP32-C3 CombatBot Expansion Board and tested IDE library versions.
  - Configure ESC properly before connecting controller into bot, or it causes serious hazard!
  - Test bot with precaution and only weapon motor attached, not weapon itself!
  - Do not use any other board manager or library versions than those which are mentioned as tested and safe ones in this scripts read me area!
    It might cause serious injuries because board functionalities are changing. Future updates to this script includes fresher and tested information from later versions.
  - Remember always check that you have correct versions installed before updating script into board.
  - Modify script only if you know what you are doing!

  *****  
  COMMUNICATION:
  *****
  - Script uses 2,4GHz Bluetooth Low Energy (BLE) network to receive data from mobile phone controller as string.
  - Can handle incoming bluetooth messages in 20ms intervals.
  - String format ch1:ch2:ch3:ch4\n .
  - ch1 = fwd/bwd speed, ch2 = left/right speed, ch3 = servo angle or weapon speed, ch4 = AI on/off.
  - ch1 and ch2 values are in scale of -100~100, ch3 and ch4 0~100. 0 is stop. Signals are converted to PWM value scale 0~255. Negative numbers are absoluted.

  *****
  CONTROLLER:
  *****
  - Android: Rebuild Robotics - Bot Controller (Download from: https://github.com/RebuildRobotics).
  - Iphone: Not available, hopefully some day.
  - Controller is specially made for controlling combat robots and Arduino based bots.
  - Bot name, weapon/servo presets, drive motor directions and trim levels can be updated straight from controller.
    
  *****
  PRESETS:
  *****
  - Basic presets can be changed from controller or from script below.
  - Presets will be saved into Eeprom when updated from controller.
  - Presets saved in Eeprom will be erased in upload if "Tools > Erase All Flash Before Sketch Upload" is enabled.

  *****
  DEBUG:
  *****
  - Debug mode and serial monitoring can be enabled from below by changing "#define DEBUG" to true and reuploading script to ESP.
  - You might have to reset ESP once from button to get clean serial monitor output in start.
  - If facing problems uploading script and having "exit status 2..." error keep Arduino IDE open, plug ESP off from USB port, keep pressing Boot button while plugging ESP back into computer,
    reupload script and let go off from the Boot button when uploading has been started. https://wiki.dfrobot.com/SKU_DFR0868_Beetle_ESP32_C3
