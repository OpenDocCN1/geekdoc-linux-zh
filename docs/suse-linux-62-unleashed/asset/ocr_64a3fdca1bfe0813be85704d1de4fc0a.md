# Networking and Internet Services
PART II

To add authentic PAP/CHAP authentication, you need to make sure you're running one of the mgety variants, not just standard getty or agety. This means making sure the mgety package is installed (rpm -qa | grep mgety) and then making sure your /etc/initab entries for the modem ports point to mgety. Once this is done, PAP/CHAP authentication should automatically work. If it doesn't, edit the file /etc/mgety/login.config. It should have a line like the following:

```
/AutoPPP/ a_ppp /usr/sbin/pppd auth -chap +pap login debug
```

If the line isn't there, add it; if it's commented, uncomment it. If the line is PAP/CHAP still doesn't work, you might need some extra PPP options. Check the pppd(8) man for more information.

If some or all of your users' PPP programs don't support PAP or CHAP, you need to perform a trick: Create the ppp script outlined to /usr/local/bin/pppp in the previous section (it has to be a script, not an alias). Set your users' login shell to /usr/local/bin/pppp /etc/passwd (just as an example). This makes the getty login process start the pppd daemon instead of the standard shell.

> Tip  This method isn't as secure as it should be. A knowledgeable user could use Ctrl+C to stop the script's execution