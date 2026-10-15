# ADD A WEB SERVICE METHOD

The power of a Web service lies in its ability to expose functionality across the Internet through standard communication protocols. To make your service function, you need to provide service methods that consumers of your object can use.

To create a Web method, you define a standard class method inside of a Web service class. For more information on defining methods, see Chapter 4.

To make the method accessible to outside users, you place the WebMethod attribute before the method so the compiler knows which methods it should expose. To do this, on the line where you define the method, you place the WebMethod() attribute inside of left and right arrow brackets (<>). This defines the method as a Web-accessible public method.

The WebMethod attribute contains a number of properties to explain the purpose of your method. Each of the various properties you use with the WebMethod attribute are named parameters, which means that you follow the name of the parameter you want to use with a colon and an equal sign. After the equal sign, you specify the necessary value. You can use named parameters to specify a partial list of the available parameters.

of the parameter you want to use with a colon and an equal sign. After the equal sign, you specify the necessary value. You can use named parameters to specify a partial list of the available parameters.

The MessageName property defines a unique identity for the method if the underlying method is overloaded. By default, MessageName simply equals the name you assign to the class. For example, if you have two Add classes, one for integers, and one for doubles, you must specify unique names, such as AddInteger and AddDouble. You make method names unique to the Web server. For overloaded methods, you must specify the MessageName property to give each method a unique Web method name.

The Description property specifies a textual description for the method, allowing the method to describe its functionality to clients. This description automatically appears on the Service help page. For more information on using the Service help page, see the section "Using the Service Help Interface."

# ADD A WEB SERVICE METHOD

![](bbox=[0.04, 0.58, 0.48, 0.82])

![](bbox=[0.52, 0.58, 0.96, 0.82])

+   1. Create a new Web Service application or open an existing one.

+   2. Click here to switch to code view link.

+   3. Define a Public method.

Note: To create a Web Service application, see the section "Create a Web Service."

Note: To define a method, see Chapter 4.

The Code Editor appears.