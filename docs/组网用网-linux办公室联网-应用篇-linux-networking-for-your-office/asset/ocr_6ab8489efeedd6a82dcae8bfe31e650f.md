If you have problems at this stage, you should resolve them now, or you probably won’t have much luck with PPP. Table 8.1 lists some common modem problem symptoms and possible solutions.

**Table 8.1  Modem Troubleshooting Tips**

| Symptom | Possible Causes/Solutions |
|---|---|
| `minicom` won’t run; get a `NO GLOBAL CONFIGURATION FILE` message | As root, run `minicom -s`, enter configuration data, and then save it as `df1`. |
| `minicom` won’t run; get a `PERMISSION DENIED` message | Run `minicom` as root. Alter permissions on serial port device. |
| No response from modem | The modem is not turned on. The modem is a Windows-only model. Attempting to use the wrong device file. Linux serial device driver is not loaded; use `cat /proc/interrupts` and check for a serial device interrupt. Bad modem cable, or cable plugged into wrong port. |
| Can dial, but get gibberish from ISP | This is normal when dialing an ISP that expects to make a PPP connection. |

# PPP Authentication

When you dial an ISP to make a PPP connection, the ISP wants to know who you are for both security and accounting purposes. The process by which you (or your dialing scripts) confirm your identity to your ISP is known as authentication, and there are several different methods of authentication in use today:

+   - **Manual login—**If you dial your ISP and get a prompt asking for your username and password, it’s likely that your ISP supports a manual login procedure. This doesn’t mean that a manual login is your *only* option, though. Manual login is distinctly antiquated by today’s standards, and few ISPs require manual logins. If yours does, you can create a login script to supply appropriate information at appropriate times, but given the scarcity of systems requiring this procedure, this book doesn’t cover creating such a script.