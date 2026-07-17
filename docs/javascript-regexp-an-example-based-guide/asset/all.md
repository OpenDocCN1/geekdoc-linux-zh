![](media/js_regexp.png)

1.  [Cover](text/cover.xhtml)
2.  [Table of contents](#nav.xhtml_toc)

# Preface

Scripting and automation tasks often need to extract particular portions of text from input data or modify them from one format to another. This book will help you learn Regular Expressions as implemented in JavaScript. Regular expressions can be considered as a mini-programming language in itself and is well suited for a variety of text processing needs.

The book heavily leans on examples to present features of regular expressions one by one. It is recommended that you manually type each example and experiment with them. Understanding both the nature of sample input string and the output produced is essential. As an analogy, consider learning to drive a bike or a car — no matter how much you read about them or listen to explanations, you need to practice a lot and infer your own conclusions. Should you feel that copy-paste is ideal for you, [code snippets are available chapter wise on GitHub](https://github.com/learnbyexample/learn_js_regexp/tree/master/code_snippets).

## Prerequisites

A good understanding of basic-level programming concepts and prior experience working with JavaScript. Should also know functional programming concepts like `map` and `filter`.

## Conventions

*   The examples presented here have been tested on Chrome/Chromium console (version 81+) and includes features not available in other browsers and platforms.
*   Code snippets shown are copy pasted from the console and modified for presentation purposes. Some of the commands are preceded by comments to provide context and explanations. Blank lines have been added to improve readability and output is skipped when it is `undefined` or otherwise unnecessary to be shown.
*   Unless otherwise noted, all examples and explanations are meant for *ASCII* characters.
*   External links are provided for further reading throughout the book. Not necessary to immediately visit them. They have been chosen with care and would help, especially during rereads.
*   The [learn_js_regexp](https://github.com/learnbyexample/learn_js_regexp) repo has all the code snippets and exercises and other details related to the book. Click the **Clone** button to get the files.

## Acknowledgements

*   [MDN: Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) — documentation and examples
*   [/r/learnjavascript/](https://www.reddit.com/r/learnjavascript/) and [/r/regex/](https://www.reddit.com/r/regex/) — helpful forums for beginners and experienced programmers alike
*   [stackoverflow](https://stackoverflow.com/) — for getting answers to pertinent questions on JavaScript and regular expressions
*   [tex.stackexchange](https://tex.stackexchange.com/) — for help on `pandoc` and `tex` related questions
*   Cover image: [LibreOffice Draw](https://www.libreoffice.org/discover/draw/) and [regulex](https://jex.im/regulex)
*   [Warning](https://commons.wikimedia.org/wiki/File:Warning_icon.svg) and [Info](https://commons.wikimedia.org/wiki/File:Info_icon_002.svg) icons by [Amada44](https://commons.wikimedia.org/wiki/User:Amada44) under public domain

## Feedback and Errata

I would highly appreciate if you'd let me know how you felt about this book, it would help to improve this book as well as my future attempts. Also, please do let me know if you spot any error or typo.

Issue Manager: [https://github.com/learnbyexample/learn_js_regexp/issues](https://github.com/learnbyexample/learn_js_regexp/issues)

Goodreads: [https://www.goodreads.com/book/show/49090622-javascript-regexp](https://www.goodreads.com/book/show/49090622-javascript-regexp)

E-mail: [learnbyexample.net@gmail.com](mailto:learnbyexample.net@gmail.com)

Twitter: [https://twitter.com/learn_byexample](https://twitter.com/learn_byexample)

## Author info

Sundeep Agarwal is a freelance trainer, author and mentor. His previous experience includes working as a Design Engineer at Analog Devices for more than 5 years. You can find his other works, primarily focused on Linux command line, text processing, scripting languages and curated lists, at [https://github.com/learnbyexample](https://github.com/learnbyexample). He has also been a technical reviewer for [Command Line Fundamentals](https://www.packtpub.com/application-development/command-line-fundamentals) book and video course published by Packt.

**List of books:** [https://learnbyexample.github.io/books/](https://learnbyexample.github.io/books/)

## License

This work is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-nc-sa/4.0/)

Code snippets are available under [MIT License](https://github.com/learnbyexample/learn_js_regexp/blob/master/LICENSE)

Resources mentioned in Acknowledgements section above are available under original licenses.

## Book version

1.5

See [Version_changes.md](https://github.com/learnbyexample/learn_js_regexp/blob/master/Version_changes.md) to track changes across book versions.

# What's so special about Regular Expressions?

Regular Expressions is a versatile tool for text processing. You'll find them included in the standard library of most programming languages that are used for scripting purposes. If not, you can usually find a third-party library. Syntax and features of regular expressions vary from language to language. JavaScript's syntax is similar to that of Perl language, but there are significant feature differences.

The [String object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) in JavaScript supports variety of methods to deal with text. So, what's so special about regular expressions and why would you need it? For learning and understanding purposes, one can view regular expressions as a mini programming language in itself, specialized for text processing. Parts of a regular expression can be saved for future use, analogous to variables. There are ways to perform AND, OR, NOT conditionals. Operations similar to range and repetition and so on.

Here's some common use cases:

*   Sanitizing a string to ensure that it satisfies a known set of rules. For example, to check if a given string matches password rules.
*   Filtering or extracting portions on an abstract level like alphabets, numbers, punctuation and so on.
*   Qualified string replacement. For example, at the start or the end of a string, only whole words, based on surrounding text, etc.

You are likely to be familiar with graphical search and replace tool, like the screenshot shown below from LibreOffice Writer. **Match case**, **Whole words only**, **Replace** and **Replace All** are some of the basic features supported by regular expressions.

![find and replace](media/file0.png)

Another real world use case is password validation. The screenshot below is from GitHub sign up page. Performing multiple checks like **string length** and the **type of characters allowed** is another core feature of regular expressions.

![password check](media/file1.png)

Here's some articles on regular expressions to know about its history and the type of problems it is suited for.

*   [The true power of regular expressions](https://nikic.github.io/2012/06/15/The-true-power-of-regular-expressions.html) — it also includes a nice explanation of what *regular* means in this context
*   [softwareengineering: Is it a must for every programmer to learn regular expressions?](https://softwareengineering.stackexchange.com/questions/133968/is-it-a-must-for-every-programmer-to-learn-regular-expressions)
*   [softwareengineering: When you should NOT use Regular Expressions?](https://softwareengineering.stackexchange.com/questions/113237/when-you-should-not-use-regular-expressions)
*   [codinghorror: Now You Have Two Problems](https://blog.codinghorror.com/regular-expressions-now-you-have-two-problems/)
*   [wikipedia: Regular expression](https://en.wikipedia.org/wiki/Regular_expression) — this article includes discussion on regular expressions as a formal language as well as details on various implementations

## How this book is organized

The book introduces concepts one by one and exercises at the end of chapters will require only the features introduced until that chapter. Each concept is accompanied by multiple examples to cover various angles of usage and corner cases. As mentioned before, follow along the illustrations by typing out the code snippets manually. It is important to understand both the nature of the sample input string as well as the actual programming command used. There are two interlude chapters that give an overview of useful external resources and some more resources are collated in the final chapter.

*   [RegExp introduction](#ch003.xhtml_regexp-introduction)
*   [Anchors](#ch004.xhtml_anchors)
*   [Alternation and Grouping](#ch005.xhtml_alternation-and-grouping)
*   [Escaping metacharacters](#ch006.xhtml_escaping-metacharacters)
*   [Dot metacharacter and Quantifiers](#ch007.xhtml_dot-metacharacter-and-quantifiers)
*   [Interlude: Tools for debugging and visualization](#ch008.xhtml_interlude-tools-for-debugging-and-visualization)
*   [Working with matched portions](#ch009.xhtml_working-with-matched-portions)
*   [Character class](#ch010.xhtml_character-class)
*   [Groupings and backreferences](#ch011.xhtml_groupings-and-backreferences)
*   [Interlude: Common tasks](#ch012.xhtml_interlude-common-tasks)
*   [Lookarounds](#ch013.xhtml_lookarounds)
*   [Unicode](#ch014.xhtml_unicode)
*   [Further Reading](#ch015.xhtml_further-reading)

By the end of the book, you should be comfortable with both writing and reading regular expressions, how to debug them and know when to *avoid* them.

# RegExp introduction

This chapter will get you started with defining RegExp objects and using them inside string methods. To keep it simple, the examples will not use special characters related to regular expressions. The main focus will be to get you comfortable with syntax and text processing examples. Two methods will be introduced in this chapter. The `test` method to search if the input contains a string and the `replace` method to substitute a portion of the input with something else.

> ![info](media/file2.svg) This book will use the terms **regular expressions** and **regexp** interchangeably. When specifically referring to a JavaScript object, **RegExp** will be used.

## Console and documentation

As mentioned in the [preface](#ch001.xhtml_preface), examples presented in this book have been tested on Chrome/Chromium console. Other browsers based on Chromium may also work. Use `Ctrl+Shift+J` shortcut from a new tab to open a console. Some variable names are reused across different chapters, open another tab in such cases to avoid errors.

See [MDN: Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) for documentation, examples and feature compatibility details.

## test method

First up, a simple example to test whether a string is part of another string or not. Normally, you'd use the `includes` method and pass a string as argument. For regular expressions, use the `test` method on a RegExp object, which is defined by the search string enclosed within `//` delimiters.

```
[](#cb1-1)> let sentence = 'This is a sample string'
[](#cb1-2)
[](#cb1-3)// check if 'sentence' contains the given string argument
[](#cb1-4)> sentence.includes('is')
[](#cb1-5)< true
[](#cb1-6)> sentence.includes('z')
[](#cb1-7)< false
[](#cb1-8)
[](#cb1-9)// check if 'sentence' matches the pattern as described by the regexp
[](#cb1-10)> /is/.test(sentence)
[](#cb1-11)< true
[](#cb1-12)> /z/.test(sentence)
[](#cb1-13)< false
```

Here's some examples of using the `test` method in conditional expressions.

```
[](#cb2-1)> let report = 'string theory'
[](#cb2-2)
[](#cb2-3)> if (/ring/.test(report)) {
[](#cb2-4)      console.log('mission success')
[](#cb2-5)  }
[](#cb2-6)< mission success
[](#cb2-7)
[](#cb2-8)> if (!/fire/.test(report)) {
[](#cb2-9)      console.log('mission failed')
[](#cb2-10)  }
[](#cb2-11)< mission failed
```

And here's some array processing examples.

```
[](#cb3-1)> let words = ['cat', 'attempt', 'tattle']
[](#cb3-2)
[](#cb3-3)// get all elements that contain 'tt'
[](#cb3-4)> words.filter(w => /tt/.test(w))
[](#cb3-5)< ["attempt", "tattle"]
[](#cb3-6)
[](#cb3-7)// check if all the elements contain 'at'
[](#cb3-8)> words.every(w => /at/.test(w))
[](#cb3-9)< true
[](#cb3-10)
[](#cb3-11)// check if any element contains 'stat'
[](#cb3-12)> words.some(w => /stat/.test(w))
[](#cb3-13)< false
```

## Flags

Some of the regular expressions functionality is enabled by passing flags, represented by an alphabet character. If you have used command line, flags are similar to command options, for example `grep -i` will perform case insensitive matching.

In this chapter, two flags will be discussed:

*   `i` flag to ignore case while matching alphabets (default is case sensitive matching)
*   `g` flag to match all occurrences (by default only the first one is matched)

Examples for `i` flag is shown below. `g` flag will be discussed in [replace method](#ch003.xhtml_replace-method) section later in this chapter.

```
[](#cb4-1)> /cat/.test('CaT')
[](#cb4-2)< false
[](#cb4-3)> /cat/i.test('CaT')
[](#cb4-4)< true
[](#cb4-5)
[](#cb4-6)> ['Cat', 'cot', 'CATER', 'SCat', 'ScUtTLe'].filter(w => /cat/i.test(w))
[](#cb4-7)< ["Cat", "CATER", "SCat"]
```

## RegExp constructor and reuse

The RegExp object can be saved in a variable. This helps to improve code clarity, enable reuse, etc.

```
[](#cb5-1)> const pet = /dog/
[](#cb5-2)
[](#cb5-3)> pet.test('They bought a dog')
[](#cb5-4)< true
[](#cb5-5)> pet.test('A cat crossed their path')
[](#cb5-6)< false
```

RegExp objects can also be constructed using the `RegExp()` constructor. The first argument is either a string or a RegExp object. The second argument is used to specify one or more flags.

```
[](#cb6-1)> const pat = new RegExp('dog')
[](#cb6-2)> pat
[](#cb6-3)< /dog/
[](#cb6-4)
[](#cb6-5)// if flags are needed, specify them as the second argument
[](#cb6-6)> new RegExp('dog', 'i')
[](#cb6-7)< /dog/i
```

The main advantage of the constructor over `//` literal is the ability to dynamically construct the regexp using `${}` to insert content of other variables or the result of an expression.

```
[](#cb7-1)> let greeting = 'hi'
[](#cb7-2)
[](#cb7-3)> const pat1 = new RegExp(`${greeting} there`)
[](#cb7-4)> pat1
[](#cb7-5)< /hi there/
[](#cb7-6)
[](#cb7-7)> new RegExp(`${greeting.toUpperCase()} there`)
[](#cb7-8)< /HI there/
```

## replace method

The `replace` string method is used for search and replace operations.

```
[](#cb8-1)// change only the first match
[](#cb8-2)> '1,2,3,4'.replace(/,/, '-')
[](#cb8-3)< "1-2,3,4"
[](#cb8-4)
[](#cb8-5)// change all the matches by adding 'g' flag
[](#cb8-6)> '1,2,3,4'.replace(/,/g, '-')
[](#cb8-7)< "1-2-3-4"
[](#cb8-8)
[](#cb8-9)// multiple flags can be combined
[](#cb8-10)> 'cArT PART tart mArt'.replace(/art/ig, '2')
[](#cb8-11)< "c2 P2 t2 m2"
```

> ![warning](media/file3.svg) A common mistake is forgetting that strings are immutable. If you want to save the changes to the same variable, you need to explicitly assign the result back to that variable.

```
[](#cb9-1)> let word = 'cater'
[](#cb9-2)
[](#cb9-3)// this will return a string but won't modify the 'word' variable
[](#cb9-4)> word.replace(/cat/, 'hack')
[](#cb9-5)< "hacker"
[](#cb9-6)> word
[](#cb9-7)< "cater"
[](#cb9-8)
[](#cb9-9)// need to explicitly assign the result for in-place modification
[](#cb9-10)> word = word.replace(/cat/, 'hack')
[](#cb9-11)< "hacker"
[](#cb9-12)> word
[](#cb9-13)< "hacker"
```

> ![warning](media/file3.svg) The use of `g` flag with `test` method allows some additional functionality. See [MDN: test](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test#Examples) for examples. However, in my opinion, it is easy to fall into a habit of using `g` with `test` and get undesired results. I'd rather suggest to use [match method](#ch009.xhtml_match-method) and explicitly write logic instead of relying on `test` with `g` flag.

## Cheatsheet and Summary

| Note | Description |
| --- | --- |
| [MDN: Regular Expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) | MDN documentation for JavaScript regular expressions |
| `/pat/` | a RegExp object |
| `const p1 = /pat/` | save regexp in a variable for reuse, clarity, etc |
| `/pat/.test(s)` | Check if given pattern is present anywhere in input string |
|  | returns `true` or `false` |
| `i` | flag to ignore case when matching alphabets |
| `g` | flag to match all occurrences |
| `new RegExp('pat', 'i')` | construct RegExp from a string |
|  | optional second argument specifies flags |
|  | use backtick strings with `${}` for interpolation |
| `s.replace(/pat/, 'repl')` | method for search and replace |

This chapter introduced how to define RegExp objects and use them with `test` and `replace` methods. You also learnt how to use flags to change the default behavior of regexps. The examples presented were more focused on introducing text processing concepts. Next chapter onwards, you'll learn regular expression syntax and features.

## Exercises

> ![info](media/file2.svg) All the exercises are also collated together in one place at [Exercises.md](https://github.com/learnbyexample/learn_js_regexp/blob/master/Exercises.md).

> ![info](media/file2.svg) For solutions, see [Exercise_solutions.md](https://github.com/learnbyexample/learn_js_regexp/blob/master/Exercise_solutions.md).

**a)** Check if the given input strings contain `two` irrespective of case.

```
[](#cb10-1)> let s1 = 'Their artwork is exceptional'
[](#cb10-2)> let s2 = 'one plus tw0 is not three'
[](#cb10-3)> let s3 = 'TRUSTWORTHY'
[](#cb10-4)
[](#cb10-5)> const pat1 =      // add your solution here
[](#cb10-6)
[](#cb10-7)> pat1.test(s1)
[](#cb10-8)< true
[](#cb10-9)> pat1.test(s2)
[](#cb10-10)< false
[](#cb10-11)> pat1.test(s3)
[](#cb10-12)< true
```

**b)** For the given array, filter all elements that do *not* contain `e`.

```
[](#cb11-1)> let items = ['goal', 'new', 'user', 'sit', 'eat', 'dinner']
[](#cb11-2)
[](#cb11-3)> items.filter(w => test(w))       // add your solution here
[](#cb11-4)< ["goal", "sit"]
```

**c)** Replace first occurrence of `5` with `five` for the given string.

```
[](#cb12-1)> let ip = 'They ate 5 apples and 5 oranges'
[](#cb12-2)
[](#cb12-3)> ip.replace()       // add your solution here
[](#cb12-4)< "They ate five apples and 5 oranges"
```

**d)** Replace all occurrences of `5` with `five` for the given string.

```
[](#cb13-1)> let ip = 'They ate 5 apples and 5 oranges'
[](#cb13-2)
[](#cb13-3)> ip.replace()      // add your solution here
[](#cb13-4)< "They ate five apples and five oranges"
```

**e)** Replace all occurrences of `note` irrespective of case with `X`.

```
[](#cb14-1)> let ip = 'This note should not be NoTeD'
[](#cb14-2)
[](#cb14-3)> ip.replace()     // add your solution here
[](#cb14-4)< "This X should not be XD"
```

**f)** For the given multiline input string, filter all lines NOT containing the string `2`.

```
[](#cb15-1)> let purchases = `items qty
[](#cb15-2)apple 24
[](#cb15-3)mango 50
[](#cb15-4)guava 42
[](#cb15-5)onion 31
[](#cb15-6)water 10`
[](#cb15-7)
[](#cb15-8)> const num =       // add your solution here
[](#cb15-9)
[](#cb15-10)> console.log(purchases.split('\n')
[](#cb15-11)                       .filter(e => test(e))       // add your solution here
[](#cb15-12)                       .join('\n'))
[](#cb15-13)< items qty
[](#cb15-14)  mango 50
[](#cb15-15)  onion 31
[](#cb15-16)  water 10
```

> ![info](media/file2.svg) You'd be able to solve this using just `replace` method by the end of [Dot metacharacter and Quantifiers](#ch007.xhtml_dot-metacharacter-and-quantifiers) chapter.

**g)** For the given array, filter all elements that contains either `a` or `w`.

```
[](#cb16-1)> let items = ['goal', 'new', 'user', 'sit', 'eat', 'dinner']
[](#cb16-2)
[](#cb16-3)> items.filter(w => test(w) || test(w))     // add your solution here
[](#cb16-4)< ["goal", "new", "eat"]
```

**h)** For the given array, filter all elements that contains both `e` and `n`.

```
[](#cb17-1)> let items = ['goal', 'new', 'user', 'sit', 'eat', 'dinner']
[](#cb17-2)
[](#cb17-3)> items.filter(w => test(w) && test(w))     // add your solution here
[](#cb17-4)< ["new", "dinner"]
```

**i)** For the given string, replace `0xA0` with `0x7F` and `0xC0` with `0x1F`.

```
[](#cb18-1)> let ip = 'start address: 0xA0, func1 address: 0xC0'
[](#cb18-2)
[](#cb18-3)> ip.replace()        // add your solution here
[](#cb18-4)< "start address: 0x7F, func1 address: 0x1F"
```

# Anchors

In this chapter, you'll be learning about qualifying a pattern. Instead of matching anywhere in the given input string, restrictions can be specified. For now, you'll see the ones that are already part of regular expression features. In later chapters, you'll learn how to define your own rules for restriction.

These restrictions are made possible by assigning special meaning to certain characters and escape sequences. The characters with special meaning are known as **metacharacters** in regexp parlance. In case you need to match those characters literally, you need to escape them with a `\` character (discussed in [Escaping metacharacters](#ch006.xhtml_escaping-metacharacters) chapter).

## String anchors

This restriction is about qualifying a regexp to match only at the start or end of an input string. These provide functionality similar to the string methods `startsWith` and `endsWith`. First up is `^` metacharacter, which restricts the matching to the start of string.

```
[](#cb19-1)// ^ is placed as a prefix to the pattern
[](#cb19-2)> /^cat/.test('cater')
[](#cb19-3)< true
[](#cb19-4)> /^cat/.test('concatenation')
[](#cb19-5)< false
[](#cb19-6)
[](#cb19-7)> /^hi/.test('hi hello\ntop spot')
[](#cb19-8)< true
[](#cb19-9)> /^top/.test('hi hello\ntop spot')
[](#cb19-10)< false
```

To restrict the match to the end of string, `$` metacharacter is used.

```
[](#cb20-1)// $ is placed as a suffix to the pattern
[](#cb20-2)> /are$/.test('spare')
[](#cb20-3)< true
[](#cb20-4)> /are$/.test('nearest')
[](#cb20-5)< false
[](#cb20-6)
[](#cb20-7)> let words = ['surrender', 'unicorn', 'newer', 'door', 'empty', 'eel', 'pest']
[](#cb20-8)> words.filter(w => /er$/.test(w))
[](#cb20-9)< ["surrender", "newer"]
[](#cb20-10)> words.filter(w => /t$/.test(w))
[](#cb20-11)< ["pest"]
```

Combining both the start and end string anchors, you can restrict the matching to the whole string. Similar to comparing strings using the `==` operator.

```
[](#cb21-1)> /^cat$/.test('cat')
[](#cb21-2)< true
[](#cb21-3)> /^cat$/.test('cater')
[](#cb21-4)< false
```

The anchors can be used by themselves as a pattern. Helps to insert text at the start or end of string, emulating string concatenation operations. These might not feel like useful capability, but combined with other regexp features they become quite a handy tool.

```
[](#cb22-1)> 'live'.replace(/^/, 're')
[](#cb22-2)< "relive"
[](#cb22-3)> 'send'.replace(/^/, 're')
[](#cb22-4)< "resend"
[](#cb22-5)
[](#cb22-6)> 'cat'.replace(/$/, 'er')
[](#cb22-7)< "cater"
[](#cb22-8)> 'hack'.replace(/$/, 'er')
[](#cb22-9)< "hacker"
```

## Line anchors

A string input may contain single or multiple lines. The `\r`, `\n`, `\u2028` (line separator) and `\u2029` (paragraph separator) characters are considered as line separators. When the `m` flag is used, the `^` and `$` anchors will match the start and end of every line respectively.

```
[](#cb23-1)// check if any line in the string starts with 'top'
[](#cb23-2)> /^top/m.test('hi hello\ntop spot')
[](#cb23-3)< true
[](#cb23-4)
[](#cb23-5)// check if any line in the string ends with 'er'
[](#cb23-6)> /er$/m.test('spare\npar\nera\ndare')
[](#cb23-7)< false
[](#cb23-8)
[](#cb23-9)// check if any complete line in the string is 'par'
[](#cb23-10)> /^par$/m.test('spare\npar\nera\ndare')
[](#cb23-11)< true
```

Just like string anchors, you can use the line anchors by themselves as a pattern.

```
[](#cb24-1)> let items = 'catapults\nconcatenate\ncat'
[](#cb24-2)
[](#cb24-3)> console.log(items.replace(/^/gm, '* '))
[](#cb24-4)< * catapults
[](#cb24-5)  * concatenate
[](#cb24-6)  * cat
[](#cb24-7)
[](#cb24-8)> console.log(items.replace(/$/gm, '.'))
[](#cb24-9)< catapults.
[](#cb24-10)  concatenate.
[](#cb24-11)  cat.
```

> ![warning](media/file3.svg) If there is a line separator character at the end of string, there is an additional start/end of line match after the separator.

```
[](#cb25-1)// 'foo ' is inserted three times
[](#cb25-2)> '1\n2\n'.replace(/^/mg, 'foo ')
[](#cb25-3)< "foo 1
[](#cb25-4)  foo 2
[](#cb25-5)  foo "
[](#cb25-6)
[](#cb25-7)> '1\n2\n'.replace(/$/mg, ' baz')
[](#cb25-8)< "1 baz
[](#cb25-9)  2 baz
[](#cb25-10)   baz"
```

> ![warning](media/file3.svg) If you are dealing with Windows OS based text files, you may have to convert `\r\n` line endings to `\n` first. Otherwise, you'll get end of line matches for both `\r` and `\n` characters. You can also handle this case in regexp by making `\r` as optional character with quantifiers (see [Greedy quantifiers](#ch007.xhtml_greedy-quantifiers) section).

## Word anchors

The third type of restriction is word anchors. Alphabets (irrespective of case), digits and the underscore character qualify as word characters. You might wonder why there are digits and underscores as well, why not only alphabets? This comes from variable and function naming conventions — typically alphabets, digits and underscores are allowed. So, the definition is more oriented to programming languages than natural ones.

The escape sequence `\b` denotes a word boundary. This works for both the start of word and end of word anchoring. Start of word means either the character prior to the word is a non-word character or there is no character (start of string). Similarly, end of word means the character after the word is a non-word character or no character (end of string). This implies that you cannot have word boundary `\b` without a word character.

```
[](#cb26-1)> let sample = 'par spar apparent spare part'
[](#cb26-2)
[](#cb26-3)// replace 'par' irrespective of where it occurs
[](#cb26-4)> sample.replace(/par/g, 'X')
[](#cb26-5)< "X sX apXent sXe Xt"
[](#cb26-6)// replace 'par' only at the start of word
[](#cb26-7)> sample.replace(/\bpar/g, 'X')
[](#cb26-8)< "X spar apparent spare Xt"
[](#cb26-9)// replace 'par' only at the end of word
[](#cb26-10)> sample.replace(/par\b/g, 'X')
[](#cb26-11)< "X sX apparent spare part"
[](#cb26-12)// replace 'par' only if it is not part of another word
[](#cb26-13)> sample.replace(/\bpar\b/g, 'X')
[](#cb26-14)< "X spar apparent spare part"
```

You can get lot more creative with using word boundary as a pattern by itself.

```
[](#cb27-1)// space separated words to double quoted csv
[](#cb27-2)// note that 'replace' method is used twice here
[](#cb27-3)> let sample = 'par spar apparent spare part'
[](#cb27-4)> console.log(sample.replace(/\b/g, '"').replace(/ /g, ','))
[](#cb27-5)< "par","spar","apparent","spare","part"
[](#cb27-6)
[](#cb27-7)// make a programming statement more readable
[](#cb27-8)// shown for illustration purpose only, won't work for all cases
[](#cb27-9)> 'foo_baz=num1+35*42/num2'.replace(/\b/g, ' ')
[](#cb27-10)< " foo_baz = num1 + 35 * 42 / num2 "
[](#cb27-11)// excess space at start/end of string can be trimmed off
[](#cb27-12)// later you'll learn how to add a qualifier so that trim is not needed
[](#cb27-13)> 'foo_baz=num1+35*42/num2'.replace(/\b/g, ' ').trim()
[](#cb27-14)< "foo_baz = num1 + 35 * 42 / num2"
```

The word boundary has an opposite anchor too. `\B` matches wherever `\b` doesn't match. This duality will be seen later with some other escape sequences too.

```
[](#cb28-1)> let sample = 'par spar apparent spare part'
[](#cb28-2)
[](#cb28-3)// replace 'par' if it is not start of word
[](#cb28-4)> sample.replace(/\Bpar/g, 'X')
[](#cb28-5)< "par sX apXent sXe part"
[](#cb28-6)// replace 'par' at the end of word but not whole word 'par'
[](#cb28-7)> sample.replace(/\Bpar\b/g, 'X')
[](#cb28-8)< "par sX apparent spare part"
[](#cb28-9)// replace 'par' if it is not end of word
[](#cb28-10)> sample.replace(/par\B/g, 'X')
[](#cb28-11)< "par spar apXent sXe Xt"
[](#cb28-12)// replace 'par' if it is surrounded by word characters
[](#cb28-13)> sample.replace(/\Bpar\B/g, 'X')
[](#cb28-14)< "par spar apXent sXe part"
```

Here's some standalone pattern usage to compare and contrast the two word anchors.

```
[](#cb29-1)> 'copper'.replace(/\b/g, ':')
[](#cb29-2)< ":copper:"
[](#cb29-3)> 'copper'.replace(/\B/g, ':')
[](#cb29-4)< "c:o:p:p:e:r"
[](#cb29-5)
[](#cb29-6)> '-----hello-----'.replace(/\b/g, ' ')
[](#cb29-7)< "----- hello -----"
[](#cb29-8)> '-----hello-----'.replace(/\B/g, ' ')
[](#cb29-9)< " - - - - -h e l l o- - - - - "
```

> ![warning](media/file3.svg) Negative logic is handy in many text processing situations. But use it with care as you might end up matching things you didn't intend!

## Cheatsheet and Summary

| Note | Description |
| --- | --- |
| metacharacter | characters with special meaning in regexp |
| `^` | restricts the match to the start of string |
| `$` | restricts the match to the end of string |
| `m` | flag to match the start/end of line with `^` and `$` anchors |
|  | `\r`, `\n`, `\u2028` and `\u2029` are line separators |
|  | dos-style files use `\r\n`, may need special attention |
| `\b` | restricts the match to the start/end of words |
|  | word characters: alphabets, digits, underscore |
| `\B` | matches wherever `\b` doesn't match |

In this chapter, you've begun to see building blocks of regular expressions and how they can be used in interesting ways. But at the same time, regular expression is but another tool in the land of text processing. Often, you'd get simpler solution by combining regular expressions with normal string methods. Practice, experience and imagination would help you construct creative solutions. In coming chapters, you'll see more applications of anchors in combination with other regexp features.

## Exercises

**a)** Check if the given input strings contain `is` or `the` as whole words.

```
[](#cb30-1)> let str1 = 'is; (this)'
[](#cb30-2)> let str2 = "The food isn't good"
[](#cb30-3)> let str3 = 'the2 cats'
[](#cb30-4)> let str4 = 'switch on the light'
[](#cb30-5)
[](#cb30-6)> const pat1 =      // add your solution here
[](#cb30-7)> const pat2 =      // add your solution here
[](#cb30-8)
[](#cb30-9)> pat1.test(str1) || pat2.test(str1)
[](#cb30-10)< true
[](#cb30-11)> pat1.test(str2) || pat2.test(str2)
[](#cb30-12)< false
[](#cb30-13)> pat1.test(str3) || pat2.test(str3)
[](#cb30-14)< false
[](#cb30-15)> pat1.test(str4) || pat2.test(str4)
[](#cb30-16)< true
```

**b)** For the given input string, change only whole word `red` to `brown`

```
[](#cb31-1)> let ip = 'bred red spread credible red;'
[](#cb31-2)
[](#cb31-3)> ip.replace()       // add your solution here
[](#cb31-4)< "bred brown spread credible brown;"
```

**c)** For the given array, filter all elements that contains `42` surrounded by word characters.

```
[](#cb32-1)> let items = ['hi42bye', 'nice1423', 'bad42', 'cool_42a', 'fake4b']
[](#cb32-2)
[](#cb32-3)> items.filter(e => test(e))       // add your solution here
[](#cb32-4)< ["hi42bye", "nice1423", "cool_42a"]
```

**d)** For the given input array, filter all elements that start with `den` or end with `ly`

```
[](#cb33-1)> let items = ['lovely', '1\ndentist', '2 lonely', 'eden', 'fly\n', 'dent']
[](#cb33-2)
[](#cb33-3)> items.filter(e => test(e) || test(e))        // add your solution here
[](#cb33-4)< ["lovely", "2 lonely", "dent"]
```

**e)** For the given input string, change whole word `mall` to `1234` only if it is at the start of line.

```
[](#cb34-1)> let para = `ball fall wall tall
[](#cb34-2)mall call ball pall
[](#cb34-3)wall mall ball fall
[](#cb34-4)mallet wallet malls`
[](#cb34-5)
[](#cb34-6)> console.log(para.replace())        // add your solution here
[](#cb34-7)< ball fall wall tall
[](#cb34-8)  1234 call ball pall
[](#cb34-9)  wall mall ball fall
[](#cb34-10)  mallet wallet malls
```

**f)** For the given array, filter all elements having a line starting with `den` or ending with `ly`.

```
[](#cb35-1)> let items = ['lovely', '1\ndentist', '2 lonely', 'eden', 'fly\nfar', 'dent']
[](#cb35-2)
[](#cb35-3)> items.filter(e => test(e) || test(e))      // add your solution here
[](#cb35-4)< ["lovely", "1\ndentist", "2 lonely", "fly\nfar", "dent"]
```

**g)** For the given input array, filter all whole elements `12\nthree` irrespective of case.

```
[](#cb36-1)> let items = ['12\nthree\n', '12\nThree', '12\nthree\n4', '12\nthree']
[](#cb36-2)
[](#cb36-3)> items.filter(e => test(e))     // add your solution here
[](#cb36-4)< ["12\nThree", "12\nthree"]
```

**h)** For the given input array, replace `hand` with `X` for all words that start with `hand` followed by at least one word character.

```
[](#cb37-1)> let items = ['handed', 'hand', 'handy', 'unhanded', 'handle', 'hand-2']
[](#cb37-2)
[](#cb37-3)> items.map(w => w.replace())        // add your solution here
[](#cb37-4)< ["Xed", "hand", "Xy", "unhanded", "Xle", "hand-2"]
```

**i)** For the given input array, filter all elements starting with `h`. Additionally, replace `e` with `X` for these filtered elements.

```
[](#cb38-1)> let items = ['handed', 'hand', 'handy', 'unhanded', 'handle', 'hand-2']
[](#cb38-2)
[](#cb38-3)> items.filter(w => test(w)).map(w => w.replace())        // add your solution here
[](#cb38-4)< ["handXd", "hand", "handy", "handlX", "hand-2"]
```

**j)** Why does the following code show `false` instead of `true`?

```
[](#cb39-1)> /end$/.test('bend it\nand send\n')
[](#cb39-2)< false
```

# Alternation and Grouping

Many a times, you want to check if the input string matches multiple patterns. For example, whether a car color is *green* or *blue* or *red*. In programming terms, you need to perform OR conditional. This chapter will show how to use alternation for such cases. These patterns can also have some common elements between them, in which case grouping helps to form terser regexps. This chapter will also discuss the precedence rules used to determine which alternation wins.

## OR conditional

In a conditional expression, you can use the logical operators to combine multiple conditions. With regular expressions, the `|` metacharacter is similar to logical OR. The regexp will match if any of the expression separated by `|` is satisfied. Each of these alternations is a full regexp. For example, anchors are specific to that particular alternation.

```
[](#cb40-1)// match either 'cat' or 'dog'
[](#cb40-2)> const pets = /cat|dog/
[](#cb40-3)> pets.test('I like cats')
[](#cb40-4)< true
[](#cb40-5)> pets.test('I like dogs')
[](#cb40-6)< true
[](#cb40-7)> pets.test('I like parrots')
[](#cb40-8)< false
[](#cb40-9)
[](#cb40-10)// replace either 'cat' at start of string or 'cat' at end of word
[](#cb40-11)> 'catapults concatenate cat scat'.replace(/^cat|cat\b/g, 'X')
[](#cb40-12)< "Xapults concatenate X sX"
[](#cb40-13)
[](#cb40-14)// replace either 'cat' or 'dog' or 'fox' with 'mammal'
[](#cb40-15)> 'cat dog bee parrot fox'.replace(/cat|dog|fox/g, 'mammal')
[](#cb40-16)< "mammal mammal bee parrot mammal"
```

> ![info](media/file2.svg) You might infer from the above examples that there can be situations where many alternations are required. See [Dynamically building alternation](#ch006.xhtml_dynamically-building-alternation) section for examples and details.

## Grouping

Often, there are some common things among the regexp alternatives. It could be common characters or regexp qualifiers like the anchors. In such cases, you can group them using a pair of parentheses metacharacters. Similar to `a(b+c)d = abd+acd` in maths, you get `a(b|c)d = abd|acd` in regular expressions.

```
[](#cb41-1)// without grouping
[](#cb41-2)> 'red reform read arrest'.replace(/reform|rest/g, 'X')
[](#cb41-3)< "red X read arX"
[](#cb41-4)// with grouping
[](#cb41-5)> 'red reform read arrest'.replace(/re(form|st)/g, 'X')
[](#cb41-6)< "red X read arX"
[](#cb41-7)
[](#cb41-8)// without grouping
[](#cb41-9)> 'par spare part party'.replace(/\bpar\b|\bpart\b/g, 'X')
[](#cb41-10)< "X spare X party"
[](#cb41-11)// taking out common anchors
[](#cb41-12)> 'par spare part party'.replace(/\b(par|part)\b/g, 'X')
[](#cb41-13)< "X spare X party"
[](#cb41-14)// taking out common characters as well
[](#cb41-15)// you'll later learn a better technique instead of using empty alternate
[](#cb41-16)> 'par spare part party'.replace(/\bpar(|t)\b/g, 'X')
[](#cb41-17)< "X spare X party"
```

> ![info](media/file2.svg) There's plenty more features to grouping than just forming terser regexp. It will be discussed as they become relevant in coming chapters.

## Precedence rules

There's some tricky situations when using alternation. If it is used for testing a match to get `true/false` against a string input, there is no ambiguity. However, for other things like string replacement, it depends on a few factors. Say, you want to replace either `are` or `spared` — which one should get precedence? The bigger word `spared` or the substring `are` inside it or based on something else?

The regexp alternative which matches earliest in the input string gets precedence.

```
[](#cb42-1)> let words = 'lion elephant are rope not'
[](#cb42-2)
[](#cb42-3)// starting index of 'on' < index of 'ant' for given string input
[](#cb42-4)// so 'on' will be replaced irrespective of order of alternations
[](#cb42-5)> words.replace(/on|ant/, 'X')
[](#cb42-6)< "liX elephant are rope not"
[](#cb42-7)> words.replace(/ant|on/, 'X')
[](#cb42-8)< "liX elephant are rope not"
```

So, what happens if two or more alternatives match on same index? The precedence is then left to right in the order of declaration.

```
[](#cb43-1)> let mood = 'best years'
[](#cb43-2)
[](#cb43-3)// starting index for 'year' and 'years' will always be same
[](#cb43-4)// so, which one gets replaced depends on the order of alternations
[](#cb43-5)> mood.replace(/year|years/, 'X')
[](#cb43-6)< "best Xs"
[](#cb43-7)> mood.replace(/years|year/, 'X')
[](#cb43-8)< "best X"
```

Another example with `replace` to drive home the issue.

```
[](#cb44-1)> let sample = 'ear xerox at mare part learn eye'
[](#cb44-2)
[](#cb44-3)// this is going to be same as: replace(/ar/g, 'X')
[](#cb44-4)> sample.replace(/ar|are|art/g, 'X')
[](#cb44-5)< "eX xerox at mXe pXt leXn eye"
[](#cb44-6)// this is going to be same as: replace(/are|ar/g, 'X')
[](#cb44-7)> sample.replace(/are|ar|art/g, 'X')
[](#cb44-8)< "eX xerox at mX pXt leXn eye"
[](#cb44-9)// phew, finally this one works as expected
[](#cb44-10)> sample.replace(/are|art|ar/g, 'X')
[](#cb44-11)< "eX xerox at mX pX leXn eye"
```

## Cheatsheet and Summary

| Note | Description |
| --- | --- |
| `pat1&#124;pat2&#124;pat3` | multiple regexp combined as OR conditional |
|  | each alternative can have independent anchors |
| `()` | group pattern(s) |
| `a(b&#124;c)d` | same as `abd&#124;acd` |
| Alternation precedence | pattern which matches earliest in the input gets precedence |
|  | tie-breaker is left to right if matches have same starting location |

So, this chapter was about specifying one or more alternate matches within the same regexp using `|` metacharacter. Which can further be simplified using `()` grouping if there are common aspects. Among the alternations, earliest matching pattern gets precedence. Left to right ordering is used as a tie-breaker if multiple alternations match starting from the same location. In the next chapter, you'll learn how to construct alternation from an array of strings taking care of precedence rules. Grouping has various other uses too, which will be discussed in coming chapters.

## Exercises

**a)** For the given input array, filter all elements that start with `den` or end with `ly`

```
[](#cb45-1)> let items = ['lovely', '1\ndentist', '2 lonely', 'eden', 'fly\n', 'dent']
[](#cb45-2)
[](#cb45-3)> items.filter()        // add your solution here
[](#cb45-4)< ["lovely", "2 lonely", "dent"]
```

**b)** For the given array, filter all elements having a line starting with `den` or ending with `ly`

```
[](#cb46-1)> let items = ['lovely', '1\ndentist', '2 lonely', 'eden', 'fly\nfar', 'dent']
[](#cb46-2)
[](#cb46-3)> items.filter()        // add your solution here
[](#cb46-4)< ["lovely", "1\ndentist", "2 lonely", "fly\nfar", "dent"]
```

**c)** For the given input strings, replace all occurrences of `removed` or `reed` or `received` or `refused` with `X`.

```
[](#cb47-1)> let s1 = 'creed refuse removed read'
[](#cb47-2)> let s2 = 'refused reed redo received'
[](#cb47-3)
[](#cb47-4)> const pat1 =      // add your solution here
[](#cb47-5)
[](#cb47-6)> s1.replace(pat1, 'X')
[](#cb47-7)< "cX refuse X read"
[](#cb47-8)> s2.replace(pat1, 'X')
[](#cb47-9)< "X X redo X"
```

**d)** For the given input strings, replace `late` or `later` or `slated` with `A`.

```
[](#cb48-1)> let str1 = 'plate full of slate'
[](#cb48-2)> let str2 = "slated for later, don't be late"
[](#cb48-3)
[](#cb48-4)> const pat2 =      // add your solution here
[](#cb48-5)
[](#cb48-6)> str1.replace(pat2, 'A')
[](#cb48-7)< "pA full of sA"
[](#cb48-8)> str2.replace(pat2, 'A')
[](#cb48-9)< "A for A, don't be A"
```

# Escaping metacharacters

You have seen a few metacharacters and escape sequences that help to compose a RegExp literal. There's also the `/` character used as a delimiter for RegExp objects. This chapter will discuss how to remove the special meaning of such constructs. Also, you'll learn how to take care of special characters when you are building a RegExp literal from normal strings.

## Escaping with \

To match the metacharacters literally, i.e. to remove their special meaning, prefix those characters with a `\` character. To indicate a literal `\` character, use `\\`.

```
[](#cb49-1)// even though ^ is not being used as anchor, it won't be matched literally
[](#cb49-2)> /b^2/.test('a^2 + b^2 - C*3')
[](#cb49-3)< false
[](#cb49-4)// escaping will work
[](#cb49-5)> /b\^2/.test('a^2 + b^2 - C*3')
[](#cb49-6)< true
[](#cb49-7)
[](#cb49-8)> '(a*b) + c'.replace(/\(|\)/g, '')
[](#cb49-9)< "a*b + c"
[](#cb49-10)
[](#cb49-11)> '\\learn\\by\\example'.replace(/\\/g, '/')
[](#cb49-12)< "/learn/by/example"
```

## Dynamically escaping metacharacters

When you are defining the regexp yourself, you can manually escape the metacharacters where needed. However, if you have strings obtained from elsewhere and need to match the contents literally, you'll have to somehow escape all the metacharacters while constructing the regexp. The solution of course is to use regular expressions! Usually, the programming language itself would provide an in-built method for such cases. JavaScript doesn't, but [MDN: Regular Expressions doc](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) has it covered in the form of a function as shown below.

```
[](#cb50-1)> function escapeRegExp(string) {
[](#cb50-2)    return string.replace(/[.*+\-?^${}()|[\]\\]/g, '\\$&')
[](#cb50-3)  }
```

There are many things in the above regexp that you haven't learnt yet. They'll be discussed in coming chapters. For now, it is enough to know that this function will automatically escape all the metacharacters. Examples are shown below.

```
[](#cb51-1)// sample input on which regexp will be applied
[](#cb51-2)> let eqn = 'f*(a^b) - 3*(a^b)'
[](#cb51-3)// sample string obtained from elsewhere which needs to be matched literally
[](#cb51-4)> const usr_str = '(a^b)'
[](#cb51-5)
[](#cb51-6)// case 1: replace all matches
[](#cb51-7)// escaping metacharacters using 'escapeRegExp' function
[](#cb51-8)> const pat = new RegExp(escapeRegExp(usr_str), 'g')
[](#cb51-9)> pat
[](#cb51-10)< /\(a\^b\)/g
[](#cb51-11)> eqn.replace(pat, 'c')
[](#cb51-12)< "f*c - 3*c"
[](#cb51-13)
[](#cb51-14)// case 2: replace only at the end of string
[](#cb51-15)> eqn.replace(new RegExp(escapeRegExp(usr_str) + '$'), 'c')
[](#cb51-16)"f*(a^b) - 3*c"
```

> ![info](media/file2.svg) Note that the `/` delimiter character isn't escaped in the above function. Use `[.*+\-?^${}()|[\]\\\/]` to escape the delimiter as well.

## Dynamically building alternation

Examples in previous chapter showed cases where a single regexp can contain multiple patterns combined using `|` metacharacter. Often, you have an array of strings and you need to match any of their content literally. To do so, you need to escape all the metacharacters before combining the strings with `|` metacharacter. The function shown below uses the `escapeRegExp` function introduced in the previous section.

```
[](#cb52-1)> function unionRegExp(arr) {
[](#cb52-2)    return arr.map(w => escapeRegExp(w)).join('|')
[](#cb52-3)  }
```

And here's some examples with `unionRegExp` function used to construct the required regexp.

```
[](#cb53-1)// here, order of alternation wouldn't matter
[](#cb53-2)// and assume that other regexp features aren't needed
[](#cb53-3)> let w1 = ['c^t', 'dog$', 'f|x']
[](#cb53-4)> const p1 = new RegExp(unionRegExp(w1), 'g')
[](#cb53-5)> p1
[](#cb53-6)< /c\^t|dog\$|f\|x/g
[](#cb53-7)> 'c^t dog$ bee parrot f|x'.replace(p1, 'mammal')
[](#cb53-8)< "mammal mammal bee parrot mammal"
[](#cb53-9)
[](#cb53-10)// here, alternation precedence rules needs to be applied first
[](#cb53-11)// and assume that the terms have to be matched as whole words
[](#cb53-12)> let w2 = ['hand', 'handy', 'handful']
[](#cb53-13)// sort by string length, longest first
[](#cb53-14)> w2.sort((a, b) => b.length - a.length)
[](#cb53-15)< ["handful", "handy", "hand"]
[](#cb53-16)> const p2 = new RegExp(`\\b(${unionRegExp(w2)})\\b`, 'g')
[](#cb53-17)> p2
[](#cb53-18)< /\b(handful|handy|hand)\b/g
[](#cb53-19)// note that 'hands' and 'handed' aren't replaced
[](#cb53-20)> 'handful handed handy hands hand'.replace(p2, 'X')
[](#cb53-21)< "X handed X hands X"
```

> ![info](media/file2.svg) The [XRegExp](https://github.com/slevithan/xregexp) utility provides [XRegExp.escape](http://xregexp.com/api/#escape) and [XRegExp.union](http://xregexp.com/api/#union) methods. The union method has additional functionality of allowing a mix of string and RegExp literals and also takes care of renumbering [backreferences](#ch011.xhtml_backreferences).

## source and flags properties

If you need the contents of a RegExp object, you can use `source` and `flags` properties to get the pattern string and flags respectively. These methods will help you to build a RegExp object using contents of another RegExp object.

```
[](#cb54-1)> const p3 = /\bpar\b/
[](#cb54-2)> const p4 = new RegExp(p3.source + '|cat', 'g')
[](#cb54-3)
[](#cb54-4)> p4
[](#cb54-5)< /\bpar\b|cat/g
[](#cb54-6)> console.log(p4.source)
[](#cb54-7)< \bpar\b|cat
[](#cb54-8)> p4.flags
[](#cb54-9)< "g"
[](#cb54-10)
[](#cb54-11)> 'cater cat concatenate par spare'.replace(p4, 'X')
[](#cb54-12)< "Xer X conXenate X spare"
```

## Escaping delimiter

Another character to keep track for escaping is the delimiter used to define the RegExp literal. Or depending upon the pattern, you can use the `new RegExp` constructor to avoid escaping.

```
[](#cb55-1)> let path = '/abc/123/foo/baz/ip.txt'
[](#cb55-2)
[](#cb55-3)// this is known as 'leaning toothpick syndrome'
[](#cb55-4)> path.replace(/^\/abc\/123\//, '~/')
[](#cb55-5)< "~/foo/baz/ip.txt"
[](#cb55-6)
[](#cb55-7)// using 'new RegExp' improves readability and can reduce typos
[](#cb55-8)> path.replace(new RegExp(`^/abc/123/`), '~/')
[](#cb55-9)< "~/foo/baz/ip.txt"
```

## Escape sequences

Certain characters like tab and newline can be expressed using escape sequences as `\t` and `\n` respectively. These are similar to how they are treated in normal string literals. However, `\b` is for word boundaries as seen earlier, whereas it stands for backspace character in normal string literals. Additionally, there are several sequences that are specific to regexps.

The full list is mentioned in the **Using special characters** section of [MDN documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions). These are `\b \B \cX \d \D \f \n \p \P \r \s \S \t \uhhhh \uhhhhh \v \w \W \xhh \0`.

```
[](#cb56-1)> 'a\tb\tc'.replace(/\t/g, ':')
[](#cb56-2)< "a:b:c"
[](#cb56-3)
[](#cb56-4)> '1\n2\n3'.replace(/\n/g, ' ')
[](#cb56-5)< "1 2 3"
[](#cb56-6)
[](#cb56-7)// use \\ instead of \ when constructing regexp from string literals
[](#cb56-8)> new RegExp('123\tabc')
[](#cb56-9)< /123    abc/
[](#cb56-10)> new RegExp('123\\tabc')
[](#cb56-11)< /123\tabc/
```

Here's a console screenshot of another example.

![Backslash in RegExp](media/file4.png)

If an escape sequence is not defined, it will be treated as the character it escapes.

```
[](#cb57-1)// here \e is treated as e
[](#cb57-2)> /\e/.test('hello')
[](#cb57-3)< true
```

You can also represent a character using hexadecimal escape of the format `\xhh` where `hh` are exactly two hexadecimal characters. If you represent a metacharacter using escapes, it will be treated literally instead of its metacharacter feature. [Codepoints](#ch014.xhtml_codepoints) section will discuss escapes for unicode characters.

```
[](#cb58-1)// \x20 is space character
[](#cb58-2)> 'h e l l o'.replace(/\x20/g, '')
[](#cb58-3)< "hello"
[](#cb58-4)
[](#cb58-5)// \x7c is '|' character
[](#cb58-6)> '12|30'.replace(/2\x7c3/g, '5')
[](#cb58-7)< "150"
[](#cb58-8)> '12|30'.replace(/2|3/g, '5')
[](#cb58-9)< "15|50"
```

> ![info](media/file2.svg) See [ASCII code table](https://ascii.cl/) for a handy cheatsheet with all the ASCII characters and their hexadecimal representation.

## Cheatsheet and Summary

| Note | Description |
| --- | --- |
| `\` | prefix metacharacters with `\` to match them literally |
| `\\` | to match `\` literally |
| `source` | property to convert RegExp object to string |
|  | helps to insert a RegExp inside another RegExp |
| `flags` | property to get flags of a RegExp object |
| ``RegExp(`pat`)`` | helps to avoid or reduce escaping the `/` delimiter character |
| Alternation precedence | tie-breaker is left to right if matches have same starting location |
|  | robust solution: sort the alternations based on length, longest first |

## Exercises

**a)** Transform given input strings to expected output using same logic on both strings.

```
[](#cb59-1)> let str1 = '(9-2)*5+qty/3'
[](#cb59-2)> let str2 = '(qty+4)/2-(9-2)*5+pq/4'
[](#cb59-3)
[](#cb59-4)> const pat1 =      // add your solution here
[](#cb59-5)> str1.replace()        // add your solution here
[](#cb59-6)< "35+qty/3"
[](#cb59-7)> str2.replace()        // add your solution here
[](#cb59-8)< "(qty+4)/2-35+pq/4"
```

**b)** Replace `(4)\|` with `2` only at the start or end of given input strings.

```
[](#cb60-1)> let s1 = '2.3/(4)\\|6 foo 5.3-(4)\\|'
[](#cb60-2)> let s2 = '(4)\\|42 - (4)\\|3'
[](#cb60-3)> let s3 = 'two - (4)\\|\n'
[](#cb60-4)
[](#cb60-5)> const pat2 =      // add your solution here
[](#cb60-6)
[](#cb60-7)> s1.replace()      // add your solution here
[](#cb60-8)< "2.3/(4)\|6 foo 5.3-2"
[](#cb60-9)> s2.replace()      // add your solution here
[](#cb60-10)< "242 - (4)\|3"
[](#cb60-11)> s3.replace()      // add your solution here
[](#cb60-12)< "two - (4)\|
[](#cb60-13)  "
```

**c)** Replace any matching item from given array with `X` for the given input strings.

```
[](#cb61-1)> let items = ['a.b', '3+n', 'x\\y\\z', 'qty||price', '{n}']
[](#cb61-2)
[](#cb61-3)// add your solution here
[](#cb61-4)> const pat3 =      // add your solution here
[](#cb61-5)
[](#cb61-6)> '0a.bcd'.replace(pat3, 'X')
[](#cb61-7)< "0Xcd"
[](#cb61-8)> 'E{n}AMPLE'.replace(pat3, 'X')
[](#cb61-9)< "EXAMPLE"
[](#cb61-10)> '43+n2 ax\\y\\ze'.replace(pat3, 'X')
[](#cb61-11)< "4X2 aXe"
```

**d)** Replace backspace character `\b` with a single space character for the given input string.

```
[](#cb62-1)> let ip = '123\b456'
[](#cb62-2)
[](#cb62-3)> ip.replace()      // add your solution here
[](#cb62-4)< "123 456"
```

**e)** Replace all occurrences of `\e` with `e`.

```
[](#cb63-1)> let ip = 'th\\er\\e ar\\e common asp\\ects among th\\e alt\\ernations'
[](#cb63-2)
[](#cb63-3)> ip.replace()      // add your solution here
[](#cb63-4)< "there are common aspects among the alternations"
```

**f)** Replace any matching item from the array `eqns` with `X` for given the string `ip`. Match the items from `eqns` literally.

```
[](#cb64-1)> let ip = '3-(a^b)+2*(a^b)-(a/b)+3'
[](#cb64-2)> let eqns = ['(a^b)', '(a/b)', '(a^b)+2']
[](#cb64-3)
[](#cb64-4)// add your solution here
[](#cb64-5)> const pat4 =      // add your solution here
[](#cb64-6)
[](#cb64-7)> ip.replace(pat4, 'X')
[](#cb64-8)< "3-X*X-X+3"
```

# Dot metacharacter and Quantifiers

This chapter introduces several more metacharacters. Similar to the `repeat` string method, quantifiers allow to repeat a portion of regular expression pattern and thus make it compact and improve readability. Quantifiers can also be specified as both bounded and unbounded ranges to match varying quantities of the pattern. Previously, alternation was used to construct OR conditional. Adding dot metacharacter and quantifiers to the mix, you can construct AND conditional.

## Dot metacharacter

The dot metacharacter serves as a placeholder to match *any* character except `\r`, `\n`, `\u2028` (line separator) and `\u2029` (paragraph separator) characters.

```
[](#cb65-1)// matches character 'c', any character and then character 't'
[](#cb65-2)> 'tac tin c.t abc;tuv acute'.replace(/c.t/g, 'X')
[](#cb65-3)< "taXin X abXuv aXe"
[](#cb65-4)
[](#cb65-5)// matches character 'r', any two characters and then character 'd'
[](#cb65-6)> 'breadth markedly reported overrides'.replace(/r..d/g, 'X')
[](#cb65-7)< "bXth maXly repoX oveXes"
[](#cb65-8)
[](#cb65-9)// matches character '2', any character and then character '3'
[](#cb65-10)> '42\t33'.replace(/2.3/, '8')
[](#cb65-11)< "483"
```

The [s flag](#ch007.xhtml_s-flag) section will show how to include line separators as well. Chapter [Character class](#ch010.xhtml_character-class) will discuss how to define your own custom placeholder for limited set of characters.

## split method

This chapter will additionally use `split` method to illustrate examples. The `split` method separates the string based on given regexp (or string) and returns an array of strings.

```
[](#cb66-1)> 'apple-85-mango-70'.split(/-/)
[](#cb66-2)< ["apple", "85", "mango", "70"]
[](#cb66-3)
[](#cb66-4)// use optional 'limit' argument to specify max no. of output elements
[](#cb66-5)> 'apple-85-mango-70'.split(/-/, 2)
[](#cb66-6)< ["apple", "85"]
[](#cb66-7)
[](#cb66-8)// example with dot metacharacter
[](#cb66-9)> 'bus:3:car:5:van'.split(/:.:/)
[](#cb66-10)< ["bus", "car", "van"]
```

See [split with capture groups](#ch009.xhtml_split-with-capture-groups) section for details of how capture groups affect the output of `split` method.

## Greedy quantifiers

Quantifiers helps you to repeat a portion of regexp. They can be applied to literal characters, groupings and other features that you'll learn later. Apart from ability to specify exact quantity and bounded range, these can also match unbounded varying quantities. If the input string can satisfy a pattern with varying quantities in multiple ways, you can choose among two types of quantifiers to narrow down the possibilities. In this section, **greedy** type of quantifiers is covered.

First up, the `?` metacharacter which quantifies a character or group to match `0` or `1` times. This helps to define optional patterns and build terser regexps.

```
[](#cb67-1)// same as: /ear|ar/g
[](#cb67-2)> 'far feat flare fear'.replace(/e?ar/g, 'X')
[](#cb67-3)< "fX feat flXe fX"
[](#cb67-4)
[](#cb67-5)// same as: /\bpar(t|)\b/g
[](#cb67-6)> 'par spare part party'.replace(/\bpart?\b/g, 'X')
[](#cb67-7)< "X spare X party"
[](#cb67-8)
[](#cb67-9)// same as: /\b(re.d|red)\b/
[](#cb67-10)> ['red', 'ready', 're;d', 'redo', 'reed'].filter(w => /\bre.?d\b/.test(w))
[](#cb67-11)< ["red", "re;d", "reed"]
[](#cb67-12)
[](#cb67-13)// same as: /part|parrot/g
[](#cb67-14)> 'par part parrot parent'.replace(/par(ro)?t/g, 'X')
[](#cb67-15)< "par X X parent"
[](#cb67-16)// same as: /part|parrot|parent/g
[](#cb67-17)> 'par part parrot parent'.replace(/par(en|ro)?t/g, 'X')
[](#cb67-18)< "par X X X"
```

The `*` metacharacter quantifies a character or group to match `0` or more times. There is no upper bound, more details will be discussed later in this chapter.

```
[](#cb68-1)// match 't' followed by zero or more of 'a' followed by 'r'
[](#cb68-2)> 'tr tear tare steer sitaara'.replace(/ta*r/g, 'X')
[](#cb68-3)< "X tear Xe steer siXa"
[](#cb68-4)
[](#cb68-5)// match 't' followed by zero or more of 'e' or 'a' followed by 'r'
[](#cb68-6)> 'tr tear tare steer sitaara'.replace(/t(e|a)*r/g, 'X')
[](#cb68-7)< "X X Xe sX siXa"
[](#cb68-8)
[](#cb68-9)// match zero or more of '1' followed by '2'
[](#cb68-10)> '3111111111125111142'.replace(/1*2/g, 'X')
[](#cb68-11)< "3X511114X"
```

Here's some more examples with `split` method.

```
[](#cb69-1)// last element is empty because there is nothing after '2' at the end of string
[](#cb69-2)> '3111111111125111142'.split(/1*2/)
[](#cb69-3)< ["3", "511114", ""]
[](#cb69-4)
[](#cb69-5)// note how '25' and '42' gets split, there is '1' zero times in between them
[](#cb69-6)> '3111111111125111142'.split(/1*/)
[](#cb69-7)< ["3", "2", "5", "4", "2"]
```

The `+` metacharacter quantifies a character or group to match `1` or more times. Similar to `*` quantifier, there is no upper bound. More importantly, this doesn't have surprises like matching empty string.

```
[](#cb70-1)> 'tr tear tare steer sitaara'.replace(/ta+r/g, 'X')
[](#cb70-2)< "tr tear Xe steer siXa"
[](#cb70-3)> 'tr tear tare steer sitaara'.replace(/t(e|a)+r/g, 'X')
[](#cb70-4)< "tr X Xe sX siXa"
[](#cb70-5)
[](#cb70-6)> '3111111111125111142'.replace(/1+2/g, 'X')
[](#cb70-7)< "3X5111142"
[](#cb70-8)> '3111111111125111142'.split(/1+/)
[](#cb70-9)< ["3", "25", "42"]
```

You can specify a range of integer numbers, both bounded and unbounded, using `{}` metacharacters. There are three ways to use this quantifier as listed below.

| Pattern | Description |
| --- | --- |
| `{m,n}` | match `m` to `n` times |
| `{m,}` | match at least `m` times |
| `{n}` | match exactly `n` times |

```
[](#cb71-1)> let demo = ['abc', 'ac', 'abbc', 'xabbbcz', 'bc', 'abbbbbc']
[](#cb71-2)
[](#cb71-3)> demo.filter(w => /ab{1,4}c/.test(w))
[](#cb71-4)< ["abc", "abbc", "xabbbcz"]
[](#cb71-5)> demo.filter(w => /ab{0,2}c/.test(w))
[](#cb71-6)< ["abc", "ac", "abbc"]
[](#cb71-7)
[](#cb71-8)> demo.filter(w => /ab{3,}c/.test(w))
[](#cb71-9)< ["xabbbcz", "abbbbbc"]
[](#cb71-10)
[](#cb71-11)> demo.filter(w => /ab{3}c/.test(w))
[](#cb71-12)< ["xabbbcz"]
```

> ![info](media/file2.svg) The `{}` metacharacters have to be escaped to match them literally. However, unlike `()` metacharacters, these have lot more leeway. For example, escaping `{` alone is enough, or if it doesn't conform strictly to any of the forms listed above, escaping is not needed at all.

## AND Conditional

Next up, how to construct AND conditional using dot metacharacter and quantifiers.

```
[](#cb72-1)// match 'Error' followed by zero or more characters followed by 'valid'
[](#cb72-2)> /Error.*valid/.test('Error: not a valid input')
[](#cb72-3)< true
[](#cb72-4)
[](#cb72-5)> /Error.*valid/.test('Error: key not found')
[](#cb72-6)< false
```

To allow matching in any order, you'll have to bring in alternation as well. That is somewhat manageable for 2 or 3 patterns. See [AND conditional with lookarounds](#ch013.xhtml_and-conditional-with-lookarounds) section for an easier approach.

```
[](#cb73-1)> /cat.*dog|dog.*cat/.test('cat and dog')
[](#cb73-2)< true
[](#cb73-3)> /cat.*dog|dog.*cat/.test('dog and cat')
[](#cb73-4)< true
[](#cb73-5)
[](#cb73-6)// if you just need true/false result, this would be a scalable approach
[](#cb73-7)> let patterns = [/cat/, /dog/]
[](#cb73-8)> patterns.every(p => p.test('cat and dog'))
[](#cb73-9)< true
[](#cb73-10)> patterns.every(p => p.test('dog and cat'))
[](#cb73-11)< true
```

## What does greedy mean?

When you are using `?` how does JavaScript decide to match `0` or `1` times, if both quantities can satisfy the regexp? For example, consider `'foot'.replace(/f.?o/, 'X')` — should `foo` be replaced or `fo`? It will always replace `foo`, because these are **greedy** quantifiers, meaning they try to match as much as possible.

```
[](#cb74-1)> 'foot'.replace(/f.?o/, 'X')
[](#cb74-2)< "Xt"
[](#cb74-3)
[](#cb74-4)// a more practical example
[](#cb74-5)// prefix '<' with '\' if it is not already prefixed
[](#cb74-6)> console.log('blah < foo \\< bar < baz'.replace(/\\?</g, '\\<'))
[](#cb74-7)< blah \< foo \< bar \< baz
[](#cb74-8)
[](#cb74-9)// say goodbye to /handful|handy|hand/ shenanigans
[](#cb74-10)> 'hand handy handful'.replace(/hand(y|ful)?/g, 'X')
[](#cb74-11)< "X X X"
```

But wait, how did the `/Error.*valid/` example work? Shouldn't `.*` consume all the characters after `Error`? Good question. The regexp engine actually does consume all the characters. Then realizing that the regexp fails, it gives back one character from end of string and checks again if regexp is satisfied. This process is repeated until a match is found or failure is confirmed. In regular expression parlance, this is called **backtracking**.

```
[](#cb75-1)> let sentence = 'that is quite a fabricated tale'
[](#cb75-2)
[](#cb75-3)// t.*a will always match from first 't' to last 'a'
[](#cb75-4)> sentence.replace(/t.*a/, 'X')
[](#cb75-5)< "Xle"
[](#cb75-6)> 'star'.replace(/t.*a/, 'X')
[](#cb75-7)< "sXr"
[](#cb75-8)
[](#cb75-9)// matching first 't' to last 'a' for t.*a won't work for these cases
[](#cb75-10)// the regexp engine backtracks until .*q matches and so on
[](#cb75-11)> sentence.replace(/t.*a.*q.*f/, 'X')
[](#cb75-12)< "Xabricated tale"
[](#cb75-13)> sentence.replace(/t.*a.*u/, 'X')
[](#cb75-14)< "Xite a fabricated tale"
```

> ![warning](media/file3.svg) Backtracking can be quite time consuming for certain corner cases. Or even catastrophic (see [cloudflare: Details of the Cloudflare outage on July 2, 2019](https://blog.cloudflare.com/details-of-the-cloudflare-outage-on-july-2-2019/)).

## Non-greedy quantifiers

As the name implies, these quantifiers will try to match as minimally as possible. Also known as **lazy** or **reluctant** quantifiers. Appending a `?` to greedy quantifiers makes them non-greedy.

```
[](#cb76-1)> 'foot'.replace(/f.??o/, 'X')
[](#cb76-2)< "Xot"
[](#cb76-3)
[](#cb76-4)> 'frost'.replace(/f.??o/, 'X')
[](#cb76-5)< "Xst"
[](#cb76-6)
[](#cb76-7)> '123456789'.replace(/.{2,5}?/, 'X')
[](#cb76-8)< "X3456789"
[](#cb76-9)
[](#cb76-10)> 'green:3.14:teal::brown:oh!:blue'.split(/:.*?:/)
[](#cb76-11)< ["green", "teal", "brown", "blue"]
```

Like greedy quantifiers, lazy quantifiers will try to satisfy the overall regexp.

```
[](#cb77-1)> let sentence = 'that is quite a fabricated tale'
[](#cb77-2)
[](#cb77-3)// t.*?a will always match from first 't' to first 'a'
[](#cb77-4)> sentence.replace(/t.*?a/, 'X')
[](#cb77-5)< "Xt is quite a fabricated tale"
[](#cb77-6)> 'star'.replace(/t.*?a/, 'X')
[](#cb77-7)< "sXr"
[](#cb77-8)
[](#cb77-9)// matching first 't' to first 'a' for t.*?a won't work for this case
[](#cb77-10)// so, regexp engine will move forward until .*?f matches and so on
[](#cb77-11)> sentence.replace(/t.*?a.*?f/, 'X')
[](#cb77-12)< "Xabricated tale"
```

## s flag

Use `s` flag to allow `.` metacharacter to match `\r`, `\n` and line/paragraph separator characters as well.

```
[](#cb78-1)// by default, the . metacharacter doesn't match line separators
[](#cb78-2)> 'Hi there\nHave a Nice Day'.replace(/the.*ice/, 'X')
[](#cb78-3)< "Hi there
[](#cb78-4)  Have a Nice Day"
[](#cb78-5)
[](#cb78-6)// 's' flag will allow line separators to be matched as well
[](#cb78-7)> 'Hi there\nHave a Nice Day'.replace(/the.*ice/s, 'X')
[](#cb78-8)< "Hi X Day"
```

## Cheatsheet and Summary

| Note | Description |
| --- | --- |
| `.` | match any character except line separators |
| `s` | flag to match line separators as well with `.` metacharacter |
| greedy | match as much as possible |
| `?` | greedy quantifier, match `0` or `1` times |
| `*` | greedy quantifier, match `0` or more times |
| `+` | greedy quantifier, match `1` or more times |
| `{m,n}` | greedy quantifier, match `m` to `n` times |
| `{m,}` | greedy quantifier, match at least `m` times |
| `{n}` | greedy quantifier, match exactly `n` times |
| `pat1.*pat2` | any number of characters between `pat1` and `pat2` |
| `pat1.*pat2&#124;pat2.*pat1` | match both `pat1` and `pat2` in any order |
| non-greedy | append `?` to greedy quantifier |
|  | match as minimally as possible |
| `s.split(/pat/)` | split a string based on regexp |

This chapter introduced the concept of specifying a placeholder instead of fixed string. When combined with quantifiers, you've seen a glimpse of how a simple regexp can match wide range of text. In coming chapters, you'll learn how to create your own restricted set of placeholder characters.

## Exercises

> ![info](media/file2.svg) Use `s` flag for these exercises depending upon the contents of input strings.

**a)** Replace `42//5` or `42/5` with `8` for the given input.

```
[](#cb79-1)> let ip = 'a+42//5-c pressure*3+42/5-14256'
[](#cb79-2)
[](#cb79-3)// add your solution here
[](#cb79-4)< "a+8-c pressure*3+8-14256"
```

**b)** For the array `items`, filter all elements starting with `hand` and ending with at most one more character or `le`.

```
[](#cb80-1)> let items = ['handed', 'hand', 'handled', 'handy', 'unhand', 'hands', 'handle']
[](#cb80-2)
[](#cb80-3)// add your solution here
[](#cb80-4)< ["hand", "handy", "hands", "handle"]
```

**c)** Use `split` method to get the output as shown for the given input strings.

```
[](#cb81-1)> let eqn1 = 'a+42//5-c'
[](#cb81-2)> let eqn2 = 'pressure*3+42/5-14256'
[](#cb81-3)> let eqn3 = 'r*42-5/3+42///5-42/53+a'
[](#cb81-4)
[](#cb81-5)> const pat1 =      // add your solution here
[](#cb81-6)
[](#cb81-7)> eqn1.split(pat1)
[](#cb81-8)< ["a+", "-c"]
[](#cb81-9)> eqn2.split(pat1)
[](#cb81-10)< ["pressure*3+", "-14256"]
[](#cb81-11)> eqn3.split(pat1)
[](#cb81-12)< ["r*42-5/3+42///5-", "3+a"]
```

**d)** For the given input strings, remove everything from the first occurrence of `i` till end of the string.

```
[](#cb82-1)> let s1 = 'remove the special meaning of such constructs'
[](#cb82-2)> let s2 = 'characters while constructing'
[](#cb82-3)
[](#cb82-4)> const pat2 =      // add your solution here
[](#cb82-5)
[](#cb82-6)> s1.replace(pat2, '')
[](#cb82-7)< "remove the spec"
[](#cb82-8)> s2.replace(pat2, '')
[](#cb82-9)< "characters wh"
```

**e)** For the given strings, construct a regexp to get output as shown.

```
[](#cb83-1)> let str1 = 'a+b(addition)'
[](#cb83-2)> let str2 = 'a/b(division) + c%d(#modulo)'
[](#cb83-3)> let str3 = 'Hi there(greeting). Nice day(a(b)'
[](#cb83-4)
[](#cb83-5)> const remove_parentheses =        // add your solution here
[](#cb83-6)
[](#cb83-7)> str1.replace(remove_parentheses, '')
[](#cb83-8)< "a+b"
[](#cb83-9)> str2.replace(remove_parentheses, '')
[](#cb83-10)< "a/b + c%d"
[](#cb83-11)> str3.replace(remove_parentheses, '')
[](#cb83-12)< "Hi there. Nice day"
```

**f)** Correct the given regexp to get the expected output.

```
[](#cb84-1)> let words = 'plink incoming tint winter in caution sentient'
[](#cb84-2)
[](#cb84-3)// wrong output
[](#cb84-4)> const w1 = /int|in|ion|ing|inco|inter|ink/g
[](#cb84-5)> words.replace(w1, 'X')
[](#cb84-6)"plXk XcomXg tX wXer X cautX sentient"
[](#cb84-7)
[](#cb84-8)// expected output
[](#cb84-9)> const w2 =        // add your solution here
[](#cb84-10)> words.replace(w2, 'X')
[](#cb84-11)"plX XmX tX wX X cautX sentient"
```

**g)** For the given greedy quantifiers, what would be the equivalent form using `{m,n}` representation?

*   `?` is same as
*   `*` is same as
*   `+` is same as

**h)** `(a*|b*)` is same as `(a|b)*` — true or false?

**i)** For the given input strings, remove everything from the first occurrence of `test` (irrespective of case) till end of the string, provided `test` isn't at the end of the string.

```
[](#cb85-1)> let s1 = 'this is a Test'
[](#cb85-2)> let s2 = 'always test your regexp for corner\ncases'
[](#cb85-3)> let s3 = 'a TEST of skill tests?'
[](#cb85-4)
[](#cb85-5)> let pat3 =        // add your solution here
[](#cb85-6)
[](#cb85-7)> s1.replace(pat3, '')
[](#cb85-8)< "this is a Test"
[](#cb85-9)> s2.replace(pat3, '')
[](#cb85-10)< "always "
[](#cb85-11)> s3.replace(pat3, '')
[](#cb85-12)< "a "
```

**j)** For the input array `words`, filter all elements starting with `s` and containing `e` and `t` in any order.

```
[](#cb86-1)> let words = ['sequoia', 'subtle', 'exhibit', 'asset', 'sets', 'tests', 'site']
[](#cb86-2)
[](#cb86-3)// add your solution here
[](#cb86-4)< ["subtle", "sets", "site"]
```

**k)** For the input array `words`, remove all elements having less than `6` characters.

```
[](#cb87-1)> let words = ['sequoia', 'subtle', 'exhibit', 'asset', 'sets', 'tests', 'site']
[](#cb87-2)
[](#cb87-3)// add your solution here
[](#cb87-4)< ["sequoia", "subtle", "exhibit"]
```

**l)** For the input array `words`, filter all elements starting with `s` or `t` and having a maximum of `6` characters.

```
[](#cb88-1)> let words = ['sequoia', 'subtle', 'exhibit', 'asset', 'sets', 'tests', 'site']
[](#cb88-2)
[](#cb88-3)// add your solution here
[](#cb88-4)< ["subtle", "sets", "tests", "site"]
```

**m)** Delete from the string `start` if it is at beginning of a line up to the next occurrence of the string `end` at end of a line. Match these keywords irrespective of case.

```
[](#cb89-1)> let para = `good start
[](#cb89-2)start working on that
[](#cb89-3)project you always wanted
[](#cb89-4)to, do not let it end
[](#cb89-5)hi there
[](#cb89-6)start and end the end
[](#cb89-7)42
[](#cb89-8)Start and try to
[](#cb89-9)finish the End
[](#cb89-10)bye`
[](#cb89-11)
[](#cb89-12)> const pat3 =      // add your solution here
[](#cb89-13)> console.log(para.replace(pat3, ''))
[](#cb89-14)< good start
[](#cb89-15) 
[](#cb89-16)  hi there
[](#cb89-17) 
[](#cb89-18)  42
[](#cb89-19) 
[](#cb89-20)  bye
```

**n)** Can you reason out why this code results in the output shown? The aim was to remove all `<characters>` patterns but not the `<>` ones. The expected result was `'a 1<> b 2<> c'`.

```
[](#cb90-1)> let ip = 'a<apple> 1<> b<bye> 2<> c<cat>'
[](#cb90-2)
[](#cb90-3)> ip.replace(/<.+?>/g, '')
[](#cb90-4)< "a 1 2"
```

**o)** Use `split` method to get the output as shown below for given input strings.

```
[](#cb91-1)> let s1 = 'go there  ::   this :: that'
[](#cb91-2)> let s2 = 'a::b :: c::d e::f :: 4::5'
[](#cb91-3)> let s3 = '42:: hi::bye::see :: carefully'
[](#cb91-4)
[](#cb91-5)> const pat4 =      // add your solution here
[](#cb91-6)
[](#cb91-7)> s1.split()        // add your solution here
[](#cb91-8)< ["go there", "this :: that"]
[](#cb91-9)> s2.split()        // add your solution here
[](#cb91-10)< ["a::b", "c::d e::f :: 4::5"]
[](#cb91-11)> s3.split()        // add your solution here
[](#cb91-12)< ["42:: hi::bye::see", "carefully"]
```

# Interlude: Tools for debugging and visualization

As your regexp gets complicated, it can get difficult to debug if you run into issues. Building your regexp step by step from scratch and testing against input strings will go a long way in correcting the problem. To aid in such a process, you could use [various online regexp tools](https://news.ycombinator.com/item?id=20614847).

## regex101

[regex101](https://regex101.com/) is a popular site to test your regexp. You'll have first choose the flavor as JavaScript. Then you can add your regexp, input strings, choose flags and an optional replacement string. Matching portions will be highlighted and explanation is offered in separate panes. There's also a quick reference and other features like sharing, code generator, quiz, etc.

The below image is a screenshot from this link — [regex101: `/ab{0,2}c/g`](https://regex101.com/r/HSeO0z/1)

![regex101 example](media/file5.png)

> ![info](media/file2.svg) [regexr](https://regexr.com/) is another site that offers similar functionality.

## regulex

Another useful tool is [jex: regulex](https://jex.im/regulex/) which converts your regexp to a rail road diagram, thus providing a visual aid to understanding the pattern.

The below image is a screenshot from this link — [regulex: `/\bpar(en|ro)?t\b/`](https://jex.im/regulex/#!flags=&re=%5Cbpar(en%7Cro)%3Ft%5Cb)

![regulex example](media/file6.png)

> ![info](media/file2.svg) [debuggex](https://www.debuggex.com/) is another site that offers similar functionality.

## regexcrossword

For practice, [regexcrossword](https://regexcrossword.com/) is often recommended. This site supports only JavaScript flavor. See [regexcrossword: howtoplay](https://regexcrossword.com/howtoplay) for help.

The below image is a screenshot from this link — [regexcrossword: tutorial puzzle 5](https://regexcrossword.com/challenges/tutorial/puzzles/5)

![regexcrossword example](media/file7.png)

## Summary

This chapter briefly presented three online tools that can help you with understanding and interactively solving/debugging regular expressions. Syntax and features can vary, sometimes significantly, between various tools and programming languages. So, ensure that the program you are using supports the flavor of regular expressions you are using.

# Working with matched portions

Having seen a few regexp features that can match varying text, you'll learn how to extract and work with those matching portions in this chapter. Three new methods are introduced. You'll also learn a few tricks like using functions and dictionaries in replacement section of `replace` method.

## match method

The `match` method can be used in different ways. When `g` flag isn't used and the regexp succeeds, you get an array object containing various details of the first matching portion.

```
[](#cb92-1)// note that 'g' flag isn't used
[](#cb92-2)> 'abc ac adc abbbc'.match(/ab*c/)
[](#cb92-3)< ["abc", index: 0, input: "abc ac adc abbbc", groups: undefined]
[](#cb92-4)
[](#cb92-5)// to get only the matching portion
[](#cb92-6)> 'abc ac adc abbbc'.match(/ab*c/)[0]
[](#cb92-7)< "abc"
[](#cb92-8)
[](#cb92-9)// non-regexp object will get processed as: RegExp(object)
[](#cb92-10)> 'abc ac adc abbbc'.match('ab*c')
[](#cb92-11)< ["abc", index: 0, input: "abc ac adc abbbc", groups: undefined]
```

The `index` property gives the starting location of matched portion. The `input` property gives the input string on which the `match` method was used. If the given regexp fails, the output is `null` and not an empty array. The `groups` property will be discussed in [Named capture groups](#ch011.xhtml_named-capture-groups) section. See [MDN: match](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match) for more details and examples.

```
[](#cb93-1)> let s1 = 'cat and dog'
[](#cb93-2)
[](#cb93-3)> s1.match(/dog/).index
[](#cb93-4)< 8
[](#cb93-5)> s1.match(/dog/).input
[](#cb93-6)< "cat and dog"
[](#cb93-7)
[](#cb93-8)> s1.match(/xyz/)
[](#cb93-9)< null
```

## search method

The `search` method gives the index of first matching portion. If the regexp fails, it returns `-1` as output.

```
[](#cb94-1)// same as: match(/dog/).index
[](#cb94-2)> 'cat and dog'.search(/dog/)
[](#cb94-3)< 8
[](#cb94-4)// cannot use match(/xyz/).index here
[](#cb94-5)// as 'match' returns 'null' if regexp doesn't match
[](#cb94-6)> 'cat and dog'.search(/xyz/)
[](#cb94-7)< -1
```

## Capture groups

The regexp grouping inside `()` is also known as a **capture group**. It has multiple uses, one of which is the ability to work with matched portions of those groups. When capture groups are used with `match` method, the matched portions of those groups will also be part of the array output. The first element is always the entire matched portion followed by portions of capture groups. The leftmost `(` will get group number `1`, second leftmost `(` will get group number `2` and so on.

```
[](#cb95-1)// there are two capture groups used here
[](#cb95-2)> 'abc ac adc abbbc'.match(/a(.*)d(.*a)/)
[](#cb95-3)< ["abc ac adc a", "bc ac a", "c a", index: 0,
[](#cb95-4)   input: "abc ac adc abbbc", groups: undefined]
[](#cb95-5)
[](#cb95-6)// entire matched portion
[](#cb95-7)> 'abc ac adc abbbc'.match(/a(.*)d(.*a)/)[0]
[](#cb95-8)< "abc ac adc a"
[](#cb95-9)
[](#cb95-10)// capture group portions
[](#cb95-11)> 'abc ac adc abbbc'.match(/a(.*)d(.*a)/)[1]
[](#cb95-12)< "bc ac a"
[](#cb95-13)> 'abc ac adc abbbc'.match(/a(.*)d(.*a)/)[2]
[](#cb95-14)< "c a"
```

## Getting all matched portions

The `match` method returns all the matched portions when the `g` flag is used. Capture group portions and the three properties won't be part of the output.

```
[](#cb96-1)> 'abc ac adc abbbc'.match(/ab*c/g)
[](#cb96-2)< ["abc", "ac", "abbbc"]
[](#cb96-3)
[](#cb96-4)> 'abc ac adc abbbc'.match(/ab+c/g)
[](#cb96-5)< ["abc", "abbbc"]
[](#cb96-6)
[](#cb96-7)> 'par spar apparent spare part'.match(/\bs?pare?\b/g)
[](#cb96-8)< ["par", "spar", "spare"]
[](#cb96-9)
[](#cb96-10)// entire matching portion is returned even if capture group is used
[](#cb96-11)> 'par spar apparent spare part'.match(/\bs?par(e|t)\b/g)
[](#cb96-12)< ["spare", "part"]
```

It is a useful method for debugging purposes as well, for example to see what is going on under the hood before using `replace` method.

```
[](#cb97-1)> 'that is quite a fabricated tale'.match(/t.*a/g)
[](#cb97-2)< ["that is quite a fabricated ta"]
[](#cb97-3)> 'that is quite a fabricated tale'.match(/t.*?a/g)
[](#cb97-4)< ["tha", "t is quite a", "ted ta"]
```

## matchAll method

If you need capture group portions and properties for every match with `g` flag active, use the `matchAll` method. The return value is an iterator.

```
[](#cb98-1)> 'abc ac adc abbbc'.matchAll(/ab*c/g)
[](#cb98-2)< RegExpStringIterator {}
[](#cb98-3)
[](#cb98-4)// convert the iterator result to array of arrays
[](#cb98-5)> let arr = [...'abc ac adc abbbc'.matchAll(/ab*c/g)]
[](#cb98-6)> arr
[](#cb98-7)< (3) [Array(1), Array(1), Array(1)]
[](#cb98-8)  0: ["abc", index: 0, input: "abc ac adc abbbc", groups: undefined]
[](#cb98-9)  1: ["ac", index: 4, input: "abc ac adc abbbc", groups: undefined]
[](#cb98-10)  2: ["abbbc", index: 11, input: "abc ac adc abbbc", groups: undefined]
[](#cb98-11)  length: 3
[](#cb98-12)  __proto__: Array(0)
[](#cb98-13)
[](#cb98-14)// get array with details for first match
[](#cb98-15)> arr[0]
[](#cb98-16)< ["abc", index: 0, input: "abc ac adc abbbc", groups: undefined]
[](#cb98-17)// get index for second match
[](#cb98-18)> arr[1].index
[](#cb98-19)< 4
```

You can also use [Array.from()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from) to convert the iterator to array object. `Array.from` allows you to provide a mapping function as second argument.

```
[](#cb99-1)// same as: match(/ab*c/g)
[](#cb99-2)> Array.from('abc ac adc abbbc'.matchAll(/ab*c/g), m => m[0])
[](#cb99-3)< ["abc", "ac", "abbbc"]
[](#cb99-4)// get index for each match
[](#cb99-5)> Array.from('abc ac adc abbbc'.matchAll(/ab*c/g), m => m.index)
[](#cb99-6)< [0, 4, 11]
[](#cb99-7)
[](#cb99-8)// get only capture group portions as an array for each match
[](#cb99-9)> Array.from('xx:yyy x: x:yy :y'.matchAll(/(x*):(y*)/g), m => m.slice(1))
[](#cb99-10)< (4) [Array(2), Array(2), Array(2), Array(2)]
[](#cb99-11)  0: (2) ["xx", "yyy"]
[](#cb99-12)  1: (2) ["x", ""]
[](#cb99-13)  2: (2) ["x", "yy"]
[](#cb99-14)  3: (2) ["", "y"]
[](#cb99-15)  length: 4
[](#cb99-16)  __proto__: Array(0)
```

> ![info](media/file2.svg) Before the introduction of `matchAll` method, `exec` method had to be used. See [MDN: exec](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec) details and examples.

## split with capture groups

Capture groups affects `split` method as well. If the pattern used to split contains capture groups, the portions matched by those groups will also be a part of the output array.

```
[](#cb100-1)// without capture group
[](#cb100-2)> '31111111111251111426'.split(/1*4?2/)
[](#cb100-3)< ["3", "5", "6"]
[](#cb100-4)
[](#cb100-5)// to include the matching portions of the pattern as well in the output
[](#cb100-6)> '31111111111251111426'.split(/(1*4?2)/)
[](#cb100-7)< ["3", "11111111112", "5", "111142", "6"]
```

If part of the pattern is outside a capture group, the text thus matched won't be in the output. If a capture group didn't participate, it will be represented by `undefined` in the output array.

```
[](#cb101-1)// here 4?2 is outside capture group, so that portion won't be in output
[](#cb101-2)> '31111111111251111426'.split(/(1*)4?2/)
[](#cb101-3)< ["3", "1111111111", "5", "1111", "6"]
[](#cb101-4)
[](#cb101-5)// multiple capture groups example
[](#cb101-6)// note that the portion matched by b+ isn't present in the output
[](#cb101-7)> '3.14aabccc42'.split(/(a+)b+(c+)/)
[](#cb101-8)< ["3.14", "aa", "ccc", "42"]
[](#cb101-9)
[](#cb101-10)// here (4)? matches zero times on the first occasion
[](#cb101-11)> '31111111111251111426'.split(/(1*)(4)?2/)
[](#cb101-12)< ["3", "1111111111", undefined, "5", "1111", "4", "6"]
```

Use of capture groups and optional `limit` argument can help you partition an input string into three parts:

*   portion before the first match
*   portion matched by the pattern itself
*   portion after the pattern

```
[](#cb102-1)// use 's' flag as well if needed
[](#cb102-2)> '3.14aabccc42abc88'.split(/(a+b+c+)(.*)/, 3)
[](#cb102-3)< ["3.14", "aabccc", "42abc88"]
```

## Using function in replacement section

Sometimes, simple replacement string isn't enough and you need to do some processing on the matched portion. For such cases, you can use function in the replacement section. The arguments available to the function are similar to the details provided by `match` method. The first one is entire matched portion. If capture groups are used, portions matched by those groups will be next. Then comes index of matched portion and finally the input string. Depending on the complexity, you can use fully defined function or arrow function expressions.

```
[](#cb103-1)> function titleCase(m) {
[](#cb103-2)      return m[0].toUpperCase() + m.substr(1).toLowerCase()
[](#cb103-3)  }
[](#cb103-4)
[](#cb103-5)// only function name is enough as second argument
[](#cb103-6)// the matched portion details will be passed automatically to the function
[](#cb103-7)// in this example, 'titleCase' is using only the entire matched portion
[](#cb103-8)> 'aBc ac ADC aBbBC'.replace(/a.*?c/ig, titleCase)
[](#cb103-9)< "Abc Ac Adc Abbbc"
[](#cb103-10)
[](#cb103-11)// can also use arrow function expressions for simple cases
[](#cb103-12)> 'abc ac adc abbbc'.replace(/ab*c/g, m => m.toUpperCase())
[](#cb103-13)< "ABC AC adc ABBBC"
[](#cb103-14)
[](#cb103-15)// \d will be covered later
[](#cb103-16)// for now, it is enough to know that it will match all digit characters
[](#cb103-17)> '1 42 317'.replace(/\d+/g, m => m*2)
[](#cb103-18)< "2 84 634"
```

Here's an example with capture groups. See also [MDN: replace](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/replace) for more details.

```
[](#cb104-1)> function titleCase(m, g1, g2) {
[](#cb104-2)        return g1.toUpperCase() + g2.toLowerCase()
[](#cb104-3)  }
[](#cb104-4)> 'aBc ac ADC aBbBC'.replace(/(a)(.*?c)/ig, titleCase)
[](#cb104-5)< "Abc Ac Adc Abbbc"
```

## Using dictionary in replacement section

Sometimes, the functionality you need in replacement section can be simplified to using a dictionary. The matched portion acts as the key to get corresponding value from the dictionary.

```
[](#cb105-1)// one to one mappings
[](#cb105-2)> let h = { '1': 'one', '2': 'two', '4': 'four' }
[](#cb105-3)
[](#cb105-4)> '9234012'.replace(/1|2|4/g, k => h[k])
[](#cb105-5)< "9two3four0onetwo"
[](#cb105-6)
[](#cb105-7)// providing a default value if the matched text doesn't exist as a key
[](#cb105-8)> '9234012'.replace(/\d/g, k => k in h ? h[k] : 'X')
[](#cb105-9)< "XtwoXfourXonetwo"
```

For swapping two or more strings without using intermediate result, using a dictionary is recommended.

```
[](#cb106-1)> let swap = { 'cat': 'tiger', 'tiger': 'cat' }
[](#cb106-2)
[](#cb106-3)> 'cat tiger dog tiger cat'.replace(/cat|tiger/g, k => swap[k])
[](#cb106-4)< "tiger cat dog cat tiger"
```

For a dictionary that has many entries and likely to undergo changes during development, building alternation list manually is not a good choice. Also, recall that as per precedence rules, longest length string should come first. The `unionRegExp` function, introduced in [Dynamically building alternation](#ch006.xhtml_dynamically-building-alternation) section, is helpful here.

```
[](#cb107-1)> let d = { 'hand': 1, 'handy': 2, 'handful': 3, 'a^b': 4 }
[](#cb107-2)
[](#cb107-3)> const p = unionRegExp(Object.keys(d).sort((a, b) => b.length - a.length))
[](#cb107-4)> console.log(p)
[](#cb107-5)< handful|handy|hand|a\^b
[](#cb107-6)> 'handful hand pin handy (a^b)'.replace(new RegExp(p, 'g'), k => d[k])
[](#cb107-7)< "3 1 pin 2 (4)"
```

## Cheatsheet and Summary

| Note | Description |
| --- | --- |
| `m = s.match(/pat/)` | assuming `g` flag isn't used and regexp succeeds, |
|  | returns an array with matched portion and 3 properties |
|  | `index` property gives the starting location of the match |
|  | `input` property gives the input string `s` |
|  | `groups` property gives dictionary of [named capture groups](#ch011.xhtml_named-capture-groups) |
| `m[0]` | for above case, gives entire matched portion |
| `m[1]` | matched portion of first capture group |
| `m[2]` | matched portion of second capture group and so on |
| `s.match(/pat/g)` | returns only the matched portions, no properties |
|  | capture group doesn't affect the output |
|  | `match` returns `null` if regexp fails |
| `s.matchAll(/pat/g)` | returns an iterator containing details for |
|  | each matched portion and its properties |
|  | use `[...]` or `Array.from` to convert to array |
|  | `Array.from` also allows mapping function |
| `s.replace(/pat/, func)` | you can use a function to provide replacement string |
|  | each matched portion details gets passed as arguments |
|  | similarly, dictionary can be used for replacement |
| `s.search(/pat/)` | gives starting location of first match if regexp succeeds |
|  | `-1` if regexp fails |

This chapter introduced `match` and `matchAll` methods, which allows you to work with various matching portions of input string. The `search` method is handy if you just need the starting location of the first match. The `replace` method allows you to use a function as replacement, which helps to process the matching portions before being used as replacement string. You can also use a dictionary to provide replacement string based on matched portion as key. You learnt about capture groups and you'll see even more uses of groupings in coming chapters.

## Exercises

**a)** For the given strings, extract the matching portion from first `is` to last `t`

```
[](#cb108-1)> let str1 = 'What is the biggest fruit you have seen?'
[](#cb108-2)> let str2 = 'Your mission is to read and practice consistently'
[](#cb108-3)
[](#cb108-4)> const pat1 =      // add your solution here
[](#cb108-5)
[](#cb108-6)// add your solution here for str1
[](#cb108-7)< "is the biggest fruit"
[](#cb108-8)// add your solution here for str2
[](#cb108-9)< "ission is to read and practice consistent"
```

**b)** Find the starting index of first occurrence of `is` or `the` or `was` or `to` for the given input strings. Assume that there will be at least one match for each input string.

```
[](#cb109-1)> let s1 = 'match after the last newline character'
[](#cb109-2)> let s2 = 'and then you want to test'
[](#cb109-3)> let s3 = 'this is good bye then'
[](#cb109-4)> let s4 = 'who was there to see?'
[](#cb109-5)
[](#cb109-6)> const pat2 =      // add your solution here
[](#cb109-7)
[](#cb109-8)// add your solution here for s1
[](#cb109-9)< 12
[](#cb109-10)// add your solution here for s2
[](#cb109-11)< 4
[](#cb109-12)// add your solution here for s3
[](#cb109-13)< 2
[](#cb109-14)// add your solution here for s4
[](#cb109-15)< 4
```

**c)** Find the starting index of last occurrence of `is` or `the` or `was` or `to` for the given input strings. Assume that there will be at least one match for each input string.

```
[](#cb110-1)> let s1 = 'match after the last newline character'
[](#cb110-2)> let s2 = 'and then you want to test'
[](#cb110-3)> let s3 = 'this is good bye then'
[](#cb110-4)> let s4 = 'who was there to see?'
[](#cb110-5)
[](#cb110-6)> const pat3 =      // add your solution here
[](#cb110-7)
[](#cb110-8)// add your solution here for s1
[](#cb110-9)< 12
[](#cb110-10)// add your solution here for s2
[](#cb110-11)< 18
[](#cb110-12)// add your solution here for s3
[](#cb110-13)< 17
[](#cb110-14)// add your solution here for s4
[](#cb110-15)< 14
```

**d)** The given input string contains `:` exactly once. Extract all characters after the `:` as output.

```
[](#cb111-1)> let ip = 'fruits:apple, mango, guava, blueberry'
[](#cb111-2)
[](#cb111-3)// add your solution here
[](#cb111-4)< "apple, mango, guava, blueberry"
```

**e)** Extract all words between `(` and `)` from the given input string as an array (including the parentheses). Assume that the input will not contain any broken parentheses.

```
[](#cb112-1)> let ip = 'another (way) to reuse (portion) matched (by) capture groups'
[](#cb112-2)
[](#cb112-3)// add your solution here
[](#cb112-4)< ["(way)", "(portion)", "(by)"]
```

**f)** Extract all occurrences of `<` up to next occurrence of `>`, provided there is at least one character in between `<` and `>`.

```
[](#cb113-1)> let ip = 'a<apple> 1<> b<bye> 2<> c<cat>'
[](#cb113-2)
[](#cb113-3)// add your solution here
[](#cb113-4)< ["<apple>", "<> b<bye>", "<> c<cat>"]
```

**g)** Use `matchAll` to get the output as shown below for the given input strings. Note the characters used in the input strings carefully.

```
[](#cb114-1)> let row1 = '-2,5 4,+3 +42,-53 4356246,-357532354 '
[](#cb114-2)> let row2 = '1.32,-3.14 634,5.63 63.3e3,9907809345343.235 '
[](#cb114-3)
[](#cb114-4)> const pat4 =      // add your solution here
[](#cb114-5)
[](#cb114-6)// add your solution here for row1
[](#cb114-7)< (4) [Array(2), Array(2), Array(2), Array(2)]
[](#cb114-8)  0: (2) ["-2", "5"]
[](#cb114-9)  1: (2) ["4", "+3"]
[](#cb114-10)  2: (2) ["+42", "-53"]
[](#cb114-11)  3: (2) ["4356246", "-357532354"]
[](#cb114-12)  length: 4
[](#cb114-13)  __proto__: Array(0)
[](#cb114-14)
[](#cb114-15)// add your solution here for row2
[](#cb114-16)< (3) [Array(2), Array(2), Array(2)]
[](#cb114-17)  0: (2) ["1.32", "-3.14"]
[](#cb114-18)  1: (2) ["634", "5.63"]
[](#cb114-19)  2: (2) ["63.3e3", "9907809345343.235"]
[](#cb114-20)  length: 3
[](#cb114-21)  __proto__: Array(0)
```

**h)** This is an extension to previous question. Sum each pair of numbers that are separated by a comma.

```
[](#cb115-1)> let row1 = '-2,5 4,+3 +42,-53 4356246,-357532354 '
[](#cb115-2)> let row2 = '1.32,-3.14 634,5.63 63.3e3,9907809345343.235 '
[](#cb115-3)
[](#cb115-4)// should be same as previous question
[](#cb115-5)> const pat5 =      // add your solution here
[](#cb115-6)
[](#cb115-7)// add your solution here for row1
[](#cb115-8)< [3, 7, -11, -353176108]
[](#cb115-9)
[](#cb115-10)// add your solution here for row2
[](#cb115-11)< [-1.82, 639.63, 9907809408643.234]
```

**i)** Use `split` method to get the output as shown below.

```
[](#cb116-1)> let ip = '42:no-output;1000:car-truck;SQEX49801'
[](#cb116-2)
[](#cb116-3)// add your solution here
[](#cb116-4)< ["42", "output", "1000", "truck", "SQEX49801"]
```

**j)** Write a string function that changes given input to alternate case. The first alphabet should be changed to lowercase, the next one to uppercase and then lowercase and so on. Characters other than alphabets should be left alone and not affect case changing.

```
[](#cb117-1)> function aLtErNaTeCaSe(ip) {
[](#cb117-2)      // add your solution here
[](#cb117-3)  }
[](#cb117-4)
[](#cb117-5)> aLtErNaTeCaSe('HI THERE!')
[](#cb117-6)< "hI tHeRe!"
[](#cb117-7)> aLtErNaTeCaSe('good morning')
[](#cb117-8)< "gOoD mOrNiNg"
[](#cb117-9)> aLtErNaTeCaSe('Sample123string42with777numbers')
[](#cb117-10)< "sAmPlE123sTrInG42wItH777nUmBeRs"
```

**k)** Replace the string `par` with `spar`, `spare` with `extra` and `park` with `garden`

```
[](#cb118-1)> let s1 = 'apartment has a park'
[](#cb118-2)> let s2 = 'do you have a spare cable'
[](#cb118-3)> let s3 = 'write a parser'
[](#cb118-4)
[](#cb118-5)> let d1 =          // add your solution here
[](#cb118-6)> const pat6 =      // add your solution here
[](#cb118-7)
[](#cb118-8)> s1.replace(pat6, k => d1[k])
[](#cb118-9)< "aspartment has a garden"
[](#cb118-10)> s2.replace(pat6, k => d1[k])
[](#cb118-11)< "do you have a extra cable"
[](#cb118-12)> s3.replace(pat6, k => d1[k])
[](#cb118-13)< "write a sparser"
```

# Character class

This chapter will discuss how to create your own custom placeholders to match limited set of characters and various metacharacters applicable inside character classes. You'll also learn about escape sequences for predefined character sets.

## Custom character sets

Characters enclosed inside `[]` metacharacters is a character class (or set). It will result in matching any one of those characters once. It is similar to using single character alternations inside a grouping, but without the additional effects of a capture group. In addition, character classes have their own versions of metacharacters and provide special predefined sets for common use cases. Quantifiers are applicable to character classes as well.

```
[](#cb119-1)// same as: /cot|cut/ or /c(o|u)t/
[](#cb119-2)> ['cute', 'cat', 'cot', 'coat', 'cost'].filter(w => /c[ou]t/.test(w))
[](#cb119-3)< ["cute", "cot"]
[](#cb119-4)
[](#cb119-5)// same as: /(a|e|o)+t/g
[](#cb119-6)> 'meeting cute boat site foot'.replace(/[aeo]+t/g, 'X')
[](#cb119-7)< "mXing cute bX site fX"
[](#cb119-8)
[](#cb119-9)> 'Sample123string42with777numbers'.match(/[0123456789]+/g)
[](#cb119-10)< ["123", "42", "777"]
```

## Range of characters

Character classes have their own metacharacters to help define the sets succinctly. Metacharacters outside of character classes like `^`, `$`, `()` etc either don't have special meaning or have completely different one inside the character classes. First up, the `-` metacharacter that helps to define a range of characters instead of having to specify them all individually.

```
[](#cb120-1)// all digits
[](#cb120-2)> 'Sample123string42with777numbers'.match(/[0-9]+/g)
[](#cb120-3)< ["123", "42", "777"]
[](#cb120-4)
[](#cb120-5)// whole words made up of lowercase alphabets and digits only
[](#cb120-6)> 'coat Bin food tar12 best'.match(/\b[a-z0-9]+\b/g)
[](#cb120-7)< ["coat", "food", "tar12", "best"]
[](#cb120-8)
[](#cb120-9)// whole words made up of lowercase alphabets, but starting with 'p' to 'z'
[](#cb120-10)> 'coat tin food put stoop best'.match(/\b[p-z][a-z]*\b/g)
[](#cb120-11)< ["tin", "put", "stoop"]
[](#cb120-12)
[](#cb120-13)// whole words made up of only 'a' to 'f' and 'p' to 't' lowercase alphabets
[](#cb120-14)> 'coat tin food put stoop best'.match(/\b[a-fp-t]+\b/g)
[](#cb120-15)< ["best"]
```

## Negating character sets

The `^` metacharacter has to specified as the first character of the character class. It negates the set, so all characters other than those specified will be matched.

```
[](#cb121-1)// all non-digits
[](#cb121-2)> 'Sample123string42with777numbers'.match(/[^0-9]+/g)
[](#cb121-3)< ["Sample", "string", "with", "numbers"]
[](#cb121-4)
[](#cb121-5)// deleting characters from start of string based on a delimiter
[](#cb121-6)> 'foo=42; baz=123'.replace(/^[^=]+/, '')
[](#cb121-7)< "=42; baz=123"
[](#cb121-8)> 'foo:123:bar:baz'.replace(/^([^:]+:){2}/, '')
[](#cb121-9)< "bar:baz"
[](#cb121-10)
[](#cb121-11)// deleting characters at end of string based on a delimiter
[](#cb121-12)> 'foo=42; baz=123'.replace(/=[^=]+$/, '')
[](#cb121-13)< "foo=42; baz"
```

As highlighted earlier, handle negative logic with care, as you might end up matching more than you wanted. Sometimes, it is easier to use positive character class and inverting the test condition instead of using negated character class.

```
[](#cb122-1)> let words = ['tryst', 'fun', 'glyph', 'pity', 'why']
[](#cb122-2)
[](#cb122-3)// elements not containing vowel characters
[](#cb122-4)> words.filter(w => /^[^aeiou]+$/.test(w))
[](#cb122-5)< ["tryst", "glyph", "why"]
[](#cb122-6)
[](#cb122-7)// easier to write and maintain, note the use of '!' operator
[](#cb122-8)// but this'll match empty strings too unlike the previous solution
[](#cb122-9)> words.filter(w => !/[aeiou]/.test(w))
[](#cb122-10)< ["tryst", "glyph", "why"]
```

## Matching metacharacters literally

Similar to other metacharacters, prefix `\` to character class metacharacters to match them literally. Some of them can be achieved by different placement as well.

`-` should be first or last character or escaped using `\`.

```
[](#cb123-1)> 'ab-cd gh-c 12-423'.match(/\b[a-z-]{2,}\b/g)
[](#cb123-2)< ["ab-cd", "gh-c"]
[](#cb123-3)
[](#cb123-4)> 'ab-cd gh-c 12-423'.match(/\b[a-z\-0-9]{2,}\b/g)
[](#cb123-5)< ["ab-cd", "gh-c", "12-423"]
```

`^` should be other than first character or escaped using `\`.

```
[](#cb124-1)> 'f*(a^b) - 3*(a+b)'.match(/a[+^]b/g)
[](#cb124-2)< ["a^b", "a+b"]
[](#cb124-3)
[](#cb124-4)> 'f*(a^b) - 3*(a+b)'.match(/a[\^+]b/g)
[](#cb124-5)< ["a^b", "a+b"]
```

`[` doesn't need escaping, but you can escape it if you wish. `]` should be escaped with `\`.

```
[](#cb125-1)> 'words[5] = tea'.match(/[a-z[\]0-9]+/)[0]
[](#cb125-2)< "words[5]"
```

`\` should be escaped using `\`.

```
[](#cb126-1)> console.log('5ba\\babc2'.match(/[a\\b]+/)[0])
[](#cb126-2)< ba\bab
```

## Escape sequence character sets

Commonly used character sets have predefined escape sequences:

*   `\w` is similar to `[A-Za-z0-9_]` for matching word characters (recall the definition for word boundaries)
*   `\d` is similar to `[0-9]` for matching digit characters
*   `\s` is similar to `[ \t\r\n\f\v]` for matching whitespace characters

These escape sequences can be used as a standalone sequence or inside a character class. As mentioned before, the examples and description will assume that the input is made up of ASCII characters only. Use `\W`, `\D` and `\S` respectively for their negated set.

```
[](#cb127-1)> 'Sample123string42with777numbers'.split(/\d+/)
[](#cb127-2)< ["Sample", "string", "with", "numbers"]
[](#cb127-3)
[](#cb127-4)> 'sea eat car rat eel tea'.match(/\b\w/g).join('')
[](#cb127-5)< "secret"
[](#cb127-6)
[](#cb127-7)> 'tea sea-pit sit-lean bean'.match(/[\w\s]+/g)
[](#cb127-8)< ["tea sea", "pit sit", "lean bean"]
[](#cb127-9)
[](#cb127-10)> 'Sample123string42with777numbers'.replace(/\D+/g, '-')
[](#cb127-11)< "-123-42-777-"
[](#cb127-12)
[](#cb127-13)> '   1..3 \v\f foo_baz 42\tzzz \r\n1-2-3  '.match(/\S+/g)
[](#cb127-14)< ["1..3", "foo_baz", "42", "zzz", "1-2-3"]
```

## Numeric ranges

Character classes can also be used to construct numeric ranges.

```
[](#cb128-1)// numbers between 10 to 29
[](#cb128-2)> '23 154 12 26 98234'.match(/\b[12]\d\b/g)
[](#cb128-3)< ["23", "12", "26"]
[](#cb128-4)
[](#cb128-5)// numbers >= 100
[](#cb128-6)> '23 154 12 26 98234'.match(/\b\d{3,}\b/g)
[](#cb128-7)< ["154", "98234"]
[](#cb128-8)// numbers >= 100 if there are leading zeros
[](#cb128-9)> '0501 035 154 12 26 98234'.match(/\b0*[1-9]\d{2,}\b/g)
[](#cb128-10)< ["0501", "154", "98234"]
```

However, it is easy to miss corner cases and some ranges are complicated to design. In such cases, it is better to match all the numbers and then add code to use actual numeric operations.

```
[](#cb129-1)// numbers < 350
[](#cb129-2)> '45 349 651 593 4 204'.match(/\d+/g).filter(n => n < 350)
[](#cb129-3)< ["45", "349", "4", "204"]
[](#cb129-4)> '45 349 651 593 4 204'.replace(/\d+/g, m => m < 350 ? 0 : 1)
[](#cb129-5)< "0 0 1 1 0 0"
[](#cb129-6)
[](#cb129-7)// numbers between 200 and 650
[](#cb129-8)> '45 349 651 593 4 204'.match(/\d+/g).filter(n => n >= 200 && n <= 650)
[](#cb129-9)< ["349", "593", "204"]
```

> ![info](media/file2.svg) See [regular-expressions: matching numeric ranges](https://www.regular-expressions.info/numericranges.html) for more examples.

## Cheatsheet and Summary

| Note | Description |
| --- | --- |
| `[ae;o]` | match **any** of these characters once |
|  | quantifiers are applicable to character classes too |
| `[3-7]` | **range** of characters from `3` to `7` |
| `[^=b2]` | **negated set**, match other than `=` or `b` or `2` |
| `[a-z-]` | `-` should be first/last or escaped using `\` to match literally |
| `[+^]` | `^` shouldn't be first character or escaped using `\` |
| `[\]\\]` | `]` and `\` should be escaped using `\` |
|  | `[` doesn't need escaping, but `\[` can also be used |
| `\w` | similar to `[A-Za-z0-9_]` for matching word characters |
| `\d` | similar to `[0-9]` for matching digit characters |
| `\s` | similar to `[ \t\n\r\f\v]` for matching whitespace characters |
|  | assumes input encoding is ASCII |
|  | use `\W`, `\D`, and `\S` for their opposites respectively |

This chapter focused on how to create custom placeholders to match limited set of characters. Grouping and character classes can be considered as two levels of abstractions. On the one hand, you can have character sets inside `[]` and on the other hand, you can have multiple alternations grouped inside `()` including character classes. As anchoring and quantifiers can be applied to both these abstractions, you can begin to see how regular expressions is considered a mini-programming language. In coming chapters, you'll even see how to negate groupings similar to negated character class in certain scenarios.

## Exercises

**a)** For the array `items`, filter all elements starting with `hand` and ending with `s` or `y` or `le`. No other character in between, for example, `hands` should match but not `hand-has`.

```
[](#cb130-1)> let items = ['-handy', 'hand', 'handy', 'handled', 'hands', 'handle']
[](#cb130-2)
[](#cb130-3)// add your solution here
[](#cb130-4)< ["handy", "hands", "handle"]
```

**b)** Replace all whole words `reed` or `read` or `red` with `X`.

```
[](#cb131-1)> let ip = 'redo red credible :read: rod reed bred'
[](#cb131-2)
[](#cb131-3)// add your solution here
[](#cb131-4)< "redo X credible :X: rod X bred"
```

**c)** For the array `words`, filter all elements containing `e` or `i` followed by `l` or `n`. Note that the order mentioned should be followed.

```
[](#cb132-1)> let words = ['surrender', 'unicorn', 'newer', 'door', 'empty', 'eel', 'pest']
[](#cb132-2)
[](#cb132-3)// add your solution here
[](#cb132-4)< ["surrender", "unicorn", "eel"]
```

**d)** For the array `words`, filter all elements containing `e` or `i` and `l` or `n` in any order.

```
[](#cb133-1)> let words = ['surrender', 'unicorn', 'newer', 'door', 'empty', 'eel', 'pest']
[](#cb133-2)
[](#cb133-3)// add your solution here
[](#cb133-4)< ["surrender", "unicorn", "newer", "eel"]
```

**e)** Extract all hex character sequences, with `0x` optional prefix. Match the characters case insensitively, and the sequences shouldn't be surrounded by other word characters.

```
[](#cb134-1)> let str1 = '128A foo 0xfe32 34 0xbar'
[](#cb134-2)> let str2 = '0XDEADBEEF place 0x0ff1ce bad'
[](#cb134-3)
[](#cb134-4)> const hex_seq =       // add your solution here
[](#cb134-5)
[](#cb134-6)> str1.match(hex_seq)
[](#cb134-7)< ["128A", "0xfe32", "34"]
[](#cb134-8)> str2.match(hex_seq)
[](#cb134-9)< ["0XDEADBEEF", "0x0ff1ce", "bad"]
```

**f)** Delete from `(` to the next occurrence of `)` unless they contain parentheses characters in between.

```
[](#cb135-1)> let str1 = 'def factorial()'
[](#cb135-2)> let str2 = 'a/b(division) + c%d(#modulo) - (e+(j/k-3)*4)'
[](#cb135-3)> let str3 = 'Hi there(greeting). Nice day(a(b)'
[](#cb135-4)
[](#cb135-5)> const remove_parentheses =        // add your solution here
[](#cb135-6)
[](#cb135-7)> str1.replace(remove_parentheses, '')
[](#cb135-8)< "def factorial"
[](#cb135-9)> str2.replace(remove_parentheses, '')
[](#cb135-10)< "a/b + c%d - (e+*4)"
[](#cb135-11)> str3.replace(remove_parentheses, '')
[](#cb135-12)< "Hi there. Nice day(a"
```

**g)** For the array `words`, filter all elements not starting with `e` or `p` or `u`.

```
[](#cb136-1)> let words = ['surrender', 'unicorn', 'newer', 'door', 'empty', 'eel', 'pest']
[](#cb136-2)
[](#cb136-3)// add your solution here
[](#cb136-4)< ["surrender", "newer", "door"]
```

**h)** For the array `words`, filter all elements not containing `u` or `w` or `ee` or `-`.

```
[](#cb137-1)> let words = ['p-t', 'you', 'tea', 'heel', 'owe', 'new', 'reed', 'ear']
[](#cb137-2)
[](#cb137-3)// add your solution here
[](#cb137-4)< ["tea", "ear"]
```

**i)** The given input strings contain fields separated by `,` and fields can be empty too. Replace last three fields with `WHTSZ323`.

```
[](#cb138-1)> let row1 = '(2),kite,12,,D,C,,'
[](#cb138-2)> let row2 = 'hi,bye,sun,moon'
[](#cb138-3)
[](#cb138-4)> const pat1 =      // add your solution here
[](#cb138-5)
[](#cb138-6)// add your solution here for row1
[](#cb138-7)< "(2),kite,12,,D,WHTSZ323"
[](#cb138-8)// add your solution here for row2
[](#cb138-9)< "hi,WHTSZ323"
```

**j)** Split the given strings based on consecutive sequence of digit or whitespace characters.

```
[](#cb139-1)> let s1 = 'lion \t Ink32onion Nice'
[](#cb139-2)> let s2 = '**1\f2\n3star\t7 77\r**'
[](#cb139-3)
[](#cb139-4)> const pat2 =      // add your solution here
[](#cb139-5)
[](#cb139-6)> s1.split(pat2)
[](#cb139-7)< ["lion", "Ink", "onion", "Nice"]
[](#cb139-8)> s2.split(pat2)
[](#cb139-9)< ["**", "star", "**"]
```

**k)** Delete all occurrences of the sequence `<characters>` where `characters` is one or more non `>` characters and cannot be empty.

```
[](#cb140-1)> let ip = 'a<apple> 1<> b<bye> 2<> c<cat>'
[](#cb140-2)
[](#cb140-3)// add your solution here
[](#cb140-4)< "a 1<> b 2<> c"
```

**l)** `\b[a-z](on|no)[a-z]\b` is same as `\b[a-z][on]{2}[a-z]\b`. True or False? Sample input lines shown below might help to understand the differences, if any.

```
[](#cb141-1)> console.log('known\nmood\nknow\npony\ninns')
[](#cb141-2)  known
[](#cb141-3)  mood
[](#cb141-4)  know
[](#cb141-5)  pony
[](#cb141-6)  inns
```

**m)** For the given array, filter all elements containing any number sequence greater than `624`.

```
[](#cb142-1)> let items = ['h0000432ab', 'car00625', '42_624 0512', '3.14 96 2 foo1234baz']
[](#cb142-2)
[](#cb142-3)// add your solution here
[](#cb142-4)< ["car00625", "3.14 96 2 foo1234baz"]
```

**n)** Convert the given input string to two different arrays as shown below.

```
[](#cb143-1)> let ip = 'price_42 roast^\t\n^-ice==cat\neast'
[](#cb143-2)
[](#cb143-3)// add your solution here
[](#cb143-4)< ["price_42", "roast", "ice", "cat", "east"]
[](#cb143-5)
[](#cb143-6)// add your solution here
[](#cb143-7)< ["price_42", " ", "roast", "^ \n^-", "ice", "==", "cat", "\n", "east"]
```

**o)** Filter all elements whose first non-whitespace character is not a `#` character. Any element made up of only whitespace characters should be ignored as well.

```
[](#cb144-1)> let items = ['    #comment', '\t\napple #42', '#oops', 'sure', 'no#1', '\t\r\f']
[](#cb144-2)
[](#cb144-3)// add your solution here
[](#cb144-4)< [" \napple #42", "sure", "no#1"]
```

**p)** For the given string, surround all whole words with `{}` except for whole words `par` and `cat`.

```
[](#cb145-1)> let ip = 'part; cat {super} rest_42 par scatter'
[](#cb145-2)
[](#cb145-3)// add your solution here
[](#cb145-4)< "{part}; cat {{super}} {rest_42} par {scatter}"
```

# Groupings and backreferences

This chapter will show how to reuse portion matched by capture groups via backreferences within regexp definition and replacement section. You'll also learn some special grouping syntax for cases where plain capture groups isn't enough.

## Backreferences

First up, how to refer to capture group portions directly in regexp definition and replacement section. You have already seen how to refer to text captured by groups with `match` and `matchAll` methods. You've also seen how to pass captured portions to a function in `replace` method. More directly, you can use backreference `\N` (within the regexp definition) and `$N` (replacement section), where `N` is the capture group you want. What's more, you can also apply quantifiers to backreferences when used in regexp definition. All the various forms is listed below:

*   in replacement section, use `$1`, `$2`, etc to refer to the corresponding capture group
*   in replacement section, use `$&` to refer to entire matched portion
    *   `` $` `` gives string before the matched portion
    *   `$'` gives string after the matched portion
*   within regexp definition, use `\1`, `\2`, etc to refer to the corresponding capture group

```
[](#cb146-1)// remove square brackets that surround digit characters
[](#cb146-2)> '[52] apples [and] [31] mangoes'.replace(/\[(\d+)\]/g, '$1')
[](#cb146-3)< "52 apples [and] 31 mangoes"
[](#cb146-4)
[](#cb146-5)// replace __ with _ and delete _ if it is alone
[](#cb146-6)> '_foo_ __123__ _baz_'.replace(/(_)?_/g, '$1')
[](#cb146-7)< "foo _123_ baz"
[](#cb146-8)
[](#cb146-9)// swap words that are separated by a comma
[](#cb146-10)> 'good,bad 42,24'.replace(/(\w+),(\w+)/g, '$2,$1')
[](#cb146-11)< "bad,good 24,42"
```

Here's some examples for using backreferences available by default without needing capture groups.

```
[](#cb147-1)// add something around the entire matched portion
[](#cb147-2)> '52 apples and 31 mangoes'.replace(/\d+/g, '($&)')
[](#cb147-3)< "(52) apples and (31) mangoes"
[](#cb147-4)> 'Hello world'.replace(/.*/, 'Hi. $&. Have a nice day')
[](#cb147-5)< "Hi. Hello world. Have a nice day"
[](#cb147-6)
[](#cb147-7)// duplicate first field and add it as last field
[](#cb147-8)> 'fork,42,nice,3.14'.replace(/,.+/, '$&,$`')
[](#cb147-9)< "fork,42,nice,3.14,fork"
```

And here's some examples for using backreferences within regexp definition.

```
[](#cb148-1)// elements that have at least one consecutive repeated word character
[](#cb148-2)> let words = ['moon', 'mono', 'excellent', 'poll']
[](#cb148-3)> words.filter(w => /(\w)\1/.test(w))
[](#cb148-4)< ["moon", "excellent", "poll"]
[](#cb148-5)
[](#cb148-6)// remove any number of consecutive duplicate words separated by space
[](#cb148-7)// note the use of quantifier on backreference
[](#cb148-8)// use \W+ instead of space to cover cases like 'a;a<-;a'
[](#cb148-9)> 'aa a a a 42 f_1 f_1 f_13.14'.replace(/\b(\w+)(  \1)+\b/g, '$1')
[](#cb148-10)< "aa a 42 f_1 f_13.14"
```

## Backreference oddities

Since `$` is special in replacement section, there's an issue to place it literally if followed by numbers. Usually, escaping is used for such purposes, but here you need to use `$$`.

```
[](#cb149-1)// no capture group used, so '$1' is inserted literally
[](#cb149-2)> 'cat'.replace(/a/, '{$1}')
[](#cb149-3)< "c{$1}t"
[](#cb149-4)// capture group used, '\$1' is same as '$1' here
[](#cb149-5)> 'cat'.replace(/(a)/, '{\$1}')
[](#cb149-6)< "c{a}t"
[](#cb149-7)
[](#cb149-8)// use '$$' to avoid backreference and insert '$' literally
[](#cb149-9)> 'cat'.replace(/(a)/, '{$$1}')
[](#cb149-10)< "c{$1}t"
```

Another issue is how to avoid ambiguity when you have normal digits immediately following a backreference? It'll depend on how many backreferences are present in the pattern and whether you need to avoid ambiguity in regexp definition or replacement section. For example, if there are less than 10 groups, then something like `$12` will refer to first capture group and `2` as a character. If there are no capture groups, then something like `$5` will get inserted literally as `$` and `5`.

```
[](#cb150-1)// $15 here will backreference 1st group and use 5 as a character
[](#cb150-2)> '[52] apples and [31] mangoes'.replace(/\[(\d+)\]/g, '($15)')
[](#cb150-3)< "(525) apples and (315) mangoes"
[](#cb150-4)
[](#cb150-5)// $3 will be inserted literally since there is only one capture group
[](#cb150-6)> '[52] apples and [31] mangoes'.replace(/\[(\d+)\]/g, '$3')
[](#cb150-7)< "$3 apples and $3 mangoes"
[](#cb150-8)
[](#cb150-9)// $1 will be inserted literally since there are no capture groups
[](#cb150-10)> '[52] apples and [31] mangoes'.replace(/\[\d+\]/g, '$1')
[](#cb150-11)< "$1 apples and $1 mangoes"
```

On the other hand, if you have more than `9` but less than `100` groups, then there would be an issue if you want to refer to single digit group followed by literal digit characters. The workaround is to prefix `0` such that number of digits after `$` equals the number of digits required for the highest capture group. So, if you have more than `9` but less than `100` groups, `$05` will refer to 5th capture group and any digit after that will be treated literally.

```
[](#cb151-1)// for illustration purposes, 12 capture groups have been defined here
[](#cb151-2)// if you want to reference 2-digit group, there's no issue
[](#cb151-3)> 'abcdefghijklmn'.replace(/(.)(.)(.)(.)(.)(.)(.)(.)(.)(.)(.)(.)/, '$11')
[](#cb151-4)< "kmn"
[](#cb151-5)
[](#cb151-6)// what if you wanted to reference 1st group followed by '1' as a character?
[](#cb151-7)// using \x31 wouldn't work as it still results in $11
[](#cb151-8)> 'abcdefghijklmn'.replace(/(.)(.)(.)(.)(.)(.)(.)(.)(.)(.)(.)(.)/, '$1\x31')
[](#cb151-9)< "kmn"
[](#cb151-10)// prefix a '0' so that '$01' becomes the reference and '1' becomes character
[](#cb151-11)> 'abcdefghijklmn'.replace(/(.)(.)(.)(.)(.)(.)(.)(.)(.)(.)(.)(.)/, '$011')
[](#cb151-12)< "a1mn"
```

The workaround is simpler in regexp definition. The `0` prefix trick doesn't work, but using ASCII code with `\xhh` works. For example, `\1\x31` will refer to first capture group followed by `1` as a character.

```
[](#cb152-1)> 'abcdefghijklmna1d'.replace(/(.)(.)(.)(.)(.)(.)(.)(.)(.)(.)(.)(.).*\1\x31/, 'X')
[](#cb152-2)< "Xd"
```

## Non-capturing groups

Grouping has many uses like applying quantifier on a regexp portion, creating terse regexp by factoring common portions and so on. It also affects the output of `split` method as seen in [split with capture groups](#ch009.xhtml_split-with-capture-groups) section. Unlike similar methods in other languages, `match` method with `g` flag isn't affected by capture groups and returns entire matched portions.

```
[](#cb153-1)// split method without capture group
[](#cb153-2)> 'Sample123string42with777numbers'.split(/\d+/)
[](#cb153-3)< ["Sample", "string", "with", "numbers"]
[](#cb153-4)// split method with capture group
[](#cb153-5)> 'Sample123string42with777numbers'.split(/(\d+)/)
[](#cb153-6)< ["Sample", "123", "string", "42", "with", "777", "numbers"]
[](#cb153-7)
[](#cb153-8)// match method example with 'g' flag and capture groups
[](#cb153-9)> 'effort flee facade oddball rat tool'.match(/\b\w*(\w)\1\w*\b/g)
[](#cb153-10)< ["effort", "flee", "oddball", "tool"]
[](#cb153-11)// here's another example
[](#cb153-12)> 'hi 123123123 bye 456123456'.match(/(123)+/g)
[](#cb153-13)< ["123123123", "123"]
```

When backreferencing is not required, you can use a non-capturing group to avoid behavior change of `split` method. It also helps to avoid keeping a track of capture group numbers when that particular group is not needed for backreferencing. The syntax is `(?:pat)` to define a non-capturing group, where `pat` is an abbreviation for a portion of regular expression pattern. More such special groups starting with `(?` syntax will be discussed later on.

```
[](#cb154-1)// here, grouping is needed to take out common portion and apply quantifier
[](#cb154-2)// but using capture group will not give expected output
[](#cb154-3)> '123hand42handy777handful500'.split(/hand(y|ful)?/)
[](#cb154-4)< ["123", undefined, "42", "y", "777", "ful", "500"]
[](#cb154-5)// non-capturing group to the rescue
[](#cb154-6)> '123hand42handy777handful500'.split(/hand(?:y|ful)?/)
[](#cb154-7)< ["123", "42", "777", "500"]
[](#cb154-8)
[](#cb154-9)// with normal grouping, need to keep track of all the groups
[](#cb154-10)> '1,2,3,4,5,6,7'.replace(/^(([^,]+,){3})([^,]+)/, '$1($3)')
[](#cb154-11)< "1,2,3,(4),5,6,7"
[](#cb154-12)// using non-capturing groups, only relevant groups have to be tracked
[](#cb154-13)> '1,2,3,4,5,6,7'.replace(/^((?:[^,]+,){3})([^,]+)/, '$1($2)')
[](#cb154-14)< "1,2,3,(4),5,6,7"
```

Referring to text matched by a capture group with a quantifier will give only the last match, not entire match. Use a capture group around the grouping and quantifier together to get the entire matching portion. In such cases, the inner grouping is an ideal candidate to use non-capturing group.

```
[](#cb155-1)// '$1' here contains only the fourth field
[](#cb155-2)> 'so:cat:rest:in:put:to'.replace(/^([^:]+:){4}/, '($1)')
[](#cb155-3)< "(in:)put:to"
[](#cb155-4)
[](#cb155-5)// '$1' will now contain the entire matching portion
[](#cb155-6)> 'so:cat:rest:in:put:to'.replace(/^((?:[^:]+:){4})/, '($1)')
[](#cb155-7)< "(so:cat:rest:in:)put:to"
```

## Named capture groups

Regexp can get cryptic and difficult to maintain, even for seasoned programmers. There are a few constructs to help add clarity. One such is naming the capture groups and using that name for backreferencing instead of plain numbers. In addition, the named capture group portions can be extracted as key-value pairs using the `groups` property. The syntax is:

*   `(?<name>pat)` for naming the capture groups
*   `\k<name>` for backreferencing in regexp definition
*   `$<name>` for backreferencing in replacement section

```
[](#cb156-1)> let row = 'today,2008-03-24,food,2008-03-24,nice,2018-10-25,5632'
[](#cb156-2)
[](#cb156-3)// same as: /(\d{4}-\d{2}-\d{2}).*\1/
[](#cb156-4)> row.match(/(?<date>\d{4}-\d{2}-\d{2}).*\k<date>/)[0]
[](#cb156-5)< "2008-03-24,food,2008-03-24"
[](#cb156-6)
[](#cb156-7)// giving names to first and second captured words
[](#cb156-8)// same as: replace(/(\w+),(\w+)/g, '$2,$1')
[](#cb156-9)> 'good,bad 42,24'.replace(/(?<fw>\w+),(?<sw>\w+)/g, '$<sw>,$<fw>')
[](#cb156-10)< "bad,good 24,42"
```

Here's an example with `groups` property.

```
[](#cb157-1)> let m = '2018-10-25,car'.match(/(?<date>[^,]+),(?<product>[^,]+)/)
[](#cb157-2)
[](#cb157-3)> m.groups
[](#cb157-4)< {date: "2018-10-25", product: "car"}
[](#cb157-5)> m.groups.date
[](#cb157-6)< "2018-10-25"
[](#cb157-7)> m.groups.product
[](#cb157-8)< "car"
```

## Cheatsheet and Summary

| Note | Description |
| --- | --- |
| Backreference | gives matched portion of Nth capture group |
|  | use `$1`, `$2`, `$3`, etc in replacement section |
|  | `$&` gives entire matched portion |
|  | `` $` `` gives string before the matched portion |
|  | `$'` gives string after the matched portion |
|  | use `\1`, `\2`, `\3`, etc within regexp definition |
| `$$` | insert `$` literally in replacement section |
| `$0N` | same as `$N`, allows to separate backreference and other digits |
| `\N\xhh` | allows to separate backreference and digits in regexp definition |
| `(?:pat)` | non-capturing group |
| `(?<name>pat)` | named capture group |
|  | use `\k<name>` for backreferencing in regexp definition |
|  | use `$<name>` for backreferencing in replacement section |
|  | named captures are also accessible via `groups` property |

This chapter covered many more features related to grouping — backreferencing to get matched portion of capture groups and naming the groups to add clarity. When capture groups results in unwanted behavior change (ex: `split` method), you can use non-capturing groups instead. You'll see more such special groups in [Lookarounds](#ch013.xhtml_lookarounds) chapter.

## Exercises

**a)** Replace the space character that occurs after a word ending with `a` or `r` with a newline character.

```
[](#cb158-1)> let ip = 'area not a _a2_ roar took 22'
[](#cb158-2)
[](#cb158-3)> console.log()     // add your solution here
[](#cb158-4)  area
[](#cb158-5)  not a
[](#cb158-6)  _a2_ roar
[](#cb158-7)  took 22
```

**b)** Add `[]` around words starting with `s` and containing `e` and `t` in any order.

```
[](#cb159-1)> let ip = 'sequoia subtle exhibit asset sets tests site'
[](#cb159-2)
[](#cb159-3)// add your solution here
[](#cb159-4)< "sequoia [subtle] exhibit asset [sets] tests [site]"
```

**c)** Replace all whole words with `X` that start and end with the same word character. Single character word should get replaced with `X` too, as it satisfies the stated condition.

```
[](#cb160-1)> let ip = 'oreo not a _a2_ roar took 22'
[](#cb160-2)
[](#cb160-3)// add your solution here
[](#cb160-4)< "X not X X X took X"
```

**d)** Convert the given **markdown** headers to corresponding **anchor** tag. Consider the input to start with one or more `#` characters followed by space and word characters. The `name` attribute is constructed by converting the header to lowercase and replacing spaces with hyphens. Can you do it without using a capture group?

```
[](#cb161-1)> let header1 = '# Regular Expressions'
[](#cb161-2)> let header2 = '## Named capture groups'
[](#cb161-3)
[](#cb161-4)> function hyphenify(m) {
[](#cb161-5)      // add your solution here
[](#cb161-6)  }
[](#cb161-7)
[](#cb161-8)> header1.replace()     // add your solution here
[](#cb161-9)< "# <a name='regular-expressions'></a>Regular Expressions"
[](#cb161-10)> header2.replace()     // add your solution here
[](#cb161-11)< "## <a name='named-capture-groups'></a>Named capture groups"
```

**e)** Convert the given **markdown** anchors to corresponding **hyperlinks**.

```
[](#cb162-1)> let anchor1 = "# <a name='regular-expressions'></a>Regular Expressions"
[](#cb162-2)> let anchor2 = "## <a name='subexpression-calls'></a>Subexpression calls"
[](#cb162-3)
[](#cb162-4)> const hyperlink =         // add your solution here
[](#cb162-5)
[](#cb162-6)> anchor1.replace()         // add your solution here
[](#cb162-7)< "[Regular Expressions](#regular-expressions)"
[](#cb162-8)> anchor2.replace()         // add your solution here
[](#cb162-9)< "[Subexpression calls](#subexpression-calls)"
```

**f)** Check if given input strings have words with at least two consecutive repeated alphabets irrespective of case. For example, words like `stillnesS` and `Committee` should return `true` but words like `root` or `readable` or `rotational` should return `false`. Consider word to be as defined in regular expression parlance.

```
[](#cb163-1)> let s1 = 'readable COMMItTEe'
[](#cb163-2)> let s2 = 'rotational sti1lness _foot_'
[](#cb163-3)> let s3 = 'needed repeated'
[](#cb163-4)> let s4 = 'offsh00t'
[](#cb163-5)
[](#cb163-6)> const pat1 =      // add your solution here
[](#cb163-7)
[](#cb163-8)> pat1.test(s1)
[](#cb163-9)true
[](#cb163-10)> pat1.test(s2)
[](#cb163-11)false
[](#cb163-12)> pat1.test(s3)
[](#cb163-13)false
[](#cb163-14)> pat1.test(s4)
[](#cb163-15)true
```

**g)** For the given input string, replace all occurrences of digit sequences with only the unique non-repeating sequence. For example, `232323` should be changed to `23` and `897897` should be changed to `897`. If there no repeats (for example `1234`) or if the repeats end prematurely (for example `12121`), it should not be changed.

```
[](#cb164-1)> let ip = '1234 2323 453545354535 9339 11 60260260'
[](#cb164-2)
[](#cb164-3)// add your solution here
[](#cb164-4)< "1234 23 4535 9339 1 60260260"
```

**h)** Replace sequences made up of words separated by `:` or `.` by the first word of the sequence. Such sequences will end when `:` or `.` is not followed by a word character.

```
[](#cb165-1)> let ip = 'wow:Good:2_two:five: hi-2 bye kite.777.water.'
[](#cb165-2)
[](#cb165-3)// add your solution here
[](#cb165-4)< "wow hi-2 bye kite"
```

**i)** Replace sequences made up of words separated by `:` or `.` by the last word of the sequence. Such sequences will end when `:` or `.` is not followed by a word character.

```
[](#cb166-1)> let ip = 'wow:Good:2_two:five: hi-2 bye kite.777.water.'
[](#cb166-2)
[](#cb166-3)// add your solution here
[](#cb166-4)< "five hi-2 bye water"
```

**j)** Split the given input string on one or more repeated sequence of `cat`.

```
[](#cb167-1)> let ip = 'firecatlioncatcatcatbearcatcatparrot'
[](#cb167-2)
[](#cb167-3)// add your solution here
[](#cb167-4)< ["fire", "lion", "bear", "parrot"]
```

**k)** For the given input string, find all occurrences of digit sequences with at least one repeating sequence. For example, `232323` and `897897`. If the repeats end prematurely, for example `12121`, it should not be matched.

```
[](#cb168-1)> let ip = '1234 2323 453545354535 9339 11 60260260'
[](#cb168-2)
[](#cb168-3)> const pat2 =      // add your solution here
[](#cb168-4)
[](#cb168-5)// entire sequences in the output
[](#cb168-6)// add your solution here
[](#cb168-7)< ["2323", "453545354535", "11"]
[](#cb168-8)
[](#cb168-9)// only the unique sequence in the output
[](#cb168-10)// add your solution here
[](#cb168-11)< ["23", "4535", "1"]
```

**l)** Convert the comma separated strings to corresponding key-value pair mapping as shown below. The keys are `name`, `maths` and `phy` for the three fields in the input strings.

```
[](#cb169-1)> let row1 = 'rohan,75,89'
[](#cb169-2)> let row2 = 'rose,88,92'
[](#cb169-3)
[](#cb169-4)> const pat3 =      // add your solution here
[](#cb169-5)
[](#cb169-6)// add your solution here for row1
[](#cb169-7)< {name: "rohan", maths: "75", phy: "89"}
[](#cb169-8)
[](#cb169-9)// add your solution here for row2
[](#cb169-10)< {name: "rose", maths: "88", phy: "92"}
```

**m)** Surround all whole words with `()`. Additionally, if the whole word is `imp` or `ant`, delete them. Can you do it with single substitution?

```
[](#cb170-1)> let ip = 'tiger imp goat eagle ant important'
[](#cb170-2)
[](#cb170-3)// add your solution here
[](#cb170-4)< "(tiger) () (goat) (eagle) () (important)"
```

# Interlude: Common tasks

Tasks like matching phone numbers, ip addresses, dates, etc are so common that you can often find them collected as a library. This chapter shows some examples for [CommonRegexJS](https://github.com/talyssonoc/CommonRegexJS). See also [Awesome Regex: Collections](https://github.com/aloisdg/awesome-regex#collections).

## CommonRegexJS

There are several ways to use the patterns, see [CommonRegexJS: Usage](https://github.com/talyssonoc/CommonRegexJS#usage) for details. You can also go through [commonregex.js](https://github.com/talyssonoc/CommonRegexJS/blob/master/lib/commonregex.js) and choose the regular expression you need.

```
[](#cb171-1)> let data = 'hello 255.21.255.22 okay'
[](#cb171-2)
[](#cb171-3)> const comm = new CommonRegex(data)
[](#cb171-4)
[](#cb171-5)> comm.IPv4
[](#cb171-6)< ["255.21.255.22"]
```

Make sure to test these patterns for your use case. For example, the below data has a valid IPv4 address followed by another number separated by a dot character. If such cases should be ignored, then you'll have to create your own version of the pattern or change the input accordingly.

```
[](#cb172-1)> let new_data = '23.14.2.4.2 255.21.255.22 567.12.2.1'
[](#cb172-2)
[](#cb172-3)> const ip = new CommonRegex(new_data)
[](#cb172-4)
[](#cb172-5)> ip.IPv4
[](#cb172-6)< ["23.14.2.4", "255.21.255.22"]
```

## Summary

Some patterns are quite complex and not easy to build and validate from scratch. Libraries like **CommonRegexJS** are helpful to reduce your time and effort needed for commonly known tasks. However, you do need to **test** the solution for *your* use case. See also [stackoverflow: validating email addresses](https://stackoverflow.com/questions/201323/how-to-validate-an-email-address-using-a-regular-expression).

# Lookarounds

You've already seen how to create custom character classes and various avatars of special groupings. In this chapter you'll learn more groupings, known as lookarounds, that help to create custom anchors and add conditions within regexp definition. These assertions are also known as **zero-width patterns** because they add restrictions similar to anchors and are not part of the matched portions. Also, you will learn how to negate a grouping similar to negated character sets.

## Conditional expressions

Before you get used to lookarounds too much, it is good to remember that JavaScript is a programming language. You have control structures and you can combine multiple conditions using logical operators, methods like `every/some`, etc. Also, do not forget that regexp is only one of the tools available for string processing.

```
[](#cb173-1)> let items = ['1,2,3,4', 'a,b,c,d', '#foo 123']
[](#cb173-2)
[](#cb173-3)// filter elements containing digit and '#' characters
[](#cb173-4)> items.filter(s => /\d/.test(s) && s.includes('#'))
[](#cb173-5)< ["#foo 123"]
[](#cb173-6)
[](#cb173-7)// modify elements only if it doesn't start with '#'
[](#cb173-8)> items.filter(s => s[0] != '#').map(s => s.replace(/,.+,/, ' '))
[](#cb173-9)< ["1 4", "a d"]
```

## Negative lookarounds

Lookaround assertions can be added in two ways — **lookbehind** and **lookahead**. Each of these can be a **positive** or a **negative** assertion. Syntax wise, lookbehind has an extra `<` compared to the lookahead version. Negative lookarounds can be identified by the use of `!` whereas `=` is used for positive lookarounds. This section is about negative lookarounds, whose complete syntax is shown below.

*   `(?!pat)` for negative lookahead assertion
*   `(?<!pat)` for negative lookbehind assertion

As mentioned earlier, lookarounds are not part of matched portions and do not capture the matched text.

```
[](#cb174-1)// change 'foo' only if it is not followed by a digit character
[](#cb174-2)// note that end of string satisfies the given assertion
[](#cb174-3)// 'foofoo' has two matches as the assertion doesn't consume characters
[](#cb174-4)> 'hey food! foo42 foot5 foofoo'.replace(/foo(?!\d)/g, 'baz')
[](#cb174-5)< "hey bazd! foo42 bazt5 bazbaz"
[](#cb174-6)
[](#cb174-7)// change 'foo' only if it is not preceded by _
[](#cb174-8)// note how 'foo' at start of string is matched as well
[](#cb174-9)> 'foo _foo 42foofoo'.replace(/(?<!_)foo/g, 'baz')
[](#cb174-10)< "baz _foo 42bazbaz"
[](#cb174-11)
[](#cb174-12)// overlap example
[](#cb174-13)// 'foot' doesn't match because it is preceded by '_'
[](#cb174-14)// the '_' before 'foot' was considered even though it got replaced
[](#cb174-15)> 'food _fool 42foo_foot'.replace(/(?<!_)foo./g, 'baz')
[](#cb174-16)< "baz _fool 42bazfoot"
```

Can be mixed with anchors and other regexp features to define truly powerful restrictions.

```
[](#cb175-1)// change whole word only if it is not preceded by : or --
[](#cb175-2)> ':cart apple --rest ;tea'.replace(/(?<!:|--)\b\w+/g, 'X')
[](#cb175-3)< ":cart X --rest ;X"
[](#cb175-4)
[](#cb175-5)// add space to word boundaries, but not at start or end of string
[](#cb175-6)// similar to: replace(/\b/g, ' ').trim()
[](#cb175-7)> 'foo_baz=num1+35*42/num2'.replace(/(?<!^)\b(?!$)/g, ' ')
[](#cb175-8)< "foo_baz = num1 + 35 * 42 / num2"
```

In all the examples so far, lookahead grouping was placed as a suffix and lookbehind as a prefix. This is how they are used most of the time, but not the only way to use them. Lookarounds can be placed anywhere and multiple lookarounds can be combined in any order. They do not consume characters nor do they play a role in matched portions. They just let you know whether the condition you want to test is satisfied from the current location in the input string.

```
[](#cb176-1)// these two are equivalent
[](#cb176-2)// replace a character as long as it is not preceded by 'p' or 'r'
[](#cb176-3)> 'spare'.replace(/(?<![pr])./g, '*')
[](#cb176-4)< "**a*e"
[](#cb176-5)> 'spare'.replace(/.(?<![pr].)/g, '*')
[](#cb176-6)< "**a*e"
[](#cb176-7)
[](#cb176-8)// replace 'par' as long as 's' is not present later in the input
[](#cb176-9)// this assumes that the lookaround doesn't conflict with search pattern
[](#cb176-10)// i.e. 's' will not conflict 'par' but would affect if it was 'r' and 'par'
[](#cb176-11)> 'par spare part party'.replace(/par(?!.*s)/g, 'X')
[](#cb176-12)< "par sXe Xt Xty"
[](#cb176-13)> 'par spare part party'.replace(/(?!.*s)par/g, 'X')
[](#cb176-14)< "par sXe Xt Xty"
[](#cb176-15)
[](#cb176-16)// since the three assertions used here are all zero-width,
[](#cb176-17)// all of the 6 possible combinations will be equivalent
[](#cb176-18)> 'foo_baz=num1+35*42/num2'.replace(/(?!$)\b(?<!^)/g, ' ')
[](#cb176-19)< "foo_baz = num1 + 35 * 42 / num2"
```

> ![info](media/file2.svg) See [this stackoverflow Q&A](https://stackoverflow.com/questions/50011366/javascript-regex-negative-lookbehind-not-working-in-firefox) for a workaround if lookbehind isn't supported.

## Positive lookarounds

Unlike negative lookarounds, absence of the pattern will not satisfy positive lookarounds. Instead, for the condition to satisfy, the pattern has to match actual characters and/or zero-width assertions. Positive lookaround can be identified by use of `=` in the grouping. The complete syntax looks like:

*   `(?=pat)` for positive lookahead assertion
*   `(?<=pat)` for positive lookbehind assertion

```
[](#cb177-1)// extract digits only if it is followed by ,
[](#cb177-2)// note that end of string doesn't qualify as this is positive assertion
[](#cb177-3)> '42 foo-5, baz3; x83, y-20; f12'.match(/\d+(?=,)/g)
[](#cb177-4)< ["5", "83"]
[](#cb177-5)// extract digits only if it is preceded by - and followed by , or ;
[](#cb177-6)> '42 foo-5, baz3; x83, y-20; f12'.match(/(?<=-)\d+(?=[;,])/g)
[](#cb177-7)< ["5", "20"]
[](#cb177-8)
[](#cb177-9)// same as: match(/\b\w/g).join('')
[](#cb177-10)> 'sea eat car rat eel tea'.replace(/(?<=\b\w)\w*\W*/g, '')
[](#cb177-11)< "secret"
[](#cb177-12)
[](#cb177-13)// replace 'par' as long as 'part' occurs as a whole word later in the line
[](#cb177-14)> 'par spare part party'.replace(/par(?=.*\bpart\b)/g, 'X')
[](#cb177-15)< "X sXe part party"
```

Lookarounds are quite handy in dealing with field based processing.

```
[](#cb178-1)// except first and last fields
[](#cb178-2)> '1,two,3,four,5'.match(/(?<=,)[^,]+(?=,)/g)
[](#cb178-3)< ["two", "3", "four"]
[](#cb178-4)
[](#cb178-5)// replace empty fields with NA
[](#cb178-6)// note that in this example, order of lookbehind and lookahead doesn't matter
[](#cb178-7)> ',1,,,two,3,,'.replace(/(?<=^|,)(?=,|$)/g, 'NA')
[](#cb178-8)< "NA,1,NA,NA,two,3,NA,NA"
[](#cb178-9)// same thing with negative lookarounds
[](#cb178-10)> ',1,,,two,3,,'.replace(/(?![^,])(?<![^,])/g, 'NA')
[](#cb178-11)< "NA,1,NA,NA,two,3,NA,NA"
[](#cb178-12)
[](#cb178-13)// there is an extra empty string match at end of non-empty columns
[](#cb178-14)> ',cat,tiger'.replace(/[^,]*/g, '{$&}')
[](#cb178-15)< "{},{cat}{},{tiger}{}"
[](#cb178-16)// lookarounds to the rescue
[](#cb178-17)> ',cat,tiger'.replace(/(?<=^|,)[^,]*/g, '{$&}')
[](#cb178-18)< "{},{cat},{tiger}"
```

## Capture groups inside positive lookarounds

Even though lookarounds are not part of matched portions, capture groups can be used inside positive lookarounds. Can you reason out why it won't work for negative lookarounds?

```
[](#cb179-1)> console.log('a b c d e'.replace(/(\S+\s+)(?=(\S+)\s)/g, '$1$2\n'))
[](#cb179-2)< a b
[](#cb179-3)  b c
[](#cb179-4)  c d
[](#cb179-5)  d e
```

## AND conditional with lookarounds

As promised earlier, here's how lookarounds make it simpler to construct AND conditionals.

```
[](#cb180-1)> let words = ['sequoia', 'subtle', 'questionable', 'exhibit', 'equation']
[](#cb180-2)
[](#cb180-3)// words containing 'b' and 'e' and 't' in any order
[](#cb180-4)// same as: /b.*e.*t|b.*t.*e|e.*b.*t|e.*t.*b|t.*b.*e|t.*e.*b/
[](#cb180-5)> words.filter(w => /(?=.*b)(?=.*e).*t/.test(w))
[](#cb180-6)< ["subtle", "questionable", "exhibit"]
[](#cb180-7)
[](#cb180-8)// words containing all vowels in any order
[](#cb180-9)> words.filter(w => /(?=.*a)(?=.*e)(?=.*i)(?=.*o).*u/.test(w))
[](#cb180-10)< ["sequoia", "questionable", "equation"]
[](#cb180-11)
[](#cb180-12)// words containing 'a' and 'q' but not 'n' at the end of the element
[](#cb180-13)> words.filter(w => /(?=.*a)(?=.*q)(?!.*n$)/.test(w))
[](#cb180-14)< ["sequoia", "questionable"]
```

## Variable length lookbehind

In some of the implementations of regular expressions, lookbehind doesn't work if the pattern can match varying number of characters. For example, `(?<=foo\d+)` is looking behind for `foo` followed by one or more of digit characters. As far as I've tested on the console, there's no such restriction in JavaScript. Here's some examples that were tested.

```
[](#cb181-1)// positive lookbehind examples
[](#cb181-2)> '=314not :,2irk ,:3cool =42,error'.match(/(?<=[:=]\d+)[a-z]+/g)
[](#cb181-3)< ["not", "cool"]
[](#cb181-4)// replace only 3rd occurrence of 'cat'
[](#cb181-5)> 'cat scatter cater scat'.replace(/(?<=(cat.*?){2})cat/, 'X')
[](#cb181-6)< "cat scatter Xer scat"
[](#cb181-7)
[](#cb181-8)// negative lookbehind examples
[](#cb181-9)// match only if 'cat' doesn't occur before 'dog'
[](#cb181-10)> /(?<!cat.*)dog/.test('fox,cat,dog,parrot')
[](#cb181-11)< false
[](#cb181-12)// match only if 'parrot' doesn't occur before 'dog'
[](#cb181-13)> /(?<!parrot.*)dog/.test('fox,cat,dog,parrot')
[](#cb181-14)< true
```

## Negated grouping

You've seen a few cases where negated character class was useful than a positive set. For example, in field based processing, it is needed to match the field contents by creating a negated character set of the delimiter character. In a similar manner, there are cases where you need to negate a regexp pattern. This is made possible by using negative lookahead and advancing one character at a time as shown below.

```
[](#cb182-1)// cannot use /at(?<!go)par/ as lookarounds do not consume characters
[](#cb182-2)// match if 'go' is not there between 'at' and 'par'
[](#cb182-3)> /at((?!go).)*par/.test('fox,cat,dog,parrot')
[](#cb182-4)< true
[](#cb182-5)// match if 'do' is not there between 'at' and 'par'
[](#cb182-6)> /at((?!do).)*par/.test('fox,cat,dog,parrot')
[](#cb182-7)< false
[](#cb182-8)
[](#cb182-9)// if it gets confusing, use 'match' method to see the matching portions
[](#cb182-10)> 'fox,cat,dog,parrot'.match(/at((?!go).)*par/)[0]
[](#cb182-11)< "at,dog,par"
[](#cb182-12)> 'at,baz,a2z,bad-zoo'.match(/a((?!\d).)*z/g)
[](#cb182-13)< ["at,baz", "ad-z"]
```

## Cheatsheet and Summary

| Note | Description |
| --- | --- |
| lookarounds | allows to create custom positive/negative assertions |
|  | zero-width like anchors and not part of matching portions |
| `(?!pat)` | negative lookahead assertion |
| `(?<!pat)` | negative lookbehind assertion |
| `(?=pat)` | positive lookahead assertion |
| `(?<=pat)` | positive lookbehind assertion |
|  | variable length lookbehind is allowed |
| `(?!pat1)(?=pat2)` | multiple assertions can be specified next to each other in any order |
|  | as they mark a matching location without consuming characters |
| `((?!pat).)*` | Negates a regexp pattern |

In this chapter, you learnt how to use lookarounds to create custom restrictions and also how to use negated grouping. With this, most of the powerful features of regexp have been covered. The next chapter will give a brief introduction to working with unicode characters.

## Exercises

> ![info](media/file2.svg) Please use lookarounds for solving the following exercises even if you can do it without lookarounds.

**a)** Replace all whole words with `X` unless it is preceded by `(` character.

```
[](#cb183-1)> let ip = '(apple) guava berry) apple (mango) (grape'
[](#cb183-2)
[](#cb183-3)// add your solution here
[](#cb183-4)< "(apple) X X) X (mango) (grape"
```

**b)** Replace all whole words with `X` unless it is followed by `)` character.

```
[](#cb184-1)> let ip = '(apple) guava berry) apple (mango) (grape'
[](#cb184-2)
[](#cb184-3)// add your solution here
[](#cb184-4)< "(apple) X berry) X (mango) (X"
```

**c)** Replace all whole words with `X` unless it is preceded by `(` or followed by `)` characters.

```
[](#cb185-1)> let ip = '(apple) guava berry) apple (mango) (grape'
[](#cb185-2)
[](#cb185-3)// add your solution here
[](#cb185-4)< "(apple) X berry) X (mango) (grape"
```

**d)** Extract all whole words that do not end with `e` or `n`.

```
[](#cb186-1)> let ip = 'at row on urn e note dust n'
[](#cb186-2)
[](#cb186-3)// add your solution here
[](#cb186-4)< ["at", "row", "dust"]
```

**e)** Extract all whole words that do not start with `a` or `d` or `n`.

```
[](#cb187-1)> let ip = 'at row on urn e note dust n'
[](#cb187-2)
[](#cb187-3)// add your solution here
[](#cb187-4)< ["row", "on", "urn", "e"]
```

**f)** Extract all whole words only if they are followed by `:` or `,` or `-`.

```
[](#cb188-1)> let ip = 'poke,on=-=so:ink.to/is(vast)ever-sit'
[](#cb188-2)
[](#cb188-3)// add your solution here
[](#cb188-4)< ["poke", "so", "ever"]
```

**g)** Extract all whole words only if they are preceded by `=` or `/` or `-`.

```
[](#cb189-1)> let ip = 'poke,on=-=so:ink.to/is(vast)ever-sit'
[](#cb189-2)
[](#cb189-3)// add your solution here
[](#cb189-4)< ["so", "is", "sit"]
```

**h)** Extract all whole words only if they are preceded by `=` or `:` and followed by `:` or `.`.

```
[](#cb190-1)> let ip = 'poke,on=-=so:ink.to/is(vast)ever-sit'
[](#cb190-2)
[](#cb190-3)// add your solution here
[](#cb190-4)< ["so", "ink"]
```

**i)** Extract all whole words only if they are preceded by `=` or `:` or `.` or `(` or `-` and not followed by `.` or `/`.

```
[](#cb191-1)> let ip = 'poke,on=-=so:ink.to/is(vast)ever-sit'
[](#cb191-2)
[](#cb191-3)// add your solution here
[](#cb191-4)< ["so", "vast", "sit"]
```

**j)** Remove leading and trailing whitespaces from all the individual fields where `,` is the field separator.

```
[](#cb192-1)> let csv1 = ' comma  ,separated ,values '
[](#cb192-2)> let csv2 = 'good bad,nice  ice  , 42 , ,   stall   small'
[](#cb192-3)
[](#cb192-4)> const trim_whitespace =       // add your solution here
[](#cb192-5)
[](#cb192-6)> csv1.replace(trim_whitespace, '')
[](#cb192-7)< "comma,separated,values"
[](#cb192-8)> csv2.replace(trim_whitespace, '')
[](#cb192-9)< "good bad,nice  ice,42,,stall   small"
```

**k)** Filter all elements that satisfy all of these rules:

*   should have at least two alphabets
*   should have at least 3 digits
*   should have at least one special character among `%` or `*` or `#` or `$`
*   should not end with a whitespace character

```
[](#cb193-1)> let pwds = ['hunter2', 'F2h3u%9', '*X3Yz3.14\t', 'r2_d2_42', 'A $B C1234']
[](#cb193-2)
[](#cb193-3)// add your solution here
[](#cb193-4)< ["F2h3u%9", "A $B C1234"]
```

**l)** For the given string, surround all whole words with `{}` except for whole words `par` and `cat` and `apple`.

```
[](#cb194-1)> let ip = 'part; cat {super} rest_42 par scatter apple spar'
[](#cb194-2)
[](#cb194-3)// add your solution here
[](#cb194-4)< "{part}; cat {{super}} {rest_42} par {scatter} apple {spar}"
```

**m)** Extract integer portion of floating-point numbers for the given string. A number ending with `.` and no further digits should not be considered.

```
[](#cb195-1)> let ip = '12 ab32.4 go 5 2\. 46.42 5'
[](#cb195-2)
[](#cb195-3)// add your solution here
[](#cb195-4)< ["32", "46"]
```

**n)** For the given input strings, extract all overlapping two character sequences.

```
[](#cb196-1)> let s1 = 'apple'
[](#cb196-2)> let s2 = '1.2-3:4'
[](#cb196-3)
[](#cb196-4)> const pat1 =      // add your solution here
[](#cb196-5)
[](#cb196-6)// add your solution here for s1
[](#cb196-7)< ["ap", "pp", "pl", "le"]
[](#cb196-8)// add your solution here for s2
[](#cb196-9)< ["1.", ".2", "2-", "-3", "3:", ":4"]
```

**o)** The given input strings contain fields separated by `:` character. Delete `:` and the last field if there is a digit character anywhere before the last field.

```
[](#cb197-1)> let s1 = '42:cat'
[](#cb197-2)> let s2 = 'twelve:a2b'
[](#cb197-3)> let s3 = 'we:be:he:0:a:b:bother'
[](#cb197-4)
[](#cb197-5)> const pat2 =      // add your solution here
[](#cb197-6)
[](#cb197-7)> s1.replace(pat2, '')
[](#cb197-8)< "42"
[](#cb197-9)> s2.replace(pat2, '')
[](#cb197-10)< "twelve:a2b"
[](#cb197-11)> s3.replace(pat2, '')
[](#cb197-12)< "we:be:he:0:a:b"
```

**p)** Extract all whole words unless they are preceded by `:` or `<=>` or `----` or `#`.

```
[](#cb198-1)> let ip = '::very--at<=>row|in.a_b#b2c=>lion----east'
[](#cb198-2)
[](#cb198-3)// add your solution here
[](#cb198-4)< ["at", "in", "a_b", "lion"]
```

**q)** Match strings if it contains `qty` followed by `price` but not if there is **whitespace** or the string `error` between them.

```
[](#cb199-1)> let str1 = '23,qty,price,42'
[](#cb199-2)> let str2 = 'qty price,oh'
[](#cb199-3)> let str3 = '3.14,qty,6,errors,9,price,3'
[](#cb199-4)> let str4 = '42\nqty-6,apple-56,price-234,error'
[](#cb199-5)> let str5 = '4,price,3.14,qty,4'
[](#cb199-6)
[](#cb199-7)> const neg =       // add your solution here
[](#cb199-8)
[](#cb199-9)> neg.test(str1)
[](#cb199-10)< true
[](#cb199-11)> neg.test(str2)
[](#cb199-12)< false
[](#cb199-13)> neg.test(str3)
[](#cb199-14)< false
[](#cb199-15)> neg.test(str4)
[](#cb199-16)< true
[](#cb199-17)> neg.test(str5)
[](#cb199-18)< false
```

**r)** Can you reason out why the output shown is different for these two regular expressions?

```
[](#cb200-1)> let ip = 'I have 12, he has 2!'
[](#cb200-2)
[](#cb200-3)> ip.replace(/\b..\b/g, '{$&}')
[](#cb200-4)< "{I }have {12}{, }{he} has{ 2}!"
[](#cb200-5)
[](#cb200-6)> ip.replace(/(?<!\w)..(?!\w)/g, '{$&}')
[](#cb200-7)< "I have {12}, {he} has {2!}"
```

**s)** Simulate string partitioning to get an array of three elements — string before separator, portion matched by separator and string after separator. For the first case, split the given input string on first occurrence of digits. For the second case, split based on last occurrence of digits.

```
[](#cb201-1)> let w2 = 'Sample123string42with777numbers'
[](#cb201-2)
[](#cb201-3)// add your solution here for splitting based on first occurrence
[](#cb201-4)< ["Sample", "123", "string42with777numbers"]
[](#cb201-5)
[](#cb201-6)// add your solution here for splitting based on last occurrence
[](#cb201-7)< ["Sample123string42with", "777", "numbers"]
```

**t)** Find the starting index of last occurrence of `is` or `the` or `was` or `to` for the given input strings using `search` method. Assume that there will be at least one match for each input string.

```
[](#cb202-1)> let s1 = 'match after the last newline character'
[](#cb202-2)> let s2 = 'and then you want to test'
[](#cb202-3)> let s3 = 'this is good bye then'
[](#cb202-4)> let s4 = 'who was there to see?'
[](#cb202-5)
[](#cb202-6)> const pat3 =      // add your solution here
[](#cb202-7)
[](#cb202-8)> s1.search(pat3)
[](#cb202-9)< 12
[](#cb202-10)> s2.search(pat3)
[](#cb202-11)< 18
[](#cb202-12)> s3.search(pat3)
[](#cb202-13)< 17
[](#cb202-14)> s4.search(pat3)
[](#cb202-15)< 14
```

# Unicode

So far in the book, all examples were meant for strings made up of ASCII characters only. A few years back that would've been sufficient for most of the use cases. These days it would be rare to encounter ASCII only project. This chapter will briefly discuss unicode matching.

## Unicode character sets and u flag

Similar to escape sequence character sets, the `\p{}` construct offers various predefined sets to work with unicode. For negated sets, use `\P{}`. You'll also need to set the `u` flag.

```
[](#cb203-1)// extract all consecutive letters
[](#cb203-2)> 'fox:αλεπού,eagle:αετός'.match(/\p{L}+/gu)
[](#cb203-3)< ["fox", "αλεπού", "eagle", "αετός"]
[](#cb203-4)
[](#cb203-5)// delete all characters other than letters
[](#cb203-6)> 'φοο12,βτ_4,foo'.replace(/\P{L}+/gu, '')
[](#cb203-7)< "φοοβτfoo"
[](#cb203-8)
[](#cb203-9)// extract whole words not surrounded by punctuation marks
[](#cb203-10)> 'tie. ink east;'.match(/(?<!\p{P})\b\w+\b(?!\p{P})/gu)
[](#cb203-11)< ["ink"]
```

> ![info](media/file2.svg) See [MDN: Unicode property escapes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Unicode_Property_Escapes) for more details and list of `\p{}` sets. See also [regular-expressions: unicode](https://www.regular-expressions.info/unicode.html) for an overview of challenges with unicode matching.

## Codepoints

You can also use codepoints inside `\u{}` construct to specify unicode characters. This is similar to how `\xhh` can be used to specify ASCII characters with two hexadecimal digits.

```
[](#cb204-1)// to get codepoints in hexadecimal from given string
[](#cb204-2)> Array.from('fox:αλεπού', c => c.codePointAt().toString(16))
[](#cb204-3)< ["66", "6f", "78", "3a", "3b1", "3bb", "3b5", "3c0", "3bf", "3cd"]
[](#cb204-4)
[](#cb204-5)// using codepoint to represent a character
[](#cb204-6)> '\u{3b1}'
[](#cb204-7)< "α"
[](#cb204-8)
[](#cb204-9)// character range for lowercase alphabets using \u{}
[](#cb204-10)// note that \u{} will work with 'u' flag only
[](#cb204-11)> 'fox:αλεπού,eagle:αετός'.match(/[\u{61}-\u{7a}]+/gu)
[](#cb204-12)< ["fox", "eagle"]
```

> ![info](media/file2.svg) See also [stackoverflow: Unicode string to hex](https://stackoverflow.com/questions/21647928/javascript-unicode-string-to-hex).

## Cheatsheet and Summary

| Note | Description |
| --- | --- |
| `u` | flag to enable unicode matching |
| `\p{}` | Unicode character sets |
| `\P{}` | negated unicode character sets |
|  | see [MDN: Unicode property escapes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions/Unicode_Property_Escapes) for details |
| `\u{}` | specify unicode characters using codepoints |

A comprehensive discussion on regexp usage with Unicode characters is out of scope for this book. Resources like [regular-expressions: unicode](https://www.regular-expressions.info/unicode.html) and [Programmers introduction to Unicode](http://reedbeta.com/blog/programmers-intro-to-unicode/) are recommended for further study.

## Exercises

**a)** Check if given input strings are made up of ASCII characters only. Consider the input to be non-empty strings and any character that isn't part of 7-bit ASCII set should result in `false` as output.

```
[](#cb205-1)> let str1 = '123 × 456'
[](#cb205-2)> let str2 = 'good fοοd'
[](#cb205-3)> let str3 = 'happy learning!'
[](#cb205-4)
[](#cb205-5)> const pat1 =      // add your solution here
[](#cb205-6)
[](#cb205-7)> pat1.test(str1)
[](#cb205-8)< false
[](#cb205-9)> pat1.test(str2)
[](#cb205-10)< false
[](#cb205-11)> pat1.test(str3)
[](#cb205-12)< true
```

**b)** Retain only punctuation characters for the given string.

```
[](#cb206-1)> let ip = '❨a❩❪1❫❬b❭❮2❯❰c❱❲3❳❴xyz❵⟅123⟆⟦⟧⟨like⟩⟪3.14⟫'
[](#cb206-2)
[](#cb206-3)// add your solution here
[](#cb206-4)< "❨❩❪❫❬❭❮❯❰❱❲❳❴❵⟅⟆⟦⟧⟨⟩⟪.⟫"
```

**c)** Is the following code snippet showing the correct output?

```
[](#cb207-1)> 'fox:αλεπού'.match(/\w+/g)
[](#cb207-2)< ["fox"]
```

# Further Reading

Note that some of these resources are not specific to JavaScript, so use them with caution and check if they apply to JavaScript's syntax and features.

*   [regex101](https://regex101.com/) and [regexr](https://regexr.com/) — visual aid and online testing tool for regular expressions, select flavor as JavaScript before use
*   [regulex](https://jex.im/regulex) and [debuggex](https://www.debuggex.com/) — for visualization of regexp as rail road diagrams
*   [XRegExp](https://github.com/slevithan/xregexp) — utility with features like metacharacter escaping, recursive matching, etc
*   [JSVerbalExpressions](https://github.com/VerbalExpressions/JSVerbalExpressions) — construct regexp with natural language terms
*   [CommonRegexJS](https://github.com/talyssonoc/CommonRegexJS) — collection of common regular expressions
*   [Awesome Regex](https://github.com/aloisdg/awesome-regex) — curated collection of libraries, tools, frameworks and software
*   [randexp.js](https://github.com/fent/randexp.js) — Generate strings that match a given regular expression
*   [stackoverflow: JavaScript regexp](https://stackoverflow.com/questions/tagged/javascript+regex?sort=votes&pageSize=15)
*   [stackoverflow: regex FAQ](https://stackoverflow.com/questions/22937618/reference-what-does-this-regex-mean)
    *   [stackoverflow: regex tag](https://stackoverflow.com/questions/tagged/regex) is a good source of exercise questions
*   [rexegg](https://www.rexegg.com/) — tutorials, tricks and more
*   [regular-expressions](https://www.regular-expressions.info/) — tutorials and tools
*   [regexcrossword](https://regexcrossword.com/) — tutorials and puzzles
*   [swtch](https://swtch.com/~rsc/regexp/regexp1.html) — stuff about regular expression implementation engines
*   [news.ycombinator: collection of regexp related resources](https://news.ycombinator.com/item?id=20614847)

Here's some links for specific topics:

*   [rexegg: best regex trick](https://www.rexegg.com/regex-best-trick.html)
*   [regular-expressions: matching numeric ranges](https://www.regular-expressions.info/numericranges.html)
*   [regular-expressions: Zero-Length Matches](https://www.regular-expressions.info/zerolength.html)
*   [stackoverflow: Greedy vs Reluctant vs Possessive Quantifiers](https://stackoverflow.com/questions/5319840/greedy-vs-reluctant-vs-possessive-quantifiers)
*   [cloudflare: Details of the Cloudflare outage on July 2, 2019](https://blog.cloudflare.com/details-of-the-cloudflare-outage-on-july-2-2019/) — see appendix for details about CPU exhaustion caused due to regular expression backtracking