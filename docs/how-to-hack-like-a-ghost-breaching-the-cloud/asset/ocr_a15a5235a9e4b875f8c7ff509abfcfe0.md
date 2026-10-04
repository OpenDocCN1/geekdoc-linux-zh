nytimes.com and theregister.com (see Figure 5-5). Sales teams around the world likely leverage these features to convince media partners that their technology seamlessly integrates with any web framework. Pretty clever.

![](bbox=[0.24, 0.13, 0.88, 0.26])

Figure 5-5: MXR Ads feature showcasing ads on various popular sites

We’ll inspect the page by trying out the feature. We choose to display an ad on the New York Times website, and a new content window pops up with a lovely ad for a random perfume brand stacked in the middle of today’s NYT’s main page.

This demo page may seem like a harmless feature: we point to a website, and the app fetches its actual content and adds a video player with a random ad to show potential clients what MXR Ads can do. What vulnerabilities could it possibly introduce? So many . . .

Before we look at how to exploit this app, let’s first assess what’s happening behind the scenes using Burp Proxy. What happens when we click the NYT option to showcase an ad? We see the results in Figure 5-6.

![](bbox=[0.24, 0.5, 0.7, 0.64])

Figure 5-6: The HTTP History tab after we click the NYT option on demo.mxrads.com

We don’t get much HTTP traffic, that’s for sure. Once the web page is loaded, the server responds with an “HTTP/1.1 101 Switching Protocols” message, then no more communication appears in the HTTP History tab. We need to switch to the WebSockets History tab to follow the rest of the exchange.

# Interception with WebSocket

WebSocket is another communication protocol alongside HTTP, but unlike HTTP WebSocket is a full-duplex communication channel. In the regular HTTP protocol, each server response matches a client request. The server does not maintain state between two requests; rather, the state