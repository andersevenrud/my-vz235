# Slicer Setup

OrcaSlicer is preferred

> OrcaSlicer comes with a AWD profile that can be modified for all nozzle sizes.

## Parameters

These are the default parameters:

* Bed shape: 220x220
* Max print height: 200
* Firmware retraction: Yes
* Maximum feedrate X: 800
* Maximum feedrate Y: 800
* Maximum feedrate Z: 20
* Maximum feedrate E: 120
* Maximum acceleration X: 50000
* Maximum acceleration Y: 50000
* Maximum acceleration Z: 1500
* Maximum acceleration E: 15000
* Maximum acceleration when extruding: 50000
* Maximum acceleration when retracting: 15000
* Maximum jerk X: 0
* Maximum jerk Y: 0
* Maximum jerk Z: 0
* Maximum jerk E: 0
* Extruder clearance: 45mm radius, 36mm to rod, 140mm to lid

## Speed profiles

TODO. Currently calibrating, however the Vz official ones seems to be OK.

## Macros

### Start G-Code

```gcode
START_PRINT EXTRUDER_TEMP={first_layer_temperature[initial_extruder]} BED_TEMP={bed_temperature_initial_layer_single} FILAMENT_TYPE={filament_type[0]} FILAMENT_VENDOR={filament_vendor[0]}
SET_PRINT_STATS_INFO TOTAL_LAYER=[total_layer_count]
```

### End G-Code

```gcode
END_PRINT
; total layers count = [total_layer_count]
```

### Before layer change G-Code

```gcode
;BEFORE_LAYER_CHANGE
G92 E0
;{layer_z}
```

### After layer change G-Code

```gcode
;AFTER_LAYER_CHANGE
SET_PRINT_STATS_INFO CURRENT_LAYER={layer_num + 1}
;{layer_z}
```

### Color change G-Code

```gcode
PAUSE
```

### Pause print G-Code

```gcode
M25 ; pause print
```
