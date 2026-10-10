fashion so that a tool such as `hosts_to_named` can safely and efficiently administer database files for you as in the following example:

```
/etc/hosts
15.17.186.159 wtec712-rtx

127.0.0.1 localhost loopback
# 812 Bogus Domain BASEBALL.HP.COM

# NL~ EAST DIVISION
10.1.1.1 atlantabraves.baseball.hp.com
10.1.1.2 newyork newyorkmets.baseball.hp.com
# NL- CENTRAL DIVISION
10.1.2.1 houstonastros houstonastros.baseball.hp.com
10.1.2.2 chicagocubs chicagocubs.baseball.hp.com
10.1.2.3 stlouiscardinals stlouiscardinals.baseball.hp.com
```

2. Create a `param` file with the parameters for your domain as shown in the following example for `/tmp/param`:

```
/tmp/param
-d baseball.hp.com <---------- Your domain.
-n 10.1.1
-n 10.1.2
-n 10.1.3
-n 15.17.186
-H /etc/hosts.dnctest <---------- hosts file you will use.
-r <---------- If this nameserver is a
root NS. Our examples
below are NOT for root NS.
```

3. Run `hosts_to_named` with your newly created `param` file from the directory in which you want to place the database. Note that the `param` file is not necessary, but, it is a good idea; the options can be run from the command line instead of including a file. Another common error with `hosts_to_named` is not running it in a "clean" directory. If you need to preserve results before you run it, `mkdir /etc/named.data.old; mv /etc/named.data/* /etc/named.data.old` to preserve the prior configuration.

```
# cd /etc/named.data
# hosts_to_named -f /tmp/param
```