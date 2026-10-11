# Disabling or Deleting Unused Accounts

If you decide you don't want a particular user on your system anymore (say, another programmer writes better code or someone's changed office-mates), you should disable or delete the account. There are various ways to disable an account, but if you delete, you should probably not do it manually; all your files must be properly cleared first.

# DISABLING AN ACCOUNT

To lock an account, use the -l option with the passwd command.

```
```
bash# passwd -l vertech
Password changed.
```
```

You can see the account information with the -S option. Note the L for locked.

```
```
bash# passwd -S vertech
veritech L 07/19/98 0 99999 7 -1
```
```

Note that nothing is changed in /etc/passwd, but there is a noticeable difference in the password field of /etc/shadow.

```
```
bash# cat /etc/shadow
halt:*:10426:0:99999:7:::
operator:*:10426:0:99999:7:::
root:zDv78WL5BVg2:10426:0:99999:7:::
shutdown:*:10426:0:99999:7:::
sync:*:10426:0:99999:7:::
bin:*:10426:0:99999:7:::
ftp:*:10426:0:99999:7:::
daemon:*:10426:0:99999:7:::
ad m:*:10426:0:99999:7:::
lp:*:10426:0:99999:7:::
mail:*:10426:0:99999:7:::
postmaster:*:10426:0:99999:7:::
news:*:10426:0:99999:7:::
uucp:*:10426:0:99999:7:::
man:*:10426:0:99999:7:::
games:*:10426:0:99999:7:::
nobody:*:10426:0:99999:7:::
boB:TH54ciu/THDu.:10426:0:99999:7:::
veritech:!jHg1DqoCj1pIy:10426:0:99999:7:::
```
```