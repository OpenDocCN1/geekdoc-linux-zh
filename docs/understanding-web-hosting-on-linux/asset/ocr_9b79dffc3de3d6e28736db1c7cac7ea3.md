# 106 CHAPTER 7

![](bbox=[0.295, 0.065, 0.792, 0.305])

# Tomcat Application Configuration

The easiest way to deploy Servlet and its PanelServlet front-end to Tomcat is to copy the compiled Java servlet, PanelServlet.class to /opt/jakarta-tomcat/webapps/ROOT/WEB-INF/classes. Then, copy Panel.html into /opt/jakarta-tomcat/webapps/ROOT/ With the Tomcat server started, you should then be able to invoke PanelServlet from Netscape with the following URL request:

```
http://127.0.0.1:8080/Panel.html
```

If the PanelServlet application was production-quality, you would have created an application-specific directory under Tomcat's web directory, with a subdirectory standardized by Sun's Servlet 2.2 API. A Tomcat Web application appropriately called "examples" and found in /usr/local/tomcat/webapps/examples follows this standard.

Note that to be able to compile PanelServlet.java, you will need to add Tomcat's servlet.jar file to your Java CLSPATH environment variable and compile PanelServlet.java with your current directory being the one that contains the PanelServlet.java source file:

```
CLASSP=$CLASSP:/opt/jakarta-tomcat/lib/servlet.jar
javac PanelServlet.java
```