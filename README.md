# LuxPythoncard
LuxPythoncard is a custom card for Home Assistant for the LuxPowerTek Inverter. It is dependant on LuxPython.




# How to Install

This isn't fully working yet, if you want access to the luxpower integration, you can email me at my username at hotmail dot com



Copy the "luxpower" integration to your Home Assistant instance into the "custom_components" folder

./custom_components/luxpower/ to your HA data directory (where your configuration.yaml lives)

If you are new to HA you will likely have to create this folder but if you use HACS it should already be created.

Next REBOOT, it's mandatory otherwise the next bit will not work.

Open up Settings>Devices and Services> Add Integration and search for "LuxPower Inverter"


If you have an ACS Inverter you should modify the sensors.yaml with the following:
```
## Custom LUX Sensors for ACS Systems. Intended to replace the two existing sensor code. However, there's a new name to prevent conflict. 
    lux_new_home_consumption:
      friendly_name: "Lux - Home Consumption (Daily)"
      unit_of_measurement: 'kWh'
      value_template: >
        {{ '%0.1f' | format(states('sensor.lux_power_from_grid_daily') | float(0) + 
                            states('sensor.lux_power_from_inverter_daily') | float(0) +
                            states('sensor.lux_daily_solar') | float(0) - 
                            states('sensor.lux_power_to_inverter_daily') | float(0) - 
                            states('sensor.lux_power_to_grid_daily') | float(0)) }}
    lux_new_home_consumption_live:
      friendly_name: "Lux - Home Consumption (Live)"
      unit_of_measurement: 'W'
      value_template: >
        {{ '%0.1f' | format(states('sensor.lux_power_from_grid_live') | float(0) + 
                            states('sensor.lux_power_from_inverter_live') | float(0) +
                            states('sensor.lux_current_solar_output') | float(0) - 
                            states('sensor.lux_power_to_inverter_live') | float(0) - 
                            states('sensor.lux_power_to_grid_live') | float(0)) }}
                            
## ##### END OF Custom Lux Sensors   ######
```
# Thanks!

