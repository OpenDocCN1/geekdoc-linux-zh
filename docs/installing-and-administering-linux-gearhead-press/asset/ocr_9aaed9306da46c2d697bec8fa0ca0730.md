```
```
$ cat private_bu
#!/bin/bash
var3=`df -h | grep hda6 | grep % | cut -c 40-42`
BUP=nightly-$USER-backup-5(grep +$\tmd).tgz
if [ $var3 -it "85" ] ; then
tar -cZf $BUP -
else
echo "The file system is too full! Call system administrator NOW!"
fi
```
```

This script also sets a variable called `var3` to the results of the piped commands. This method is a very nice way to supply information to a script. This specific case takes the results of the `df - h` command, `grxeps` out the “`% used`” number, and then uses `cut` to singel out the value. If the value exceeds 85 percent, then it is to issue a console message to contact the system administrator.

# ## For, Cron, While, and Until Loops

Nothing is handier than a little mechanism that can save you lots of redundant keying. We are going to show you how to use basic `for`, `while`, and `until` loops to aid your productivity. We also mention `crontab`, too.

# ### For Looping

`For` is good for iterating over strings of data and performing basic functions.

# #### Example 13.13 “For Looping” the Scripts to the Boss

Suppose that Lady Dulcinea wants a copy of Freston's script files at the end of every day. Freston would write a script with a `for` loop to accommodate this request. Here he goes:

```
```
$ cat > cp4boss<Enter>
#!/bin/bash
#
# Copy files to the bosses directory
#
for i in $( ls script* ) ; do

cp $i /home/dulcinea
	echo $i copied to Lady Ds directory
done
<Ctrl>-d
```
```