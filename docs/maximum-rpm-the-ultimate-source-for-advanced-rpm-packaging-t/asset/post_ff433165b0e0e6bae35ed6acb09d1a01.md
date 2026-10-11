
# G.2.3. Ready to Go!

After building and installing PGP, you’re ready to start using RPM’s package-signature capabilities. If your primary interest is in checking the signatures on packages built by someone else, see Chapter 7, “Using RPM to Verify Package Files,” which will tell you everything you need to know.

On the other hand, if you are a package builder and would like to start signing packages, see Chapter 17, “Adding PGP Signatures to a Package,” and it will have you signing packages in no time.

# I

# Index

## Symbols

- %attr file directive, 196, 399
- %attr macro, 235
- %attr build-time script, 394
- %build script, 287-288
- %build section, 130
- %clean build-time script, 395
- %clean section, 132
- %config file directive, 196, 399
- %description tag, 252, 389
- %dict directive tag, 293, 400
- %docfile directive tag, 220, 293-294
- %doc file directive, 195, 399
- %docdir directives, 400
- %docdir directory directive, 197-199
- %else conditional, 203, 402
- %endif conditional, 203, 402
- %files list, 131, 194, 254, 398
  - %doc directive tag, 220, 294
  - adding to spec file, 285
  - checking, 146-148
  - clients, 292-293, 304
  - creating, 291
  - directives, 194
    - %attr, 196, 399
    - %build, 199, 400
    - %clean, 195, 399
    - %docdir, 198, 400
    - %verify, 196, 400
    - -f <file>, 200
  - config, 196
  - directory-related, 197
  - file directives (%config), 399
  - files, locating, 291-293
  - packages, 254
  - prefix tag, 217
  - restrictions, 218
  - servers, 292-293, 304
  - subpackages, 253
- %ifcxx conditional, 272
- %ifarch conditional, 202, 401
- %ifnxxx conditional, 272
- %ifnarch conditional, 202, 402
- %ifnos conditional, 203, 402
- %ifios conditional, 203, 402
- %install build-time script, 395
- %install script, 288-289
- %setup script, 129, 286
  - -n option, 201, 250, 401
- %patch macros, 286
  - -n option, 398
  - -E option, 398
  - -P option, 398
- %post install scripts, 395
- %postun erase-time script, 396
- %prep installation scripts, 395
- %prep, 141
- %prep build-time script, 394
- %prep script, 129, 286
- %preun erase-time script, 396
- %setup macro, 396
  - -a option, 397
  - -n option, 397
  - -c option, 397
  - -D option, 397
  - -T option, 397
- %verify file directive, 196, 400
- %verify script, 396
- %verify verification-time script, 183

## A

- -a %setup macro option, 397
- absolute symlinks, 217, 223
- accessing
  - ftp ports, 34
  - help, 104
  - read/write, 298
  - RPM database, 42
- adding
  - %files list to spec file, 285
  - build-time, 284
  - directories, 197
  - disclaimers to downloaded software, 415
  - entries to headers, 326
- packages
  - dependency processing, 320
  - signatures, 241, 244
- signatures to packages, 152, 373
  - --addsign command, 373
  - --addsign signature command option, 244-245
- alpha architecture, 338
- amanda
  - %files list, 285
  - backups, 292, 298
  - building, 287-288
  - cleaning, 281-282
  - clients, 280, 284, 297-298
    - backups, 276
    - dump utility, 276
    - configuration, 278-279
    - dumps, 298
  - files
    - clients, 292
    - configuration, 299
  - ftp site, 276-277
  - installation, 279-280, 285, 288-289
  - patches, 297, 281-283
  - restores, 292
  - scripts, 298
    - build-time, 284
    - installation, 297
  - servers, 284, 298
  - .rhosts files, 300
    - backups, 276
    - configuration names, 300
    - postinstall scripts, 300
  - sources, unpacking, 277
  - spec file, 283
  - subpackages, 284
  - testing, 277, 303
  - uninstallation, 300-302
  - user IDs, 298
- applications
  - pointing to multiple operating systems, 116
  - upgrading, 116
- Applied Cryptography, 420
- arch canon rpmrc file entry, 359
- arch compat entry, 360

## B

