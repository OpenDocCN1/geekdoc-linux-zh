# HASHCAT ATTACK TYPES

The "-a" option allows you to designate the attack mode type. Hashcat has multiple attack modes and you need to specify which one you want to use. The only time it is not necessary to use it is if you are doing a Single wordlist or straight mode attack.

The available attack types include:

+   0 = Straight
+   1 = Combination
+   3 = Brute-force
+   6 = HybrId Wordlist + Mask
+   7 = HybrId Mask + Wordlist

Straight: Single wordlist attack. Each word in the wordlist will be used against each password hash. You can also use Rules in this mode.

Combination: Combines words from separate wordlists to create new words on the fly.

Brute-force: Enter your own combination of characters, numbers & symbols or use Mask attacks to automated guesses. For example: ?u?l?s?d?a (upper, lower, symbol, decimal, all) would attempt to crack passwords like, "Aa!0a" to "Zz!9z" and everything in-between. You can also use "?b" for binary (00-ff), this is useful when cracking foreign language passwords.

Hybrid Attacks: Use a wordlist in combination with brute force characters or a pre-defined mask. For example, using the Rockyou wordlist with the Mask ?u?l?s?d?a would produce hash guess attempts like, "passwordAa!0a" and "monkeyZZ!9z".