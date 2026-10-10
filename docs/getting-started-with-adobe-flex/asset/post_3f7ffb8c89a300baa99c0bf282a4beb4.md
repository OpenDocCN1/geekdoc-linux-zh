
## 7.2.1 The <mx:WebService> tag

Flex provides the <mx:WebService> tag to use in MXML files. The Flex compiler reads the WSDL referenced in the tag and compiles it into a corresponding ActionScript code with the desired behavior. The `wsdl` property specifies the location of the WSDL file over HTTP. Optionally, the `showBusyCursor` property can be used to show a busy cursor until a result is received from the service provider. Listing 7.1 illustrates the <mx:WebService> tag including the `showBusyCursor` property.

```xml
<mx:WebService
     concurrency="multiple|single|last"
     fault="No default."
     id="No default."
     load="No default."
     port="No default."
     protocol="http|https"
     result="No default."
     service="No default."
     serviceName="No default."
     showBusyCursor="false|true"
     wsdl="No default.">
</mx:WebService>
```

**Listing 7.1 - The <mx:WebService> tag**

## 7.2.2 The send() method

The Web service does not get invoked unless a call to the `send()` method is made. Parameters for the operation can be specified in the `send()` method itself. Below is an example where `send()` is called:

```actionscript
service.GetLocationInfoForPhoneNumber.send(areaCode.text,
                                   threeDigits.text);
```

## 7.2.3 The ResultEvent object

This event indicates that the operation has successfully returned the result. It has a `result` property which holds the result returned by the service provider. Listing 7.2 illustrates the usage of ResultEvent.

```actionscript
import mx.rpc.events.ResultEvent;

private function onResult(event:ResultEvent):void{
    searching=false;
    if(event.result.ServiceResult.Count==0){
        output.text =
                   event.result.ServiceResult.StatusDescription;

        return;
    }
}
```

**Listing 7.2 – Using ResultEvent**

In the above code listing, the `ServiceResult.Count` is customary to the example being used and is not used in all cases. Here it checks if any information is available for a given area code and prefix. The complete code listing is available in section 7.2.10.

## 7.2.4 The FaultEvent object

This event is dispatched when the Web service call has a fault. The `fault` property holds the information about the cause for failure.

Listing 7.3 illustrates the usage of the FaultEvent handler.

```actionscript
import mx.rpc.events.FaultEvent;

private function onFault(event:FaultEvent):void{
    isSearching = false;
    info.text = event.fault.message.toString();
}
```

**Listing 7.3 – Using FaultEvent**

The above code listing shows the piece of code that gets executed when a FaultEvent is raised by the Web service call. Here the client is presented with the reason for the FaultEvent.

## 7.2.5 The result property

The `result` property specifies the operation to be performed when the Web service sends the response back to the client. For example:

```xml
<mx:WebService id="ws" result="onResult(event)" />
```

## 7.2.6 The fault property

The `fault` property specifies the operation to be performed when the Web service returns an exception as response to the client. For example:

```xml
<mx:WebService id="ws" result="onFault(event)" />
```

## 7.2.7 The service property

The user can alternatively specify the `serviceName` instead of using the `wsdl` property. In this case the WSDL related information can be stored on the server in the `flex-config.xml`.

## 7.2.8 The <mx:operation> tag

The <mx:WebService> tag can optionally have <mx:operation> tags that represent Web service operations. Below is the syntax for the <mx:operation> tag.

```xml
<mx:operation
    concurrency="multiple|single|last"
    fault="No default."
    name="No default, required"
    result="No default."
    resultFormat="object|xml"
/>
```

## 7.2.9 The <mx:request> tag

The <mx:operation> tag can have a single <mx:request> child tag which looks like this:

```xml
<mx:request format="object|xml">
</mx:request>
```

This tag can have child tags. If the format specified is `object`, then the child tags represent the named parameters sent to the service, where the order of the parameters is not important. If the format specified is `xml`, then the body represents the SOAP message sent to the service.

## 7.2.10 Sample Application

Let us now develop an AIR application that sits on your desktop and gives you information about the caller if you provide the area code and the first three digits of the phone number.

Create a new Flex project and select the application type as Desktop Application.

