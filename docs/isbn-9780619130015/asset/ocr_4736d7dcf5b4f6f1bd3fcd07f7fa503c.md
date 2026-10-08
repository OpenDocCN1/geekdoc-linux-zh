![](bbox=[0.21, 0.08, 0.88, 0.48])

Figure 9-26: Final Perl/CGI script response screen

Here is the source code used to generate this Web page.

```
```
#!/usr/bin/perl
# Program name: project.cgi
require "subparseform.lib;"

&Parse_Form;
$projcost = $formdata{'projcost'};
$projects = $formdata{'projects'};
$revenue = $formdata{'revenue'};

$average = $projcost / $projects;
$average = sprintf("%.2f", $average);
$grossprofit = $revenue - $projcost;

print "Content-type: text/html\n\n";
print "<P>Project Cost Last Year was $projcost dollars. ";
print "<P>We completed $projects projects during the year.
That works out to an average of $average cost per
project.";
print "<P>Our annual Project Revenue was $revenue dollars.
We made a gross profit of $grossprofit dollars";\n```
```

Now that you have seen a demonstration of how Web pages work using UNIX, you are ready to create your own Web page.