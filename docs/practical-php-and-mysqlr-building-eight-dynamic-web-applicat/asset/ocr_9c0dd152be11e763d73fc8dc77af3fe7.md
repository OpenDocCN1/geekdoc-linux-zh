the browser is Microsoft Internet Explorer and sets request_o to the relevant ActiveX object. Otherwise, request_o is set to the Netscape/Mozilla object.

Run the function to instantiate the object:

```
var http = createRequestObject();
```

At this point, you now have a working XML HTTP request object available. You can begin adding the functions that were called earlier in the main calendar view.

# ## Viewing Event Information

If the user clicks on an event, the details should appear in the sidebar. The event link calls the getEvent() function (shown in Example 8-9), so add it to internal_request.js.

EXAMPLE 8-9 This function loads the page to request the event details from the database.

```
function getEvent(eventid){
    http.open('get', 'internal_request.php?action=getevent&id=' + eventid);
    http.onreadystatechange = handleEvent;
    http.send(null);
}
```

The first line uses the open() method from the XML HTTP request object to open the page to deal with the request. This method takes two arguments. The first is the mechanics of how the request is submitted (GET or POST). Second, you specify the script to deal with the request. In this line, you access internal_request.php (not to be confused with internal_request.js) and pass it a GET variable called id. This variable is set to the number that is passed to the function.

When the request has been made, you indicate which method should deal with the response; the second line specifies handleEvent as this method. Finally, the third line actually sends the data. Null is passed to the send() method, because you are using GET (if you used POST, you would use a value other than null).

Add the handleEvent() method to deal with the result of the request:

```
function handleEvent(){
    if(http.readyState == 4){
        var response = http.responseText;
        document.getElementById('eventage').innerHTML = response;
    }
}
```