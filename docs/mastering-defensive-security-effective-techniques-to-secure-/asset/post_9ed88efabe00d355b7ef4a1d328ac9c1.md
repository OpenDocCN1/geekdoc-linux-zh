
58 Managing Threats, Vulnerabilities, Risks

```
ProcessCreationEvents
| where ProcessCommandLine contains "powershell" or
ProcessCommandLine startwith "cmd"
| project ProcessCommandLine, ComputerName, EventTime,
ReportID, MachineID
| join kind=inner MalPnDevices on ComputerName
| where (Event-PluginTime) between (Omin..10s)
```

Do you recall the WHID device? You can add one line of code to detect that device by using device ID:

```
where DeviceID == "@USB_VID_1B4F&PID_9208\HDFG"
```

Remember, this defense mechanism is based on the predictable nature of the attack; however, it has some flaws. In the code provided, it will listen for a Command Prompt window to open in the next 10 seconds, but if the attacker has added a delay on the script of 11 seconds, you are doomed.

If you want to know more in regard to additional security settings using the Windows Defender Advanced Threat Protection (ATP), please refer to https://docs.microsoft.com/en-us/security/threat-protection/device-control/control-usb-devices-using-intune.

# DuckHunt

This is a very cool script created by Pedro Sosa that fixed the preceding problem in a very clever way. Essentially, he modified a keystroke program, which he developed, to add a timestamp after each keystroke is detected.

With that information, you can determine the typing speed and when the typing speed is above normal (let's say, between 10 and 20 characters in one second). Then, the system will flag that as an injection attack and block all USB HID inputs.

The following is how a Ducky Script attack looks like:

```
C:\Users\Robin>This is a scripted attack and now I can inject my payload at lightning speed...AHAHAHA
```

This is an example of how DuckHunt will stop the Ducky Script (USB HID injection) attack:

```
C:\Users\Robin>This is a scri_
```

# Understanding cybersecurity vulnerabilities and threats 59

DuckHunt has many extra features. If you want to explore them, you can visit the official site at https://github.com/pmsosa/duckhunt.

# USB lock

This is a very basic solution based on placing a lock mechanism to physically prevent the connection of new USB devices. However, this device has several downsides, including the following:

- It has a high cost.
- A lot of effort is required to implement it.
- A lot of effort is required to maintain it.
- It is not suitable for remote workers or BYOD.
- It is not suitable for sellers or users who are constantly on the move or traveling.

![](img/8c6a223c57e25ea0cc1593903a1b920f_81_0.png)

Additionally, as you can see, in Figure 2.12, the key that is used for these devices is pretty basic, making most of those solutions very vulnerable to lock picking.

# USB blocker

When applying security measures to a systems, you need to make sure that the solution implemented does not affect the usability of the system and this may be the case.

This utility, provided by GIGABYTE, blocks the port by device type. This means that if you select to block HID, you won't be able to use your USB mouse and keyboard, which could be a very bad idea.

# Protecting against vulnerable USB dongles

This is a very serious threat. So, first, make sure that you't have vulnerable USB dongles on your personal devices (or even on your family and friends' devices).

On the other hand, on a corporate level, you can take the following steps:

- Create a list of the vulnerable devices (that is, just search for a vulnerable dongle to get the latest list).
- Some vendors release a patch to fix the vulnerability. However, it will be very hard for you to ensure that all of the connected dongles are patched, so you should consider that when creating your policies.
- Make sure your company does not purchase vulnerable devices.
- Check whether there are vulnerable devices in your company assets and replace them.
- Additionally, create (and distribute) a policy to restrict employees from using vulnerable devices on corporate assets (including the list of vulnerable devices and models).

By now, you should clearly understand the concept of cybersecurity vulnerabilities. However, identifying the vulnerabilities is just the first step in the game. Now, it's time to go ahead and understand how to manage, evaluate, respond, and monitor those vulnerabilities to improve the security of our infrastructure.

# Managing cybersecurity risks

Risk management is a very interesting topic, and there are hundreds of books and certifications about this topic. However, instead of giving you a lot of overwhelming information, I will try to summarize all the available knowledge regarding risk management, tropicalize it to the cybersecurity environment, and present you with just the right information in order to manage your risks like a pro!

To make this simple, let's define a risk as an event that will have an impact on your systems or infrastructure if a given condition is met. These events are normally triggered by a threat (or a threat agent) that leverages a given vulnerability.

Now, the process of identifying and analyzing the impact and the probability of that event happening is called risk management.

All systems and infrastructures have a plurality of associated risks, so it is crucial that you identify and mitigate them as early as possible.

# Managing cybersecurity risks 61

There are many methodologies and frameworks to manage risks, and while most of them are very similar, the name of the concepts differ slightly; however I will focus on the most recognized approaches to make this easier for you.

Now, let's view the details of each of the four steps (**risk identification, risk assessment, risk response,** and **risk monitoring**) to manage your cybersecurity risks like a *master*.

# Risk identification

First, you need to *identify* the risks associated with your infrastructure or systems. Now, let me share some tips that will help you here:

- **Make a detailed and extensive inventory of your assets:** Most of the time, risks are not discovered because *ghosts* or legacy systems have not been identified, so it is key that you start by doing a thorough discovery of your assets to make sure that all your infrastructure and systems are covered.

- **The ongoing discovery of new assets:** Remember that this is an ongoing task that you need to regularly scan your environment and network to uncover any new devices that have been added to your infrastructure.

- **Asset evaluation:** A good practice is to evaluate your assets to determine which are critical for your organization (that is, your crown jewels) so that you can justify a higher investment to defend them. This will also help you in terms of prioritization and risk analysis.

> Tip Don't do this alone; ask for help

During this identification process, you will have to create a **risk register**, which is a database of all risks. There are hundreds of templates that you can use, using Excel. Just make sure you include the minimal factors, as follows:

- **Risk_ID:** The unique identifier of the risk.
- **Description:** A clear and concise description of the risk.
- **Risk_Owner:** The person who is in charge of monitoring the risk.

# Managing Threats, Vulnerabilities, Risks

- *Risk_Trigger*: The event(s) that will convert the risk into an issue.
- *Risk_Category*: To help you manage all risks, it is recommended that you create groups of risks; for example, physical access, network, software, web apps, and more.
- **Probability (Qualitative)**: Here, you can use 3 or 5 ratings (such as insignificant, low, medium, high, and critical).
- **Impact (Qualitative)**: Rate the impact to the business if the risk is materialized.
- **Response**: Describe the kind of response you implemented to reduce the probability and/or impact of risk (such as mitigate, transfer, and so on):

| Risk ID | Description | Risk Owner | Risk Category | Probability (Qualitative) | Impact (Qualitative) | Risk Response |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Unauthorized access to the data center due to lack of biometric controls. | Mikela Moter (IT) | Physical Access | Low | High | A camera placed to monitor the entrance to the data center using CCTV |

Figure 2.13 – An example of a risk register

# Risk assessment

As the name suggests, this step is about assessing the risk in terms of *probability* of occurrence and business *impact*.

There are two ways in which to do this type of assessment: qualitative and quantitative.

# Quantitative analysis

Let’s pause for a second to let me ask you a question:

If you have an asset that costs $500,000, would you invest $75,000 to protect that asset?

That is a tricky question, regardless of whether your answer is yes or no, what really matters is here that you support your answer with *numbers* as this will tell you whether you will be getting that budget or not.
