Reminder: Don't use opiekey from telnet or dial-in sessions.

Enter secret pass phrase:

+   1: SAP GRAD COT BOWL BOLD TASK
+   2: OLAF DATA JIIVE COLD REIN TIRE
+   3: GRID TAR FUNK FIND TWIG TOAD
+   4: HAP WILD KONG TWIT HYNN HERS
+   5: GAIL SUNK READ CLAW HALL DAR
+   6: EDIT RUDY SAN BAG HATH SUE
+   7: TOW LEO DUAL TINA HATE BUB
+   8: BEAN ROVE SALT BOSE RECK BOLT
+   9: TOE MITE GAM GINA REB RODIE
+   10: HACK MARC JAY CEIL SUM DARE
+   11: SIRE AD IONS RUE RASH LUB
+   12: TROOD BOGY CEIL GREW NIL LUND
+   13: TEN DUB SAD MORT FORE REB
+   14: YET MART VEND IOWA TOE MONK
+   15: BEER HANG ONTO DEAD WEAR DANE

Or, if Alice would like to print out the list so she can take it with her, she would enter the following command:

```
[alice]$ otp-md5 15 e6667 ext | lp
```

Note that every time Alice successfully logs on to challenger with her OPIE response, the sequence number is decremented by one. So the next time she will be prompted with the 14th challenge.

As you can see, these is a fair amount of up-front work to be done to set up OPIE, but once it is ready, the advantages over regular username/password authentication are obvious: There will never be a need to expose user passwords in the clear again.

# # Pluggable Authentication Modules (PAMs)

With the explosion of network-aware Linux applications, authentication has become an important issue. Traditionally, Linux application developers included their own authentication mechanisms in their programs, ranging anywhere from no authentication (e.g., TFTP) to strong Kerberos and S/Key authentication (e.g., telnet). Hard-coding authentication into each application has several drawbacks:

+   - The user is forced into a specific mode of authentication.
+   - Changing authentication mechanisms involves recompiling the application.