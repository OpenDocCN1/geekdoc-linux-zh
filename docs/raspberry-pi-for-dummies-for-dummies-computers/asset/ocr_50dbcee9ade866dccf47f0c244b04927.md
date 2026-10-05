There are two ways to label the pins. Figure 16-1 shows what is known as BCM mode, which corresponds to the numbers used in the Broadcom data sheet that defines the hardware. Another system was used in the early days – the BOARD system – but it is falling out of favor now. BOARD referred to pins mainly by a mixture of special function names and arbitrarily assigned “free” GPIO pins. The idea was, as the pinout (what connections are on pins) on the header changed, the names could remain constant.

# Model 1nIssue 1

# Model 1
Issue 2

| 3V3 | 1 | | 2 | 5V |
|---|---|---|---|---|
| GPIO 0 | GPIO 2 | | 4 | SV |
| GPIO 1 | 3 | | 6 | Gnd |
| GPIO 3 | 5 | | 8 | GPIO 14 |
| GPIO 4 | 7 | | 10 | GPIO 15 |
| Gnd | 9 | | 12 | GPIO 18 |
| GPIO 17 | 11 | | 14 | Gnd |
| GPIO 21 | 13 | | 16 | GPIO 23 |
| GPIO 22 | 15 | | 18 | GPIO 24 |
| 3V3 | 17 | | 20 | Gnd |
| GPIO 10 | 19 | | 22 | GPIO 25 |
| GPIO 9 | 21 | | 24 | GPIO 8 |
| GPIO 11 | 23 | | 26 | GPIO 7 |
| Gnd | 25 | | 28 | ID_SC |
| ID_SD | 27 | | 30 | Gnd |
| GPIO 5 | 29 | | 32 | GPIO 12 |
| GPIO 6 | 31 | | 34 | Gnd |
| GPIO 13 | 33 | | 36 | GPIO 16 |
| GPIO 19 | 35 | | 38 | GPIO 20 |
| GPIO 26 | 37 | | 40 | GPIO 21 |
| Gnd | 39 | |

![](bbox=[0.136, 0.723, 0.233, 0.773])

# Model 1
Issue 1 & 2

# Model 1 B+
Model 2
Model 3
Pi Zero

ID_SD = GPIO 0
ID_SC = GPIO 1 But only for identification EEPROM

As we noted, the first pin of the Pi had a different pin to all the rest, and those were only for three pins. These are shown in Figure 16–1, on the left side. Model 1 before the B+ had only 26 pins, whereas all subsequent models 40 pins. You cannot buy the earlier models nowadays, so you have no to worry; the extra information is only given in case you have an older Pi.

322 PART 5 Exploring Electronics with the Raspberry Pi