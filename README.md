# home_assistant_car
Using Python to connect a Raspberry pi to an electric car and displaying the car stats in Home Assistant

!Current version of the code probably only supports Renault EV's!

Hat tip to https://github.com/fesch/CanZE

Sample Home Assistant view of battery, and energy consumption from last four commutes (partly in danish)
![hass](https://user-images.githubusercontent.com/2146064/140410287-934e83ef-4c88-42ff-8b41-db64af84acbb.jpg)

State: fairly experimental. Stable code, but requires some effort to install

The Python code requires a Bluetooth connected serial connection to the car. I am using a USB dongle, and a 5 meter cable, as the Raspberry is out of car range. The code works well, and reconnects fully automated, when the car leaves and returns. You need to fit your car with a Bluetooth OBD2/OBDII dongle, same type as is described here: https://canze.fisch.lu/hardware/ 

On the Home Assistant side you need to have MQTT installed to receive data, and you need to add this to configuration.yaml to receive the data:

```
  - platform: mqtt
    name: "SOC"
    state_topic: "home-assistant/SOC"
    unit_of_measurement: "%"
  - platform: mqtt
    name: "Car"
    state_topic: "home-assistant/car"
  - platform: mqtt
    name: "ODO"
    state_topic: "home-assistant/ODO"
    unit_of_measurement: "km"
  - platform: mqtt
    name: "kWh"
    state_topic: "home-assistant/kWh"
    unit_of_measurement: "kWh"
  - platform: mqtt
    name: "Last trip km"
    state_topic: "home-assistant/lastkm"
    unit_of_measurement: "km"
  - platform: mqtt
    name: "Last trip kWh"
    state_topic: "home-assistant/lastkWh"
    unit_of_measurement: "kWh"
  - platform: mqtt
    name: "SOH"
    state_topic: "home-assistant/SOH"
    unit_of_measurement: "%"
  - platform: mqtt
    name: "Commute km"
    state_topic: "home-assistant/commutekm"
    unit_of_measurement: "km"
  - platform: mqtt
    name: "Commute kWh"
    state_topic: "home-assistant/commutekWh"
    unit_of_measurement: "kWh"

```


