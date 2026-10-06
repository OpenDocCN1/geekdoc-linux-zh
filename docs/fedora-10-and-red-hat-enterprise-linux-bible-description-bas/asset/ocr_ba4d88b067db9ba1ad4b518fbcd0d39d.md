# Chapter 26: Integrating Fedora with Apple Macs 987

![](bbox=[0.17625, 0.09633, 0.60375, 0.26932999999999996])

**Figure 26-2:** In Mac OS, see Samba and AppleTalk shares from the Connect To Server window.

Enter the address, as shown in Figure 26-2, or click the Browse button to see a list of servers.

After you click Connect, a pop-up window appears, prompting for a user name and password. Use the Options window to set up your preferences for logging on to the server. You can have the password added to your keychain so you don't have to type it each time you access the server.

From the Options window, you can also select to send the password in clear text (which is the default) and be warned you are doing that. The server determines whether you need to enter a clear-text or encrypted password (if you send the wrong type of password, it will fail). You can also request a secure connection over SSH for your login (which is a good idea to prevent someone from sniffing out your password from the network).

**Figure 26-3** shows the Options window for selecting password options as just described.

![](bbox=[0.19625, 0.58933, 0.58375, 0.80933])

**Figure 26-3:** Select authentication options when you connect to your AppleTalk (netatalk) server.