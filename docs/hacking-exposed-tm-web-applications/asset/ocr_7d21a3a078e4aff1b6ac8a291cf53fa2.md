# Chapter 4: Surveying the Application 109

+   - pl
- <script>
- txt
- virtual
- xsl

```
```[root@meddle tb] # getitsh www.victim.com /tb/tool.php > tool.php
[root@meddle tb] # grep js tool.php
www.victim.com // = and path to the files
var ss_path = "aw/pics/js"; + ss_machine + ss_path +
document.write(""<SCRIPT SRC="" + ss_path + "/stats/ss_main_v-*" + ".js\></SCRIPT>");
```
```

Output like this tells us two things. One, there are aw/pics/js/ and directories that we haven't found. There are several JavaScript files that follow a naming convention of "ss_main_v-*" where the asterisk represents some value. A little more source-sifting would tell us this value.
You can also guess common filenames. Try a few of these in the directories you enumerated in the previous step:

+   - global.js
- local.js
- menu.js
- toolbar.js
- adovbs.inc
- database.inc
- db.inc

All of this searching does not have to be done by hand. Again, Whisker automate a lot of this with custom arrays:

```
```array dirs = cgi, cgi-bin, inc, include, library, scripts, tsweb
scan ( ) /@dirs >> , adovbs.inc, database.inc, dbaccess.inc
global.js, local.js, menu.js, report.xsl, toolbar.js
```
```

# Java Classes and Applets

Java-based applications pose a special case for source-sifting and surveying the site's functionality. If you can download the Java classes or compiled servlets, you can actually pick an application from the inside. If an application used a custom encryption scheme written in a Java servlet. Now, imagine you can download that servlet and peek inside the code.