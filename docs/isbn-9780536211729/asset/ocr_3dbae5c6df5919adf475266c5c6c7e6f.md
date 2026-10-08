So what did the crackers do to the system? They ran an IRC 'bot, left a few files under .mh, which had not existed previously, and in /tmp, and left the system undamaged.

# B.6 Ken Thompson Cracks the Navy

The U.S. Navy has a postgraduate school in beautiful Monterey, California. They're not just a bunch of beach bums, though. There is serious research going on, including some in Computer Science. One of the areas of research was computer security and they spent considerable time modifying UNIX to be more secure. Naturally, the military is very concerned about security and these guys were sharp. When they were ready, they contacted Ken Thompson, the co-inventor of UNIX, and proudly invited him to try to break in. He took them up on the invitation. Some weeks later Ken demonstrated that he was “in” as root. Put yourself in the place of the sailors and think of possible types of exploits.

> What Ken did was to modify the C compiler to recognize a particular code pattern in the source of the login program. He then sent an “update tape” that included this Trojan horse and waited for the Navy to recompile the system. Receiving update tapes from Bell Labs was routine, as was periodically recompiling the system.

Although I do not know, they might have studied the source on the update tape and might even have run diff on it. Compiler code is notoriously complex and they may not have been able to tell that the change was other than a bug fix. At some point, Ken got even more devious. Although an expert in compiler construction could have found this problem, consider his next demonstration.

Recall that Ken had modified the C compiler to deliberately miscompile the login program to plant a Trojan. He then added a second Trojan to the C compiler that added both this first Trojan and this new second Trojan to the compiled binary of the C compiler even if the source did not contain these two Trojans. Thus, after this second version of the C compiler was built, the two Trojans could be removed from the source to the C compiler. Now, all subsequent versions of the C compiler would have this Trojan even though the source of the C compiler (and login) contained no Trojans.

The only way to detect this Trojan is to disassemble the compiled C compiler and spot the Trojan in the binary, a virtually impossible task. Ken discussed this exploit in his very famous ACM Turing Award lecture, “Reflections on Trusting Trust.”¹

1. *Communication of the ACM*, Vol. 27, No. 8, August 1984, pp. 761–763. ACM is the Association for Computing Machinery. A copy of the lecture may be read from *www.acm.org/classics/sep95*.