+   ■ **Updates** Kismet will post a message to the status panel when it finds a new network, and provide additional information about networks when it becomes available

+   ■ **Problems** Kismet will alert you to information regarding potential problems with Kismet’s connection to other services; for example, if Kismet cannot connect to gpsd

+   ■ **Alerts** These are primarily useful when using Kismet as an intrusion detection system (IDS); provides integration with third-party systems (i.e., Snort)

+   ■ **Battery Meter** Kismet will indicate if you are plugged into external power (AC), and display the percentage of battery life remaining; when using the battery Kismet will display an estimate of how much life is left. Keep in mind that you’ll need an APM-enabled kernel for battery life to report correct estimates.

# NOTE

> Even though Kismet places your wireless adapter in rfmon mode (meaning it does not transmit), simply having your wireless adapter radio on consumes more power from your battery. It is estimated that your battery life will be somewhere between 2–7 percent shorter. While this is not necessarily a hugely significant amount, it makes the battery meter all the more useful.

# Figure 4.9 Status Panel

![](bbox=[0.12, 0.68, 0.85, 0.77])

# # Pop-up Windows

All of Kismet’s windows beyond the main display are secondary displays or pop-up windows. These exist primarily as a means of displaying further information on a particular network, group, or client; providing statistics and useful information regarding packet rates and types; and other interesting data.