
## -query format tag

- URL, 379
- VENDORS, 378
- VERIFYSCRIPT, 386
- VERSION, 376
- XPM, 378

### query options, 213

### query tags
- ARCH, 73
- FILENAMES, 73
- FILESIZES, 73
- INSTALLTIME, 71
- modifiers, 71
- NAMES, 70, 73
- RELEASE, 70
- RPMTAG, 73
- RPMTAG.ARCH, 73
- RPMTAG
- VERIFYSCRIPT, 73
- VERSION, 73

- -quiet option, 104
- -quiet rpm -b command option, 159
- qip, 194

## R
- .ghosts files, 300
- .rpm files, see packages
- -root <path> rpm -U command option, 46

- random bits (key pairs), 240

- --rcfile <rcfile> rpm
  - -b command option, 160
  - -c command option, 38, 42
  - -i command option, 18, 33
  - -U command option, 46

- --rcfile rpm -V command option, 90

- rcfile <rcfile> command option, 94, 100

- read/write access (amanda backups), 298

### reading
- files (disk devices), 298
- headers, 324

- README file (packages), 221
- - rebuild build command, 161-162
- - rebuild command, 373
- - rebuilddb command, 374
- --rebuilddb option, 102

### rebuilding
- databases, 312
- packages, 10, 102-103, 373

- - recompile build command, 160-161
- - recompile command, 373

### recapling
- packages, 161
- software, 373

### records (databases)
- locating, 333
- numbers, 312

- Red Hat Package Manager, see RPM

- reducing output, 104
- reinstallation (packages), 24
- relative symlinks, 223
- release, 128

### files, 338
- naming tag, 166
- software, 338

## RELEASE
- - -queryformat tag, 376

- release package-naming tag, 388
- RELEASE query tag, 70
- releasee (package labels), 13
- relocatable packages, 216

- %files list, 218
- installation, 174, 223
- memory, 216
- prefix tag, 216-217, 221
- software references, 219
- symlinks, 219, 223
- cisting, 222

### relocation
- packages, 31-32, 219
- config file, 221
- testing, 223
- verification, 221
- software, 217-219

- relocation tags (prefix), 216-217

### removing
- %doc directive tag from %files list, 220
- directory trees, 154
- output files, 193
- --replacefiles option, 137

- --replacefiles rpm
  - -i command option, 18, 25-29, 370
  - -U command option, 46, 371

- --replaces rpm
  - -i command option, 18, 24-25, 370
  - -U command option, 46, 371

### replacing
- files (installation), 28-29
- packages (signatures), 241, 243
- signatures, 243, 373

- require distribution entry, 364
- require icon entry, 364
- require vendor entry, 364

### required
- capabilities, 65-66, 206, 209
- packages, 170, 213

## REQUIREFLAGS
- - -queryformat tag, 383

## REQUIRENAME
- - -queryformat tag, 383

- requires dependency tag, 170, 390
- --requires query option, 213
- --requires rpm -q command option, 369
- requires tag (version requirements), 210

## REQUIREVERSION
- - -queryformat tag, 383

- requiring packages, 60

- - resign command, 373
- - resign signature command option, 243

- resources (iterators), freeing, 328

- restores, 292

### Bourne-again shell, 43
- configuration files, 26-27
- files, 7
- packages, 43

### restrictions
- %files list, 218
- package labels (names), 56
- PGP software, 421

- - retrieving header entries, 326
  - `--root <path>` rpm
    - `-c` command option, 38, 42
    - `-i` command option, 18, 33
  - `--root` rpm -V command option, 90
- ROOT — `.querformat` tag, 381
- root directories, 33, 42, 74, 90, 361
  - alternate, 155-156
  - build roots, 155
  - databases, 74
  - scripts, 33
  - selecting, 226-227
  - software (installation), 157
- routines, 409

## RPM
- discussion groups, 408
- locating on your system, 404
- mailing lists, 408
- packages (signatures), 240-241
- Perl, 9
- technical support, 408
- Web site, 409

