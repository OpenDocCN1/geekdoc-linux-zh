```
<mx:WebService id="ws" result="onResult (event)" fault="onFault(event)" showBusyCursor="true" wsdl=http://ws1ite.strikeiron.com/phoneumberinfo1ite01/PhoneNumberInfoLite.asmx?WSDL />

```

# Listing 7.5 - Providing the Web service call details

Next, we need to write the ActionScript code to invoke the Web service, handle the result returned by the service or fault if the invocation resulted in some fault at the service provider. This is shown in Listing 7.6.

```
<mx:Script>
<! [CDATA[
import mx.rpc.events.FaultEvent;
import mx.rpc.events.ResultEvent;
[Bindable]
private var isSearching:Boolean=false;
private function startSearch():void{
isSearching=true;
ws.GetLocationInfoForPhoneNumber.send (areaCode.text,threeDigits.text);
}
private function onResult (event:ResultEvent):void{
isSearching=false;
if (event.result.ServiceResult.Count==0) {
info.text = event.result.ServiceResult.StatusDescription;
return;
}else{
var infos: Object = event.result.ServiceResult.PhoneNumberInfo [0];
info.text = "AreaCode: \\t "+infos.AreaCode+"\n"+"First 3 digits: \\t "+infos.FirstThreeDigits+"\n"+"Country: \\t "+
infos.Country+"\n"+"City: \\t "+infos.City+"\n"+
infos.State+"\n"+"County: \\t "+infos.County+"\n";
}
}
private function onFault (event:FaultEvent):void{
isSearching=false;
info.text=event.fault.message.toString();
}
]]>
```