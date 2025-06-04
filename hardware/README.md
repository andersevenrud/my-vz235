# Hardware

A QuadXY FFF/FDM 3D printer.

## Specifications

* Optimal print volume: 220x220x200mm
* Max print volume: 235x235x220mm
* Max acceleration: 50000mm/s^2
* Max movement speed: 1000mm/s
* Max volumetric speed: 50mm^3/s
* Max chamber temperature: 50C
* Max bed temperature: 120C
* Max hotend temperature: 300C
* Stepper voltage: 48V X/Y, 24V Z
* Enclosure: Yes; front Doors, top Hat
* Lighting: Yes; White overhead, RGB Neopixel ambient
* Camera: Yes (Full HD, Wide Angle)
* Chamber heating: Passive
* Exhaust: Filtered
* Filament Management: Cutter
* Parts Cooling: CPAP, RSCS
* Bed Probe: Eddy (Touch and Scan)
* Bed Tramming: Manual
* Bed Plate: Magnetic, PEI, Double-sided
* Display: 5" LCD w/touch

### Power draw

Approximate values:

* Idle (after cold boot): < 50W
* Active (homed, all steppers active): < 90W
* Heat soaking (while active): ~ 200W - 750W
* Printing (standard petg profile): ~ 120W - 300W

## Parts

All assembly parts were printed with ABS

* Frame
    * 2020 Black Aluminum Extrusion
    * 3mm Polycarbonate glass side panels
    * 3mm aluminum back/bottom panels
    * DIN Rails for electronics attachment
    * Rubber feet (25mm)
* Bed
    * LDO 42STH48-2504AC stepper
    * TMC2240 driver
    * Mellow double-sided PEI spring sheet
    * Mellow 8mm aluminum bed
    * Mellow 500W (220V) silicone heater
    * Omron G3NB-1 Solid State Relay
    * Silicone solid mounts
    * Gates 40T pulleys
    * Mellow NF Oldham couplers
    * Fushi LM10LUU (x4)
    * Optical Axis Chrome plated rods (x4)
    * SHOOMO T8 lead screws (x2)
* Gantry
    * LDO 42STH48-2804AH(S40R) long shaft stepper (x4)
    * TMC5160 Pro driver (x4)
    * Mellow aluminum long shaft motor mounts
    * Mellow aluminum gantry
    * Mellow aluminum gantry rail
    * Mellow lightweight aluminum spacers
    * Mellow Titanium screws and bolts
    * HIWIN MGN12H Linear X Rails (x2)
    * HIWIN MGN9H Linear Y Rail
    * Gates 20T pulleys/idlers
    * Gates 2GT 6mm belt
    * Jinger micro switch endstops
* Toolhead
    * Moons CSE14HRA1L410A-01 stepper
    * TMC2240 driver (24V)
    * Mellow HextrudORT Low PLUS (60:10)
    * Mellow Vz Printhead MGN9 (Clone)
    * Mellow Magneto Cutter
    * Cartographer 3D eddy probe
    * Phaetus Rapido 2.0 UHF hotend
    * Bondtech Bi-Metal CHT 0.6mm Volcano nozzle
* MCUs
    * BTT Octopus Pro v1.1
    * Raspberry Pi 4 Host
* Temperature Control
    * Mellow WS7040 24V CPAP Blower fan
    * Mellow 15mm CPAP fan pipe
    * WINSINN 2510 24V Hydraulic dual bearing hotend cooling fan
    * Sunon Maglev 4020 24V mcu cooling fans (x3)
    * Sunon Maglev 4020 12V raspi cooling fan
    * Sunon Maglev 4020 24V stepper motor cooling fans (x2)
    * GDSTIME 5015 24V bed fans (x2)
    * GDSTIME 6025 24V brushless exhaust fans (x2)
    * GDSTIME 7530 24V dual ball bearing aux cooling fans (x2)
    * 3950 Thermistors for chamber (top / bottom)
    * 3950 Thermistors for steppers (x2)
    * 3950 M3 Screw-in Thermistor for bed edge
* PSUs
    * Sompom 24V (15A)
    * Sompom 48V (7.5A)
    * KIS3R33S 5V Buck Converter (15W)
* Misc
    * Mellow Fly 5" LCD
    * Piezo Buzzer
    * DWS 136deg 1080p USB camera
    * LED Strips (24V White ambient & Neopixel accents/indicators)
    * Carbon + HEPA exhaust filters
