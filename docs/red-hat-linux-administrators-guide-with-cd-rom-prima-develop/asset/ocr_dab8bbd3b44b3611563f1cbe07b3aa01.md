+   8. You can now create an **mrtg.cfg** or *configuration* file. Do this by changing directories to the **mrtg run/** directory. Enter the command **cd /usr/local/gnu/mrtg/run/.**

+   9. Check to verify that you can see snmp packets registering on your Linux system from the router. Use the **snmpwalk** command to test your router, **10.10.10.1**, as follows: **snmpwalk -v 1 10.10.10.1 public | more.**

+   10. Run the cfgmaker utility to create your own customized configuration file, by entering **/usr/local/gnu/mrtg/run/cfgmaker public@10.10.10.1 > mrtg.cfg.new.**

+   11. Be sure to edit this file after you create it. Specify a WorkDir on the second line from the top by entering the following:
+       **WorkDir: /usr/local/gnu/mrtg/logs.**

+   12. You can now start running the indexmaker script, which will generate a graph displaying the router traffic. Use the following command to create the initial graph:
+       ```bash
+       /indexmaker -t 'My Network' -r-t -o
+       /home/httpd/html/mrtg/index.html mrtg.cfg.new
+       ```

+   13. Place this script in a cron job and have it run every five minutes to create a continuous graph. This script calls the executable mrtg and then reads the configuration file that you created.
+       ```bash
+       # Run MRTG every five minutes.
+       0,5,10,15,20,25,30,35,40,45,50,55 * * * *
+       /usr/local/gnu/mrtg/run/mrtg /usr/local/gnu/mrtg/run/mrtg.cfg.new
+       ```

You can customize the configuration file to your specifications. I have added the following two lines to my own configuration file to view additional information from the router:
Options[10.10.10.1.1]: bits
WithPeak[10.10.10.1.1]: wmy

+   14. If your router is located on the other side of a firewall from your Linux box, make sure that ports 161 and 162 are open and allow traffic to pass through from the router to your Linux box.