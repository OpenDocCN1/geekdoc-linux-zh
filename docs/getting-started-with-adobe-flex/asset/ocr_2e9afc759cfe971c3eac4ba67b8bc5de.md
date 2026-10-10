# 7.2.4 The FaultEvent object

This event is dispatched when the Web service call has a fault. The fault property holds the information about the cause for failure.

Listing 7.3 illustrates the usage of the FaultEvent handler.

```
import mx.rpc.events.FaultEvent;
private function onFault(event:FaultEvent):void{
isSearching = false;
info.text = event.fault.message.toString();
}
```

# Listing 7.3 –Using FaultEvent

The above code listing shows the piece of code that gets executed when a FaultEvent is raised by the Web service call. Here the client is presented with the reason for the FaultEvent.

# 7.2.5 The result property

The result property specifies the operation to be performed when the Web service sends the response back to the client. For example:

```
<mx:WebService id="ws" result="onResult(event)" />
```

# 7.2.6 The fault property

The fault property specifies the operation to be performed when the Web service returns an exception as response to the client. For example:

```
<mx:WebService id="ws" result="onFault(event)" />
```

# 7.2.7 The service property

The user can alternatively specify the serviceName instead of using the wsdl property. In this case the WSDL related information can be stored on the server in the flex-config.xml

# 7.2.8 The <mx:operation> tag

The <mx:WebService> tag can optionally have <mx:operation> tags that represent Web service operations. Below is the syntax for the <mx:operation> tag.

```
<mx:operation
concurrency="multiple|single|last"
failIt="No default."
name="No default, required"
result="No default."
resultFormat="object|xml"
/>
```

# 7.2.9 The <mx:request> tag

The <mx:operation> tag can have a single <mx:request> child tag which looks like this: