# 198 CHAPTER 11 Other Helpful Tools

| Package | Core | Frequency stats | Device stats | Tunables |
| --- | --- | --- | --- | --- |
| C2 (pc2) 13.1% | CPU 0 0.7k | CPU 1 2.8k | | 0.0 ms |
| 0.0% | POLL 0.0k 0.0 ms 0.0k | 0.1 ms |
| C3 (pc3) 0.0% | C3 (cc3) 0.1k | CIE-SNB 0.0k 0.0k | 0.9 ms |
| 0.0% | C6 (cc6) 0.0k | C3-SNB 0.1k 0.3 ms 1.0 ms |
| C7 (pc7) 71.4% | C7 (cc7) 88.7k | C7-SNB 98.4k 11.8 ms 91.9k | 3.4 ms |
| | | CPU 2 0.1k | CPU 3 0.2k | |
| | | POLL 0.0k 0.0 ms 0.0k | 0.0 ms |
| | | CIE-SNB 0.0k | 0.2 ms 0.3 ms 0.2 ms |
| | | C3 (cc3) 0.7k | C1-SNB 0.0k 0.0 ms 0.0k 0.5 ms |
| | | C6 (cc6) 0.0k | CIE-SNB 0.0k 0.0k | |
| | | C7 (cc7) 97.4k | C7-SNB 98.2k 43.2 ms 59.9k | 48.2 ms |
| | | CPU 4 0.1k | CPU 5 0.2k | |
| | | POLL 0.0k 0.0 ms 0.0k | 0.0 ms |
| | | CIE-SNB 0.0k | 0.4 ms 0.2 ms |
| | | C3 (cc3) 1.5k | C1-SNB 0.0k 0.1 ms 0.0k 0.5 ms |
| | | C6 (cc6) 0.0k | CIE-SNB 0.0k 0.0k | |
| | | C7 (cc7) 97.7k | C7-SNB 99.6k 34.8 ms 30.6k | 30.6 ms |
| | | CPU 6 0.1k | CPU 7 0.2k | |
| | | POLL 0.0k 0.0 ms 0.0k | 0.0 ms |
| | | CIE-SNB 0.0k | 0.0 ms 0.2k 0.2 ms |
| | | | | C3 (cc3) 0.0k | C1-SNB 0.0k 0.0 ms 0.0k 0.5 ms |
| | | C6 (cc6) 0.0k | CIE-SNB 0.0k 0.0k | |
| | | C7 (cc7) 96.3k | C7-SNB 96.4k 40.7 ms 99.1k | 55.8 ms |
| GPU | | | | |
| | Powered On 0.4k | | | |
| | RC5 95.4k | | | |
| | RC6p 0.0k | | | |
| | RC6pp 0.0k | | | |

FIGURE 11.2

PowerTop nurses interface displaying C state residents.

# 11.3.3 FREQUENCY STATS

The Frequency Stats displays the percentage of time each package, core, and hardware spends running in the various supported frequencies, including both P states and Turbo Boost frequencies.

Unlike the idle stats window, frequencies are added to the list after they have been observed. Since P states only make sense when the processor is executing instructions, that, in Co, an idle system often will not display in terms of frequency information.

Figure 11.3 shows an example Frequency Stats. Notice, similar to the idle stats window, the processor topology is sorted with the larger resources and power savings to the left of the screen and dependencies moving further to the right.