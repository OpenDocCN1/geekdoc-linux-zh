```
{
    write(sd, "Too many users - sorry...\n", 26);
    close(sd);
}
}
```

```
free_user_slot(int slot)
{
    user[slot].in_use = 0;
    close(user[slot].sd);
}
```

```
fatal(char *mess)
{
    printf("Error: %s\n", mess);
    exit(1);
}
```