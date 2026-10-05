lib: Library routines

include: Header files

samples: Prototype scripts and configuration files

site: Where user-editable site configuration files are stored before being
cied out to the actual news directory for implementation

doc: Manual pages

config: Tools to aid in site configuration

Take this opportunity to apply any patches to the software, and be sure to
look through the README files, FAQ, Install files, and other pertinent doc-
mentation before attempting to configure and install INN. Pay special
tention to section 2 of the FAQ where it talks about Linux-specific tips and
problems.

# 10.3 Compiling and Installing INN

Unlike gnu utilities, INN has no autoconfiguration scripts, so all param-\eter settings must be done by editing the config files and setting the parame-
by hand. INN has built-in steps, with the first section being the "sub"
program, located in the config directory. In this version of INN, subst comes
as a shell script or C source. Unless problems occur, using the shell script ver-
s of subst is usually easiest, but the C version is often faster. To test the
sub program the following:

```
$cd INNSRC/config
$cp ../sample-configs/config.data-linux-<version number> config.data
$chmod 644 config.data
customize config.data
$make sh
```

If you receive errors and the shell script was used, compile the C version
and try again. If all goes well, subst works the true configuration can
now be done by editing the global configuration file, config.data. The con-
fig.data file uses the "#" character as comment line and the file format is
follows:

```
<parameter><one-or-more-tabs><value>
```

Even if there is no <value>, the <one-or-more-tabs> is still required to
avoid syntax errors.