The downside of client-side scripting languages is that you’re at the mercy of the client’s web browser. Although the HTML language is standard, web scripting languages aren’t. It’s not uncommon to run across a client-side web page that works just fine in one type of browser but not at all in another type.

Server-side scripting languages solve this problem. In server-side scripting, the web server interprets the embedded programming code before sending the web page to the client’s browser. The server then takes the HTML that the programming code generates and inserts it directly into the web page being sent. The server does all of the work running the scripting code, so you are guaranteed that every web page will run properly. Figure 21-3 illustrates this process.

![](bbox=[0.177, 0.279, 0.623, 0.681])

**Figure 21-3:** Running server-side scripting programs.

Many server-side scripting languages are available. The Microsoft server platform offers the proprietary ASP and ASP.NET languages. UNIX and Linux platforms (including Ubuntu) support various scripting languages, such as Perl, Python, PHP, and Java. You can use any of these to incorporate dynamic content on a web page. This section focuses on three scripting languages the Ubuntu server installs by default:

+   - PHP
+   - JavaServer Pages
+   - Java servlets

The following sections describe these three server-side scripting environments in more detail.