- rpm-b command options, 149, 159
  - `--buildarch`, 151, 372
  - `--buildos`, 372
  - builds `<>`, 152
  - `--buildroot`, 155-157, 372
  - `--clean`, 154-155, 372
  - `--noscripts`, 372
  - output, 159
  - `--quiet`, 159
  - `--rifle <rifle>`, 160
- rpm-ba, 145-146
- rpm-bc, 142-143
- rpm-bi, 143
- rpm-bi, 144
- rpm-bl, 146-148
- rpm-bp, 141
  - `--short-circuit`, 149-150
  - `--short-circut`, 372
  - `--sign`, 152, 372
  - `--test`, 153, 372
  - `--timecheck`, 158, 372
  - `--vv`, 159
- rpm-ba command, 145-146
- rpm-bb command, 144
- rpm-`bc` command option, 142-143
- rpm-`bi` command option, 143-144
- rpm-`bl` command option, 146-148
- rpm-`bp` command option, 141
- rpm-`e` command, 38, 43
- options
  - `--dbpath <path>`, 38, 42
  - `--nodeps`, 38, 41
  - `--noscripts`, 38, 41-42
  - `rfile <rfile>`, 38, 42
  - `root <path>`, 38, 42
  - `--test`, 18, 38-41
  - `--vv`, 38-40
- parameters (pkg)...(pkgN), 38
- postuninstall scripts, 39
- preuninstall scripts, 39
- syntax, 38
- rpm-e command options, 372
- rpm-i command
  - `--dbpath <path>`, 18, 34
  - `--excludedocs`, 18, 30, 370
  - `--force`, 18, 30, 370
  - `--fport <port>`, 18, 34
  - `--fpport <host>`, 18, 34
  - `--hash`, 18, 22, 370
  - `--ignorearch`, 18, 35, 370
  - `--ignoreos`, 18, 35, 370
  - `--includedocs`, 18, 31, 370
  - `--nodeps`, 18, 29, 370
  - `--noscripts`, 18, 32, 370
  - `--percent`, 18, 33, 370
  - `--prefix <path>`, 18, 31-32, 370
  - `--rfile <rfile>`, 18, 33
  - `--replacefiles`, 18, 25-29, 370
  - `--replacepkgs`, 18, 24-25, 370
  - `--root <path>`, 18, 33
  - `--test`, 18, 23-24, 370
  - `--vv`, 18, 22
- parameters
- rpm-i, parameters (filel.rpm)...(fileN.rpm), 18

- rpm-K command, 94-96
  - `--nopp`, 374
  - output, 96
- rpm-q command, 54
  - options, 369
    - package labels, 56
    - selections, 55
- rpm-U command, 47, 50
  - options
    - `--dbpath <path>`, 46
    - `--excludedocs`, 46, 371
    - `--force`, 46, 51, 371
    - `--fport <port>`, 46
    - `--fppport <host>`, 46
    - `--hash`, 46, 371
    - `--ignorearch`, 46, 371
    - `--ignoreos`, 46
    - `--includedocs`, 46, 371
    - `--nodeps`, 46, 371
    - `--noscripts`, 46, 51-52, 371
    - `--oldpackage`, 46, 50-51, 371
    - `--percent`, 46, 371
    - `--prefix <path>`, 46, 371
    - `--rfile <rfile>`, 46
    - `--replacefiles`, 46, 371
    - `--replacepkgs`, 46, 371
    - `--root <path>`, 46
    - `--test`, 46, 371
    - `--vv`, 46
    - parameters, 46
- rpm-V command
  - file groups, 82
  - file mode, 82
  - file ownership, 82
  - file size, 82
  - major number, 83
  - MD5 checksum, 82
  - minor number, 83
  - modification time, 83
  - options
    - `--dbpath`, 90
    - `--nodeps`, 87, 370
    - `--nolibs`, 88, 370
    - `--noscripts`, 88, 370
    - `--rfile`, 90
    - `--root`, 90
  - `rpm -Va`, 85

