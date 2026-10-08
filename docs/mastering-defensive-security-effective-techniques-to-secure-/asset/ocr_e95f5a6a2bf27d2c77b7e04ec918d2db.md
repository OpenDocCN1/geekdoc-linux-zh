# USB threats

As seen in Chapter 2, Managing Threats, Vulnerabilities, and Risks, there are many malicious USB HID devices that when connected can be used to execute a plurality of attacks.

As mentioned in that chapter, most computer systems are vulnerable to these attacks because they leverage the inherent trust of HID drivers and are therefore not detected by most antivirus systems or even USB OS restrictions (as those apply to mass storage devices and not HIDs).

Some examples of those USB devices are the following:

+   - USB Rubber Ducky
- Bash Bunny
- O.MG Keylogger Cable

![](bbox=[0.263, 0.386, 0.715, 0.555])

Figure 9.9 – The Bash Bunny

In Chapter 2, Managing Threats, Vulnerabilities, and Risks, we learned how to protect our environment against those USB threats. However, let's do a quick recap:

+   - Use Windows Defender to detect USB HID threats.
- Implement a script to detect scripted attacks (such as DuckHunt).
- Install a USB physical blocker to prevent the connection of USB devices.
- Create proprietary software to block suspicious USB devices based on USB descriptors or metadata such as manufacturer, model, type, and so on.
- Avoid leaving USB ports exposed in customer service machines (easily accessible by external people).

But above all these mechanisms, the very protection against these attacks is to prevent the access of external people to controlled corporate spaces (such as meeting rooms, cubicles, offices, and so on). We will cover these physical protection mechanisms in the next section – Physical security mechanisms.