Otherwise, the file is downloaded to the current directory. Recall the danger of storing extensions in your home directory.

# Local Access with the Command Line

The second tool is the `mydsl-load` command. Running `mydsl-load xmahjongg.uci` loads the named extension (in this example, `xmahjongg.uci`). You may also use a full path name to manually load extensions this way. This command is rarely used except in conjunction with the above `mydsl-wget`. It could be used in a scripted way, but with all the boot time load options, it is usually not needed.

# SETUP AND USAGE ERRORS

As I stated early on, the community of DSL users creates the collection of MyDSL extensions. The extensions are not an official part of DSL. Only the infrastructure to support for MyDSL is official. Having said that, the community of users is also responsible for the updates and corrections of any problems associated with the extensions.

Sometimes, your system may be impacted when using an extension. If you have just downloaded the extension, a reboot will eliminate it. If the extension is already in a persistent store and part of your automatic loading, you need to remove it.

There are situations when the infrastructure does not seem to be working correctly. Typically, I have found the following to be common situations:

+   - **Nothing happens or a blank screen**—Check that you have a working Internet connection. Also check that you can access the chosen download mirror.

+   - **Please mount media containing optional dir and try again**—This message usually occurs when running DSL in `toram` mode. When running in `toram` mode, the media is unmounted for removal. If there was an optional directory on such media, the submenu for their installation expects the media to be mounted for access to the stored extensions. This message may also appear when manually downloaded extensions are corrupt, or when system memory may not be sufficient to support all the loaded extensions.

+   - **Non DSL User error message**—This appears when extensions are trying to be loaded by anyone except the default DSL user. As I have said many times, the extensions are designed for live CD and therefore the single default DSL user. The exception to this is the command-line-only installation as previously discussed.