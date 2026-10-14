
⇒ Here are two ways to use this.

- To output all of the synonyms for the noun “break,” type:
  $ wn break -synsn [RET]

- To output all of the synonyms for the verb “break,” type:
  $ wn break -synsv [RET]

## 11.2.4 Listing the Antonyms of a Word

An antonym of a word is a different word that has the opposite meaning of the first in some context. To output antonyms for a word with wn, give the word as an argument, followed by one of the following options: -antsv for verbs, -antsa for adjectives, or -antar for adverbs.

⇒ To output all of the antonyms for the adjective “sad,” type:

```
$ wn sad -antsa [RET]
```

## 11.2.5 Listing the Hypernyms of a Word

A hypernym of a word is a related term whose meaning is more general than the given word. (For example, the words “mammal” and “animal” are hypernyms of the word “cat.”)

To output hypernyms for a word with wn, use one of the following options: -hyper for nouns or -hypev for verbs.

⇒ To output all of the hypernyms for the noun “cat,” type:

```
$ wn cat -hyper [RET]
```

## 11.2.6 Checking Online Dictionaries

Dict
DEB: dict
RPM: dict
WWW: http://www.dict.org/

The DICT Development Group has a number of free dictionaries on its Web site [http://www.dict.org/]. On that page, you can look up words (including using a thesaurus and other searches) from a dictionary that contains over 300,000 headwords, or you can make a copy of its dictionary for use on your own system. A dict client exists for accessing DICT servers and outputting definitions locally; this tool is available in the dict package.

There are a number of specialized dictionaries available from the DICT Development Group as well. These dictionaries are plain text files. One such dictionary is called FILE, The Free Internet Lexicon and Encyclopedia. It is an effort to build a free, open source collection of modern-word, idiom, and jargon dictionaries. FILE is a volunteer effort and depends on the support of scholars and lexicographers; the DICT pages contain information on how to help contribute to this worthy project.

## 11.3 Checking Grammar

Diction
DEB: diction
WWW: http://www.gnu.org/software/diction/diction.html

Two venerable UNIX tools for checking writing have recently been made available for Linux-based systems: style and diction.

Old-timers probably remember these names—the originals came with AT&T UNIX as part of the much-loved “Writer’s Workbench” (WWB) suite of tools back in the late 1970s and early 1980s.

AT&T “unbundled” the Writer’s Workbench from its UNIX Version 7 product, and as the many flavors of UNIX blossomed over the years, these tools were lost by the wayside—eventually becoming the stuff of UNIX lore.

In 1997, Michael Haardt wrote new Linux versions of these tools from scratch. They support both the English and German languages, and they’re now part of the GNU Project.

Two additional commands that were part of the Writer’s Workbench have long been standard on Linux: look and spell, described previously in this chapter.

The following are recipes that use either diction or style.

### 11.3.1 Checking Text for Misused Phrases

Use diction to check for wordy, trite, clichéd, or misused phrases in a text. It checks for all the kind of expressions William Strunk warned us about in his Elements of Style [http://www.bartleby.com/141/].

There was also a set of tools for formatting text called the “Documenter’s Workbench” (DWB), and there was a planned “Reader’s Workbench”; today, we can only guess at what that might have been.

According to The UNIX Environment (see Appendix D [References for Further Interest], page 731), the diction tool that came with the old Writer's Workbench just found the phrases, and a separate command called suggest would output suggestions. In the GNU version that works for Linux systems, both functions have been combined in the single diction command.

In GNU diction, the words or phrases are enclosed in brackets "[like this]." If diction has any suggested replacements, it gives them preceded by a right arrow, "-> like this."

When checking more than just a screenful of text, you'll want to pipe the output to less so that you can peruse it on the screen (see Recipe 9.1 [Perusing Text], page 211), or pipe the output to a file for later examination.

⇒ Here are two ways to use this.

- To check the file dissertation for clichés or other misused phrases, type:
  $ diction dissertation | less [RET]

- To check the file dissertation for clichés or other misused phrases, and write the output to a file called dissertation.diction, type:
  $ diction dissertation > dissertation.diction [RET]

If you don't specify a file name, diction reads text from the standard input until you type <CTRL>-D on a line by itself. This is especially useful when you want to check a single sentence, as in Figure 11-3.

```
$ diction [RET]
Let us ask the question we wish to state. [RET]
(stdin):1: Let us [ask the question -> ask]
[we wish to state -> (cliche, avoid)].
<CTRL>-D
$
```

Figure 11-3. Checking a sentence with diction.

To check the text of a Web page, use lynx with the -dump and -nolist options to output the plain text of a given URL, and pipe this output to diction. (If you expect there to be a lot of output, add another pipe at the end to less so you can peruse it.)

To peruse the URL http://www.westegg.com/cliche/random.cgi with markings for possible wordy and misused phrases, type (all on one line):

```
$ lynx -dump -nolist http://www.westegg.com/cliche/random.cgi | diction | less [RET]
```
