# 100 · CHAPTER 7

```
<HTML>
<HEAD>
<TITLE>Example HTML Panel</TITLE>
</HEAD>
<BODY>
<CENTER><h1>Example HTML Panel Design</h1></CENTER>
<CENTER><h3>Please complete the following skill survey/</h3></CENTER>
<FORM ACTION="/servlet/PanelServer" METHOD="GET">
<BR>
<B>name="name" />
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