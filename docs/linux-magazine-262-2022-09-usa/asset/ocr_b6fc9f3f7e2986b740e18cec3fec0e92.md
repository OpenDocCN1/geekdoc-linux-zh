named test/test1 and receive the value as a subscriber, you would use the commands:

```
$ mosquitto_pub -v mqtgv211
-h 192.168.3.7 -t test/test1 -m 10
$ mosquitto_sub -h 192.168.3.7
-t test/test1
```

For a more practical example, I’ll use MQTT to transfer the measured values of a one-wire temperature sensor of the DS18x20 type connected to a Raspberry Pi to the broker listening on another Raspberry Pi. To do this, you need to enable one-wire support up front with

```
dtoverlay=w1-gpio
```

in the /boot/config.txt file.
After connecting the sensor to the standard one-wire GPIO port, the temperature values can be queried as four-digit integers in /sys/bus/w1/devices/28-0417c1b1ff/ui slave. The value 28-0417c1b1fff is the unique ID of the sensor on the bus. The complete command sequence is:

```
$ mosquitto_pub -h 192.168.3.7
-t wohn/temp/28-0417c1b1f7ff
-m $value
$ mosquitto_sub -h localhost
-t wohn/temp/28-0417c1b1f7ff
```

To transfer the values to the Home Assistant environment, you need to enter the broker you are using in the configuration.yaml file (in this case, it is running on the same host (Listing 1, lines 1-2)). The entries in the lines that follow take care of subscribing to the appropriate topic and fielding the sensor data in Home Assistant; the last line also specifies degrees Celsius as the unit.

# ESP8266 Controller

The theoretical side is now covered, but to use a separate Raspberry Pi for each remote actuator or sensor seems a little unrealistic in practice. The ESP8266 controller will come in handy here. On the one hand, you can source low-priced and useful developer boards that use this controller; on the other hand, the chip is used in various products from the Far East, and you can take control of many of these simply by flashing them with freely available firmware.

![](bbox=[0.37, 0.09, 0.91, 0.34])

Figure 1: The Sonoff Basic WiFi smart switch with temperature sensor.

For the tests here, I used a Sonoff Basic WiFi smart switch [2] (Figure 1). This controllable relay switch has a screw connection for a 220V mains supply with switchable output.

*CAUTION: There is a danger to life if this hardware is not used correctly. In this article, I am restricting the supply voltage to the module to 3.3V.*

The firmware is Tasmota. The software lets you configure a variety of supported sensors and components on the existing GPIO ports of the controller, such as the temperature sensor I referred to earlier. Tasmota uses MQTT to transmit the data from the sensors.

```
Listing 1: configuration.yaml
01 mqtt:
02 broker: localhost
03
04 sensor:
05 - platform: mqtt
06 name: templ
07 state_topic: "/living/temp/28-0417c1b1f7ff"
08 unit_of_measurement: '°C'
```

![](bbox=[0.37, 0.63, 0.91, 0.9])

Figure 2: Wiring the Sonoff Basic to the Raspberry Pi.