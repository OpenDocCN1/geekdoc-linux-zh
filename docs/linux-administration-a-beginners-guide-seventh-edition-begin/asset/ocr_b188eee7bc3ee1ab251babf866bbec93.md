# CHAPTER 21 Voice over Internet Protocol (VoIP) 57

> TIP The Asterisk CLI supports command-line completion on all commands, including many arguments. To use it, simply press the TAB key at entering the beginning of any command. If Asterisk can complete the command unambiguously, it will do so; otherwise, it will complete as much of the command as possible. Additionally, Asterisk will print a list of all possible matches, if.

We have compiled a list of CLI commands that you will most use frequently in managing the Asterisk installation and troubleshooting issues:

+   **core restart now** Immediately restarts Asterisk. You will exit the CLI and be returned to the Linux prompt.
**core stop now** Immediately stops Asterisk. You will exit the CLI and be returned to the Linux prompt.
**core show calls** [uptime] Displays information on calls.
**core show channels** [concise| verbose|count] Displays information on channels.
**core show channel** Displays information on a specific channel.
**sip show peers** Lists all configured SIP devices. The output includes the account name used for a device and its IP address.
**dialplan show** Displays all of the active (memory) dialplan. This includes, but is not limited to, the configuration in /etc/asterisk/extensions.conf.
**channel request hangup** Requests a hangup on a given channel.
**core reload** Globally reloads the configuration files.
**core set verbose XX** Sets level of verbosity.
**dialplan debug** Shows fast extension pattern matching data structures.
**dialplan reload** Reloads extensions and only extensions.
**sip reload** Reloads SIP configuration.
**sip show {channels|subscriptions}** Lists active SIP channels and subscriptions.
**sip show channel** Shows detailed SIP channel info.
**sip show registry** Lists SIP registration status.

# Common Issues with VoIP

We've equipped you with the basics of setting up and configuring a simple VoIP server in this chapter. However, many things can go wrong or prevent you and your users from getting the best VoIP experience possible. Even more annoying is that some the factors causing this are usually out of your control and hard to pinpoint.