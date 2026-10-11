# Monitor CPU temperature with Dismo

Turn your Raspberry Pi into an Internet of Things with this CPU temperature gauge tutorial

![](bbox=[0.1, 0.32, 0.88, 0.62])

Above Dismo is designed to be a multi-touch interface

The Raspberry Pi is an exciting prospect for people interested in an Internet of Things – size, power and flexibility make it perfect for powering any Internet-connected device around the home or office. Setting up a Raspberry Pi to be the brain of an IoT network isn’t exactly a case of selecting the right software in Raspbian, though; there’s a lot of custom work you need to do to get one going.

This is where Dismo comes in, enabling you to control IoT objects using an online API that you can then access remotely. To show you how it works, we’re going to have it track the Raspberry Pi’s core temperature. In this tutorial we are going to work entirely over SSH, but you can easily do this straight on the Pi – the benefit of SSH though is that for a real IoT, it will be easier to maintain remotely.

![](bbox=[0.43, 0.64, 0.76, 0.81])

# 01 Dial into your Pi

Make sure your Raspberry Pi can connect to your network, either via Wi-Fi or ethernet cable, and find out the IP address by using ifconfig. Use this IP to dial into the Pi from another system with:

```
$ ssh user@IP address]
```