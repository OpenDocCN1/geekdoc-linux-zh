This feature actually can open up a lot of options for an administrator. For instance, let’s say that you manage three data centers in New York, London, and Tokyo. As a good administrator, you have set up a unique subdomain for each of these data centers, so the New York, London, and Tokyo servers use ny.example.net, london.example.net, and tokyo.example.net respectively as their domains. More likely than not you would have custom preseed options you would want to set for each of the different data centers, so you could then put these custom options in ny.example.net.cfg, london.example.net.cfg, and tokyo.example.net.cfg on the same server as your generic preseed.cfg file. Then in your preseed.cfg file you could add

```
d-i preseed/include_command \
string echo `hostname -d`.cfg
```

The hostname -d command will output a host’s domain name, so if a host in New York’s fully qualified domain name is web1.ny.example.net, then hostname -d would output ny.example.net. Our preseed command would then echo ny.example.net.cfg.

# Run Custom Commands During the Install

If you find yourself writing longer and longer one-liners into the include_command option, you will definitely want to look into some of the other preseed options that allow you to run entire scripts. There are three different preseed options that allow you to execute commands within the installer environment.

The first option I will mention is in a way an extension of the include options. Where those options allowed you to list an additional preseed file to download and read in, the preseed/run option will instead download and execute a script of your choice:

```
d-i preseed/run string command.sh
```

This command.sh script could perform all of the shell logic you might have used before in include_command, only now it’s much easier to organize. You can even read and set preseed values within your script. Just use the debconf-get and debconf-set commands to get and set different preseed settings for your install. For instance, if I wanted to retrieve the preseeded hostname, I could run