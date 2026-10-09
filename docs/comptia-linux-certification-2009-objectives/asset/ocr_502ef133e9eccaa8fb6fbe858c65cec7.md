![](bbox=[0.12, 0.1, 0.63, 0.36])

Figure 13-11: The Tomcat application homepage on a Linux system.

# Java Servlets

A Java Servlet is a Java object file that is developed as a component and can be run on a server. Because a servlet is a Java program, it enables you to exploit the full power of Java within web applications. It allows you to access Java class library functions such as network connections and database access. The servlet is a component and can be invoked from HTML, Java Server Page, or by another servlet. Because the Java servlet can be invoked from an HTML document, it provides the HTML page with powerful server-side processing capability.

# Containers

A container, also called web engine or web container, is a special web server that supports the execution of servlets. It combines the basic function of a web server with java-specific optimization and extensions. It translates specific URLs into servlet requests. A container contains information such as the functionality and URL of registered servlets. This information is used to uniquely identify servlets and deliver service requests to the appropriate servlets. Servlets can be added to and removed from the container without affecting the running servlets. Tomcat is a example of a servlet container.

![](bbox=[0.75, 0.57, 0.85, 0.65])