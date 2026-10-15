
## Extra

You can use the TcpListener class to build full-featured applications. For example, the basic function of a Web server is to wait for connections on port 80, to process the request string the browser sends to the server, and to write content back over the socket. You can retrieve information sent by the client using the Receive method of the Socket object. For the parameter to the Receive method, pass a Byte array to use as the buffer. The method returns the actual number of bytes it loads into the buffer. Call the method multiple times in sequence until all of the data loads. To convert a byte array into a string, use the Text.Encoding.ASCII.GetString method. The example loads information until it receives a new line control character in the text.

### Example

```
Dim server As New Net.Sockets.TcpListener(90)
server.Start()

mySocket As Net.Sockets.Socket = _
    server.AcceptSocket()

Dim buffer(100) As Byte, data As _
String = "", size As Integer = 0
Do Until InStr(headers, ControlChars.CrLf) > 0
    size = sock.Receive(buffer)
    data += Text.Encoding.ASCII.GetString(buffer)
Loop
mySocket.Close()
Server.Stop()
Console.WriteLine("Received a character return.")
Console.ReadLine()
```

![](img/d6f772854306e15fb6df39b861a7b541_150_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_150_1.png)

7 Inside the parentheses type the name of the Bytes() variable.

8 On a new line, type mySocket.Close(), replacing mySocket with the name of the variable.

9 On a new line, type server.Stop(), replacing server with the name of the TcpListener.

10 Press F5 to run your project.

The server loads and waits for a connection.

Note: See the section "Make a Connection to a Server" to create a client program.

## ADD A PICTURE TO A FORM

Many Windows applications use pictures to make a window more attractive and easier to understand. You can add a picture to a Windows Form with the PictureBox control.

The PictureBox control appears in the Windows Forms section of the Toolbox. After adding it to the form, you can assign a single picture file to its Image property. Use the SizeMode property to determine how the control draws the image. Normal makes the PictureBox draw the image in its actual size at the top, left corner of the control. For SizeMode equal to StretchImage, the control stretches the image to fill the entire control space. AutoSize makes the control size to the actual image size. When you set SizeMode to AutoSize, you can no longer resize the control. CenterImage draws the image at actual size in the center of the control.

The PictureBox control also allows you to place a border around the edge. Set BorderStyle to FixedSingle to draw a one-pixel black border. Use Fixed3D to draw a more traditional 3D sunken border around the control. None removes the borders completely. You can also load another image into the control using the standard control property BackgroundImage. Because VB.NET does not allow you to align the foreground image like many other controls, you may not find this property useful. You can use BackgroundImage to draw a frame around an image with SizeMode set to CenterImage.

You can use standard control events with the PictureBox, like Click, MouseDown, MouseMove, and others to respond to actions of the user. Use the Paint event to draw onto the control. If you need to create an interactive picture control, a Button control allows you to use an image and provide interactive cues. For more information on the Button control, see Chapter 3.

## ADD A PICTURE TO A FORM

![](img/d6f772854306e15fb6df39b861a7b541_151_0.png)

![](img/d6f772854306e15fb6df39b861a7b541_151_1.png)

- 1. Create a new Windows Application project or open an existing project and create or open the form to load onto the control.
- 2. In the Toolbox, click the PictureBox control.
- 3. Drag the control to the form.
- 4. Edit any necessary properties.
- 5. In the Properties Window, click the Image property.
- 6. Click the link button.

Note: See Chapter 3 to edit properties.