rpm -Vf, 86
rpm -Vg, 87
rpm -Vp, 86
rpm -Vv, 89
rpm -Vvv, 89
symlinks, 83
rpm -Va command option, 85
rpm -Vf command option, 86
rpm -Vg command option, 87
rpm -Vp command option, 86
rpm -Vv command option, 89
rpm -Vvv command option, 89
rpm -y command, 370

## RPM ARCH
- build-time variable, 394
- environmental variable, 179

## RPM BUILD DIR
- build-time variable, 394
- environmental variable, 179

## RPM BUILD ROOT
- build-time variable, 394
- environmental variable, 179

## RPM database, accessing, 42

## RPM DOC DIR
- build-time variable, 394
- environmental variable, 179

## RPM INSTALL PREFIX
- environmental variable, 181
- variable, 395

## RPM OPT FLAGS
- build-time variable, 394
- environmental variable, 179

## RPM OS
- build-time variable, 394
- environmental variable, 179

## RPM PACKAGE NAME
- build-time variable, 394
- environmental variable, 179

## RPM PACKAGE RELEASE
- build-time variable, 394
- environmental variable, 179

## RPM PACKAGE VERSION
- build-time variable, 394
- environmental variable, 179

## RPM ROOT DIR build-time variable, 394

## RPM SOURCE DIR
- build-time variable, 394
- environmental variable, 179

RPM version 1, 9–10
- configuration files (automatic handling), 9
- databases, 10
- file formats, 10
- multiple architecture, 10
- packages, rebuilding, 10
- size requirements, 10
- speed, 10

RPM version 2, 10
- rpm2cpio command, 105
- performance, 10

- rpm -c command options, 157
- rpm-list mailing list, 408
- rpm2cpio command, 105
- rpMAChtool, 349
- rpmArchStore() rpmrc function, 310
- rpmdBClose() database manipulation function, 311
- rpmdBFindByConflict() database search function, 315
- rpmdBFindByFile() database search function, 313
- rpmdBFindByGroup() database search function, 314
- rpmdBFindByProvides() database search function, 314
- rpmdBFindByRequiredBy() database search function, 315
- rpmdBFindPackage() database search function, 314
- rpmdBFirstRecNum() database traversal functions, 312
- rpmdBGetRecord() database traversal function, 312
- rpmdBInit() database manipulation function, 311
- rpmdBNextRecNum() database traversal function, 312
- rpmdBOpen() database manipulation function, 311
- rpmdBRebuild() database manipulation function, 312
- rpmdpeAddPackage() dependency functions, 320
- rpmdpeAvailable Package() dependency function, 321
- rpmdpeCheck() dependency function, 321
- rpmdpeDependencies() dependency functions, 320
- rpmdpeDone() dependency function, 322
- rpmdpeFreeconflicts() rpmdpeFreeconflict(), 321
- rpmdpeRemovePackage() dependency function, 321
- rpmdpeUpgradePackage() dependency function, 320
- rpmDirEntry, 364
- rpmsError() error handling function, 306
- rpmsSetCallback() error handling function, 307
- rpmsGetString() error handling function, 307
- rpmGetArchName() rpmrc function, 310
- rpmGetBooleanVar() variable manipulation function, 309
- rpmGetOsName() rpmrc functions, 310
- rpmGetVar() variable manipulation function, 308
- rpmGetVerbosity() diagnostic control function, 322
- rpmhdr tool, 349
- rpmsIDebug() diagnostic control function, 323
- rpmsIferbose() diagnostic control functions, 322
- rpmladd tool, 349

### rpmlib
- dependency, 320–322
- diagnostic control, 322
- error handling functions, 306–307
- files, 328
- header manipulation functions, 324–325
- headers, 329
- iterator functions, 327–328
- package data, 307–308, 316
