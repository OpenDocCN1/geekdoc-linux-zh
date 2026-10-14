
2. The `apt-cache search` command can be used to search through the list of available software. To search for Frozen-Bubble, something similar to the following could be typed:

- `apt-cache search frozen bubble`

Here’s what I see on my test system:

```text
fb-music-high - High quality, large music files for Frozen-Bubble
fb-music-low - Lower quality, small music files for Frozen-Bubble
frozen-bubble - Pop out the bubbles!
frozen-bubble-data - Data files for Frozen-Bubble
pengupop - Online multiplayer clone of Bust a Move
```

3. To view complete details about any package, use the `apt-cache show` command; for example:

- `apt-cache show frozen-bubble`

The information provided can scroll off the screen so it’s often useful to pipe it into the less text viewer, for easy reading (i.e. `apt-cache show frozen-bubble | less`).

4. Once you’ve found the name of the correct package, the `apt-get install` command can be used to install it; installing software requires root powers, so the command must be preceded with `sudo`:

- `sudo apt-get install frozen-bubble`

If no dependencies are required, the package will be downloaded and installed instantly. If dependencies are required, which is likely, they will automatically be added to the list of files to be downloaded and installed. A summary will be shown to which you can type Y, to agree, or N, to cancel software installation.

Assuming you agree, the software will be downloaded and installed. Progress will be displayed as it happens.

Sometimes certain system configuration tasks might be carried out during the installation of software packages. For example, if you choose to install a new package containing fonts, the system font caches will probably be refreshed. Such tasks happen automatically and, if Synaptic is used, are usually hidden from view. However, when installing at the command-line you'll see each task complete. Usually there is nothing about which to be concerned. If any administrative task has even the possibility of damaging the system, or changing a vital setting, you'll be prompted to confirm that you wish it to run.

## Uninstalling software

Removing software is just as easy as installing software, and all you need is the name of the package. If you've forgotten what this is, you can once again use apt-cache search to find it.

Following this, use the apt-get autoremove command—the following will uninstall Frozen-Bubble:

- sudo apt-get autoremove frozen-bubble

You'll be shown a list of the packages to be removed (that will include any redundant dependencies), and asked to confirm your decision by hitting Y or N.

> NOTE Only unused dependencies will be marked for removal. This might vary from the list of dependencies that were originally installed. This disparity occurs because other software you've installed since also requires the dependencies.

## Reinstalling software

To refresh a package that's already installed, type the following, replacing packagename with the name of the program as it is listed in Synaptic or via apt-cache search:

- sudo apt-get --reinstall install packagename

If the package isn't already present in the system's package cache (located at /var/cache/apt/archives), it will be downloaded afresh.

## Manually installing/uninstalling packages

If you find yourself having to install a package manually, the dpkg command can be used. The -i command option is used to install and the -r option can be used to remove packages, as follows:

- sudo dpkg -i packagename.deb

- sudo dpkg -r packagename

> NOTE Once a package is installed using dpkg, it can also be removed using the apt-get autoremove command.

The full filename of the package file must be specified when installing.

This isn't necessary for removal of the software. Instead, you need only refer to the package by its "short name"—how it appears in the list of packages provided by Synaptic or apt-cache search.

TIP The short name is usually the first part of the package's filename.

To see the full description contained in a downloaded package file, that includes a list of the dependencies it requires, use the -I command option (pipe the output to less because otherwise it will scroll off the screen):

- dpkg -I packagename.deb | less

To see if a package is installed—useful for checking if the required dependencies for a package are met—use the -l command option with dpkg (that's lower-case L), and specify the package's short name. If the package isn't installed, you will see "No packages found". If it is installed you will see a table showing the package version number and sundry details.

## Installation limitations

Because of dependency issues, restrictions are placed on how dpkg works when installing/removing software. This protects the system from damage.

If you attempt to install a package that requires dependencies that aren't already installed, you'll be told what they are. The software will then be installed but won't be configured for use. This means that, essentially, the program files are in place, but any vital system tweaks necessary for the program to work correctly haven't been carried out.

A package installed without dependencies is known as a broken package. Installing a broken package will leave the package management system in a damaged state; apt-get will refuse to work until the dependencies are met or the errant package is uninstalled, while Synaptic will automatically insist on removing the package before allowing any further package installation.

TIP If the dependency packages are available in the repositories, it's possible to fix the situation at the command-line by typing sudo apt-get -f install. This will download the dependencies, install them, and configure the broken package for use.

## Uninstallation limitations

If you attempt to use dpkg to uninstall a package that is a dependency of other packages, you simply won't be allowed. Instead, you'll be told what other programs depend on that package, and you must manually
