```
do
mv $d.2001 ;
gzip $d.2001 ;
done
```

Sometimes you need to run through a file line by line, executing some command on each line that matches a certain set of criteria. This is most easily done with a while loop. Suppose you're providing mandatory network training for five users, weekly until all users have been trained. To determine who is up for training, you maintain the /etc/training_list data file. A person's training is categorized in segments from A through D, with D signifying a fully trained user. Network training is C training (training for users at level C). Assume that /etc/training_list is as shown in Listing 17.4.

# Listing 17.4: A Sample /etc/training_list Data File

```
sam|501|34|A
tom|502|23|B
terry|503|43|B
john|504|12|C
mike|505|67|D
sarah|506|45|C
leonard|507|78|B
meg|508|15|D
toml|509|33|B
larry|510|67|C
jeffrey|511|45|D
mark|512|23|C
chris|513|34|D
anne|514|24|A
ellen|515|16|B
jake|516|27|C
pat|517|45|C
```

You might create a script like Listing 17.5 to determine which employees remain to be trained. (This script uses the cut command, discussed later in this chapter.)

# Listing 17.5: A Script for Updating the Training File

```
#!/bin/bash
#remove the old tobe trained file if one exists
if [ -e /home/$USER/tobetrained ]; then
    rm /home/$USER/tobetrained
fi

cat /etc/training_list |
while read line
do
    training=`echo $line|cut -d"|" -f4`
    if [ $training = C ];
    then
        name=`echo $line|cut -d"|" -f1`
        echo $name >> /home/$USER/tobetrained
        echo "$name added to user list"
    fi
done
```