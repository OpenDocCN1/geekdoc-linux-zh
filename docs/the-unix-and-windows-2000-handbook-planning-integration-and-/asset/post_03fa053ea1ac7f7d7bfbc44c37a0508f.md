
break into the IT system. Such actions can have a direct effect on the protection and detection components.

**Detection** is any action whose goal is to detect an intrusion and track down the opponent with the intent to prosecute.

**Recovery** corresponds to the action to take when it is too late and how to recover when you have lost the race and have become the victim of an intrusion. Good methods and a minimum of action in the three areas of protection + prevention + detection are likely to protect your organization from 90-95% of all possible intrusions. However it is important not to neglect the last 5% as these are generally the most dangerous. The final 5% are those types of attacks that can only be attempted by an intruder with a high level of knowledge, and with that increased knowledge, the amount of potential damage an intruder can inflict also increases.

Before going further into this journey, here are some thoughts that you may want to keep in mind while working with security:

The security of an IT system can be addressed from a technical point of view (patching security holes, restricting access), but overall it has to be defined by a policy. The policy must define what a user can/cannot do inside the IT system (for example, what system(s) they cannot access, what commands they can execute, etc.).

An analogy can be established between the concepts of quality and security of an IT system. Security represents a cost (loss) for the organization. Enforcing a security policy requires time and dedicated means, and it can have an indirect impact on productivity (users may have to follow some rules which may slow them down in their use of the IT system). But, not doing security can lead to greater costs, as will be explained later.

The system administrator, when working on security, has to be paranoid by nature. Security is a way of life, and must be present in every action done by the system administrator. Doing something (like setting up a server) without paying attention to security or saying, “I have no time right now, I will secure the system later.” is wrong, as “later” may become “too late”.

## Know Your Opponents and Types of Attacks

As generally stated by the military: The preparation of a good defense requires good knowledge of the opponent.

## WHO IS THE INTRUDER?

Before going further, it is important to understand the jargon and slang used on the “dark side” of system administration. Speaking your enemy’s language is the first step to understanding how they think. A good starting point is:

```
http://packetstorm.securify.com/docs/hack/jargon-4.1.2/jargon.html
```

Intruders can be classified from a defacto point of view into two main categories: outsiders and insiders.

### Insiders

A statistic that is frequently quoted by security vendors and in articles is the rule of 80%-20%. It means that 80% of the intrusion attempts come from inside the organization, with the remaining 20% coming from outside the organization. Insiders can be:

- Angry employees seeking revenge.
- Employees trying to benefit by stealing private information and selling it or using it to their advantage.

Insiders break into IT systems through:

- **Physical intrusion**—They take advantage of special privileges that access to the physical console of the system can offer. For example, they reboot the system into single-user mode or from installation media in order to access data thereby bypassing the normal access control list. A physical intrusion can also include removing the hard drive from a system to read/write it more easily from another machine.
- **System intrusion**—The intruder uses existing low-privilege access and tries, by exploiting a security hole or by taking advantage of a system misconfiguration, to gain additional administrative privileges.

### Outsiders

Outsiders try to break into your system remotely, from outside the network that is part of your infrastructure. It is possible to classify outsiders into four main categories:

- **Script kiddies**—Script kiddies are considered the least dangerous of the outsiders. They are generally teenagers, out to explore and
