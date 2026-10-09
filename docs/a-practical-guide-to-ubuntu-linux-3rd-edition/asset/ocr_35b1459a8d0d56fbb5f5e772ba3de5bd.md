/var/log hierarchy. In addition to providing logging facilities, **syslogd** allows a single machine to serve as a log repository for a network and allows arbitrary programs to process specific log messages.

**rsyslog.conf** The /etc/rsyslog.conf file stores configuration information for **rsyslogd** while the /etc/rsyslog.d/50-default.conf file stores default rules for **rsyslogd**. Each line in the 50-default.conf file contains one or more *selectors* and an *action*, separated by whitespace. The selectors define the origin and type of the messages; the action specifies how **rsyslogd** processes the message. Sample lines from **r syslog.conf** follow (a # indicates a comment):

```
# First some standard logfiles. Log by facility.
    kern.*        -/var/log/kern.log
    lpr.*         -/var/log/lpr.log
    mail.*        -/var/log/mail.log
    #
    # Some "catch-all" logfiles.
    *.=debug;\   auth,authpriv.none;\
               news.none;mail.none          -/var/log/debug
    *.=info;*.=notice;*.=warning;\  auth,authpriv.none;\
               cron,daemon.none;\        mail,news.none -/var/log/messages
    #
    # Emergencies are sent to everybody logged in.
    *.emerg       *
```

**Selectors** A selector is split into two parts, a *facility* and a *priority*, which are separated by a period. The facility indicates the origin of the message. For example, **kern** messages come from the kernel and **mail** messages come from the mail subsystem. Following is a list of facility names used by **rsyslogd** and the systems that generate these messages:

Facilities |   
auth | Authorization and security systems including login 
authpriv | Same as *auth*, but should be logged to a secure location 
cron | cron 
daemon | System and network daemons without their own categories 
kern | Kernel 
lpr | Printing subsystem 
mail | Mail subsystem 
news | Network news subsystem 
user | Default facility; all user programs use this facility 
uucp | The UNIX-to-UNIX copy protocol subsystem 
local0 to local7 | Reserved for local use

The priority indicates the severity of the message. The following list of the priority names and the conditions they represent appears in priority order: