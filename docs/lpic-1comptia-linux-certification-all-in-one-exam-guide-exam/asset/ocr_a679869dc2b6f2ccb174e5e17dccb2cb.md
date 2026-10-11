![](bbox=[0.12, 0.07, 0.22, 0.13])

**TIP** You could also use a whole series of if/then statements instead of a case statement. However, it can get really messy and is considered poor form. If you have a condition that can be evaluated to return more than two responses, you should use a case statement.

The syntax for using a case structure is as follows:

```
case variable in
    response_1 ) commands
        ;;
    response_2 ) commands
        ;;
    response_3 ) commands
        ;;
esac
```

Essentially, the case statement compares the value of the variable listed to the list of responses within the case statement. If a match is found, then the commands associated with that response are run. Commands for all other list items are ignored.

For example, we could write a script that asks users what month they were born in. Based on the response they give, you could cause the script to provide a customized response using a case statement. Here is a sample script that does this:

```
#!/bin/bash
# A simple script to demonstrate the case structure.
echo "What month were you born in?"
read MYMONTH
case $MYMONTH in
    December | January | February ) echo "Being born in" "$MYMONTH", you were born during the winter in the Northern Hemisphere.
        ;;
    March | April | May ) echo "Being born in" "$MYMONTH", you were born during the spring in the Northern Hemisphere.
        ;;
    June | July | August ) echo "Being born in" "$MYMONTH", you were born during the summer in the Northern Hemisphere.
        ;;
    September | October | November ) echo "Being born in" "$MYMONTH", you were born during the fall in the Northern Hemisphere.
        ;;
    * ) echo "Sorry, I'm not familiar with that month!"
        ;;
esac
exit 0
```

This script asks users what month they were born in and then determines the season of their birth using a case structure. Five options are provided:

+   - December, January, or February
+   - March, April, or May
+   - June, July, or August