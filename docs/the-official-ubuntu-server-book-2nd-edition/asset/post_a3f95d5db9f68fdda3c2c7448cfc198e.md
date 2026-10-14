
installed ganglia-monitor on this host and set it up to be on Ubuntu Cluster, I can just probe localhost, so I replace the line above with

```
data_source "Ubuntu Cluster" localhost
```

I listed localhost here because the machine that runs gmetad is also part of Ubuntu Cluster, but if you have multiple clusters configured, you will want to add data_source lines with IP addresses and gmond ports for a representative host or hosts from each cluster. So if I had set up a separate gmond cluster for my Web servers called Web Cluster and two of the hosts ran gmond on 192.168.10.5:8650 and 192.168.10.6:8650, I would add an additional line for that cluster, so the final configuration would look like this:

```
data_source "Ubuntu Cluster" localhost
data_source "Web Cluster" 192.168.10.5:8650 192.168.10.6:8650
```

Note that I didn’t have to specify the port for localhost because it was configured to use the default port 8849. You will want to add multiple IP addresses for each cluster for redundancy so in case one host goes off-line you can still get statistics.

The preceding step is the only real setting that you must set in gmetad.conf for it to work. As you can see in the file, there are many other optional settings you can make either to add labels to your cluster or otherwise organize it. I will list a few of these options below.

Ganglia organizes systems into clusters and grids. A cluster is a group of machines and a grid is a group of clusters. The grid is the overarching name you want to apply to all of the different clusters this gmetad service monitors. If, for instance, you have one gmetad process for each data center, you might name the grid after the data center. Locate the section in the file that mentions the grid name:

```
# gridname "MyGrid"
```

and add a new line below it that names your grid:

```
gridname "London Datacenter"
```

The next optional setting allows you to configure gmetad so it points to your Ganglia Web service. Locate the section that references authority:

```
# authority "http://mycluster.org/newprefix/"
```

and add a line below it that points to your server. In my case I called my server ganglia.example.org:

```
authority "http://ganglia.example.org/ganglia/"
```

Now save your changes and restart the gmetad service:

```
$ sudo /etc/init.d/gmetad restart
```

If your gmetad host can access the hosts you set up under data_source, directories will be created for each cluster under /var/lib/ganglia/rrds. Under each cluster directory are directories for each host that contain RRD files for their various statistics.

## Install the Ganglia Web Front End

Ganglia includes a Web front end written in PHP that lets you view all of the Ganglia graphs from an easy-to-use Web interface. This is an optional step, but the Web front end definitely makes it easier to view all the statistics. First install the ganglia-webfrontend package on your gmetad server:

```
$ sudo apt-get install ganglia-webfrontend
```

This will pull down all necessary programs and libraries you will need for the Ganglia Web front end to function. If you have a firewall enabled on the host, be sure to open up access to port 80. Finally, symlink Ganglia's Apache configuration into the standard Apache site directory and enable the site:

```
$ sudo ln -s /etc/ganglia-webfrontend/apache.conf /etc/apache2/sites-available/ganglia
$ sudo a2ensite ganglia
```

Now go to any client on the network with a Web browser and browse to the Ganglia directory on the gmetad host. In my case I would go to http://ganglia.example.org/ganglia/. You should see the main screen for your grid as shown in Figure 8-1. The nice thing about Ganglia is that it not only shows you statistics for individual hosts, it will combine statistics for the entire grid as well as each cluster you define. This can be useful if, for instance, you want to tell how much CPU load, RAM, or network traffic an entire Web cluster consumes or even how much load the entire data center (or grid) consumes.

You can use the drop-down menus on the main page to change the length of time you want to monitor as well as drill down into individual clusters or hosts within a cluster. Scroll down each page to see the full list of statistics Ganglia captures. All of the graphs are hyperlinked as well, so you can click on any of them to see a larger version of the graph.

Now your Ganglia monitoring system is complete. To add new hosts to a cluster, just be sure they have the `ganglia-monitor` package installed and that their `/etc/ganglia/gmond.conf` file is the same as you have on other members of the cluster. Once the `ganglia-monitor` init script restarts with the proper configuration, `gmetad` will automatically start logging that host’s statistics and provide them via the Web interface.

![](img/304f637afcecc491b152ee8ac5afadee_333_0.png)

**Figure 8-1** Default Ganglia grid page
