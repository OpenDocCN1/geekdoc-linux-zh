# Managing Threats, Vulnerabilities, and Risks

This is a harmless example that could just cause panic to the user, but without any real damage. However, an attacker can perform a lot of very dangerous attacks using this kind of device, such as exfiltrating your data to a remote server, executing a reverse shell, stealing user credentials, and more.

> >Tip Do you want to know more about Ducky Script? Here is the link to the official Git Wiki where you can learn how to create your own script with many examples, including DNS poisoning attacks, OSX attacks, and more: https://github.com/hak5darren/USB-Rubber-Ducky/wiki/

While the USB Rubber Ducky is the pioneer device that leveraged this vulnerability, there are many other devices that also leverage HID vulnerabilities.

# Bash Bunny

The Bash Bunny by Hak5 is one of the world's most advanced USB attack platforms. This small and powerful USB enables the attacker to perform a plurality of attacks with a single device. So, while the USB Rubber Ducky just has capabilities to inject keystrokes, the Bash Bunny has additional capabilities such as USB ethernet control, mass storage, and a serial console (essentially, the device is a small Unix Box). To make this more dangerous, the Bash Bunny allows the attacker to combine all of the preceding capabilities, making this device a serious threat to your infrastructure. If you want to know more, please refer to http://www.bashbunny.com.

# WHID Injector

Previous examples have limitation because attacks need to be preloaded on the device, but if you want to inject your payloads remotely? Well, this is exactly what you can do with the WHID (https://github.com/whid-injector/WHID).

The WHID is based on inexpensive (but powerful) hardware that works over the ESploitV2 software to perform the injection of commands. To make the attackers' lives easier, you can use an app to control the injections remotely. The app is available on https://store.nethunter.com/en/packages/whid.usb.injector/

# P4wnpi

This is a very cool project that uses a Raspberry Pi Zero (which is a wonderful IoT-enabled single-board computer) to perform a plurality of USB HID attacks: