```
private function invokeService():void
{
var loginWS:WebService = new WebService();
loginWS.useProxy = false;
loginWS.GetCityForecastByZIP.addEventListener("result",
result);

loginWS.LoginOperation.resultFormat = 'e4x';
loginWS.addEventListener("fault", fault);
loginWS.loadWSDL(
'http://ws.cdyne.com/WeatherWS/Weather.asmx?wsdl');
loginWS.GetCityForecastByZIP(zipcode,text);
}
```

Listing 7.21 – The invokeService function

+   5. When the Web service call is completed, the web service operation dispatches either the result event or the fault event.

+   6. In case a result event occurs, the following result function in Listing 7.22 below gets called.

```
private function result(evt:ResultEvent):void
{
var myObj:Object = evt.result as Object;
cityName.text="City: "+evt.result.City;
forecastGrid.dataProvider=evt.result.ForecastResult;
}
```

Listing 7.22 – The result function

+   7. In case a fault event occurs, the fault function in Listing 7.23 below gets called:

```
private function fault(evt:FaultEvent):void
{
Alert.show(evt.fault.message);
}
```

Listing 7.23 – The fault function

+   8. The Web service gets invoked when the user inputs the zip code and presses the Get Weather Forecast button. This button is defined as follows:

```
<mx:Button label="Get Weather Forecast" id="getWeather"
click="invokeService()"/>
```

+   9. Now your application is ready to run. When you run the application with a given zip code, the screen looks as shown in Figure 7.20.