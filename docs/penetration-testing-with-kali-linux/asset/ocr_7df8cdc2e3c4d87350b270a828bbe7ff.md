# OffSec

Penetration Testing with Kali Linux

+   - Heuristic-based Detection
- Behavioral Detection
- Machine Learning Detection

Signature-based antivirus detection is mostly considered a restricted list technology. In other words, the filesystem is scanned for known malware signatures and if any are detected, the offending files are quarantined.

A signature can be as simple as the hash of the file itself or a set of multiple patterns, with specific binary values and strings that belong only to that specific malware.

Relying on just the file hash as the only detection mechanism is a weak strategy because changing a single bit of the file would result in a completely different hash.

As an example, we created a text file on our local Kali machine that contains the string "offsec". Let's dump its binary representation via the xxd552 b argument before the file name.

```
kali:~ xxd -b malware.txt
00000000: 01101111 01100110 01100110 01101111 01100101 01100111 offsec
00000006: 00101010
```

Listing 233 - Inspecting the file content with xxd

We displayed the content of the file through the xxd utility. The output shows the binary offset on the leftmost column, the actual binary representation in the middle column, and the ASCII translation on the rightmost one. We also highlighted the binary representation of the letter 'c' in red. Its purpose will be clear shortly.

Now, as this is real malware, we need to calculate the hash of the file and we can do so through the sha256sum

```
kali:~ sha256sum malware.txt
c316e96c9c8f22fd45e8a990c1cfba4ae85a3a09e7c40598a0ba2383ff63510e malware.txt
```

Listing 234 - Calculating the SHA256 hash of the file

Now let's replace the first of "offsec" with a capital C and dump its binary value by xxd once more.

```
kali:~ xxd -b malware.txt
00000000: 01101111 01100110 01100110 01101111 01100101 01000111 offC
00000006: 00101010
```

Listing 235 - Inspecting the file content with xxd

In 235, the binary value of the last character is changed only in its third bit from the left.

Since every hashing algorithm is supposed to produce a totally different hash even if only one bit of it has changed, calculate the SHA256 on the modified string.

```
kali:~ sha256sum malware.txt
15defda07fdb5627bb27ca87841c76a8b10f743b3ae697cf12afacf732742a003c7c malware.txt
```

> 552 (die. net, 2022), https://linux.net/man/1/xxd

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

353