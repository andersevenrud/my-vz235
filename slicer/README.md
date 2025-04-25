# Slicer Setup

## Parameters

* Bed shape: 220x220
* Max print height: 200
* Firmware retraction: Yes

## Macros

### Start G-Code

```gcode
START_PRINT EXTRUDER_TEMP={first_layer_temperature[initial_extruder]} BED_TEMP={first_layer_bed_temperature[initial_extruder]} FILAMENT_TYPE={filament_type[0]} FILAMENT_VENDOR={filament_vendor}
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
M600
```

### Pause print G-Code

```gcode
M25 ; pause print
```
