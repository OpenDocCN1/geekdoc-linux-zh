| Area | Description |
|------|-------------|
| Screen status area | • Consists of the right-most 21 character positions of the last line. • Screen status indicators appear here. • Indicates whether the current environment is CP or VM. • The status displayed here can be one of the following values: - CP READ indicates CP issued a read request to the display and is waiting for the user to enter something before it can continue processing. - VM READ indicates the virtual machine is awaiting a response from the user before it can continue processing. - RUNNING indicates CP or VM is either ready to accept commands, or is processing an already executed command. - MORE ... indicates that the output display area is full but more data is available to display, as follows: • CP waits 60 seconds (default) and then displays the next window. • Use the PA key (3270) to see the next screen without waiting 60 seconds. • Use the Enter key (3270) to keep the current screen (status changes to HOLDING). - HOLDING indicates that user pressed Enter (3270) in response to MORE ... - NOT ACCEPTED indicates that the previous input was not accepted (CP locks keyboard for 3 seconds). |

a. Use SET FULLSCREEN ON from CMS if you want the scroll back option. This is disabled by default. (Note this works only for CMS.)

# 2.7.6 Session management

Your session begins when you log to the system, and it ends when you log off. This section describes the logging on, logging out, and several other actions you can perform during a session.

# Logging on

Refer to Figure 2-13 on page 55 as you read through the following details in this section about logging on.

+   The logon screen contains three fields:
+   - USERID
+   - PASSWORD
+   - COMMAND

As mentioned in 2.7.5, "Getting to know your virtual console" on page 54, the two ways to log in are as follows:

+   • Enter your user name and password in the USERID and PASSWORD fields.