- ARCH query tag, 73, 379
- architecture, 354
  - alpha, 338
  - compatibility, 35, 267, 310, 360
  - conditionals
    - %ifxxx, 272
    - nested, 271
  - detection logic, overriding, 151
  - files
    - conditional, 201
    - naming, 338
    - i386, 338
    - m68k, 338
    - mips, 338
    - multiple (support), 10
    - name, 310
    - packages, building, 172-173
    - ppc, 338
    - RPM version 1, 10
    - SGI, 338
    - sparc, 338
    - spec files, 202-203
    - tags (exclusive xxx), 270
    - verification, overriding, 35
  - tags
    - architectures, 172, 264
    - conditionals (%ifnxxx), 272
    - multiple, 8, 161
    - packages, building, 201
    - excludearch, 172, 392
    - excludetarch, 173, 392
  - see also hardware; platforms
- archives
  - compression, 349
  - cpio, 105
  - files, extracting, 106
  - packages, 349
  - source files, unpacking, 186
- ARCHIVESIZE --queryformat tag, 382
- arguments, 298
- erase-time scripts, 181
- install scripts, 181
- array iterators, 71-72
- attributes (files), 91, 196-197, 233-234, 400
- authentication (packages)
  - digital signatures, 14
  - signatures, 238
- automatic dependencies, 206-209
- autoreqprov tag, 209
  - scripts, 207-208
- automatic handling (configuration files), 9
- automatic packages, building, 116
- AUTOEREQPROV --queryformat tag, 385
- autoreqprov dependency tag, 171, 391
- autoreqprov tag, 209

## B

- -% patch macro option, 398
- -b %setup macro option, 397
- backups, 292, 298
  - amanda (read/write access), 298
  - clients, 276
  - file extensions (patch% macros), 193
- bazbin subpackage, 249
- BIN header structure value, 343
- binary files
  - directories, 364
  - installation, 316
  - package files, 108-109, 123, 135
- binary packages, 116, 145, 289-291, 340
  - creating, 162
  - files, 157
  - installation, 406
  - queries, 62
- block structures (conditionals), 271
- BOGUS distribution, 9
- Boolean values, 309
- Born again shell, restoring, 43
- -buildarch <arch> rpm -b command option, 151
- -buildarch rpm -b command option, 372
- build command
  - --rebuild, 161-162
  - --recompile, 160-161
  - --sign option, 241-242
- -buildos <os> rpm -b command option, 152
- -buildos rpm -b command option, 372
- build platform, 265
- build root, 156, 229
- -buildroot <path> rpm -b command option, 155
- -buildroot rpm -b command option, 156-157, 372
- -buildroot rpm -b command option, 157
- build roots, 226-227
  - alternate, 227
  - cleaning, 230
  - configuration, 230-231
  - default, 226
  - selecting, 227
- build sections, 122
- build system (packages), 137
- build xxx translate rpm file, 267
- build% build-time script, 180
- build-time package signatures, 241
- build-time scripts, 178, 284
  - %build, 180, 394
  - %clean, 180, 395
  - %install, 180, 395
  - %prep, 179, 394
  - environmental variables, 179, 394
  - subpackages, 257
- buildarchtranslate entry, 359
- builder entry, 361
- BUILDHOST --queryformat tag, 377
- building
  - amanda, 287-288
  - databases, 374
  - packages, 115-116, 132-136, 140, 143-144, 201, 303, 372
    - %build, 142
    - %build section, 130
    - %files list, 131, 147-148
    - %checkin, 146
    - %install section, 130
    - %prep, 141

## C

- conditionals
  - - `-timecheck`, 372
  - `-timecheck <ecs>`, 158
  - `-v`, 159

- **rpm -c**
  - `-dbpath <path>`, 38, 42
  - `-nodeps`, 38, 41, 372
  - `rfile <rfile>`, 38, 42
  - **root <path>**, 38, 42
  - `-test`, 18, 38-41
  - `-vv`, 38-40

