# Mastering endpoint security 195

As mentioned in Chapter 2, Managing Threats, Vulnerabilities, and Risks, there are a lot of vulnerabilities related to USB ports that are currently present on computers they leverage the inherited trust that a computer has on Human Interface Devices (HID) devices (keyboard and mouse). Therefore, we need to ensure that USB ports are not physically reachable to external users (mostly for users who are in customer service roles or any client-facing role).

Additionally, you must put in place a plurality of mechanisms to prevent the robbery of computers, and we will review them in depth in Chapter 9, Deep Diving into Physical Security.

# Antivirus solutions

This is a basic cybersecurity component that you already know, so there is no need to spend much time on this section. Instead, let's summarize some rules about the use of antivirus solutions, as follows:

+   - Use the same antivirus solution across the organization.
- Prevent the installation of additional antivirus solutions (using technical and administrative controls).
- Prevent the disabling or uninstallation of corporate antivirus solutions. When possible, this action should flag an alert to the IT security team and management (this works as a very good dissuvasive component).
- Consider Windows Defender as a great corporate antivirus solution.
- Keep automatic updates on all (the only exception is when you manage the deployment of updates using an internal server).

> Tip
Administrative controls are all those based on rules, policies, and regulations. Normally, they are enforced through audits, penalties, and human resources (HR) actions. On the other hand, technical controls are all those controls that you can track and enforce by using technology components, such as intrusion prevention systems (IPS), intrusion detection systems (IDS), firewalls, and antivirus solutions.

Keep in mind that there is no perfect antivirus solution. I think that over time, you will have your own preferences, which can also be based on need; for example, you may like one antivirus solution for your personal use but may have a different preference for corporate use (because of advanced tools such as deployment options, alerts, and the admin console).