
120 Patching Layer 8

Also, there are many systems that automate the analysis of logs. So, instead of giving you some brands and names, I am going to show you the type of tools that will help you to achieve this, so you can search and find the solution that bet your organization. Additionally, I would suggest you look for alternatives that leverage machine learning algorithms in order to improve detection and reduce false positives.

The systems are as follows:

- Behavior analytics systems
- Threat intelligence
- Anomaly detection
- Predictive alerts

However, I want to know that not having those systems is not an excuse to waste your valuable data. In fact, I remember a very interesting scenario in which, by analyzing several logs, we found a system administrator that was illegally using corporate assets to *mine* bitcoins.

## How did we find it?

By checking the logs, we discovered that several systems and non-production servers were normally turned on from 10 pm until 4 am with the sole purpose of mining bitcoins. Additionally, those logs contained the level of detail required to *identify the users involved* but also the evidence required to *pursue the associated penalties and sanctions against them.**

## Alerts

Another great way to identify a malicious insider is by setting up monitors to give you alerts when a cybersecurity system is disabled.

This is especially useful in those companies that give administrative rights to all the *employees* because they think they can bypass the security mechanisms (such as disabling the antivirus software or a firewall); however, what they dont know is that you are already one ahead.

> Important note
> There are several ways in which to prevent a user from disabling some security features: however, not all companies or IT departments have the tools, knowledge, or interest in doing so, and that is why it is important for you to learn how to deal with these scenarios.

## Understanding layer 8 – the insider threat 121

Now, let's take a look at one example of a very common practice in IT departments, which is a really bad practice for security.

## Shared credentials

By default, the best practice says that shared credentials should NOT be allowed in your infrastructure. However, in case you do have them, you need to set up additional controls in place such as Multifactor Authentication (MFA), Role-Based Access Control (RBAC), and Privileged Access Management (PAM).

PAM works by locking shared credentials into a repository that can only be accessed by authenticated employee accounts (enabling accountability). The credential is used by the system administrator, the credential is reset for the next employee. Although PAM solves the challenge of shared accounts, it is very expensive to implement:

![](img/8c6a223c57e25ea0cc1593903a1b920f_143_0.png)

Figure 4.7 – An example of a PAM system

The preceding diagram is an example of a PAM system and shows how each user logs into a centralized system (to enable accountability), and then from there, inject the shared account into the server.

## Audits

This topic was already covered in detail in Chapter 3, Comprehending Policies, Procedures, Compliance, and Audits; however, I want to highlight that audits are one of the most effective ways to detect malicious insiders, so make sure your infrastructure is audited regularly (either internally or externally).

## Cybersecurity policies

As discussed in Chapter 3, Comprehending Policies, Procedures, Compliance, and Audits, policies need to be well defined and communicated. Additionally, those policies must include the associated sanctions in case there are any violations of them. Those sanctions are a great mechanism to dissuade malicious insiders, and why it is so important to make sure that all employees are aware of your cybersecurity policies.

We already talked about two types of insiders: the inadvertent users and the malicious insiders. In this attack, an outsider will use the power of influence and psychological manipulation to convince or persuade an employee to perform a set of actions aimed to disrupt the systems or gather/modify sensitive data. This technique is known as Social Engineering, which we will be discussing next.

## Mastering the art of social engineering

Social engineering is one of the most fascinating topics in security. In fact, many experts define social engineering as an art: an art that requires a lot of social skills that enables the attackers to gain access to the victim's mind to gather personal information or even persuade the victim to perform certain actions that will benefit the attacker.

This is like hacking into the human brain to read the user's data or inject instructions for the human to perform.

As I mentioned earlier, this is a very exciting and important topic, so I will try to summarize it as much as I can.

> Important note
> As a professional in defensive security, you must master this topic because the better you understand how this works, the better you can defend against it.

Next, let's take a look at the attacks that are aimed to trick the user. Additionally, keep in mind that while not all authors agree on classifying these attacks as types of social engineering, the truth is that these attacks share the same concepts and strategies as social engineering attacks.

## The social engineering cycle

There are many techniques that attackers can use to perform a social engineering attack, but they need to be orchestrated, as follows, to improve the efficiency of the attack:

1. **Information gathering**: First, the attacker will gather as much information as possible about the target individual or organization. The more the attacker knows about the organization, the higher the chances to succeed. For example, an attacker would be very interested in knowing the organizational structure, the processes, and procedures for the next steps.
2. **Building trust**: Here, the attacker will use the data gathered plus a combination of social techniques to gain trust. In more elaborate attacks, the attacker will need to gain trust from a plurality of individuals to bypass additional security layers before reaching the target or victim.

As you can see in the following screenshot, the attacker might also leverage some technical knowledge to gain the trust of the victim. For example, the attacker might impersonate an IT person by telling the user that their computer was infected by a virus and ask the user to check whether the svhost Windows process is presented on the Task Manager:

![](img/8c6a223c57e25ea0cc1593903a1b920f_145_0.png)

Figure 4.8 – SVCHOST running on Windows

Of course, the attacker knows that such a process will be **always** there, and when the user finds it, it will be a way to legitimate the attacker, gaining full trust and opening the **door** for the next step.

3. **Influencing the victim**: Having gained the trust of the user, the attacker can manipulate the victim to either provide some confidential information (such as usernames and passwords) or to perform some actions (such as resetting a password, opening a terminal, opening a web page).

4. **Executing the attack**: By now, the attacker might have valid credentials, full remote control of the computer, and many other paths in which to execute their final attack (such as deleting, modifying, or copying confidential data, accessing a given system, and more).

5. **Erasing tracks**: Once the attack is completed, the attacker may want to cover their tracks to avoid detection and prosecution, but also to retain access to the systems and data for a longer period of time:

![](img/8c6a223c57e25ea0cc1593903a1b920f_146_0.png)

Now, let's take a quick look at some of the techniques used by attackers to successfully launch a social engineering attack.

## Social engineering techniques

Here are few techniques that an attacker can use to launch a social engineering attack:

- Impersonation: One of the most common techniques used by attackers is to present themselves as someone else; for example, as someone with authority, someone with power, or someone representing a reputable company or group.

This is normally used to gain trust from the victim in order to either gain information or to make the victim execute a given action.

Some of the most common impersonations are impersonating an IT person, a government representative, a bank employee, or a reputable business.
