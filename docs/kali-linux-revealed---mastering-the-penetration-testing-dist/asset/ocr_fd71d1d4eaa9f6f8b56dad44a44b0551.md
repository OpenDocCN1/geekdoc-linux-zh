A pre-dependency is very demanding for apt because it adds a strict constraint on the ordering of the packages to install. As such, pre-dependencies are discouraged unless absolutely necessary. It is recommended to consult other developers debian-devel@lists.debian.org before adding a pre-dependency as it is generally possible to find another solution as a work-around.

# Recommends, Suggests, and Enhances Fields

The Recommends and Suggests fields describe dependencies that are not compulsory. The recommended dependencies, the most important, considerably improve the functionality offered by the package but are not indispensable to its operation. The suggested dependencies, of secondary importance, indicate that certain packages may complement and increase their respective utility, but it is perfectly reasonable to install one without the others.

You should always install the recommended packages unless you know why you do not need them. Conversely, it is not necessary to install suggested packages unless you know why you need them.

The Enhances field also describes a suggestion, but in a different context. It is located in the suggested package, and not in the package that benefits from the suggestion. Its interest lies that it is possible to add a suggestion without having to modify the package that is concerned. Thus, all add-ons, plug-ins, and other extensions of a program can appear in the list of suggestions largely ignored by programs such as apt or synapticaptic. The original goal was to let a package like xul-ext-adblock-plus (a Firefox extension) declare Enhances: firefox, firefox-esr and thus appear in the list of suggested packages associated to firefox and firefox-esr.

# Conflicts: the Conflicts Field

The Conflicts field indicates when a package cannot be installed simultaneously with another. The most common reasons for this are that both packages include a file of the same name, provide the same service on the same transmission control protocol (TCP) port, or would hinder each other's operation.

If it triggers a conflict with an already installed package, dpkg will refuse to install a package, except the new package specifies that it will replace the installed package, in which case dpkg will choose to replace the old package with the new one. APT always follows your instructions: if you choose to install a new package, it will automatically offer to uninstall the package that poses a.