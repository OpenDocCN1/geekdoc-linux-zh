# Part 5: Programming in Ubuntu

You can test the Ruby on Rails installation by checking the versions installed. Open a Terminal session by selecting Applications ⇨ Accessories ⇨ Terminal from the Panel menu, and then enter the command:

```
```text
$ ruby -v
ruby 1.8.7 (2008-08-11 patchlevel 72) [i486-Linux]
$
```
```

This output shows that Ruby is installed and ready to go.

![](bbox=[0.108, 0.246, 0.226, 0.384])

> **Secret**
> 
> There is currently a disagreement between the Debian developers and the Ruby developers about the best way to install and update Ruby on Debian-based Linux systems (which is what Ubuntu is). The Ruby application comes with its own installer and updater program, called gems. Unfortunately, if you install or update Ruby programs using gems, those programs won't appear in the Debian software installation database, nor will they be automatically updated by the Synaptic updater. However, if you install Ruby via the Ubuntu Synaptic Package Manager, you're not guaranteed to get the latest version of Ruby available—only what's been added to the Ubuntu repositories.
> 
> The Ubuntu repositories have been doing a fairly decent job of keeping up with Ruby development, but the repositories don't always contain the latest release. If you're not concerned about working with the absolute latest version of Ruby, using the Synaptic Package Manager is a perfectly valid (and the easiest) way to install Ruby on your Ubuntu system. If you want to work with the latest version of Ruby, here's the recommended way:

+   1. **Install only the `ruby` package** from the Synaptic Package Manager.
+   2. **Download the latest version of gems** directly from the Ruby web site:
+      `http://rubygems.org`
+   3. **Install the latest version of gems you downloaded:**
+      ```text
+      tar zxvf rubygems-1.3.1.tgz
+      cd rubygems-1.3.1
+      sudo ruby setup.rb
+      cd ..
+      rm -r rubygems-1.3.1
+      ```
+   4. **Update Ruby and gems** using gems:
+      ```text
+      sudo gem update --system
+      ```
+   5. **Install Rails using gems:**
+      ```text
+      sudo gems install rails
+      ```

This procedure installs the latest versions of Ruby and Rails available, directly from the Ruby software repository. Because the Ruby installation is no longer part of the Debian software database on your system, the Synaptic Package Manager will not be able to maintain it. You'll have to manually update Ruby and Rails using the gems update command from time to time.