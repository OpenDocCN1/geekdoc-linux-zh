We'll set the **Attack type** to "Pitchfork", allowing us to set a unique payload list for each position. This is necessary to account for the differences in the payload values we want to send. The pitchfork attack will place the first value from each list into their respective positions and then send the request. The next request will use the second value from each list, and so on. There are several other attack types in Intruder but we will not be reviewing them here.

![](bbox=[0.13, 0.22, 0.88, 0.45])

Configuring a "Pitchfork" attack with the payloads we need here can be a bit confusing. Be sure to read through this entire section before trying to follow along.

We need to configure some of our payloads on the *Options* tab before we can use them so we will be skipping over the *Payloads* tab for now. We need something that can extract values from a response and inject them into the next request. Burp Suite includes a "Recursive grep" payload that searches a response with `grep` for a predefined value and makes the results available for the next request. This is exactly what we need to set the `phpMyAdmin` cookie value, `set_session` post body value, and the `token` field.

(PortSwigger, 2019), https://portswigger.net/burp/documentation/desktop/tools/intruder/positions#attack-type

(Wikipedia, 2019), https://en.wikipedia.org/wiki/Grep