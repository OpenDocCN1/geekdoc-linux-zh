...and then variations on her first name There is a very good chance that the target’s password is among this custom made password list.

# # Hashcat

Combining the outputs from cewl , crunch, and cupp (the three C’s) to create a custom list is an effective strategy in many cases, but what if none of these work and you need to brute force the password? This is where pure speed is critical.

Hashcat is among the fastest and most sophisticated password crackers. In addition, it enables us to use the GPU on our graphics card which is much faster than our CPU for password cracking.

134 | P a g e

```
```
root@kali-2019:~# hashcat --help
hashcat - advanced password recovery

Usage: hashcat [options]... hash[hashfile]...|hccapxfile [dictionary][mask][directory]...

- [ Options ] -

Options Short / Long    | Type | Description                                  | Example
====================================================================================================
-#, --hash-type        | Num  | Hash-type, see references below              | -m 1000
-0, --attack-mode      | Num  | Attack-mode, see references below            | -a 3
-V, --version          |      | Print version
-h, --help             |      | Print help
     --quiet            |      | Suppress output
     --hex-charset      |      | Assume charset is given in hex
     --hex-salt         |      | Assume salt is given in hex
     --hex-wordlist    |      | Assume words in wordlist are given in hex
     --force            |      | Ignore warnings
     --status           |      | Enable automatic update of the status screen
     --status-timer     | Num  | Sets seconds between status screen updates to X    | --status-timer=1
     --stdin-timeout-abort| Num | Abort if there is no input from stdin for X seconds | --stdin-timeout-abort=300
     --machine-readable |      | Display the status view in a machine-readable format
     --keep-guessing    |      | Keep guessing the hash after it has been cracked
     --self-test-disable|      | Disable self-test functionality on startup
     --loopback         |      | Add new plains to input directory
     --markov-hcstat2  | File | Specify hcstat2 file to use                  | --markov-hcstat2=my.hcstat2
     --markov-disable  |      | Disables markov-chains, emulates classic brute-force
     --markov-classic  |      | Enables classic markov-chains, no per-position
-t, --markov-threshold | Num  | Threshold X when to stop accepting new markov-chains| -t 50
     --runtime           | Num  | Abort session after X seconds of runtime     | --runtime=10
     --session           | Str  | Define specific session name               | --session=mysession
     --restore           |      | Restore session from --session
     --restore-disable   |      | Do not write restore file
     --restore-file-path | File | Specify path to restore file                 | --restore-file-path=xs.restore
     --outfile           | File | Define outfile for recovered hash          | -O outfile.txt
     --outfile-format    |      | Define outfile-format X for recovered hash | --outfile-format=7
     --outfile-autohex-disable|  | Disable the use of [HEX] in output plains
     --outfile-check-timer| Num | Sets seconds between outfile checks to X     | --outfile-check=30
     --wordlist-autohom-disable|  | Disables the conversion of [HEX] from the wordlist
-p, --separator         | Char | Separator char for hashlists and outfile   | P :
     --stdout            |      | Do not crack a hash, instead print candidates only
     --show              |      | Compare hashlist with potfile: show cracked hashes
     --left              |      | Compare hashlist with potfile: show uncracked hashes
     --username          |      | Enable ignoring of usernames in hashfile
```
```