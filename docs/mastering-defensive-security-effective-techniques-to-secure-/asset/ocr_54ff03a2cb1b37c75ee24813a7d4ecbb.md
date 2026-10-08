# IoT vulnerabilities

IoT is a booming technology and almost all companies have some type of IoT implementation in their infrastructure. Therefore, it is very important that you analyze IoT implementation to check for vulnerabilities.

Sometimes, those devices are installed without the authorization of the security team, and the main risk is when they are left with default credentials. So, make sure all IoT implementation (even if it's just some gadgets) are properly configured.

There are several websites that crawl the internet to look for vulnerable web pages. You can find a variety of sites that vary from pages that scan the internet for webc with default passwords (such as www.insec.com) to more robust pages that scan several ports to find vulnerable systems.

One of the best websites to do that is shodan.io. This search engine allows you to find vulnerabilities on websites, IoT devices, webcams, databases, industrial control systems (ICS), routers, network devices, and more. With a quick search, you will be impressed by the huge number of devices with default credentials on the web:

![](bbox=[0.178, 0.442, 0.782, 0.796])

Figure 2.3 – Shodan's search categories

As you can see, in Figure 2.2, you can even search by categories on Shodan.io to find vulnerable devices, cams, Databases, and even ICS systems (we will review them in more detail in the following section).