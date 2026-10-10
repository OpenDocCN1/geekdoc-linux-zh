# PERMISSION MODE REFERENCE (CONT.)

| Numeric Mode | Symbolic Mode | Permsisions as Displayed in File Listings |
| :----------- | :------------ | :----------------------------------------- |
| 62 | g=rw,0=w | - - -   r--   --w- |
| 64 | g=rw,0=r | - - -   rw-   r-- |
| 65 | g=rw,0=rx | - - -   rw-   r-x |
| 66 | go=rw | - - -   rw-   rw- |
| 67 | g=rw,0=rx | - - -   rw-   rwx |
| 70 | g=rwx | - - -   rwx   - - - |
| 71 | g=rwx,0=x | - - -   rwx   --x |
| 72 | g=rwx,0=w | - - -   rwx   -w- |
| 74 | g=rwx,0=wr | - - -   rwx   r- - |
| 75 | g=rwx,0=rx | - - -   rwx   r-x |
| 76 | g=rwx,0=rw | - - -   rwx   rw- |
| 77 | go=rwx | - - -   rwx   rwx |
| 100 | u=x | --x   - - -   - - - |
| 101 | uo=x | --x   - - -   --x |
| 102 | u=x,0=w | --x   - - -   --w- |
| 104 | u=x,0=r | --x   - - -   r-- |
| 105 | u=x,0=rx | --x   - - -   r-x |
| 106 | u=x,0=rw | --x   - - -   rw- |
| 107 | u=x,0=rwx | --x   - - -   rwx |
| 110 | ug=x | --x   -x-   --x |
| 111 | a=x | --x   -x-   - -x |
| 112 | ug=x,0=w | --x   -x-   --w- |
| 114 | ug=x,0=r | --x   -x-   r-- |
| 115 | ug=x,0=rx | --x   -x-   r-x |
| 116 | ug=x,0=rw | --x   -x-   rw- |
| 117 | ug=x,0=rwx | --x   -x-   rwx |
| 120 | u=x,g=w | --x   --w-  |