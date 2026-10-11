
## Taking the Test

### Enumeration of Facts

The easiest questions to answer are those that fall into the enumeration of facts category. These questions simply test your memorization. In this type of question, you might be asked to supply a specific term or define a term. You might be asked a question such as “What are the types of partitions?”

Extraneous material might even be supplied in the question itself. However, if you read each question and identify what information is wanted, it should be obvious what the correct answer is. For example, you might have a question that gives you a list of all the hardware on a computer as well as what is on the hard drive, but the question actually wants to know if another primary partition can be created.

### Understanding the Concept

A more difficult type of question for most individuals to answer is the one that asks for a concept instead of discrete facts. Let’s use our previous example of partitioning. A question testing the concept of partitioning might be looking for evidence that you understand the concept of the types of partitions that can be created on any single hard disk.

So, you might have a question that gives extensive information on the hardware configuration of your computer but is actually attempting to ascertain whether you understand the limitations on the number and types of partitions you can have on a single hard disk.

### Applying the Concept

The third, and hardest, type of question tries to determine whether you can take a concept and apply it in real life. Instead of asking you what types of partitions you can create, the question might present a scenario in which you must identify that the problem relates to partition creation and then decide how to correct it.

Using the same example, your question might be that you have free space you want to use for a new database application, but the operation fails. Your answer would be based on identifying why you can’t create the partition and how to correct it.

When reading each question, you will want to identify the type of question it is. This will go a long way toward being able to select the correct response.

You also should try to identify the objective that is being tested. If the question is intended to gauge your abilities in using text filters, the answer will not be one that has to do with the directory structure.

If the question is scenario-based, you will be presented with a situation and have to select the answer that best solves the problem. Some candidates become overwhelmed when faced with scenarios, but scenarios really are not that hard.

### Reviewing Marked Questions

Once again, you want to use that writing material. As you read the scenario, take notes on the facts presented; you can expect to be given more information than is necessary to answer the question. Writing down each item makes it easier to pick out the salient points and ignore the rest.

Still having trouble with the scenario? Try approaching it from the other direction. Forget the answers given. Instead, think about what you would do in a similar situation. Oftentimes if you use this method, you will find that the question is really not that hard.

After you have read all the questions and answered them, go back and review those questions you have marked. When you go through the question for the second time, you can take more time. Analyze the question and pick out the most important points. What is the objective of the question? What information is provided that is not relevant to answering it?

When reading the questions, remember not to read anything into them. Rather, take each question at face value. Don't assume anything that is not explicitly mentioned in the question itself.

Remember, the people who write the questions are not trying to trick you; they're just trying to provide an objective measurement of your skills in relation to the exam's stated objectives.

## Alternate Resources

Hundreds of resources exist online for information about and help with Linux. A few are listed here to get you started—you'll surely discover more as you surf the Net.

### Support Sites

- CNET.com—Linux: `http://linux.cnet.com/linux`
- Filesystem Hierarchy Standard: `http://www.pathname.com/fhs/`
- Linux Fool Dot Com: `http://www.linuxfool.com/`
- Partition types: `http://www.win.tue.nl/~aeb/partitions/partition_types-1.html`
- Planet IT Linux Technology Center: `http://www.planetii.com/techcenters/linux`
- System Administrator's Guide: `http://members.xoom.com/basiclinux/sag/book1.html`
- TechRepublic: `http://techrepublic.com/trbbs/trbbs.jhtml`

### Documentation

- Linux Documentation Project: `http://metalab.unc.edu/LDP/`
- Linux Knowledge Base Org.: `http://www.linuxkb.org/`
- Linux.com—HOWTOs: `http://linux.com/howto/`

### Software Sites

- Bash prompts: `http://bash.current.nu/`
- Freshmeat: `http://freshmeat.net`
- FtpFind: `http://www.ftpfind.com/`
- Linux RPM search: `http://www.whichrpm.com/`
- Linux software: `http://linux.tucows.com`

### Linux News

- Linux Gazette: `http://www.linuxgazette.com/`
- Slashdot: `http://www.slashdot.org/`

### Humor

- Humorix—All Linux Humor: `http://i-want-a-website.com/about-linux/`
- User Friendly the Comic Strip: `http://www.userfriendly.org/`

### Tutorials

- Basic Linux: `http://basiclinux.hypemart.net`
- Linux OpenContent Stuff: `http://w3.one.net/~johnb/linux/`

### Miscellaneous

- Linux User Groups WorldWide: `http://lugww.counter.li.org/`
- LPI—Getting Certified: `http://www.lpi.org/`
- Linus Torvalds: `http://www.cs.helsinki.fi/~torvalds/`
- The EZLinux Command Card: `http://www.csxtech.com/aff.pl?page=downloads/command/index.html&aff_id=0`

## Using the CD-ROM

The CD-ROM accompanying this book contains 250 questions that comprise the practice tests covering the material you have studied. These questions should be used when you have finished the book and think you are ready to take the exam.

All the questions presented here are multiple choice or short answers. When typing in your answers, use lowercase unless a command requires uppercase. These are the same types of questions you will see on the exam.

## Equipment Requirements

To use the Self-Tests, you must have an Intel-based computer running the Linux operating system. The distribution does not matter. The test is designed to run under the command-line interface; therefore, it is not guaranteed to run correctly in a terminal window under X.

## Installing the Self-Test Software

Installation consists of creating a directory and copying the appropriate files from the CD-ROM to this directory. The steps to do this are as follows:

1. Create a directory to contain the testing files. Usually, this should be a subdirectory of your home directory.
2. Copy the following files into this directory:
   - `1pic`
   - `test`
3. While this directory is your working directory, first use the `su` command to become root and then change the ownership of these files by issuing the following command:
   `chown <your_name> *`
4. Type `exit` to quit being root. Change the `1pic` file to be executable by issuing the following command:
   `chmod a+x lpic`
5. Verify that you have the permission to read the test file by using the `ls -1` command. If you need to change it then issue this command:
   `chmod a+r test`

## Running the Self-Test Software

To run the Self-Test Software, make the directory containing the files your working directory and then type:

```
./lpic
```

When you start the test, you will be presented with a screen in which you can select which test you want to take. Tests 1–5 each randomly present 50 questions from a static pool of questions. After you finish all five tests, you will have seen all the questions. Test 6 presents you with 50 questions randomly selected from all the questions. This will be very similar to taking the real exam.

Make sure your Caps Lock key is *not* on while taking this test. All answers are case sensitive, so your answer might be scored as incorrect if you use capital letters.

During the test, you can quit at any time by typing the letter q and pressing Enter. You then will be given the chance to score your test or quit.

To answer a question, type your answer and then press Enter to proceed to the next question. If you want to come back to this question later, type the letter U and press Enter. (Notice that it must be a capital U.)

## Scoring Your Test

When you finish a test, you will be presented with your overall score. In addition, your score will be broken down according to objectives. You should use this information as a guide to further study.
