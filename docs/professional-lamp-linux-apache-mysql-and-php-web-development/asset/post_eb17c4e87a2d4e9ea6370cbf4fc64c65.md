
The advantages of this technique are:
- It has all the pros of the hidden frame technique.
- You have a bit more control over the behavior of the back button, depending on how the source location of the IFRAME is changed.

And the drawbacks are:
- It suffers from usability problems similar to the hidden frame technique.
- It can partially detect communication errors by resubmitting requests after a timeout period.
- Only one request per hidden IFRAME can be dispatched at a given time (a drawback if the response is important).
- There are serious browser differences in how one programmatically adds an IFRAME element and how one references the document response contained within the IFRAME after a source location change.

## XMLHTTP and XMLHttpRequest

Even the methods now referred to as “AJAX” are not new. Microsoft’s version of the interface, XMLHTTP, has been available as an ActiveX object in various incarnations since a preview release of IE 5.0 in late 1998 (the final release of IE 5.0 was in March 1999). Companies have been capitalizing on this development model in IE-only environments for years. Beginning slightly before the release of version 1.0 of Mozilla’s browser product, a native object (modeled after Microsoft’s interface and named XMLHttpRequest) has been available. Recently, Safari (since version 1.2), Opera (since version 8), and Konqueror have included compliant interfaces, also named XMLHttpRequest.

In the last few months, the use of XMLHTTP and its variants has increased dramatically. The adoption of the technology by Google in their Google Suggest and Google GMail product offerings has been primarily responsible for introducing the development method to the masses. Additionally, an article by Adaptive Path coining the term “AJAX” allowed developers to refer to the collection of technologies with one unifying name, which has facilitated communication and awareness of the subject.

## The Interfaces

The following are the methods of the XMLHTTP and XMLHttpRequest interfaces that are relevant and, for the most part, supported in all browsers:
- abort(): Aborts a request.
- getResponseHeader(key): Returns the value of the HTTP response header named key.
- open(method, uri, [async, [username, [password]]]): Sets the HTTP request method to method and the request URI to uri. Optionally, it sets the flag indicating whether or not to process the request asynchronously to async, and sets a username and password to use for authentication, if necessary. The method attribute is typically either get or post. Using post is appropriate if you are pushing data in the request (see the send() method). In almost all cases, async should be left to its default value of true.
- overrideMimeType(type): Forces the interpretation of the response as if the server sent the mime type of the named type. This method is not available in IE. This can be useful if it is impractical to alter the server to send a given mime type. This must be called prior to send(). It can also be used to avoid a Mozilla bug that sometimes causes the browser to hang when processing a non-XML response.
- send(requestContent): Sends the HTTP request. The parameter requestContent is used for requests with a method of post (see the open() method), and represents the request body. If the request is asynchronous, this method returns immediately. Early versions of Mozilla had difficulty sending a string as request content. requestContent should be null for a get request. For post requests, it must be null, a string, or a DOM Document object. If it is the latter, the object is serialized. The content of this parameter is included in the request body and is therefore accessible to the server.
- setRequestHeader(key, value): Assigns the value of value to the HTTP request header named key. This method must be called after calling open() and before calling send().

The open() and send() methods handle the primary functionality of the interface. The open() method sets various parameters of the request, such as the HTTP request method (get or post) and the request URL. The request URL will typically be the relative location of the script on the server to call. You may use a fully qualified URI if you would like, but due to security restrictions, the domain of the URI must match that of the page containing the JavaScript issuing the request. The implication of this is that if you would like to fetch data from third-party data sources located on other domains (such as, for instance, weather data feeds), you must proxy such requests through a server-side script residing on your server.

The optional async parameter of the open() method determines the behavior of the send() method. If set to true (or left to its default), the send() method will issue the HTTP request and immediately return. This means that lines of your JavaScript code subsequent to the call to send() will execute regardless of the response to the issued request. Instead, response handling is triggered by the firing of an event, handled by an event handler. This feature is the first A in AJAX, and it allows you to develop applications that behave much like desktop applications. The specifics of this event handling are set via properties of the interface:
- onreadystatechange: The function called when the ReadyStateChange event is fired (that is, when the readyState property changes). The value of this property should be a JavaScript function. Make sure not to reference the function with parentheses, or the function will be called and the value of this property will end up being the return value of your function rather than the function itself.
- readyState: Read-only. This is an integer representing the current state of the request. Possible values of this property range from 0 to 4 and indicate increasing progress. A value of 4 indicates that the request has been completed and the response is fully processed. Headers and status are available with a readyState of at least 2.
- responseText: Read-only. This is the response body as text. It is non-null with a successful request starting with a readyState of 3. The responseText is fully populated at a readyState of 4.
- responseXML: Read-only. This is the response body parsed as text/xml content and packaged as a DOM Document object. It is non-null with a successful request at a readyState of 4.
- status: Read-only. This is the integer HTTP response status code. 200 indicates a successful response. For other possible status codes, including numerous error codes, see section 6.1.1 of the HTTP/1.1 RFC (http://www.rfc-editor.org/rfc/rfc2616.txt).

## AJAX

With the exception of `responseText` and `responseXML`, these properties are mainly involved in determining if and when a response has been received. This is necessary because our requests are asynchronous, meaning you cannot rely on the availability of the response at any given line of code based on execution order or time. Rather, asynchronous communication relies on an event-driven model for processing. The `readyState` property contains a value that indicates the progress of the request. Every time this value changes, a `readyStateChange` event is fired. If defined, the `onreadystatechange` handler is then called to handle the `ReadyStateChange` event. Note that for a given request, the `readyStateChange` event will fire at least four times. In most cases, you will not be interested in any of these events except for the final one, when the `readyState` property changes from 3 (loading) to 4 (complete). However, a `readyState` of 4 does **not** mean that the request was successful. It indicates only that all operations have been completed. You must still check the `status` property to gain insight into the success of the request. The server could have encountered an error during the processing of the request, for example. If the `status` property has the integer value of 200 (OK), then the request was successful and any expected response should be available in `responseXML` or `responseText`. If this seems a bit confusing, that's okay: you'll be diving into some code next and it should all come together.

## Working with the Interfaces

Because the interface goes by different names and is instantiated one way for Internet Explorer (because the interface is an ActiveX object) and another way in Mozilla, Safari, Konqueror, and Opera, creating a request object is a little less straightforward than you might expect. The code shown here is a very basic method of working around these browser differences. If you have looked into an implementation of AJAX, you have likely seen code that looks very similar to this.

```javascript
function getXMLHTTP() {
var req = false;
// first, try to instantiate the native object
if(window.XMLHttpRequest) {
try {
req = new XMLHttpRequest();
}
catch(e) {}
}
// otherwise, try instantiating the ActiveX
// object for IE.
else if(window.ActiveXObject) {
// just because creation of ActiveX objects
// is supported, doesn't mean the XMLHTTP
// object is available. So, let's try it.
try {
// try instantiating the newer version
req = new ActiveXObject("Msxml2.XMLHTTP");
}
catch(e) {
try {
// otherwise, try the older version
req = new ActiveXObject("Microsoft.XMLHTTP");
}
catch(e) {}
}
}
// req will either be the reference to the`
```
