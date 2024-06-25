# OrcaSlicer Filament and Bed-Type Z_Offset Macros
These are two Macros wich will make you able to change Z-Offsets for different Bed and Filament types.


### Whats really important, is that the config is designd for both to work together. If you just want to use one of them for example because you don´t use multiple beds change the macro accordingly. If you don´t do that the SET_GCODE_OFFSET Z_ADJUST=XY will multiply causing issues up to a damaged bed!

First you have to add the following in your Orca Start GCODE under Printer Settings:
```
FILAMENT_TYPE="{filament_type[0]}" CURR_BED_TYPE="{curr_bed_type}"
```
Then you will have to upload the z_offset_macro.cfg file and inculde it anywhere in your printer.cfg with:

```
#####################################################################
###   Z_OFFSET_MACRO
#####################################################################

[include z_offset_macro.cfg]
```

Then add the following at the beginning of your PRINT_START macro:

```
  {% set CURR_BED_TYPE = params.CURR_BED_TYPE|lower|replace(" ", "_") %}  #|lower|replace(" ", "_") is there because otherwise Klipper wont understand the string
  {% set FILAMENT_TYPE = params.FILAMENT_TYPE %}                          
```

If you want to use the macros together like I do activate in the Bed Macro
```
SET_GCODE_OFFSET Z=0.000
```

And use the other one for the Filament:
```
SET_GCODE_OFFSET Z_ADJUST=0.000
```

If you only use one of them don´t use 
```
SET_GCODE_OFFSET Z_ADJUST=0.000
```
Because if you directly start a print again it will multiply the adjustments!

At the end of the Print do not do
```
SAVE_CONFIG
```
Because that would save the Z-Offset to. If you have changed something that you want to save, bring your Z_OFFSET back to 0. You could use this command in the console to do that!
```
SET_GCODE_OFFSET Z=0.000
```
# Disclaimer

### You use it at your onw risk! I'm not responsible for any damage that might result. Although, this extension works rock solid for me. Always be careful and double check everything when configuring or working with your printer. And as always, never leave unattended while printing!

### Huge thanks to multiple Discord users from the Klipper Discord helping me getting this working.
