in Linux) to hiragana. When a line of hiragana is highlighted, it means that the line has not yet been converted beyond that. In the second line, however, the user has subsequently pressed the spacebar, which caused the IME to convert the hiragana string into the appropriate Kanji, hiragana, and katakana elements. The first word, Linux, has been converted to katakana text, because it is a borrowed word, while Japanese input has been converted to Kanji; the rest stays in hiragana.

りなっくすでにほんごにゅうりょくができます。
リナックスで日本語入力ができます。

Figure 11-7: IME conversions while typing in Japanese

# Korean

The job of the Korean IME is again quite different from that of the Chinese and Japanese IMEs, because the language is written in a very different way. Korean is written either entirely in alphabetic letters, called Hangul, or in a combination of Hangul and ideographic characters borrowed from Chinese called Hanja. While the Hanja characters are essentially the same as their Chinese and Japanese counterparts, Hanzi and Kanji, the Korean phonetic alphabet, Hangul, has its own unique appearance, as you can see in the Korean word for Korea, Hangug(k), in Figure 11-8.

![](bbox=[0.28, 0.68, 0.68, 0.78])

Figure 11-8: Korea (Hangug) written horizontally in Hangul

This seems simple; however, the representation is not quite correct, because Korean is very unique in the way that its alphabetic characters are put to the page. Unlike the usual side-by-side positioning of hiragana, katakana, and most other languages written with an alphabet, Hangul letters are grouped in pairs, triplets, or even quadruplets, which are written, as a general rule, clockwise. The IME, therefore, must take the input (usually based on a Korean alphabetical keyboard layout) while it is being typed, and it must adjust the size, spacing, and positioning of each of the letters as it puts them into appropriate clusters (see Figure 11-9).