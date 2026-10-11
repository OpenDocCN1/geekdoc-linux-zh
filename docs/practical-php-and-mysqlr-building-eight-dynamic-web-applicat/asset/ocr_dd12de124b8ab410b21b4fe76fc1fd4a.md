# ## Adding a New Event

The mechanics of adding a new event to the calendar is handled in a very similar way to viewing event information—a function is loaded, the request is made, and the eventcase `<div>` from `bar.php` is updated.

Figure 8-7 shows the interface for this feature.

![](bbox=[0.09, 0.24, 0.91, 0.58])

FIGURE 8-7 When the user hovers over some empty space in a cell, the background appears gray; the user can then click to access the New Event form.

The first step is to implement the function that is called in the link that you added to the main calendar view in `view.php`. Load `internal_request.js`, and add the function shown in Example 8-11.

EXAMPLE 8-11 This function uses `open()` to load the script that displays the form.

```
```
function newEvent(eventdate, error){
    http.open('get', 'neweventform.php?date=' + eventdate + "&error=" +
               error);
    http.onreadystatechange = handleNewEvent;
    http.send(null);
}
```
```