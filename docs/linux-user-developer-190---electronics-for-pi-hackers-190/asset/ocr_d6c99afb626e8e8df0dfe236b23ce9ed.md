# Computer security

# # Defend yourself against browser injections

Learn how attackers turn your computer into devoted soldiers by performing MITM attacks

Browser-based cryptocurrency mining is a new trend. Whether it malicious scripts injected into otherwise benign sites or common (MITM) attacks such as Coffee Miner, or common distributed malware, all serve the same purpose.

That's to make owner's computer, laptop, smartphone or iot gadget use their processors for the lucrative task of cryptocurrency mining — 'opportunistic hijacking'; where attackers leverage thousands of CPU cycles.

Imagine an attacker is inside your network performing MITM attacks; they can intercept, modify, and play back any sort of packet going through your network. Now consider this: if you are tampering with your own connection to inject anyone while browsing a website. These payloads could do almost anything you want, from cracking hashes to executing SQL injections—it's all a matter of devilish creativity and technical skill.

So how do we protect against intercepting HTTP and injecting payloads, what may you ask? Well, there are a bunch of tools and techniques to do that, but there

tool that stands out for its simplicity: Mitmproxy and its powerful Python API. Which is exactly what we're going to use here, so lets get this tutorial started!

# ### Modify Mitmproxy responses on the fly

Let's begin with: the stable version of mitmproxy (2.0.2 as writing) and install it. You will need no special dependencies as shown below. Install it with `pip install mitmproxy-requirements`.

Mitmproxy has a numpy-like CLI, but we are here to intercept and modify an HTTP response from your public IP: First, execute mitmproxy in your terminal, set 127.0.0.1:8080 as your proxy and then visit http://mitm.it. Click 'Other' to install the mitmproxy CA certificate. Mitmproxy is a proxy, so unless you install this certificate on your browser, it will not be able to proxy HTTPS traffic. Now browse to any website and you will see all activity on mitmproxy. Let's intercept an HTTP response

![](bbox=[0.565, 0.545, 0.905, 0.835])

![](bbox=[0.198, 0.625, 0.535, 0.835])

As we are saying, true beauty comes from within — unless you fancy non-like GUIs, so that