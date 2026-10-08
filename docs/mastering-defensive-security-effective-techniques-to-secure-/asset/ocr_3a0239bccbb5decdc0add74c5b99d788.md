+   Regularly check the CVE site to determine whether any of your systems are impacted by a newly discovered XSS vulnerability: https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=xss.

Now, let's talk about one of the best tools used to test vulnerabilities on web applications:
Burp Suite!

# Using Burp Suite

Burp Suite is a great platform that allows us to look for vulnerabilities in our web applications. In fact, if you have web applications, you must have at least one person trained to use Burp Suite to test the security of your web applications.

But don't worry if you don't have any experience with this tool—this section is for you!

Here, you will learn how to set up Burp Suite to be ready for the next sections, in which you will see how to use Burp Suite and DVWA to test a web application against two very common attacks: SQL injection and brute-force attacks.

# Burp Suite versions

Let's start talking about the three main versions of the tool (but to make it easier, we will separate it into two—the free and the paid versions).

# Professional and Enterprise editions

These versions come with more advanced tools, plus you can leverage them during your web application testing. Additionally, they also come with automation settings, which may be essential for large companies or corporations.

# Community edition

This is a basic version of the tool that is included on Kali Linux by default.

With this version, you can perform many tests with the limitation that tests cannot be automated (they all have to be manually executed) but is good enough for medium-to-small companies.

But that is enough theory, so, if you want to know more about the details of each version and its price, visit their site at https://portswigger.net/burp.