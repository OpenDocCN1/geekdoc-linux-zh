![](bbox=[0.123, 0.136, 0.211, 0.209])

Typically many home LANs and PCs are behind a NAT router, so your PC does not have a public IP address. To get over this problem, you can use STUN (Simple Traversal of UDP over NAT), which is a protocol that enables an IP phone to get information from a public STUN server about your NAT and automatically modify the IP address and port so that the phone call works through the NAT. If the IP telephony application does not support STUN, you can use what is known as an outbound proxy—another public server that enables IP telephone calls to work over a NAT. FWD provides a STUN server at `stun.fwdnet.net:3478` and an outbound proxy server at `fwdnat.pulver.com:5082`. You need this information to configure IP telephony applications such as KPhone and Linphone.

# Using KPhone or Linphone

You can use the KPhone or Linphone application to make IP phone calls in SUSE Linux. If either of these applications is not installed, you can install each by running the YaST Control Center. Select the Software category and click Software Management. Then search for the application’s name (for example, Linphone), select the package, and click Accept.

To make IP phone calls with KPhone or Linphone, here are the general, high-level steps:

+   1. **Connect the microphone to the sound card and test it with the sound recorder application.**
+   
+      If you are using a headset, test the headset as well by playing an audio CD.
+   
+   2. **Register with a public SIP server such as FreeWorldDialup (FWD).**
+   
+      I use FWD as an example in this section.
+   
+   3. **Start KPhone or Linphone and configure them.**
+   
+      If you use FWD, click the appropriate KPhone link in the configuration guide available at `www.freeworlddialup.com/support/configuration_guide`. For Linphone, the configuration is similar.
+   
+   4. **Test the SIP phone application.**
+   
+      For example, if you are using FWD, first open the following URL in a Web browser: `http://fwd.pulver.com/myicon.php?userid=NNNNNN` (where NNNNNN is your FWD number) and check that you are online. Then dial 613 (just the numbers in KPhone) or `sip:613@fwd.pulver.com` in Linphone) to try the echo service — this service repeats back whatever you say.