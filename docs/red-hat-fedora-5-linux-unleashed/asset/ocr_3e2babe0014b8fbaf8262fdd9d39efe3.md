+   3. Secure physical access to the server.
+   4. Create worst-case-scenario policies.
+   5. Keep up-to-date with security news.

Each of these is covered in the following sections, and each is as important as the others.

# ### Assessing Your Vulnerability

It is a common mistake for people to assume that switching on a firewall makes them safe. This is not the case and, in fact, has never been the case. Each system has distinct security needs, and taking the time to customize its security layout gives you maximum security and the best performance.

The following list summarizes the most common mistakes:

+   - **Installing every package**—Do you plan to use the machine as a DNS server? If not, why have BIND installed? Go through the Add/Remove Applications dialog and ensure that you have only the software you need.
+   - **Enabling unused services**—Do you want to administer the machine remotely? Do you want people to upload files? If not, turn off SSH and FTP because they just add needless attack vectors. This goes for many other services.
+   - **Disabling the local firewall on the grounds that you already have a firewall at the perimeter**—In security, depth is crucial. The more layers someone has to hack through, the higher the likelihood she will give up or get caught.
+   - **Letting your machine give out more information than it needs to**—Many machines are configured to give out software names and version numbers by default, which is just giving hackers a helping hand.
+   - **Placing your server in an unlocked room**—If so, you might as well just turn it off now and save the worry. The exception to this is if all the employees at your company are happy and trustworthy. But why take the risk?
+   - **Plugging your machine into a wireless network**—Unless you need wireless, avoid it, particularly if your machine is a server. Never plug a server into a wireless network because it is just too fraught with security problems.

After you have ruled out these mistakes, you are onto the real problem: Which attack vectors are open on your server? In Internet terms, this comes down to which services are Internet-facing and which ports they are running on.

Two tools are often used to determine your vulnerabilities: Nmap and Nessus. Nessus scans your machine, queries the services running, checks their version numbers against its list of vulnerabilities, and reports problems.