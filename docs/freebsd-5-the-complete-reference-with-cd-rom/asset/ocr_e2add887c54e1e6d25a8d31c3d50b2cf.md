# # while Loops

A second type of loop uses the keyword *while*. These loops continue to execute while a specified condition remains true. The basic form for this loop type is

```
```bash
while [ condition ]
do
    commands
done
```
```

For instance, you might use a structure such as this to perform some operation so long as a file continues to exist, while two variables continue to be equal to each other, or until a user decides to stop an operation. Listing 31-12 illustrates a *while* loop in action. This script calls **passwd** for multiple users, enabling you to change many users' passwords without typing **passwd** for each one. (You must still type the password twice for each user, though.)

**Listing 31-12 A Script Demonstrating the Use of while**

```
```bash
#!/bin/sh
echo "This script changes multiple user passwords."
echo "Enter a username ('n' to exit):"
read username
while [ $username != "n" ]
do
    passwd $username
    echo "Enter a username ('n' to exit):"
    read username
done
exit 0
```
```

> **Note** *Listing 31-12 must be run as root; only root may change passwords for arbitrary users.*

In operation, Listing 31-12 prompts you for a username, then calls **passwd** for that username. The **passwd** program in turn asks for the password twice. (The password you type doesn't echo to the screen.) The result looks like this:

```
```
# ./multipasswd
This script changes multiple user passwords.
Enter a username ('n' to exit):
```
```