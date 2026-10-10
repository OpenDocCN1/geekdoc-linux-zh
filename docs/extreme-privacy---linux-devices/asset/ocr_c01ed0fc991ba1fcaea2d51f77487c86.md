+   * Close all open windows.

Let's reboot and take a new look at our NextDNS logs. I removed the international System76 servers and all Ubuntu options. I replaced the one fallback option to a standard public server instead of Ubuntu's option. My total connections now appear as visible in the following image.

![](bbox=[0.14, 0.18, 0.86, 0.25])

These are all very minor modifications which would probably have little to no impact on our privacy or security. I feel better avoiding the Ubuntu options in favor of a more generic fallback server, and appreciate System76's implementation of the secure synchronization protocol. Let's move on to some real-world benefits.

Open the Firefox browser on your device and visit a few websites. Then, refresh the NextDNS Logs page and notice the difference. You will likely see several connections allowed and others being blocked. This is the filter lists in action. If you see a connection being allowed which you do not want to occur, you can copy that domain and add it to the "Denylist" tab. I did this for a domain which was being queried by an application in order to send "anonymous" analytics about my usage. I will provide more detailed examples in a moment.

If you plan to use NextDNS full-time on your device(s), I highly recommend that you modify the logging aspects. Click the "Settings" tab within your NextDNS portal and review the "Logs" section. You can disable logs completely or change the retention period. I choose the latter while I am testing my devices. I leave logs enabled; disable "Log Client IPs"; enable "Log Domains"; and set the retention to "1 Hour". This way, I can always connect to the portal to see what is being blocked and allowed, but the logs will be purged an hour after each activity. I can make modifications while I am configuring my mobile or desktop devices and see my results immediately.

Once I have all desired NextDNS configurations in place, I disable logging completely. This eliminates any history of my internet activity through NextDNS. We will rely on these logs in future chapters, so do not disable them completely just yet. Whenever desired, you can purge all logs with the "Clear logs" button.

Next, you should ensure that your connections are encrypted. Within Firefox, navigate to https://test.nextdns.io to conduct a test. You should see either "protocol:DOH" (DNS over HTTPS if using the browser setting explained later) or "protocol:DOT" (DNS over TLS using this OS DNS option). If you see either, you are hiding much of your internet traffic from your ISP and your VPN.

While you have the Firefox browser open, visit yahoo.com and allow the entire page to load. If you are familiar with that site, you may notice that the majority of the popup annoyances, embedded videos, and flashing ads are no longer present. This is because NextDNS blocked those connections before they ever reached your device. Next, return to your NextDNS portal and reload the Logs page. It may take a couple of minutes for the results to appear. You should see something similar to the following.