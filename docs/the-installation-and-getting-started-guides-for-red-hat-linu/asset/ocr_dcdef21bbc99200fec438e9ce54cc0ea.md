button, releasing the pressure (and the package) once you're over the Install window. You'll see a progress indicator when your package is being installed.

# Configuration

GnoRPM offers a wide selection of choices for installing and uninstalling packages, documentation and other features. You can customize GnoRPM through the Preferences dialog, which you can access from Operations -> Preferences on the menu. To make selections in the Preferences dialog, select the check boxes next to the options. Under the Behavior tab, you'll find a number of options for configuring the way GnoRPM installs, uninstalls and upgrades packages. The Behavior tab is split into five sections: Install, Upgrade, Other, Database and Architecture. Note that by default these boxes are not checked. Under Install Options, you have the following choices:

+   - No dependency checks - When selected, this will install or upgrade a package without checking for other types of files on which the program may be dependent in order to work. However, unless you know what you're doing we strongly suggest you not use this option as some packages may depend on other packages for files, libraries or programs to function correctly.
+   - No reordering - This option is useful if RPM is unable to change the installation order of some packages to satisfy dependencies.
+   - Don't run scripts - Pre- and post-install scripts are sequences of commands that are sometimes included in packages to assist with installation. This check box is similar to the --noscripts option when installing from the shell prompt.

Under Upgrade Options, you can select the following:

+   - Allow replacement of packages - Replaces a package with a new copy of itself. Similar to the --replacepkgs option from the shell prompt. This option can be useful if an already-installed package has become damaged or may require other repair to function correctly.
+   - Allow replacement of files - Allows the replacement of files which are owned by another package. The shell prompt equivalent for this RPM option is --