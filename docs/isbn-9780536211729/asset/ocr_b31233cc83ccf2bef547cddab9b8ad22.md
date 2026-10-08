# Limiting Unreasonable Access

Some old UNIX systems would say root login not allowed if someone supplied the correct password and Login incorrect otherwise. This allowed someone to guess the root password on an insecure tty without having to do so from an ordinary account (such). Then when the correct password was guessed a quick su followed by erasing the logs.

Some ancient Linux systems will say root login refused on this terminal prior to accepting a password. This is only slightly less secure than the monolithic Login incorrect.

You will need to decide which devices should be considered secure, and thus worthy to be listed in /etc/security. The console device is used as a login device if virtual consoles are not enabled. If you use virtual consoles then it is a good idea to enable root login on console, in case virtual consoles accidentally disabled. If virtual consoles are in use, they use devices tty1, tty2, Including all of these devices in /etc/security is reasonable. There may not be a need to list more than six or eight tty devices here, that is, tty1 through tty6.



![](bbox=[0.125, 0.435, 0.905, 0.485])

Warding is the term used when someone programs his computer's modem to dial a sequence of phone numbers searching for those with modems connected to them that answer. This is for the purpose of finding computers to break into and it is a standard cracker technique. The very ambitious cracker will try all 10,000 numbers in a phone exchange. In this situation if your number is up, it is up. Frequently a cracker will pick one or more companies to target. Perhaps Pentacorp has announced that it will go public next week.

All a cracker needs to do is to telephone Information in the appropriate area code and be told that Pentacorp's main number is 555-642-6000. The cracker then has his system wardial all numbers between 555-642-6000 and 555-642-6999, note which ones answer with modem tones, the login prompt for operating system type and version name, and start cracking. The operating system type and version tells him what exploits to try and the system name tells him whether it might have interesting data.

The solution to this is rather simple. Change the numbers. In a number off the organization's switchboard or Centrex, get an entirely different number with a different exchange. The slight increase in cost will be well worth the increased security. Remember, any modem behind the corporate firewall can compromise security. See "Stopping End Around Firewalls” on page 68.