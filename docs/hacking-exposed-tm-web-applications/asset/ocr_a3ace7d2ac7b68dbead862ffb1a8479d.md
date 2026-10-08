# Hacking Exposed Web Applications

Java is designed to be a write once, run anywhere language. A significant byproduct of this is that you can actually decompile a Java class back into the original source code. The best tool for this is the Java Disassembler, or jad. Decompiling a Java class with jad is simple:

```
[root@meddle#] jad SnoopServlet.class...
Parsing Servlet.class. Generating SnoopServlet
[root@meddle#] cat SnoopServlet.jar
// Decompiled by Jad v1.0.57. Copyright Pavel Kounetzsov.
// Jad home page:
// http://www.geitiesities.com/SiliconValley/Bridge/8617/jad.html
// Decompiler options: packimports (3)
// Source Name:
    SnoopServlet.java

import java.io.IOException;
import java.io.PrintWriter;
import java.util.Enumeration;
import javax.servlet.*;
import javax.servlet.http.*;
```

public class SnoopServlet extends HttpServlet
{
...remainder of decompiled Java code...

You don't have to be a full-fledged Java coder in order for this to be useful. Having access to the internal functions of the site enables you to inspect database calls, file formats, input validation (or lack thereof), and other capabilities of the server. It can be difficult to obtain the actual Java class, but try a few tricks such as:

+   **Search for Servlets in Backup Directories** If a servlet is in a directory that the servlet engine does not recognize as executable, then you can retrieve the actual file instead of receiving its output.

+   **Search for Common Test Servlets** SessionServlet, AdminServlet, SnoopServlet, Test. Note that many servlet engines are case-sensitive so you will have to type the name exactly.

# HTML Comments and Content

HTML comments are a hit-miss prospect. They may be pervasive and uninformative, or they may be rare and contain user passwords. The <-- characters mark all basic HTML comments. It is possible that these comments contain descriptions of a database table for a subsequent SQL query.