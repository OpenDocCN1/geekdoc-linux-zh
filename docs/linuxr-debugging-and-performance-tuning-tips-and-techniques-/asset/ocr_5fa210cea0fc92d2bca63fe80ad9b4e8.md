+   11.8 Crossing a Security Minefield: Setuid root 422
+   11.9 Suggested Reading 423
+   11.10 Summary 424

+   Exercises 426

# Chapter 12 General Library Interfaces - Part 2 427

+   12.1 Assertion Statements: assert() 428
+   12.2 Low-Level Memory: The memXXX() Functions 432
+       12.2.1 Setting Memory: memset() 432
+       12.2.2 Copying Memory: memcpy(), memmove(), and memccpy() 433
+       12.2.3 Comparing Memory Blocks: memcmp() 434
+       12.2.4 Searching for a Byte Value: memchr() 435

+   12.3 Temporary Files 436
+       12.3.1 Generating Temporary Filenames (Bad) 437
+       12.3.2 Creating and Opening Temporary Files (Good) 441
+       12.3.3 Using the TMPDIR Environment Variable 443

+   12.4 Committing Suicide: abort() 445
+   12.5 Nonlocal Gotos 446
+       12.5.1 Using Standard Functions: setjmp() and longjmp() 447
+       12.5.2 Handling Signal Masks: sigsetjmp() and siglongjmp() 449
+       12.5.3 Observing Important Caveats 450

+   12.6 Pseudorandom Numbers 454
+       12.6.1 Standard C: rand() and srand() 455
+       12.6.2 POSIX Functions: random() and srandom() 457
+       12.6.3 The /dev/random and /dev/urandom Special Files 460

+   12.7 Metacharacter Expansions 461
+       12.7.1 Simple Pattern Matching: fnmatch() 462
+       12.7.2 Filename Expansion: glob() and globfree() 464
+       12.7.3 Shell Word Expansion: wordexp() and wordfree() 470

+   12.8 Regular Expressions 471
+   12.9 Suggested Reading 480
+   12.10 Summary 481
+   Exercises 482