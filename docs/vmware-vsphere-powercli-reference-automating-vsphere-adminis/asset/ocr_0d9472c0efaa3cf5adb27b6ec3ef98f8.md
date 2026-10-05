during execution; it provides real-time feedback of results and variable values and is invaluable for debugging and troubleshooting.

There are two times when we can log data to a script. The first is logging the output of the script to a file so that it can be stored and retrieved at any time. The second is writing directly to a log file from inside a script to document actions and progress.

Logging all output from a script is accomplished using the Start-Transcript and Stop-Transcript cmdlets. Just as the name describes, everything that is output to the console to a file. The stop cmdlet ends this behavior. Let's look at an example of using Start-Transcript and Stop-Transcript (see Listing 25.6).

# LISTING 25.6 Starting and stopping transcript recording

```
# Frequently it's helpful to log to the same location as the script.
# Using this path variable we will log to a file in the same directory,
# with the same name, as the invoking script but ending with ".log"
Start-Transcript -Path $($($MyInvocation.Command.Definition).log"

# output something to the console
Get-VM | Where-Object {$_.PowerState -eq "PoweredOn"}

# stop writing to the transcript file
Stop-Transcript
```

If you check the contents of the file that was created, it will contain everything that was output by the command(s) executed. While logging console output via the script is helpful, sometimes you want more control over what is being logged and where it is being logged. To help with this, we have provided a function, shown in Listing 25.7, that can be included in your scripts and used as a convenient helper for logging messages with different priority.

# LISTING 25.7 TheNew-Log-Entry function

```
function New-Log-Entry {
    <#n    .SYNOPSIS
    Creates log entries in a file and on the console.

    .DESCRIPTION
```