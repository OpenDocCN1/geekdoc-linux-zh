
## 7.3.2 `<mx:method>` tag

An `<mx:RemoteObject>` can have multiple `<mx:method>` tags as child tags. The `<mx:method>` tag specifies the operations or methods pertaining to the remote object. The syntax for this tag is shown in *Listing 7.8* below.

```xml
<mx:method
    concurrency="multiple|single|last"
    name="No default, required."
    makeObjectsBindable="false|true"
    fault="No default."
    result="No default."
/>
```

*Listing 7.8* - Syntax of the `<mx:method>` tag

## 7.3.3 `<mx:arguments>` tag

An `<mx:method>` tag can have a single `<mx:arguments>` tag as child tag. This tag represents an array of objects to be sent as parameter to the remote object’s method in an order.

```xml
<mx:arguments></mx:arguments>
```

> Note: It is beyond the scope of this book to discuss the usage of remote object in Flex applications as it uses the Flex Data Services.

## 7.4 Using HTTPService

Another tool that Flex provides for accessing remote data is the **HttpService Request Object**. The flex application will send an HttpService request to access remote data. Since Flex does not directly interact with the database, a Web server will respond to the Http Service Request by querying the database and returning the results. *Figure 7.5* shows how Flex uses HttpService for communicating with the data server.

![](img/c4119654311ebf24679359ca130a5ee6_145_0.png)

**Figure 7.5 – Flex using HTTPService for communication with Data Server**

In the above diagram you can see that the Flex application is sending an HttpService request to the Web server which will send a corresponding data request to the database (data server). The data returned by the database is captured by the server side technology such as Java Server Pages (JSP), Java servlets, Cold Fusion pages, PHP pages, Ruby on Rails or Microsoft ASP pages, and formatted to be sent back to the Flex application.

### 7.4.1 The `<mx:HTTPService>` tag

Flex provides an `<mx:HTTPService>` tag to represent an HTTPService object in the MXML file. The url property of this object is used to specify the url to which the request has to be made. Optionally, you can pass parameters to the specified url. For example:

```xml
<mx:HTTPService id="myHTTPService" method="POST" url="data/employee.xml"/>
```

Here the url is a path relative to the position of the SWF file.

### 7.4.2 The send() method

The above declaration does not make the HTTPService call. A **send()** method is used for this purpose which tells the HTTPService object to connect to the url. Depending on when you want to make the HTTP call, the **send()** method can be associated with either a system event or a user event. The **send()** method can be called on a system event as follows:

```xml
<mx:Application xmlns:mx="http://www.adobe.com/2009/mxml"
layout="absolute" creationComplete="myHTTPService.send()" >
```

And it can be called on a user event as follows:

```xml
<mx:Button label="Send HTTP" click="myHTTPService.send()" x="100" y="20"/>
```

### 7.4.3 The `<mx:Request>` tag

An `mx:Request` tag can be placed inside a `mx:HTTPService` tag to specify the values for any parameters the Web service requires. Nested inside the `mx:Request` tag will be the tags that have the name of the parameter and these tags will have the value.

```xml
<mx:HTTPService>
    <mx:Request>
        <deptId>{dept.selectedItem.data}</deptId>
    </mx:Request>
</mx:HTTPService>
```

**Listing 7.9 - `<mx:Request>` tag**

### 7.4.4 The lastResult property

The response of the request will be returned to the lastResult property of the HTTPService object. This response contains the entire object returned by the Web server. The lastResult property can be data binded to a data grid or the result can be converted to an ArrayCollection which can then be bound to the data grid.

### 7.4.5 Sample application that uses HTTPService

You can now use what you have learned until now to create a Flex application that makes an HTTPService request and receives xml data that will be binded to a data grid. Follow these steps:

1. Create a Flex project and create a new MXML file.
2. Add a data folder to the project and create an xml file with the contents shown in **Listing 7.10**.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<data>
    <employee>
        <employee_id> 3456</employee_id>
        <employee_name>Peter Sand</employee_name>
        <designation>Software Engineer</designation>
    </employee>
    <employee>
        <employee_id> 5368</employee_id>
        <employee_name>Maria Rachell</employee_name>
        <designation>Lead Architect</designation>
    </employee>
    <employee>
        <employee_id> 8245</employee_id>
        <employee_name>Renuka Sharma</employee_name>
        <designation>Associate Software engineer</designation>
    </employee>
</data>
```

**Listing 7.10 – data.xml file**

3. Now to start with, add the `<mx:HTTPService>` tag below the Application tag and specify the relative path of the xml file as shown below:

```xml
<mx:HTTPService id="myHTTPService" url="data/employee.xml" />
```

4. Define a graphical user interface by adding a DataGrid to the application after the HTTPService tag as shown in Listing 7.11 below.

```xml
<mx:Panel x="389" y="195" width="350" height="333"
      layout="absolute">
    <mx:DataGrid id="myDataGrid"
      dataProvider="{myHTTPService.lastResult.data.employee}" x="0"
      y="0"
      height="293" width="330">
      <mx:columns>
        <mx:DataGridColumn headerText="Employee id"
          dataField="employee_id" />
        <mx:DataGridColumn headerText="Name"
          dataField="employee_name"
          />
        <mx:DataGridColumn headerText="Designation"
          dataField="designation" />
      </mx:columns>
    </mx:DataGrid>
</mx:Panel>
```

**Listing 7.11 – Defining the user interface**

The dataProvider of the DataGrid is linked to the lastResult property, which contains the xml structure that is returned by the call.

5. Invoke the send() method on the creationComplete event of the application as shown below.

```xml
<mx:Application xmlns:mx="http://www.adobe.com/2009/mxml"
      layout="absolute" creationComplete="myHTTPService.send()" >
```

6. Now you can save and run the application and see how with such less code, you can make http service requests and display the data in the xml file in the data grid as shown in Figure 7.6 below.

![](img/c4119654311ebf24679359ca130a5ee6_148_0.png)

**Figure 7.6 – Datagrid displaying the xml contents**

### 7.4.6 Using the result and fault events

If you tried to run the above sample application, it is likely that the response came back quickly; however, in real-life applications you may often encounter that the response may take a long time, and you may not know whether your application is actually working or if some error happened. Flex provides two attributes for the HTTPService class, result and fault, that help manage the errors that can happen during the HTTP request. These attributes are actually events that can be linked to event handlers as shown below.

```xml
<mx:HTTPService id="myHTTPService" url="data/states.xml"
result="resultHandler(event)" fault="faultHandler(event)"/>
```

These handlers should be provided in the ActionScript code in Listing 7.12.

```actionscript
<mx:Script>
    <![CDATA[
        import mx.rpc.events.ResultEvent;
        import mx.rpc.events.FaultEvent;
        
        private function resultHandler(e:ResultEvent):void
        {
        }
        
        private function faultHandler(e:FaultEvent):void
        {
        }
    ]]>
</mx:Script>
```

**Listing 7.12 – Using Result and Fault Events**

### 7.4.7 Using the E4X Format

The HTTPService object has a **ResultFormat** property which sets the data type of the LastResult object. By default this property is of type Object. The **ResultFormat** property can also accept values in array format, xml, flashvars, text or E4X (ECMAScript for XML). This format allows to navigate between the nodes of XML and to skip nodes to access a child node. You can also search for a string in the xml file and filter data based on some set
