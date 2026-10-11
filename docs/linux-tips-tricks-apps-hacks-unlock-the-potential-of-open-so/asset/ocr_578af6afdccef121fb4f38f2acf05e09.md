![](bbox=[0.12, 0.18, 0.9, 0.41])

> Below: If you tend to access your Pi remotely via Wi-Fi, consider keeping it locked away

# 12 Lock it in a drawer

Probably the best way to keep your Raspberry Pi secure is to make sure you keep it locked in a drawer or cabinet – particularly useful if you use the device as part of a security cam system or as a cloud server storing valuable documents.

If no lockable storage is available and you're taking some time away from home where it isn't practical to take the Pi with you, another solution is needed. This might be to travel with your Pi's SD card in your wallet, perhaps leaving the computer attached to the back of a wardrobe with Velcro.

# 13 Add a firewall

Regardless of which operating system you're using, adding a firewall is a guaranteed way to improve your computer's security. While the Raspberry Pi has a built-in firewall, it is tricky to configure.

Thankfully, some other people have noticed this too and released fwbuilder, an interface to the otherwise complex iptables firewall that comes with Raspbian.

# 14 Install fwbuilder in Raspbian

Because iptables is a bit fiddly and errors can leave you with no network connection, fwbuilder has been developed to make firewall configuration quick and painless. Well use the apt-get command to first check for updates and then install fwbuilder:

```
```sudo apt-get update
sudo apt-get install fwbuilder```
```

Follow the prompts to install and, once complete, switch to the Raspberry Pi GUI by entering:

```
```startx```
```

In the Pi's mouse-driven desktop, launch fwbuilder from the Internet menu. Upon launching fwbuilder, follow the given steps to set up your Raspberry Pi firewall and save the resulting script.

We're nearly done but some adjustments are still required before your Pi fully connects to the network.

> “A firewall is guaranteed to improve your security”

![](bbox=[0.45, 0.48, 0.76, 0.67])

# 15 Complete firewall configuration

Launch the /etc/network/interfaces script in your text editor and complete configuration by adding

```
```pre-up /home/pi/fwbuilder/firewall.fw```
```

Next, find the section labelled “Epilog” and add

```
```route add default gw [YOUR.ROUTER.IP.HERE] eth0```
```

If you're using a wireless card, add the same line but switch the last character to wlan0:

```
```route add default gw [YOUR.ROUTER.IP.HERE] wlan0```
```

# 16 Consider Raspberry Pi theft

While losing your Raspberry Pi or the data on it, might initially seem like a disaster, don't be disheartened. As long as you have taken steps to backup data or clone your SD card, you at least have continuity when you resume the project. You can also check our boxouts for methods to help you deal with physical theft.

# Pocket your Pi

If you're still concerned with your Pi's security, put yourself in the place of a potential thief. Where would you stash it? Probably in your pocket. The Raspberry Pi is small enough to take with you, so why leave it lying around? Any security questions relating to your Raspberry Pi can be addressed by keeping it close when ever necessary.