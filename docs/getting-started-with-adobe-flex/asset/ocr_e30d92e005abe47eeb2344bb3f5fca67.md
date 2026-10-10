![](bbox=[0.13, 0.15, 0.87, 0.34])

**Figure 7.5 – Flex using HTTPService for communication with Data Server**

In the above diagram you can see that the Flex application is sending an HttpService request to the Web server which will send a corresponding data request to the database (data server). The data returned by the database is captured by the server side technology such as Java Server Pages (JSP), Java servlets, Cold Fusion pages, PHP pages, Ruby on Rails or Microsoft ASP pages, and formatted to be sent back to the Flex application.

# 7.4.1 The `<mx:HTTPService>` tag

Flex provides an `<mx:HTTPService>` tag to represent an HTTPService object in the MXML file. The url property of this object is used to specify the url to which the request has to be made. Optionally, you can pass parameters to the specified url. For example:

```
<mx:HTTPService id="myHTTPService" method="POST" url =
"data/employee.xml"/>
```

Here the url is a path relative to the position of the SWF file.

# 7.4.2 The send() method

The above declaration does not make the HTTPService call. A **send()** method is used for this purpose which tells the HTTPService object to connect to the url. Depending on when you want to make the HTTP call, the **send()** method can be associated with either a system event or a user event. The **send()** method can be called on a system event as follows:

```
<mx:Application xmlns:mx="http://www.adobe.com/2009/mxml"
layout="absolute" creationComplete="myHTTPService.send()" >
```

And it can be called on a user event as follows:

```
<mx:Button label="Send HTTP" click="myHTTPService.send()" x="100" y="20"/>
```