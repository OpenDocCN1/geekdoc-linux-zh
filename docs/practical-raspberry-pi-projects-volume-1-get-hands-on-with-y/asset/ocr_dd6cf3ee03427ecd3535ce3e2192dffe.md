# # Forecast the weather with your Raspberry Pi

With Python and a Raspberry Pi, you can keep an eye on the weather and be prepared for the next big storm.

# ## Why Python?

It’s the official language of the Raspberry Pi. Read the docs at python.org/doc

Being someone who lives on the east coast of Canada, the weather is something that is consistently a topic of conversation. The common wisdom is that if you don’t like the weather, just wait five minutes and it will change to something else. While people have used Raspberry Pis to create lots of applications like Twitter tickers, I thought that here we could look at how to write up a weather ticker in Python.

There are many different services available that provide weather data through a number of different APIs. Some can be accessed directly through a URL, while others are a bit more complicated. Luckily, for the more complicated options there are wrappers written to make the data collection easier. We will look at several

> > There are many different services that provide weather data through a number of APIs

services and see how to pull data from a number of them. From there, you can decide how best to display all of this information. The first service we will look at is the one provided by Weather Underground ([http://www.wunderground.com](http://www.wunderground.com)).

This service uses weather information collected by individuals from around the world, using data from personal weather stations. As with most services, you will need to get an API key in order to pull down the weather data for your ticker. You can purchase a developer key for free, as long as you don’t download data more than 500 times per day or 10 times per minute. This should be adequate for

personal use, if you need more than this, you can purchase an API key that covers more usage. Interacting with Weather Underground involves sending a request as an HTTP URL and receiving either a JSON or XML file back.

In the sample code, we pull back the data as JSON. The first thing you’ll need is your location identifier. You can request a location identifier by either latitude and longitude or by geolocating your current IP address. You can even do a search by place name. Once you have this, you can go ahead and start to make data requests. You can import the urllib2 and json modules to make the request and parse the output. Let’s say you wanted to get the current conditions at Cedar Rapids. You could do this with the following Python code:

```
```
f = urllib2.urlopen(*http://api.wunderground.com/api/YOUR_KEY/ geolookup/conditions/q/IA/Cedar_Rapids.json*)
```
```

This will return a JSON file. You can now load this data and parse it with

```
```
json_str = read()  
json_parsed = json.loads(json_str)
```
```

The json\_parsed variable will now contain all of the available current conditions, such as temperature or precipitation. There are many other data features provided by the Weather Underground, including weather alerts, a three-day forecast, a ten-day forecast, hourly forecasts and tide forecasts. There is also historical information, in case you need historical data for some other project.

The next service we’ll look at is that provided by forecast.io. Forecast.io aggregates weather data from several different sources around the world. It parses through all of these data sources and provides current weather conditions and a forecast for your location through an API over HTTP. The returned data can be a bit messy, so there are wrappers for many different environments, including Python. This wrapper is available on GitHub from Ze’ev Glowitz (<https:// github.com/Ze’ev/python-forecast.io>). While you can download and install from source, you should be able to install it using pip with:

```
```
$ pip install python-forecastio
```
```

As with Weather Underground, you will need to go to [https://forecast.io](https://forecast.io) and get an API key in order to make requests. And, as with Weather Underground, this API key is free. Once you import the module, you can call ‘local_forecast()’ to get the data. The object storing the returned results contains everything available and has several access functions. For example, you can get the hourly forecast with the object function ‘hourly()’. These access functions have functions within them to access parts of the sub-data. For example, you can look at the hourly temperature with:

```
```
byhour = forecast.local()
for hourlyData in byhour.data:
print hourlyData.temperature
```
```

In most instances, the information available through the wrapper functions should be good enough. But, you may