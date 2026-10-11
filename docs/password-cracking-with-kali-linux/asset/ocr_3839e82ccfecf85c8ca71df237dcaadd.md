two password hashes are ever the same. If a salt isn't used (like on Microsoft NTLM hashes), if you can crack one hash, all the users that used the same password will have the same hash. So, all you need to do is take the hash and compare it to known hashes and if you get a match, you have the password.

Basically, on a system using LM hashes, any password that is fourteen characters or less is converted into all uppercase, and then broken into two 7-character passwords. Each half is then encrypted and combined to form the final hash. Cracking 7-character passwords using only uppercase letters is trivial, this is why LM hashes are not very secure.

Again, there is no salt used, so basically if you can get the LM hashes from a system, all you need to do is a look up table comparison to other known hashes and you can get the actual password. The LM hash is usually stored along with the better encrypted NT hash. The combination of the two hashes is called an NTLM hash. One odd caveat with Windows NTLM hashes is that if the password is greater than 14 characters, the LM hash is not used at all and the contents of the LM hash will be invalid. Storing the weak LM hash can also be turned off on Windows systems, which is the case in most newer operating systems.

A typical Windows NTLM hash looks something like this:

```
ac93c8016d14e75a2e9b76bb9e8c2bb6:8516cd0838d1a4dfdl ac3e8eb9811350
```

The LM hash is on the left of the colon and the more secure NT hash is on the right. The LM and NT hash combined are called an NTLM hash.