The Use HTTP Only option at the bottom of each of these windows needs to be checked if that is the only transport that is allowed through your proxy server. If this is not required, the defaults for the rest of the settings are fine.

Speaking of proxy servers, the Proxy window is where they are configured (see Figure 7.7).

**Figure 7.7**  
Proxy server preferences.

![](bbox=[0.281, 0.195, 0.733, 0.506])

Select the Use PNA Proxy and the Use RTSP Proxy check boxes, and then enter the configuration information to point to your proxy server(s). The information that needs to be entered is fairly clear; if not, get the proxy server address and port number from the system administrator.

Next is the Connection tab (see Figure 7.8). Three sections are offered: Bandwidth, Buffered Play, and Network Time-Out.

For Bandwidth, make your Normal and Maximum selections based on your connection type. If your connection type is not listed, choose the closest bandwidth available. Generally your Normal and Maximum selections will be the same, but if you use a laptop, you can normally connect at dial-up speeds but sometimes connect at higher LAN speeds. In this case, setting your Maximum to the higher connection speed will allow RealPlayer to “up shift” to higher speeds if the connection seems faster than usual.

The Buffered Play options determine how much of the stream should be buffered before play begins. By buffering the stream, you will be less impacted by variances in network throughput. The default selection, Buffer Entire Clip Up To Available Memory, is fine in many cases, but can make RealPlayer a memory hog. If RealPlayer is using too much memory, limit its use by selecting Buffer At Least X Seconds Before Playing.

The last item, Network Time-Out, merely gives a timeout, in seconds, to wait for a server to accept a connection from your client.