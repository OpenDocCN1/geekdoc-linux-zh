# # WATCH LIVE TRAFFIC AND DATA WITH WIRESHARK

The definitive network protocol analyser

Wireshark is one of the best-known network analysis tools. It is capable of analysing live traffic as well as data captured to the disk. Wireshark can be launched from the Sniffing and Spoofing category in the Applications menu in Kali Linux.

Wireshark has many uses. Chief among these is, should malware make it onto your network, you will be able to analyse malicious files as they enter and also find what data (if any) was successfully stolen.

At first the display can seem very garbled, as it will show all data packets. Click the filter bar at the top to pare this down. To start, enter http.request.full_uri to see HTTP requests.

Filter displays can be dischained; for example: `http.request.full_uri || ssl.handshake.certificate || dns`

If you regularly use the same search criteria, go to the Analyze\Filter Display Macros menu to set up a shortcut. For a full list of display filters, visit www.wireshark.org/docs/dfref. Right-click any packets of interest and choose Follow>TCP stream to find out more.

![](bbox=[0.35, 0.25, 0.94, 0.5])

Go to File>Save As to choose which packets to save and in what format. These can be opened later in Wireshark and other tools such as Kismet (featured later) for analysis.

The full user guide for Wireshark is available as a PDF from: www.wireshark.org/download/docs/user-guide-3.4.pdf

# # PREVENT MALWARE FORWARDING WITH CLAMAV

Check individual files or multiple emails with this powerful antivirus scanner

Although Linux systems cannot be affected by Windows malware, by default they will happily forward on malicious files via internet or USB to more vulnerable machines.

ClamAV is an excellent FOSS (free and open source software) antivirus software toolkit. Its database is updated once every few hours and its detection rate beats that of many commercial scanners.

In Kali, run: `apt-get install clamav clamav-update clamdscan clamav-daemon`

...to install the necessary files. You can use the command freshclam to update the virus database manually, but it's far better to schedule this as a cron job. Run the command:

![](bbox=[0.35, 0.68, 0.94, 0.78])

```
`clamdscan -r <filename>`
```

...to scan individual files or folders. The ClamAV daemon will launch automatically once installed, but is not a real-time scanner in that it will not check files as they are written. The application ClamFS, however, can be used to automate checks of folders such as Downloads. Visit clamfs.sourceforge.net for more information.

ClamAV is most commonly used on mail servers running Postfix to prevent the sending of malware and phishing emails through installing the additional program ClamSMTP. After installation, the ClamAV config files need to be updated to reflect the ports used by PostFix. This is to make sure all mail is scanned. Visit the developer page at theclavier.tetof.software/clamsmtp for full instructions.