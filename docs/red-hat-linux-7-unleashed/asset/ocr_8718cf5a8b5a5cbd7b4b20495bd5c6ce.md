Create a script hold with the contents of Listing 26.4.

# **LISTING 26.4** hold—A "Keep-Alive" Written in Expect

```
```expect
#!/usr/bin/expect
# Usage: "hold HOST USER PASS".
# Action: login to node HOST as USER. Offer a shell prompt for
# normal usage, and also print to the screen the word HELD
# every five seconds, to exercise the connection periodically.
# This is useful for testing and using WANS with short time-outs.
# You can walk away from the keyboard, and never lose your
# connection through a time-out.
# WARNING: the security hazard of passing a password through the
# command line makes this example only illustrative. Modify to
# a particular security situation as appropriate.
set hostname [lindex $argv 0]
set username [lindex $argv 1]
set password [lindex $argv 2]
# There's a trouble if Susername's prompt is not set to "..." .
# A more sophisticated manager knows how to look for different
# prompts on different hosts.
set prompt_sequence ") "
spawn telnet $hostname
expect "login: "
send "$username\r"
expect "Password:"
send "$password\r"
# Some hosts don't inquire about TERM. That's another
# complication to consider before widespread use
# of this application is practical.
# Note use of global [gl] pattern matching to parse "*"
# as a wildcard.
expect -gl "TERM = (*))"
send "\r"
expect $prompt_sequence
send "sh -c 'while true; do echo HELD; sleep 5; done'\r"
interact
```
```

This script starts a telnet session and then keeps the connection open by sending the string "HELD" every five seconds. I work with several telephone lines that are used with short timeouts, as a check on out-of-pocket expenses. I use a variant of the script in Listing 26.4 daily, for I often need that to hold one of the connections open.