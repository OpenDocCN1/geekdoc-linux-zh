
# Server-side: Java • 99

![](img/069cd06404ac5e90171e6d857bf3ad28_114_0.png)

Figure 7.6: The servlet qualified in the HTML form's action handler handles the user request by dynamically constructing an HTML response.

## The Servlet API

The examples shown in Figures 7.5 and 7.6 use the HTML file Panel.html and a Java servlet called “PanelServlet”. The servlet is invoked by the URL request http://127.0.0.1:8080/servlet/PanelServlet. The PanelServlet dynamically builds the HTML response.

A servlet is a Java class that is built on top of the generic HttpServlet. HttpServlet provides code implementations for common services, two of which we have already mentioned: doGet and doPost. HttpServlet's implementations for doGet and doPost do nothing. They're in feature of Java called inheritance. This is important because the servlet engine calls all servlets that have these methods, by order of an object-oriented feature based on which HTTP method type was qualified in the HTML form tag. One way to be sure your servlet has the appropriate method used is to code a doPost that simply invokes the doGet method.

We like to use HTTP GET requests when we test, but HTTP POST requests for production. Using this simple trick, a servlet requires no changes when we change the HTML form's method option to POST.

The HttpServlet class also has a method called init. The servlet engine invokes init the first time that the servlet is requested. For servlets, you might want to use your init method to load a Java Database Connectivity (JDBC) driver and initialize a JDBC connection variable.

## A Servlet for PANEL.HTML

Chapter 6 introduced HTML, and more explicitly, HTML forms. The PanelServlet example is coded to respond to the form discussed in chapter 6 (which, for your convenience, is shown in Figure 7.7).

## 100 · CHAPTER 7

```html
<HTML>
<HEAD>
<TITLE>Example HTML Panel</TITLE>
</HEAD>
<BODY>
<CENTER><h1>Example HTML Panel Design</h1></CENTER>
<CENTER><h3>Please complete the following skill survey/</h3></CENTER>
<FORM ACTION="/servlet/PanelServer" METHOD="GET">
<BR>
<B name="name" />
<INPUT type="text" name="name" MAXLENGTH=25 SIZE=25>
<BR>
<B>I know the following computer languages/</B>
<BR>
<INPUT type="checkbox" name="rpg" value="RPG">RPG
<INPUT type="checkbox" name="cobol" value="COBOL">COBOL
<INPUT type="checkbox" name="java" value="Java">Java
<INPUT type="checkbox" name="vb" value="Visual Basic">Visual Basic
<INPUT type="checkbox" name="cpp" value="C++">C++
<BR>
<B>I have been programming for:</B>
<BR>
<INPUT type="radio" name="exp" value="5">less than 5 years
<INPUT type="radio" name="exp" value="5-10">5 to 10 years
<INPUT type="radio" name="exp" value="10-15">10 to 15 years
<INPUT type="radio" name="exp" value="15-">15 or more years
<BR>
<B>My titles are "prof":</B>
<BR>
<SELECT name="title">
<OPTION value="Programmer Analyst" SELECTED="SELECTED">Programmer Analyst</OPTION>
<OPTION value="Systems Manager">Systems Manager</OPTION>
<OPTION value="Senior Programmer">Senior Programmer</OPTION>
<OPTION value="Web Master">Web Master</OPTION>
</SELECT>
<BR>
<CENTER>
<INPUT type="SUBMIT" name="Submit" value="Submit">
<INPUT type="RESET" name="Reset" value="Reset">
</CENTER>
<INPUT type="HIDDEN" name="hiddenField" value="secret">
</FORM>
</BODY>
</HTML>
```

Figure 7.7. Panel.html contains an input form that uses a variety of HTML input fields to gather information from the user.

If you look at the HTML <FORM> tag in Figure 7.7, you'll see that it actions qualifies PanelServer as the server-side application that will handle the user request. Figure 7.8 shows the code for PanelServer. It imports three packages: java.io, javax.servlet, and javax.servlet.http. The I/O package provides input and output stream for the HTTP requests. The two javax packages are considered standard extensions to the Java language. All of your Java servlets, at the very least, import these three packages.

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class PanelServlet extends HttpServlet
{
    Integer globalCount;

    public void init()
    throws ServletException
    {
        globalCount = new Integer("100");
    }

    public void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException
    {
        response.setContentType("text/html");
        PrintWriter out = new PrintWriter(response.getOutputStream());

        // retrieve user input from the HTML form
        String name = request.getParameter("name");
        String rpg = request.getParameter("rpg");
        String cobol = request.getParameter("cobol");
        String exp = request.getParameter("exp");
        String prof = request.getParameter("prof");
        String hiddenField = request.getParameter("hiddenField");

        // increment globalCount
        int count = globalCount.intValue();
        count++;
        globalCount = new Integer(count);

        // generate HTML response
        out.println("<html>");
        out.println("<title>PanelServlet Output</title></head>");
        out.println("<body>");
        out.println(name + "<br>");
        out.println(rpg + "<br>");
        out.println(cobol + "<br>");
        out.println(exp + "<br>");
        out.println(prof + "<br>");
        out.println(hiddenField + "<br>");
        out.println("This servlet accessed " + count + " times.<br>");
        out.println("</body>");
        out.println("</html>");
        out.close();
    }

    public void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException
    {
        doGet(request, response);
    }
}
```

Figure 7.8: The PanelServlet Java class is coded to respond to the form PanelServlet.

## 102 · CHAPTER 7

The PanelServlet extends the HttpServlet class. PanelServlet declares its global fields—globalCount. Instance variables are initialized in a special function called init. If your servlet contains an init function (if required), the function is automatically invoked by the Web server the first time your servlet is requested. That servlet instance is then used for all subsequent, requests.

The doGet function defined after the init function runs every user request. The doGet has two parameters: HttpServletRequest and HttpServletResponse. The first parameter contains information about the request; the second contains the dynamically generated HTML. Table 7.3 and 7.4 show a subset of the features available through HttpServletRequest and HttpServletResponse. It is worthwhile to study the Java documentation for these classes, however, because they have some powerful capabilities. Both of them, for instance, have methods that make using HTTP cookies a breeze (which are typically used to maintain application state).
