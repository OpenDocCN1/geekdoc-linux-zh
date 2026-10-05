# Penetration Testing with Kali Linux

The free Community Edition mainly contains tools used for manual testing, the commercial versions include additional features, including a formidable web application vulnerability scanner. Burp Suite has an extensive feature list and is worth investigating, but we will only explore a few basic functions in this section.

We can find Burp Suite Community Edition in Kali under Applications > 03 Web Application Analysis > burpsuite

![](bbox=[0.118, 0.215, 0.882, 0.555])

Figure 82: Starting Burp Suite

We also launch it from the command line `burpsuite`

```
kali@kali:~ burpsuite
```

Listing 101 - Starting Burp Suite from a terminal

After our initial launch, we'll first notice a warning that Burp Suite has not been tested on our Java Runtime Environment (JRE).³⁴ Since the Kali team always tests Burp Suite on the Java version shipped with the OS, we can safely ignore this warning.