# CHAPTER 18 Secure File Transfer Protocol (FTP) Service

# LISTING 18.1 Continued

lp*:11899:0:99999:7:::

```
ftp*:11899:0:99999:7:::
```

The shadow file (only a portion of it which is shown in Listing 18.1) contains additional information not found in the standard /etc/passwd file, such as account expiration, password expiration, when the account is locked, and the encrypted password. The * in the password field indicates that the account isn't a standard login account, thus it doesn't have a password.

Although passwords are in our system, the password aren't transmitted in a secure manner when using FTP. Because FTP was written before the necessity of encryption and security, it doesn't provide the mechanics to send encrypted passwords. Account information is stored in plain text on FTP servers; anyone with enough technical knowledge and a network sniffer can find the password for the account you connect to the server. Many sites use an anonymous-FTP server specifically to prevent normal account passwords from being transmitted over the Internet.

Figure 18.1 shows an ethereal capture of an FTP session displaying the username and password for a user. The ethereal client is a graphical browser to display network traffic in real time, and it can be used to watch packet data, as an FTP login on a LAN.

| No. | Time | Source | Destination | Protocol | Info |
|---|---|---|---|---|---|
| 1008 | 08:59:024 | cellio.home.org | shuttle2,home.org | FTP | Response: 220 FTP Welcome |
| 1008 | 08:59:024 | cellio.home.org | shuttle2,home.org | FTP | Response: 530 Login failed with USER |
| 1008 | 08:56:372 | shuttle2,home.org | cellio,home.org | FTP | Request: AUTH KERBEROS |
| 1253 | 09:48:000 | shuttle2,home.org | cellio,home.org | FTP | Response: 530 Login failed with USER AND PASSWORD |
| 1258 | 10:03:0704 | shuttle2,home.org | cellio,home.org | FTP | Request: USER login |
| 1347 | 14:03:a374 | shuttle2,home.org | cellio,home.org | FTP | Request: Password required for. |
| 1347 | 14:03:5672 | shuttle2,home.org | cellio,home.org | FTP | Response: PMUS foobar |
| 1347 | 13:03:5672 | shuttle2,home.org | cellio,home.org | FTP | Response: User logged in. |
| 1346 | 13:05:7118 | cellio,home.org | shuttle2,home.org | FTP | Response: 215 UNIX Type: L8 |

FIGURE 18.1 The ethereal client can filter and sniff FTP sessions to capture usernames and passwords.