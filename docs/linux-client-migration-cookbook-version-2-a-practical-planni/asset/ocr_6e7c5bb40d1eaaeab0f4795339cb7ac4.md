# Example 7-2 Mapping profiles to users and groups in /etc/kde-user-profile

```
[General]
groups=itso,redbook,users

[Groups]
itso=ITSO
redbook=Redbook
users=default

[Users]
anette=Designer
root=Administrator
```

![](bbox=[0.26985000000000003, 0.31633, 0.81645, 0.7633300000000001])

Figure 7-1 Configuring users and groups with the Kiosk Admin Tool

Another interesting case happens when a user not listed in the Users section is part of different UNIX groups that are mapped to different profiles in the Groups section. In that case, the profiles listed earlier will have higher priority. Last but not least, if a user is listed in the Users section, only the profiles in this entry