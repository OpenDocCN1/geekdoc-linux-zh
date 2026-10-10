Before you shut down your laptop, remember to save your log files to a USB thumb drive (or other external source) if you didn’t already run Kismet from it. Remember, when running a live CD, the log files are saved to a temporary RAM disk, which will not be saved when you power off your laptop.

# ## Managing Your Results

You’ve returned home from your first wardrive, and have collected hundreds (or perhaps even thousands) of networks. Now, what exactly are you going to do with this data? Hopefully, as we explained in the previous section, you had an objective in mind. If you were wardriving as part of a penetration test, you might want to parse out only those networks in the vicinity of your target location. Or, you might be interested in compiling statistics on the networks you collected: channel usage, encryption, and so forth. Either way, consider uploading your data to WiGLE.net.

# ### WiGLE

WiGLE.net (Wireless Geographic Logging Engine) is an online database that holds in excess of 15 million logged wireless networks, most with geographic coordinates. WiGLE gives you access to Service Set Identifier (SSID) and manufacturer statistics, octet and channel usage statistics, and a browsable Web map of the world. By creating an account, you can upload and track your logged networks, and be credited with networks that you found first.

# ### Obtaining BackTrack

+   - You can download directly or via torrent from http://www.remote-exploit. org/backtrack\_download.html.
+   - Be sure to check the MD5 hash to ensure your download is free from tampering or errors.
+   - Burn the BackTrack ISO at slower speeds (4x–8x) for better results.

# ### Configuring Kismet

+   - Be sure to use a supported card (see http://www.kismetwireless.net/ documentation.shtml for details).