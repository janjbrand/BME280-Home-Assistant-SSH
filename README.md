# BME280-Home-Assistant-SSH

A simple way to add temperature and humidity of a BME280 sensor connected to a Raspberry Pi to Home Assistant via a python script and SSH, if Home Assistant is running on another device than the one the BME280 sensor is connected to.

Requirements:
- BME280 sensor
- Raspberry Pi
- Home Assistant, running on another device
- Generic SSH plugin for Home Assistant

Installation
Add both .py-files to /home/pi

Home Assistant configuration.yaml:
'
  - platform: ssh
    host: IP_of_Raspberry_Pi
    unit_of_measurement: "°C"
    name: Rpi3b Temp        
    username: your_username
    password: your_ssh_password
    command: python bme280.py
    value_template: >-
      {%- set line = value.split("\r\n") -%}
      {{ (line[1]) }}

- platform: ssh
    host: IP_of_Raspberry_Pi
    unit_of_measurement: "%"
    name: Rpi3b Hum        
    username: your_username
    password: your_ssh_password 
    command: python bme280_hum.py
    value_template: >-
      {%- set line = value.split("\r\n") -%}
      {{ (line[1]) }}
'
