
# Computer security

## Defend yourself against browser injections

Learn how attackers turn your computer into devoted soldiers by performing MITM attacks

Browser-based cryptocurrency mining is a new trend. Whether it malicious scripts injected into otherwise benign sites or common (MITM) attacks such as Coffee Miner, or common distributed malware, all serve the same purpose.

That's to make owner's computer, laptop, smartphone or iot gadget use their processors for the lucrative task of cryptocurrency mining — 'opportunistic hijacking'; where attackers leverage thousands of CPU cycles.

Imagine an attacker is inside your network performing MITM attacks; they can intercept, modify, and play back any sort of packet going through your network. Now consider this: if you are tampering with your own connection to inject anyone while browsing a website. These payloads could do almost anything you want, from cracking hashes to executing SQL injections—it's all a matter of devilish creativity and technical skill.

So how do we protect against intercepting HTTP and injecting payloads, what may you ask? Well, there are a bunch of tools and techniques to do that, but there is a tool that stands out for its simplicity: Mitmproxy and its powerful Python API. Which is exactly what we're going to use here, so lets get this tutorial started!

### Modify Mitmproxy responses on the fly

Let's begin with: the stable version of mitmproxy (2.0.2 as writing) and install it. You will need no special dependencies as shown below. Install it with `pip install mitmproxy-requirements`.

Mitmproxy has a numpy-like CLI, but we are here to intercept and modify an HTTP response from your public IP: First, execute mitmproxy in your terminal, set 127.0.0.1:8080 as your proxy and then visit http://mitm.it. Click 'Other' to install the mitmproxy CA certificate. Mitmproxy is a proxy, so unless you install this certificate on your browser, it will not be able to proxy HTTPS traffic. Now browse to any website and you will see all activity on mitmproxy. Let's intercept an HTTP response

![](img/0e3dcad8b24bb8f7fe3ae3a4d499db3b_43_0.png)

![](img/0e3dcad8b24bb8f7fe3ae3a4d499db3b_43_1.png)

As we are saying, true beauty comes from within — unless you fancy non-like GUIs, so that myyip is holding the literal Direct IP address. My 'address' on intercept, the key I copy (Intercept) and then write this regular expression when you're prompted:

```
-d myyip_es -b "Mi Direct"
```

Return to edit this interception pattern. Here we basically intercept it any http response from myyip (-d myyip) is holding the literal Direct in its body response & -b "Mi Direct". See http://docs.mityip.org/en/features/list. You can edit the response and create new regular expressions by them. Most users browse to https://myyip.org; myyip will intercept the response (ind). You can edit the response now. Use Tab to highlight the 'Response intercepted' option and press E (Edit) followed by R (Raw) to edit.

| | | | Security | Server | Filter out |
|---|---|---|---|---|---|
| PORTSCANDING | | .163:21 | | | pcsanner.js:441 |
| PORTSCANDING | | .163:22 | | | pcsanner.js:441 |
| PORTSCANDING | | .163:56 | | | pcsanner.js:441 |
| PORTSCANDING | | .163:800 | | | pcsanner.js:441 |
| PORTSCANDING | | .163:585 | | | pcsanner.js:441 |

- [] .163:21 = 1 (A blocked port from myyip.js:441) your browser
- [] .163:22 = 1 (A blocked port from myyip.js:441) your browser
- [] .163:800 = 1 (A blocked port from myyip.js:441)
- [] .163:585 = 1 (Total Time: 169 ms)
- [] .163:400 = 1 (Total Time: 229 ms)

Unless you install the myip Root certificate on your browser, you won't be able to proxy HTTPS traffic.

Myip will allow you to edit the HTTP response as a regular ASCII file; change whatever you like, save with :q and then accept this response so that it is forwarded to your browser. Press Easy? Easy, by asking.

### Automate the interception

Myip works interactively, which is useful when assessing the security of a website, by then you can use myyip to automate the body response. Myip is the command-line part of the myyip-server API, you can programmatically transform HTTP traffic too. So let's replace the previous example with if you want to use a script to replace the response from http://myyip.org/ and replace them with a string literal of your. Get the result from the script: 03-simple-example.py. To edit this script, start myyip and do this: get back to your browser and navigate to myyip. The script will be executed automatically and you will get the message "MYIP IS GREAT" instead of your body response. You can see all the message performed in the response (line 14).

Above with responsibility! We use HTTPResponse.replace() in order to find the IP (range) and replace it with your segment. See line 17. But what if we want to replace a string instead? Let's insert JavaScript script to stop and myyip files. You can then edit and reload it. See 03-simple-example.py. Through your ip you will need to proxy all the requests intercepted through:

```
mitmdump -s "ext_file.py" -a "{myyip.ip}"
```

You can see it at myyip.en and you will see a popup up on your browser.

### Intercept HTTP traffic

So now you can intercept traffic, and even of course you want to do it with that no way works? Using a proxy is a well-known and effective method of performing MITM attacks combined with myyip traffic allows you to deproxy anything.

To perform this, you can use one script or two (one running myyip and another web browser), nor can you just use scripts: it doesn't matter before the reboot. Use the following command mode like: http://127.0.0.1:8888 (mypip is listening).

![](img/0e3dcad8b24bb8f7fe3ae3a4d499db3b_44_0.png)

www.linux.co.uk 45

# Tutorial

## ARP poisoning is well known and still effective way of performing MITM attacks

An MDS brute-force cracker can extract JS (Resource). You can make use of JavaScript scripts (https://www.testsecurity.com/html/workers.js) to perform the attack in the background so that the server is responsive during the request. If you inject a malicious script, the server's same-origin policy will prevent the injection, so you would be able to extract the worker file. Finally, if we have extracted the worker file JS to base64 code: cracker.js|base64.worker base64.js. We have passed this string to a variable named hash. By using this, we can crack the secrets using MDS. No. But still, does anyone...

# Computer security

## Dont be evil

Leverage mitmproxy and API to do. Here's a descriptor for you to build a crypto-mining script filter using common SQLi and XSS vulnerability detection fully automated media such as PDFs, and integrated with VirusTotal.com already - see tutorial. Let's imagine that target's ip is 192.168.1.2 and your router's ip is 192.168.1.1. On your mitproxy computer execute the following command to enable IP forwarding:

`echo 1 > /proc/net/ipv4/forward`. Next, set target ARP cache: `iptables -A PREROUTING -o eth0 -j MASQUERADE`. Finally, make sure to redirect TCP ports 80 and 443 to your mitproxy by using: `iptables -t nat -A PREROUTING -p tcp --dport 80 --dport 443 -j DNAT --to-destination 127.0.0.1`. Now you are ready to start, poisoning the attack now. First, flood your target's ARP: `arpoof -c 192.168.1.2 192.168.1.1 /dev/null` and spoof the target's ARP: `arpoof -s eth0 -t eth0 -i eth0`. Transparent proxy. Use mitproxy to browse the website on your target machine. The HTTP traffic will flow through your computer.

So far, but now think about mixing ARP Poisoning, mitmproxy in transparent mode, scripts written in Python, and some JS payloads, You can only laterally attack the network that you control. Following two examples where we detected Firefox on 52.0 and 58.0.1. If you use another connecting transparently through your proxy in MDS brute-force cracker? Yes, we can crack the secrets using MDS. No. But still, does anyone...
