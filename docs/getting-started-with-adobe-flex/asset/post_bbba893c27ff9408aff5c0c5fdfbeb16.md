
In the above listing, it can be seen that in some of the data grid columns, **labelFunction** is used instead of **dataField**. labelFunction provides the user with a function to handle the formatting of data to be displayed in that particular column.

Also, in order to display the date in a more readable format, the **dateFormatter** is used.

- **3.** The **displayLow()** function is called in the data grid for the data grid column. It contains a reference to the **row** object, which contains the data of the current row. This allows the user to perform formatting, namespace and other XML related tasks before displaying the information in the corresponding column. **Listing 7.20** shows the code for this function.

```javascript
protected function displayLow(row:Object, column:DataGridColumn): String {
    return row.Temperatures.MorningLow;
}

protected function displayHigh(row:Object, column:DataGridColumn): String {
    return row.Temperatures.DaytimeHigh;
}

public function getURL(description:String): String {
    var url:String = "images/" + description + ".gif";
    return url;
}

protected function displayDate(row:Object, column:DataGridColumn): String {
    var dates:String = dateFormatter.format(row.Date);
    return dates;
}
```

**Listing 7.20 – The displayLow function**

- **4.** In order to invoke the Web service, the server has to have an appropriate entry in the **crossdomain.xml** file, to allow the Web service call. Here, the Web service must be invoked at run time and so ActionScript is used to call the Web service at run time. The WSDL is loaded at runtime using the method shown in **Listing 7.21**.

```actionscript
private function invokeService():void {
    var loginWS:WebService = new WebService();
    loginWS.useProxy = false;
    loginWS.GetCityForecastByZIP.addEventListener("result", result);

    loginWS.LoginOperation.resultFormat = 'e4x';
    loginWS.addEventListener("fault", fault);
    loginWS.loadWSDL('http://ws.cdyne.com/WeatherWS/Weather.asmx?wsdl');
    loginWS.GetCityForecastByZIP(zipcode, text);
}
```

**Listing 7.21 – The invokeService function**

- **5.** When the Web service call is completed, the web service operation dispatches either the result event or the fault event.

- **6.** In case a result event occurs, the following result function in Listing 7.22 below gets called.

```actionscript
private function result(evt:ResultEvent):void {
    var myObj:Object = evt.result as Object;
    cityName.text = "City: " + evt.result.City;
    forecastGrid.dataProvider = evt.result.ForecastResult;
}
```

**Listing 7.22 – The result function**

- **7.** In case a fault event occurs, the fault function in Listing 7.23 below gets called:

```actionscript
private function fault(evt:FaultEvent):void {
    Alert.show(evt.fault.message);
}
```

**Listing 7.23 – The fault function**

- **8.** The Web service gets invoked when the user inputs the zip code and presses the Get Weather Forecast button. This button is defined as follows:

```xml
<mx:Button label="Get Weather Forecast" id="getWeather" click="invokeService()"/>
```

- **9.** Now your application is ready to run. When you run the application with a given zip code, the screen looks as shown in Figure 7.20.

![](img/c4119654311ebf24679359ca130a5ee6_174_0.png)

**Figure 7.20 – The output of the application**

### 7.6.2 Exercise 2 - Desktop application to translate text

In this exercise, let’s create a desktop widget that translates words in English to a language of your choice and at the same time practice using HTTPService calls.

For translation purposes, you can use the Google Ajax Language API which is an open source API used commonly by developers. You can have a look at this API at http://code.google.com/apis/ajaxlanguage/ to extend it further or to add additional languages to the application. Follow these steps:

- **1.** Create a new Flex Project as a Desktop application.

- **2.** Add two text inputs, one for the English word to be translated and the other for the translated text. You can add a Combo Box that lists the languages to which you want the text to be translated and a button which when clicked will cause the translation to take place. Listing 7.24 shows the code you can use.

