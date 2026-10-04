# Attacking and Defending Windows XP Professional • Chapter 4

The three IP security policy objects included by default are as follows:

+   - Client (Respond Only)
- Secure Server (Require Security)
- Server (Request Security)

In general, you should only generate permanent IPSec rulesets for static systems that you communicate with on a frequent basis. There are a few scenarios for which you may want to set up secure communication streams:

+   - You want to secure communications between your workstation and network devices.
- You want to secure communications between you and a peer workstation.
- You want to secure communications between you and a system on sporadic times.

Installing these rulesets for any of these scenarios would be quite simple. The following guidelines will walk you through the steps you would need to take to create any of the given IPSec rulesets. After you have created your ruleset, you will be ready to implement the ruleset on your system for future communications on your system.

+   1. Double-click on the Secure Server (Require Security) object.
2. Select the Route Creation Wizard.
3. Click Add to create a new rule then click Next to proceed.
4. Click the radio button that says “This tunnel is specified by your IP address” and then enter the IP address of the desired system.
5. Click the Local Area Network (LAN) button and then proceed to the authentication specification box. You can choose whichever authentication schema you desire but ensure that if you select the preshared secret key schema, it is a long and nondictionary-based phrase.
6. Click the All IP Traffic button then click Next.
7. Click the Secure Server (Require Security) button and then click Next again.

![](bbox=[0.71, 0.942, 0.928, 0.966])