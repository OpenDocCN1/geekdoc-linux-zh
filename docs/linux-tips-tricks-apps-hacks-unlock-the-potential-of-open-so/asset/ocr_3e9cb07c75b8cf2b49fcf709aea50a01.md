```
set :rbenv_type, :system # or :user
set :rbenv_ruby, "2.1.2"
set :rbenv_prefix, "RBENV_"
ROOT=(#{fetch(:rbenv_path)} RBENV_
VERSION=\"\#{fetch(:rbenv_ruby)\")
#{fetch(\"\#{rbenv_path}/bin/rbenv exec\
SET :rbenv_map_bins, %w(rake gem bundle
ruby rails)
```

# 11 Parallel lines

With the simple on/withd syntax of the Rake-derived DSL, flexible splitting of tasks across servers is easy. For example, to run something on every server at once:

```
on -all, in: parallel do
# parallel task here
end
```

Getting your servers to start a task in sequence, perhaps to avoid hitting a shared database, involves defining :sequence and then:

```
on -all, in: :sequence, wait: 15 do
# sequential code here
end
```

For a rolling restart of a large cluster, you can group servers together to go in parallel:

```
on -all, in: :groups, limit: 3, wait: 5 do
# Your rolling restart ...
end
```

You can see the parallel execution of code for different groups of servers in the Capistrano developers' example over at bit.ly/1FuodCh (look under “Parallelism”), which was developed specifically to replace the previous version's more hacky parallel do :session.

# 12 Off the Rails

There's plenty of documentation available out there to go beyond the simple introductions we give here. The Capistrano website (http://capistranorb.com) should be your first port of call, but you'll find docs elsewhere for integrating Capistrano with everything from Jenkins to Angular.js—just double check to make sure that you're reading something that has been updated for Capistrano 3. Integrating Capistrano's scripts for continuous deployment into a larger environment of a continuous integration server like Jenkins is easy enough—a job in Jenkins, as an example, has cap deploy as its build step (and your Git repository as its URL).

Away from Rails, gems exist that can ease deployment for most web platforms, from Sinatra to Django. For Drupal (with Drush and the CapDrupal gem) you can automate taking the site offline, backing up the database, cloning your new code and pointing the site root there, updating the database, and putting the site back online as well as all of the advantages of cap deploy/rollback.

# 09 Test and prepare

Setting tests will halt the deployment should tests fail.

```
# tests under lib/capistrano/tasks/
run_tests.cap
set :tests, []
```

Now edit the set :server_name and server lines in config/deploy/production.rb to your server's domain name.

We're about ready to deploy now. You could add a task deploy:setup_config to install the server software, and that would be desirable with a multi-server setup—but we're keeping things simple in this introduction, hence the earlier manual set up of the server.

# 10 Deploy

Now for deployment. Our config wound up the spring; to set the clockwork in motion we:

```
cap production deploy
```

For that to work first time, you'll have had to have done a bit of work on the config—beyond what we've specifically outlined in the case of many setups. Capistrano is designed to expand and stretch to cover all sorts of circumstances, and your app and server setup won't be exactly the same as anyone else's. Although that said, if you deploy to a large cloud provider then they may have Capistrano example configs you can copy. Capistrano's modularity and flexibility means there's a lot to explore to get it doing what you need. It is essentially a utility for running tasks, in parallel, across remote servers.

# SSHKit

The Capistrano 3 development process gave birth to the SSHKit library developed by Lee Hambley—who did much of the great work of making Capistrano 3 such an improvement over an already pretty powerful piece of code. SSHKit is a lower level toolkit that Capistrano uses for everything such as logging, formatting, connection management and pooling, parallelism, and batch execution. You too can use it for running commands in a structured way on one or more servers. Within Capistrano, you'll find SSHKit called upon most of the time you issue one). To use it yourself, start with some of the examples on the GitHub page and adapt for your site. Here SSHKit will build a path from the nested directives:

```
on hosts do
within "War" do
puts capture(\"pwd\")
within -log do
puts capture(\"pwd\")
end
end
end
```

Behind the scenes File.join() is taking care of the slashes for you to build the paths and it should return:

```
/var/
/var/log
```

![](bbox=[0.64, 0.63, 0.9, 0.9])