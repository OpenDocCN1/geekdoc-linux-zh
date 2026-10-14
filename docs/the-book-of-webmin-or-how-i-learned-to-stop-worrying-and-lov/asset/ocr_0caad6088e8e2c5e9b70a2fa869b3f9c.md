cache.log, and store.log. As mentioned previously, I usually place my Squid2 logs into /var/log/squid2, so this directory must be created with ownership by the same user and group names that Squid runs under (squid:squid on Red Hat Linux).

Finally, copy your Squid start-up script to a new location and modify it to call Squid with the new configuration file and check against the new PID file. For example, on my Red Hat system I would copy /etc/rc.d/init.d/squid to /etc/rc.d/init.d/squid2. You can now configure access controls in Webmin to allow access to separate administrators for each Squid process or further modify the Squid2 configuration to provide different functionality than the primary Squid process.

# Delete Modules

In this section, you may select any modules that you'd like to delete from your Webmin installation. Beware that using this form will delete the selected modules entirely from the system. If you decide later to use a deleted module, you will have to download the module again and reinstall it. It is usually a better idea to simply remove the module from each users access list (possibly even including root), rather than deleting the module here. However, if disk space is a concern, you can use this to delete all unneeded modules from your system.

# Operating System

Webmin knows how to interact with your system based on configuration files for each module that are selected based on the operating system configured here. If your system has Webmin preinstalled, you usually will not need to concern yourself with this. But if you upgrade your system, and the new version moves some configuration files to new locations, updating this may be necessary. On this page you may also set the search path for both programs (like system commands) and for libraries (such as for the password encryption library). Again, these options rarely need to be changed unless you have installed system tools and configuration files in odd locations on your system.

> NOTE In current versions of Webmin, at least up to 1.020, changing the OS does not alter existing module configuration files and will only apply to newly installed modules. A future version will likely alter this behavior to modify the already installed module configurations only if they have not been altered by the user.

# Language

Webmin supports a large number of languages for titles and module text. This page allows you to choose the language of your Webmin. New languages are being added regularly. Users of languages that are not supported are encouraged to write a translation and send it to the author of Webmin. He's always happy to receive new translations, and users are always happy to find that their native language is one that is provided with the distribution.