# 110 Chapter 5 • The Hacking Top 10

about a network or a specific host. For a more in-depth explanation of the many uses of nmap, check out the man page or the Insecure homepage.⁴

# Nessus

Like nmap, nessus is a popular open source vulnerability and port scanner distributed by Tenable Network Security, and the mighty #1 on the top 100 network security tools survey!⁵ Tenable boasts “…the world leader in active scanners, featuring high speed discovery, configuration auditing, asset profiling, sensitive data discovery, and vulnerability analysis of your security posture. Nessus scanners can be distributed throughout an entire enterprise, inside demilitarized zones (DMZs), and across physically separate networks.

Nessus has been around since 1998. It has a Ness GUI, powerful plug-in options, and offers the ability to export its results in a variety of formats including easy-to-read Hypertext Markup Language (HTML) pages. It is used by penetration testers and network security professionals all over the world in their ongoing efforts to identify and eliminate possible attack vectors.

Nessus is a client/server model which can run via a remote server, or completely locally. Once the nessus daemon has been started, the Nessus GUI can be launched and the scanner can be used. By default, nessus installs into /usr/bin with a block size of 418200 (version 2.2.9), however, some of additional binaries are also placed in /usr/sbin.

Although Nessus is meant for security professionals to be able to identify exposures in their systems, it can be used by hackers for the same reason. Like with nmap, the goal is the same; find what is vulnerable and exploit it. Nessus does a very good job at identifying OSes, processes, ports, and various configuration settings. This is not all that different from nmap. The main difference is that Nessus will actually try and enumerate information such as passwords, URL strings, and certain configuration information from the target system. In addition, Nessus will provide you with references to various vulnerability sites that explain the issue in greater detail.

Below is an example of a scan I ran against my local Apache Web server. As you can see, not only does Nessus pick up that I was running Apache on port 8080, but it was also able to successfully enumerate that the /software directory was found. This

⁴ www.insecure.org
⁵ www.nessus.org/nessus/

![](bbox=[0.042, 0.947, 0.263, 0.977])