might be unable to type their username and password to log in if the keyboard layout is incorrect.

If a multi-computer system is serving users who need to type multiple languages or use different keyboard layouts, the system and the greeter should be started using a common language layout, which can be changed by the individual users after logging in. Desktop Multiplier supports full internationalization of its configuration tools with translations available in most commonly languages. Support for additional languages are typically available within several business days of a request for supporting a new language.

# Security considerations

Security security on multi-station Linux poses significant challenges beyond those of single-user Linux workstation deployments. The key security difference between a single-user Linux workstation and multi-station Linux is that multiple users share access to the same computer system; therefore, its storage, processes, programs, and other hardware are also shared. Any system compromise or corruption during one user's activity can potentially affect all users.

Sharing systems is not explicitly a problem if the users never modify their workstation environment, for example, by installing browser plug-ins and applications, or by adding or compiling shared libraries. But multiple users are able to simultaneously run potentially untrusted applications on the same computer, a physical or electronic compromise of one user's environment could result in the compromise of all local user environments.

In order to minimize the effect of user configuration changes, we recommend that users of multi-station systems never get local root or administrator level access, and that users are made aware of how to install software in their own private directories without adversely affecting the shared multi-station computer environment. In this manner, no user can have access to another user's temporary files or running processes, and no user can modify the shared environment.

# Privacy considerations

As discussed above, sharing a computer could result in the inappropriate, inadvertent, or deliberate disclosure of confidential information. The potential for sharing data and the sometimes complicated access controls required to prevent

> 3 The default keyboard layout is set in the X.Org configuration file and is generally guessed by the default system language.

Appendix D. Multi-station computing deep dive using Useful Desktop Multiplier 305