```
```
Redis server v=6.0.16 sha=00000000:0
memic=jemalloc-5.2.1 bits=64
buildId=828defb5a45b9b2a8d
```
```

Lastly, you need to verify that the Redis service is working properly. Enter the following command:

```
`$ redis-cli ping`
```

which should result in PONG as the response.

# ## NetBox and Dependencies

You will need to also install the NetBox dependencies (as shown in Figure 3) using:

```
```
$ sudo apt install -y python3
python3-pip python3-venv python3-dev
build-essential libxml2-dev
libxslt1-dev libffi-dev libpq-dev
libsasl2-dev zlib1g-dev git
```
```

Double-check that you have at least version 3.8 of Python [7] installed by running:

```
`$ python3 -V`
```

Now you need to create the installation directory and cd (change directory) into it and download NetBox with:

```
```
$ cd ~
$ sudo mkdir -p /opt/netbox/
$ cd /opt/netbox/
$ sudo git clone -b master --depth 1
https://github.com/netbox-community/netbox.git .
```
```

# ## Configuration

If you read the NetBox documentation, you will notice that my configuration instructions vary somewhat from the documentation. The documentation does mention doing what I recommend, but it doesn't make it obvious, so I will try to make these steps a bit easier to understand.

# ### Listing 1: Modifying Database Parameters

```
```
DATABASE = {
    'ENGINE': 'django.db.backends.postgresql',    # Database engine
    'NAME': 'netbox',                            # Database name
    'USER': 'netbox',                            # PostgreSQL username
    'PASSWORD': 'SuperSecurePassword',            # PostgreSQL password
    'HOST': 'localhost',                         # Database server
    'PORT': '',                                   # Database port (leave blank for default)
    'CONN_MAX_AGE': 300,                         # Max database connection age (seconds)
}
```
```

Note: The period (.) at the end of the last command is required for the command to work properly.

Next you need to create the NetBox user and change ownership of the installation directory to that user with:

```
```
$ sudo adduser --system --group netbox
$ sudo chown --recursive netbox
/opt/netbox/netbox/media/
```
```

First, I'll edit the NetBox configuration file using Cockpit [8] on Ubuntu Server (see the "Config Editors" box as follows:

```
```
$ cd /opt/netbox/netbox/netbox/
$ sudo cp configuration_example.py configuration.py
$ sudo nano configuration.py
```
```

# ### Config Editors

I did the install for this article using Cockpit on Ubuntu Server because (in my experience) it makes administration very easy. I installed a 45Drives add-on for Cockpit called cockpit-navigator, which greatly improves running servers in general, especially if you need to edit lots of config files and create configs from templates and perform other common configuration actions regularly. You can also do all this in the terminal (which Cockpit also includes) if you prefer to use something like nano [10] or Vim [11].

![](bbox=[0.08, 0.63, 0.92, 0.9])

**Figure 4:** You can edit configuration.py with Navigator from 45Drives in Cockpit to set up NetBox if you prefer a graphical editor.