# 410 PART 3 Building a Layered Linux Security Strategy

# Nessus

Even though the code for Nessus is no longer released under open source licenses, it is number one on the http://sectools.org/ list of top-100 security tools. The company behind the Nessus user interface (UI) is Tenable Security, which calls Nessus “the Network Vulnerability Scanner." With all other IDS such as Snort, the value comes with the professional fee, which includes information on all current security issues.

When installed, Nessus configuration and command files can be found in the /opt/nessus/ directory. To set up secure communication to the Nessus UI via a Web browser, you'll need to set a certificate authority. The simplest method is the nessus-mkcert script in the /opt/nessus/bin/ directory. You'll be prompted for basic information associated with a self-signed certificate.

Once this is configured, you can access the Nessus UI through a Web browser. Just navigate to the hostname or IP address of the machine with Nessus installed over HTTPS and port 8834. For example, on a system with IP address 10.192.168.100, you'd navigate to the:

```
https://10.192.168.100:8834/
```

But logins require an appropriate username and password. The Nessus database is different from any standard Linux authentication database. To create a Nessus user,

![](bbox=[0.065, 0.375, 0.935, 0.855])

FIGURE 13-8 An excerpt from a Nessus report.