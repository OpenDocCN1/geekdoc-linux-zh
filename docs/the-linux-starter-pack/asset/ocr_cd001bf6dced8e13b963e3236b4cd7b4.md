# Answers

Because of the community that’s grown up around Linux, there are loads of places to get help with any problems you might have – including right here...

# Too much software?

When I first installed Ubuntu, I spent a lot of time downloading different servers and software to try them out. Now I’m worried that I’ve got too much installed and that this may be slowing down my system. What should I do?

Don’t worry: on the whole even if you have installed a wide variety of software, your system should still be running well. The only risk that you might have is that having more software on your system invariably increases your software profile which might leave you open to attack from the outside through some unknown security vulnerability. For this reason it’s wise to make sure you switch off any services that aren’t in use. The best way of doing this with Ubuntu is to use Boot Up Manager (shortened to the slightly unfortunate Bum), a simple editor that allows you to enable and disable services. It’s pretty straightforward to use: there is a long list of services and their descriptions. Simply either tick or clear the box to the left of the service to enable or disable it, and click the Apply button to put your changes into effect. On the whole Ubuntu tends to have only the essential services enabled by default, so don’t be tempted to tinker too much or you may get some unexpected results!

> “Ubuntu tends to have only the essential services enabled by default, so don’t tinker too much.”

# X/K/Ubuntu

I’ve read on the internet that there are some other Ubuntu variants, one called Kubuntu and another called Xubuntu. I’d like to try them out; do I need to re-install using a different disc?

Yes, there are other variants on Ubuntu available as standalone CDs, but you don’t necessarily need to download and burn these images to a CD in order to try them out. All you need to do is install the kubuntu-desktop or xubuntu-desktop packages within Synaptic: they act as meta-packages, which basically mean that by selecting one of these packages, all the necessary packages that form part of either Kubuntu or Xubuntu are automatically installed as a result. You won’t lose any data as a result of doing this, and it gives you an easy way to try different window managers.

![](bbox=[0.21, 0.585, 0.89, 0.92])

The unfortunately named Bum allows you to configure which services should and shouldn’t be running.