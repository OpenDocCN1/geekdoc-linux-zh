# 03  Installation on agents and post-installation

On all the agent nodes, you now need to run the following command:

```
`$ sudo apt-get install puppet`
```

This will install Puppet and an init script (`/etc/init.d/puppet`) for running the Puppet agent daemon. With this, we complete the installation process but Puppet is not started yet. Let's now configure the master and the agents, so they can talk to each other as and when required. The first step in this process is to set the master's name and certificates. You will need a DNS server that can resolve the names to corresponding IP addresses, then in the main section of the master's `puppet.conf` file, set the `dns_alt_names` setting to a comma separated value of each hostname that master can have. The default name to which an agent will try to connect is **puppet**. So, if you use "puppet" as the hostname for master, it will save you some effort. This is one of the most important steps and should be done carefully to avoid communication issues at later stages.

# 04  Activate certificates

The next step is to activate the certificates on the master. If this is the only Puppet master in your deployment, or if it will be acting as the CA server for a multi-master site, you should now run the following:

```
`$ sudo puppet master --verbose --no-daemonize`
```

This will create the CA certificate and the Puppet master certificate, with the appropriate DNS names included. As soon as the terminal output displays:

> Notice: Starting Puppet master version 3.8.3.

...kill the process by typing Ctrl+C, because we don't want the master to run. Now put all the Puppet manifests and modules in place and then configure a web server if you are planning to use Puppet to manage configuration loads.

# 05  Configure the agent

First of all, you will need to configure the `puppet.conf` settings in each of the agent nodes so that they are able to connect to your Puppet master server. Also, certain environment-specific factors should be changed according to your infrastructure requirements. Then you will need to start the Puppet agent service. You can either configure it to start on boot or set up a cron job, so that it runs at specific intervals. To start the Puppet service, type:

your infrastructure requirements. Then you will need to start the Puppet agent service. You can either configure it to start on boot or set up a cron job, so that it runs at specific intervals. To start the Puppet service, type:

```
`$ sudo puppet resource service <NAME>
ensure=running enable=true`
```

Then configure the cron job using:

```
`$ sudo puppet resource cron puppet-agent \
ensure=present user=root minute=30 command=/usr/\
bin/puppet_agent --onetime --no-daemonize --play`

The final step is to sign the certificates for each of the agent nodes. Note that in an agent/master deployment, an admin must approve a certificate request for each agent node before the node can fetch configurations. Agent nodes will request certificates the first time they attempt to run. To approve the requests, log on to the Puppet master server and view outstanding requests using:
```

```
`$ sudo puppet cert list`
```

Then sign a request by typing:

```
`$ sudo puppet cert sign <NAME>`

You can also sign all the requests in one go using:
```

```
`$ sudo puppet cert sign --all`

With this, the agent nodes are now ready to communicate with the master. Puppet also enables a higher level of configuration by letting you classify the nodes. With this, you can determine which agent nodes receive which information from the master.
```

![](bbox=[0.46, 0.16, 0.8, 0.44])

![](bbox=[0.08, 0.16, 0.41, 0.32])

# Run when file updates

You can run a command automatically whenever a file changes. Just use an exec resource with `refreshonly` set to `true`, for example:

```
```
file { "/etc/bind: \
source => "/dist/apps/ \
bind" }

exec { "/usr/bin/ndc \
reload: \
subscribe => File["/ \
etc/bind"], \
refreshonly => true \
}```
```

![](bbox=[0.82, 0.16, 0.94, 0.44])