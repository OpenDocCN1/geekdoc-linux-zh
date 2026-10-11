![](bbox=[0.106, 0.197, 0.367, 0.322])

![](bbox=[0.386, 0.195, 0.9, 0.535])

# 01 Install Capistrano

# 03 On the server

Essentially, Capistrano copies your app from Git, over SSH, to your server and takes care of all the operations you'd have to do if you were to move the files by hand. Capistrano will deal with any database migration, changes to files and file names, restarting the web server and so on. Installing Capistrano, and the extras package which is nice to have, is as simple:

```
gem install capistrano
```

Any problems, check your Ruby installation. The capistrano-ext gem you may see referred to elsewhere is no longer essential, as features like extra staging options have been integrated into the main codebase.

On your servers, you'll need a similar environment of rbenv, Git and your choice of Apache or Nginx. Use rbenv to grab the latest Ruby (or an earlier one if appropriate to your app):

```
rbenv install --list
rbenv install 2.1.3
```

You won't need unnecessary packages like Ruby documentation so when you come to install bundler, specify no docs:

```
gem install bundler --no-ri --no-rdoc
```

Better yet, put:

```
gem: --no-rdoc --no-ri
```

...in `/.gemrc`. You'll also need to set up the database - or separate database server - as required by your setup. A typical Rails use case is SQLite on the developer's laptop and PostgreSQL on the production servers.

include Capistrano and anything else you want. You'll want more gems. In your project's Gemfile:

```
gem "capistrano", "~> 3.2.1"
gem "capistrano-rails", "~> 1.1.2"
gem "capistrano-bundler" # if you are using RBENV
gem "capistrano-btm", "~> 2.0" # if you're using Unicorn app server
gem "unicorn"
# Otherwise gem "passenger" or "puma"
```

This will also integrate bundler with Capistrano. bundle install downloads the gems specified in your Gemfile and installs them.

The `~> 3.2.1` means that while 3.2.2 will be installed when it's released, 3.3.0 will not to avoid major version changes breaking your code.

# 02 SSH Keys

If you've been logging into your web server with a SSH password, it's time to generate keys. This is so that the login can be automated for Capistrano (or any other scripts you want) to use - it's a good idea to do this on any server. You'll also need it for your GitHub account if you are going to be setting one up. Start generating the keys with:

```
ssh-keygen -t rsa
```

...if you've not got one already in `~/.ssh` - and copy the `~/.ssh/id_rsa.pub` to the server with:

```
ssh-copy-id -i ~/.ssh/id_rsa.pub user@ 
remote-host
```

...which works by substituting your username, and servername or address.

# 04 Bundling gems

For a Rails project, you can skip the install step and simply edit your Gemfile to

![](bbox=[0.106, 0.546, 0.367, 0.636])

> “Capistrano will deal with any changes to files and file names”