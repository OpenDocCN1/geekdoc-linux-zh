For the following benchmark, we'll use a different system with an attached GPU. Again, we'll use the benchmark mode of Hashcat to calculate the hash rates for MD5, SHA1, and SHA-256.

# A GPU benchmark test cannot be run in the lab.

```
C:\Users\admin\Downloads\hashcat-6.2.5>hashcat -b
hashcat (v6.2.5) starting in benchmark mode

* Device #1: NVIDIA GeForce 3090, 23336/24575 MB, 82MCU
Benchmark reveal options:
=================
* --optimized-kernel-enable

* Hash-Mode 0 (MD5)

Speed.#1........: 68185.1 MH/s (39.99ms) @ Accel:256 Loops:1024 Thr:128 Vec:8

* Hash-Mode 100 (SHA1)

Speed.#1........: 21528.2 MH/s (63.45ms) @ Accel:64 Loops:512 Thr:512 Vec:1

* Hash-Mode 1400 (SHA-256)

Speed.#1........: 9276.3 MH/s (73.85ms) @ Accel:16 Loops:1024 Thr:512 Vec:1
```

Listing 261 - Benchmark GPU with MD5, SHA1, and SHA-256

| Algorithm | GPU | CPU |
|---|---|--|
| MD5 | 68,185.1 MH/s | 450.8 MH/s |
| SHA1 | 21,528.2 MH/s | 298.3 MH/s |
| SHA256 | 9,276.3 MH/s | 134.2 MH/s |

Listing 262 - Comparison of GPU and CPU hash rates

Let's compare our GPU and CPU hash rates.

This highlights the speed improvement offered by GPUs. Now that we have all values we need, let's calculate the cracking time for our five-character password.

In this example, we'll calculate the cracking time for SHA256 with 916,132,832 hashes, which we calculated previously. We already know that 1 MH/s equals 1,000,000 hashes per second. Therefore, we can use Python to calculate CPU and GPU times. The first command uses the SHA-256 hash rate of the CPU calculated in Listing 260, and the second command uses the SHA-256 hash rate of the GPU calculated in Listing 261. The output format of our calculations will be in seconds.