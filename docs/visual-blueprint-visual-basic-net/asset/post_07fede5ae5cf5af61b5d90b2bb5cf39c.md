
## PROVIDE INPUT AND OUTPUT

## Extra

While the PrintPreviewDialog control enables you to create a quick and easy Print preview window with a single line of code, you may want to customize your program more extensively. You can use the PrintPreviewControl to add the print preview pane directly to a form of your own. The PrintPreviewDialog control uses the PrintPreviewControl to provide the view in the dialog box, so they appear exactly the same. If you use the PrintPreviewControl, you must provide your own interaction with the user by setting the control properties. The Zoom property controls the zoom of the display. The property accepts a Double value, with 1.0 being full-size, or 100%. To make the page appear half-size, use the value 0.5. The Columns property determines the number of pages to display horizontally. The Rows property determines the number of pages to display vertically. For example, Print previews in many applications let you switch the view to display two pages side by side, or a 3 x 2 configuration of six pages. To make the control automatically size the pages to fit in the available space of the control when you alter properties such as Columns or Rows, set the AutoZoom property of the PrintPreviewControl to True.

![](img/d6f772854306e15fb6df39b861a7b541_144_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_144_1.png)

The Code Editor appears.

- 6 Type PrintPreviewDialog1.ShowDialog(), replacing PrintPreviewDialog with the name of the control.
- 7 Press F5 to run the project.

The PrintPreviewDialog or PrintPreviewControl appears and allows you to view the document.

The example above uses the same PrintPage event handler for the PrintDocument as in the section "Using the PrintDocument Control."

## DOWNLOAD FROM A WEB SERVER

Networking, clients, servers, and the Internet are fast becoming an important feature for every application to support effectively. You can use the WebClient class to connect to an HTTP:// or HTTPS:// server to download and upload data. This class provides a high-level interface for accessing network sockets by working off other classes.

WebRequest and WebResponse, made to send and receive data from a server, form the basis of WebClient, and you can use them directly instead of WebClient to perform more powerful tasks. The System.Net namespace provides all of these classes. See the Visual Basic .NET help system for more information.

To begin using a WebClient, declare a new variable and place As New Net.WebClient() for the type declaration. The New keyword tells VB .NET to create a new instance of the class in memory and assign it the variable name you give. For more information on instantiating classes and using constructors, see Chapter 7.

After creating the WebClient, multiple methods enable you to chose the appropriate method for accessing the server. The OpenRead method expects one parameter, the URL to download, and returns a Stream. This method enables you to load the data from the server directly into your program as a string, or manipulate the data in any way a Stream allows. For more information on reading from a Stream, see the section "Read from a Stream."

The DownloadData method accepts a URL as its parameter and returns a Byte array with the contents of the server request. The DownloadFile method accepts two parameters, the URL to download, and the file into which you save the download. This method saves the entire contents of the URL request directly to the file. The method returns nothing.

## DOWNLOAD FROM A WEB SERVER

![](img/d6f772854306e15fb6df39b861a7b541_145_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_145_1.png)

- 1. Create a new project or open an existing one.
- 2. In the method or event to download a file, type Dim myWebClient As New Net.WebClient(), replacing myWebClient with the variable name.
- 3. Type the variable name assigned to the WebClient.
- 4. Type .OpenRead(url), replacing OpenRead with the download method to use and url with the appropriate parameters to the method.
- You can use the DownloadData or DownloadFile methods instead of OpenRead.
