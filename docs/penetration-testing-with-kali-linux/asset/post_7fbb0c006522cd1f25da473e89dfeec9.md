
When testing a file upload should always determine what happens when a file is uploaded twice. If the web application indicates that the file already exists, we can use this method to brute force the contents of a web server. Alternatively, if the web application displays an error message, this may provide valuable information such as the programming language or web technologies in use.

Review the test.txt upload in Burp. We find the POST request in HTTP history, send it to Repeater, and click Send.

| Request | Response |
| --- | --- |
| POST /upload HTTP/1.1 | HTTP/1.1 200 OK |
| Host: mountainserts.com:8000 | Date: 26 Apr 2022 11:46:49 GMT |
| User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:91.0) Gecko/20100101 Firefox/91 | Content-Length: 37 |
| Accept: text/html,application/xml+xml;q=0.9,image/** | Content-Type: text/plain; charset=utf-8 |
| Accept-Language: en-US,en | Connection: close |
| Accept-Encoding: gzip, deflate | |
| Content-Type: multipart/form-data; | |
| Boundary: ---17927853383372631346091296--- | Successfully uploaded file: test.txt |
| Content-Length: 229 | | |
| Origin: mountainserts.com:8000 | | |
| Connection: close | | |
| Refer: http://mountainserts.com:8000/ | | |
| Upgrade-Insecure-Requests: 1 | | |
| | ---179278533833726313460912296--- | | |
| Content-Disposition: form-data; name="file"; filename="test.txt" | | |
| Content-Type: text/plain | | |
| | this is a test | | |
| | ---179278533833726313460912296--- | | |

Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

Figure 14: Relative path in filename to upload file outside of root

# OffSec

Penetration Testing with Kali Linux

The Response area shows that the output includes the ../ sequences. Unfortunately, we have no knowing of how the relative path was used for placing the file. It's possible that the web application's response merely echoed its filename and internally. Now we assume the relative path was used for placing the file, since we cannot find any other attack vector. If our assumption is correct, we can try to overwrite files, which may lead us to system access. We should be aware, that blindly overwriting files in a real-life penetration test could result in lost data or costly downtime of a production system. Before moving forward, let's briefly review server accounts and permissions.

Web applications using Apache, Nginx or other dedicated web servers run with specific users, such as www-data on Linux. Traditionally on Windows, the IIS web server runs as a Network Service account, a passwordless built-in Windows identity with low privileges. Starting with IIS version 7.5, Microsoft introduced the IIS Pool Identities.¹³⁹ These are virtual accounts running web applications grouped by application pools.⁴⁴⁰ Each pool has its own pool identity, making it possible to set more precise permissions for running web applications.

When programming languages that can include the web server, administrators and developers often deploy the web application without any privilege structures by running applications as root or Administrator to avoid any issues. This means we should always verify whether we can leverage root or administrator privileges in a file vulnerability.

Let's try to authorize the authorized_keys file in the home directory for root. If this file contains the public key of a private key we can access the system with SSH as root user. To do this, we'll create an SSH key with ssh-keygen⁴⁴¹ as well as a file with the name authorized_keys the previously created public key.

```
kali@kali:~$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/kali/.ssh/id_rsa): fileup
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in fileup
Your public key has been saved in fileup.pub
...
```

```
kali@kali:-$ cat fileup.pub > authorized_keys
```

Listing 164 - Prepare authorized_keys file for File Upload

Now that the authorized_keys file contains our public key, we can upload it using the relative path ../../../../../rootroot/ssh/authorized_keys. We will select our authorized_keys file in the file upload form and enable intercept in Burp before we click on the Upload button. When Burp shows the intercepted request, we can modify the filename accordingly and proceed.

¹³⁹ (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/iis/configure/security/application-identities

⁴⁴⁰ (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/iis/configuration/system-applicationhost/applicationpools

⁴⁴¹ (Wikipedia, 2021), https://en.wikipedia.org/wiki/SSH-keygen

PWK - © 2023 OffSec Services Limited. All rights reserved.

# # OffSec

Penetration Testing with Kali Linux

```
HTTP WebSockets Options
Request / http://mountaindesserts.com:8080 HTTP/1.1
Host: mountaindesserts.com:8080
Action: Browser
```
```

Comment this item

```
curl -v -s -L - http://mountaindesserts.com
```
```

```
Host: mountaindesserts.com
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 1542
Connection: keep-alive
Server: Apache/2.4.41 (Ubuntu)

<html>
<body>...</body>n</html>
```

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

Figure 14: Relative path in filename to upload file outside of root

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

> Figure 14 shows the same output as we do in the browser, without any new or valuable information. Now, let's check if the web application allows us to specify a relative path in the filename and write a file in Directory Traversal outside of the root. We can do this by modifying the `filename` parameter in the request so it contains `../../../../test.txt`, then click send.

* Learn about command injection
* Understand how to leverage command injection to gain system access

# 9.4 Command Injection

Web applications need to interact with the operating system, such as when a file is created. In this Learning Unit we will explore how to identify and exploit injection vulnerabilities. We will learn about command injection, which allows us to inject commands into the command line.

## 9.4.1 OS Command Injection

Web applications need to interact with the operating system, such as when a file is created. Web applications should always offer specific APIs or functionalities that use prepared commands. However, these APIs and functions are often very time consuming to develop.

Sometimes a web application needs to address a multitude of cases, and a set of predefined functions can be too inflexible. In these cases, developers often tend to directly accept user input, then sanitize it. This means that user input is filtered for any command sequences that might trigger the change of behavior for malicious purposes.

For this demonstration, let's review the "Mountain Vaults" web application, running on 8000 on the MOUNTAIN system. We can open **it** in our browser by navigating to http://192.168.50.189:8000.

> Attention: Our desserts business didn't go well... We decided to show you the tech area!
Since we found out could we had to create any desserts anyone... Anyway, we tried a new process and had a fantastic idea, which will be provided to a server, backup and deploy on. We now get only a small demo. Use it to clone a repository and when we bunch for now we get a credit of 7 days VIP subscription for free.
Try the following command in the below:
git clone repository.com

```
git clone

> Attention: Our desserts business didn't go well... We decided to show you the tech area!
Since we found out could we had to create any desserts anyone... Anyway, we tried a new process and had a fantastic idea, which will be provided to a server, backup and deploy on. We now get only a small demo. Use it to clone a repository and when we bunch for now we get a credit of 7 days VIP subscription for free.
Try the following command in the below:
git clone repository.com

> Attention: Our desserts business didn't go well... We decided to show you the tech area!
Since we found out could we had to create any desserts anyone... Anyway, we tried a new process and had a fantastic idea, which will be provided to a server, backup and deploy on. We now get only a small demo. Use it to clone a repository and when we bunch for now we get a credit of 7 days VIP subscription for free.
Try the following command in the below:
git clone repository.com

> Attention: Our desserts business didn't go well... We decided to show you the tech area!
Since we found out could we had to create any desserts anyone... Anyway, we tried a new process and had a fantastic idea, which will be provided to a server, backup and deploy on. We now get only a small demo. Use it to clone a repository and when we bunch for now we get a credit of 7 days VIP subscription for free.
Try the following command in the below:
git clone repository.com

> Attention: Our desserts business didn't go well... We decided to show you the tech area!
Since we found out could we had to create any desserts anyone... Anyway, we tried a new process and had a fantastic idea, which will be provided to a server, backup and deploy on. We now get only a small demo. Use it to clone a repository and when we bunch for now we get a credit of 7 days VIP subscription for free.
Try the following command in the below:
git clone repository.com

> Attention: Our desserts business didn't go well... We decided to show you the tech area!
Since we found out could we had to create any desserts anyone... Anyway, we tried a new process and had a fantastic idea, which will be provided to a server, backup and deploy on. We now get only a small demo. Use it to clone a repository and when we bunch for now we get a credit of 7 days VIP subscription for free.
Try the following command in the below:
git clone repository.com

> Attention: Our desserts business didn't go well... We decided to show you the tech area!
Since we found out could we had to create any desserts anyone... Anyway, we tried a new process and had a fantastic idea, which will be provided to a server, backup and deploy on. We now get only a small demo. Use it to clone a repository and when we bunch for now we get a credit of 7 days VIP subscription for free.
Try the following command in the below:
git clone repository.com

> Attention: Our desserts business didn't go well... We decided to show you the tech area!
Since we found out could we had to create any desserts anyone... Anyway, we tried a new process and had a fantastic idea, which will be provided to a server, backup and deploy on. We now get only a small demo. Use it to clone a repository and when we bunch for now we get a credit of 7 days VIP subscription for free.
Try the following command in the below:
git clone repository.com

> Attention: Our desserts business didn't go well... We decided to show you the tech area!
Since we found out could we had to create any desserts anyone... Anyway, we tried a new process and had a fantastic idea, which will be provided to a server, backup and deploy on. We now get only a small demo. Use it to clone a repository and when we bunch for now we get a credit of 7 days VIP subscription for free.
Try the following command in the below:
git clone repository.com

> Attention: Our desserts business didn't go well... We decided to show you the tech area!
Since we found out could we had to create any desserts anyone... Anyway, we tried a new process and had a fantastic idea, which will be provided to a server, backup and deploy on. We now get only a small demo. Use it to clone a repository and when we bunch for now we get a credit of 7 days VIP subscription for free.
Try the following command in the below:
git clone repository.com

> Attention: Our desserts business didn't go well... We decided to show you the tech area!
Since we found out could we had to create any desserts anyone... Anyway, we tried a new process and had a fantastic idea, which will be provided to a server, backup and deploy on. We now get only a small demo. Use it to clone a repository and when we bunch for now we get a credit of 7 days VIP subscription for free.
Try the following command in the below:
git clone repository.com
