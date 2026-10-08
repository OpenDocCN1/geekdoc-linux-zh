# 244 LOCALIZATION

/etc/keytables/local.map which contains only the changes. In the rc scripts, this file is loaded with loadkeys and the keyboard is set up accordingly.

If for some particular reason, you want to use a special pair of symbols as opening and closing quotes you can compose these characters by means of a Compose key. Listing 9.1 shows an example of a possible Compose key configuration, in this case the right-hand Ctrl key yields 97 (as shown by the showkey program). The construction of the French opening quote is achieved by pressing and holding the right-hand Ctrl key and pressing the French closing quote is obtained by pressing and holding the right-hand Ctrl key and pressing the key twice,

```
keycode 97 = Compose
compose         = to'
compose         = to`
```

**Listing 9.1** Additional keyboard assignments with loadkeys.

# 9.2 Using the ISO-Latin-1 character set

 after system start-up, LINUX uses a modified IBM character set. This character set includes both of the ISO-8859-1 characters from the range 127–255 and a series of graphical symbols which are used, for example, by the mc program for representation of frames. Thus, this character set cannot be used to represent all of the characters of the ISO-Latin-1 character set.

This can instead be achieved by the appropriate character set together with the corresponding conversion table, and subsequently activating the newly loaded character set.

```
(Linux)-> setfont iso01.f14
(Linux)-> mapscrn trivial
(Linux)-> echo -e '\033(K'
```

Loading the character set and the conversion table applies to all virtual consoles, whereas switching character sets by means of the ESC sequence applies only to the current console. Unfortunately, the output of the mc program afterwards is not readable because the frames are not built out of the correct characters. Programs and character sets used can be found in the package kbd0.89.tar.gz.