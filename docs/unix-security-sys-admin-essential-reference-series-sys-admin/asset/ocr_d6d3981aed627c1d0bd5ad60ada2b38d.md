# Test Your Application

At this point, your system is running Enhanced Security and you should test your applications as appropriate before declaring success. Before your users attempt to log in and perhaps run afoul of the system, note that if any user’s password under Base security was longer than eight characters, only the first eight characters will now be accepted as valid. For example, if a password was toogood2be, the user must enter only toogood2 to successfully log in. When the user changes his or her password under Enhanced Security, the global or user defaults, if different, will dictate the password length. Make sure your users are aware of this password issue before they log into the newly Enhanced Security-enabled system.

# Listing 18.1 (continued)

```
awk 'FS="=", OFS="=" {print $1,"**",$3,$4,$5,$6,$7}' /etc/passwd > \
/etc/ptmp/passwd.modified

cp /etc/ptmp/passwd.modified /etc/passwd

if [ -f /etc/passwd.pag -o -f /etc/passwd.dir ]
then
    print 'Rebuilding the password database...'
    ( cd /etc ; mkpasswd passwd )
else
    print 'The hashed password database does not exist.'
    print -n 'Do you want to create it [y]/n? '
    if read y
    then
        case "$y" in
            in [yY]* ) print 'Rebuilding the password data base...'
                        ( cd /etc ; mkpasswd passwd ) ;;
        esac
    fi
fi

rm -rf /etc/ptmp
print 'Successfully replaced encrypted passwords with asterisks'
exit 0
```