
# Overviews the most common attacks on web applications

- Use session_regenerate_id() every time you provide any important data (this will delete the old session number and generate a new one).
- Save in $SESSION some fingerprinting about the user (such as IP address, browser-agent, and so on). Then, you can correlate that every cookie is received and if there is a mismatch, then you know something is not good.
- Use an SSL certificate to encrypt your data in transit.
- Educate your users to always log out instead of just closing the browser when using your web applications.
- Use timeout to kill idle sessions (expire sessions).
- Keep session Identifiers (IDs) out of the Uniform Resource Locator (URL).
- Avoid reuse of session IDs for authentication.
- Flag session ID cookies as HTTPOnly.
- Request reauthentication when accessing a sensitive resource in your web application.

It is also important to highlight that there are many other known XSS attacks, such as the following:

- Execution of unauthorized activities
- Phishing
- Capturing keystrokes
- Capturing sensitive information

Now, let's overview some additional tips that you can leverage to better protect your web applications against XSS attacks.

# Additional mitigation steps against XSS attacks

Here is a list of some best practices that can be used to reduce the risk of being impacted by an XSS attack:

- Keep your web application up to date with security updates.
- Sanitize inputs.
- Rest JavaScript entries on input fields (input validation).
- Ensure that all third-party modules of your web application are also up to date.
- Regularly check the CVE site to determine whether any of your systems are impacted by a newly discovered XSS vulnerability: https://cve.mitre.org/cgi-bin/cvekey.cgi?keyword=xss.

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

Now, let's briefly explore the interface of the Community version of Burp Suite on Kali Linux before we jump into some real case scenarios that you can execute yourself of the most common testing operations for web applications, including SQL injections and brute-force attacks; but first, let's get familiar with the tool.

# Setting up Burp Suite on Kali

To execute Burp Suite on Kali, just open the command line and type the following command:

```bash
burpsuite
```

If it is the first time you have used Burp Suite, you need to read and accept the terms, and then you will be to see the interface of Burp Suite.

Wait—did you get an error about the Java Runtime Environment (JRE)?

No worries—this is a known error when you launch Burp Community for the first time, and it is related to the version of the JRE installed on your OS, as you can just bypass the message to launch Burp:

![](img/8c6a223c57e25ea0cc1593903a1b920f_373_png)
Figure 12.13 – JRE error when executing Burp Suite

On the free version, the only available option is to select Temporary Project, so let's click there and select default options to finally access the Graphical Interface (GUI).

Congratulations! Now you should be able to see the main interface of Burp Community, as shown in the following:

![](img/8c6a223c57e25ea0cc1593903a1b920f_374_png)
Figure 12.14 – Burp Suite Community

You have the environment ready to start doing, so let's move on to see how you can use Burp Suite and DVWA to test your web applications using SQL injection attacks.

# SQL injection attack on DVWA

For this demo, we use Kali Linux, two tools we set up: Burp Suite and DVWA.

Tip: If you reboot the machine, you need to start the services required for DVWA again and restart your browser using the following commands:

```bash
sudo service apache2 start
sudo service mysql start
```

One of the cool features of DVWA is that you can customize the difficulty of the attack (security levels). Here is a quick explanation about each of them:

- **Low**: The computer is super vulnerable, and it has no security measures at all.
- **Medium**: Intended to be simulation of a web application without good practices.
- **High**: This is extension of the previous level, in which exploitation is harder to achieve.
- **Impossible**: This is simulation of machine with all the best practices applied.

In the case of SQL attacks, the **Low** security level shows you a text field in which you can easily insert a direct SQL injection, as shown in the following:

![](img/8c6a223c57e25ea0cc1593903a1b920f_375_png)
Figure 12.15 – DVWA low security level: SQL injection

However, for our example, we will take it to the next level and we will use the **Medium** security level in which, instead of a static text field, we will only see a drop-down menu. Therefore, to accomplish this security test, we are going to need an extra tool to inject SQL. Let's see step-by-step instructions to perform this security test of SQL injection, as follows:

1. Open Burp Suite and create a temporary project using Burp defaults.
2. From the main top menu, select **Proxy**, and from the submenu, select **Intercept**.
3. Then, select the **Open Burp Browser** option.
4. Using the Burp browser, open DVWA and go to the left menu and click on **Security**, on the dropdown, select Medium and click on Submit, as shown in the following:

![](img/8c6a223c57e25ea0cc1593903a1b920f_376_0.png)
Figure 12.16 – Changing the security level in DVWA
5. Now, go to SQL Injection on the left menu, and there, you should see a drop-down menu with a Submit button, as shown in the following:

![](img/8c6a223c57e25ea0cc1593903a1b920f_376_1.png)
Figure 12.17 – SQL injection on the medium security level

Go back to Burp Suite and click on Intercept to turn it off, as seen in the following:

![](img/8c6a223c57e25ea0cc1593903a1b920f_377_0.png)
Figure 12.18 – Turning on Intercept in Burp Suite

Go back to DVWA, and click on Submit (as seen in Figure 12.17). If you go back to Burp Suite, you should be able to see the intercepted data, as seen in the following:

![](img/8c6a223c57e25ea0cc1593903a1b920f_377_1.png)
Figure 12.19 – Data captured by Burp Suite

9. As seen at the end of Figure 12.19, the value that we selected on the dropdown was sent as id=1, so let's play around with that number to see how we secure this web application.
10. Let's change the value of id from 1 to 2 on Burp Suite and then click on Forward to see what happens.
11. If you go back to DVWA, you will see that the dropdown is still showing User ID 1; however, the information of User ID 2 is being displayed. This means Burp Suite was able to successfully inject a new value without touching the web page, as illustrated in the following screenshot:

![](img/8c6a223c57e25ea0cc1593903a1b920f_378_0.png)

12. But that was just a test. Now that we see we can inject data, let's try to do a real SQL injection. To do this, let's change the value of User ID to see what we can achieve with different values. Let's go back to Burp Suite and make sure that Intercept is ON and then click on Submit on DVWA to get the data on Burp Suite.
13. Now, Burp Suite should display the same information as shown in Figure 12.20. Here, let's go back to the road and change the value of ID from 1 to 1 OR 1=1# and click on Forward.
14. As you can see in the screenshot, the web page in DVWA is now displaying the information from all five users at the same time, even when there is no option to do that. This means that we just discovered a security flaw! Here it is:
