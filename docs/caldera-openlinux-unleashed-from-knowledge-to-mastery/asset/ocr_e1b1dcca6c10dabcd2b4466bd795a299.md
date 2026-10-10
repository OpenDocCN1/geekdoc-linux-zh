Suppose you want to add the string value 'Winner of the 1999 safety award.' to the Description attribute of the object named hsimpson, which is in the PowerPlant organization of the NDS tree named cburns. You issue the following nwmodyfy command:

```
nwdsmodify -o /NetWare/NDS/cburns/PowerPlant/hsimpson
-a Description -v "Winner of the 1999 safety award." -s "CI String" -c a
```

You can also use:

```
nwdsmodify -o /NetWare/NDS/cburns/Engineering/ATG
-a Member -v hsimpson.PowerPlant -s "Distinguished Name" -c d
```

In the first case, the distinguished name hsimpson.PowerPlant (which could have also been referred to as /NetWare/NDS/cburns/PowerPlant/hsimpson) is removed from the Member attribute of the group named ATG, which is in the Engineering organization of the NDS tree named cburns.

Here's another version of nwdsmodify for the example:

```
nwdsmodify -o /NetWare/NDS/Macmillan/Publishing/silenz -a "Home Directory"
-v "0:server1_sys.Publishing"/home/silenz -s Path -c a
```

This command adds a new value to the Home Directory property of the object silenz in the Publishing organization of the Macmillan NDS tree. The Home Directory property is type Path, and that new path value is the directory /home/silenz on the volume whose NDS distinguished name is server1_sys.Publishing.

# # Managing Disk Quotas on NDS Servers

As with bindery servers, you can assign a space quota to each directory on a volume attached to an NDS server. To view the present disk space allocated for a quota, you use nwsshowspace:

```
nwsshowspace -d path_to_directory_service
```

To change the disk quota or to set it in the first place, you use the nwssetspace command. You must include the -d argument along with one of the -b, -k, or -m arguments, each with its own parameter. The syntax is

```
nwssetspace -d path_to_directory_service
```

At the end, you must add one of the following options:

+   - -k With the number of kilobytes that this directory can use.
+   - -m With the number of megabytes that this directory can use.