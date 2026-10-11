# # CONCLUSION

In this chapter, we covered multiple ways to use Hashcat for cracking passwords. There are many additional ways to use the Hashcat tools, I highly recommend the reader take time and read up on this powerful tool. There are many patterns you will discover as you delve into password cracking. One password “obfuscation” technique used by a lot countries is to use a foreign language to spell English words using the foreign alphabet. So, for example, if a Russian wanted to use the word “spoon” in their password, they would not use the Russian word for spoon, but spell out the English word “spoon” directly using their alphabet.

You will run into a lot of keywalk passwords too. The big thing to keep in mind, especially when dealing with multi-national passwords is that the keyboard layout changes per country. It won’t always look like the familiar “qwerty”. Add in how Hashcat displays some characters (UTF8 to ANSI) and it can get a little confusing.

For example:

1234567890Д¹Ñ+ÑƒĐ°Đµı¹²Đ³Ñ^Ñ%оĐ·Ñ...ÑŚ

Is a Russian Keyboard walk:

1234567890йцукенгшщзхъ

Basically just, “1-0” and then “q” through “y” on the keyboard.

You can use character sets in Hashcat to brute force foreign language passwords, but I have never had a lot of success with doing that. I found using wordlists or just binary characters was more effective. But depending on your target, you may find success with it. See the Hashcat documentation for more information on cracking with character sets.

Lastly, a lot of modern passwords are a combination of a person’s name or names, a date and a symbol. I have had great success cracking these using the Facebook First and Last name wordlists in