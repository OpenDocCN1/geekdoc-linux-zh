
## Chapter 4 • Initial Triage and Live Response: Data Analysis

log, but don't. They have wanted to be put in an Intrusion Detection System (IDS), or Intrusion Prevention System (IPS), but have not had the resources. You will need to find out what they have, where it sits on the network, and does it do log. Make sure you request any logs they do have.

- **Status of Effected Systems** This is another one of those items in which the customer may not really know much about. I have been involved in several cases in which you are told one thing, for instance that a particular system as not been rebooted; only to find out the exact opposite is true once you arrive on-site. So if you asked the questions prior to your arrival have to ask them again, and verify if possible. This information can affect the direction of your investigation.

- **Business as Usual** As much as possible, you need to understand what “normal” is to the customer. When responding to an incident, you are most likely looking at the customer infrastructure for the first time. You will have no idea what their ID naming convention is, what kind of traffic they experience on an average day, which systems communicate with each other, or any of literally hundreds of variables that make up their typical day. For you to perform any sort of initial analysis you need to understand this as possible.

While you need to ask as many questions regarding this subject as possible, understand that more questions will undoubtedly arise as the investigation progresses. Make sure you let the customer know you will have more questions, and you will need a solid point of contact (POC) that is knowledgeable enough about their technical and business processes to intelligently answer them.

Once you have gathered all of the information you deem to be relevant (which will most assuredly change), you can begin initial analysis. The most important thing at this stage in the investigation is to remain neutral about the incident. Try not to formulate premature conclusions about the direction the data is taking. Simply let the data dictate the path you take.

## Log Analysis

In my humble opinion, the starting point for your investigation should be an analysis of whatever log files the customer was able to provide. This may be nothing, in which case you might well take some aspirin now, because a headache is rapidly approaching, or it may be terabytes of data, in which case you should probably take the aspirin anyway, as that same headache is rapidly approaching.

Start at the beginning. It is the simple notion that in any incident, the intruder has to get onto the customer network from somewhere, so there. It may be a Virtual Private Network (VPN) concentrator, it may be a satellite office, and it may be from a specific workstation or server. Whatever the case be, start there.

Log files on Linux systems can be wonderful things. They are highly configurable, efficient, and detailed. With any luck, the system you are gathering and/or analyzing logs has at the very least, the default configurations for logging in place. Linux logs are in plain text, so you will not need to use any third-party software or utilities to perform effective searches. Additionally, you can write custom scripts to perform automatic actions based on the content of the logs, and your desired output.

Linux logs are located in the /var/log directory. These are the log files maintained by the system, and more than likely (and usually by default), from any third-party software that has been installed into the system. You will also see files in the directory which end in a name, as seen in Figure 4.1.

### Figure 4.1 Files in Endings

```
log_type       syslog          var.log         dmes.log         kern.log         mail           couple.log,1  udev           postgresql
auth.log       auth.log.1      boot.log        dbw.0          dpkg.dplog.1     messages       syslog           user.log        updated-apt-grades   kern.log.0
acpid.log      acpid.log.1     btmp.0          btmp.0          dpkg.dplog.1     kern.log.1      messages.1       syslog           user.log.1
auth62.log     auth62.log.1    wtmp.0          wtmp.0          dpkg.dplog.2     kern.log.2      messages.2       syslog           user.log.2
auth64.log     auth64.log.1    lastlog.0       lastlog.0       dpkg.dplog.3     kern.log.3      messages.3       syslog           user.log.3
cron.log       cron.log.1      creds.0          creds.0          dpkg.dplog.4     kern.log.4      messages.4       syslog           user.log.4
fail.log       fail.log.1      fpc.0           fpc.0           dpkg.dplog.5     kern.log.5      messages.5       syslog           user.log.5
ufw.log        ufw.log.1       gmmp.0          gmmp.0          dpkg.dplog.6     kern.log.6      messages.6       syslog           user.log.6
hhold.log       hhold.log.1      hd.0            hd.0            dpkg.dplog.7     kern.log.7      messages.7       syslog           user.log.7
ndmp.log       ndmp.log.1      info.0          info.0           dpkg.dplog.8     kern.log.8      messages.8       syslog           user.log.8
nscd.log       nscd.log.1      journal.0       journal.0        kern.dplog.9     kern.log.9      messages.9       syslog           user.log.9
apport.log    apport.log.1    base.0          base.0          dpkg.dplog.10    kern.log.10     messages.10      syslog           user.log.10
port.log       port.log.1      port.0          port.0          dpkg.dplog.11    kern.log.11     messages.11      syslog           user.log.11
report.log    report.log.1    report.0        report.0        dpkg.dplog.12    kern.log.12     messages.12      syslog           user.log.12
stat.log       stat.log.1      stat.0          stat.0          dpkg.dplog.13    kern.log.13     messages.13      syslog           user.log.13
stack.log      stack.log.1     stack.0         stack.0         dpkg.dplog.14    kern.log.14     messages.14      syslog           user.log.14
tmp.log        tmp.log.1       tmp.0           tmp.0           dpkg.dplog.15    kern.log.15     messages.15      syslog           user.log.15
ern.log       kern.log.1      kern.0          kern.0          dpkg.dplog.16    kern.log.16     messages.16      syslog           user.log.16
apt.log        apt.log.1       apt.0           apt.0           dpkg.dplog.17    kern.log.17     messages.17      syslog           user.log.17
smp.log        smp.log.1       smp.0           smp.0           dpkg.dplog.18    kern.log.18     messages.18      syslog           user.log.18
sambad.log     sambad.log.1    sambad.0        sambad.0        dpkg.dplog.19    kern.log.19      messages.19      syslog           user.log.19
mail.log       mail.log.1      mail.0          mail.0           dpkg.dplog.20    kern.log.20     messages.20      syslog           user.log.20
var.log        var.log.1       var.0           var.0           dpkg.dplog.21    kern.log.21     messages.21      syslog           user.log.21
root.log       root.log.1      root.0          root.0           dpkg.dplog.22    kern.log.22     messages.22      syslog           user.log.22
kern.log       kern.log.1      kern.0          kern.0          dpkg.dplog.23    kern.log.23     messages.23      syslog           user.log.23
log.log        log.log.1      log.0           log.0           dpkg.dplog.24    kern.log.24     messages.24      syslog           user.log.24
sys.log        sys.log.1       sys.0           sys.0           dpkg.dplog.25    kern.log.25     messages.25      syslog           user.log.25
auth.log       auth.log.1      auth.0          auth.0           dpkg.dplog.26    kern.log.26     messages.26      syslog           user.log.26
user.log       user.log.1      user.0           user.0           dpkg.dplog.27    kern.log.27     messages.27      syslog           user.log.27
```

These are called rotated archives. Depending on what level of granularity logging has set, logs get large and cumbersome. Linux provides a command “logrotate”, which does exactly you would think it does: rotates the log files by appending a numerical suffix to the end of the file. For example, in Figure 4.1 you can see “syslog” without a numerical suffix. The first log in the archive is “syslog.0.gz” file, and the previously active log file. Next you will see “syslog.1.gz” through “syslog.6.gz”. These are the remainder of the archived logs in a gzip format. When “logrotate” runs, usually daily (can be found by default in /etc/cron.daily), it takes the current file, appends a “.0” to the end of the file, and starts logging again in the standard name of this file, “syslog.”
