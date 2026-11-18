# Hardware Details

This document outlines the hardware improvements made to the base Ender 3 printer by TerawattX, along with notes about the printer like known issues or other information.

## Marlin Config Values

These values were altered to fit the printer in the marlin configuration files.

### `Configuration.h`

| Area | Setting | Value | Printer-specific detail |
| --- | --- | --- | --- |
| Controller | `MOTHERBOARD` | `BOARD_BTT_SKR_MINI_E3_V1_2` | BigTreeTech SKR Mini E3 v1.2 |
| Driver | `X_DRIVER_TYPE` | `TMC2209` | X-axis driver |
| Driver | `Y_DRIVER_TYPE` | `TMC2209` | Y-axis driver |
| Driver | `Z_DRIVER_TYPE` | `TMC2209` | Z-axis driver |
| Driver | `E0_DRIVER_TYPE` | `TMC2209` | Extruder driver |
| Host connection | `SERIAL_PORT` | `2` | Primary serial port |
| Host connection | `BAUDRATE` | `115200` | Serial baud rate |
| Machine name | `CUSTOM_MACHINE_NAME` | `Ender-3 (SKR Mini E3 v1.2)` | Name shown by the firmware |
| Bed dimensions | `X_BED_SIZE` | `235 mm` | Configured X bed size |
| Bed dimensions | `Y_BED_SIZE` | `235 mm` | Configured Y bed size |
| X travel limit | `X_MIN_POS` | `-5 mm` | Minimum X coordinate after homing |
| Y travel limit | `Y_MIN_POS` | `-10 mm` | Minimum Y coordinate after homing |
| Z travel limit | `Z_MAX_POS` | `250 mm` | Maximum Z coordinate after homing |
| Motion calibration | `DEFAULT_AXIS_STEPS_PER_UNIT` | `{80, 80, 400, 138.81}` | X, Y, Z, and E steps/mm; E is calibrated for the direct-drive extruder |
| Motion tuning | `DEFAULT_MAX_ACCELERATION` | `{3000, 3000, 100, 5000}` | X, Y, Z, and E maximum acceleration in mm/s^2 |
| Motion tuning | `S_CURVE_ACCELERATION` | Enabled | Enables S-curve acceleration |
| Motor direction | `INVERT_X_DIR` | `true` | X-axis direction |
| Motor direction | `INVERT_Y_DIR` | `true` | Y-axis direction |
| Motor direction | `INVERT_Z_DIR` | `false` | Z-axis direction |
| Motor direction | `INVERT_E0_DIR` | `true` | Extruder direction |
| Probe | `BLTOUCH` | Enabled | Configures the BL-Touch v1 |
| Probe | `Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN` | Enabled | Uses the Z-min endstop input for the probe |
| Probe offset | `NOZZLE_TO_PROBE_OFFSET` | `{-53.49, -15.69, -3.70} mm` | X, Y, and Z offsets from nozzle to probe |
| Z homing | `Z_SAFE_HOMING` | Enabled at bed center | Homes Z with the probe positioned over the bed |
| Bed leveling | `AUTO_BED_LEVELING_UBL` | Enabled | Unified Bed Leveling |
| Bed leveling | `GRID_MAX_POINTS_X` | `10` | Number of UBL mesh points along X |
| Bed leveling | `GRID_MAX_POINTS_Y` | `GRID_MAX_POINTS_X` (`10`) | Number of UBL mesh points along Y |
| Bed leveling | `MESH_INSET` | `10 mm` | Inset from the bed edges for UBL mesh bounds |
| Bed leveling | `G26_MESH_VALIDATION` | Enabled | Enables the G26 mesh validation pattern |
| Probing | `PROBING_MARGIN` | `MESH_INSET` (`10 mm`) | Matches the mesh inset to keep probing away from the bed edges |
| Temperature sensor | `TEMP_SENSOR_0` | `1` | 100k EPCOS hotend thermistor |
| Temperature sensor | `TEMP_SENSOR_BED` | `1` | 100k EPCOS bed thermistor |
| Temperature limit | `HEATER_0_MAXTEMP` | `275 C` | Maximum configured hotend temperature |
| Temperature limit | `BED_MAXTEMP` | `125 C` | Maximum configured bed temperature |
| Hotend PID | `DEFAULT_KP` | `23.5` | Proportional term |
| Hotend PID | `DEFAULT_KI` | `3.11` | Integral term |
| Hotend PID | `DEFAULT_KD` | `48.81` | Derivative term |
| Filament runout | `FILAMENT_RUNOUT_SENSOR` | Enabled | Enables filament runout sensing |
| Filament runout | `NUM_RUNOUT_SENSORS` | `1` | One runout sensor |
| Filament runout | `FILAMENT_RUNOUT_SCRIPT` | `M600` | Runs the filament-change command on runout |
| Filament runout | `FILAMENT_RUNOUT_DISTANCE_MM` | `10 mm` | Continues this filament distance before running the script; enables motion-sensor mode |
| Display | `CR10_STOCKDISPLAY` | Enabled | Retains the stock CR-10 display |
| Storage | `SDSUPPORT` | Enabled | Enables SD-card support |
| Storage | `SDCARD_READONLY` | Disabled | SD-card write access is not disabled |
| Settings storage | `EEPROM_SETTINGS` | Enabled | Saves and restores settings with `M500` / `M501` |

