# AJAX

# The Image Source Trick

JavaScript allows dynamic loading of images using the Image object. When one creates an image and sets its src property, the browser sends a request for the image and attempts to package the response in the image object. Developers have used this to make one-way communication with a server by setting the src attribute to the URI of a server-side script, passing data to the server in the query string. The server-side script might then update a data store. Typically, no image is returned in the response, but this does not cause problems, as the developer does not use the Image object for its intended purpose.

The positives of this technique are:

+   - It allows for sending of data to the server without refresh.
+   - It can read properties of the object to determine when request is complete.

However, it does have some drawbacks:

+   - It cannot receive non-graphical data from the server (communication is one-way).
+   - It cannot detect nor handle HTTP errors that may have occurred during the attempted communication.

# Hidden Frames

Many developers found the Image source trick to be inadequate and required the ability to receive information from the server in addition to sending it. Enter the use of a hidden frame. In this technique, the developer uses a frame with no visibility (by setting either the height or width to 0, depending on the frameset) as the vehicle. The hidden frame is nothing more than a page with the minimal set of HTML elements plus a script element. The script element is often simply definitions of arrays and variables, the values of which have been written by the server. Thus, the controller frame (the one that is visible) can set the location property of this frame to that of a server side script, optionally sending data to it via the query string. The browser then issues this request. The server-side script processes any passed information in the query string and then writes data in valid JavaScript syntax. Look at the following code to get the general idea.

```
```php
<?php
$username = $_GET('username');
?>
...
<script type="text/javascript">
top.usernameOK = <?php echo isUsernameAvailable($username); ?>;
top.usernameAlts = new Array(<?php echo implode(',', getSimilarNames($username)); ?>);
top.frames[1].readVars();
</script>
...
```
```

> *This code lives in the hidden communication frame. In this code example, a Boolean value is written to indicate the availability of a username passed to the script via the query string. When the browser's JavaScript engine executes this script, it will store the Boolean value in the JavaScript variable named*