
```
$ lpq -Pattic3

attic3@intuitive.com:  driver not active

Printing is disabled.
```

| 序号 | 用户 | 纸盒 | 大小 | 作业名称 |
| --- | --- | --- | --- | --- |
| 1 | KOSHIHWE | 0104 | 008 | KOSHIHWE0104a |
| 2 | KOSHIHWE | 0104 | 008 | KOSHIHWE0104b |
| 3 | KOSHIHWE | 0104 | 008 | KOSHIHWE0104c |
| 4 | kleimanj | 0317 | 032 | kleimanj0317a |
| 5 | zeta | 0042 | 008 | zeta0042a |
| 6 | jharger | 0167 | 008 | jharger0167a |
| 7 | jharger | 0167 | 008 | jharger0167b |
| 8 | ssinfo | 0353 | 000 | ssinfo0353a |
| 9 | fuelling | 0216 | 024 | fuelling0216a |
| 10 | zeta | 0042 | 152 | zeta0042b |
| 11 | tkjared | 0142 | 012 | tkjared0142a |
| 12 | SUJATHA | 0043 | 016 | SUJATHA0043a |
| 13 | SUJATHA | 0043 | 024 | SUJATHA0043b |
| 14 | taylor | 0889 | 000 | taylor0889a |

```
attic3: waiting to be transmitted to intuitive.com

The queue is empty.
```

```
$ alias mathprint='lpr -Pmathlw'

$ alias libprint='lpr -Plibrary'

$ alias edprint='lpr -Pedlw'
```

```
$ alias mathprint='lp -dmathlw'

$ alias libprint='lp -dlibrary'

$ alias edprint='lp -dedlw'
```

```
$ lpinfo mathlw

mathlw: server.utech.edu; MATH 734; multiple HP LaserJet Pro
```

```
$ lpinfo -v mathlw

mathlw description:

    driver: /usr/local/lib/lp/lpmq

    printer control group: cc

    graphic filter: /usr/local/bin/psplot

    log file: /usr/spool/lpr/mathlw/logfile

    lock file: /usr/spool/lpr/mathlw/lock

    hardware line: /dev/null

    maximum job count per user = 25

    subqueue list: mathlw1,mathlw2,mathlw3

    maximum print file blocks = 3000

    make unique via bin change

    network driver: /usr/local/lib/lp/lpnc

    ditroff filter: /usr/local/lib/devps/devps

    print formats: graphics, ditroff, use pr, troff

    queue ordering: age

    host attachment: server.utech.edu

    spooling directory: /usr/spool/lpr/mathlw

    location: MATH 734

    description: multiple HP LaserJet Pro
```

```
$ lpinfo -a | head -15

aglw:  server.utech.edu; AG 23; multiple HP LaserJet Pro

aglw1:        server.utech.edu; AG 23; HP LaserJet Pro

aglw2:        server.utech.edu; AG 23; HP LaserJet Pro

aglw3:        server.utech.edu; AG 23; HP LaserJet Pro

aglw4:        server.utech.edu; AG 23; HP LaserJet Pro

alpslw: sentinel.utech.edu; LIB 111; HP LaserJet ProX

bio:   ace.utech.edu; COM B117; DataPrinter (self-service)

cary:  franklin.utech.edu; CQuad (NE-B7); IBM 4019 Laser Printer

cslw: server.utech.edu; CS 2249; HP LaserJet Pro

cs115lw:     expert.utech.edu; CS 115; IBM 4019 LaserPrinter (for CS180)

cs115lw2:    expert.utech.edu; CS 115; IBM 4019 LaserPrinter (for CS180)

csg40lw: franklin.utech.edu; CS G040; IBM 4019 LaserPrinter

csg501w:  franklin.utech.edu; CS G050; IBM 4019 LaserPrinter

cslp1: expert.utech.edu; CS G73; C.Itoh, white paper (self-service)

eng130ci:  age.utech.edu; ENG 130; C.Itoh, white paper (self-service)

Broken pipe
```

```
$ who | pr -2 | more
```
