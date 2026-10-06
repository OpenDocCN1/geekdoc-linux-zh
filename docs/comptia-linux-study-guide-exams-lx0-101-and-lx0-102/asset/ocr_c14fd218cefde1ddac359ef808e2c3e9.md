11. Your manager has asked that you configure logrotate to run on a regular, unattended basis. What utility/feature should you configure to make this possible?

+   A. at
B. logrotate.d
C. cron
D. inittab
E. nptpd

12. You have set your system (software) clock on a Linux-only computer to the correct time, and now you want to set the hardware clock. What command might you use to accomplish this goal?

+   A. date --sethwclock
B. sysclock --tohwc
C. set --hw
D. time --set --hw
E. hwclock --utc --systohc

13. As root, you type date 12110710. What will be the effect of the current year.

+   A. The software clock will be set to 7:10 a.m. on December 11 of the current year.
B. The software clock will be set to 12:11 p.m. on October 7 of the current year.
C. The software clock will be set to 7:10 a.m. on November 12 of the current year.
D. The software clock will be set to 12:11 p.m. on July 10 of the current year.
E. The software clock will be set to July 10 in the year 1221.

14. What will be the effect of a computer having the following two lines in /etc/ntp.conf?

server pool1.ntp.org
server tardis.example.org

+   A. The local computer's NTP server will poll a server in the public NTP server pool; the first server overrides subsequent server options.
B. The local computer's NTP server will poll the tardis.example.org time server; the last option overrides earlier server options.
C. The local computer's NTP server will poll both server in the public NTP server pool and tardis.example.org and use whichever site provides the cleanest time data.
D. The local computer's NTP server will refuse to run because of a malformed server specification in /etc/ntp.conf.
E. The local computer's NTP server will poll a computer in the public NTP server pool but will fall back on tardis.example.org if and only if the public pool server is down.