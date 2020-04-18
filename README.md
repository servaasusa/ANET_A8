# ANET_A8 (AM8) Notes

## Calibratate Printer
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
TODO
```
### Bed PID Autotune 
```
TODO
```
### Probe Offset + Z_SAFE_HOMING
```
#define BLTOUCH
#define NOZZLE_TO_PROBE_OFFSET { <your x delta>, <your y delta>, 0 }

#define Z_SAFE_HOMING

#if ENABLED(Z_SAFE_HOMING)
  #define Z_SAFE_HOMING_X_POINT ((X_BED_SIZE) / 2)    // X point for Z homing when homing all axes (G28).
  #define Z_SAFE_HOMING_Y_POINT ((Y_BED_SIZE) / 2)    // Y point for Z homing when homing all axes (G28).
#endif
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




Also See Wiki TAB!
