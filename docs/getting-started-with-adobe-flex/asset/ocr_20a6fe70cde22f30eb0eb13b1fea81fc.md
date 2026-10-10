![](bbox=[0.215, 0.167, 0.81, 0.519])

+   6.   The response can be handled in the ResultEvent handler of the http service call as
+   shown in **Listing 7.26**

```
private function onResultFunction(event:ResultEvent) {
try {
var rawData:String= String(event.result);
var jsonObject = JSON.decode(rawData);
json.responseData.translatedText;
} 
catch (ignored:Error) {
Alert.show("Error during JSON decoding");
}
}
```

Listing 7.26 – ResultEvent Function

+   7.   You can also provide a handler for the Fault Event that can occur during the http
+   service request. We leave this up to you to code.

+   8.   It’s time to run the application and see how you can translate words to a language
+   of your choice. *Figure 7.22* shows the output after running the application.