Warning: OS detection will be MUCH less reliable because we did not find at least 1 open and 1 closed TCP port For OSScan assuming that port 22 is open and port 43640 is closed and neither are firewalled Interesting ports on unixhost (192.168.0.5): (The 1600 ports scanned but not shown below are in state: filtered) Port State Service 22/tcp open ssh Remote operating system guess: Solaris 9 with TCP_STRONG_ISS set to 2 OS Fingerprint: TSeq(Class=TR%IPID=I%TS=100HZ) T1(Resp=Y%DF=Y%W=C0B7%ACK=S++%Flags=AS%Ops=NNTMNW) T2(Resp=N) T3(Resp=N) T4(Resp=N) T5(Resp=N) T6(Resp=N) T7(Resp=N) PU(Resp=N) Uptime 0.107 days (since Tue Sep 14 15:43:22 2004) TCP Sequence Prediction: Class=truly random Difficulty=9999999 (Good luck!) TCP ISN Seq. Numbers: 60665B23 2CC002B3 C9C05D50 61377D05 7947ED9B 6B5510E9 IPID Sequence Generation: Incremental Nmap run completed -- 1 IP address (1 host up) scanned in 924 seconds

The program found an open port and tried to determine the operating system by using a database containing the reactions of various operating systems in answer to certain network packages. The program determined the right operating system (Solaris). Further the information indicates that the OS is using a hardened TCP/IP stack. Listing 7.19 shows the scan of a GNU-Linux system.

# LISTING 7.19 Using nmap to Reveal the Operating System Used (2)

```
root@unixhost> nmap -PO -v -v -O 192.168.0.2

Starting nmap V. 3.00 ( www.insecure.org/nmap/ )
No tcp,udp, or ICMP scantype specified, assuming SYN Stealth scan. Use -SP if you really don't want to portscan (and just want to see what hosts are up).
Host linuxhost (192.168.0.2) appears to be up ... good.
```