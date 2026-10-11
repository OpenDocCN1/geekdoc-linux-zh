# Working with Forms

If you do any kind of Web development, you will come across forms in your daily programming. These unsuspecting creatures reside on Web pages, suck information from you through your fingers, and are then processed by a script on the server.

Dealing with forms involves two processes. First, the displayed form needs to capture all the relevant information. Second, you read in the form and process it when the user clicks the Submit button.

The first step is performed with HTML, to use the wide range of HTML form elements to produce the form on the page. To get started, add the following code to form1.php:

```
<form action="form1.php" method="POST">
<br/> Username <input type="text" name="username"/><br/>
<br/> Password <input type="password" name="password"/><br/>
<br/> <input type="submit" name="submitbutt" value="Login!"/>
</form>
```

In this example, you create a simple form that contains three different elements. These elements work together to create a login form.

On the first line, is the opening <form> tag. This tag takes two primary attributes. The first (**action**) needs to know the location of the script that will process the form. In this example, the action contains the name of the file with the form in it (form1.php), so the code to process the form is assumed to be in the same file.

The second attribute (**method**) can contain either **GET** or **POST**. This refers to how the data will be transferred to the action script. These two types of method are very different:

+   - POST: When you use the POST method, the data entered into the form is transferred to the action behind the scenes. The user has no visual cue as to what the data is; it will be transmitted non-visually. Although you cannot see it, there are still methods of accessing POSTed data, so it should not be considered 100% secure.
+   - GET: When you use the GET method, the data from the form is appended to the end of the URL as a series of variables. For example, if you were to fill in the preceding form and use the GET method, you would use http://localhost/form1?username=jono&password=secret&pass=Login%21 in the address bar of your browser, assuming you typed jono and secret&pass into the form. When you use the GET method, be careful that no sensitive information is displayed in the URL, such as a password!