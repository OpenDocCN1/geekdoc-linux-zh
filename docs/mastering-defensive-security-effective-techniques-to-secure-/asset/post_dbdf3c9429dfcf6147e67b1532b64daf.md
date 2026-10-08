
42 Managing Threats, Vulnerabilities, and Risks

## User vulnerabilities

Users are one of the most vulnerable factors in any organization and there are many reasons for this; for instance, you can have users who use a weak password, users who use the same passwords in all systems (both personal and professional), and users who leave unlocked systems unattended. The list goes on.

However, this is very complex, so we will be addressing this vulnerability in more detail, including how you can protect against it, in Chapter 4, Patching Layer 8.

## Physical vulnerabilities

As if you don't have enough to take care of, you also need to check for vulnerabilities related to the building or campus where your systems are located. For example, you need to make sure that the building is not vulnerable to a given weather condition, which could disrupt your systems (such as flooding or water leaks). Additionally, you also need to evaluate the vulnerabilities related to your physical access systems; we will cover that in more detail in Chapter 9, Deep Diving into Physical Security.

## Web vulnerabilities

It is imperative that you check your web-facing devices and systems to see what others see and find any vulnerability that you can patch before someone exploits it. There are several ways to find web vulnerabilities, and we will explore more of them this book. One simple method that you can leverage to check your web resources are exposed the **Google Hacking Database** (GHDB). This is a compilation of Google search keys (known as dorks) that enable you to leverage the Google search engine to discover exposed documents and information on websites and devices connected to the internet indexed by Google.

There are thousands of possible dorks that you can use to find vulnerabilities in your web resources, which could expose sensitive information such as usernames, passwords, directories, config files, tables, databases, documents, and more.

> Do you want to learn more about the GHDB?
> this page, you can find more than 5,000 dorks ready for you to use. I am sure you will be shocked by what you find here: https://www.exploit-db.com/google-hacking-database.

There is a super cool application, called **Damn Vulnerable Web Application** (DWWA), that you can use to see and explore web vulnerabilities in a controlled environment. If you want to know more about this great application, jump to Chapter 12, Mastering Web App Security.

## IoT vulnerabilities

IoT is a booming technology and almost all companies have some type of IoT implementation in their infrastructure. Therefore, it is very important that you analyze IoT implementation to check for vulnerabilities.

Sometimes, those devices are installed without the authorization of the security team, and the main risk is when they are left with default credentials. So, make sure all IoT implementation (even if it's just some gadgets) are properly configured.

There are several websites that crawl the internet to look for vulnerable web pages. You can find a variety of sites that vary from pages that scan the internet for webcams with default passwords (such as www.insec.com) to more robust pages that scan several ports to find vulnerable systems.

One of the best websites to do that is shodan.io. This search engine allows you to find vulnerabilities on websites, IoT devices, webcams, databases, industrial control systems (ICS), routers, network devices, and more. With a quick search, you will be impressed by the huge number of devices with default credentials on the web:

![](img/8c6a223c57e25ea0cc1593903a1b920f_65_0.png)

Figure 2.3 – Shodan's search categories

As you can see, in Figure 2.2, you can even search by categories on Shodan.io to find vulnerable devices, cams, Databases, and even ICS systems (we will review them in more detail in the following section).

## Managing Threats, Vulnerabilities, and Risks

> Tip
> You can use Shodan.io to look for vulnerabilities on your sites, systems, and devices exposed to the internet. The search engine allows you to look by URL, IP address, subnet, type of device, country, and more.

I will expand this topic with many examples (including how to leverage IoT-enabled devices for security) in Chapter 10, Applying IoT Security.

## Vulnerabilities on SCADA/ICS

If your company does any type of manufacturing; has a smart building; uses smart systems to manage energy, waste, and water; or is in the business of smart cities, it is very possible that they have SCADA systems.

Those systems are critical, and you need to ensure that they are protected as the impact of an attack on these systems is usually devastating for the company. One good example of the impact of this type of attack is Stuxnet. This state-backed attack was able to disrupt a nuclear power plant by targeting its SCADA systems.

These systems are very complex, and depending on the vendor, they can be very different from each other, making the task of securing them quite complex. However, there are some steps or best practices you can apply to secure these systems:

- If possible, schedule maintenance services performed by the vendor, and make sure those services include a vulnerability assessment.
- Keep the devices up to date with the latest updates.
- Understand the protocols used by the system and look for associated vulnerabilities.
- Delete or disable users on the systems.
- Disable the features that are not in use by your organization to reduce the number of risks and possible vulnerabilities.
- Avoid the use of third-party plugins if not approved by the vendor.
- Disable remote access connections or mobile applications if not in use.
- Disable unused APIs.
- Apply network segmentation and isolate those devices from other web-facing systems.
- Restrict physical access to the management consoles of the devices.
- Make sure that all default users and passwords are changed for strong credentials.

## Understanding cybersecurity vulnerabilities and threats 45

If your organization does not have any experience with these systems, the best practice is to hire a third-party company to either provide your team with training on how to secure those systems or have a contract with them in order to keep those systems secure.

## Supplier vulnerabilities

Remember that the availability of your systems relies on your suppliers, so you need to analyze them to uncover any possible vulnerabilities associated with those suppliers (such as the internet provider, cloud provider, hardware provider, and more).

## Client vulnerabilities

There there be cases in which you will have to connect your systems to the network or infrastructure of a partner; in those cases, you need to perform a detailed vulnerability assessment of those foreign systems to ensure they do not add additional vulnerabilities to your infrastructure.

## Dependencies

One important aspect to consider when doing a vulnerability assessment is identifying your system or infrastructure dependencies and then analyzing those dependencies to uncover any potential vulnerabilities. One clear example of this is a system that might consume artificial intelligence (such as a chatbot) through an API connection that, if down, will not work properly or can be spoofed.

## Process vulnerabilities

Imagine that your company does not have a process regarding what to do when an employee leaves the company. In this scenario, one system administrator might just disable the user (which creates a residual risk), while another might delete the user (which could be a problem because you leave no traceability to that user). Therefore, both scenarios could cause a problem. This is why, incomplete, or poorly designed Identity and Access Management process is, itself, a big vulnerability.

> **Tip**
Starting a vulnerability assessment is probably the hardest part of the process because you might not know where to start. Here, my recommendation will be to first outline the vulnerability types as categories and then start looking for vulnerabilities in those areas. That will serve you as a starting point, but it will also help you to avoid leaving an entire category unassessed.
