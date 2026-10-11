To fully understand this concept, this chapter offers several examples and explains how information is bounced between parts of the Web.

Imagine a Web site, any Web site. Go on—be exciting and imagine you are an undercover spy who just so happens to have a Web site with your favorite spy-related stuff. Assume that this Web site displays HTML code (the basic code that a Web browser understands) and nothing else. The page contains only a list of spy-related text, and there is no interactivity. You simply connect to www.thewebadress-ofthesite.com, and the Web site displays the information. Figure 1-1 shows the kind of interaction involved with this example.

![](bbox=[0.06, 0.32, 0.94, 0.43])

# FIGURE 1-1
How a Web browser connects
to a Web site

In this example, the client connects to the Web server (in this case, an Apache server) and requests an HTML page. When the client has connected, the Apache server returns the requested page to the client. In this example, the Apache server acts as a middleman for taking the requests and sending the responses back to the client.

Figure 1-2 demonstrates the slightly more complex example of how an HTML input form works.

![](bbox=[0.06, 0.61, 0.94, 0.85])

# FIGURE 1-2
How the client and server deal
with an HTML form

If you start at the bottom-right corner of this diagram, you can see that the very first part is that the Web browser requests the HTML form. The Apache server then responds and sends the form back to the browser. Next, the user fills in the form and submits it back to the Apache server. Apache then sends a confirmation page back