### `Configuration_adv.h`

| Area | Setting | Value | Printer-specific detail |
| --- | --- | --- | --- |
| Stepper current | `X_CURRENT` | `580 mA RMS` | X-axis TMC2209 run current |
| Stepper current | `Y_CURRENT` | `580 mA RMS` | Y-axis TMC2209 run current |
| Stepper current | `Z_CURRENT` | `580 mA RMS` | Z-axis TMC2209 run current |
| Stepper current | `E0_CURRENT` | `650 mA RMS` | Extruder TMC2209 run current |
| Stepper hold current | `HOLD_MULTIPLIER` | `0.5` | Holding current is half the run current |
| Driver mode | `STEALTHCHOP_XY` | Enabled for X/Y only | Z and E use the other TMC stepping mode |
| Chopper timing | `CHOPPER_TIMING` | `CHOPPER_DEFAULT_24V` | 24V timing preset selected for all axes |
| Linear Advance | `LIN_ADVANCE` | Enabled | Enables Linear Advance |
| Linear Advance | `ADVANCE_K` | `0.05` | Pressure advance value for the direct-drive extruder |
| G-code support | `ARC_SUPPORT` | Disabled | Arc commands are not used |
| Babystepping | `BABYSTEPPING` | Enabled | Enables babystepping |
| Babystepping | `BABYSTEP_ALWAYS_AVAILABLE` | Disabled | Babystepping is not enabled outside active movement |
| Filament change | `ADVANCED_PAUSE_FEATURE` | Enabled | Provides `M600` support for the runout script |
| Filament change | `FILAMENT_CHANGE_UNLOAD_LENGTH` | `5 mm` | Configured unload length |
| Filament change | `ADVANCED_PAUSE_PURGE_LENGTH` | `50 mm` | Configured post-load purge length |
| Filament change | `PAUSE_PARK_NO_STEPPER_TIMEOUT` | Enabled | Keeps XYZ steppers energized during filament change |
| Filament change | `PAUSE_PARK_NOZZLE_TIMEOUT` | `45 s` | Turns off the nozzle after this pause timeout |
| Serial buffer | `TX_BUFFER_SIZE` | `4` | Transmission buffer size |
| SD print behavior | `SD_FINISHED_STEPPERRELEASE` | `true` | Releases steppers after an SD print |
| SD print behavior | `EVENT_GCODE_SD_ABORT` | `G28XY` | Homes X/Y when an SD print is aborted |
| Firmware transfer | `BINARY_FILE_TRANSFER` | Enabled | Enables optimized binary file transfer with `M28 B1` |
| Bed leveling | `MESH_MIN_X`, `MESH_MIN_Y`, `MESH_MAX_X`, `MESH_MAX_Y` | Commented out | Uses the inset-derived mesh bounds instead of coordinate overrides |

### `Version.h`

`Version.h` is a tracked source file selected by `CUSTOM_VERSION_FILE`; it is not generated build output.

| Area | Setting | Value | Printer-specific detail |
| --- | --- | --- | --- |
| Firmware version | `SHORT_BUILD_VERSION` | `2.1.2.9` | Marlin release version string |
| Firmware version | `DETAILED_BUILD_VERSION` | `SHORT_BUILD_VERSION` | Uses the short version as the detailed version |
| Build metadata | `STRING_DISTRIBUTION_DATE` | `2026-11-18` | Distribution date reported by the firmware |
| Printer identity | `MACHINE_NAME` | `Ender-3 (SKR Mini E3 v1.2)` | Printer name supplied by `Version.h` |
| Source location | `SOURCE_CODE_URL` | `https://github.com/TerawattX/Marlin` | URL reported as the firmware source |
| Printer identity | `DEFAULT_MACHINE_UUID` | `a5520f0c-e436-4dd5-b2a2-6807c010c552` | Default printer UUID; `MACHINE_UUID` in `Configuration.h` is set to the same value |

### Configuration changes

#### 2026-11-17

- Removed the obsolete `EXPERIMENTAL_SCURVE` setting; `S_CURVE_ACCELERATION` is enabled in `Configuration.h`.
- Disabled `ARC_SUPPORT` because arc commands were not being used.
- Enabled `BINARY_FILE_TRANSFER` to support firmware transfer using `M28 B1`.
- Enabled `G26_MESH_VALIDATION` and disabled `SDCARD_READONLY`.
- Updated the PID setting names to the current Marlin spelling (`DEFAULT_KP`, `DEFAULT_KI`, and `DEFAULT_KD`); the configured PID values are unchanged.
- Updated the documented firmware version and distribution date from `Version.h`.

