The two main changes to the function are

+   - A case statement sets the variable PSOPTS based on the operating system name.
+   - The STDERR of ps is redirected to /dev/null in order to discard the warning message generated on older versions of Linux.

# Linux ps

In Linux the ps command varies between different versions. In older versions of Linux 2.0, the hyphen in the -auxx command is not properly supported, whereas in current versions the hyphen is supported, as are the System V style -ef options. Taking this into account, you could modify the getPID() function as follows:

```
getPID() {
  if [ $# -lt 1 ]; then
    echo "ERROR: Insufficient Arguments." >&2
    return 1
  fi

  PSOPTS="-ef"
  case `getOSName` in
    bsd|sunOS|darwin)
      PSOPTS="-auxx" ;;
    linux)
      case `uname -r` in
        [01].*) PSOPTS="-auxx" ;;
        2.0*) PSOPTS="-auxx" ;;
      esac
      ;;
  esac

  `/bin/ps $PSOPTS | grep "$1" |`
  awk '/grep/ { next; } { print $2; }'
}
```

This version avoids having to redirect to /dev/null and allows you to detect any problems that might be reported by the ps command.

# Summary

In this chapter, you learned how to determine which version of UNIX is running using uname. In addition, you developed the getOSName and isNS$ functions to help adapt shell scripts to multiple versions of UNIX. You also looked at the following techniques for improving the portability of shell scripts:

+   - Conditional execution
+   - Abstraction