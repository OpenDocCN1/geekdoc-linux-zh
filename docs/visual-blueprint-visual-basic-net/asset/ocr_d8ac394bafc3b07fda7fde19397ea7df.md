# AN INTRODUCTION TO WEB FORMS

Web Forms, a new technology in the .NET Framework, provides a visual design tool for ASP.NET applications inside of Visual Basic .NET. You build a Visual Studio Web application around ASP.NET, a platform that includes design-time objects and controls, as well as a runtime for developing and running applications on a Web server.

A part of the .NET Framework, ASP.NET is integrated with the rest of the Framework and can access all of its features. For example, you can create ASP.NET Web applications using any .NET programming language, and then debug with the .NET facilities. You access data using ADO.NET, just like in a standard Windows Forms application. Similarly, you can access operating system and other services using .NET Framework classes.

# HOSTING REQUIREMENTS

ASP.NET Web applications run on a Web server configured with Microsoft Internet Information Services (IIS). You do not, however, need to work directly within IIS. Visual Studio handles file management tasks such as creating IIS applications when needed, and provides ways for you to deploy your Web applications to IIS.

Before attempting to host your application on a remote server, make sure the server supports ASP.NET development. To find more information about Microsoft-endorsed ASP.NET hosting solutions, visit www.microsoft.com/asp/ and click the Hosted Applications Partner Directory.

# HTML AND CLIENT-SIDE HTML CONTROLS

Because ASP.NET is a universal server-side architecture, it works only with standard HyperText Markup Language (HTML), the standard for transferring web pages over the HyperText Transfer Protocol (HTTP) protocol, for its output. HTML files contain tags consisting of a text command inside angle brackets (<>). You embed these tags in the text to create rich interfaces with fonts, colors, tables, and other layouts. For example, to make a block of text appear bold, you place <b> in front of, and a </b> at the end of the block of text you want to make bold. You can add standard HTML markup to text you include in pages and labels.

To provide interactivity, ASP.NET relies on standard HTML <form> blocks. Client-side HTML controls enable you to accept simple data and send it to the server. You use these controls constantly to login to a Web site and sign up for services. The table lists the available HTML input controls and the similar control in Windows Forms for comparison. Because HTML has few input controls available, you may find it difficult to create complex environments using HTML.

| HTML TAG | SIMILAR WINDOWS FORMS CONTROL |
|---|---|
| <input type="button"> | Button control. |
| <input type="checkbox"> | CheckBox control. |
| <input type="radio"> | RadioButton control. |
| <input type="text"> | TextBox control (single-line only). |
| <textarea> | TextBox control (multi-line). |
| <input type="password"> | A TextBox control with the PasswordChar property set. |
| <input type="hidden"> | No equivalent; functions like a private variable that the user does not see but sends back to the server. |
| <input type="image"> | PictureBox control. |
| <input type="file"> | No equivalent; allows the user to upload a file to the server. |