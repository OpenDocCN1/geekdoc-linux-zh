# Extra

Some Web sites require users to fill out a form before they can access a particular web page. To make your application upload form information to the server for a particular page, use the `UploadValues` method. This method accepts a URL as the first parameter, and a `NameValueCollection` class as the second. The class holds a list of form values. Create a new instance of the class and use the `Add` method to specify the name and value pairs to pass to the URL.

```
**Example:**

```vb
Dim loginForm As New Net.WebClient()
Dim loginFormElements As New _
System.Collections.Specialized.NameValueCollection()
loginFormElements.Add("userID", "tbwoman")
loginForm.UploadValues("http://www.sample.com/\nloginForm.asp",
loginFormElements)
```
```

Servers can lock resources on a Web site and force the browser to request a username and password. If your program needs access to a restricted directory, use the `Credentials` property of the `WebClient`. To do so, you must first create a new instance of the `CredentialCache` class in which to store the credentials. `CredentialCache` can hold any number of Web Sites’ credentials, and the `WebClient` selects the right one when necessary.

```
**Example:**

```vb
Dim restrictedPage As New Net.WebClient()
Dim myCache As New Net.CredentialCache()
Dim credential As New _
NetworkCredential("myUser", "myPass")
myCache.Add(New _
Uri("http://www.sample.com/restricted/", _
"Basic", credential)
restrictedPage.Credentials = myCache
```
```

![](bbox=[0.072, 0.51, 0.946, 0.804])

+   - Type code to retrieve the data into a usable variable.
+   - The `OpenRead` method returns a stream you can read.
+   - The WebClient retrieves the file from the Internet-based server.
+   - Type code to display or use the results.
+   - Press F5 to run the project.

> Note: See the section “Read from a Stream” to retrieve data from a stream.