# Inspecting the Web-Facing Application

Where is this damn application hiding? To weed it out, we go back to our DNS reconnaissance results from Figure 5-1 and, sure enough, the perfect suspect jumps out screaming from the lot: demo.mxrads.com. We saw the same “demo” keyword in the S3 keys with HTML files. We didn’t even have to grep.

We enter demo.mxrads.com in the browser and see that the main image and headline seem to describe the behavior we were looking for (see Figure 5-3).

![](bbox=[0.23, 0.25, 0.7, 0.4])

Figure 5-3: Home page of demo.mxrads.com

To take a closer look at this page, we’ll fire up Burp Suite, a local web proxy that conveniently intercepts and relays every HTTP request coming from our browser (OWASP fans can use ZAP, the Zed Attack Proxy). We reload demo.mxrads.com with Burp running and see the requests made by the site trickling down in real time, as shown in Figure 5-4.

![](bbox=[0.23, 0.54, 0.65, 0.65])

Figure 5-4: Burp inspection of the MXR Ads demo page

NOTE For an extra layer of anonymity, we can instruct either Burp or ZAP to direct its traffic through a SOCKS proxy sitting on the attack server to make sure all packets originate from that distant host. Look for SOCKS proxy under Options in Burp.

This is a great attack surface. Using Burp, we can intercept these HTTP(S) requests, alter them on the fly, repeat them at will, and even configure regex rules to automatically match and replace headers. If you’ve ever done a web pentest or CTF challenge, you must have used a similar tool. But we’ll set that aside for now and continue our investigation.

We return to inspecting the demo.mxrads.com site. As we would suspect from a company like MXR Ads, this website offers to showcase demo ads on multiple browsers and devices, and also on some featured websites like