Table 13.7 tiger Command-Line Options

| Option | Use |
|---|---|
| -v | Prints tiger version information. |
| -B | Specifies tiger base directory on the command line. |
| -1 | Specifies tiger log directory. |
| -w | Specifies tiger work directory. |
| -b | Specifies tiger binary directory. |
| -c | Specifies tigerrc file. |
| -e | Generates a verbose report (with full explanations inserted where each message ID appears). |
| -E | Produces a report similar to the default report, but generates a separate report that includes the full text of each message ID referenced in the output. |
| -S | Server check. Means check the server and the diskless clients configured on it. Probably doesn't work very well on systems other than SunOS 4. |
| -O | Specifies operating system. |
| -A | Specifies architecture. |
| -R | Specifies revision of OS. |
| -t | Specifies tiger test mode. |

# OVERVIEW OF RUN-TIME OPERATION

tiger comes preconfigured for a variety of operating systems. Much of this information is stored in the systems directory (and typically needs to be tinkered with only by developers). When you run tiger (or a stand-alone tiger script), the scripts/config executable tries to locate the most appropriate configuration files, but it will use more generic configuration information if it cannot locate exact matches. The configuration that it uses is reported at the beginning of the output. The config script also parses command-line options. An example of the output is shown in Example 13-3.

**Example 13-3** *tiger* Shows Which Configuration Files Were Used at Run-Time.

```
# scripts/check_perms
Configuring ...  
Will try to check using config for 'i686' running Linux 2.0.36 ...  
--CONFIG-- [con005c] Using configuration files for Linux 2.0.36.  
Using configuration files for generic Linux 2.  
Not all checks may be performed.
```