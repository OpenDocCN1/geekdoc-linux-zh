# Enhancing Your Network Defensive Skills

> Tip
By default, Nmap scans 1,000 ports, but you can increase, decrease, or specify that number by using parameters as -F (fast scan of fewer ports), -p (to specify the ports to scan), or -r (to scan all ports in consecutive order).

There are many more parameters that you can use with nmap. To explore them, simply type the following:

```
nmap --help
```

But there is more! nmap supports scripts created by the community to augment their capabilities, as explained in the next section.

# Nmap scripts

Let's review some of the best nmap scripts that you can leverage in defensive security.

# vulners

This script will make your life easier. It will provide you with Common Vulnerabilities and Exposures (CVEs) related to the open ports, services, and versions found in an Nmap scan.

> What is a CVE?
In Chapter 2, Managing Threats, Vulnerabilities, and Risks, we talked about one of the best places to find vulnerabilities: the CVE site at https://cve.mitre.org/.

The magical script is called vulners and can be found on the following link: https://github.com/vulnersCom/nmap-vulners.

This script is loaded by default into the standard Nmap Scripting Engine (NSE) library, so there is no need to install it.

The command structure is very simple, so let's explain it:

```
nmap -sV --script vulners [--script-args mincvss=<arg_val>] <target>
```

First, we have the standard nmap command, then we use the -sV parameter because the script needs the version to properly gather the CVE.

Then we call the CVE by using the --script {script_name} parameter.