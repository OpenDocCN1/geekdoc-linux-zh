# # USING A LARGER DICTIONARY FILE

If first you don’t succeed, try a larger dictionary! A larger dictionary file provides more known passwords to compare target hashes against. This can crack a greater number of hashes, but because of the increased dictionary size can greatly increase the time it takes to run. Though I have found it is best to run a large dictionary file first and have Hashcat remove any hashes that are recovered. This will make the un-cracked file smaller for when you run the more intensive rules and masks attacks. The website **Crackstation.net** has a couple very large wordlists available. They have a 15GB monster and a smaller “Human Only” version that is about 700 MB. The larger wordlist has just about every everything that you can imagine in it, the smaller human only version only contains passwords recovered from actual password dumps.

For the next attempt, I went ahead and downloaded the human only wordlist as the larger one will not fit without expanding the Kali VM’s hard drive space. Don’t bother downloading it just for this example, you will see why in a minute. After downloading and expanding the wordlist to the desktop, I ran the following command:

```
> hashcat -D 1 -m 1000 Hardhash.txt Crackstation-human.txt -o Hardcracked.txt --remove
```

Nothing really new to this command line, other than naming a separate output file, but I did add the "**--remove**"switch. It is not really necessary on such a small hash list, but on large lists, once a hash is cracked, it is removed from the list to increase cracking time on future attempts.

And the results: