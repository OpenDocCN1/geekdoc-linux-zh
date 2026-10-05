# CHAPTER 9 • ADVANCED VIRTUAL MACHINE FEATURES

# TABLE 9.2 Regular expressions reference sheet

| Character | Definition | Example |
|---|---|---|n| (dot) | Matches any character. | "pos.* matches pos or posh but not. |
| + | Preceding item must match one or more times. | "pos.*+ matches posh or poshable but not pos. |
| * | Preceding item must match zero or more times. | "pos.** matches po and poss but not pos. |
| () | Creates a subset or group. | "po (sh)* matches po and creates two groups: po and sh. |
| [] | Matches one of characters enclosed. | "po[os]* matches po and po. |
| \s | A single whitespace character. | "pos\s matches po sh not pos. |
| \S | A single non-whitespace character. | "po\S* matches po and posh but not po. |
| \w | A single word character (alphanumeric, numeric, underscore). | "po\w* matches posh but not po$5. |
| \d | A single numeric character. | "pos\d* matches pos5 but not pos. |

Although seemingly daunting first, using simple regular expressions is critical to getting useful objects out of any text-based tools like SSH. Many online utilities can assist in developing regular expressions, but basic column matching can be done using nothing more than subgroups and the whitespace delimiter, \s|\S. As an alternative, you can offload more of the parsing work in the command passed over SSH. Which method you employ depends on your comfort level. There isn't a right way to do it. Feel free to use any skillset or tools to meet the needs.

# Using Windows Native Tools

There are two main ways to interact with the Windows OS: Windows Management Instrumentation (WMI) and PowerShell Remoting. WMI allows scripting languages like VBScript or Windows PowerShell to manage Windows systems, both locally and remotely. WMI is preinstalled in Windows 2000 and newer OSs. PowerShell's new way of interacting with remote systems and comes with PowerShell 2.0 or later. The drawbacks of both methods is that they require a network connection not be blocked by a company