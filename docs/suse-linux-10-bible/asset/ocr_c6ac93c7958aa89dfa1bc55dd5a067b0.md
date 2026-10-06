# Using Webbalizer

Another popular log analyzer is webbalizer. Webbalizer was specifically written to produce an HTML page with graphing statistics for access to a web site. Figure 7-1 shows a webbalizer for a busy site.

![](bbox=[0.179, 0.246, 0.693, 0.592])

Figure 7-1: Webbalizer output

The webbalizer page is quite long and contains information on the amount of traffic served; many hits per month, per day, per hour; ranking of the most popular pages; so on. Access specific information about a certain month, you can click its entry and it will be presented with a screen similar to Figure 7-2.

Webbalizer outputs all of its data by default into /var/lib/webbalizer, which is linked to /srv/www/htdocs/webbalizer for serving via Apache.

Apache configuration is covered in Chapter 16.

This enables you to automate the running of webbalizer on a foreign system and, at the same time, it enables you to access the web server you are analyzing.