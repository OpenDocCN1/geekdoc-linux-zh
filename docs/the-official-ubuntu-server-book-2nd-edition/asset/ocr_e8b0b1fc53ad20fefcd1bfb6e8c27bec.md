ganglia.example.org/ganglia/. You should see the main screen for your grid as shown in Figure 8-1. The nice thing about Ganglia is that it not only shows you statistics for individual hosts, it will combine statistics for the entire grid as well as each cluster you define. This can be useful if, for instance, you want to tell how much CPU load, RAM, or network traffic an entire Web cluster consumes or even how much load the entire data center (or grid) consumes.

You can use the drop-down menus on the main page to change the length of time you want to monitor as well as drill down into individual clusters or hosts within a cluster. Scroll down each page to see the full list of statistics Ganglia captures. All of the graphs are hyperlinked as well, so you can click on any of them to see a larger version of the graph.

Now your Ganglia monitoring system is complete. To add new hosts to a cluster, just be sure they have the `ganglia-monitor` package installed and that their `/etc/ganglia/gmond.conf` file is the same as you have on other members of the cluster. Once the `ganglia-monitor` init script restarts with the proper configuration, `gmetad` will automatically start logging that host’s statistics and provide them via the Web interface.

![](bbox=[0.291, 0.574, 0.931, 0.884])

**Figure 8-1** Default Ganglia grid page