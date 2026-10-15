
## The Results

```
$ moonphase 08/03/2121
On 08/03/2121 the moon = 74% illuminated.

$ moonphase
Today the moon is 100% illuminated.

$ moonphase 12/12/1941
On 12/12/1941 the moon = 43% illuminated.
```

Listing B-6: Running the moonphase script

> NOTE December 12, 1941 is when the classic Universal horror film The Wolf Man was first released to movie theaters. And it wasn’t a full moon. Go figure!

## Hacking the Script

From an internal perspective, the script could be greatly improved by having a better error-checking sequence, or even by just utilizing Script #3 on page 17. That would let users specify dates in more formats. An improvement would be to replace the if/then/else statement at the end with a function that translates illumination level into more common moon phase phrases like “waning,” “waxing,” and “gibbous.” NASA has a web page you could use that defines the different phases: http://starchild.gsfc.nasa.gov/docs/StarChild/solar_system_level2/moonlight.html.

## INDEX

### Symbols and Numbers

- << notation, 35
- * (asterisk)
  - in cron entry, 157
  - for globbing files, 306, 346–348
- ^ operator, 87
- $() notation, 57, 66
- ${()} notation, 34–36
- . (period)
  - escaping for grep command, 70
  - for hidden files, 12
  - to source script, 43
- "404 Not Found" errors, preventing, 220
- 2001: A Space Odyssey (movie), 274
- archive
  - file, emailing or copying to cloud storage, 166
  - remote, for backups, 246–249
  - of removed files, 58–62
- archivedir script, 169–171
- area codes, looking up, 183–185
- askvalue() function, 148–149
- asterisk (*), in cron entry, 157
- Atkin, sieve of, 287
- automated screencapture, 263–266
- awk command, 98, 181
  - for disk capacity, 125–126
  - for displaying random text, 213–214
- general format for script, 189
- printf command, 39–34

### A

- -a (logical AND), 25–26
- access_log file, 235–239
  - splitting from error_log, 243
- Acey Deucey, 290–297
- addagenda script, 90–95
- adduser script, 131–133
- admin account, for apm, 226, 228
- agenda script, 90–95
- album script, 211–213
- aliases, 104
- alphanumeric input, validating, 15–17
- alternatives system (Debian), 104
- AND, logical (-a), 25–26
- ANSI color sequences, 40–42
  - for region highlighting, 107–109
- Apache web server
  - access_log file, 235–239
  - error_log file, 242–246
  - installing, 201
  - managing passwords, 223–229
- apm_footer.html, 227–228
- apm script, 223–229
- apt package manager, installing with, 201

### B

- backups
  - automated, based on sftp, 106, 229–233
  - of directories, 169–171
  - of files as they’re removed, 55–58
  - managing, 166–169
- .bash_profile (login script), 4–5, 12
- .bashrc (login script), 4–5, 12
- bash shell, 1–2
  - customizing, 4
  - installing on Windows, 341–344
  - running commands, 3–4
  - running shell scripts, 5–7
- batch files, 175
- bc program, wrappers for, 34–36, 82–85
- bestcompress script, 113–115
- Bitcoin, address information retrieval, 192–194
- blank phrase, vs. zero-character quoted phrase, 17
- bold type, 41–42
- border for image, 318–322
- brew package manager, installing with, 329
- broken internal links, identifying, 217–220
- bugs. See debugging
- bulkrename script, 346–348
- bulkrun script, 348–351
- bzip2, 109, 114

### C

- calc script, 82–85
- calculations
  - currency values, 190–192
  - loan payments, 87–90
- calculators
  - floating-point, 34–36
  - interactive, 82–85
- calendar program, 90–95
- capitals of states quiz, 282–284
- carriage return, tr command to replace with newline, 262
- case sensitivity, of Unix, 72
- case statements, as regular expressions, 72
- cat command
  - alternative to, 101–103
  - compressed files and, 109–112
  - -n flag, 98–99
  - OS X files and, 262
  - printing file contents to screen, 4
  - reading user data with, 81
- Celsius units, translating between Fahrenheit or Kelvin and, 85–87
- CentOS, /cgi-bin directory for, 201
- CGI (Common Gateway Interface)
  - scripts, 199
  - running, 201
  - viewing environment, 202–203
- grep script, 107–109
- change mode (chmod) command, 7, 57
- changetrack script, 194–197
- chattr command, 64
- checkexternal script, 220–222
- checklinks script, 217–220
- chmod (change mode) command, 7, 57
- Chrome operating system (Google), 299
- city, checking time in, 76
- cleaning up after guest user, 141–143
- cloud storage, 299
  - creating slide shows from photo streams, 304–306
  - emailing or copying archive file to, 166
  - keeping Dropbox running, 300–301
  - syncing Dropbox, 301–304
  - syncing files with Google Drive, 307–309
- color sequences, ANSI, 40–42
  - for region highlighting, 107–109
- command line interface, shell as, 2
- commands
  - count of those in PATH, 51–52
  - running, 3–4
  - running in bulk, 348–351
- Common Gateway Interface. See CGI
- (Common Gateway Interface) scripts
- Common Log Format, 235
- composite utility, 317
- compressed files, 109–112, 113–115
- convertdate script, 85–87
- convertcurrency script, 190–192
- Coordinated Universal Time (UTC), 73
- copyright
  - header in bc program, silencing, 36
  - issues, 207
- cron
  - archivedir in, 171
  - ensuring jobs are run, 159–162
  - scheduling jobs with, 154
- crontab
  - entry for netstat log generation, 254
  - for office document synced with Google Drive, 308
  - validating user entries, 154–159
- curl tool, 173–174, 182–183
- currency, calculating values, 190–192
- cut command, 19, 89

### D

- daemons, 119, 301
- Darwin (Unix core), 261
- database
  - checking size of, 70
  - searching with locate, 68–71
  - secure search, 127–131
- data storage. See cloud storage; disk usage
