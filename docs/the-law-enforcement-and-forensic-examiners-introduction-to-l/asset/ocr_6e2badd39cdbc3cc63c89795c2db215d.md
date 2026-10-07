# v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

illustrated in small image analysis example, might not work as expected with larger images and the causes could exit with an error similar to:

```
grep: memory exhausted
```

The most apparent cause for this is that grep does its searches line by line. When you are “grepping” a large disk image terabytes in size, you might find that you have a huge number of bytes to read before grep comes across a newline. What if grep had to read several gigabytes of data before coming across a newline? It would “exhaust” itself (the input buffer fills up). There are many variables that affect this, and the causes are actually far complex.

One potential solution is to force-feed some newlines. In our analysis we are “grepping” for text. We are not concerned with non-text characters at all. If we could the input stream to grep and change the non-text characters to newlines, in cases grep would have no problem. Note that changing the input stream to grep does not change the image itself. Also, remember that we are still looking for a byte offset. Luckily, the character sizes remain the same, and the offset does not change as we feed newlines into the stream (simply replacing one “character” with another).

Let's say we want to take all of the control characters streaming into grep from the disk image and change them to newlines. We can use the translate command, tr, to accomplish this. Check out tr for more information about this powerful command:

```
barry@forensic1:-$ tr '[:ctrl:]' '\n' < fat_fs.raw | grep -abif analysis/searchlist.txt
```

7541:i have enough of your minded corporate piracy and will no longer stand for it. you will receive another letter next. It will have a single bank account number and bank name. I want you to deposit $50,000 in the account the day receive the letter.

7567:Don't try anything, and contact the cops. If you do, I will unleash a virus that will bring your whole network and destroy your consumer's confidence.

This command would: “Translate all the characters contained in the set of characters [:ctrl:] to newlines \n. Take the input to tr from fat_fs.raw (we are redirecting in the opposite direction this time) and pipe the output to grep, and then to head. The output does not change. The translation occurs in the stream, and it’s for a character swap.

This is only one of many possible problems you could come across. My point is that when these issues arise, you need to be familiar with the Linux tools to be able to understand why such errors might have been produced, and how you can get around them. Remember, the shell tools and the GNU software that accompany a Linux

184