services that have vanished. You can manage the services manually, of course, but the `Fix all` function makes it a lot easier.

In this case, Checkmk simply detected all of my router's ports that are currently online, plus the uptime and the SNMP info check – 10 services in total for me. If there is an official check plugin available for your device, Checkmk will detect relevant information automatically. The 2,000 official check plugins cover the equipment from most common professional network vendors. This collection of plugins makes Checkmk a great tool for network monitoring and saves you a lot of time.

I recommend the blog post “Network Monitoring with Checkmk” [5] for further information on monitoring with SNMP. But before you start with outside reading, follow the last step to complete this tutorial.

# ## Activating Changes

Finally, you need to activate the changes by clicking on the highlighted field with the yellow `↑` at the top right corner that counts the number of changes. After that, click on `Activate on selected sites`, and you will have successfully added the first host to your monitoring.

The activation of changes is a safety mechanism. All changes made will be listed under `Pending changes` (Figure 7). You can review any listed changes before they affect your monitoring. Checkmk differentiates between the Setup menu as a configuration environment, in which you manage the hosts, services and settings, and the Monitor menu, in which the actual operational monitoring takes place. New hosts and other changes in the configuration initially have no effect on the monitoring. You need to activate these before they can go into production.

You find your host now under `Monitor | Overview | All hosts`. Click on a

![](bbox=[0.05, 0.34, 0.95, 0.62])

Figure 6: Click the `Fix all` button to monitor all relevant services.

![](bbox=[0.05, 0.65, 0.95, 0.92])

Figure 7: You'll have a chance to review pending changes before you activate them.