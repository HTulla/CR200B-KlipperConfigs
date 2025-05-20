# Cura slicer printer configurations

## Printer settings
![image](https://github.com/user-attachments/assets/52ab7a82-fa2c-469b-8e71-e9ac8cf11db7)

### Start G code
``
; CR200B
G92 E0 ; Reset Extruder
G28 ; Home all axes
G1 Z5.0 F3000 ; Move Z Axis up a bit during heating to not damage bed
M104 S{material_standby_temperature} ; Start heating up the nozzle most of the way
M190 S{material_bed_temperature_layer_0} ; Start heating the bed, wait until target temperature reached
M109 S{material_print_temperature_layer_0} ; Finish heating the nozzle
BED_MESH_CALIBRATE ADAPTIVE=1;
BED_MESH_PROFILE SAVE=cura_adaptive;
BED_MESH_PROFILE LOAD=cura_adaptive;
G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
G1 X0.1 Y20 Z0.3 F5000.0 ; Move to start position
G1 X0.1 Y200.0 Z0.3 F1500.0 E15 ; Draw the first line
G1 X0.4 Y200.0 Z0.3 F5000.0 ; Move to side a little
G1 X0.4 Y20 Z0.3 F1500.0 E30 ; Draw the second line
G92 E0 ; Reset Extruder
G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
G1 X5 Y20 Z0.3 F5000.0 ; Move over to prevent blob squish
``

### End G-code
```
G91 ;Relative positioning
G1 E-2 F2700 ;Retract a bit
G1 E-2 Z0.2 F2400 ;Retract and raise Z
G1 X5 Y5 F3000 ;Wipe out
G1 Z50 ;Raise Z more
G90 ;Absolute positioning

G1 X0 Y{machine_depth} ;Present print
M106 S0 ;Turn-off fan
M104 S0 ;Turn-off hotend
M140 S0 ;Turn-off bed

M84 X Y E ;Disable all steppers but Z

END_PRINT ; Run Klipper end macro
``

## Extruder 1 settings
![image](https://github.com/user-attachments/assets/5aa594a1-ab0d-4849-9c81-8083525b8eef)



