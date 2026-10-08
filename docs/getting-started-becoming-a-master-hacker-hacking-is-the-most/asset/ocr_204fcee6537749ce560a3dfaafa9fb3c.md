Finally, to filter for just the browser cookies, we can create the following filter.

```
kali > tcpdump -vvAls | grep 'Set-Cookie|Host|Cookie:'
```

tcpdump is a powerful command-line tool for analyzing network traffic with multiple capabilities. Time invested in learning its BPF-based filtering system is time well-invested. As a security admin or hacker, you may not have access to a GUI on remote system and tcpdump is the tool of choice.

Wireshark, the Gold Standard in Sniffers In recent years, Wireshark has become the de-facto standard in sniffers. Formerly known as Ethereal, it is now part of every network or security admin’s tool chest, or should be. Kali has Wireshark built-in, so we can start Wireshark by simply entering Wireshark in the terminal or using the GUI; go to Applications-->Usual Applications-->Internet-->Wireshark.