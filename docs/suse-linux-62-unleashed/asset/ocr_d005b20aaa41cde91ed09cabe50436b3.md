# SuSE System Administration
PART III

```
# setup Mon Sep 27 17:48:10 EDT 1999
#
remote|lp4|aptiva-lp|aptiva lp|\
:lp=:\n:rm=aptiva|\
:rp=lp|\
sd=/var/sp/lpd/aptiva-lp|\
:lf=/var/sp/lpd/aptiva-lp/log/\
:af=/var/sp/lpd/aptiva-lp/acct/\
:ark=mx#@:\n:tr=cl-sh
```

### END aptfsiler: ### remote aptiva lp ###

The rm and :rp entries define the remote host and printer. The remote machine (aptiva in this example) has a configured printer name lp and should also have a properly configured hosts.lpd file under the /etc directory. For example, to enable printing on the lp queue from other computers, you should enter a list of allowed remote hostnames in aptiva's /hosts.lpd file, like this:

+   ascentia.home.org
presario.home.org
hitachi.home.org

This allows print jobs from the three listed computers. However, in order to print properly prepared streams of text, you will need to configure filters for the remote computer. After you add the remote printer, return through the SETUP menu to the DEVICE section and press Enter. You'll again see it a dialog as shown in Figure 24.10. This time, scroll down and select the PREFILTER menu item. You'll then see a dialog listing configured printers (see Figure 24.14).

# Figure 24.14
Select your remote printer definition to configure a software filter.

![](bbox=[0.318, 0.706, 0.941, 0.843])

Scroll through the listed printers, highlight your network printer definition, and press Enter. You'll then see the dialog shown in Figure 24.15.