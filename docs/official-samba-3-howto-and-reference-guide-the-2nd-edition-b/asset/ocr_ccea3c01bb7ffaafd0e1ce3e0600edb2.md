In the event that the ADS trust was not established, or is broken for one reason or another, the following error message may be obtained:

```
```
root#  net ads testjoin -UAdministrator%secret
Join to domain is not valid
```
```

The following demonstrates the process of creating a machine trust account in the target domain for the Samba server from which the command is executed:

```
```
root#  net rcp join -S 13000 -Uroot%not24get
Joined domain MIDEARTH.
```
```

The joining of a Samba server to a Samba domain results in the creation of a machine account. An example of this is shown here:

```
```
root#  pdbedit -Lw merlin$
merlin$:1009:9B4489D6B90461FDBA3E3C3AB96147E16:\
      176DC8554E99914BDF3407DEA2231D80:[S          ]:LCT-42891919:
```
```

The S in the square brackets means this is a server (PDC/BDC) account. The domain join can be cast to join purely as a workstation, in which case the S is replaced with a W (indicating a workstation account). The following command can be used to affect this:

```
```
root#  net rcp join member -S 13000 -Uroot%not24get
Joined domain MIDEARTH.
```
```

Note that the command-line parameter *member* makes this join specific. By default the type is deduced from the *smb.conf* file configuration. To specifically join as a PDC or BDC, the command-line parameter will be [PDC | BDC]. For example:

```
```
root#  net rcp join bdc -S 13000 -Uroot%not24get
Joined domain MIDEARTH.
```
```

It is best to let Samba figure out the domain join type from the settings in the *smb.conf* file.

The command to join a Samba server to a Windows ADS domain is shown here:

```
```
root#  net ads join -UAdministrator%not24get
Using short domain name -- GDANSK
Joined 'FRANDIMITZ' to realm 'GDANSK.ABMAS.BIZ'
```
```