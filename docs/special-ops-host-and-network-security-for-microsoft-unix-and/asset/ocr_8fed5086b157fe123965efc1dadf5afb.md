# Attacking and Defending Unix • Chapter 14

# Figure 14.4 Checklist of Information to Gather when Planning a Secure Server

| Monitoring Software | Analog, HP OpenView |
| :--- | :--- |
| Availability Needs | 24/7 with SLA |
| Number Of Users | 10 |
| Type Of Network Router | Cisco |
| Required Services | smtp, sshd, pop3 |
| Public Or Private Host | Public |
| Access Limitations | Shd for admin only |
| Untrusted User Access | Yes |

# Gathering Relevant Information

Having enough information to adequately plan a server is critical. However, in the quest to gather enough information it is easy to inadvertently irrelevant information. In doing so, you populate your notes with details that are confusing, conflicting, and can result in misinformation.

Preventing this type of situation can be tricky. In concept, as more information and details are gathered to create the model of your target system, flexibility is lost as the possible configurations narrow. The goal is to gather information that will allow you to implement a secure system with a minimal sacrifice of flexibility.

When sufficient details have been gathered, conduct a final review of the details list. This primarily ensures that no significant details have been overlooked. Also, this ensures that irrelevant details included in the list are identified and eliminated. Figure 14.5 shows our modified checklist; portions that have been deemed irrelevant have been crossed out.

In our example, we removed a few items from the list. First, we removed the neighbor servers because of the impact of these systems on the host. These systems may not interact with the host in the future. Additionally, boring systems may change, making information in the original design document irrelevant. Our goal is to keep information that is pertinent to the host, and will remain throughout the life of the system. We performed the same elimination with the Type Of Network Router field.

![](bbox=[0.707, 0.943, 0.927, 0.966])