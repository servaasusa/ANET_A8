# ANET_A8 (AM8) Notes

Place to download older (hard to find) versions of cura:
http://domoticx.com/3d-slicer-cura-software/

## Calibratate Printer (Marlin 2.0 firmware)
- https://github.com/MarlinFirmware/Marlin
- https://github.com/MarlinFirmware/Configurations

### Nozzle offset 
```
(Firmware configuration.h - requires board flash)
#define MANUAL_X_HOME_POS 0
#define MANUAL_Y_HOME_POS 0
```
### Extruder steps/mm
```
TODO
```
### Extruder PID Autotune 
```
  #define DEFAULT_Kp <value from Autotune>
  #define DEFAULT_Ki <value from Autotune>
  #define DEFAULT_Kd <value from Autotune>
```
### Bed PID Autotune 
```
  #define DEFAULT_bedKp <value from Autotune>
  #define DEFAULT_bedKi <value from Autotune>
  #define DEFAULT_bedKd <value from Autotune>
```
### Probe Offset + Z_SAFE_HOMING
```
#define NOZZLE_TO_PROBE_OFFSET { <your x delta>, <your y delta>, 0 }
#define Z_MIN_PROBE_ENDSTOP_INVERTING false  // Set to true to invert the logic of the probe.
#define BLTOUCH
#define Z_CLEARANCE_DEPLOY_PROBE    5 // Z Clearance for Deploy/Stow
#define AUTO_BED_LEVELING_BILINEAR // Untested
#define Z_SAFE_HOMING // Home Z when centered on bed
#define Z_SAFE_HOMING_X_POINT ((X_BED_SIZE) / 2)    // Adjust for probe offset?
#define Z_SAFE_HOMING_Y_POINT ((Y_BED_SIZE) / 2)    // Adjust for probe offset?
```
## Cura Settings based on (Thanks Daniel from https://www.crosslink.io/)
https://www.youtube.com/watch?v=LEvmc4FFa90
```
*** Cura Start GCODES: (set under printer config)
M117 Auto Home...
G28 ;Home
;G29 ;auto level. enable only if you have a probe!
M117 Priming Extruder...
G1 Z15.0 F6000 ;Move the platform down 15mm
G0 X0 Y0 F9000 ; Go to front
G0 Z0.4 ; Drop to bed
G92 E0 ; zero the extruded length
G1 X40 E25 F500 ; Extrude 25mm of filament in a 4cm line
G92 E0 ; zero the extruded length
G1 E-1 F500 ; Retract a little
G1 X80 F4000 ; Quickly wipe away from the filament line
M117 Printing...

*** Cura End GCODES: (set under printer config)
G4 ; Wait
M220 S100 ; Reset Speed factor override percentage to default (100%)
M221 S100 ; Reset Extrude factor override percentage to default (100%)
G91 ; Set coordinates to relative
G1 F1800 E-3 ; Retract filament 3 mm to prevent oozing
G1 F3000 Z20 ; Move Z Axis up 20 mm to allow filament ooze freely
G90 ; Set coordinates to absolute
G1 X0 Y{machine_depth} F1000 ; Move Heat Bed to the front for easy print removal
M117 Disabling Steppers
M84 ; Disable stepper motors
```

Marlin 119 setup summary:
#define Z_MIN_PROBE_ENDSTOP_INVERTING false  // Set to true to invert the logic of the probe.
#define BLTOUCH
#define X_PROBE_OFFSET_FROM_EXTRUDER 0   // X offset: -left  +right  [of the nozzle]
#define Y_PROBE_OFFSET_FROM_EXTRUDER -65   // Y offset: -front +behind [the nozzle]
#define Z_PROBE_OFFSET_FROM_EXTRUDER 0   // Z offset: -below +above  [the nozzle]
#define MIN_PROBE_EDGE 65 // Distance away from bed edges to probe
#define Z_CLEARANCE_DEPLOY_PROBE   5 // Z Clearance for Deploy/Stow
#define AUTO_BED_LEVELING_BILINEAR // Untested
#define Z_SAFE_HOMING // Home Z when centered on bed

Also See Wiki TAB!
