# # BUILD A RASPBERRY PI CAR COMPUTER

# 07  **Update GCC**

Recent Raspberry Pi kernels are compiled with GCC 4.8. Raspbian only comes with 4.6 so you will have to install 4.8 to continue with the following steps. Do this by entering:

```
`sudo apt-get install -- gcc-4.8 g++-4.8 ncurses-dev`
```

Then you have to set GCC 4.8 as the default:

```
`sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.6 20`

`sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 50`

`sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.6 20`

`sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-4.8 50`
```

# 08  **Pick the module to compile**

Rpi-source puts the kernel source in a folder called ‘linux’. To choose the USB Touchscreen Driver, enter the following:

```
`cd linux`
`make menuconfig`

Device Drivers → Input device
support → Generic input layer
(needed for keyboard, mouse, .) → Touchscreens (press space to include) → USB Touchscreen
Driver (press M to make module)
```

Once you’ve done that, you then need to make sure you save your changes as ‘.config’ and run scripts/diffconfig to see the differences.

# 09  **Compile and install the module**

Now you need to compile and install the module. Do so by entering:

```
`make prepare`

`make SUBDIRS=drivers/input/ touchscreen modules`

`sudo make SUBDIRS=drivers/input/ touchscreen modules_install`

`sudo depmod`
```

If you unplug and reconnect the touchscreen, it should work fine but it will probably need calibrating.

# ## Full code listing

```
```python
#!/usr/bin/env python2
import os, sys, requests, pygame
from gps import *
from pygame.locals import *

class WeatherClient:
    apikey = "7232af6857090f33b9d1c7a74721"

    @staticmethod
    def latlon():
        gpsd = gps(mode=WATCH_ENABLE)
        # Needs better error handling
        try:
            while True:
                if report := gpsd.next():
                    if report['class'] != 'TPV':
                        gpsd.close()
                        return report['lat'], report['lon']
                
        except:
            return None, None

    @staticmethod
    def usefuldata():
        # returns a string of useful weather data from a LOT of json
        d = json.loads(requests.get(f"http://api.worldweatheronline.com/free/v2/weather.ashx?q={o[0]}[o[0]current_condition}]&key={api key}").text)
        out = f"\n\n- Now - Temp: {o[1]}, Feels Like: {o[2]}C, Description: {o[3]}\n\n"

        hourly = json.loads(requests.get(f"http://api.worldweatheronline.com/free/v2/weather.ashx?q={o[0]}[o[0]hourly})&key={api key}").text)
        hour_count = 1
        for h in hourly:
            out += f"- (+{h}hr) - Temp: {h[1]}C, Feels Like: {h[2]}C, Chance of Rain:"
                   f" {h[3]}%, Description: {h[4]}\n"
        hour_count += 1

        # Rstrip removes trailing newline
        return out.rstrip()

    @staticmethod
    def update():
        errstr = "Error getting weather data"

        lat, lon = WeatherClient.latlon()
        if lat == None or lon == None:
            return errstr

        api_req = f"http://api.worldweatheronline.com/free/v2/weather.ashx"
                  f"?q={o[0]%2C(2)[0]&format=json&key={2}")
        
        r = None
        ...
```
```