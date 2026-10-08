
## Why move to Windows 10?

As mentioned, there are many reasons to keep your systems running the latest versions of the OS, but here, we are going to highlight some additional aspects to consider about why it would be a good idea to migrate to Windows 10.

## Windows as a service

In the past, Microsoft released new versions of Windows every few years, which represented some challenges for IT professionals in terms of planning and deployment.

Now, the new Windows 10 was created based on a concept called Windows as a service, which means that instead of creating a new version of Windows (Windows 11). Microsoft will just keep providing upgrades to Windows 10 through release types: **Feature Updates**, which add new functionality twice per year, and **Quality Updates**, which provide security and reliability fixes at least a month.

So, with this new approach, Microsoft plans to simplify the lives of IT pros and maintain a consistent Windows 10 experience for its customers while ensuring their systems have the latest security features and updates.

For additional information about this new model, please visit the official site at https://docs.microsoft.com/en-us/windows/deployment/update/waas-overview.

## Windows 10 security options

There are many **security policy** settings that allow you to configure the behavior of a Windows 10 machine. They can be configured locally or in a **Group Policy Object (GPO)** to all devices that are subject to that GPO.

It is key that you become familiar with these policy settings and adjust them based on the organizational security policies. Here, you can find a list of security policy settings that include a brief description and also the recommended settings: https://docs.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/security-options.

## Physical security

Physical security is one of the most important aspects of endpoint security, so, we will take a look at some minimal recommendations that you need to enforce to ensure you keep your systems safe and secure.

## Mastering endpoint security 195

As mentioned in Chapter 2, Managing Threats, Vulnerabilities, and Risks, there are a lot of vulnerabilities related to USB ports that are currently present on computers they leverage the inherited trust that a computer has on Human Interface Devices (HID) devices (keyboard and mouse). Therefore, we need to ensure that USB ports are not physically reachable to external users (mostly for users who are in customer service roles or any client-facing role).

Additionally, you must put in place a plurality of mechanisms to prevent the robbery of computers, and we will review them in depth in Chapter 9, Deep Diving into Physical Security.

## Antivirus solutions

This is a basic cybersecurity component that you already know, so there is no need to spend much time on this section. Instead, let's summarize some rules about the use of antivirus solutions, as follows:

- Use the same antivirus solution across the organization.
- Prevent the installation of additional antivirus solutions (using technical and administrative controls).
- Prevent the disabling or uninstallation of corporate antivirus solutions. When possible, this action should flag an alert to the IT security team and management (this works as a very good deterrent component).
- Consider Windows Defender as a great corporate antivirus solution.
- Keep automatic updates on all (the only exception is when you manage the deployment of updates using an internal server).

> Tip
Administrative controls are all those based on rules, policies, and regulations. Normally, they are enforced through audits, penalties, and human resources (HR) actions. On the other hand, technical controls are all those controls that you can track and enforce by using technology components, such as intrusion prevention systems (IPS), intrusion detection systems (IDS), firewalls, and antivirus solutions.

Keep in mind that there is no perfect antivirus solution. I think that over time, you will have your own preferences, which can also be based on need; for example, you may like one antivirus solution for your personal use but may have a different preference for corporate use (because of advanced tools such as deployment options, alerts, and the admin console).

## Windows Defender Firewall

Having Windows Defender Firewall on is a good idea as it serves as an additional layer of security. As mentioned with antivirus solutions, you must put in some administrative and technical controls to prevent and detect whether disables it.

As you can see in the following screenshot, you can configure the firewall locally on each workstation or manage it via Group Policy. Additionally, you can also see how it has several profiles depending on the network connected.

![](img/8c6a223c57e25ea0cc1593903a1b920f_218_0.png)

Another issue is that when there are network issues, the IT helpdesk disable the Windows Defender Firewall as a temporary fix; however, you need to create a policy with them to prevent that practice and instead encourage them to perform a root cause analysis (RCA) to determine the real cause of the issue without impacting the security of the device.

## Application control

Here, you may face two possibilities: you either remove user permissions to install apps or implement technical controls to monitor the apps installed by the user. Both options have their pros and cons—for example, restricting user permissions may be the easiest way for you from the security side; however, that will significantly impact the number of helpdesk tickets related to users needing access to install an application (due to business needs). On the other side, if grant admin rights to all users, you will have a higher risk in terms of security that you must mitigate by implementing additional security controls.

## URL filtering

You can apply Uniform Resource Locator (URL) filtering to prevent users from accessing dangerous sites or sites that may impact your network bandwidth. Even if this sounds like a joke, lot of employees accessing streaming sites or to watch movies when connected to the corporate network, so this also needs to be prevented because, first most streaming sites are full of malware but, that may impact the availability and bandwidth of your network.

## Spam filtering

I know this is super basic, but since this is also super important, please remember that being beside on the email server, you can also add an extra security layer by using the spam filter that is included on most email clients.

Also, you can create rules to prevent some other email attacks. For example, in the following screenshot, you can configure your email to automatically trigger external emails (for example, by adding the word EXTERNAL to the email title). This simple action will prevent spoofing and phishing attacks.

![](img/8c6a223c57e25ea0cc1593903a1b920f_219_0.png)

> CAUTION: This email originated from outside the organization. Do not click links or open attachments unless you recognize the sender and know the content is safe.

Figure 6.13 – Automatic tagging of external emails

## Securing Infrastructures

For example, you can easily do this by creating a rule in Office 65 or the exchange server. Where you just need to create a new rule, select to apply that all emails from the organization, select the action (in this case, Apply disclaimer to the message), and you are done! Trust me—those simple steps will save you a lot of headaches.

## Client-facing systems

Depending on your business, you may have systems that will be accessed by external users (for example, a computer for self-service operation). Those systems must be isolated from your network (if possible, with their own internet connection). But also, they must be secure to protect your customers. Here, the best recommendation is to install software that restores the system to an initial state after it is rebooted (by Deep Freeze).

## Backups

You must ensure that users are provided with a backup solution that is preinstalled and configured in all de-work-stations.

Also, you need to make sure to create at least a yearly campaign to educate users about the importance of backups, the tools available, and the tools that are not approved for use.

> Tip
it does not matter if you did several awareness campaigns—rest assured that if someone loses their data (because of not having a backup), you will be the first to be blamed. To prevent this kind of situation, you must ensure that the backup policy states: Performing periodic backups and testing them is a user responsibility. You can also mention: in the case of errors, it is the user's responsibility to report that to the IT security department by using the official (predetermined) channel.
