Red Hat Linux release 7.0 (Guinness)
Kernel 2.2.16-22 on an i686
login: `alice`
otp-md5 15 re6667 ext
Response:

At this point, alice has two options. The first option is to use the `otp-md5` utility on her own system (at1antis) in another xterm window, as shown in Listing 13.18.

# Listing 13.18  Using the `otp-md5` utility in an xterm window

```
```
[alice]$ hostname
at1antis
[alice]$ otp-md5 15 re6667 ext
Using the MD5 algorithm to compute response.
Reminder: Don't use opiekey from telnet or dial-in sessions.
Enter secret pass phrase:
BEER HANG ONTO DEAD WEAR DANE
```
```

The `otp-md5` utility simply generates a one-time password using the MD5 hashing algorithm. It takes two arguments:

```
```
otp-md5 sequence seed
```
```

The *sequence* is the number of MD5 iterations that the `otp-md5` utility uses to hash the seed into a one-time password (the response). Note that both the *sequence* (15) and the *seed* (re6667) are included in the challenge in the previous example. Once the response has been calculated, Alice can simply cut it from the at1antis window and paste it at the prompt in the challenger window, as follows:

```
```
login: alice
otp-md5 15 re6667 ext
Response: BEER HANG ONTO DEAD WEAR DANE
Last Login: Tue Feb 27 15:38:47 from at1antis
You have mail.
```
```

Alice’s second option is to pre-print a number of one-time passwords and keep the entire sequence with her. She can use the `otp-md5` utility to do this by specifying the -n *sequence* option, as shown in Listing 13.19.

# Listing 13.19  Using the `otp-md5` utility to pre-print one-time passwords

```
```
[alice]$ otp-md5 -n 15 15 re6667
Using the MD5 algorithm to compute response.
```
```