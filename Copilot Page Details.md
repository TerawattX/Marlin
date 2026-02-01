# 3D Printing (FDM)

3D printing troubleshooting and testing for fused deposition modeling (FDM).

## Printer

* Custom Creality Ender 3

### Upgrades

* SKR Mini E3 V1.2 main board

* Micro Swiss all metal hot end

* Direct drive conversion (no bowden tube)

* Upgraded part cooling fan

  * Hero Me Gen 7

* 3 point bed leveling plate

* Insulated bed

* Filament run-out detection

* BL Touch Z-probe

### Firmware

* Marlin firmware

  * Official Repo: <https://github.com/MarlinFirmware/Marlin>

  * My Fork: <https://github.com/TerawattX/Marlin>

* Latest build based on v2.1.2.1

* Board uses **STM32F103RC_btt_USB**

  * FIL_RULOUT_PIN corrected to PC12

#### Configuration.h

For specifics, view the uploaded [configuration.txt](https://configuration.txt) file.

* Motherboard: BOARD_BTT_SKR_MINI_E3_V1_2
* Serial Port
  * Port: 0

  * Baudrate: 115200
* Drivers (X, Y, Z, & E0): TMC2209
* Bed Temp Sensor: enabled
  * Bed Max temp: 125

  * PID values:

    * Kp=50.71

    * Ki=9.88

    * Kd=173.43
* Hotend PID:
  * Kp=23.5

  * Ki=3.11

  * Kd=48.81
* Misc Features
  * PID Edit Menu: enabled

  * PID Autotune menu: enabled
* Extruder:
  * Extrude max length: 600
* Default Axis Steps per Unit: 80, 80, 400, 138.81
* Default Max Feedrate: 500, 500, 5, 25
* Default Max Acceleration: 3000, 3000, 100, 5000
* Default
  * Acceleration: 200

  * Retract Acceleration: 500

  * Travel Acceleration: 500
* Bed Size:
  * X_BED_SIZE: 235
  * Y_BED_SIZE: 235
  * Z_MAX_POS: 250
* PID Settings:
  * Hot End:
* Extrude Max Length: 600
* Classic Jerk: Disabled
  * Junction Deviation MM: 0.01
* S Curve Acceleration enabled
* BL Touch enabled
  * Nozzle to Probe Offset: -53.49, -15.69, -3.70

  * Probing Margin: 2.5

  * Z Probe Low Point: -5

  * Delay Before Probing: 200ms

  * Preheat before probing: enabled
* Invert Directions:
  * INVERT_X_DIR: true
  * INVERT_E0_DIR: true
* Position Limits:
  * X_MIN_POS: -5
  * Y_MIN_POS: -10
* Filament Runout Sensor
  * Enabled

  * Distance: 10mm

  * Filament Motion Sensor": enabled
* Auto Bed Leveling UBL enabled
* EEPROM Settings enabled
* Preheat 1 Temp Hotend: 200
* Preheat 1 Temp Bed: 50
* Nozzle Park Feature enabled
* SD Support enabled
* Individual Axis Homing Menu enabled
* EXPERIMENTAL_SCURVE enabled

#### Configuration_adv.h

For specifics, view the uploaded configuration_adv.txt file.

* Enabled Settings:

  * No fan slowing in PID Tuning

  * Quick home

  * Adaptive Step Smoothing

  * Probe Offset Wizard

  * LCD Info Menu

  * Preheat Shortcut Menu

  * Status Message Scrolling

  * Set Progress Manually

  * Set Progress Percent

  * SD Card

    * Ignore at Startup

    * ReadOnly

    * SD Sort Uses Ram

    * SD Sort Cache Names

    * Connection onboard

  * Babystepping

    * Double-click For Z Babystepping

    * Babystep display total

  * Allow Low E-Jerk

  * Arc Support

  * Emergency Parser

  * CHOPPER_TIMING CHOPPER_DEFAULT_24V

  * Square Wave Steppint

  * Host Action Commands

* Z Stepper align iterations: 3

* Linear Advance:

  * LIN_ADVANCE enabled
  * ADVANCE_K: 0.05
  * Experimental S-Curve acceleration: Enabled

* Mesh

  * Min X: 0

  * Min Y: 5

  * Max X: X_BED_SIZE - (10)

  * Max Y: Y_BED_SIZE - (0)

* Buffer Size: 32

* TX Buffer Size: 4

* Advanced Pause Feature

  * Filament Change Unload Length: 5

  * Filament Load Unload GCodes: enabled

* Stepper Currents

  * X: 580

  * Y: 580

  * Z: 580

  * E0: 650

### EEPROM Settings

Some firmware defaults overridden in local settings:

## Printer Management/Control

Prints managed through OctoPrint running on a Raspberry Pi 3b.

* Version 1.11.6

* Official Documentation: <https://docs.octoprint.org/>

### Plugins

* AstroPrint

* Bed Visualizer

* Firmware Updater

* HeaterTimeout

* Marlin EEPROM Editor

* OctoPod Plugin

* OctoPrint-Dashboard

* Preheat Button

* PrintJobHistory

* PrintTimeGenius Plugin

* Themeify

* Z Probe Offset

## Slicer

UltiMaker Cura

* Version 5.11.0

### Printer Settings

* X: 235.0 mm

* Y: 235.0 mm

* Z: 250.0 mm

* Build plate shape: Rectangular

* Origin at center: false

* Headed Bed: true

* Headed build volume: false

* G-Code flavor: Marlin

### Printhead Settings

* X min: -26 mm

* Y min: -34 mm

* X max: 32

* Y max: 34

* Gantry Height: 25mm

* Number of Extruders: 1

* Apply Extruder offsets to GCode: true

* Start GCode must be first: false

Nozzle Settings

* Nozzle Size: 0.4mm

* Compatible material diameter: 1.75 mm

* Nozzle offset X: 0.0 mm

* Nozzle offset Y: 0.0 mm

* Cooling Fan Number: 0

* Extruder Change duration: 0.0 s

* Extruder Start G-code duration: 0.0 s

* Extruder End G-Code duration: 0.0s

### Start G-Code

```
; Ender 3 Custom Start G-code G92 E0 ; Reset Extruder
; Home M117 Homing axes G28 ; Home all axes
; Probe Bed using UBL G29 L0 G29 A
; Prime extruder G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed G1 X0.1 Y20 Z0.3 F5000.0 ; Move to start position G1 X0.1 Y200.0 Z0.3 F1500.0 E15 ; Draw the first line G1 X0.4 Y200.0 Z0.3 F5000.0 ; Move to side a little G1 X0.4 Y20 Z0.3 F1500.0 E30 ; Draw the second line G92 E0 ; Reset Extruder G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed G1 X5 Y20 Z0.3 F5000.0 ; Move over to prevent blob squish
```

### End G-Code

```
G91 ;Relative positioning G1 E-2 F2700 ;Retract a bit G1 E-2 Z0.2 F2400 ;Retract and raise Z G1 X5 Y5 F3000 ;Wipe out G1 Z10 ;Raise Z more G90 ;Absolute positioning
G1 X0 Y{machine_depth} ;Present print M106 S0 ;Turn-off fan M104 S0 ;Turn-off hotend M140 S0 ;Turn-off bed
M84 X Y E ;Disable all steppers but Z

```


### Profiles

#### Extra Fine

#### Fine

#### Normal

#### Draft

* Quality (mm)

  * Layer Height: 0.2
  * Initial Layer Height: 0.3
  * Line Width: 0.4
    * Wall Line Width: 0.4
      * Outer Wall Line Width: 0.4
      * Inner Wall Line Width: 0.4
    * Top/Bottom Line Width: 0.4
    * Infill Line Width: 0.4
    * Skirt/Brim Line Width: 0.4
  * Initial Layer Line Width (%): 100.0

* Walls (mm)

  * Wall Thickness: 0.8
    * Wall Line Count: 2
  * Wall Transition Length: 0.4
  * Wall Distribution Count: 1
  * Wall Transitioning Threshold Angle (°): 10.0
  * Wall Transitioning Filter Margin (mm): 0.1
  * Outer Wall Wipe Distance (mm): 0.2
  * Outer Wall Inset (mm): 0.0
  * Optimize Wall Printing Order: true
  * Wall Ordering: Inside to Outside
  * Alternate Extra Wall: false
  * Minimum Wall Line Width (mm): 0.34
    * Minimum Even Wall Line Width (mm): 0.34
    * Minimum Odd Wall Line Width (mm): 0.34
  * Print Thin Walls: true
  * Minimum Feature Size (mm): 0.1
  * Minimum Thin Wall Line Width (mm): 0.34
  * Horizontal Expansion (mm): 0.0
  * Initial Layer Horizontal Expansion (mm): 0.0
  * Hole Horizontal Expansion (mm): 0.0
  * Z Seam Alignment: Sharpest Corner
  * Seam Corner Preference: Hide Seam

* Top/Bottom (mm)

  * Top Surface Skin Layers: 0
  * Top/Bottom Thickness: 0.8
    * Top Thickness: 0.8
      * Top Layers: 7
    * Bottom Thickness: 0.8
      * Bottom Layers: 7
      * Initial Bottom Layers: 7
  * Top/Bottom Pattern: Lines
  * Bottom Pattern Initial Layer: Lines
  * Monotonic Top/Bottom Order: unchecked
  * Top/Bottom Line Directions: []
  * No Skin in Z Gaps: unchecked
  * Extra Skin Wall Count: 1
  * Enable Ironing: unchecked
  * Skin Overlap Percentage (%): 5.0
    * Skin Overlap (mm): 0.02
  * Skin Removal Width (mm): 0.0
    * Top Skin Removal Width (mm): 0.8
    * Bottom Skin Removal Width (mm): 0.8
  * Skin Expand Distance (mm): 0.8
    * Top Skin Expand Distance (mm): 0.8
    * Bottom Skin Expand Distance (mm): 0.8
  * Maximum Skin Angle for Expansion (°): 90.0
    * Minimum Skin Width for Expansion (mm): 0.0

* Infill

  * Infill Density (%): 15.0
    * Infill Line Distance (mm): 5.3333
  * Infill Pattern: Grid
  * Connect Infill Lines: checked
  * Infill Line Directions: []
  * Infill X Offset (mm): 0.0
  * Infill Y Offset (mm): 0.0
  * Randomize Infill Start: unchecked
  * Infill Line Multiplier: 1
  * Extra Infill Wall Count: 0
  * Infill Overlap Percentage (%): 10.0
    * Infill Overlap (mm): 0.04
  * Infill Wipe Distance (mm): 0.1
  * Infill Layer Thickness (mm): 0.12
  * Gradual Infill Steps: 0
  * Infill Before Walls: checked
  * Minimum Infill Area (mm²): 0.0
  * Infill Support: unchecked
  * Skin Edge Support Thickness (mm): 0.0
    * Skin Edge Support Layers: 0

* Material (°C / %)

  * Printing Temperature: 205.0
  * Printing Temperature Initial Layer: 220.0
  * Initial Printing Temperature: 195.0
  * Final Printing Temperature: 190.0
  * Build Plate Temperature: 60.0
  * Build Plate Temperature Initial Layer: 60.0
  * Scaling Factor Shrinkage Compensation (%): 100.0
    * Horizontal Scaling Factor Shrinkage Compensation (%): 100.0
    * Vertical Scaling Factor Shrinkage Compensation (%): 100.0
  * Flow (%): 85.11
    * Wall Flow (%): 85.11
      * Outer Wall Flow (%): 85.11
      * Inner Wall(s) Flow (%): 85.11
    * Top/Bottom Flow (%): 85.11
    * Infill Flow (%): 85.11
    * Skirt/Brim Flow (%): 85.11
    * Support Flow (%): 85.11
    * Prime Tower Flow (%): 85.11
  * Initial Layer Flow (%): 90.0
  * Initial Layer Inner Wall Flow (%): 90.0
  * Initial Layer Outer Wall Flow (%): 90.0
  * Initial Layer Bottom Flow (%): 90.0
  * Enable Linear Advance: unchecked

* Speed (mm/s)

  * Print Speed: 60.0
    * Infill Speed: 60.0
    * Wall Speed: 30.0
      * Outer Wall Speed: 30.0
      * Inner Wall Speed: 60.0
    * Top/Bottom Speed: 30.0
    * Support Speed: 60.0 (linked)
      * Support Infill Speed: 60.0 (linked)
  * Travel Speed: 120.0
  * Initial Layer Speed: 20.0
    * Initial Layer Print Speed: 20.0
    * Initial Layer Travel Speed: 40.0
  * Skirt/Brim Speed: 20.0
  * Z Hop Speed: 10.0
  * Number of Slower Layers: 2 (linked)
  * Flow Equalization Ratio (%): 100.0
  * Enable Acceleration Control: unchecked
  * Enable Jerk Control: unchecked

* Travel

  * Enable Retraction: checked
  * Retract at Layer Change: checked
  * Retraction Distance (mm): 0.1
  * Retraction Speed (mm/s): 20.0
    * Retraction Retract Speed (mm/s): 20.0
    * Retraction Prime Speed (mm/s): 20.0
  * Retraction Extra Prime Amount (mm³): 0.1
  * Retraction Minimum Travel (mm): 0.8
  * Maximum Retraction Count: 90
  * Minimum Extrusion Distance Window (mm): 0.1
  * Combing Mode: All
  * Max Comb Distance With No Retract (mm): 0.0
  * Retract Before Outer Wall: unchecked
  * Avoid Printed Parts When Traveling: unchecked
  * Layer Start X (mm): 0.0
  * Layer Start Y (mm): 20.0
  * Z Hop When Retracted: checked
  * Z Hop Height (mm): 1.0

* Cooling

  * Enable Print Cooling: checked
  * Fan Speed (%): 100.0
    * Regular Fan Speed (%): 100.0
    * Maximum Fan Speed (%): 100.0
  * Regular/Maximum Fan Speed Threshold (s): 10.0
  * Initial Fan Speed (%): 0.0
  * Regular Fan Speed at Height (mm): 0.3
    * Regular Fan Speed at Layer: 2
  * Minimum Layer Time (s): 5.0
  * Minimum Speed (mm/s): 10.0
  * Lift Head: unchecked

* Support

  * Generate Support: checked
  * Support Structure: Normal
  * Support Placement: Touching Buildplate
  * Support Overhang Angle (°): 50.0
  * Support Pattern: Zig Zag
  * Support Wall Line Count: 0
  * Connect Support ZigZags: checked
  * Support Density (%): 5.0
    * Support Line Distance (mm): 8.0
    * Initial Layer Support Line Distance (mm): 8.0
  * Support Infill Line Directions: []
  * Enable Support Brim: checked
    * Support Brim Width (mm): 1.2
  * Support Brim Line Count: 3
  * Support Z Distance (mm): 0.1
    * Support Top Distance (mm): 0.1
  * Support X/Y Distance (mm): 0.7
  * Support Distance Priority: Z overrides X/Y
  * Minimum Support X/Y Distance (mm): 0.2
  * Support Stair Step Height (mm): 0.3
  * Support Stair Step Maximum Width (mm): 5.0
  * Support Stair Step Minimum Slope Angle (°): 10.0
  * Support Join Distance (mm): 2.0
  * Support Horizontal Expansion (mm): 0.8
  * Support Infill Layer Thickness (mm): 0.12
  * Gradual Support Infill Steps: 0
  * Minimum Support Area (mm²): 0
  * Enable Support Interface: unchecked
  * Fan Speed Override: unchecked
  * Use Towers: checked
  * Tower Diameter (mm): 3.0
  * Maximum Tower-Supported Diameter (mm): 3.0
  * Tower Roof Angle (°): 65

* Build Plate Adhesion

  * Adhesion type: Brim
  * Skirt/Brim Minimum Length (mm): 250.0
  * Brim Width (mm): 8.0
    * Brim Line Count: 20
  * Brim Distance (mm): 0.0
  * Brim Replaces Support: checked

* Mesh Fixes

  * Union Overlapping Volumes: checked
  * Remove All Holes: unchecked
  * Extensive Stitching: unchecked
  * Keep Disconnected Faces: unchecked
  * Merged Meshes Overlap (mm): 0.15
  * Remove Mesh Intersection: unchecked
  * Maximum Resolution (mm): 0.5
  * Maximum Travel Resolution (mm): 0.8
  * Maximum Deviation (mm): 0.025
  * Maximum Extrusion Area Deviation (µm²): 50000.0

* Special Modes

  * Print Sequence: All at Once
  * Mold: unchecked
  * Surface Mode: Normal
  * Spiralize Outer Contour: unchecked
  * Relative Extrusion: unchecked

* Experimental

  * Slicing Tolerance: Middle
  * Infill Travel Optimization: checked
  * Minimum Polygon Circumference (mm): 1.0
  * Break Up Support In Chunks: checked
    * Support Chunk Size (mm): 20.0
  * Support Chunk Line Count: 2
  * Enable Draft Shield: unchecked
  * Make Overhang Printable: unchecked
  * Enable Coasting: unchecked
  * Enable Conical Support: unchecked
  * Fuzzy Skin: unchecked
  * Flow Rate Compensation Max Extrusion Offset (mm): 0.0
  * Flow Rate Compensation Factor (%): 100.0
  * Use Adaptive Layers: unchecked
  * Overhanging Wall Angle (°): 90.0
  * Enable Bridge Settings: unchecked
  * Wipe Nozzle Between Layers: unchecked
  * Small Hole Max Size (mm): 20.0
  * Alternate Wall Directions: checked

#### Extra Fast

#### Coarse

#### Extra Coarse

### Filament Specific Settings

Inland PLA

* Information
  * Density (g/cm3): 1.24
  * Diameter (mm): 1.75
* Print Settings
  * Default Printing Temperature (°C): 215.0
  * Default Build Plate Temperature (°C): 60.0
  * Standby Temperature (°C): 175.0
  * Retraction Distance (mm): 0.1
  * Retraction Speed (mm/s): 25.0
  * Fan Speed (%): 100

Inland PLA+

* Information
  * Density (g/cm3): 1.24
  * Diameter (mm): 1.75
* Print Settings
  * Default Printing Temperature (°C): 205.0
  * Default Build Plate Temperature (°C): 60.0
  * Standby Temperature (°C): 175.0
  * Retraction Distance (mm): 3.0
  * Retraction Speed (mm/s): 20.0
  * Fan Speed (%): 100