#### 2026-11-18

- Increased `MESH_INSET` to `10 mm` and set `PROBING_MARGIN` to `MESH_INSET`.
- Commented out the `MESH_MIN_X`, `MESH_MIN_Y`, `MESH_MAX_X`, and `MESH_MAX_Y` overrides so the inset defines the mesh bounds.
- Moved the mesh inward to avoid skipping probing column 0 (`X=0`) and to keep the probe on the bed at row 0 (`Y=0`).
- Updated the documented distribution date to `2026-11-18`.

## Hardware Upgrades

### Build Plate

Originally installed a [Creality Tempered Glass plate](https://www.amazon.com/dp/B07FSM8DK9?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_12), but retired this due to added weight.

Currently using a `Spring-Steel PEI coated build plate`.  This kit came with a magnet that you lay on the plate base and then the sheet can be removed easily.

### Hotend

[Micro Swiss All metal Hotend Kit](https://www.amazon.com/dp/B0789V2D7C?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_11)

### Z probe

I replaced the standard switch with a `BL-Touch` v1.

### Mainboard

The default mainboard has been replaced with an [SKR Mini E3 v1.2](https://www.amazon.com/dp/B07YW86YS7?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_5)

This board is one of the early ones where the chip was a `STM32F103RCT6`.  The Marlin firmware locks this to 256k of flash storage, but I confirmed that more than 256k is accessible, though some of the flash beyond 256k is faulty and using it can cause CR10 stock display timing issues (garbled screens).

### Bed Leveling

The print bed has been upgraded to use a `3 point leveling plate`.  Additionally the stock bed springs were replaced with [Adiyer 8mm OD 20mm Length Compression Mould Die Springs](https://www.amazon.com/dp/B07KF9LZ2L?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_5).

### Part cooling

The standard part cooling fan was upgraded using the [Hero Me Gen7 release 4](https://www.printables.com/model/39322-hero-me-gen7-platform-release4) and uses two 4020 cooling fans.

### Direct Drive

The printer was converted from using a Bowden tube to direct drive using a [direct drive extruder upgrade kit](https://www.amazon.com/dp/B0824ZQ3D1?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_4).

### Filament Runout Detection

A [BigTreeTech Smart Filament Detection Module](https://github.com/bigtreetech/smart-filament-detection-module) was installed to detect both runout and clogs.

### Dual Z-Axis

The Z axis was upgraded to a [Dual Z-axis upgrade Kit with Lead Screw](https://www.amazon.com/dp/B07VJG4ZCG?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_2).  From what I remember, both stepper motors connect to the same stepper driver vs having independent control - and there is no belt to keep the 2 in sync.

### Bed insulation

A [cotton + foil insulation](https://www.amazon.com/dp/B09QKRCDPG?ref_=ppx_hzsearch_conn_dt_b_fed_asin_title_1) kit was installed on the bed to help prevent heat from escaping.

### Printer Management

The printer is connected and managed via [Octoprint](https://octoprint.org/).

### Other/Minor

These upgrades don't have a major impact on printer operation or don't directly impact anything that needs to be aware of when adjusting settings or configuration.

#### Filament guide

A [Filament Roller Guide](https://www.thingiverse.com/thing:3052488) was added to help guide the filament into the bowden leading to the direct drive unit.

#### Cable Chains

A cable chain was added to the hotend (horizontal and vertical) and the print bed to help with strain relief and prevent snags.

#### Motor Grounding

Some strange behaviors were identified early on where movement on the Z axis might cause jumping on the Y axis, or other odd electrical issues.  A grounding wire was run from each stepper motor and the bed to the frame of the printer and resolved these issues.

#### Electronics Box

The main board and RaspberryPi running the Octoprint server were mounted in a [Ender 3 all in one, universal rear electronics case](https://www.thingiverse.com/thing:3688967).

## Known Issues

### Flash capacity

The maximum capacity of 256k is very limiting, preventing all desired features from being enabled.

### Print Bed Thermal Expansion

The print bed appears to experience some notable thermal expansion, specifically in the front right corner (X=235, Y=0).  The bed itself appears to bow upward after reaching thermal equilibrium enough that a cold print will not stick to the bed.

### Probe limits

Due to the X and Y offsets of the Z-Probe mount, the probe itself is unable to reach the far right (X=235).  Using a 10 point UBL mesh, the last 2 columnns are unable to be automatically probed.

Additionally the bed itself is right at the 235mm size defined in the code, and if not careful the probe will drop off the edge of the plate at the front (y=235).