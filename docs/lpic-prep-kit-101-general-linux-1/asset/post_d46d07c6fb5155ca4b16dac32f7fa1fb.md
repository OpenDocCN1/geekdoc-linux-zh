
Chapter 10, “Administrative Tasks,” provides an introduction to basic system administration.

Chapter 11, “Backup and Restore,” outlines how to plan for disaster recovery and discusses the more common utilities.

- Appendix A, “Glossary,” provides definitions of terms presented in this book.
- Appendix B, “Certification Process,” discusses the road to LPI certification.
- Appendix C, “Testing Tips,” presents some hints to help you be successful on your exams.
- Appendix D, “Alternate Resources,” lists other places to go for information.
- Appendix E, “Using the CD-ROM,” explains how to use the CD-ROM that comes with this book.
- Appendix F, “Lab Exercises,” is a comprehensive test for you to use to gauge your readiness for this exam.
- Appendix G, “Objectives Index,” includes a list of LPIC Test 101 objectives and a discussion of each objective.

Even if you feel comfortable with the material covered in a specific chapter, please be sure to review that chapter before proceeding to the next one. Because each chapter builds on the preceding ones, you'll want to have a firm grasp of the foundation chapter before moving on.

A bonus that you received when you purchased this book is the tear-out booklet. This booklet contains a brief synopsis of each chapter covering the most important points. Use it in conjunction with the prerequisites at the beginning of each chapter to ensure you understand the foundation chapters before proceeding.

You also can use the tear-out booklet for your review before taking the final test at the end of the book. In addition, you can take the tear-out booklet with you the day of your exam to review in the parking lot right before your test.

Each chapter begins with a series of “While You Read” questions that test your preconceptions of how chapter topics are put to task in an administrative environment. To gauge your own learning curve, write down your answers before moving on to the rest of the chapter. While you read the chapter, refer to your answers and revise them as necessary. The answers are provided at the end of the chapter.

A collection of Practice Test questions also appears at the end of each chapter. Both the correct and incorrect answers are explained in an effort to optimize the benefits you get from this practice test. After completing the end-of-chapter test, review the answers to see how well you did. Not doing this is only cheating yourself.

If you find that you have missed several of the end-of-chapter questions, go back and review that chapter before proceeding to the next chapter. If you still are unclear about a concept, try another resource such as the Linux Documentation Project or any of the other resources listed in Appendix D.

## Preparing to Test

This exam is intended for the individual who has experience with Linux. You need to have a Linux system available that you can use. Practice each of the concepts covered in this book until you are comfortable with them.

To get the most from this book, you should start with Chapter 1 and complete each chapter in the order in which they are presented. When starting a chapter, the first thing you should do is to read the prerequisites. If you don't feel you have a good grasp of these principles, go back and review before proceeding.

Next, read the “While You Read” questions and write down your answers. You also might want to make note of any other questions that come to mind. After you have finished reading the chapter, look over the answers. Make sure you understand why the answers are correct.

The next thing you will want to do is any associated lab exercise. These are designed to reinforce the didactic material you have read. The hands-on experience will be invaluable when you are sitting there taking the exam.

The last thing you should do is answer the end-of-chapter questions. Write down your answer to each question before checking it. If you miss any, review the rationale for each possible answer. You also should review the appropriate section in the chapter. If you still are unclear, consult Appendix D for other places that will provide additional explanations. While you are studying for your first exam, take the tear-out booklet with you wherever you go. It is designed to be portable. You can use it to review whenever you have a few minutes, such as when standing in line, waiting at the auto repair shop, and any other time you are stuck with a few minutes to fill.

After you have completed the book and the end-of-book test, you will want to use the practice test engine provided on the CD-ROM that accompanies this book. Enough questions are provided for four completely different tests, although by using the randomizing feature, you'll get a "new" test every time you sit down. This is excellent experience to get you ready for the real thing. See Appendix E for information on how to use the test engine.

The test will contain questions that require you to evaluate and diagnose the situation. The answer you choose will be the result of this evaluation. It is in this situation that the hands-on experience you get from the exercises in Appendix F and your own experience will be invaluable.

Study well and best of luck on your certification endeavor!

## CHAPTER PREREQUISITE

Before beginning this chapter you should have access to a computer running Linux that you can use to practice these concepts and skills. You should be able to log on to your system and understand the basics of typing at the command line.

# Finding and Creating Documentation

## WHILE YOU READ

1. You ask a co-worker how to locate a file on your Linux system and he tells you to check the man pages for find and locate. What does he mean by the term man?
2. You are looking at the man page about using tar to find the option to compress the tar file. How can you find it without having to read the entire page?
3. Why does using man command not find the correct manual page?
4. How can you configure your computer to make Spanish the default language for manual pages?
5. Where can you find information on setting up your new zip drive?
6. What is the Linux Documentation Project?
7. You find a file in /usr/bin but do not know what it does. How can you find this out?
8. How do you find the exact name of the command to change your password?

## Getting Help

Usually there is no hard copy manual supplied with Linux unless you purchase a distribution that includes a manual. However, there is an almost unlimited amount of information available from many sources. These may be categorized as

- Local documentation
- Online via the Internet
- Newsgroups
- Mailing lists
- Books

The ability to find and use this documentation will be tested on the exam.

### Local Documentation

There are several types of locally installed documentation. Table 1.1 shows the types and their locations.

**Table 1.1** Installed Documentation and Their Locations

| Documentation | Location |
| :--- | :--- |
| manual pages | /usr/man |
| info | /usr/info |
| HOWTOs | /usr/doc/HOWTO |
| Frequently Asked Questions (FAQ) | /usr/doc/FAQ |
| program documentation | /usr/doc/<program name> |

Each one of these has its advantages and disadvantages. Usually information on the same topic can be found in more than one source. However, one source may be easier for you to understand than the other.

#### man Pages

There is extensive local online help available on almost every utility, system call, or command on your system called the *manual pages*. The manual pages are not user-friendly and are more helpful for looking up syntax than using as a tutorial.

They are frequently referred to as man pages and are invoked using the man utility. man searches for a man page on a specified topic and sends the output through a pager. The pager then prints the man page to your display. How you navigate through the man page is dependent on which pager is being used.

The syntax for man is

```
man [options] [section] [topic]
```

You invoke a man page by passing the topic to the man command. If you type man man the manual page describing how the manual pages work is displayed. If you are looking for information on the command who, you could get it by typing man who. The displayed man page will present a summary of what the who command does and its syntax.

Each man page is divided into sections, although not all sections appear in every page. Table 1.2 lists the sections and what they might contain.

**Table 1.2** Sections of man Pages

| Section | Description |
|---------|-------------|
| NAME | The name and a brief description of the command |
| SYNOPSIS | How to use the command and its command-line options |
| DESCRIPTION | Explanation of the program and its options |
| OPTIONS | All options with a brief description of each |
| SEE ALSO | Related man pages |
| DIAGNOSTICS | Description of error messages |
| FILES | List of files used by the command and their locations |
| BUGS | Known problems |
| HISTORY | Milestones of program's development |
| AUTHOR | Program's author and contributors |

Not only are the individual manual pages internally organized into sections, the pages themselves are arranged in a specific directory structure. Table 1.3 lists the names of these directories and what type of man pages each contains. This is information you may need to know for the exam.
