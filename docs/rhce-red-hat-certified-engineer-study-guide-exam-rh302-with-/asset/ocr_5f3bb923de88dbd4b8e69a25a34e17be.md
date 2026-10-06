A related flag, -F, lets you update a package only if it's present. For example, the command

rpm -Fvh gnorpm-0.9-10.i386.rpm

would update the gnorpm package only if the package is installed. The -F flag helps you keep your system current. Red Hat maintains a list of updated packages at www.redhat.com/support/errata. You should monitor the list and apply any fixes that you believe are important to the operation of your system using the -F flag.
Now, complete Exercise 12.3, which requires you to update an RPM package.

EXERCISE 12.3

Updating a Package
As explained, a diligent system administrator monitors the Red Hat Errata page and timely applies useful fixes. To check your ability to do so, use the rpm command to update a package with fix downloaded from the Red Hat Errata page. You can consult this chapter for help during the exercise, but bear in mind you won't have this opportunity during the RHCE exam.

# Identifying Installed Packages

You can use RPM to learn the version and build numbers of an installed package. To do so, issue a command of the form

rpm -q package_name

where package_name is the name of the installed package. The output consists of a single line that gives the package name, version number, and build number—example:
\gnorpm-0.9-10

To learn the version and build number of each installed package, issue the command

rpm -qa