# FORECAST THE WEATHER WITH YOUR RASPBERRY PI

have need of more control over your request. In these cases, the forecast.io module has a function called 'manual()'. You can use this to send a particular URL data request to the forecast.io service to pull back the exact information you are interested in.

The last option we will look at is the python-weather-api module. This module provides access to weather service providers such as Yahoo! Weather, weather.com and NOAA. This module is actually available as a package within Raspbian. You can install it with the command:

```
```bash
sudo apt-get install python-pyapi
```
```

You can also install it with pip. Once you have it installed, you can import it and request data from any of the three data service providers. The three main functions are:

+   pywapi.get_weather_from_yahoo()  
+   pywapi.get_weather_from_weather.com()  
+   pywapi.get_weather_from_nooa()

These functions essentially get all of the available information from these different servers in a single call. You can then parse the results to pull out the information you are most interested in. The results actually come back as XML data and are then parsed in the return object. You can then pull out the relevant data by using keywords, such as 'forecasts'. You should review the module documentation to see what information is available from each of the data sources.

Once you have collected the weather data that you were looking for, you need to display this information. The simplest is to just print it out. This works well if you are using a console as the interface. There are also several LCD options available if you want to make a self-contained weather reporting service.

The exact code used to handle the LCD will vary by manufacturer, but they all have very good documentation available. Now that you have weather reports being served to you, you will no longer have any excuses for being caught unawares by a storm or for showing up to work drenched by the rain.

# Full code listing

```
```python
# To talk to Weather Underground we need
# to import modules to handle URLs and
# JSON data
import urllib2
import json

# The next step is to open a URL and
# read the data
f = urllib2.urlopen('http://api.wunderground.com/api/UR_KEY/
 geolookup/conditions/q/IA/Cedar_Rapids.json')
json_string = f.read()

# Now you can parse the JSON data
# read off the information you need
parsed_json = json.loads(json_string)
location = parsed_json['location']['city']
temp_f = parsed_json['current_observation']['temp_f']

# To talk to forecast.io you need to
# import the forecastio module
import forecastio

# You need your API key and location
apikey = "YOUR_KEY"
latitude = 35.4
longitude = 46.567

# The next step is to load the forecast data
forecast = forecastio.load_forecast(apikey, latitude, longitude)

# You can print out the available hourly data
for_houly_data = forecast.hourly
for hourly_data in by_hourly_data:
    print hourly_data

# You can also get summaries
by_day = forecast.daily()
print by_day.summary

# To use the Python weather API you need to
# import the pywapi module
import pywapi

# Getting the weather from any of the
# available sources is a single call
# You will need to find and use the
# appropriate location ID
weather_com_result = pywapi.get_weather_from_weather_com('10001')
yahoo_result = pywapi.get_weather_from_yahoo('10001')
noaa_result = pywapi.get_weather_from_noaa('KJKF')

# The data is now in a key/value pair
# structure, ready to read off and used
print weather_com_result['current_conditions']['text']
print yahoo_result['condition']['text']
print noaa_result['weather']
```
```

# Weather station

You can use Python to log weather data and send it to Weather Underground; just install the required module with pip install weather. This actually contains three separate submodules that need to be imported individually. The first provides a number of conversion functions, as well as calculation functions such as weather.units.calc_wind_chill(). The second, weather.stations, provides the capabilities to talk to the weather station over a serial connection, but this module currently only talks to the Vantage and VantagePro. The third, weather.service, provides the functions to upload your data to the online services.

91