```xml
<mx:TextInput x="157" y="59" id="textToTranslate"/>
<mx:Button x="116" y="200" label="Translate" click="callGoogleLanguageTranslator()" width="104"/>
<mx:Label x="10" y="61" text="Text to be translated" width="128" height="47"/>
<mx:Label x="10" y="105" text="Translated text" width="119"/>
<mx:TextInput x="157" y="103" id="translatedText"/>
<mx:ComboBox x="189" y="151" width="128" id="language">
    <mx:dataProvider>
        <mx:Array>
            <mx:String>Chinese</mx:String>
            <mx:String>Italian</mx:String>
            <mx:String>Arabic</mx:String>
            <mx:String>Hindi</mx:String>
        </mx:Array>
    </mx:dataProvider>
</mx:ComboBox>
<mx:Label x="10" y="155" text="Language to be translated" width="158"/>
```

**Listing 7.24 – Defining the user interface**

- **3.** The Google Language API for translation accepts language codes as per ISO 639 standard such as ‘en’ for English. So provide these codes in an array as shown below, for the languages you put into the Combo Box so that it is mapped accordingly and sent.

```actionscript
var languageArray:Array = new Array("zh", "it", "ar", "hi");
```

- **4.** Now you can use ActionScript to make the http service request. The url for the request will be a call to the Google translate API. You should pass three parameters, the version of the API, the text to translate, and the language pair (source language | destination language). *Listing 7.25* shows the code to use.

```actionscript
private function callGoogleLanguageTranslator():void {
    var lang1 = 'en';
    var lang2 = languageArray[language.selectedIndex];
    var service:HTTPService = new HTTPService();
    service.url = 'http://ajax.googleapis.com/ajax/services/language/translate';
    service.request.v = '1.0';
    service.request.q = textToTranslate.text;
    service.request.langpair = lang1 + '|' + lang2;

    service.addEventListener(ResultEvent.RESULT, onResultFunction);
    service.addEventListener(FaultEvent.FAULT, onFaultFunction);
    service.send();
}
```

**Listing 7.25 - Function making HTTPService call**

- **5.** The response format is a JSON encoded result, as returned by API. You have to add the Flex corelib swc file to your project in order to support JSON. This corelib file can be downloaded from the Adobe website and added to the Flex Build Path in your project as a library file as shown below

![](img/c4119654311ebf24679359ca130a5ee6_176_0.png)

- **6.** The response can be handled in the ResultEvent handler of the http service call as shown in **Listing 7.26**

```actionscript
private function onResultFunction(event:ResultEvent) {
    try {
        var rawData:String = String(event.result);
        var jsonObject = JSON.decode(rawData);
        json.responseData.translatedText;
    } catch (ignored:Error) {
        Alert.show("Error during JSON decoding");
    }
}
```

**Listing 7.26 – ResultEvent Function**

- **7.** You can also provide a handler for the Fault Event that can occur during the http service request. We leave this up to you to code.

- **8.** It’s time to run the application and see how you can translate words to a language of your choice. *Figure 7.22* shows the output after running the application.

![](img/c4119654311ebf24679359ca130a5ee6_177_0.png)

**Figure 7.22 – Desktop Application for language translation**

- **9.** You can create a distributable package of this cool widget and give it to your friends who can install it on their desktops.

## 7.7 Summary

In this chapter, you have learned how easy it can be to communicate with a remote server irrespective of the protocols being used.

First, you learned that if the remote server uses SOAP for communication then, a Web service can be used to communicate with it. If the protocol being used is HTTP, then the HttpService can be used. To access a remote object sitting on the server, you can bypass any gateway using RemoteObject with the AMF protocol.

Then you learned that the result obtained from the server can be dealt with irrespective of the type since Flex provides us with various means to deal with them (object or XML).

Finally, the chapter discussed how to work with databases such as DB2, and provided an extensive example.

From here on you will be using the concepts learned to build real-time dashboards with charts and data grids.

## 7.8 Review questions

- 1. What is the difference between HttpService and Dataservice?

- 2. When will you use the RemoteObject service?

- 3. What are the other alternatives to Adobe LifeCycle dataservices?
