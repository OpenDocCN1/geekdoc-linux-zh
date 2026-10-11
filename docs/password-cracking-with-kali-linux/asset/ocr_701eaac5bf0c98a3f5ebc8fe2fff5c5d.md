# FOREIGN LANGUAGE KEYWALKS

If you need to crack foreign language keywalks, just use one of the foreign languages keymap files.
So, to create a Russian keywalk wordlist:

```
>    ./kwp basechars/full.base  keymaps/ru.keymap
    routes/2-to-16-max-3-direction-changes.route  >  rukwp.txt
```

And the resultant file:

![](bbox=[0.19, 0.31, 0.37, 0.55])

If we have a password hash list that contains any of the words that were generated, it will crack them.
The Hashcat KWP tool is great for quickly create keymap walking wordlists. It’s easy too to change the keymap language, which can come in handy if you are cracking international passwords. If you want to learn more about KWP, check out the Hashcat GitHub page - https://github.com/hashcat/kwprocessor