- **rpm -i**
  - `-dbpath <path>`, 18, 34
  - `-excludedocs`, 18, 30, 370
  - `-force`, 18, 30, 370
  - `-ffport <port>`, 18, 34
  - `-ffproxy <host>`, 18, 34
  - `-bash`, 18, 22, 370
  - `ignorearch`, 370
  - `ignoreos`, 18, 35, 370
  - `ignorereach`, 18, 35
  - `includedocs`, 18, 31, 370
  - `-nodeps`, 18, 29, 370
  - `-noscripts`, 18, 32, 370
  - `-percent`, 18, 33, 370
  - `-prefix`, 18, 31-32, 370
  - `rfile <rfile>`, 18, 33
  - `replacefiles`, 18, 25-29, 370
  - `replacepkg`, 18, 24-25, 370
  - `-root <path>`, 18, 33
  - `-test`, 18, 23-24, 370
  - `-v`, 18, 22
  - `-vv`, 18, 23

- **rpm -K**
  - `-nppg`, 94, 99
  - `rfile <rfile>`, 94, 100
  - `-vv`, 94, 100
  - `-v`, 94-97

- **rpm -K command**
  - `rfile <rfile>`, 94, 100
  - `-vv`, 94, 100

- **rpm -noscripts**, 38, 41-42
- **rpm -q**
  - `-dump`, 369
  - `-provides`, 369
  - `-queryformat`, 369
  - `-requires`, 369
  - `-scripts`, 369
  - `-whatprovides`, 369
  - `-prefix`, 371
- **rpm -U**
  - `-dbpath <path>`, 46
  - `excludedocs`, 46, 371
  - `-force`, 46, 51, 371
  - `-ffport <port>`, 46
  - `-ffproxy <host>`, 46
  - `-bash`, 46, 371
  - `ignorearch`, 46
  - `ignoreos`, 46, 371
  - `includedocs`, 46, 371
  - `-nodeps`, 46, 371
  - `-noscripts`, 46, 51-52, 371
  - `-oldpackage`, 46, 50-51, 371
  - `-percent`, 46, 371
  - `-prefix <path>`, 46
  - `rfile <rfile>`, 46
  - `replacefiles`, 46, 371
  - `replacepkgs`, 46, 371
  - `root <path>`, 46
  - `-test`, 46, 371
  - `-v`, 46
  - `-vv`, 46

- **rpm -V**
  - `-dbpath`, 90
  - `-nolibs`, 87, 370
  - `-nofiles`, 88, 370
  - `-noscripts`, 88, 370
  - `-rfile`, 90
  - `-root`, 90
- **rpm -V**a, 86
- **rpm -V**f, 86
- **rpm -V**g, 87
- **rpm -V**p, 86
- **rpm -V**s, 89
- **rpm -V**u, 89

- **signature**
  - `-addsign`, 244-245
  - `-resign`, 243

- **command parameters**
  - **rpm -c**, 38
  - **rpm -K**, 94

- **commands**
  - `-addsign`, 373
  - `-checksig`, 374
  - `-initdb`, 374
  - `-rebuild`, 373
  - `-rebuilddb`, 374
  - `-recompile`, 373
  - `-resign`, 373
- **build**
  - `-rebuild`, 161-162
  - `-recompile`, 160-161

- file(1), 339, 351
- grep, 57
- output, 104, 159

- **rpm -c**, 38, 43
- **rpm -K**, 94-96, 374
- **rpm -U**, 47, 50
- **rpm2cpio**, 105
- syntax (build-related), 160

- **comment lines**, 129
  - creating, 164
  - ignoring, 164
  - spec file, 388

- **commercial use (PGP)**, 421
- comparing source trees, 121
- comparison operators' version requirements, 210

- **compatibility**, 206
  - architecture, 35, 267, 310, 360
  - libraries, 60, 171
  - operating systems, 35, 310, 360
  - packages (queries), 60
  - software versions, 341
  - updated software, 341

- **compression**
  - archives, 349
  - patch files, 194
  - zip, 194

- **conditional files**, 201
- **conditionals**, 201
  - `%else`, 203, 402
  - `%endif`, 203, 402
  - `%if`, 203, 272
  - `%ifarch`, 202, 401
  - `%ifnxxx`, 272
  - `%ifnarch`, 202, 402
  - `%ifnos`, 203, 402
  - `%ifos`, 203, 402
  - block structures, 271-272
  - nested, 271
  - platform-dependent, 266
  - structure, 271

429
