# Nevermore Wartungsintervall  
  
### <u>Configs einfügen</u>   
  
1. printtime.cfg -- *duration config*
2. filter.cfg -- *filter config*
3. user_variable.cfg -- *User variablen*
4. display.cfg -- *Diplay statistic menue*
5. boot.cfg  -- *Initialisiert User_variablen*  
  
### <u>In End_Print einfügen</u>  
  
```
    _ADD_PRINT_TIME
    _SD_PRINT_STATS R='done'
    _SD_PRINTER_STATS
```
  
### <u>In Cancle_Print einfügen</u>
  
```
    _ADD_PRINT_TIME
    _SD_PRINT_STATS R='done'
    _SD_PRINTER_STATS
```
  
### <u>In Start_Print einfügen</u>
```
[gcode_macro START_PRINT]
variable_var: {'filter'      : True}
gcode:  
{% set FILAMENT_TYPE = params.FILAMENT|default(PLA)|string %}
{% if FILAMENT_TYPE == "ABS" or FILAMENT_TYPE == "ASA" %}
        _FILTER_ON
        {% set var = {'filter'      : True} %}
    {% else %}
        SET_FAN_SPEED FAN=filter SPEED=0
        {% set var = {'filter'      : False} %}
    {% endif %}
```
  
### <u>In Printer cfg einfügen</u>

[include ./printtime.cfg]
[include ./filter.cfg]
[include ./user_variable.cfg]
[include ./display.cfg]
[include ./boot.cfg]

[save_variables]
filename: /home/pi/klipper_config/.variables.stb
  
---
    

### <u>Filter konfigurieren</u>
  
Trage in der user_variable.cfg unter der Sektion "Peripheral" deine gewünschten Werte wie speed und Wartungsintervall ein.
  
---

### <u>SuperSlicer</u>
  
Ausgabeoptionen: 
  
`[input_filename_base]-[print_settings_id]-[filament_settings_id].gcode`
