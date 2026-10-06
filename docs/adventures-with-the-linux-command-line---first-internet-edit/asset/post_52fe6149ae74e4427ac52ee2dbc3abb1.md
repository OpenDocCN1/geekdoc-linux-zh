
```bash
install() {
  if [[ -z "$1" ]]; then
    echo "Usage: install package..." >&2
    return 1
  elif [[ "$1" = "-h" || "$1" = "--help" ]]; then
    echo "Usage: install package..."
    return
  elif [[ -x /usr/bin/apt ]]; then
    sudo apt update && sudo apt install "$1"
    return
  elif [[ -x /usr/bin/apt-get ]]; then
    sudo apt-get update && sudo apt-get install "$1"
    return
  elif [[ -x /usr/bin/yum ]]; then
    sudo yum install "$1"
  fi
}

# Perform a system update
# Supports Debian, Ubuntu, CentOS, Arch

update() {
  if [[ -x /usr/bin/apt ]]; then # Debian, et al
    sudo apt update && sudo apt upgrade
    return
  elif [[ -x /usr/bin/apt-get ]]; then # Old Debian, et al
    sudo apt-get update && sudo apt-get install
    return
  elif [[ -x /usr/bin/yum ]]; then # CentOS/Fedora
    sudo yum update -y
    return
  elif [[ -x /usr/bin/pacman ]]; then # Arch
    sudo pacman -S
  fi
}

# Display distro release (prints OS name and version)

version() {
  local s
  for s in /etc/os-release /etc/debian_release /etc/centos-release /etc/fedora-release; do
    [[ -r "$s" ]] && cat "$s"
  done
}
```

## Ever Wonder Why it is Called .bashrc?

In various windings around Linux we encountered files that end with the mysterious suffix "rc" like .bashrc, .vimrc, etc. Many distributions have a bunch of directories in /etc named rc. Why is that? Its a holdover from ancient Unix. Its original meaning was "run," but it later became "run-control." A run-control file is generally kind of script or configuration file that prepares an environment for a program to use. In the case of .bashrc for example, it is a script that prepares a user's bash environment.

## Security Considerations and Other Subleties

Even though sourced files are not directly executable, they contain code that will be executed by anything that sources them. It is important, therefore, that permissions be set to allow writing only by their owners.

```
me@linuxbox:~$ sudo chmod 644 /etc/bashrc.cfg
```

While bash, ksh, and zsh all have the source builtin, dash and all strictly POSIX compatible shells support only the single dot (.). If the name argument given to source does not contain a / character, the directories listed in the PATH variable are searched for the specified file. For security reasons, it’s probably not an idea to rely on it. Always specify an explicit path.

Another subtlety has to do with positional parameters. source executes its commands in the current shell environment, this includes the positional parameters script was given as well. This is fine in most cases; however, if source is used within a shell function and that function has its own positional parameters, source will ignore them and use the shell’s environment instead. To overcome this, positional parameters may be specified after the file name. Consider the following script:

```bash
#!/bin/bash

# foo_script
source ~/foo.sh

foo() {
  source ~/foo.sh
}
```

foo "string2"

foo.sh contains this one line of code:
echo $1

We expect to see the following output:
me@linuxbox: ~ foo_script string1
string1
string2

But, what we actually get is this:

```
me@linuxbox:~$ foo_script string1
string1
string1
```

This is because source uses the shell environment script was given, not the one that exists when the function is called. To correct this, we need to write our script this way:

```bash
#!/bin/bash

# foo_script

source ~/foo.sh

foo() {
  source ~/foo.sh "$1"
}

foo "string2"
```

By adding the desired parameter to the source command within the function foo, we are able to get the desired behavior. Yes, it's subtle.

## Summing Up

By using source, we can greatly reduce the effort needed to maintain our bash scripts particularly when we are deploying them across multiple machines. It also allows us to effectively reuse code with function libraries that all of our scripts can share. Finally, we can use source to build much more capable shell environments for our day to day command line use.

## Further Reading

- Wikipedia article on the dot command from which the source builtin is derived: https://en.wikipedia.org/wiki/Dot_(command)
- Another article about run-commands: https://en.wikipedia.org/wiki/Run_commands

## 12 Coding Standards Part 1: Our Own

Most computer programming is done by organizations and teams. Some programs are developed by lone individuals within a team and others by collaborative groups. In order to promote program quality, many organizations develop formal programming guidelines called coding standards that define specific and stylistic coding practices to help ensure quality and consistency.

In this adventure, we are going to develop our own shell script coding standard to be known henceforth the LinuxCommand Bash Script Coding Style Guide. The source adventure is a necessary prerequisite for this adventure.

Roaming around the Internet, we can find lots of articles about "proper" shell script standards and practices. Some are listed in the "Further Reading" at the end of this adventure. While the scripts presented in TLCL do not follow any particular standard (instead, they present common practice from historical perspectives), let's follow some ideas:

- Write cleanly and simply.
- Document your work.
- Be careful and defensive.
- Anything that can go wrong, eventually will.
