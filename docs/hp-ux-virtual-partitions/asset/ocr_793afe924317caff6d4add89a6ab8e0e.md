# hpx

hpx - Boot HP-UX operating system.

hpxux(1M)	hpxux(1M)

# NAME

+   •	*hpx* - HP-UX bootstrap

# SYNOPSIS

```
hpx [-P] [-lm] [-a[C|R|S|D] devicefile] [-fn]umber] [-istring] [boot] [devicefile]
hpx ll [devicefile] (same as hpx ls -aflm)
hpx ls [-a]in] [devicefile]
hpx set autofile devicefile string
hpx show autofile [devicefile]
hpx -v
hpx restore devicefile (Series 700 only; see DEPENDENCIES.)
```

# DESCRIPTION

*hpx* is the HP-UX specific secondary system loader (SSL) utility for bootstrap (see isli(M) for the initial system loader). It supports the operations summarized below, as shown in the SYNOPSIS and detailed later in this DESCRIPTION.

+   *boot*	Loads an object file from an HP-UX file system or raw device and transfers control to the loaded image. (Note: the boot operation is position dependent.)

+   *ll*	Lists the contents of HP-UX directories in a format similar to `ls -aflm`. (See `lsli`; `ls` only works on a local disk with a HFS file system.)

+   *ls*	Lists the contents of HP-UX directories. (See `lsli`; `ls` only works on a local disk with a HFS file system.)

+   *show autofile*	Displays the contents of the autoexecute file.

+   *set autofile*	Changes the contents of the autoexecute file to that specified by *string*.

+   *-v*	Displays the release and version numbers of the hpx utility.

+   *restore*	Recovers the system from a properly formatted bootable tape. (Series 700 specific; see DEPENDENCIES.)

hpx commands can be given interactively from the keyboard, or provided in an isil autoexecute file.

hpx is limited to operations on the interface initialized by pdc(1M). In most cases, operations are limited to the boot device interface.