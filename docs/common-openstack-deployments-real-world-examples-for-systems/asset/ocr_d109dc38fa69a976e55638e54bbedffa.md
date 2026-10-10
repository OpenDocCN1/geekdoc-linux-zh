geographically. A node in Europe will have different NTP and DNS servers than a node in the Americas. Read more about the power of Hiera at https://docs.puppet.com/hiera/1/.

# Passwords in Hiera

Another issue you will need to solve is storing passwords in Hiera. Checking passwords into git unencrypted is not a good idea and is unsafe. Using the hiera-eyaml back end is one solution to this problem. The passwords will be encrypted on disk and decrypted for catalog compiles (see: https://puppet.com/blog/encrypt-your-data-using-hiera-eyaml). This has the drawback that your Puppet master will need a decryption key but is a large improvement over plain text. There are other solutions to consider as well. Just keep in mind that managing passwords that hold the keys to your entire deployment should be a top consideration. Hiera includes passwords for the OpenStack admin user, RabbitMQ, and MySQL, any of which, if leaked, would be extremely dangerous.

# Node Classification

As noted earlier, in this book you are choosing what type of node you have by manually running puppet apply on a given box. This method does not scale well and is error prone. What would happen to your OpenStack cluster if someone accidentally applied the foundations\_public\_cloud.pp catalog to a compute host? In order to run this (production you need to first think about how you will do your Puppet node classification (https://docs.puppet.com/pe/latest/puppet\_assign\_configurations.html). This can be done using the Puppet console that ships with Puppet Enterprise (paid), but it can also be done with Hiera and the site.pp file. This is something you’ll need to consider as you productize this code.

# Module Management

One major consideration will be how you manage Puppet modules and stay in-sync with upstream. The versions of the modules are managed by the Puppetfile and then pulled by the Puppet deployment toolset r10k. For the most part, the Puppetfile shipped with this book puts you in good shape. Versions of non-\*OpenStack modules are locked to specific tags, which means that their code cannot "move" unless you move it. But new modules are tagged and released every day. In fact, many of the tags in that Puppetfile are probably already outdated. What system will you have for updating those tags and tracking new releases? How will you test the new modules? These are key considerations that you will need to make. I advise that falling behind and then trying to do a massive jump on all the modules at once is not a good plan. Plan on reviewing the module tags at least every few months to see if they can be upgraded. The following is an example of a module pinned to a tag:

```
```
mod 'stdlib'
  :git => 'https://github.com/puppetlabs/puppetlabs-stdlib.git'
  :ref => '4.6.0'
```
```