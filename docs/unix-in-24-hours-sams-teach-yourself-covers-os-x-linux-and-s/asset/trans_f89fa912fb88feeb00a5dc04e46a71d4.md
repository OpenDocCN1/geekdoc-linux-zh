

```text
$ hi-low
You're trying to guess a number between 1 and 100
Guess? 50
... bigger!
Guess? 75
... smaller!
Guess? 69
Right!! Guessed 69 in 3 guesses.

$ hi-low
You're trying to guess a number between 1 and 100
Guess? 50
... bigger!
Guess? 75
... smaller!
Guess? 68
... bigger!
Guess? 73
... smaller!
Guess? 71
Right!! Guessed 71 in 5 guesses.
```

## Samsung_ML_191x_252x_Series__MiniMe

```text
$ lpadmin -p "Samsung_ML_191x_252x_Series__MiniMe" -c "ml191"
$
```

```text
$ lpstat -a ml191
ml191 accepting requests since Mon Jun 29 09:39:48 2015
```

```text
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

```text
attic3: waiting to be transmitted to intuitive.com

The queue is empty.
```

```text
$ alias mathprint='lpr -Pmathlw'
$ alias libprint='lpr -Plibrary'
$ alias edprint='lpr -Pedlw'
```

```text
$ alias mathprint='lp -dmathlw'
$ alias libprint='lp -dlibrary'
$ alias edprint='lp -dedlw'
```

```text
$ lpinfo mathlw
mathlw: server.utech.edu; MATH 734; multiple HP LaserJet Pro
```

```text
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

```text
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

```text
$ who | pr -2 | more
```

| 用户（左） | 终端（左） | 时间（左） | 用户（右） | 终端（右） | 时间（右） | 主机（右） |
|---|---|---|---|---|---|---|
| root | console | May 6 18:02 | ab | ttypk | May 9 07:57 | (nova) |
| princess | ttyaV | May 9 13:44 | dutch | ttypl | May 8 13:36 | (dov) |
| tempus | ttyaW | May 9 13:43 | malman | ttypm | May 9 13:07 | (dov) |
| enatsuex | ttyaY | May 9 13:41 | bakasmg | ttypq | May 9 13:09 | (age) |
| coxt | ttyaZ | May 9 13:35 | dodsont | ttyps | May 8 11:37 | (age) |
| scfarley | ttyAa | May 9 13:36 | md | ttypv | May 8 08:23 | (kraft) |
| nancy | ttyAb | May 9 13:12 | rothenba | ttypw | May 9 13:15 | (trinetra) |
| rick | ttyAc | May 9 13:12 | xuxiufan | ttypy | May 9 13:16 | (ector) |
| fitzte | ttyAd | May 9 13:47 | nashrm | ttyq3 | May 9 13:04 | (pc115) |
| maluong | ttyAe | May 9 13:46 | dls | ttyq5 | May 9 13:06 | (dialup01) |
| af5 | ttyAg | May 9 09:12 | myounce | ttyq8 | May 9 02:14 | (limbo) |
| zjin | ttyAh | May 9 13:44 | liyan | ttyq9 | May 9 13:11 | (volt) |
| herbertl | ttyAi | May 9 13:29 | daffnelr | ttyqA | May 9 13:36 | (localhost) |
| ebranson | ttyAj | May 9 13:44 | mm | ttyqB | May 9 10:32 | (mm) |
| billiam | ttyAk | May 9 13:36 | jlapham | ttyqC | May 9 12:46 | (mac18) |
| linet2 | ttyAm | May 9 11:04 | chuicc | ttyqE | May 9 13:38 | (icarus) |