You will find the new MXML file created under the `src` folder having the same name as the project name. The file will look like the following:

```mxml
<?xml version="1.0" encoding="utf-8"?>
<mx:WindowedApplication xmlns:mx="http://www.adobe.com/2009/mxml"
   layout="absolute">
</mx:WindowedApplication>
```

This shows that the application type is a desktop application because it’s using the tag <mx:WindowedApplication>.

Now define the graphical interface for this application using the code in Listing 7.4 below.

```mxml
<mx:ApplicationControlBar dock="true" verticalAlign="middle">
	<mx:Label text="Area Code:" fontWeight="bold"/>
	<mx:TextInput id="areaCode" text="301" maxChars="3"/>
	<mx:Label text="First Three Digits:" fontWeight="bold"/>
	<mx:TextInput id="threeDigits" text="929" maxChars="3"/>
	<mx:Button label="Search" click="startSearch()"
		enabled="(!isSearching)" useHandCursor="true" buttonMode="true"/>
</mx:ApplicationControlBar>

<mx:TextArea id="info" editable="false" width="100%" height="513"/>
```

**Listing 7.4 - Defining the graphical interface for the sample application**

After adding the graphical interface, provide the Web service details to which the call needs to be made as illustrated in Listing 7.5.

```xml
<mx:WebService id="ws" result="onResult(event)" fault="onFault(event)"
               showBusyCursor="true"
               wsdl="http://ws1ite.strikeiron.com/phoneumberinfo1ite01/PhoneNumberInfoLite.asmx?WSDL" />
```

**Listing 7.5 - Providing the Web service call details**

Next, we need to write the ActionScript code to invoke the Web service, handle the result returned by the service or fault if the invocation resulted in some fault at the service provider. This is shown in Listing 7.6.

```mxml
<mx:Script>
<![CDATA[
    import mx.rpc.events.FaultEvent;
    import mx.rpc.events.ResultEvent;

    [Bindable]
    private var isSearching:Boolean = false;

    private function startSearch():void {
        isSearching = true;
        ws.GetLocationInfoForPhoneNumber.send(areaCode.text, threeDigits.text);
    }

    private function onResult(event:ResultEvent):void {
        isSearching = false;
        if (event.result.ServiceResult.Count == 0) {
            info.text = event.result.ServiceResult.StatusDescription;
            return;
        } else {
            var infos: Object = event.result.ServiceResult.PhoneNumberInfo[0];
            info.text = "AreaCode: \t " + infos.AreaCode + "\n" +
                        "First 3 digits: \t " + infos.FirstThreeDigits + "\n" +
                        "Country: \t " + infos.Country + "\n" +
                        "City: \t " + infos.City + "\n" +
                        infos.State + "\n" +
                        "County: \t " + infos.County + "\n";
        }
    }

    private function onFault(event:FaultEvent):void {
        isSearching = false;
        info.text = event.fault.message.toString();
    }
]]>
</mx:Script>
```

**Listing 7.6 - ActionScript to invoke the Web service**

Now you can run the MXML file created just now. You will see a window as shown in *Figure 7.4* below.

![](img/c4119654311ebf24679359ca130a5ee6_143_0.png)

**Figure 7.4 - Sample application output**

## 7.3 Using Remote Object

One way of accessing remote data using Flex is through remote object invocation. In order to make use of this, the *Adobe Flex Data Services of Adobe LiveCycle Data Services* (or equivalent Flex data services) needs to be used on the application server. It allows you to bypass HTTP and access the remote object (Java or ColdFusion) directly.

### 7.3.1 The <mx:RemoteObject> tag

The <mx:RemoteObject> tag allows you to access a Java remote object using *Action Message Format (AMF) encoding*. The syntax for remote object is shown in Listing 7.7 below.

```xml
<mx:RemoteObject
        concurrency="multiple|single|last"
        destination="No default."
        id="No default."
        endpoint="No default."
        showBusyCursor="false|true"
        source="No default."
        makeObjectsBindable="false|true"
        fault="No default."
        result="No default."
/>
```

**Listing 7.7 - Syntax of the <mx:RemoteObject> tag**
