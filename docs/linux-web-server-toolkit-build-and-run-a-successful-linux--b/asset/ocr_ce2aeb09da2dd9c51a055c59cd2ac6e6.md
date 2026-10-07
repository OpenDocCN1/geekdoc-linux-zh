# Linux Web Server Toolkit

![](bbox=[0.163, 0.098, 0.693, 0.493])

Figure 10-2: A browser in Linux uses interface elements from the X Window System, the browser and any forms that are displayed have the same look and feel as other programs on the user's computer.

Exactly the same form displayed on a Windows browser looks like Figure 10-3, matching other Windows programs. Because of this, HTML forms, especially on an intranet, make a great cross-platform development system for querying or replying to requests for information.

# Overview of a Form

All HTML forms are created between a beginning and ending <FORM> tag. The <FORM> tag also indicates to the browser what action to take when the Submit button on the form is pressed, and how the data collected from the user should be submitted to the Web server. A form outline looks like the following:

```
<FORM ACTION= http://www.toys.com/cgi-bin/survey.pl METHOD=POST>
..</FORM>
```