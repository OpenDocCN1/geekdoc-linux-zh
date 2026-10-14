```
a|A)
    echo "Hostname: $HOSTNAME"
    uptime
    ;;
b|B)
    df -h
    ;;
c|C)
    if [[ $(id -u) -eq 0 ]]; then
        echo "Home Space Utilization (All Users)"
        du -sh /home/*
    else
        echo "Home Space Utilization ($USER)"
        du -sh $HOME
    fi
    ;;
*)
    echo "Invalid entry" >&2
    exit 1
    ;;
esac
```

Here, we modify the case-menu program to use letters instead of digits for menu selection. Notice that the new patterns allow for entry of both upper- and lowercase letters.

# Final Note

The case command is a handy addition to our bag of programming tricks. As we will see in the next chapter, it’s the perfect tool for handling certain types of problems.