# Listing 1: Testing DMX Lights

```
$ piTest -w DMXOut_1,255

Write value 255 dez (-ff hex) to offset 525.
$ piTest -w DMXOut_9,255

Write value 255 dez (-ff hex) to offset 533.
$ piTest -w DMXOut_2,255

Write value 255 dez (-ff hex) to offset 528.
$ piTest -w DMXOut_11,255

Write value 255 dez (-ff hex) to offset 535.
```

# Listing 2: Switching Off the Lights

```
$ piTest -w 525,1,0

Write value 0 hex (= 0 dez) to offset 525.
$ piTest -w 528,1,0

Write value 0 hex (= 0 dez) to offset 528.
$ piTest -w 533,1,0

Write value 0 hex (= 0 dez) to offset 533.
$ piTest -w 535,1,0

Write value 0 hex (= 0 dez) to offset 535.
```

# Listing 3: dmx_demo.py

```
01 #!/usr/bin/python3
02 import time
03 import struct
04
05 DEBUG = False
06
07 DMX1_MASTER = 525
08 DMX1_RED = 526
09 DMX1_GREEN = 527
10 DMX1_BLUE = 528
11
12 DMX2_MASTER = 533
13 DMX2_RED = 534
14 DMX2_GREEN = 535
15 DMX2_BLUE = 536
16
17 class RevPi:
18     _rev_pi = open('/dev/piControl0', 'wbr+', 0)
19
20    def _init_(self):
21        pass
22
23 class DMX(RevPi):
24    _green = 0
25    _red = 255
26    _blue = 0
27
28    def _init_(self, master, adr_green, adr_red, adr_blue):
29        self.adr_green = adr_green
30        self.adr_red = adr_red
31        self.adr_blue = adr_blue
32        self._rev_pi.seek(master)
33        self._rev_pi.write(struct.pack('<H', 255))
34
35    def update_color(self, adr, val):
36        self._rev_pi.seek(adr)
37        self._rev_pi.write(struct.pack('<H', val))
38
39    def set_step(self, mode_val):
40        if mode_val == 1:
41            self._green += 16
42        elif mode_val == 2:
43            self._red += -16
44        elif mode_val == 3:
45            self._blue += 16
46        elif mode_val == 4:
47            self._green += -16
48        elif mode_val == 5:
49            self._red += 16
50        elif mode_val == 6:
51            self._blue += -16
52
53    def do_green(self):
54        if DEBUG:
55            print('GREEN: %d' % self._green)
56        self.update_color(self.adr_green, self._green)
57
58    def do_red(self):
59        if DEBUG:
60            print('RED: %d' % self._red)
61        self.update_color(self.adr_red, self._red)
62
63    def do_blue(self):
64        if DEBUG:
65            print('BLUE: %d' % self._blue)
66        self.update_color(self.adr_blue, self._blue)
67
68 DMX_1 = DMX(DMX1_MASTER, DMX1_GREEN, DMX1_RED, DMX1_BLUE)
69 DMX_2 = DMX(DMX2_MASTER, DMX2_GREEN, DMX2_RED, DMX2_BLUE)
70
71 while 1:
72    for mode in range(1, 7):
73        if DEBUG:
74            print('mode=%d' % mode)
75        for i in range(0, 15):
76            if DEBUG:
77                print('i=%d' % i)
78            DMX_1.set_step(mode)
79            DMX_2.set_step(mode)
80            DMX_1.do_red()
81            DMX_2.do_red()
82            DMX_1.do_green()
83            DMX_2.do_green()
84            DMX_1.do_blue()
85            DMX_2.do_blue()
86            time.sleep(0.05)
```