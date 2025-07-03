# Calibration

A brief guide on how to calibrate the printer.

## AWD Sync

This is best done with a tension of 100Hz or below (but no slack).

1. Unscrew motor tension set screws on front steppers
2. Unscrew the grub screws on front stepperS
3. Move gantry around, and back to initial position
4. Run `ACTIVATE_STEPPERS` macro
5. Tighten the grub screws on front steppers

Leave motor tension screws lose and do a belt tensioning afterwards.

## Belt Tension

Use a mobile app and pluck the inside part of the belt in front while the
toolhead is parked in the middle of the bed. The frequency should be around 180Hz.

This should be done after AWD sync.

1. Move the printhead to the center of the bed
2. Loosen the front motor tension set screws
3. Adjust front tension screws and measure frequency
4. Tighten the front motor tension set screws

This requires a Resonance Calibration afterwards.

## Bed Tramming

First tram by hand with a feeler gauge and tighten adjustment wheels until the resistance feels the same on all four corners.

Then home and run `SCREWS_TILT_CALCULATE` for automatic probing and then adjust accordingly (00:01 is fine).

## Bed Mesh

This is done automatically upon job start with an adaptive method to only scan the area required to print.

## X/Y Offsets

The general printable area of the 235x235mm bed is 220x220mm.

Make a dot with a marker in the left corner on the build plate (15x15mm from the edge).

Home and go to `0x0`. The nozzle should line up with the dot.

Adjust the `position_endstop` and `position_min` as needed in the printer configuration.

## PID Tuning

### Bed

```
PID_CALIBRATE HEATER=heater_bed TARGET=80
```

### Extruder

```
PID_CALIBRATE HEATER=extruder TARGET=250
```

## Extrusion

### E-steps (rotation distance)

Detach the PTFE tube from the extruder.

Warm up the extruder to the recommended temperature of the filament used during test.

Feed some filament to ensure everything is primed. Mark out 120mm of filament from the entry of the extruder
with some tape or a pen.

Extrude 100mm of filament at 1mm/s, then measure how much is left.

For example, there's 2mm left over (which means 98mm was extruded) and the current rotation distance is `35.8`, then the
calculation for a new value would be:

```
35.8 * (100 / 98)

= 36.53061224489795918335
~ 36.5
```

### Temperature

Print a temperature calibration tower in OrcaSlicer and see which gives the best result
on overhangs and overall quality without too much stringing.

### Pressure Advance

Print a pressure advance pattern test in OrcaSlicer and see which gives the best result
with sharp corners and no gapping in the lines and around the anchors.

Usually a value of 0.025 for non-flexible filaments.

### Retraction

Print a retraction test in OrcaSlicer and see which gives the best result.

## Speeds

Use the included Ellis' speed test macro and look for missed steps after a run finishes.

### Square Corner Velocity (SQV)

General calculation is `acceleration / 1000`.

## Probe

The Cartographer probe is simple when the bed has been succesfully trammed.

Ensure it's in touch mode:

```gcode
PROBE_SWITCH MODE=touch
SAVE_CONFIG
```

### Set up offset

Now, home the printer and move to center of bed:

```gcode
G28 X Y
G0 X110 Y110
```

Then proceed with the "paper method" of setting an offset using the Mainsail interface:

> The nozzle should only *barely* touch the nozzle. Move until you feel resistance, then back up slightly.
> Ensure the nozzle is clean, but do not use a metal brush!
>
> A dialog will appear after running this command

```gcode
CARTOGRAPHER_CALIBRATE METHOD=manual
```

Then `SAVE_CONFIG` to save the offset.

### Check tolerances

Check the accuracy of the probing:

```gcode
PROBE_ACCURACY
```

Then calculate the backlash and save it to the printer configuration file:

> Look for `Median distance moving up` in the console output.

```gcode
CARTOGRAPHER_ESTIMATE_BACKLASH
```

### Set up touch

First, home the printer:

```gcode
G28
```

Then run the automated job to find the touch threshold:

> Watch this process. The nozzle should touch the bed after a while.

```gcode
CARTOGRAPHER_THRESHOLD_SCAN
```

After a successful run, do the calibration:

```gcode
CARTOGRAPHER_CALIBRATE
```

Now you can `SAVE_CONFIG` and proceed to print a 0.2 thick rectangle and adjust the z-offset as needed
to get a perfect first layer.

## Resonance Calibration

Use the included "ShakeTune" macros and run a `AXES_SHAPER_CALIBRATION` to automatically measure all axes.

The recommended values will be printed to the console and can be applied to the printer configuration.

## Bed Model Calibration

The `default` profile that is created during the Cartographer calibration should suffice for most scenarios
but it is possible to create different models based on what bed plate is used, i.e.:

```gcode
CARTOGRAPHER_MODEL_SELECT NAME=flat
CARTOGRAPHER_CALIBRATE
SAVE_CONFIG

CARTOGRAPHER_MODEL_SELECT NAME=textured
CARTOGRAPHER_CALIBRATE
SAVE_CONFIG
```

## RSCS

The ducts should be approx 3-4mm above the build plate.

> The gauge can be just a simple 3-4mm thick piece of cardboard or plastic, it just has to
> be straight and reach from the edge of the bed and under the ducts.

1. Unscrew top vent scews on both sides
2. Move Z to 0
3. Place the gauge on the bed and raise/lower the duct until it rests on the gauge
4. Ensure both ducts are level
5. Tighten screws

## Nozzle wiper

It should be calibrated so that the nozzle penetrates the wiper material by 0.5 - 1.0 mm.

### Arm

First calibrate the angle of the wiper arm:

> Move the arm close to the switch by hand first and ensure bed is 20mm+ away.

```
# Home arm first
MANUAL_STEPPER STEPPER=wiper MOVE=-1000 STOP_ON_ENDSTOP=1 SPEED=2000
MANUAL_STEPPER STEPPER=wiper SET_POSITION=0

# Extend arm
MANUAL_STEPPER STEPPER=wiper MOVE=845 SPEED=2000
```

Now adjust the `845` value in the gcode and re-run that step as needed until the arm is
perfectly horizontal when extended.

Add this value to the `WIPE_NOZZLE` macro paramters and retract the arm:

```
MANUAL_STEPPER STEPPER=wiper MOVE=0
```

### Body

Now adjust the body up/down until the nozzle can dig the wiper material by 0.5 - 1.0 mm.

Ensure everything is straight and tighten the screws.

### Bed

With the printer homed and arm retracted, move Z to 20mm+, extend the arm
and then jog the bed upwards slowly (down to 1mm) until the screws under the
arm barely hits the bed. Fine tune until touching.

### Macros

Now adjust the `MIN_` and `MAX_` values in the `WIPE_NOZZLE` macro to ensure
the nozzle stays on the pad in the Y-direction and the nozzle goes 5-10mm
(or as needed) outside the pad in the X-direction.

You can find these values by jogging the head and note down the values.
