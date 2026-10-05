# OffSec

Penetration Testing with Kali Linux

```
kali@kali:~ python3 -c "print(916132832 / 134200000)
6.8266231892746
```

```
kali@kali:~ python3 -c "print(916132832 / 9276300000)
0.0987685868192092
```

List 263 - Calculating the cracking time for password length of 5

The output shows that we can calculate possible hashes for this keyspace in one second with a GPU, and approximately seven seconds on a CPU.

Let's use the same character set with an increased password length of 8 and 10 to get better understanding of how cracking time scales versus password length. For this, we'll use the GPU hash rate for SHA-256 for our calculations.

```
kali@kali:~ python3 -c "print(62**8)"
2183401055848896
```

```
kali@kali:~ python3 -c "print(2183401055848896 / 9276300000)"
23537.41314081117
```

```
kali@kali:~ python3 -c "print(62**10)"
839299365683340224
```

```
kali@kali:~ python3 -c "print(839299365683340224 / 92763000000)"
90477816.14095493
```

List 264 - Calculating the cracking time for password length of 8 and 10 on a GPU for SHA-256

The output shows that when converted from seconds, it will take a GPU approximately 6.5 hours to attempt all possible combinations for an eight-character password, and approximately 2.8 years for a ten-character password, after converting the output from seconds.

Note that increasing password length increases cracking by exponential time, while increasing password complexity (charset) only increases cracking by polynomial time.⁶²⁷

This implies that a password policy encouraging longer passwords is more robust against cracking, compared to a password policy that encourages more-complex passwords.

In this section, we discussed encryption and hashing, and we benchmarked hash algorithms on a CPU and a GPU. Finally, we familiarized ourselves with the process of calculating cracking time.

# 13.2.2 Mutating Wordlists

Password policies, which have grown in recent years, dictate a minimum password length and the use of character derivations including upper and lower case letters, characters, and numerical values.

Most passwords in the commonly-used wordlists will not fulfill these requirements. If we wanted to use them against a target with strong password policies, we would need to prepare the wordlist by removing all passwords that do not satisfy the password policy or by modifying the wordlist to include appropriate passwords. We can address this by automating

> ⁶²⁷ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Time_complexity#Polynomial_time

PWK - Copyright 2023 OffSec Services Limited. All rights reserved.

392