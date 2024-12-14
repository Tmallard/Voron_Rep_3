# Voron_Rep_3
Config and Documents for Voron_Rep_3
https://klipper.discourse.group/t/btt-relay-v1-2-with-skr-mini-e3-v3-0-shuts-down-before-klipper-loads/15340
Find PS-ON pin 
During Make Menu Config assign Desiered pin to be set hi
Reflash Firmware
Maco Exmaples
[output_pin power_detect]

# Sienos Macro 
[respond]

[output_pin power_detect]
Pull the pin initially high after starting Klipper
pin: PC13
value: 1
shutdown_value: 0

[gcode_macro POWER_ON]
description: Turn on the printer via the relay
gcode: 
    SET_PIN PIN=power_detect VALUE=1

[gcode_macro POWER_OFF]
description: Turn off the printer via the relay
gcode:
    { action_respond_info('Shutting down now') }
    SET_PIN PIN=power_detect VALUE=0

[gcode_macro DO_SHUTDOWN]
description: Turn off all heaters and cut power once below 60C
gcode:
   TURN_OFF_HEATERS
   TEMPERATURE_WAIT SENSOR=extruder MAXIMUM=60
   POWER_OFF
