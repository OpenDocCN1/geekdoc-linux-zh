
```bash
kali@kali:$ sudo hydra -L /usr/share/wordlists/dirb/others/names.txt -p
"SuperS3cure1337#" rdp:192.168.50.202

[DATA] 4 tasks per server, overall 4 tasks, 14344399 login tries
(l:14344399/p1), 3586099.7 tries per task
[DATA] attacking rdp://192.168.50.202:3389;

[3389][rdp] host: 192.168.50.202 login: daniel password: SuperS3cure1337#
[ERROR] freedp: The connection failed to establish.
[3389][rdp] host: 192.168.50.202 login: justin password: SuperS3cure1337#
[ERROR] freedp: The connection failed to establish.
```

List 256 - Spraying a password on RDP service

Due to the size of the selected list, the password attack will take around 15 minutes to discover the two valid credentials. While following along, we can reduce this time by creating a list that only contains two lines, "daniel" and "justin"

In this case, we identified two usernames with the password discovered in the database leak. We should always try to leverage every plaintext password by discovering them against the target's systems. This could reveal users that use the same password across multiple systems. However we must use caution when leveraging broad-range attacks.

Dictionary attacks generate a lot of noise in terms of logs, events, and traffic. While a huge mount of network traffic can bring down a network, the reactions of various securityologies could be even more undesirable. As a basic brute force protection program could lock a user's account after three failed login attempts. In a real-world test, this could lead to a situation where we lock users out of critical production systems. Before launching tools, we must perform a thorough enumeration to identify and avoid these risks.

In this section, we performed dictionary attacks on the common SSH and RDP network services. While Hydra makes the process straightforward for most protocols, some protocols require more information. We will explore this with HTTP login forms in the next section.

Before we head into the first exercises of this Module, we need to be aware that the process of attacking a target shouldn't take longer than three minutes in the exercises or challenge lasts. If the process takes longer, you should double-check your command and arguments or try a different approach.

# 13.1.2 HTTP Login Form

In most internal and external attacks, we will face a web service. Depending on the service, may not be able to access it until we log into it. If this is only our vector and we are able to use default credentials to log in, we should consider using a dictionary attack to gain access.

Most web services come with a default user account, such as admin. This known username for our dictionary attack will dramatically increase our chances of success and reduce the expected duration of our attack.

In this section, we will perform a dictionary attack on the login form of the TinyFileManager¹⁶⁰² application, which is running on port 80 on the BRUTE web server. Let's browse to the login page.

![](img/336d6ea891e7464f18ad64426619ced4_383_0.png)

Figure 209: Login page of TinyFileManager

After reading the application's documentation, we discover TinyFileManager includes two default users: admin and user. After trying and failing to log in with the application's credentials,³ we will attack the password of user with the rockyou.out word.

Attacking an HTTP POST login form with Hydra is not straightforward as attacking SSH or RDP. We first gather two pieces of information. The first is the POST data itself, which contains the request body specifying the username and password. Second, we capture a failed login attempt to help Hydra differentiate between a successful and a failed login.

We'll use Burp⁴ to intercept a login attempt so we can grab the request body in the POST data. To do this, we'll first start Burp and activate intercept. Next, in our browser, we'll enter a username of user and password into the login form. The following figure shows the intercepted request for the login attempt.

![](img/336d6ea891e7464f18ad64426619ced4_383_1.png)

Figure 210: Intercepted Request

The highlighted area shows the request body we need to provide for Hydra in the POST request.

> ¹⁶⁰ (Github, 2022), https://github.com/pramasathmani/tinyfilemanager
⁶³ (Github, 2022), https://tinyfilemanager.github.io/docs/
⁶⁴ (PortSwigger, 2022), https://portswigger.net/burp

PWK - 2023 OffSec Services Limited. All rights reserved.

Next, we need to identify a failed login attempt. The simplest way to do this is to forward the request or turn intercept off and check the login form in the browser. The following figure shows that a message appeared, which informs us that our login failed.

![](img/336d6ea891e7464f18ad64426619ced4_384_0.png)

The highlighted text appears after a failed login attempt. We will provide this text to Hydra as a failed login identifier.

> In more complex web applications, we may need to dig deeper into the request and response or even inspect the source code of the login form to isolate a failed login indicator, but this is out of the scope of this Module.

We can assemble the pieces to start our Hydra attack. As before, we will specify -l for the wordlist, the target IP without any protocol, and a new http-post-form argument, which accepts three colon-delimited fields.

The first field indicates the location of the login. In this demonstration, the login form is located on the index.php web page. The second field specifies the request used for providing a username and password to the login form, which we retrieved with Burp. Finally we must provide the failed login identifier, also known as a condition string.

Before we provide the arguments to Hydra and launch the attack, we should understand that the condition string is searched for within the response of the web application to determine if a login is successful or not. To reduce false positives, we should always try to avoid keywords such as password or username. To do so, we shorten the condition string appropriately.

The complete command with the shortened condition string is shown below. After executing the command, we will wait a few moments for Hydra to identify a valid set of credentials.

# OffSec Penetration Testing with Kali Linux

```bash
kali:~$ sudo hydra -P /usr/share/wordlists/rockyou.txt 192.168.50.201
http-post-form "index.php?fm_user=user&pwd=PASS^Login failed. Invalid"

[DATA] 16 tasks per server, overall 16 tasks, 1434339 login tries
(1:1/1434339) - 89646.2 tries per task
[DATA] attacking http-post-
/192.168.50.201:index.php?fm_user=user&pwd=PASS^Login failed. Invalid
username or password
[STATUS] 64.00/min, 64 tasks in 00:01h, 143435 to do in 3735:31, 16 active
[80][http-post-form] host: 192.168.50.201 login: user password:12122
of 1 target successfully completed, 1 valid password found
```

Listing 257 - Successful Dictionary Attack on the Login Form

In this case, our dictionary attack was successful and we identified a valid password (12122) for our user. Let's try to log in to confirm the credentials.

![](img/336d6ea891e7464f18ad64426619ced4_385_0.png)

According to the output in Figure 22, we logged in. Nice!

With any dictionary attack, this generates a lot of noise and many enemies. If installed, a Web Application Firewall (WAF)⁶⁵ would block this activity quickly. Other brute force protection applications could also block this, as fail2ban⁶⁶ locks a user out after a set number of failed login attempts. However, servers aren't afforded this type of protection, making this a highly effective vector against those targets.

In general, dictionary attacks can be quite effective, especially if we begin with some type of known information and balance our attack in consideration of potential defense mechanisms.

# 13.2 Password Cracking Fundamentals

This Learning Unit covers the following Learning Objectives:

- Understand the fundamentals of password cracking
- Mutate words
- Explain the basic password cracking methodology
- Attack password manager key files

> ⁶⁵ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Web_application_firewall
⁶⁶ (Fail2Ban, 2022), https://www.fail2ban.org/wiki/index.php/Main:Page
