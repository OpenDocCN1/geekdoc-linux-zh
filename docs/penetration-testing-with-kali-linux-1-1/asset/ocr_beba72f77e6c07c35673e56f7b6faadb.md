![](bbox=[0.13, 0.1, 0.88, 0.31])

When the download is complete, we will rename the binary to **Current.exe** and copy it to **C:\Puppet**. This will ensure that the binary will be executed before Windows attempts to execute the real binary on service startup.

![](bbox=[0.13, 0.41, 0.88, 0.84])

Next, we need to start **msfconsole** with the configuration that we used earlier to generate the payload in order to catch our reverse shell. We will also instruct Metasploit to migrate the shell into