target's password policy requires two numbers, six uppercase letters and two special characters you can create a mask for Hashcat to use.

In this example it would look something like, `?d?d?u?u?u?u?u?u?s?s`:

```
```bash
hashcat -D 1 -m 1000 Hardhash.txt -o Hardcracked2.txt -a3
?d?d?u?u?u?u?u?u?s --remove
```
```

Play around with different masks until you get a feel for how they work. The longer the mask, the exponentially longer it will take for it to run. A three-letter mask could be finished in seconds. A 10+ character mask could take hours or years to run. Hashcat also allows for the use of “mask files” instead of manually providing the mask. Basically, a mask file is just a file that contains multiple masks. Example masks are included with Hashcat, and can be found in the `masks` subdirectory.

Below is a screenshot of the “Rockyou-1-60.hcmask”:

![](bbox=[0.28, 0.51, 0.71, 0.75])

To use a mask file, you simply provide the mask filename instead of typing a manual mask on the Hashcat command line.

```
```bash
hashcat -m 1000 Hardhash.txt -o cracked3.txt -a3 rockyou-1-60.hcmask --remove
```
```