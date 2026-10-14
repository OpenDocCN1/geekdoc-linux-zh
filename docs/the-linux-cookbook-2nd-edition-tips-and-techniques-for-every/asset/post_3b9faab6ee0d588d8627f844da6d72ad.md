
**NOTES.** To check text for overused words, use the method described in Recipe 12.2.4 [Counting Word Occurrences in Text], page 299.

### 11.3.2 Checking Text for Doubled Words

One of the things that `diction` looks for is doubled words—words repeated twice in a row. If it finds such a sequence, it encloses the second member of the doubled pair in brackets, followed by a right arrow and the text “Double word,” like “this [<i>th</i>is → Double word.]”

To check a text file for doubled words *only*, and not for any of the other things `diction` checks, use `grep` to find only those lines in `diction`’s output that contain the text “Double word,” if any.

⇒ To output all lines containing double words in the file `dissertation`, type:

```
```shell
$ diction dissertation | grep 'Double word' [RET]
```
```

### 11.3.3 Checking Text for Readability

The `style` command analyzes the writing style of a given text. It performs a number of readability tests on the text and outputs their results, and it gives some statistical information about the sentences of the text. Give as an argument the name of the text file to check.

⇒ To check the readability of the file `dissertation`, type:

```
```shell
$ style dissertation [RET]
```
```

Like `diction`, `style` reads text from the standard input if no text is given—this is useful for the end of a pipeline, or for checking the writing style of a particular sentence or other text you type.

The sentence characteristics of the text that `style` outputs are as follows:

- Number of characters
- Number of words, their average length, and their average number of syllables
- Number of sentences and average length in words
- Number of short and long sentences
- Number of paragraphs and average length in sentences
- Number of questions and imperatives

The various readability formulas that `style` uses and outputs are as follows:

- Kincaid formula, originally developed for Navy training manuals; a good readability test for technical documentation
- Automated Readability Index (ARI)
- Coleman-Liau formula
- Flesch Reading Ease Score, which gives an approximation of readability from 0 (difficult) to 100 (easy)
- Fog Index, which gives a school-grade reading level
- wSTF Index, a readability indicator for German documents
- Wheeler-Smith Index, Lix formula, and SMOG-Grading tests, all readability indicators that give a school-grade reading level

### 11.3.4 Checking Text for Difficult Sentences

To output just the “difficult” sentences of a text, use style with the -r option followed by a number; style will output only those sentences whose Automated Readability Index (ARI) is greater than the number you give.

⇒ To output all sentences in the file dissertation whose ARI is greater than a value of 20, type:

```
$ style -r 20 dissertation [RET]
```

### 11.3.5 Checking Text for Long Sentences

Use style to output sentences longer than a certain length by giving the number of words as an argument to the -l option.

⇒ To output all sentences longer than 14 words in the file dissertation, type:

```
$ style -l 14 dissertation [RET]
```

## 11.4 Using Reference Files

There are reference works and other informative text files that you can install on your system; the following recipes describe some of the more interesting and useful ones that are readily available.

To get an idea how the ARI ranks text, see its rankings for various popular Web sites at http://www.readability.info/commonscores.shtml.

### 11.4.1 Consulting Word Lists and Helpful Files

Miscfiles
DEB: miscfiles
WWW: ftp://ftp.gnu.org/pub/gnu/miscfiles/miscfiles-1.1.tar.gz

The GNU Miscfiles collection is a group of text files containing various facts and reference material, such as common abbreviations, telephone area codes, and English connective phrases.

The files are stored in the /usr/share/misc directory, and they are all compressed; use zless to peruse them (see Recipe 9.1 [Perusing Text], page 211).

The following table lists the files as they appear in /usr/share/misc and describes their contents.

| GNU-manifesto.gz | The GNU Manifesto. |
| abbrevs.talk.gz | Collections of common abbreviations used in electronic communication. |
| abbrevs.gen.gz | (This is the place to look to find the secrets of TTYL and LOL.) |
| airport.gz | List of three-letter city codes for some of the major airports. The city code is useful for querying the National Weather Service computers to get the latest weather report for your region. |
| ascii.gz | A chart of the ASCII character set. |
| birthtoken.gz | The traditional stone and flower tokens for each month. |
| cities.dat.gz | The population, political coordinates (nation, region), and geographic coordinates (latitude, longitude) of many major cities. |
| inter.phone.gz | International country and city telephone codes. |
| languages.gz | Two-letter codes for languages, from ISO 639. |
| latin1.gz | A chart of the extended ASCII character set, also known as the ISO 8859 ("Latin-1") character set. |
| mailinglists.gz | Description of all the public GNU Project mailing lists. |
