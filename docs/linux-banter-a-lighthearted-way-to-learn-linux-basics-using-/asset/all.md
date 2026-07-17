![](image_rsrc81Z.jpg)

![](image_rsrc820.jpg)​LINUX BANTER

Linux® is the registered trademark of Linus Torvalds in the US. and other countries.

All characters are fictitious. Any resemblance to any person living or dead is merely coincidental.

The GNU General Public License

The source code in the book is made available under the terms of the GNU General Public License version 3, http://www.gnu.org/licenses/gpl-3.0.en.html

Disclaimer :

Some of the source code that are machine dependant might or might not work in some machines. All the code has been tested on our computers and we haven’t noticed anything that can harm the system. However, we are not responsible for any damages that misuse of these programs can cause to your system.

Who this book is for:

It is a book for those interested in getting a bird’s eye view of Linux technicalities and what can be done vis a vis Linux  system calls and some C library functions. This book outlines the tools that can be used to write programs and what the Linux system offers a casual reader. Please note that this book is intended to make light reading compatible with learning some Linux basics. This is not a book for Linux administration and it does not impart knowledge on installation of Linux.

We also urge you to use this powerful system called the computer, built upon decades of hard work by dedicated people, making it an epitome as well as a stable base for the progress of our civilization, responsibly and with confidence. Programming has immense potential and it definitely can be used to usher in positive changes in the world. Hope you have fun going through this course. This content outlines the various ways a programming language can be used to program a system. There are utilities as well. The approach that can be learned from this can be extended to understand other programming languages as well. Of course, it is impossible to cover all aspects of the Linux system in this, because of the sheer volume of programs and efficient contributions from around the world. But it provides a base from which the reader can get her feet wet.

Requisites :

You need a Linux system with the GNU C Compiler installed and an elementary knowledge of C.

| Index | Page |
| Introduction | 4 |
| Shell scripting | 51 |
| The C Compiler | 83 |
| Files and Directories | 89 |
| Memory and command line arguments | 126 |
| Time related calls. | 142 |
| Temporary files | 146 |
| User ids and groups | 147 |
| Resources and limits | 154 |
| DATA MANAGEMENT | 157 |
| File Locking | 161 |
| Databases | 169 |
| Processes | 172 |
| Signals | 184 |
| Threads and mutex | 193 |
| Interprocess Communication Pipes | 216 |
| IPC :  Semaphores | 232 |
| IPC :  Shared Memory | 242 |
| IPC :  Message Queues | 248 |
| Sockets | 256 |
| Epilogue | 286 |
|  |  |

It also talks about the anecdotes of Lingaraj who proceeds to teach Linux to Seema, a geology expert who wants to learn. The book uses analogies to present various concepts and the reader is requested not to assume that the analogies are an exact parallel.

Linux Banter

Copyright : Author. Except source code and technical matter.

Published by : Purple Prose, Bangalore, India. Purple Prose is a registered trademark in India.

For any queries : info@purpleprose.in

Written by Sathyajit

Illustrations by : Nishant Khare

Year first published : 2022

​Linux Banter

Introduction

![](image_rsrc821.jpg)

It was a day of spring and everybody on the streets moved admiring the flowers in a good mood. But that did not rub off on Seema who was walking with anxiety towards the hospital. Seema was 26, tall and prone to be flustered with technology and was horrible at remembering passwords. The hospital had good ![](image_rsrc822.jpg)doctors and that was what mattered to most of the patients. 

Seema walked because her fiance, Vijay was lying on one of the beds. She was informed about Vijay’s accident and she had rushed. She spoke at the reception desk who directed her to the special ward on the first floor. She ran up the stairs and saw Vijay sleeping on the bed with a bandage around his head.

![](image_rsrc823.jpg)

Vijay was a young man of 30 and was an interior designer. Seema, being a geography expert had met Vijay about a year ago when he had shown up at the consultancy office she ran, to design it. They had the same taste and things had taken a turn for the good. Until this incident. Seema looked at Vijay and wished she could help him in some way. Then she went to see the doctor.

![](image_rsrc824.jpg)

The doctor was a gregarious man in his forties and was particular about making his patients and their families at ease.

“He has a mild concussion. A laptop fell on his head while he was travelling in the train. The software installed in the laptop cushioned the fall.” said the doctor.

He started to laugh at his joke.

“I hope he will be alright.” said a concerned Seema.

![](image_rsrc825.jpg)

It was then that Vijay walked in with a keyboard in his hand.

![](image_rsrc826.jpg)Both Seema and the doctor were taken aback. But the doctor, hospitable as ever, asked.

“Would you like some coffee, Vijay?”

![](image_rsrc827.jpg)

“I don’t drink coffee. It might damage my central processing unit made of silicon.” replied Vijay.

Seema and the doctor were taken aback again.

“Vijay, are you alright?” she asked with some concern.

![](image_rsrc828.jpg)

“As alright as a write command writing a byte.” said Vijay.

“Let’s go.” Seema said.

“If you have a command, please type it into this keyboard.” said Vijay.

![](image_rsrc829.jpg)

Then Vijay handed over the keyboard.

“It’s connected to me via a network.” he said.

Seema was beginning to get alarmed. With shaky hands she took the keyboard and typed.

![](image_rsrc82A.jpg)

“…..lllets go”

“I don’t understand that command.” announced Vijay.

Seema then turned to the doctor.

![](image_rsrc82B.jpg)

“What is happening?” she asked him.

“I think he’s imbibed machine consciousness. Maybe a suppressed desire from his childhood to be a robot, what with all the films glorifying it.”

“Vijay, you will be all right.” she said trying to sound convincing.

“Do you know a cure for it?” she asked the doctor.

![](image_rsrc82C.jpg)

“There is this community near the Dandeli forest. There is a doctor.”

“A neurosurgeon?”

“No, a crocodile doctor. At least he calls himself that.”

Seema was wondering whether all this was a dream.

“He is a Linux programming expert. Maybe he will teach you to communicate with Vijay as a computer and get him to revert to humanity.” continued the doctor.

“His name?”

“His name is Lingaraj.”

![](image_rsrc82D.jpg)

Seema booked a cab and was on her way to Dandeli. As she started her journey from Bengaluru, she was quite tense. The driver tried to make small talk, but she was too anxious.

![](image_rsrc82E.jpg)

After the car had gone past Tumkur, there were agricultural fields on either side of the road. The driver switched on some sad songs about love sensing the mood. The driver was sensitive to his passengers’ moods and feelings and had quite a good collection of music.

![](image_rsrc82F.jpg)

As they neared Dandeli, Seema could discern the change in climate and the sparsity of the population gave her a sense of calm.

![](image_rsrc82G.jpg)

Lingaraj’s community, were a group of people who had taken lands near the forest and had maintained themselves sustainably. The community of around 2000, which had lived there for generations had access to technology and there were a lot of academics and scholars in there.  

Seema’s car reached the location which Lingaraj had sent. It had to be accessed via a mud road, passing over old bridges. They had passed waterfalls and climbed up and down mountains.

![](image_rsrc82H.jpg)

The cab driver had switched off his music system allowing Seema to listen to the sounds of unexploited nature. 

![](image_rsrc82J.jpg)![](image_rsrc82K.jpg)

They reached the place and as the driver switched off the engine, a solitary man of around 28 came dressed wearing a T-shirt that had the words, “Legendary is overrated.”

![](image_rsrc82M.jpg)

Seema was relieved to see him because it was getting dark and there was no one around.

“You are Lingaraj, I presume. I am Seema.” Seema introduced herself.

“Yes.” replied Lingaraj.

![](image_rsrc82N.jpg)

“My fiance Vijay has imbibed machine consciousness. I came to you for help.”

“Yes, the doctor told me. And we thought the problem one day would be machines imbibing human consciousness.”

“So, when do we start?”

“Well, you both have had a tough journey. Rest and we shall start tomorrow.”

“I will go back to Bengaluru, Sir” said the driver.

![](image_rsrc82P.jpg)

“Nobody is going to know where you will go if you leave from here, least of all, yourself. Do as I say. Have a nice dinner here and go back tomorrow.” said Lingaraj.

The cab driver agreed.

Lingaraj asked them to park the car and they walked towards their camp.

![](image_rsrc82R.jpg)

Their camp was set in a large clearing and they had built eco-friendly houses for themselves. Some houses were in groups and some were set apart from the rest. Seema was shown into her private house and the driver was shown Lingaraj’s house.

![](image_rsrc82S.jpg)

Seema freshened up and sat on the porch outside. The atmosphere was very serene and crickets stridulated. There were a lot of birds chirping and she was lost in it for a while.

![](image_rsrc82T.jpg)

Then, Lingaraj and Manjunath came to where she was. Lingaraj offered her dinner made of sprouts and some healthy sandwiches. Seema tried to bring up the issue of Vijay, but Lingaraj was busy telling jokes to the cab driver Manjunath.

![](image_rsrc82U.jpg)

After they had finished, Lingaraj told her classes would start the next day at 9.

Seema went to her home and slept immediately. She dreamt of Vijay and she taking a walk in the forests.

![](image_rsrc82V.jpg)

The next day, Seema woke up and went to Lingaraj’s house. The driver had already left by then. Lingaraj then showed her a box full of supplies for food and asked Seema to take them to her house in the evening, after the class. She could notice millets and fruits with small mud containers with masalas in them. Then Lingaraj led her to the computer in his hall.

![](image_rsrc82W.jpg)

Seema had not met anyone apart from Lingaraj during the whole time and asked him about it. Lingaraj said most of the people had gone on a trek.

![](image_rsrc82X.jpg)

“Let’s begin.” said Lingaraj. “You need to be able to talk to the machine. Now, talk to this machine.” said Lingaraj showing his laptop which was being charged. It had many cables sticking out of it.

![](image_rsrc82Y.jpg)

“Hi computer, will you be friends with me?” said Seema.

“That won’t work.”

Seema thought a lot. Then she took out her hairband, loosened her hair and promptly proceeded to join her hair with the computer wires.

![](image_rsrc82Z.jpg)

“That won’t work too. If it worked, people would queue up outside ATMs and plead with the ATM to understand their plight and give them money.” said Lingaraj.

“Then what do I do? I am not a software engineer, I am a geography expert.” said Seema with desperation.

“You need to understand the system first. Then write programs to change the system or utilise it.”

“There are primarily two ways to interact with this system, which is a Linux system. Shell programming and using a programming language. To make a program you need proficiency in a programming language like C. And to get the program to make sense to the system, you need a compiler. About C basics, you will learn parallelly on your own, but before that, we need to see what the system can offer.”

“This system is a Linux system. Linux is a kernel and it’s being added to as we speak. A man called Linus Torvalds took the initiative to make software embody free spiritedness. He wrote the core of the Operating system. And Linux with contributions from all over the world is growing.” continued Lingaraj.

![](image_rsrc830.jpg)

“To work with the system you need to log in. For which you need access.” he said further.

“Okay. Vijay recognises me, so I have access.”

“Yes, he has imbibed machine consciousness. You sure you want to change him back?”

“He was so perfect. He used to satisfy my every whim. Got me flowers everyday. Used to sing for me. He always took my side in arguments.”

“Are you sure he’s not acting like a machine now.”

“What?”

“None of my business. Anyway, once you get into the system you can use it. You can make it do tasks and execute your commands. So whether he reverts or not, it’s a win win situation for you.”

“Please stick to teaching me.”

“Just kidding. There are many distributions of Linux available, called flavours.

To use a system, you need to program it as well. You can use C, C++, Java, Python etc. to program. What language did you use to talk in with Vijay?”

“English, Hindi, Kannada and Tamil. But I can learn C. Goes with my name, Seema.”

“If only it were so easy.”

Seema was at a loss about what to make of this person. She was alone near a jungle with this guy and she wondered whether he was trying to deliberately insult her or he was built like that.

“The kernel is the thing that does everything. The outer interface is called the shell. The shell is how you talk to the kernel.”

Then Lingaraj looked away.

“I will tell you a story. My story. I have lived both in the city as well as here. I worked as a chef in a hotel once near Banashankari in Bengaluru. I used to cook well but the owner sitting at the cash counter got all the credit.

![](image_rsrc831.jpg)

Nobody came to see me at the back where I was working. I had become a bit of a loner. I had decided to quit and that very evening, this guy  came running into the kitchen.

![](image_rsrc832.jpg)

I was so happy, I thought he had come to see me and tell me how great the food was. I asked him,

‘Are you here to congratulate me?’

‘No, somebody’s  chasing me, I came to escape through the kitchen like they do in movies.’ he said.” said Lingaraj.

“So you are saying the kernel does not get the credit it deserves?” asked ![](image_rsrc833.jpg)Seema.

“Not at all. I am saying how lonely people can become.”

He continued. “Anyway, this shell is called bash. This shell was written in C. The makers thought of all the various utilities you might generally need and bundled them up in the shell. I will give you the hotel example. A hotel has many ready made dishes and you can order anything. For example, a chocolate shake. This is like a program already installed. But if you want a special something like spicy noodles with sweet dates chutney, you need to tell the cooking team how it’s made. So, what’s already available in the system like a chocolate shake is akin to the programs already installed, like the ‘cat’ command, etc. Noodles with sweet dates chutney, you have to use C and program yourself. So, inbuilt programs are what is on the menu. Programming yourself is what isn’t already on the menu.

We use the Bourne again shell. Also called bash.

Let me login with my credentials.”

On the computer screen, it showed:

| $ |

“This is the command prompt, the dollar symbol.” explained Lingaraj.

Lingaraj typed ‘root’ and when prompted for a password, he typed it.  He took a long time typing it. His password was ‘LivingLegendLingaraj’.

| $ root |

“What’s root? Which plant root are you talking about?” asked Seema.

“Root is the superuser. He has complete access to the system. He can do anything to the system which others can’t. Except probably breaking the computer in frustration.”

Seema suddenly became wary.

“Have you...you ever broken a computer in frustration?”

“Yes.”

Seema was now worried.

“But it was for a film shoot. Now, we are at the command prompt, the ‘$’. I will type

| $ ls -al |

What do you think the system will do?”

“ls…..Lingaraj Seema?”

“ls is a command that tells the system to list all the files in the directory. The -al  is passing options to the command. -a stands for all files and l (small L)  tells it to show detailed information.”

Lingaraj then pressed the ‘Enter’ key. A list of files come up saying

| Loveletter_Mythri               rw-rw-rwLoveletter_Chitra​       rw-rw-rwLoveletter_Sanjana​       rw-rw-rwLoveletter_Sangeetha​       rw-rw-rwletterwriter​​       rwx-rw-rw |

“What are all those ‘r’s? Rejections? And ‘x’? Ex love affair?” asked Seema.

“Maybe I have to change the directory. Which directory am I in now?” Lingaraj asked mostly to himself.

Lingaraj then typed

| $ pwd |

The system showed

‘Love life progress’

as the directory.

“About all the ‘r’s and ‘x’s I will tell you when we get to file permissions. Enough for this session. Let’s meet after an hour. I am not in a good mood now.” said Lingaraj.

“I can understand.” said Seema.

Seema thought of taking a walk and stepped on to the path. She saw many cyclists approach in a group. There were youngsters and old people as well, those who kept themselves fit. They all looked at Seema and some of them smiled and waved at her.

![](image_rsrc834.jpg)

They all parked their bicycles and went on to their respective homes. Seema continued with her walk and found a small stream nearby. She sat there on the rocks for a while and decided that she would include this in her everyday routine.

![](image_rsrc835.jpg)

“So, do you want to start with chocolate milk shake or noodles with sweet chutney?” asked Lingaraj when they resumed in his house.

“A chocolate milk shake.”

“So, the shell. There are many ways to the kernel. This shell is one of them. There are many shell commands which you will find. There are many kinds of shells as well, like Korn shell, C shell etc. But we use Bash.

When we type

| $ /bin/bash –version |

It gives you the version of the shell.”

Lingaraj called out to a parrot making a weird sound and a parrot came and perched on the window rail.

“This is Paresh’s parrot. Say Hi.”

“Hi.” said Seema to the parrot and the parrot responded in like making Seema happy.

![](image_rsrc836.jpg)

“You can redirect the output to a file. In our community, if somebody is trying to talk to us and we are busy, we ask them to talk to a parrot’s ear. The parrot then repeats it to whoever is interested. So,

| $ ls -al > lsoutput.txt |

Here ls -al is the command that lists all the files. The output can be sent to lsoutput.txt for future use.

Of course there are cases when a person talks nonsense. We ask them to speak into a tree’s hollow. It’s gone forever. In Linux, we have

/dev/null

Once you send it there, there’s no return.”

Lingaraj continued.

“So,

| $ ls -al > /dev/null |

gives nothing.

| $ ls -al > lsoutput.txt |

If the file called lsoutput.txt exists, it will be overwritten. To append to the file, that is to make the parrot retain what was said yesterday, use the

| $ ls -al >> lsoutput.txt |

Notice there is a double greater than symbol.

Sometimes you would want to know what is going on in somebody’s mind.”

“Yes, I do have that curiosity.” said Seema.

“You can see the list of processes that are happening in the system.

Use the ‘ps’ command.” said Lingaraj.

| $ ps |

A list of processes on the system were shown.

“That would be very helpful. I can see what’s happening in Vijay’s mind.” said Seema.

“Yes, if he’s thinking of a particular car.”

“Especially if he’s thinking of me.”

“I will tell you something that can help. You can even kill a process using the kill command.”

“Let’s finish all these things quickly. I have many processes to kill. Can I add a process to his mind, like think about my birthday gift for example?”

“That would take many birthdays to learn.”

Lingaraj paused. Seema thought he would ask her when her birthday was.

“You can listen to the parrot. In Linux, you can read the contents of a file in degrees by using the

| $ cat lsoutput.txt |

Also, this

| $ more < lsoutput.txt |

Like the output was redirected, in this case the input is redirected to a utility called more.

The wc command tells you the word count. An option is

| $ wc -m |

which tells you the number of characters.

The man command…”

“Helps us understand men?” Seema interjected.

“No, helps us understand the Linux system. Man is short for manual. If you need help, type help, say

| $ ls –help |

You can even try info ls. Let’s take a walk.”

Seema and Lingaraj packed some food and went near the mountains. There was a small mountain which they agreed would be nice to climb. Lingaraj had brought his laptop. As they climbed, Seema felt she could do so comfortably without panting or being out of breath. The air was not polluted and it energised her.

![](image_rsrc837.jpg)

They reached the top and she could see rivers and make out some village settlements. There was no sign of asphalt roads.

“Shout Vijay’s name.” Lingaraj suggested.

“Vijay!” shouted Seema.

There was a prompt echo that repeated twice.

![](image_rsrc838.jpg)

“There’s this is a command in Linux. The echo command.” said Lingaraj opening his laptop and giving it to Seema.

“Wow, I can get Vijay to shout my name and the echoes will keep resonating.”

“It just repeats what you say. Once. Try it out. Say something original.”

Seema typed into the laptop.

| $ echo I am there for you, Vijay |

There was the following output.

| I am there for you, Vijay |

“As original as an echo.” Lingaraj commented.

Lingaraj was silent for a while.

“Do you want to use a pipe?” asked Lingaraj.

“What’s in it? Some herbs?”

![](image_rsrc839.jpg)

“No, it connects one command’s output to another’s input.” said Lingaraj pointing at his laptop.” He typed and showed Seema the pipe key on the keyboard just above the ‘Enter’ key.

| $ echo Seema is original &#124; wc -m18 |

The echo command is piped with the wc -m command. The echo command outputs to the wc -m command which them counts the number of characters because of -m. The > is used to input from files and < to output to files and the pipes are for commands.

“Let’s go back.” said Lingaraj.

As they approached the camp, they could see some people already at work. A few of them were making jute bags.

![](image_rsrc83A.jpg)

“Just like we use jute bags to hold things , there are directories that hold files.

![](image_rsrc83B.jpg)

There are many directories. Here’s a list of them.

/

This is the source directory.

/bin

Any idea?”

“The waste directory, some kind of a trash bin?” asked Seema.

“It contains all binaries of programs. There’s this book about directories in my room. Read that. Meanwhile, I will get some fresh juice.”

Seema proceeded to Lingaraj’s room and found the book. As she was searching, she saw books on various topics like film making, writing poetry and others.

![](image_rsrc83C.jpg)

Then she met Lingaraj outside after she read the first few pages. Lingaraj gave her watermelon juice.

![](image_rsrc83D.jpg)

Lingaraj continued.

“

/boot

Your thoughts on it?

“When a computer boots up, the necessary files are stored here.” replied Seema.

“

/dev

?”

“Development tools….no wait, device files. Devices, programs, databases, etc. etc.”

“This brings me to

/etc

?” asked Lingaraj.

“All the host specific system configuration files.”

“

/home

?”

“All your personal stuff. All those 43 letters.”

“44 now.” said Lingaraj with sadness in his tone.

“

/lib

?”

“Essential shared libraries and kernel modules.”

“What’s a shared library?” asked Seema.

“Many programs that are written can use already existing programs which are written for such a benefit. Like if you order noodles with sweet chutney, the noodles already made can be bought by the hotel management. So, if I write a program that involves adding two numbers, I can call a program from a library that already has the addition program written.”

“And kernel modules?”

“Programs loaded at run time like a device driver. A device driver is a program that talks to the device like a printer or a scanner or an external hard drive.”

Lingaraj looked into the distance.

“Something bothering you?” asked Seema.

“I fell in love with a librarian once when I was reading Linux programming in the library.

I went and told her, ‘Ever since I saw you, my circulation has stopped. I have booked two tickets to the movie.’

![](image_rsrc83E.jpg)

She said ‘Return them.’”

Seema did not know what to do. Over time, she would get used to Lingaraj’s anecdotes.

“Anyway, let me just mention them. 

/proc

The filesystem created on the go. A control and information centre for the kernel. This is where you go if you need information. For example,

| $ cat /proc/cpuinfo |

Will give you information about the CPU.”

Lingaraj pointed to some people who were sitting and gossiping.

![](image_rsrc83F.jpg)

“Let me tell you a story. There are a lot of ladies and gentlemen who sit outside and they know practically everything about our community. In fact when someone wants to make a marriage alliance, they ask this group about the man’s character. This was a long time ago, before we had heard of mobile phones.

There is another community in an island. There, they are not in touch with the world and don’t know of any technological advancements.

![](image_rsrc83G.jpg)

They were ruled by a King. I thought since I possessed a hair dryer, I thought I would take it to him and impress him. I had heard he had a daughter. So, I took this perilous journey that took 4 weeks and went to the island.

![](image_rsrc83H.jpg)

I was roaming around in modern clothes and soon I was captured. This was part of my plan. I was taken to the King.

![](image_rsrc83J.jpg)

‘Are you an alien?’ the King asked me.

‘I come from afar and now I will stun you.’ I said.

I asked for a bucket of water which they provided.

![](image_rsrc83K.jpg)

I then threw it at the King and he was drenched. He was very angry.

‘I know you are angry. But I will dry you in an instant.’ I said.

![](image_rsrc83M.jpg)

‘If you don’t do that, I will drench you in your blood.’ shouted the King.

‘Okay, this magical device here that I invented…’

![](image_rsrc83N.jpg)

I took out the hairdryer.

‘Where’s the power point for this?’ I asked.

‘What bloody power point?’

‘Oh I see!’

![](image_rsrc83P.jpg)

The King took out his sword.

I closed my eyes. Those people didn’t have electricity.

Then, as the King approached near and was about to use his sword,

![](image_rsrc83R.jpg)

these people came and saved my life. They had brought solar powered batteries.

I took the batteries in a hurry and used the hairdryer to dry him. He was mollified. He asked me to stay back and I told him I would bring more such amazing things.

“What an adventure! Is this really true?”

Lingaraj continued, ignoring the question.

“Well, these people tell every alliance that comes for me, this story and they laugh at me.”

“Is the King still around?” asked Seema.

“No, he died in his bath tub from electrocution while using a hairdryer.

Anyway, these people, they are like these control rooms, they know everything, like what I was up to in the island, etc.

/root

The superuser’s home directory.

/sbin

Essential system binaries, for whom superuser credentials are required.

/tmp

Temporary files.” explained Lingaraj.

“Temporary files. Not important, I think.” said Seema.

“Look at our world. The whole world is stored in a temporary directory. Very important.

/usr

The base directory for shareable and read only data.

/usr/include

Header files for compiling c programs.

/usr/lib

Libraries for most binary programs.

usr/sbin

Non vital system binaries.

usr/share

Architecture independent data.

usr/src

The source code.

usr/x11r6

The x window system.

/var

Variable data like email , printer logs, etc

.”

“Is there a heart directory? I want to look in to that in Vijay’s system and see if any traces of me are there.” Seema said sadly.

“A rhetorical question, I assume. If I put you in a maze, how would you get out?”

“I would begin by knowing where I am.”

“In a Linux system, how would you do that?”

“I don’t know. Ask the system where I am.”

“What’s the pwd command?”

“It shows the personal working directory, in this case, your love letter directories. I saw it.”

“No, it’s print work directory. The directory that you are now in. So, if you are stuck in a maze of directories, somewhere and don’t know where you are, you type pwd. And if you want to go back home, it’s simple. Type

| $ cd |

And if you want to go to some other directory, the /usr/lib for instance,

| $ cd /usr/lib |

| $ cd .. |

takes you one level up in the directory structure.

I will now list some commands and explain them.

| $ file textfile |

Says what kind of a file it is. Whether a directory or a C source file, or an executable or a text file, etc.

| $ cat textfile |

The cat command displays the contents of a file.”

Again Lingaraj was disturbed. Seema by now had learnt he would have a story to say. And she was willing to bet her last rupee it was going to be a sad story.

“There was this girl, Billy in the city. One day, as her cat was trying to cross the road, a guy on a bike desperate to cross the road before the cat crossed his path sped and almost killed the cat. I took the cat to a vet and I saved the cat’s life. I felt heroic and special. Billy and I became friends. One day, I went and told her, ‘Let’s concatenate our lives.’

‘You are in a queue because there are eight other people who have saved the cat’s life, because a cat has 9 lives.’”

“Why do you bring up these stories of love disappointment? You have to delete them and move on.” said Seema.

“Which brings us to the next set of commands.

‘rm’ and ‘mv’. rm, removes a file and mv moves the file to another location.”

“OK, rm Billy. Mv /home/Lingarajlovefiles to /newprospect” said Seema enthusiastically.

Further, Seema typed

| $ rm Billy$ mv /home/Lingarajlovefiles to /newprospect |

“There is no /newprospect directory.” said Lingaraj.

“So let’s create it. What’s the command to make a new directory?”

“mkdir” replied Lingaraj.

Seema then typed.

| $ mkdir /newprospect$ mv /home/Lingarajlovefiles  /newprospect |

I am assuming rmdir removes the directory.”

“Yes” replied Lingaraj.

“Let’s find all your failure files. Is there a command for that?” Seema asked.

They opened Lingaraj’s personal directory on the system.

“Now, if we use ‘grep’ and a pattern, in this case ‘failure’, it will list all the files among the 44 which have ‘failure’ in them.” said Lingaraj. He typed.

| $ grep “failure” /home |

As luck would have it, all the names of the 44 files were displayed.

“Even the law of averages fail here.” quipped Seema.

“Pipe it with more.” instructed Lingaraj.

“You want to see more of this?”

“Okay, type ‘less’. To see the contents of a file in a comfortable way. ‘more’ or ‘less’ work the same way more or less.”

Seema saw the contents of a file and was reading it with some interest when Lingaraj interrupted.

“I don’t want to see it, let’s clear the screen. Type ‘clear’.”

Seema typed

| $ clear |

The screen was immediately cleared.

“This clears the screen, not my fortune though.

| $ lpr |

Prints the file or program output to a printer.

| $ ps |

Lists all the processes

| $ w |

Shows who’s logged in and what they are doing.

So, if you want to see if anybody else is trying to get to Vijay and alter him or command him, you can find out.” said Lingaraj.

“You are making me panic.”

“If it helps, there’s a kill process as well where you can kill the process. Only the process, mind you. I will tell you about this later.

| $ cat /proc/cpuinfo |

Reveals the information about the CPU.

| $ top |

Displays the cpu processes

| $ cat/proc/meminfo |

Displays what’s  in the memory. A good place to see if you are still there in Vijay’s mind.

There are other commands like locate and find which do what they say.

I have a question. Once you get access to Vijay, what are you going to do?”

“I will become his superuser.”

“Tomorrow, we will get into shell scripting, superuser.”

Shell Scripting

It was evening and Seema thought it would be better to record Lingaraj’s classes. It would help her when she went back to Bengaluru. But it also contained some personal stories of his, and she decided against it. She made some sandwiches for herself and slept early that day. It was going to become a habit. 

![](image_rsrc83S.jpg)

“This is a shell script. But it’s not a file. We will type it into the command prompt.”

| $ for file in *> |

Lingaraj said while showing the screen on the laptop.

“The dollar just changed to this ‘>’ symbol!” exclaimed Seema.

“That happens to me in real life when it comes to money. Except it is the less than symbol.”

Lingaraj typed further. The complete program looked like this :

| $ for file in *>>do> if grep -l failure $file> then> more $file> fi> done |

What followed was the output.

| Failed relationshipThis is a file with failure in it. Please watch some motivational videos.$ |

I will explain the above later.”

“You mean the failed relationships?” asked Seema.

“The grep command.” corrected Lingaraj.

“Okay.” said Seema.

“Variables. Variables are those which vary and constants are those which don’t vary during program execution.

You can declare variables in the program as you go. Variables are case sensitive. To capital and small letters. ‘Linux’ is different from ‘linux’.”

“Let me try.” said Seema and typed on the command prompt :

| $ var=Sonal$ constant=Seema |

“I read a lot into it. To find out what the variable value is, you prefix a $ sign to it. You can use echo $var to see who the current...I mean what the current variable is.”

Seema typed on the command prompt.

| $ echo $var |

The output was then shown on the screen.

| Sonal |

She typed further.

| $ echo $constant |

The output was shown.

| Seema |

Seema felt triumphant.

“There is this peculiar situation. If you assign a value to the variable like 3 + 4 what happens?” asked Lingaraj.

Seema typed.

| $ result=3+4$ echo $result |

The output was shown.

| 3+4 |

“It didn’t add.” said Seema.

“So, we learn that the variable is stored as a string and not as a value.

No spaces on either side of the equal. And if you want to include spaces like ‘Sonal Vijay’, you quote them.”

Lingaraj was oblivious to his mistake regarding ‘Sonal Vijay’ together and Seema thought he would correct it. She typed.

| $ constant=“Seema Vijay”echo $constant |

The output was shown.

| Seema Vijay |

“You can read input also and assign the input to a variable using read and the variable name after you ask for the user input in the script.” said Lingaraj.

Seema typed.

| $ read earinput |

The she typed.

| Let’s go to the movie. |

“Now, use echo $earinput” said Lingaraj.

Seema typed.

| $ echo $earinputLet’s go to the movie. |

“Let’s try this in a program. Notice the quotation marks” said Lingaraj. And typed in a new shell script named vardemo.sh.

| #!/bin/shVijaysvar=“Are you in there”echo $Vijaysvarecho “$Vijaysvar”echo ‘$Vijaysvar’echo \$Vijaysvarecho Enter some textread Vijaysvarecho ‘$Vijaysvar’ now equals $Vijaysvarexit 0 |

He executed the shell script at the command prompt, by using

| $ sh vardemo.sh |

and the output was displayed on the screen.

| Are you in thereAre you in there$Vijaysvar$VijaysvarEnter some text |

At this point, Lingaraj entered some text.

| All variables cleared |

The program continued to execute.

| $Vijaysvar now equals All variables cleared |

“This shows the syntax of using variables and echoing them.”

Lingaraj continued.

![](image_rsrc83T.jpg)

“Suppose you find yourself in a system and want to know more about the system. The shell supplies some variables that are available once the script starts.

I allowed you to live in the house.” he said changing the topic suddenly.

“Yes, that was mighty good of you. I wanted to thank you but with all this Vijay situation…”

“Did you clean the room.”

“Did I have to? I mean it was clean enough.”

“That’s because I cleaned it before you came. Now, suppose I hadn’t cleaned the house, what would you have done?”

“I would have cleaned it.”

“While executing the task, you would have these details in your know how.

1) Home. Which is your home?

2) PATH : Where to look for tools like broom, buckets, etc.

3) The name of the task. In this case, cleaning. But it could be even disinfecting or fumigating.

4) The number of variables passed. In case you are cleaning, I will say to you, use neem paste, turmeric root extract and apple cedar vinegar as the cleaning agent. So, the count is three, there are three variables.

5) The variables passed, also called arguments. The neem paste, turmeric root extract and apple cedar vinegar.

5) The id of the job. In case there are 25 jobs you are doing, I will assign an id to each of them.

Similarly, in a shell script, we have variables as part of the environment. So, there is this class called environment variables.

These are some environment variables.

| $HOME | The home directory of the current user. |
| $PATH | Where to look for commands. |
| $0 | The name of the shell script. |
| $# | The number of variables passed. |
| $$ | The process ID of the shell script. |

Other environment variables are.

| $PS1 | A command prompt. The $ sign usually, but you can change it here. |
| $PS2 | The command prompt when prompting for additional input. |
| $IFS | The input field separator. |

Moving on, let’s try it in a program.”

Lingaraj created a new shell script started.sh and typed.

| #!/bin/shbegin=“Starting”echo $beginecho “The program $0 is now running”echo “The first parameter was $1”echo “The second parameter was $2”echo “The parameter list was $*”echo “The user’s home directory is $HOME”echo “Please enter a new greeting”read sentenceecho The sentence you entered : $sentenceecho “Script done”exit 0 |

“We can run this using ‘sh started.sh’, but if you want to run it like an executable with arguments and all, we need to change the permissions first using

| $ chmod +x started.sh |

Then we use the following command.

| $ ./started var1 var2 |

You get this output.

| StartingThe program ./started is now runningThe first parameter was var1The second parameter was var2The parameter list was var1 var2The user’s home directory is /home/LingarajPlease enter a new greeting |

At this point, Lingaraj entered some text.

| How goes the day?The sentence you entered : How goes the day?Script done.$ |

Now, conditions. You take decisions based on how a set of conditions are. To find out whether a condition is true, you test it. 

With the test command you can test if two things are equal.

The test command goes like this if there are two string variables. In a program, if you use this line of logic,

| if test speech1 = speech2thenecho Speeches are consistent.fi |

You can even use this

| if [ speech1 = speech2 ]thenecho Speeches are consistent.fi |
| if test value1 != value2thenecho Value not same.fi |

Test can work for strings, arithmetic expressions and files in the sense that you can test for conditions.

Like you can test for null strings.

| if test -n speech1thenecho The file is not a null string.fi |

| if test -z speech1thenecho The file is a null string.fi |

About the ‘if’ and ‘fi’, I will tell you later.

It can be used for arithmetical expressions too. The result, which is true or false can then be utilised for implementing a set of actions. That is where the ‘if and fi’ come in.

Some more things you need to know about testing for conditions.

| expression1 -eq expression2 | True if the expressions are equal |
| expression1 -ne expression2 | True if the expressions are not equal |
| expression1 -gt expression2 | True if expression1 is greater than expression2 |
| expression1 -ge expression2 | True if expression1 is greater than or equal to |
| expression2 |  |
| expression1 -lt expression2 | True if expression1 is less than expression2 |
| expression1 -le expression2 | True if expression1 is less than or equal to |
| expression2 |  |
| ! expression | True if the expression is false, and false if the expression is true. |

It can also be used to test files.

File Conditional

| -d file | True if the file is a directory |
| -e file | True if the file exists. |
| -f file | True if the file is a regular file |
| -x file | True if the file is executable |
| -w file | True if the file is writable |

and more.

Now, coming to the ‘if’ logic as promised. See this program. The equal sign is also used for testing when it comes to strings. Lingaraj showed her the program on the screen.

deepa.sh

| echo Do you love me Deepa?read deepipif [ "$deepip" = "yes" ]thenecho Congratselif [ "$deepip" = "no" ]thenecho Think againfi |

What it does is…”

“Give ‘Think again’ as the output?” suggested Seema playfully.

“You did not have to compute that, did you.”

He continued.

“We also have the else statement.

deepafriend.sh

| echo Do you love me Deepa?read deepipif [ “$deepip” = “yes” ]thenecho Congratulationselseecho Please pass this question to your friendsfi |

And to convince Deepa if she is sitting on the fence,

deepadesp.sh

| echo Do you love me Deepa?read deepipif [ “$deepip” = “yes” ]thenecho Congratulationselif [ “$deepip” = “maybe” ]thenecho Remember our previous incarnationselif [ “$deepip” = “no” ]thenecho You will never meet another Lingarajfi |

‘fi’ is if backwards to finish the if condition statement.

Now, the for statement. Do you have any doubts about Vijay. You feel he likes somebody in secret?”

“Well, do you have a solution?” asked Seema.

“Give me her name.”

“Swathi, Aarthi and Bharati.”

“Look at this program.”

Seema looked at the screen.

vijaysab.sh

| #!/bin/shfor interest in  Swathi, Aarthi Bharatidoecho Vijay is no longer interested in $interestdoneexit 0 |

The output was shown on the screen.

| Vijay is no longer interested in  SwathiVijay is no longer interested in AarthiVijay is no longer interested in Bharati |

Did you get it? As long as the values of the variable are true, the statements in the for loop will keep executing.”

“Thanks!” said Seema.

“Use for loop if you know the number of times it has to repeat. But if you don’t know his numerous….I mean the exact number, use the while loop.

fiancename.sh

| #!/bin/shecho “Enter fiance name”read fiancenamewhile [ “$fiancename” != “Seema” ]; doecho “Remember those times, Vijay.”read fiancenamedoneexit 0 |

This keeps going on until the user inputs your name as fiance name.

Now, the until conditional

vstate.sh

| echo Enter your stateread vstateuntil [ "$vstate" = "human" ]do    echo Seema learn more Linux    read vstatedone |

Can you tell me what this does?

“It says until Vijay comes back to the human state, I will keep learning Linux. I don’t mind doing it.”

“Now, you haven’t had a proper welcome into our community.”

“No issues. I am here to learn.”

“Suppose you have a requirement, we have different people for that. Look at this.”

requirement.sh

| #!/bin/shecho “What do you want?”read requirementcase $requirement incook)    echo “You must contact Yashasvini”    ;;herbs)    echo “Contact Lingaraj’s father Ashwath”    ;;treeclimbing)    echo “Contact Gidaa ”    ;;crocodileconversation)    echo “Contact Lingaraj ”    ;;*)    echo "Lingaraj can help"esac |

So, for each case of user input, there is a different output. You end the statement with esac. This is the syntax to follow.” said Lingaraj.

“Would you help me in talking to a crocodile?” asked Seema.

“You don’t want to do that. It hardly shuts it’s mouth once it opens. If ‘if’ has to sift through different statements life can become difficult. So we have the && list. The && list is like a sequential test. Example

seqtest.sh

| echo Can you climb trees?read treeclimbecho  Do you know how to cook millets?read cookmilecho Can you run faster than a gazelle?read gazecho Can you sing ghazals?read ghazif [ $treeclimb=“yes” ] && [ "$cookmil"=“yes” ] && [ "$gaz"=“yes” ] && [ "$ghaz"=“yes” ] ; thenecho Will you marry me?fi |

said Lingaraj as he showed Seema what he typed.

“I predicted the marriage proposal.” said Seema.

“So, only if all the conditions are satisfied, the final proposal is displayed on the screen. This was written 4 years ago. Now I have changed it. See.”

Lingaraj showed her the new version of the program.

seqtest_or.sh

| echo Can you climb trees?read treeclimbecho  Do you know how to cook millets?read cookmilecho Can you run faster than a gazelle?read gazecho Can you sing ghazals?read ghazif [ $treeclimb=“yes” ] &#124;&#124; [ "$cookmil"=“yes” ] &#124;&#124; [ "$gaz"=“yes” ] &#124;&#124; [ "$ghaz"=“yes” ] ; thenecho Will you marry me?fi |

The double pipe is an OR list. Even if one condition is satisfied, it proceeds to propose.”

“I think you really need to get engaged. I will introduce you to some women. You are a nice guy.” said Seema sensing the session was over.

The next day Seema woke up to the sound of knocking. Lingaraj came inside with boxes of bananas, apples and pineapples.

“Thanks for your gesture.” said Lingaraj and left.

They started the session at the usual time. Lingaraj began.

“Now, functions. If you have a function in the house, a ceremony or a ritual, you don’t do everything. You delegate all the different work to different contractors. Food for one, the decorations for another, invitation cards to one guy, welcoming to another,etc. So, you can concentrate on what you do. Each guy can be called whenever the need arises.

Here’s a function example.”

Lingaraj showed Seema a shell script.

foodfunc.sh

| #!/bin/shfood() {echo “Food is being prepared.”}echo “script started”foodecho “script ends”exit 0 |

Lingaraj ran the shell script and the output was shown on the screen.

| script startedFood is being prepared.script ends |

You call a function, the function executes.

When you marry Vijay, please use me as a function to bring the horse the groom rides on. One of my hobbies is catching horses near the forest and training them.” said Lingaraj.

“Really? I don’t believe it.”

“I have a hard disk full of those videos. Wait, I will show you.”

![](image_rsrc83U.jpg)

Lingaraj removed a hard disk drive from his cupboard and connected it to the laptop. Then he stopped.

“What happened?” asked Seema.

“The hard disk of horses did not mount.”

Lingaraj continued.

“In case of functions, the $* $1 $2 are replaced until the function finishes, by the parameters of that particular function. So too, variables. Variables for use within the function are called local variables.

Suppose you have a budget of 2 crore rupees earmarked for the whole function. And the value of the budget variable, $budget is 2 crore. But you will be paying me 20 lakhs for getting the horse. So, the budget variable in my function, $budget will be 20 lakhs.

“That’s too much. Give me a discount.” asked Seema.

“Neigh!”

They both laughed. Seema was finding Linux enjoyable and Lingaraj made her feel she could one day find it in her to program Vijay and make him revert to being human again.

Lingaraj showed her another shell script.

paramdiff.sh.

| #!/bin/shparamshow() {var="Lingaraj’s function"echo The variable var inside the function is $varecho The first parameter for this function is $1} |

The main part of the shell script goes like this:

| var="Seema’s wedding"echo The variable var in the program is $varecho Original first parameter for this program is $1paramshow Lingarajexit 0 |

Lingaraj ran it using the command :

| $ sh ./paramdiff.sh Seema |

“Let’s look at the output :

| The variable var is in the program is Seema’s weddingOriginal first parameter for this program is SeemaThe variable var in the function is Lingaraj’s functionThe first parameter for this function is Lingaraj |

Even though we used ‘$1’ for both the program and the function and the same variable name, ‘var’.

Now, some commands within the shell programming which you normally can’t use on the command prompt.

| break |

You can use break to escape from the loop before the condition has been met. The break statement leads to an immediate exit of the enclosing loop. And if the break is inside an if statement which is inside a while or for loop, the break will take the program out of not only the if statement, but the while loop or the for loop too.” said Lingaraj.

“In my case, when I work on my presentation I decide to work until I finish. But if I smell cake from my neighbour’s house, I take a break to bake one.” said Seema.

“In our community if a neighbour makes a cake, we simply go and partake. As if it’s made for our sake.

Just like break, we have the continue, which tells the program to continue.

Continue skips the remaining commands inside the loop for the current iteration.

Suppose you are receiving people for a seminar. These are the things you do.

do {

You see the person

You ask for the id card

You ask for the filled application form

You take money

}

while (people walking in)

This has to be a loop if it has to be done for everybody. But if you see me at the seminar? Then, we change the logic.

do {

You see the person

if person = Lingaraj

continue

You ask for the id card

You ask for the filled application form

You take money

}

while (people walking in)

Basically continue skips the loop for that particular iteration depending on the condition.

Don’t worry about the syntax for now. If you see me at the seminar,

then you skip all the remaining tasks because you know me well and won’t ask me for the id card, the filled application form or money.

“I get it. Continue is for special cases like you where we don’t want to go through the rest of the process meant for the average person.”

Lingaraj as was the trend, continued.

“Back to commands. Sometimes a command can be stored in a variable. Example:

| $ CD=”cd Lingaraj”$ eval $CD~/Lingaraj $ |

Have you encountered a situation where you do not tell Vijay what is happening and wait for him to guess?” asked Lingaraj.

“I must admit. It was my birthday and I had made a special dish. Vijay had forgotten. To make matters worse he asked, ‘What’s the occasion?’. I said ‘Nothing’, said Seema.

“Now, if eval could be used in real life,

| eval $Nothing |

The output would be

Today is my birthday, wish me!

Here, Nothing is a variable that stores a command which tells Vijay to tell you something.

eval looks at the command stored as a variable and executes it.

So, if you look at the real life program,

| $ Nothing=“echo ‘Today is my birthday, wish me!’”$ eval $Nothing |

The output would be:

| Today is my birthday, wish me! |

The ‘exec’ replaces the shell with another program. Like doing away with the shell.

| $ exec echo This shell is gone! |

The words are echoed to the screen and the shell goes away.”

“Is that okay? The shell going away? Isn’t the shell important?” asked Seema.

“Philosophically, no!”

Seema understood he meant the outer shell of a person. Lingaraj continued.

“You can remember it this way. Will execution. A person nominates someone in his place and disappears.

My great grandfather was fond of concocting all kinds of plant and vegetable juice to make his special drinks. He used to tell a lot of tall tales after that. On one fateful day, he had made a drink. He took a sip and turned blue. Before passing away, he announced my father, who is actually an academic of great stature with a biotechnology engineering degree and an MBA, as the next concoction maker. My grandfather’s old customers still come to my father to buy drinks and my father chases them away. 

The ‘exit’ command. If you type exit after a command in the program, you can return a value which can be used by the program. I have a request. If after you finish this course with me and someone asks you how it went, tell them it was 0.”

“You are not that bad!”

“In Linux, an exit code of 0 usually indicates success.

There are 125 more exit statuses.

Now, the ‘export’ command. You said I am not that bad. If you think I am great, which I am sure you will, it’s no good if you tell me. You have to tell others as well. So,

| Lingaraj=Great |

has to be made available to everybody, in addition to assigning it you have to export it.

| export Lingaraj |

So other people like you can come to me and learn from me.

In Linux, when you use the export command, that variable stops being just a local variable and it’s value can be used in other scripts and commands invoked by the current script.

Look at this shell script, echoexport1.sh

| Lingaraj=greatexport Lingarajecho The value of Lingaraj is $Lingarajecho "This is the shell script where Lingaraj=great is declared."echo Now calling the second script./echoexport2.sh |

And now, echoexport2.sh

| echo The value of Lingaraj is $Lingarajecho "This is a shell script that does not contain the declaration."echo "Yet, if it is being called by the script which had a declaration and export, this will print the value of Lingaraj." |

When we run them both, we get this output :

| The value of Lingaraj is greatThis is the shell script where Lingaraj=great is declared.Now calling the second scriptThe value of Lingaraj is greatThis is a shell script that does not contain the declaration.Yet, because it is being called by the script which had a declaration and export, this is printing the value of Lingaraj. |

‘expr’ . Like ‘eval’ looked into the variable storing the command, ‘expr’ looks into the arithmetic involved in a stored variable. Other variables are stored as strings. But expr looks beyond the string and looks at things mathematically.

expr_add.sh

| echo Enter 2 numnersread xread yresult = `expr $x + $y`echo “Result = $result” |

Notice the back tick. This is below the ‘Esc’ character.

Lingaraj ran the program.

The output was shown.

| Enter 2 numbers. |

Lingaraj entered 4, pressed the ‘Enter’ key and pressed 5.

| Result = 9 |
| $((…)) |

A better alternative is $((…)) expansion. By enclosing the expression you wish to evaluate in

$((…)) , you can perform simple arithmetic much more efficiently:

incrx.sh

| #!/bin/shx=0while [ “$x” -ne 10 ]; doecho $xx=$(($x+1))doneexit 0 |
| set |

set takes the output from a command, function or a program and makes a neat little variable list, $1, $2 etc out of it. Here’s an example :

setdate.sh

| #!/bin/shecho The date is $(date)set $(date)echo The month is $2exit 0 |

Here, the output from the date is taken and set. The month is the second variable in the list and so it is printed.

| shift |

shift reduces the parameter number $3 becomes $2, $2 becomes $1 with $1 being kicked out. $0 remains the same.

“Why would you need this?”

“You can scan only 10 parameters , that is $10 is the highest. What if somebody enters a 11th parameter. You might find it useful there.

There was this guy in our community who built a carriage that ran on herbs.  Everyone in the community wanted to ride in it. But there were only 10 seats available. So, after every ride, a guy was pushed in from the right, because nobody wanted to get out of the carriage. So, the first guy on the left would fall off. We did this until the whole community was happy. Of course, the carriage broke down and so did it’s inventor. Like that, you shift.

| unset |

Used to remove values associated with variables.

Suppose you wear a red dress and you come to have an identity associated with it. So

| favcolour = red |

In case you don’t want red to be your favourite colour any more, but can’t decide on a new colour, you do

| unset favcolour |
| $ find / -name test -print |

You will find all files named test and get it printed on screen. Starting with the / , the ….?”

“root directory.” Seema answered.

“So,

| $ find / -name Seema -print |

will print all the files named Seema in the system.”

These are a few options.

| -atime N |

N here is a number. The file was last accessed N days ago. When you know when Vijay last accessed a particular file to give you a parallel.

| -mtime N |

The file was modified N days ago.

| -name pattern |

The name of the file, excluding any path, matching the pattern provided. To ensure that the pattern is passed to find, and not evaluated by the shell immediately, the pattern must always be in quotes.

An example would be :

| find . -name “*ma” -print |

Will print all files ending with ‘ma’. Notice the dot. In the current directory. So, we learn that the * is pretty handy if you don’t know any names. It’s a great tool to use in marriage functions where some relatives come and ask you, “Remember who I am?” If this were an accepted convention, people would say, you are ‘* uncle’ or ‘* aunt’ literally and they would be happy and we can move onto more valuable pursuits like setting status messages.

Since we are on this topic, if you remember some part of the name like it has to be either Suresh or Ramesh, but can’t pinpoint, you can use ‘???esh’. That way, you will score some more social acceptability points. Because you weren’t off by a long way. You can even use [SR][ua][rm]esh. That way, people will think you are working on artificial intelligence. 

| find . -newer Seema |

Notice the period(.).

Finds the files newer than the file Seema. In case, there are any more additions since you last met Vijay.” said Lingaraj aiming to help.

“This is going a bit too far.”

“Look who’s talking.

type “-d” for a directory and “-f” for a regular file.

| $ find . \( -name “*ti” -o -newer Seema \) -a -type f -print |

“It finds all the files ending with ‘ti’ or files newer than Seema and must be a regular file as pointed out by f and then print. The backslash \ before the bracket is an escape character. 

You have seen how to find with filenames, but what about searching inside the files? You have the ‘grep’ command.

My great grandfather, as I told you made a lot of concoctions and I documented them on this computer. I have a list of files. Now, if I want to search all concoctions with grapes in them, this is how I do it

| $ grep grapes pprosedrink.txtYou shall squash these grapes |
| $ grep -c grapes pprosedrink.txtpprosedrink.txt:24 |

-c is count and there are other options. Like -v which is an inversion, shows how many lines there are without the word ‘grapes’. To see how many files have the grapes words without wanting to see the file, just add -l(small L).

| $ grep [a-h] pprosedrink.txt |

The square bracket can contain things that can be matched.

This will highlight all the words that contain alphabets between a and h.

| $ grep a[[:blank:]] pprosedrink.txtI am a fighting machine after this drink. |

After the ‘a’, ‘grep’ used the regular expression a[[:blank:]] which told the system to look for a blank after the a. That is in short, a word ending with ‘a’. ”

| grep th.[[:space:]] pprosedrink.txt |

Seema asked about the dot after th. She then told Lingaraj that she knew what was inside the square bracket was looking for a space. Lingaraj answered.

“The dot is telling the system to look for a single character

So the result is

| Huge is the skyBut if it weren’t for the eye |

A metacharacter is a normal character which has a meaning beyond it’s literal meaning.”

“The $ is a great example.” offered Seema.

“An anchor is the position in the line of text that the Regular Expression is to match. For example, ^, and $ are anchors.

What is 4 + 2?”

Seema was surprised. Seema thought of asking Lingaraj ‘Why?’ But she had a feeling Lingaraj himself did not ask himself ‘Why?’ before he did things. She answered.

“6.”

“5 + 1?”

“6”

“12/2?”

“6.”

“3+3?”

“6.”

“3 * 2?”

“6”

“Think of a vegetable.”

“OK”

“Is that a carrot?”

“Yes, how did you….”

“Works on most people.”

“Now, on the keyboard, if you use shift 6, you get a symbol. What is it called?”
Seema pressed shift and pressed 6 to get the ^ symbol.

“A caret.” she answered.

When you use regular expressions,

| $ grep ^T Seema.txt |

looks for lines beginning with T in the file Seema.txt

Moving on, you might want to execute a command and put the output of the command into as part of another command. Simple, put the command in brackets

| $ echo $(who) |

Enough for today.”

The next day, Lingaraj took Seema to a mango grove in the morning. There were a lot of monkeys there and they all seemed to recognise Lingaraj.

Lingaraj spoke as they walked.

“There is a way to talk to a system.  The system demands the syntax be right and a lot of other things. I trained a monkey once. If I snapped my fingers thrice in front of it’s face, it would fetch me mangoes from a tree. But if I snapped 5 times, it would attack me.”

“Why would you train a monkey to attack you?”

Lingaraj paused before he answered. “Guilt.”

![](image_rsrc83V.jpg)Lingaraj then called out to a monkey making a weird sound.

![](image_rsrc83W.jpg)

The monkey promptly appeared.

“This is the monkey I trained. Now, command the monkey to get mangoes from this tree.”

“You said it attacks. Now, I am confused. Should I snap or clap?”

“I knew this situation would arise. So, we have a safety option. Just say, ‘noexec’ and do what you think is the right thing.”

![](image_rsrc83X.jpg)

Seema said ‘noexec’ and clapped thrice rather than snapping her fingers.

The monkey gave a bewildered expression.

![](image_rsrc83Y.jpg)

And gave the thumbs down signal.

“In the shell script, if you use the ‘noexec’ option, the shell will tell you whether there is a syntax error or not. It won’t execute the program.”

Here you meant getting mangoes and clapped rather than snap, but the monkey doesn’t understand the syntax. And it communicates this and doesn’t execute the commands because you used ‘noexec’.

At the command prompt,

| $ sh -n <name of shellscript> |

and type the name of the shell script or

| $ set -o noexec$ sh <name of shellscript> |

in the command prompt and then execute the script. It then checks for syntax errors only.

Now, say ‘-v’, for verbose and snap your fingers thrice.

![](image_rsrc83Z.jpg)

Seema did it.

![](image_rsrc840.jpg)

The monkey repeated what Seema did by snapping it’s fingers thrice and proceeded to get mangoes from a tree.

![](image_rsrc841.jpg)

“See, the monkey echoed the command before executing it.” said Lingaraj.

| $ sh -v <script> set -o verbose$ set -v |

“Echoes commands before running them.” continued Lingaraj.

“This one,

| $ sh -x <script> set -o xtrace$ set -x |

Echoes commands after processing on the command line.” said Lingaraj.

“Okay, now he will get the mangoes and then will snap his fingers.” inferred Seema.

“Correct.”

![](image_rsrc842.jpg)![](image_rsrc840.jpg)

During rains, I programmed this monkey to sneak into a wine store and get us drinks. The command for this is, you make a thumbs up sign and say your preferred drink. Go ahead.”

![](image_rsrc843.jpg)

Seema gave a thumbs up sign and said

“Apple juice.”

![](image_rsrc844.jpg)

The monkey made a screeching sound.

“This is an error message. It happens when there is an undefined variable used. Apple juice is the undefined variable. We usually have rum or whiskey.

| $ sh -u <script> set -o nounset$ set -u |

Gives an error message when an undefined variable is used.

There is the dialog utility in Linux.

The syntax is :

| dialog --msgbox “I need rum” 9 18 |

9 and 18 are dimensions.

There are various options. The message can appear like a message box, or an info box, etc. Use the man command and try it on my laptop.”

Seema tried it on her laptop and explored various options. Lingaraj then proceeded to open his bag and distributed some bananas to the monkeys.

The C Compiler

When they were back at Lingaraj’s house, Seema proceeded to ask about Lingaraj’s parents.

“My father is in a biotechnology conference in Sweden. And my mother, on a trip to Ladakh and the Himalayas.”

“What made you choose to learn Linux? For me, it’s a necessity.”

“I like Linux because it made even a simple programmer like me see what the established programmers of great stature were seeing. Everything is shared here and it is one of the examples of a coming together of humanity, albeit in a part, to bring something of benefit to the world without really looking for a profit.

Now, let’s talk about the compiler.

The compiler takes what you write in human readable form and turns it into machine readable form.”

Lingaraj showed her a part of a C program on his laptop.

|   pthread_t t1, t2;  pthread_mutex_t mutex1;  pthread_mutex_init(&mutex1, NULL);    int iret1 = pthread_create(&t1, NULL, (void *) print_func, (void *) message);   int iret2 = pthread_create(&t2, NULL, (void *) print_func, (void *) message);  pthread_join(t1, NULL);  pthread_join(t2, NULL); |

“Oh! This is the machine readable form.”

“No, that’s human readable.”

Seema was taken aback.

“Linux usually uses the gcc. It’s a C compiler which can compile C, C++  and more.” continued Lingaraj.

The trick is to be able to speak to something in it’s language and make it do a job based on conditions.

Who lives with you at home?” asked Lingaraj.

“My mother.”

“Did you give any instructions to her as you came here?”

“Yes, I said ‘Don’t open the door unless you know the person very well.”

“See, that’s a program. You programmed her for safety.

Same with machines. But they understand only 0 and 1\. And the most basic are gates which can decide whether to allow current through it based on a condition. So, this behaviour depending on conditions is what makes computers. That an element found in mud allows current only one way through it is what made the electronics and computer worlds possible.

So, every line that you speak to a computer, current flows in a particular way and operations happen. You need to learn C. I would have suggested a good book written by me, but then I haven’t written it. I suggest you refer this book.” said Lingaraj handing over a book on C.

Seema came back the next day after poring over the book and taking notes.

“I learnt a bit of C. I now know the ‘Hello world!’ program.”

“I will cover a bit of structures and pointers now. A structure is a way to group related variables of different types in a basket, if you will. An example is

| struct example_structure{int any_number;char one_letter;}; |

The members can be accessed like this :

| example_structure.any_numberexample_structure.one_letter |

Most of the data like a variable is stored in memory. Now, C allows you the liberty to access that variable based on the memory address as well. The variable that stores the address of the variable is called a pointer. The address of the variable can be obtained as well as what’s stored there, the value.

For example

| #include <stdio.h>int main(){    int variable1 = 20;    int *vp;    vp = &variable1;    printf("The address of variable1 is %p\n", (void*) &variable1);    printf("Address stored in variable vp is %p\n", vp);    printf("The value of the variable variable1 is %d\n", variable1);    printf("The value at the address given by variable vp is %d\n", *vp);} |

We can try this program to get an idea. I won’t show you how I run it yet.”

Lingaraj ran the program and the output was displayed on the screen.

| The address of variable1 is 0x7ffe17ff187cAddress stores in variable vp is 0x7ffe17ff187cThe value of the variable variable1 is 20The value at the address given by variable vp is 20 |

The address is machine and instance specific. But if you see it, it gives you an idea of how pointers work.

Let’s test the ‘Hello World’ program. So, how do you invoke gcc, the GNU C Compiler? You just type gcc and the program name. The compiler will save the executable binary file as ‘a.out’ in the directory. But if you are bursting over with creativity and want to name it as something else, use the -o option.”

Then Lingaraj as was his wont, seemingly jumped to a completely unrelated topic.

“If you take a crocodile to the veterinary doctor for vaccination, the doctor will see it’s a crocodile from the south and he will talk to the crocodile in a language meant for crocodiles from the south. He won’t talk to it in north crocodile language. Similarly, the gcc is a cross compiler. Meaning it can understand what kind of a machine it is residing in and compile the program appropriately.

A north crocodile is different from a south crocodile

gcc knows this as it begins to compile

A different binary for a different architecture style

No wonder gcc is great and very versatile”

Seema had come to expect stories, but poetry about crocodiles was a bit too much.

“I heard you were a crocodile doctor over here.” she said.

“Right.”

Seema wondered whether he would take her to a crocodile for a demo.

“Can you really communicate with crocodiles?”

“Yes. One day there was this situation. I was wandering near the river when I saw this man of around 40 years of age. He sat meditating on the rock and put a lot of rubber crocodiles around him.

![](image_rsrc845.jpg)

He wanted to give the impression that he had some spiritual power which could deter even crocodiles from attacking him. He later said there were a lot of gullible people in the world and he had to guide them spiritually. He had brought a cameraman who was almost a gymnast.

![](image_rsrc846.jpg)

The cameraman then shot the video. It was going alright till cameraman decided to sit on one of the rubber crocodiles. Then he started moving sidewards. Everybody thought he was working the trolley shot. Actually, it was the crocodile moving. He had sat on a live one. I had to step in to calm down the crocodile. Turned out he was a fake spiritual guru, but I had to save him anyway.

Coming back to gcc, let’s run the hello world program that you learnt.”

Lingaraj saw the program. It was pretty straightforward.

| #include <stdio.h>main(){printf(“Hello World!\n”);} |

He compiled it invoking gcc.

| $ gcc hello.c -o hello$ lshello.c hello$ ./helloHello World! |

You can even invoke gcc step by step. The 4 stages in the compilation process are: preprocessing, compilation, assembly and linking.

If you want to do this step by step, this is how you go about it :

| $ gcc -E hello.c -o hello.cpp |

The above command creates the preprocessing file hello.cpp

| $ gcc -x cpp-output -c hello.cpp hello.o |

This make an object file hello.o. The cpp-output is a standard telling the input file type, in this case hello.cpp

| $ gcc hello.o -o hello |

This creates the final executable which you can run.

Files and Directories

Let’s look at the Linux system. Before that, I want to introduce you to ‘Thing Thimma.’”

They took a walk and reached a sugarcane field. The place was beautiful and they noticed a dainty looking hut in the distance. As always, Lingaraj carried his laptop. As they approached the hut, they could see lots of sugarcane pulp lying in heaps after the juice had been extracted. There was a man working in the hut.

![](image_rsrc847.jpg)

Then the man came out.

“Hi TT. This is Seema. She’s learning Linux.” said Lingaraj.

Seema proceeded to shake hands with TT.

“Thimma is into bagasse plate making, plates made of sugarcane pulp, after the juice has been extracted. Tell me Thimma how was your day? Everything okay?”

“Oh, today was quite this thing. The thing I bought from this guy had a faulty thing and I had to search in this thing for that thing to make this thing work like the thing I was used to. So I went to this guy selling this thing you use for that thing and that guy asked for this thing you see and….”

“Stop. You can go.” said Lingaraj.

Thimma walked back into his shed.

“I get the drift. ‘Thing Thimma’ has a nice ring to it.” said Seema.

“So, Thimma treats everything as a thing. From nuts, gears, press, machines, the phone etc. And Linux, too does the same. Everything is a file. From text files, programs, directories, devices, Linux treats everything as a file.”

“Ok”

“In Linux there are commands to work with files. Now ‘open’. What does this command do?” Lingaraj asked Seema.

“Opens the file.”

“Close?”

“Closes the file.”

“Read?”

“Reads the file. Wish this OS was there when I had to read all those books in school. It would have read it all for me.”

“To write a program to make the system read it for you and to transfer it all to your brain, would have meant even more reading. Now, ‘write’?”

“Writes to the file. This is so easy. We should have started with this.”

“‘ioctl’?”

“Errr….‘ioctls’ the file?”

“One day, when you have to program Vijay, this will be important to you. It passes the control to a device driver.”

Seema looked questioningly.

“His heart. Do you think his heart’s still in there? What’s the latest update about him?”

“The doctor said he stared at a picture of us we took, when we had visited this Pizza joint a long time ago, for 2 hours straight.”

“Seems like a positive development.”

“Then the doctor placed my phone number in front of him. He then called me and ordered five pizzas.”

“Poor guy, did you send them?”

“No!”

“Moving along, there are directories which store files. They are also considered files in Linux, but special ones. Can be accessed by the high level interface ‘opendir’ or ‘readdir’. High level does not mean something elite. It means it is higher because a lot of programming is below it. It is not a direct access to the system, but through a lot of programs.”

“As a man, you tell me in which directory does he store his love files.”

Lingaraj looked inspired.

“Actually, this gives me inspiration to write love poetry.”

Lingaraj sat down on a stone and started typing in his laptop.

“I have your love files in my heart directory

My heart is now, a love producing factory

You just say opendir or readdir

And it will be like drinking elixir”

Lingaraj looked dreamily towards the sugarcane fields.

“What was your question?” he asked after a while.

“Forget it.”

“Anyway, the file’s creation, permissions are stored in the inode. Inode can be thought of as a social number card for the file.”

Once I had a fight with this guy Prathap. It was over who gets a photo with a bison.

![](image_rsrc848.jpg)

I loathed him so much that I began tracking him. I got so much of his info that when he was getting married, his fiance came to meet me.”

![](image_rsrc849.jpg)

“To make you both friends again?”

“No, she wanted to know more about Prathap from me as I knew more about him than anybody else. I had become like an ‘inode’ for him. Collecting all the information.”

“How did you get out of it? This hatred?”

“Oh, I forgave him.”

“How?”

“After I saw him fend off three bison from attacking me and my family when I was sleeping. Actually I was only pretending to be asleep. I would have stepped in if he had perished and quelled the bison myself. But he did what he could.”

“Where is he now?”

“He is in Kenya now making documentaries on bison. He sent me his video link a couple of years ago.”

“Is it good?”

“I can’t say, I didn’t watch it.”

“There’s this thing called courtesy and gratitude.”

“Anyway, back to directories. A directory simply holds the inode numbers of all the files that are in it. If a file is deleted, the inode entry in the directory is deleted. The number of links for that file goes down by one. If the file is in 2 other directories, it means it has 2 links. If the files in both the directories are deleted, the number of links go to zero. The data blocks that it possessed is marked free. How do you get to your home directory?”

“cd? Right?” asked Seema.

“There is one more way. The cd tilde.

| $ cd ~ |

I have a knock knock joke.

Knock knock.”

“Who’s there?”

“Tilde”

“Tilde who?”

“Till date no one’s opened their heart for me.”

“I am really tired.”

The session was over and Seema was introduced to a guy with a boat by Lingaraj. The boatman took her on a boat ride and Seema enjoyed it very much.

The next day. Lingaraj continued at his house.

Let’s look at some hardware files. Three of them. We start with.

| dev/console |

This is the system console. A place where messages are usually displayed.

| dev/tty |

This is the controlling terminal. That is where the control of the system externally is coming from. And the messages go there.

| dev/null |

As told earlier, it is like a hollow in the tree. Most of what my great grandfather told in his later years were diverted to this hollow. The interesting thing is, I still hear his voice in the hollow. Maybe his ghost lives there. Do you want to see it?”

“No!”

“There is /dev/zero as well, which gives an endless supply of zeros if you read from it.”

“Who would want many zeros. Useless, I think.”

“I would. The difference between me and the richest man in our community is actually useless zeros as you say. But they come after the 1.”

“Character and block devices. Character devices deal with one character at a time, whereas block devices deal with one block of data at a time.

It’s like writing. If you are writing a phone number, you do it one character at a time. But if you were reading a story, you read a word, a block of data at a time. Like pigeons eat one grain at a time and dogs eat a whole chunk at a time.”

“This was the first example you gave me without involving a weird character from your community.”

“Wait, let me finish. I was once in a fight with a robber in the city. He was ![](image_rsrc84A.jpg)stealing my audio cables. He threw punches at me, like a character device.

But I took them all and gave him a solid shot with my hard disk, like a block device, which floored him.

![](image_rsrc84B.jpg)

Will help you remember.”

“The difference between character and block devices?”

“No, it will help you remember me as a hero. You said you would introduce some friends. Tell them this story.”

Seema began to count how many friends she would lose.

“Anyway, ‘ioctl’ is usually used not to pass input and output, but to make the device work which the software can’t do. Like reset the printer to it’s starting point. Or to rewind a tape drive, etc. Each driver has it’s own set of ioctl commands.

If you get to Vijay’s hand driver, you can program it to keep holding your hand. And when a bad guy approaches, you can program his hands and legs drivers to fight them. And maybe go on to participate in competitions. Maybe become a prize fighter. Maybe get into movies and earn money. I can be his programmer and we can show off Vijay to the world. It will be like a consolation for me.”

“That’s not what I came to you for. What do you mean consolation?”

“I made a robot once that looked exactly like me.

![](image_rsrc84C.jpg)

It used to act in movies in Bangalore and I had programmed it to fight well. After the robot was back home, I used to charge it and then go out and bask in all the glory of being a film celebrity.

![](image_rsrc84D.jpg)

One day I forgot to charge the robot and I had to go personally to the film scene being shot, which I found out later was a fight scene. The stunt director came and spoke to me.

![](image_rsrc84E.jpg)

He said, “Sir, you hit 50 fighters yesterday. Today, I have got 100 fighters for the climax. Action!”

![](image_rsrc84F.jpg)

There was action indeed. And lot of cuts.”

Seema had never heard such nonsense in her life. But Lingaraj made it sound so convincing.

“Let’s move on.” said Seema.

“You can use system calls or C library functions. System calls are expensive.”

“Expensive in what sense?”

“There was this guy called Ceremony Seena. Every time we used to call him, he used to come with a caravan and a retinue. And there was this huge ritual to invite him and protocol to receive him.

He lived on the main road that connected all the roads. His entourage would block the roads for hours. He was a well connected man who was in touch with people in the higher echelons of power. If a message needed to be passed to those powerful people, people had to speak to him. But whenever anybody called him, he would make a pompous ceremony. And we had to feed him, feed his followers etc. We had to make the switch between doing our work and looking after him. Overheads. So, later people devised these approaches where they called him once and finished with all the jobs. System calls are like calling Seena. Very expensive. But having people work out the details and finish all his jobs, it’s like high level access. So, we have C library functions for these.

An example is the standard I/O library. You might have data storage that deals with blocks of data. The standard I/O library makes the data to be sent to the storage, tailor made even if it’s a file that’s not used to writing in blocks of data.

So, how do you find out whether a call is a system call or a function?

C library functions are described in section 3 of the man pages. The section 2 is for system calls.

So, if you type

| $ man 2 fopen |

It says

| No manual entry for fopen in section 2 |

However, if you type

| $ man 3 fopen |

It shows the entry of fopen.

For the rest of the time, I use the phrase ‘C library function’ and the word ‘function’ for C library functions. For a function within the program, like a routine, I use just function. You have to identify whether I am talking about a C library function or a routine.

File descriptors. You so badly want to open some files in Vijay’s system.”

“And write to them.”

“You need file descriptors for that.”

“What’s a file descriptor?”
“It’s an integer associated with a file. And how is it different from an inode? An inode is a structure that has info about the files. A file descriptor is used in system calls. It is used by the system to refer to an open file.”

He then showed her a program.

writestd.c

| #include <stdio.h>#include <unistd.h>#include <stdlib.h>int main(){if ((write(1, “Standard output’s file descriptor is 1”, 38)) != 38)write(2, “Error writing to even standard output.”,39);exit(0);} |

What the above program does is, tries to write the first message indicated by write, “Standard output’s file descriptor is 1” to the standard output whose file descriptor is 1\. The string has 38 characters excluding the double quotes. It returns the number of bytes written. One byte per character. If all the bytes weren’t written, then it moves to the next line and prints the error message, “Error writing to even standard output.” to standard error, whose file descriptor is 2\. The file descriptor for standard input is 0.

readinp.c

| #include <stdio.h>#include <unistd.h>#include <stdlib.h>void main(){printf(“Please input some text.\n”);  char readinp[128];  read (0, readinp, 17);  printf("%s", readinp);} |

The above program reads 17 characters from standard input which happens when you type after running the program. Then it promptly prints the first 17 characters of what you typed. So, the syntax for the read and write system calls are :

| #include <unistd.h>size_t read(int fildes, void *buf, size_t nbytes);#include <unistd.h>size_t write(int fildes, const void *buf, size_t nbytes); |

The <unistd.h> is a header file. A header file contains declarations and macros. It does not contain implementations unlike a library which can do a job. It simply calls functions that do a job. You might have wondered in some organisations, there are heads who don’t do any work, but know people, especially those who study in libraries, who can work, even though the heads themselves know nothing about implementation. I said this only to help you remember. You can write your own header file, but if you want to include it, you use

#include “myheaderfile.h”

Also, let me talk about system calls. The kernel is not freely available to one and everybody. It is quite reserved having allocated a part of it for users to utilise the system. But sometimes you need the kernel for some operations. They could be process control, file or device management etc. The user cannot have the audacity to alter these things on his own. He needs to request the kernel for support and the kernel, with it’s rules allows the program to work on the operations. So, the mode is called supervisor mode or kernel space because it involves the kernel’s supervision.

Each system call, read or write, returns the number of bytes read. ‘filedes’ is the file descriptor. *buf is the character string which you have to declare beforehand and nbytes is the number of bytes. In ‘read’ the content is placed on the character string pointed to by buf and in write this can be an actual string. I will take you to a play.”

Seema was getting used to this unpredictability.

They both went on a bicycle on the same road which Seema had taken to get to the camp.

![](image_rsrc84G.jpg)

They reached a mud building and an open air theatre. There were about 20 people in there. Lingaraj introduced Seema to the director Nithin and a few actors. Then they watched the rehearsal of the play.

“Notice carefully.” said Lingaraj.

The actor Prashanth got into the character of a one ‘Odubari’. It was about an academic. Then Nithin, who wrote the play and who was the director as well made some changes in the script. He called out the actor, Prashanth by his character name, ‘Odubari’ and the character spoke his lines.

![](image_rsrc84H.jpg)

Lingaraj spoke to Seema in a hushed tone.

“Now, every character in the play, once he gets into the character has a character name.”

The director Nithin then called Prashanth by his character name, ‘Odubari’ and gave him a few lines.

Lingaraj continued.

“A file descriptor if you will. The dialogue writer opens this file, that is reads the dialogues by calling him, by his character name and asking him to tell the dialogue and even adds some dialogues. And even though the lines are meant for the character, Prashanth does remember them in his real life. This is like the read and write operation.

So, if it helps you remember,

The person Prashanth. A normal file.

Prashanth as ‘Odubari’. A descriptor.

Using the character name to write dialogues, append or remove etc. can be thought of as a parallel to the read() and write() system calls.”

Lingaraj took this opportunity to tell another story from his life.

“I once wanted to act in a play when I was in the city. There was a call for auditions from director Ranganath which I saw online. I caught an autorickshaw and told the auto driver that I wanted to go to Director Ranganath’s house and the area in which he lived. They had sent the audition lines via email and I practised them in the autorickshaw. Then I reached a big house with a lawn. I saw a lot of people waiting. I asked somebody who looked like the manager to let me meet Director Ranganath. He asked me to wait. I saw people of all ages and then I saw the lawn. I thought I would go there and practice, thus having an advantage over a![](image_rsrc84J.jpg)ll these idiots who weren’t practising.

I started practising in the lawn and rendered the monologue.

“What kind of a man are you? You are a corrupt person having cheated the government and the people. This is the time to expose you and let the world know your nefarious deeds.”

A lot of people came running and started hitting me. I managed to get the question out.

![](image_rsrc84K.jpg)

‘Is this Director Ranganath’s house?’
‘Yes, Ranganath, the director of the Transport and Travel department of the Government.’”

“I thought such stories were limited to your love life. Outside of your love life too, you have not done great.” said Seema.

“If you need a file descriptor, you need to open the file. There are several modes you can open them. Sometimes the dialogue writer wants to simply listen to the character’s dialogue, that is read-only. This has to be specified in the command within the parenthesis. The options are :

O_RDONLY Open for read-only : (Dialogue writer wants to only listen.)

O_WRONLY Open for write-only (Dialogue writer just gives the new dialogue. Doesn’t listen.)

O_RDWR Open for reading and writing (Dialogue writer both listens and gives new dialogues.)

| #include <fcntl.h>#include <sys/types.h>#include <sys/stat.h>int open(const char *path, int oflags);int open(const char *path, int oflags, mode_t mode); |

The char *path is the path of the file to be opened. The ‘oflags’ parameter consists of the above special access modes O_RDONLY, O_WRONLY and O_RDWR have to be used along with other options by ‘OR’ing (|) with other flags. Now, there are many scenarios in the rehearsal.

Let’s look at the oflags parameter:

| O_APPEND | Appends data to the end of the file. A new set of lines might need to be appended. Give the guy more dialogues, especially if he’s doing good. |
| O_TRUNC | Cut the file to zero, discarding existing content. This is one way to insult and say a guy’s not good at acting by removing all the lines given to him. |
| O_CREAT | Creates the file, if necessary, with permissions given in mode. A new character might have to be created. |
| O_EXCL | Used with O_CREAT , to make sure that only one instance of a file is created. If that file is already created, it won’t create a file. A new character like no other in the play might need to be created. |

Now, how do we find out the file descriptor number. The open system call returns the file descriptor as a positive integer. -1 if it fails.

When you use O_CREAT, you need to use the following further modes.

| S_IRUSR | Read permission, owner |
| S_IWUSR | Write permission, owner |
| S_IXUSR | Execute permission, owner |
| S_IRGRP | Read permission, group |
| S_IWGRP | Write permission, group |
| S_IXGRP | Execute permission, group |
| S_IROTH | Read permission, others |
| S_IWOTH | Write permission, others |
| S_IXOTH | Execute permission, others |

If you want to specify more options, use the | (pipe OR) option. I will show you how it works in a program in a little while. There is also the creat() system call which is

| #include <sys/types.h>#include <sys/stat.h>#include <fcntl.h>int creat(const char *pathname, mode_t mode); |

A  call  to creat() is equivalent to calling open() with flags equal to

O_CREAT|O_WRONLY|O_TRUNC.

Also, some functions set this global variable, ‘errno’ giving it an error number. I am quite a fan of this ‘errno’. When you ask a woman out, if she refuses, she can set the ‘errno’ privately. You can look it up and see why you were rejected. Once I wanted to go out with this woman, Roshni and gave her a letter with a form. The form included the ‘errno’ column. She said ‘no’ as usual in the letter. She was a programmer and knew this concept of ‘errno’ and that I was a fan of it. So I went and checked ‘errno’, it was written ‘errno’. I then asked her what it meant. She said ‘err…...no!’”

“It is easier to understand Linux than understand you.” replied Seema.

“Now, the number of characters a play can have in our community is limited to 16\. Same way, the number of files one process can open at a time is limited to 16\. It is defined by OPEN_MAX in limits.h. This can be changed.”

| #include <unistd.h>int close(int fildes); |

0 on success -1 on error.

This is how you close a file. I will show you a program named ‘filecopy.c’.

| #include <stdio.h>#include <unistd.h>#include <fcntl.h>#include <stdlib.h>int main(){  char c;  int in,out;  in=open("inputfile", O_RDONLY);  out=open("outputfile", O_WRONLY&#124;O_CREAT,S_IWUSR&#124;S_IRUSR);  while(read(in,&c,1) == 1)      {  ​printf("%c",c);  ​write(out,&c,1);      }close(in);close(out);    exit(0);} |

This uses the system call to copy from the inputfile (which is about 3.5MB) to the outputfile (which as of now does not exist), character by character, excruciatingly. This is like calling ceremony Seena to pass on a message and every time he comes, you tell him only one character of the message.

Compile the program using gcc.

| $ gcc filecopy.c -o filecopy |

You can measure how much time this program took by using the time command on the command line.

| $ time ./filecopy |

The output was displayed after some time.

| real​0m16.305suser​0m3.948ssys​0m12.353s |

“Maybe character by character is a wrong idea.” observed Seema.

“Yes, we did that as a lesson to him, thinking he would be exasperated, but he loved all the protocol nonsense.

If we change the read call to read and write in blocks, the speed will be boosted.

Just add this :

| char word[1024];while((nread = read(in,&word,sizeof(word))) > 0)write(out,&word,nread); |

So, the program would look like this.

filecopy_new.c

| #include <stdio.h>#include <unistd.h>#include <fcntl.h>#include <stdlib.h>int main(){  char c;  int in,out, nread;  in=open("inputfile", O_RDONLY);  out=open("outputfile", O_WRONLY&#124;O_CREAT,S_IWUSR&#124;S_IRUSR);  char word[1024];  while((nread = read(in,&word,sizeof(word))) > 0)  write(out,&word,nread);  exit(0);} |

The next system call we talk about is the ‘lseek’ call.

| #include <unistd.h>#include <sys/types.h>off_t lseek(int fildes, off_t offset, int whence); |

‘lseek’ points to a place in the file. So, offset is the distance from a point. And the offset is described with whence. The options for whence are :

| SEEK_SET | offset is an absolute position |
| SEEK_CUR | offset is relative to the current position |
| SEEK_END | offset is relative to the end of the file |

It’s like the dialogue writer can say, let’s go to the 5th dialogue, or the 3rd dialogue from where we were, or the penultimate dialogue.

‘lseek’ returns the distance from the beginning of the file in terms of bytes.

Here are some calls that tell you about files.

| #include <unistd.h>#include <sys/stat.h>#include <sys/types.h>int fstat(int fildes, struct stat *buf);int stat(const char *path, struct stat *buf);int lstat(const char *path, struct stat *buf); |

If you know the file descriptor, you can use ‘fstat’ to find out more info. If you know the path, use ‘stat’. And if the file is a link, use ‘lstat’ to get information about the link. Now, what is this information? It is a structure with the following components.

Here it is.

| st_mode |
| st_ino |
| st_dev |
| st_uid |
| st_gid |
| st_atime |
| st_ctime |
| st_mtime |
| st_nlink |

Now, suppose you are programming a part of Vijay’s brain and you feel there’s too much data, then you can take the help of your friend.

There’s the dup() system call where you can duplicate the file descriptor and get another file descriptor number for the same file. The number is the lowest available number which is free. This way, you can give another process the method to alter the file. You can work on one part and your friend on another.

“Well, all my friends are busy. So I will go at it alone. Thanks.”

“dup2 makes one file descriptor like another, but rather than using the lowest number, it uses a new number specified by you .” finished Lingaraj and showed her the calls.

| #include <unistd.h>int dup(int fildes);int dup2(int fildes, int fildes2); |

Lingaraj continued.

“Now, ceremony Seena had to be passed these messages for the good of society. Since the protocol was too expensive, we had message runners. Something like these food delivery partners. These message runners would collect messages from the people and then finally give ceremony Seena the messages to print in the evening. This way, everybody was happy.

So these high level calls are like these message runners, engaging ceremony Seena in an intelligent way without much overheads.

There are C library functions that save system overheads. They are :

| fopen |
| fclose |
| fread |
| fwrite |
| fflush |
| fseek |
| fgetc |
| getc |
| getchar |
| fputc |
| putc |
| putchar |
| fgets |
| gets |
| printf , fprintf and sprintf |
| scanf , fscanf and sscanf |

| #include <stdio.h>FILE *fopen(const char *filename, const char *mode); |

fopen opens the file named by the filename parameter and associates a stream with it. The mode parameter specifies how the file is to be opened. It’s one of the following strings:

| “r” |
| “w” |
| “a” |
| “r+” |
| “w+” |
| “a+” |

It is opened as a stream and not a file.”

“What’s the difference between a stream and a file descriptor?”

“The difference is in how the system sees the file. The stream is high level access. If you want control operations to be performed on files, you need to use the file descriptor. A file descriptor can simply send or receive data, but opening a stream makes it possible for formatted input and output.

It’s the difference between handling the situation delicately, with finesse. You talk with a particular manner, you show all kinds of etiquette. Opening a file descriptor is more about control.

It’s the different between something technical and poetic.

Moving on, if you are going through the files in Vijay’s head, and you come across a file that described Vijay’s memory of of date with a woman named Asha, what would you do.” asked Lingaraj.

“I would ask him, who Asha is.”

“And Vijay would answer without any sense of trepidation because he is a machine now. The more intelligent option would be to change the files. You can open them read only. Or update the file to change Asha’s name to yours. Or append, add details like Asha was not good for Vijay and she fought with him. Or completely remove all content.”

“I will completely remove all content.”

“Once again, the syntax to open the file is

| FILE *fopen(const char *filename, const char *mode); |

The C library function returns a pointer to the file stream in question.

| #include <stdio.h>size_t fread(void *ptr, size_t size, size_t nitems, FILE *stream);#include <stdio.h>size_t fwrite(const void *ptr, size_t size, size_t nitems, FILE *stream); |

In the just mentioned C library functions, the return from ‘fopen’ which is a file stream, is used to read and write. fread() and fwrite() return the size of the written or read data.

| #include <stdio.h>int fclose(FILE *stream); |

fclose closes the file. The file is closed even if fclose() isn’t called. But it’s not completely redundant. fclose() returns an integer which can be used to check for errors in case of failure.

| #include <stdio.h>int fflush(FILE *stream); |

This causes data on a file stream to be written immediately. No need to use it if you are using fclose() because a call to fclose() will use a flush operation.

| #include <stdio.h>int fseek(FILE *stream, long int offset, int whence); |

fseek will take you to the particular place in the file.

| #include <stdio.h>int fgetc(FILE *stream);int getchar(); |

fgetc reads the next byte as a character from a file stream.

getchar reads the character from the standard input.

| #include <stdio.h>int fputc(int c, FILE *stream); |

fputc puts a character into a file stream

| int putchar(int c); |

putchar puts a character to standard output.

| #include <stdio.h>char *fgets(char *s, int n, FILE *stream);char *gets(char *s); |

fgets writes characters to a string taking it from a file stream.

And gets? What does it do?” asked Lingaraj out of the blue.

“gets writes characters to a string taking it from standard input.” replied Seema diligently.

“From what I have heard, it does a lot more and it is advisable not to use it.” warned Lingaraj.

| #include <stdio.h>int printf(const char *format, ...);int sprintf(char *s, const char *format, ...);int fprintf(FILE *stream, const char *format, ...); |

This I hope you have covered in C.” asked Lingaraj.

“Yes, I will explain.

printf produces output on the standard output.

sprintf writes to a string.

fprintf to a specific stream.” said Seema.

“Ok. This is the format to print as you know. This, you will use a lot, so let’s visit it here.

| %d , %i |
| %o , %x |
| %c |
| %s |
| %f |

| #include <stdio.h>int scanf(const char *format, ...);int fscanf(FILE *stream, const char *format, ...);int sscanf(const char *s, const char *format, ...); |

scanf gets data from standard input.

fscanf from a file stream

and sscanf from a string.

Print reminds me of this. I have a friend from the city called ‘Dead body Doddanna.’” said Lingaraj.

“Makes me recoil in horror. What kind of a name is that?”

“There is a reason. He was the official police photographer. He used to photograph dead bodies. There came time to get married and he liked this girl. He was madly in love with her. But she was the suspicious type. She once came visiting his house for the first time and she left soon. We went and found Doddanna dejected and he had told us she had walked out and had stopped answering his calls. We did not need to search for an answer. On his wall he had taken the prints of all the dead bodies he had taken snaps of and had them pasted under the heading ‘My works.’”

“It would have been funny. Except for the dead bodies and his dejection.”

“More file navigation C library functions.

| #include <stdio.h>       int fseek(FILE *stream, long offset, int whence);       long ftell(FILE *stream);       void rewind(FILE *stream);       int fgetpos(FILE *stream, fpos_t *pos);       int fsetpos(FILE *stream, const fpos_t *pos); |

fseek sets the file position indicator for the stream and works similar to lseek.

ftell obtains the current value of the file position indicator for the stream pointed to by stream.

rewind sets the file position indicator to the beginning of the file.

fgetpos and fsetpos are equivalent to ftell() and fseek() with whence set to SEEK_SET

Of course for more information, you can always look in the man pages.

You can even remove a file with the remove function. Write it down, there might be lots of files to remove from Vijay’s head.

| int remove(const char *pathname); |

It’s not that streams and file descriptors are like oil and water,

| #include <stdio.h>int fileno(FILE *stream);FILE *fdopen(int fildes, const char *mode); |

fileno tells you the file descriptor of a stream

fdopen opens a file stream based on a file descriptor with a mode. fopen opened a file too, but using the name of the file.

So, file descriptors and streams have a link and it’s not a polarising path of choice.

What follows is the pseudocode. A way to structure a program. A pseudocode usually is more comprehensible, but since I am here with you, I guess we can skip the detailed guidance part. This is a program which uses the FILE stream to read from one file and write to the other. This isn’t a program because a full program might be spoon feeding you. I want you to write a program based on this information and try it out on your system.” Lingaraj showed her a text file in his laptop to Seema.

| Include the necessary header files.Start the main() functionDeclare two file streams, one for input and the other for output of the type FILE.Open the input file using fopen() in read mode. Assign the returning file stream to the declared file stream variable.Open the output file in write mode. And again assign the returning file stream to the declared variable.Use a while loop to get a character from the input file stream and write it to the output file using the output file stream until the End Of File(EOF) is reached.Exit. |

When you looked at my files in my directory you saw a lot of characters that looked like this. rwx.

They are permissions. I will show you my cooking directory.

Lingaraj opened the Cooking Directory on his laptop. He showed one

entry.

| Herbed bread rw_rw_r__ |

The first group of three characters is for the user, the second group is for the group of people who have access to the file. The third group is for others.

r stands for read. Which means I can read this file. w stands for write, it means I can write to this file. The missing bit x, is for executable. Since this is a text file, it cant be executed.”

Lingaraj looked into the distance. Seema sensed a story was coming.

“I once had a flock of sheep. I used to grant permissions by training the sheep with basic technology. I used to show photos of people to whom I had given contracts, to those sheep, and the sheep would trust these guys. The wool to one guy, milk to another, droppings to another.

![](image_rsrc84M.jpg)

Then I did not bother to maintain them. I used to let them roam free. The sheep would be so well trained that if a guy given the milk contract would try to get some wool, the sheep would bite him. So, a user cannot access a file that’s not meant for him.”

“I am guessing it didn’t end well. What happened?”

“One day I found them missing.”

“Somebody killed them for meat?”

“No. A neighbouring king drafted the sheep into his army.”

“Why?”

“Because the sheep bleat the droppings out of the enemies.

![](image_rsrc84N.jpg)

Seema seriously wished the laptop hadn’t fallen on Vijay’s head.

Lingaraj continued.

“

| #include <sys/stat.h>int chmod(const char *path, mode_t mode); |

This changes the mode of a file or directory.

| #include <sys/types.h>#include <unistd.h>int chown(const char *path, uid_t owner, gid_t group); |

This changes the ownership of the file or directory. Where do you get values for the uid_t and gid_t? From the getuid() and getgid() calls.

getuid and getgid return the user ids and group ids respectively. They are not integers, but of the type uid_t and gid_t, but they look like integers.

It’s like this. We have a dog called Stupid. I will demonstrate.” And Lingaraj took Seema outside.

“Stupid!” Lingaraj called out loud.

![](image_rsrc84P.jpg)

A dog suddenly appeared and looked playful.  Then it looked at Seema and tried to attack.

![](image_rsrc84R.jpg)

Seema was scared. The dog came near and was about to jump at Seema when Lingaraj shouted, “chown Seema”

The dog changed it’s attitude immediately and wagged it’s tail.

![](image_rsrc84S.jpg)

Seema gasped. Lingaraj explained.

“This dog, Stupid is good at playing and ferocious as well. Whenever a new person comes and if the dog tries to attack him, the people immediately use this command ‘chown name’. The dog then updates itself thinking he is the new owner and doesn’t attack him. He plays with him. Needless to say, I trained this dog. Just an example to teach you about ownership and ids.”

“You have stooped too low, I think it’s a ‘stoopid’ way to teach.

“That’s a good one.” They went back inside and Lingaraj resumed. He showed her some system calls.

| #include <unistd.h>int unlink(const char *path);int link(const char *path1, const char *path2);int symlink(const char *path1, const char *path2); |

unlink() is something like deletion. Except the space the file had been using is released after the last process using the file is terminated.

link() links one file with another. So, the file specified by path1 can be accessed by specifying path2\. If a file actually exists as you specified in path2, there will be an error. So, the file in path2 should not exist.

Of course, when you do ls the file specified by path2 will be listed, but will open the file specified by path1.

| #include <sys/types.h>#include <sys/stat.h>int mkdir(const char *path, mode_t mode);#include <unistd.h>int rmdir(const char *path); |

Makes and removes directories. You know the part about the mode when it comes to making directories. rmdir removes the directory only if it’s empty.  Of course, you have to try them out in your programs. All of it. I can’t teach you C programming. I only teach you the theory behind the system.

| #include <unistd.h>int chdir(const char *path); |

Changes the directory say, you are in the food directory in my system and want to move to my grandfather’s cocktail directory.

| #include <unistd.h>char *getcwd(char *buf, size_t size); |

To illustrate, look at this program:

getcwdir.c

| #include <stdio.h>#include <unistd.h>#include <stdlib.h>#include <unistd.h>int main(){    int nread;    char word[1024] = "Seema’s progress is good.";    char buf[1024];    int fd = open("/tmp/writeout.txt", O_CREAT &#124; O_WRONLY);    write(fd,&word,1024);    getcwd(buf, 1024);    printf("Current working directory is : %s\n", buf);    chdir("/tmp");    getcwd(buf, 1024);    printf("Current working directory is : %s", buf);} |

The output is

| Current working directory is : /home/Lingaraj/CprogsCurrent working directory is : /tmp |

And when the /tmp/writeout.txt file is opened, you will see:

| Seema’s progress is good. |

The directory functions are declared in a header file dirent.h. They use a structure, DIR. A pointer to this structure works like a file stream. Directory entries are returned in dirent structures.

The opendir C library function opens a directory and creates a directory stream. If successful, it returns a pointer to a DIR structure that can be used for reading directory entries. The members of this structure, defined in dirent.h are

| ino_t d_ino | File serial number |
| ulong_t d_offset | Actual offset of this entry |
| char d_name | Name of entry |
| ushort_t d_reclen | Length of this entry |
| ushort_t d_namelen | Length of the string in d_name |

So, you can access the directory entries one by one and list them. The point to remember is that opendir returns a pointer to a directory structure despite that fact that the function does not begin with f, like in fopen.

| #include <sys/types.h>#include <dirent.h>DIR *opendir(const char *name); |

opendir returns a null pointer on failure.

| #include <sys/types.h>#include <dirent.h>struct dirent *readdir(DIR *dirp); |

The above C library function returns a pointer to the next entry in the directory structure. Why not the current entry? Because opendir has already returned the first entry. And we need the entry after that.

| #include <sys/types.h>#include <dirent.h>long int telldir(DIR *dirp); |

It tells you the current position in a directory stream.

| #include <sys/types.h>#include <dirent.h>void seekdir(DIR *dirp, long int loc); |

This is used to set the directory entry pointer. The difference between this and readdir is that readdir returns the next entry, but this C library function can make readdir return the directory entry further down or back. But the location, loc has to be obtained previously using telldir().”

Seema thought for a while and asked.

“If I call telldir, get a position for loc and then again call seekdir and give it the same position, what am I achieving? The pointer stays at the same place.”

“Usually, you would have to create a loop, and get directory locations, loc using telldir for successive entries. Then, you can choose which loc value to pass to seekdir.

| #include <sys/types.h>#include <dirent.h>int closedir(DIR *dirp); |

The following program will display all the files in the current directory.

displaydir.c

| #include <unistd.h>#include <stdio.h>#include <dirent.h>#include <stdlib.h>void displayfiles(){    DIR *dp;    struct dirent *entry;    char dir[1024];    getcwd(dir, 1024);    if((dp = opendir(dir)) == NULL) {    printf("Cannot open the specified directory: %s\n", dir);    exit;    }    while((entry = readdir(dp)) != NULL) {    printf(" Name of file is : %s\n", entry®d_name);    }    closedir(dp);}void main(){    printf("Beginning to display contents of current directory.\n");    displayfiles();    exit(0);} |

The  ®  is actually a special character, but in the program you have to use ‘->’ , which is a minus sign followed by the greater than sign. We access structure members with a structure.member usually, but if it’s a pointer to a structure, we use pointer_to_structure->member.

The types of Errors you can get are :

| EPERM |
| ENOENT |
| EINTR |
| EIO |
| EBUSY |
| EEXIST |
| EINVAL |
| EMFILE |
| ENODEV |
| EISDIR |
| ENOTDIR |

| #include <string.h>char *strerror(int errnum); |

strerror is a C library function that tells you what the error was if you give it an error number. It returns a pointer to a string containing the message.

| #include <stdio.h>void perror(const char *s); |

This prints the latest error following the string you specify in s.”

Memory and command line arguments

Lingaraj began.

“We can use a file and store it in a particular memory location.”

An example would be putting a cocktail recipe in a particular location. You can even specify the location or leave it to the kernel. Usually, according to my grandfather’s instructions we place it near the pond on the rocks. You can even specify whether it can be read, written or executed. You can even allow other files and processes to access the memory location. Useful because whenever we put it on those rocks and come back to collect it, there would be more recipes added by people who would have experimented the previous night. Also, we find the inventors of this recipe still lying there in stupor.

![](image_rsrc84T.jpg)

The syntax is :

| #include <sys/mman.h>void *mmap(void *addr, size_t len, int prot, int flags, int fildes, off_t off); |

“Lots of arguments.” said Seema.

“Let’s imagine we have have a cocktail called the conflict arrestor and if you look at my grandfather’s text file for this, the contents of the file are :

‘This is a conflict arrestor where the parties indulging in a quarrel are given doses so they forget logic. This is achieved by…’”

“Forget the contents, tell me what the arguments are.” said Seema.

“

addr is the address in memory. Usually it is zero to let the kernel decide on its own.

len is the length of the memory block.

prot is what sets permissions :

| PROT_READ | You can read the segment. |
| PROT_WRITE | The segment can be written to. |
| PROT_EXEC | The segment can be executed |
| PROT_NONE | The segment can’t be accessed |

The flags parameter controls how changes made to the segment by the program are reflected in other places.

| MAP_PRIVATE |
| MAP_SHARED |
| MAP_FIXED |

filedes is the file descriptor.

off_t is the offset.

| #include <sys/mman.h>int msync(void *addr, size_t len, int flags); |

If there are changes, msync() updates the mapped file. Something like fflush.

It’s like saving.

The flags are :

| MS_ASYNC | An update be scheduled, but the call returns immediately. |
| MS_SYNC | Requests an update and waits for it to complete. |
| MS_INVALIDATE | Invalidates other mappings of the same file.(Useful when you want to update with fresh values just written.) |

Seema attempted to explain the flags.

“I can’t be as good as you at analogies or weird stories. But MS_ASYNC is like asking your subordinate to do a job, tell him and come back. MS_SYNC is like being there until the job is complete.

MS_INVALIDATE is like saying, “Don’t listen to anybody else for instructions.” to your subordinate.”

| #include <sys/mman.h>int munmap(void *addr, size_t len); |

The munmap releases the memory segment. Something you will find useful if Vijay’s memory is rife with information about a particular Sanjana or Savitri.”

Lingaraj showed her the screen.

“Look here.”

mapandunmap.c

| #include <string.h>#include <unistd.h>#include <stdio.h>#include <sys/mman.h>#include <fcntl.h>#include <stdlib.h>typedef struct {    int integer;    char string[1024];} RECORD;int main(){    RECORD record, *mapped;    int i, f;    FILE *fs;    fs = fopen("records.dat","w+");        record.integer = 1234;        strcpy( record.string , "Seema doesn't understand Linux.");        fwrite(&record,sizeof(record),1,fs);        fclose(fs);    f = open("records.dat",O_RDWR);    mapped = (RECORD *) mmap(0, sizeof(record),                          PROT_READ&#124;PROT_WRITE, MAP_SHARED, f, 0);                          printf("Number before changing the mapped value : %d\n", record.integer);    printf("Sentence before changing the mapped value : \n%s\n",     record.string);    mapped®integer = 5678;    strcpy( mapped®string , "Seema has learnt Linux.");    msync(mapped, sizeof(record), MS_ASYNC);    munmap(mapped, sizeof(record));    close(f);    fs = fopen("records.dat","r+");    fread(&record, sizeof(record),1, fs);    printf("Number after changing the mapped value : %d\n", record.integer);    printf("Sentence after changing the mapped value : \n%s\n", record.string);    fclose(fs);    exit(0);} |

This needs some explanation 

| #include <string.h>#include <unistd.h>#include <stdio.h>#include <sys/mman.h>This is an important include file.#include <fcntl.h>#include <stdlib.h>typedef struct {    int integer;    char string[1024];} RECORD;We define a structure of the type RECORD which consists of two members, an integer and a string.int main(){    RECORD record, *mapped;We declare record and mapped, which we will call later to store the return from mmap, to be structures of the type record. mapped points to the address where a record of the type RECORD is stored.    int i, f;    FILE *fs;    fs = fopen("records.dat","w+");        record.integer = 1234;        strcpy( record.string , "Seema doesn't understand Linux.");        fwrite(&record,sizeof(record),1,fs);        fclose(fs);We open a file stream because we need formatted output as we are copying the a string to the member in the structure.    f = open("records.dat",O_RDWR);    mapped = (RECORD *) mmap(0, sizeof(record),                          PROT_READ&#124;PROT_WRITE, MAP_SHARED, f, 0);We open a file called records.dat. It does not have to have a .dat extension. We use open because we need the file descriptor number to use mmap. The return is assigned to mapped, which as we have already declared points to a structure of the type RECORD and record.printf("Number before changing the mapped value : %d\n", record.integer);    printf("Sentence before changing the mapped value : \n%s\n", record.string);Here, we print the values before mapping. mapped®integer = 5678;    strcpy( mapped®string , "Seema has learnt Linux.");We change the values. Mind you, we are not changing the values of the structure members in the records.dat file directly. We are changing the mapped values, which should be reflected in the records.dat file.    msync(mapped, sizeof(record), MS_ASYNC);    munmap(mapped, sizeof(record));    close(f);We update the mapped memory and unmap. Then we close the file descriptor which had opened records.dat.    fs = fopen("records.dat","r+");    fread(&record, sizeof(record),1, fs);    printf("Number after changing the mapped value : %d\n", record.integer);    printf("Sentence after changing the mapped value : \n%s\n", record.string);    fclose(fs);    exit(0);}We then again open the file stream pertaining to records.dat because we need to read a structure stored in records.dat. We then proceed to read using fread and print the values which have been changed. |
| When we run it, the output is : |

Number before changing the mapped value : 1234

Sentence before changing the mapped value :

Seema doesn't understand Linux.

Number after changing the mapped value : 5678

Sentence after changing the mapped value :

Seema has learnt Linux.

| getopt() |

Suppose you send your friend on an errand to get a handbag. What  would you tell her?”

“I would tell her to get a handbag with a zip, a pocket for a small mirror, a compartment for my cell phone with a design involving red. The budget would be 750 rupees.”

“Okay, the fetchbag() will have instructions to get the handbag.

And all these other things you said are options. Now, these options would be

--zip

--pocket

--mirror

--cellphone holder

--design : red

--amount : 750 rupees

Notice the colons.”

“We’d use code. z,p,m,c,dred and a in short for all these options.” said Seema.

“In that case we’ll use getopt(). All you have to do is specify the code options prefixing a ‘-’ . The getopt() catches these options and makes it available to the program being called. Otherwise, you would have to use the argv list and differentiate between the arguments and the options using the ‘-’ prefixed before the option.”

If a friend you know is getting them, it’s fine. But if it’s someone like me, who does not necessarily know much about handbag options, I would have to have a program telling myself what to do at every step based on the options you specify. Let’s start with a C library function.

The syntax is :

| #include <unistd.h>int getopt(int argc, char *const argv[], const char *optstring);extern char *optarg;extern int optind, opterr, optopt; |

argc is the number of arguments, which includes the calling function.

argv is the list of arguments

optstring is the list of valid options acceptable by the program that has called getopt(). It means, the program has to know what kind of options the user is going to pass and the program better be ready with a switch case statement that takes an action based on the option passed.  

If a user like me who does not understand the handbag lexicon passes an option -b for a beer mug holder, then getopt() recognises this is beyond the scope of the program and puts it in optopt. So, a look at optopt would give you the options that were passed by a user ignorant of handbags.

Since this is updated each time getopt() runs, it is usually run in a loop.

optind is the index which helps getopt() the next time it is called. Since getopt() returns the next option character the program received, getopt() is run until getopt() returns -1, which means no more options are present. If it runs into an unknown option, it will return ?, the question mark character.

There might be further arguments to each of these options. For example, when you say budget, you have to specify the amount. That there exists a further argument to this particular option is indicated by ‘:’ the colon next to the option character. This specification argument for the option can also be accessed through the getopt() C library function through optarg. So, your program would be:

fetchbag.c

| #include <stdio.h>#include <unistd.h>#include <stdlib.h>#include <ctype.h>int main(int argc, char *argv[]){    int option;    while((option = getopt(argc, argv, "zpmcd: a:")) != -1)    {        switch(option) {        case 'z':        printf("So you want a handbag with a zip.\n");        continue;        case 'p':        printf("So you want a handbag with a pocket.\n");        continue;        case 'm':        printf("So you want a handbag with a mirror.\n");        continue;        case 'c':        printf("So you want a handbag with a cellphone holder.\n");        continue;        case 'd':        printf("You want a particular design. The design is %s.\n", optarg);        continue;        case 'a':        printf("You have a budget for this. The budget is %s.\n", optarg);        continue;        case '?':        if (optopt == 'a')        {        fprintf(stderr, "You need to be more specific for the option, %c.\n", optopt);        continue;        }        else if (optopt == 'd')        {        fprintf(stderr, "For this option too, you need to specify a design %c\n", optopt);        continue;        }else{            printf("Looks like you don't know much about handbags. %c is an invalid option.\n", optopt);        }        }    }} |

To explain,

| #include <stdio.h>#include <unistd.h>#include <stdlib.h>int main(int argc, char *argv[]){    int option; while((option = getopt(argc, argv, "zpmcd: a:")) != -1)We start a while loop and the getopt function where we list the valid options. After d and a, there is a : which indicates that it takes an argument to the option.    {        switch(option) {        case 'z':        printf("So you want a handbag with a zip.\n");        continue;        case 'p':        printf("So you want a handbag with a pocket.\n");        continue;        case 'm':        printf("So you want a handbag with a mirror.\n");        continue;        case 'c':        printf("So you want a handbag with a cellphone holder.\n");        continue;        case 'd':        printf("You want a particular design. The design is %s.\n", optarg);        continue;        case 'a':        printf("You have a budget for this. The budget is %s.\n", optarg);        continue;        case '?':        if (optopt == 'a')        {        fprintf(stderr, "You need to be more specific for the option, %c.\n", optopt);        continue;This seems a bit strange. We have already checked for ‘a’ and why do we again check for ‘a’ under the unknown single character case denoted by the question mark? This is true only if the input character is d or a and the program does not find an argument next to it. If there is an argument to the option, the previous case where we specify ‘a’ as an option would be true.        }        else if (optopt == 'd')        {        fprintf(stderr, "For this option too, you need to specify a design %c\n", optopt);        continue;        }else{            printf("Looks like you don't know much about handbags. %c is an invalid option.\n", optopt);        }This is if the single character is not either d or a, but an option input by a person ignorant of handbags.        }    }} |

If we run this,

| $ gcc fetchbag.c -o fetchbag$ /fetchbag -z -p -m -c -d red -a 750 |

The output is :

| So you want a handbag with a zip.So you want a handbag with a pocket.So you want a handbag with a mirror.So you want a handbag with a cellphone holder.You want a particular design. The design is red.You have an amount for this. The amount is 750. |

Next run :

| $ /fetchbag -z -p -m -c -d red -a |

The output is

| So you want a handbag with a zip.So you want a handbag with a pocket.So you want a handbag with a mirror.So you want a handbag with a cellphone holder.You want a particular design. The design is red../fetchbag: option requires an argument -- 'a'You need to be more specific for the option, a. |

So, you see if the user misses an argument for an option, the program informs the user.

Another run this time it’s me requesting a beer mug holder option:

| ./fetchbag -z -p -m -c -d red -a 750 -b |

The output is :

| So you want a handbag with a zip.So you want a handbag with a pocket.So you want a handbag with a mirror.So you want a handbag with a cellphone holder.You want a particular design. The design is red.You have a budget for this. The budget is 750../fetchbag: invalid option -- 'b'Looks like you don't know much about handbags. b is an invalid option |

But we see a drawback. Not that I am going to make the program foolproof, but if the red is missed as the argument to -d

| ./fetchbag -z -p -m -c -d -a 750 |

It shows this output.

| So you want a handbag with a zip.So you want a handbag with a pocket.So you want a handbag with a mirror.So you want a handbag with a cellphone holder.You want a particular design. The design is -a. |

What happened here was that the getopt assumed the next option to -d, input as -a as the argument to the option -d. The user has to input the correct sequence and be precise in his supplying of options. Otherwise it would again involve a lot of scanning of the argv array and finding out whether there is a ‘-’ next to the option and things like that.

If you want to make things simpler for me and use the long form of the options, then you use

| int getopt_long_only(int argc, char * const argv[],                  const char *optstring,                  const struct option *longopts, int *longindex); |

There is a structure of the type option, which is

struct option {

const char *name;

int         has_arg;

int        *flag;

int         val;

};

So, you can access these values through the structure.” said Lingaraj.

“Any story you have related to bags?”

“Yes.”

“And it turned out sad for you.”

“How did you guess?!” asked Lingaraj with surprise.

“Frankly, I didn’t even have to guess.”

“There was this girl’s birthday when I was in college.

![](image_rsrc84U.jpg)

She was very studious and good at making notes and many students wanted to learn from her notes. The final exams were just announced and they were scheduled a couple of weeks from then. One day, I came to know it was her birthday. So I wanted to wish her uniquely. She was having lunch on the lawn when I saw her bag lying. I then proceeded to tie the bag with balloons as she was busy talking. She didn’t notice.

![](image_rsrc84V.jpg)

I tied about a 100 balloons and yelled “Surprise!”. She turned around. I took my hands off the bag to show my handiwork. The bag flew away with the balloons. She failed in her exams.”

![](image_rsrc84W.jpg)

Seema seriously wished she could do something about Lingaraj’s love life. Lingaraj continued.

“The Linux environment. I have two resumes. In one, it says the following :

Smoke : No

Drink : No

Favourite TV shows : Documentaries

Previous affairs : Nil

Video games : No

and so on.

In the other :

Smoke : Occasionally

Drink : Occasionally

Favourite shows : Thrillers

Previous affairs : Many

Video games : Shooting zombies and so on.

Which do you think is the real one?”

“The second one obviously.” replied Seema with confidence.

“The second one is reserved for true friends. The first one for matrimonial alliances. So I keep switching between these two environments.

When I have to remember which is the value of a particular environment variable, I use this C library function

| char *getenv(const char *name); |

It tells the environment variable value of the variable given by

const char *name.

If I have to change a particular value, I use

| int putenv(const char *string); |

The string ought to be in this format.

name=value

For example,

drink=beer

This setting I use when I am with friends and have to ride back home on my horse.

“That’s because when you drink more, you are not stable, I suppose.”

“If I want to find out all the variable values, I use

| #include <stdlib.h>extern char **environ; |

It is an array of strings, that contain the list of variables. You can access them in a program one by one, using a while loop. Okay, see you tomorrow then.” said Lingaraj suddenly.

Time related functions

The next day, Seema took a walk early in the morning. She saw a group of about 4 to 5 people doing slow moving exercises.

She joined them and found it enjoyable. It was some time before she realised she was running late. Seema got ready as fast as she could and went and rang Lingaraj’s house doorbell. The doorbell was a simple bell contraption which did not run on electric power.

![](image_rsrc84X.jpg)

Lingaraj appeared near the door and Seema could see him. He lingered and though he saw Seema, he took about 5 minutes to open the door.

“Why did you open the door so late?” asked Seema with a hint of anger.

![](image_rsrc84Y.jpg)

“No. You were late. You started it. Please come inside.”

After Seema had settled, she told Lingaraj.

“I did some slow moving exercises.”

“Since we are on the topic of time,
There is this time system call, which tells you, how many seconds have elapsed since Jan 1 1970.”

“In seconds? That’s inconvenient.”

Lingaraj showed her the screen.

| #include <time.h>time_t time(time_t *tloc); |

It returns an integer of the type time_t as defined in time.h and if you specify a location in the form of tloc, it stores the value there.

So, if you have to find the time taken between two tasks, you invoke the time system call twice and then proceed to subtract one from the other. It’s just number of seconds. You said the time_t is inconvenient, but if it was in hours, minutes and seconds, and you had to subtract them?”

“I see.”

Lingaraj again showed her the screen which had this.

| #include <time.h>double difftime(time_t time1, time_t time2); |

This will give you the difference between two time durations. Recommended.”

“But all this is in seconds. I want a way to see the time in hours, minutes, etc.” said Seema. Lingaraj showed her another C library function.

| #include <time.h>struct tm *gmtime(const time_t timeval); |

This takes your time and gives you a structure which has

| tm | Member Description |
| int tm_secint tm_minint tm_hourint tm_mdayint tm_monint tm_yearint tm_wdayint tm_ydayint tm_isdst | SecondsMinutes, 0-59Hours, 0-23Day in the month, 1-31Month in the year, 0-11 (January = 0)Years since 1900Day in the week, 0-6 (Sunday = 0)Day in the year, 0-365Daylight savings in effect |
| #include <time.h>struct tm *localtime(const time_t *timeval); |
|  |  |

This gives you the local time. gmtime() gives the Greenwich Mean Time.

| #include <time.h>time_t mktime(struct tm *timeptr); |

This converts a broken down structure to raw time.

“Who would need that?”

“My grandfather used to comfort people.”

“By handing out cocktails?”

“Not just that. When people used to go to him and tell him their problem, he used to say, “You have 1261440000 seconds to live”.

“You say great grandfather sometimes and grandfather.”

“He was my grandfather…..but he was great. ”

“Thank God I missed him.”

“1261440000 seconds is a lot actually, 40 years. But it seems like less. Made people forget their worries.

Another time command is used on the command line to run programs and calculate system resource usage.

| $ time ./a.out |

| #include <time.h>char *asctime(const struct tm *timeptr);char *ctime(const time_t *timeval); |

‘asctime’ and ‘ctime’ return strings that are human readable.

If you want to print time, there’s a tool better than ‘printf’ for time related outputs.

| #include <time.h>size_t strftime(char *s, size_t maxsize, const char *format, struct tm *timeptr); |

char *s is the resultant string.

format is where you specify the formatting, the % symbols etc.

You can use the ‘strptime’ function, which takes a string connoting a date

and time and creates a ‘tm’ structure representing the same date and time:

| #include <time.h>char *strptime(const char *buf, const char *format, struct tm *timeptr); |

The buf is the string.

Temporary files

Lingaraj began the topic.

“Let’s talk about temporary files. Sometimes you might need to create temporary files.

| #include <stdio.h>char *tmpnam(char *s); |

It returns a string which is a unique filename not present on the system. It also updates it in the string ‘s’. But the problem is another program can create a file with the same name later, without using the above C library function, but before you start using it.

| #include <stdio.h>FILE *tmpfile(void); |

The above C library function creates and opens a file with the unique name and returns a file stream for immediate use, so the risk of another program creating a file by the same name is reduced.

| #include <stdlib.h>char *mktemp(char *template); |
| int mkstemp(char *template); |

If you want the new filename to adhere to a pattern or template, use the just mentioned C library functions. The template is whatever you want followed by six X characters. The six X characters are replaced to give a unique file name.

The difference between ‘mktemp’ and ‘mkstemp’ is that ‘mktemp’ gives just the file name. ‘mkstemp’ returns a file descriptor after opening the file. However it is advisable to use only tmpfile() and mkstemp().

User ids and groups

Lingaraj brought up a new topic.

“User information. The system call which gives you the ‘uid’, that is the user id of the person is

| #include <sys/types.h>#include <unistd.h>uid_t getuid(void);char *getlogin(void); |

The ‘getuid()’ system call returns the User ID with which the program is associated. This is usually the UID of the user who is running the program.

The ‘getlogin()’ C library function returns the login name of the current user.

| #include <sys/types.h>#include <pwd.h>struct passwd *getpwuid(uid_t uid);struct passwd *getpwnam(const char *name); |

You can get a lot of details about the user whose ID or name you know. The above C library functions return a structure of the type ‘passwd’. Accessing the contents will give you the details.  You know how to access a structure I suppose, having read C.”

“Yes.”

“The members of the passwd structure are :

| Member | Description |
| char *pw_nameuid_t pw_uidgid_t pw_gidchar *pw_dirchar *pw_gecoschar *pw_shell | The user’s login nameThe UID numberThe GID numberThe user’s home directoryThe user’s full nameThe user’s default shell |

You can fetch successive entries:

| #include <pwd.h>#include <sys/types.h>void endpwent(void);struct passwd *getpwent(void);void setpwent(void); |

‘getpwent’ returns a structure with a single user entry. The first time you call it, it returns the first entry. The second time you call, the second entry. So no need to have a variable and increment a value each time.

‘endpwent’ stops this C library function. ‘setpwent’ sets the position to the start.

| #include <sys/types.h>#include <unistd.h>uid_t geteuid(void);gid_t getgid(void);gid_t getegid(void);int setuid(uid_t uid);int setgid(gid_t gid); |

You can use ‘getgid’ to get the group id of the user/program. ‘setuid’ can only be used by the superuser or root, but it is cautioned against as once you change the user id of the process to something less privileged, it is not possible to get it back. This is like a king goes undercover to roam in his kingdom and when he comes back, the guards won’t let him enter. So, generally, seteuid which sets the effective user id is used.

I will show you a simple program.” he said and showed a program.

passwdent.c

| #include <sys/types.h>#include <pwd.h>#include <stdio.h>#include <unistd.h>#include <stdlib.h>int main(){uid_t userid;gid_t groupid;struct passwd *password;userid = getuid();groupid = getgid();printf(“User is %s\n”, getlogin());printf(“User IDs: User id is %d, Group id is %d\n”, userid, groupid);password = getpwuid(uid);printf(“User ID passwd entry shows the following data :\n Name is %s, User id is%d, Group id is %d, Home Directory is %s, The shell is %s\n”,password®pw_name, password®pw_uid, password®pw_gid, password®pw_dir, password®pw_shell);exit(0);} |

Do you get it? It’s a simple reading of the password structure.”

Seema saw it for a couple of minutes before saying she did.

“

| #include <sys/utsname.h>int uname(struct utsname *name); |

The uname system call writes host information to the structure pointed to by the name structure of the type ‘utsname’.  When I say structure of the type, it simply means a structure containing the same fields as that defined in the relevant header file. The ‘utsname’ structure is defined in ‘sys/utsname.h’. It must contain at least these members:

| char sysname[] | The operating system name |
| char nodename[] | The host name |
| char release[] | The release level of the system |
| char version[] | The version number of the system |
| char machine[] | The hardware type |

| #include <unistd.h>int gethostname(char *name, size_t namelen); |

This system call writes the hostname onto the string name. The ‘namelen’ is the least size that is assumed.

“Why is this important? We usually know the host’s name.”

Lingaraj remembered something and decided to tell Seema. Seema braced for another of his stories.

“When I was working as a software engineer, some 10 of us went to this hotel. We saw a party inside one of the halls and decided to gatecrash. We were working for Greaterthanall firm. The party was by a company called Some Software Solutions. They were celebrating success in a project. Since there were a great number of people and we were dressed in formal attire, nobody suspected that we were from a different company.

But we had a flight at 12 in the night and we didn’t want to miss the flight also. We got drunk and did not realise the passage of time.

![](image_rsrc84Z.jpg)

At 11, it hit me that we had only an hour to catch the flight. I tried to look for my friends, but they had merged among the crowd. So I went on stage where the DJ was playing. There were about 300 people in there. I spoke to the DJ, but he couldn’t hear with the noise. So, I signalled him to stop the music. I was too high by then and I took the mic.

![](image_rsrc850.jpg)

‘People from Greaterthanall firm, we have a flight to catch at 12, so let’s leave from here.’

Everybody started staring.

![](image_rsrc851.jpg)

Then it hit me. That is why it is important to use gethostname().

Moving on, let me show you this program. Works the same way as the program with the password file, except the structure from which we get the details from are different.

compdetails.c

| #include <sys/utsname.h>#include <unistd.h>#include <stdio.h>#include <stdlib.h>int main(){char machine[512];struct utsname comp_details;gethostname(machine, 511)uname(&comp_details);printf(“The machine host name is %s\n”, machine);printf(“The System is %s on %s hardware\n”, comp_details.sysname, comp_details.machine);printf(“The nodename of the machine is %s\n”, comp_details.nodename);printf(“The version is %s, %s\n”, comp_details.release, comp_details.version);exit(0);} |

Now, logging.

| #include <syslog.h>void syslog(int priority, const char *message, arguments...); |

It’s a log message. But future civilisations might see it as history and try to recreate the ethos of the age based on your unique case alone. It’s something like a diary, except action about where these messages go is taken depending on the priority. The options for priority are these.

| LOG_EMERG |
| LOG_ALERT |
| LOG_CRIT |
| LOG_ERR        |
| LOG_WARNING |
| LOG_NOTICE |
| LOG_INFO |
| LOG_DEBUG |

| void openlog(const char *ident, int logopt, int facility); |

If you want to ‘customise’ the way the messages are logged, you can use this C library function.

‘ident’ is what you can prepend to messages, like “Seema’s activity was: ”.

The facility parameter records a default facility value to be used for future calls to ‘syslog’.

The ‘logopt’ parameter configures the behaviour of future calls to ‘syslog’.              

| int setlogmask(int maskpri); |

setlogmask is used to control the priority of the log messages.

See the following program.

logmesg.c

| #include <syslog.h>#include <stdio.h>#include <stdlib.h>#include <dirent.h>int main(){DIR *dir_type_ptrdir_type_ptr = opendir(“Nonexisting_dir”);if (dir_type_ptr = NULL){syslog(LOG_ERR&#124;LOG_USER,“Tried to open a non existing directory.\n”);exit(0);}} |

If run, this program will write the message to the file /var/log/syslog file. You can open and see after you run the program.”

Resources and limits

Lingaraj began speaking.

“A program, a set of system calls to set limits on others who are using Vijay’s resources and set your priorities on him. Would you like that?”

“Vijay is a grown man, a machine or not, he can decide for himself. But yes, I would like to learn these calls.”

“

Some common limits on the Linux system are :

| NAME_MAX |
| CHAR_BIT |
| CHAR_MAX |
| INT_MAX |

So, to play around with these limits you need system calls.

| #include <sys/resource.h>int setpriority(int which, id_t who, int priority);int getrlimit(int resource, struct rlimit *r_limit);int setrlimit(int resource, const struct rlimit *r_limit);int getrusage(int who, struct rusage *r_usage);int getpriority(int which, id_t who); |

‘id_t’ as you know is a special type of integer used for user ids and group ids.

‘int which’ tells you whether the id is a user id or a process group id or a process id.

‘int priority’ is the priority value, an integer between -20 and +20. The default is 0.

‘r_limit’ is a structure, containing pointers. 

| rlimit |
| rlim_t rlim_cur |
| rlim_t rlim_max |

The soft limit, well you can think of it as something which gives errors, and a hard limit causes the program to terminate. If Vijay attends a lot of parties, I guess you can use this to set a limit. Allow him only to have only limited drinks.”

Seema wondered whether Lingaraj was going a bit too far with his comments about the relationship she had with Vijay. But Lingaraj was too nice a guy for her to chide him. Lingaraj continued.

“The hard limit is more than the soft limit. The hard limit is say, how much a person can drink. Prabhu’s hard limit is 750 ml. But his wife allows him to drink only 180 ml per day. This is the soft limit.

There might be other considerations too for imposing limits, like rationing. Other people might need to drink too.

You can drink, but you dare not

You can drink, but you care a lot

Hard and soft limits

Don’t matter if your heart fits

Only a superuser can increase the hard limit, say like a doctor who can increase the liver capacity. Otherwise, a normal user can only reduce the soft limit.

These are the resources with Parameter Description

| RLIMIT_AS |
| RLIMIT_CORE |
| RLIMIT_CPU |
| RLIMIT_DATA |
| RLIMIT_FSIZE |
| RLIMIT_NOFILE |
| RLIMIT_STACK |

The ‘rusage’ structure contains two more members which are again structures that are of the type ‘timeval’. It’s members are

| ru_utime |
| ru_stime |

| int setpriority(int which, id_t who, int priority); |

Sets the priority of the process.

| getpriority(int which, id_t who); |

Returns the priority value.

| getrlimit(int resource, struct rlimit *r_limit); |

Returns the limit value of one of the resources like RLIMIT_CPU.

r_limit consists of hard limit and soft limit values.

| setrlimit(int resource, const struct rlimit *r_limit); |

sets the values of soft and hard limits.

| int getrusage(int who, struct rusage *r_usage); |

Gives the user and system times spent for a process.

‘who’ is either

| RUSAGE_SELF |
| RUSAGE_CHILDREN |

Data Management

Lingaraj spoke.

Let’s talk about how memory is managed in Linux. The virtual memory. It’s an abstraction. Meaning it is organised and made to look very orderly and accessible.

| #include <stdlib.h>void *malloc(size_t size); |

size_t size is of the type unsigned long int

Imagine a warehouse which operates in your city. Memory in Linux is like the where of the warehouse.

Suppose I want to store 50 kgs of sandalwood and I book 10 ft by 10 ft in a warehouse for it. The warehouse guy, let’s call him warehouse Varadaraj, will store it in the warehouse and give me the receipt.

![](image_rsrc852.jpg)

Now, I have 10 ft by 10 ft for the sandalwood. I don’t usually ask him the location of the physical space inside the warehouse. I can find out if I ask him. But I do not necessarily have to.

So, the 10 ft by 10 ft is the memory quantity,if you will. I got it allocated through ‘malloc()’.

I can’t put elephant dung in a room in the warehouse and ask Varadaraj for the item placed in the next room. He is going to remove me from the system instantly. I won’t even get my elephant dung back.

I can’t write a program which queries other addresses in memory that is not the program’s concern.

Similarly, I cant ask for 10 ft by 10 ft space and have a wooden giraffe sculpture that is 12 feet in length. So I can’t write a program which tries to write beyond it’s allocated individual address space.

If the warehouse is small, say if it’s a startup and there’s not enough space available for extra orders, the warehouse guy, Varadaraj takes the extra items to his house to store them. But of course, he does not tell me that. If he’s done that with my order, I can see that the item if asked for takes more time to be delivered.

The using of the disk drive is called the swap space.

If he feels an item will not be used for some time, then too, he would move the item to his house. If I go to the warehouse and ask for it, he will move it to the warehouse again from the back, to give me the impression that it was in the warehouse all along and then give it from there.

Calling malloc enables the ‘malloc’ library to look after memory.

| #include <stdlib.h>void free(void *ptr_to memory); |

It’s like telling the warehouse you are done with the space and don’t need it any more. Of course, after using free, you cannot try to access that space again.

| #include <stdlib.h>void *calloc(size_t number_of_elements, size_t element_size); |

‘calloc’ allocates space for an array of structures.

‘element_size’ is the size of each structure.

| void *realloc(void *existing_memory, size_t new_size); |

‘realloc’ alters the size of a previously allocated memory. It returns a void pointer to the updated memory.

Like it’s simply a request to the warehouse to allocate a bigger space. He might allocate it next to the space already given or in some other place.

Let’s look at something that shows what memory allocation is about.”

Lingaraj showed her a program.

memory_less.c

| #include <unistd.h>#include <stdlib.h>#include <stdio.h>int main() {    char *some_memory;    int exit_code;    some_memory = (char *)malloc(5);    if (some_memory != NULL) {        sprintf(some_memory, "Will all this be printed?\n");        printf("%s", some_memory);        exit_code = EXIT_SUCCESS;    }    exit(exit_code);} |

This should be straightforward. We have allocated some memory with malloc, which is 5 bytes. For a string. some_memory is a pointer to this string. We print the string to some_memory, and then print the string stored at some_memory.

The output is

| malloc(): corrupted top sizeAborted (core dumped) |

It is not much of an output, but it shows since we allocated only 5 bytes, it could not handle such a big string which is more than 20 bytes long.

So, we change the program this time allocating 30 bytes.

The output then is :

| Will all this be printed? |

File Locking

“Let’s move on to file locking.

When I was living in the city, I lived in an apartment block. Water was scarce and there was a huge queue for the solitary tap. We used to stand in the queue for hours. This guy, Lock Lakshman used to come with three buckets. Lest others might help themselves to his third bucket which was filled while he was carrying two buckets up the stairs, he used to spit in them. Nobody would touch it.

![](image_rsrc853.jpg)

File locking reminds me of this.

Linux too kind of achieves locking. It can be either for a complete file, or a region of the file. Lock Lakshman’s locking method is not binding on the person who wants to carry away his bucket. It is not mandatory. The person who intends to carry off the bucket of water needs to cooperate. So, there are cooperative locks and mandatory locks. 

fcntl is pretty useful for not only file locking, but also other other things like modifying files, etc.

| int fcntl(int fildes, int command, struct flock *flock_structure); |

The command can be :

| F_GETLK |
| F_SETLK |
| F_SETLKW |

The flock structure :

| short l_type |
| short l_whence |
| off_t l_start |
| off_t l_len |
| pid_t l_pid |

‘short l_type’ options :

| F_RDLCK |
| F_UNLCK |
| F_WRLCK |

The command ‘fcntl’ returns -1 on failure.

When the program ends or the file descriptor is closed, all locks are cleared.

Don’t use ‘fread’ or ‘fwrite’ during a file locking process. Use read and write. This is because fread or fwrite buffers, that is places more bytes to be read or written in the buffer.”

There is also this C library function

| #include <unistd.h>int lockf(int fildes, int function, off_t size_to_lock); |

The options for function are :

| F_ULOCK |
| F_LOCK |
| F_TLOCK |
| F_TEST |

These locks are advisory in nature, that is programs have to have the courtesy to check for locks and respect the lock.

I will show you two programs, one that locks a region of a data file, between so and so bytes and the other that proceeds to see whether it can get a lock on that region. Firstly, we will test for exclusive access. lock_reg_ex.c

| #include <unistd.h>#include <stdlib.h>#include <stdio.h>#include <fcntl.h>const char *file_with_regions = "/tmp/test_lock";int main() {    int fd;    int count;    char *fill_string = "Seema";    struct flock region;We make the important declarations and also decide that the test file will be filled with “Seema”. We declare a structure, region of the type flock, which will hold details about the locking, unlocking or testing.        int res;    fd = open(file_with_regions, O_RDWR &#124; O_CREAT, 0666);    if (!fd) {        fprintf(stderr, "Unable to open %s.\n", file_with_regions);        exit(EXIT_FAILURE);    }We open, sensibly with open and not fopen for reasons I stated earlier.​for(count = 0; count < 100; count++) {        (void)write(fd, fill_string, 1);    }We just fill it with the word “Seema”.    region.l_type = F_WRLCK;    region.l_whence = SEEK_SET;    region.l_start = 40;    region.l_len = 10;We use the F_WRLCK which is the write lock or the exclusive lock.    printf("Process %d locking file\n", getpid());    res = fcntl(fd, F_SETLK, &region);We call fcntl for the opened file with file descriptor fd, use the SETLK to create a lock and specify the region structure.    if (res == -1) fprintf(stderr, "Failed to lock region.\n");    sleep(20);    printf("Process %d closing file\n", getpid());       close(fd);    exit(EXIT_SUCCESS);} |

We can obviously test it by writing a program that accesses the same file, and proceeds to query using fcntl whether a lock exists and also whether a new lock can be obtained or not.

lock_reg_ex_test.c

| #include <unistd.h>#include <stdlib.h>#include <stdio.h>#include <fcntl.h>const char *file_with_regions = "/tmp/test_lock";#define SIZE_INCREMENT 5int main() {    int fd;    int res;    struct flock region_of_interest;    int start_byte;    fd = open(file_with_regions, O_RDWR &#124; O_CREAT, 0666);    if (!fd) {        fprintf(stderr, "Unable to open %s for read/write", file_with_regions);        exit(EXIT_FAILURE);    }    for (start_byte = 0; start_byte < 99; start_byte += SIZE_INCREMENT) {        region_of_interest.l_type = F_WRLCK;        region_of_interest.l_whence = SEEK_SET;        region_of_interest.l_start = start_byte;        region_of_interest.l_len = SIZE_INCREMENT;        region_of_interest.l_pid = -1;    Before we test, we fill the structure details. We increment in a value of 5 bytes        printf("Testing for exclusive lock on region from %d to %d\n",               start_byte, start_byte + SIZE_INCREMENT);        res = fcntl(fd, F_GETLK, &region_of_interest);        if (res == -1) {            fprintf(stderr, "F_GETLK failed!\n");            exit(EXIT_FAILURE);        }        if (region_of_interest.l_pid != -1) {            printf("No opportunity to lock exists by the process : %d\n", getpid());            printf("Because of a lock by another process.\n");            printf("The details including the process number of the locking process are :\n");    printf("\tl_type %d, ", region_of_interest.l_type);    printf("l_whence %d, ", region_of_interest.l_whence);    printf("l_start %d, ", (int)region_of_interest.l_start);           printf("l_len %d, ", (int)region_of_interest.l_len);    printf("l_pid %d\n", region_of_interest.l_pid);}        else {            printf("F_WRLCK - Opportunity to lock exists by this process with pid, %d\n", getpid());        }    }        close(fd);    exit(EXIT_SUCCESS);} |

We run the lock_reg_ex.c in the background

| $ ./lock_reg_ex.c & |

And in another terminal,

| $ ./lock_reg_ex_test.c |

The output in the first terminal is:

| Process 34974 locking fileProcess 34974 closing file |

The output from the second terminal is:

| Testing for exclusive lock on region from 0 to 5F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 5 to 10F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 10 to 15F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 15 to 20F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 20 to 25F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 25 to 30F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 30 to 35F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 35 to 40F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 40 to 45No opportunity to lock exists by the process : 34980Because of a lock by another process.The details including the process number of the locking process are :​l_type 1, l_whence 0, l_start 40, l_len 10, l_pid 34974Testing for exclusive lock on region from 45 to 50No opportunity to lock exists by the process : 34980Because of a lock by another process.The details including the process number of the locking process are :​l_type 1, l_whence 0, l_start 40, l_len 10, l_pid 34974Testing for exclusive lock on region from 50 to 55F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 55 to 60F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 60 to 65F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 65 to 70F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 70 to 75F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 75 to 80F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 80 to 85F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 85 to 90F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 90 to 95F_WRLCK - Opportunity to lock exists by this process with pid, 34980Testing for exclusive lock on region from 95 to 100F_WRLCK - Opportunity to lock exists by this process with pid, 34980 |

Databases

Lingaraj started talking.

“Let’s move on to databases. Databases are you know, used to store data. Parrot Paresh was a guy who went on to become a robber. He stole a lot of valuables from people and had trained the parrot to maintain the database. He had stolen my valuables too. All Paresh had to do was tell the name of the person who was robbed and the parrot would tell the details beginning with the person’s name, what the valuables were and where they were hidden. The police finally laid his hands on him and found the parrot he had trained. The police called me and showed me the parrot. There were other victims of the robbery there.

![](image_rsrc854.jpg)

The Inspector told Ravi’s name to the parrot. The parrot began churning out the details.

‘Name : Ravi.

Valuables : 2 diamonds, 4 gold necklaces, 6 pearl necklaces, 20 lakhs in cash.

Hidden under the oak tree at the top of Sohi mountain.’

said the parrot.

Then the policeman told my name to the parrot.

‘Name : Lingaraj.

Valuables : Film scripts and poems about how to improve the world.

Thrown in the gutter outside his house.’

So, the parrot has a database which can be requested using a name, which is the key.

When you create a database, two files are created, one with a .dir extension and one with a .pag extension. These constitute a pair which is identified by a single dbm pointer. You have to change them only through dbm routines.

The major functions are these.

| #include <ndbm.h>DBM *dbm_open(const char *filename, int file_open_flags, mode_t file_mode); |

File name is a name without an extension you give the database.

file_open_flags are ‘OR’ed with O_CREAT

‘mode’ is used to set permissions.

It returns a database descriptor.

| int dbm_store(DBM *database_descriptor, datum key, datum content, int store_mode); |

datum is a data type which has at least 2 members

void *dptr;

size_t dsize

The size specifies the size of the data and *dptr points to the stored data.

‘datum key’ is the key which we have touched upon in the parrot story, an identifier.

‘datum content’ is the actual content

‘store_mode’ : What happens if you try to store some data using a key that already exists. If it’s set to dbm_insert the value isn’t stored. However if it’s set to dbm_replace, the value is replaced.

| datum dbm_fetch(DBM *database_descriptor, datum key); |

”

“This fetches the data based on the key.” said Seema. Lingaraj continued.

“

| void dbm_close(DBM *database_descriptor); |

”

“Closes the database and removes process access to the specified database.

| int dbm_delete(DBM *database_descriptor, datum key); |

It deletes a particular record in the database.

| int dbm_error(DBM *database_descriptor); |

This checks for errors in the database.

| int dbm_clearerr(DBM *database_descriptor); |

This clears any error condition flags.

| datum dbm_firstkey(DBM *database_descriptor);datum dbm_nextkey(DBM *database_descriptor); |

This is used to access records in a sequence. That does it for databases.

Processes

“Let’s take a walk.” said Lingaraj.

They took a walk and went to a coconut grove. Seema was awestruck with the place and there were a lot of tall trees. There was some bee hives in the trees and Lingaraj told Seema he had got her here to talk about bees.

![](image_rsrc855.jpg)

“Bees are always doing something. The queen bee grants the requests of many bees. But there’s only one queen bee. The request could be ‘I got this nectar. Where do I put it?’

And the Queen bee’s response would be,

‘Nectar? Definitely not on the road.’”

Seema did not laugh and Lingaraj pointed out that nectar was a play on the word tar used in road construction. Seema still didn’t laugh. Lingaraj let it go.

“So each audience of a worker bee with the Queen bee is a time slice. The Queen bee tends to have Attention Deficiency Disorder. It masks it by giving a worker bee about 5 minutes, asks him to wait and moves on to the next bee, who might ask about how to tackle the bear. She might say,

‘Please bear with it.’

Of course, there will be many more bees in the Queen’s audience.

![](image_rsrc856.jpg)

It gives the impression that she’s handling them all at once. But it is not. One thing to understand is that all the bees perform all the tasks, but in different shifts called time slices. So, as a Queen is handling the request of one cook bee who wants to cook, she and all other bees are actively working on that. Then they pause that job and move on to the next job which could be stinging a human being for singing an oft repeated song. They surround him and as the man is in shock bracing for the sting, they stop and come back. Then, they take up a cleaning job inside the hive. Then they repeat all the jobs resuming from where they had paused. What tells them where they were, the position they were in when they had surrounded the human being, for instance, is the program counter of that process.

In Linux, the processor handles one job at a time, in time slices, but they all happen so fast, it gives the impression that it is doing all this at once.

“So, the Queen is like the kernel. And a worker bee’s request can be turned into an operation when the Queen demands subsequent action.” said Seema.

“Or you can call everything a process. Each process has a PID, a process identification number. There is a process which has a PID of 1. It’s called the ‘init’. It is called the father of all processes.

When the program is stored in memory, no program can change the code. It becomes read only. Other programs can share it.” said Lingaraj.

“It’s like when the Queen commands and puts an instruction on the decree board, nobody has the guts to change it. They can take photos of it and share it among themselves for they need to carry out the instructions. They dare not change the command. They let it bee.” said Seema.

Lingaraj laughed a sarcastic laugh.

“We also have shared libraries. Libraries are ready made codes. Like potato chips. You don’t cook them yourself, but you procure already made ones because it is used often.

If the Queen tells the bees to cook ‘Rava Idly’ and ‘Dosei’ and the procedure to make chutney, an accompaniment for both, is in a shared library, which the command makes a reference to. The instructions to make chutney is not specified for each dish. That is, it is not written in a way in memory where the ‘Dosei’ dish command also contains instructions on how to make chutney and the ‘Idly’ dish command also contains instructions on how to make chutney. The instructions to make chutney are loaded in only one instance.

Of course variables can’t be shared. For example if the garnish in Idly is spice powder and the garnish to Dosei is cilantro, you can’t have only one entry for garnish. You need two instances of garnish even though it is called garnish in both cases.

A process has :

| Its own stack space. |
| Its own environment space. |
| Its own program counter. |

Do a ‘ps -ef’ command to see more. Here you can see the

User id of the process.

The Process ID

Parent Process ID

The process scheduling information

Start time

Terminal

Time duration

The command which started the process

‘ps ax’ will also show you a column which tells you the state of the process. The process can be :

| S |
| R |
| D |
| T |
| Z |
| N |
| + |
| < |

For example the ‘init’ program starts a ‘getty’ program. Once the user logs in, the ‘getty’ passes control to the login program. This can allow log in and set up the environment according to the user and starts the shell. On exit, another ‘getty’ process is started by ‘init’.

There are some bees who are more important than the others. The Queen’s schedule contains more time for implementing important jobs like adding chemicals to get more yield of honey and less time for collective fitness. Similarly processes are given different time slices in the processor. A particular process can’t take more time than allocated.

How do we start a new process? We use the system C library function.

| #include <stdlib.h>int system(const char *string); |

The string is the command of the new process to be started. A system calls a shell, which in turn executes the command. So, if it’s a shell which is executing, the command ought to be what you can type on the command prompt. The ‘system’ C library function starts a new process whenever you specify a command. 

A parallel would be the ‘system’ call is like an agent, which gets things done by others. Suppose I have a home manager. I ask him to call a cook for a party and he does the cooking at home while I was in office. The home manager would charge his commission and get the job executed by the cook. The same way with plumbing, driving and standing in a queue to pay the bills.

But if you have an all rounder, who knows how to cook, knows how to drive and pay bills, it would be helpful.

There are many types. Some who accept only one argument. Some, that accept an array of arguments and some who ask you for the path.

| #include <unistd.h>char **environ;int execl(const char *path, const char *arg0, ..., (char *)0); |

The path is obviously where the command executable is stored.

*arg0, *arg1 etc are the arguments to the program being called. If you have written a program yourself, these arguments are the arguments to the main function in that. ‘(char *) 0’ tells the ‘execl’ C library function, the argument list is over. 

Now, the ‘execl’ class of C library functions, you can think of them as Mr All round Arun.

All round Arun was a valet I had. He knew everything. He was a good driver, a good cook, a film director, a rocket scientist and a plumber. Whenever I asked him to do a job, he would don that particular hat. My job became his job and he used to execute it very well.”

“You mean a new process wasn’t started? It was like you were doing it?” asked Seema.

“Exactly. When an exec class of functions, starts a new process, it uses the process ID of the calling process. Remember will execution in shell scripts? How my grandfather died and wanted my father to take over concoction duties. This is like the same thing, but as C library functions. And they call executable files.” said Lingaraj. He continued.

“Arun never even used to charge me anything because he was rich.”

“And what happened then? He died?”

“No, I fired him.”

“Why?”

“One day he wore my hat and started thinking he was me.  He ordered me around and I worked for him until I had an opportunity to take his hat off.”

The called process actually does away with the calling process. The calling process goes away.

| int execlp(const char *file, const char *arg0, ..., (char *)0); |

Here, path is replaced with file. This suggests that the command will automatically look for the file in the PATH variable. If the file isn’t in the path, you have to specify the full path name.

| int execle(const char *path, const char *arg0, ..., (char *)0, char *constenvp[]); |

Here, the e symbolises ‘extra’. Usually the environment the new process should run in. If not defined, the environment of the current process is used.              

| int execv(const char *path, char *const argv[]); |

Here, this function takes an array of arguments.

| int execvp(const char *file, char *const argv[]); |

The name of the file in the PATH or the complete path and an array is passed as an argument.

| int execve(const char *path, char *const argv[], char *const envp[]); |

Again, the  name of the file in the PATH or the complete path and an array as an argument along with the environment.

So, if there is a ‘p’ in the function, it will search in the path, ‘e’ means something extra, an environment and ‘v’ means an array.

| #include <sys/types.h>#include <unistd.h>pid_t fork(void); |

If you want Vijay to start another process whilst he is praising your relatives...”

“I will use Ctrl+C and Ctrl+V, Copy-paste.”

“Ctrl+C is a signal that will stop the foreground process. So, if you use Ctrl+C on Vijay, you will immediately stop his foreground process, which is praising your relatives.

The fork is like the copy paste for processes, but it assigns a different PID for each process that is spawned.

Why would you need to fork? To create a child process.

Anyway the fork returns the PID of the child process to the parent process. To the child process, it returns 0\. And in case of failure, it returns -1 to the parent process. This is very important in the context of programming. It gives us a way to know whether the program is in the parent process or in the child process. Hence of the type ‘pid_t’. So, when you fork, you create another instance of the process, a child process. If it fails, it returns -1\. The reasons it might fail are :

Too many child processes, the limit being specified by CHILD_MAX. When you see the ‘errno’, it will be EAGAIN.

If there’s no space in the process table or if there’s no memory, the ‘errno’ is set to ENOMEM.

| #include <sys/types.h>#include <sys/wait.h>pid_t wait(int *stat_loc); |

Let me mention it again. How do you find out if you are in the child process or the parent in the program execution? By the return value. In the child it is zero, in the parent, the ‘pid’ of the child process.

The parent process, the one which created the child process can enquire the status of the child program, whether it is running or has stopped using wait(). The status is stored in the location pointed by ‘stat_loc’. A list of statuses are :

| WIFEXITED |
| WEXITSTATUS |
| WIFSIGNALED |
| WTERMSIG |
| WIFSTOPPED |
| WSTOPSIG |

A parent process might have many child processes. And you would need to get status based on the Process ID of that child process.

| #include <sys/types.h>#include <sys/wait.h>pid_t waitpid(pid_t pid, int *stat_loc, int options); |

pid is the process id of the child process.

Now, options :

Same as that for wait() but one particular option, WNOHANG does not suspend the execution of the caller.

This system call returns zero, if the child process is still running. One error, it will return -1.

Errors in this system call happen if :

| There are no child processes |
| The call is interrupted by a signal |
| The option argument is invalid |

Another important thing to know is that if a program opens file descriptors, they are preserved even when fork or the exec family of functions is called.

When a child process is done executing, but the kernel waits to remove it from the process table because it’s parent process might enquire the status or something, it is called a ‘Zombie’ process. Until the parent process terminates or calls wait, the entry in the process table still remains. If the parent process terminates, the ‘init’ becomes the child process’ parent process.

Let’s look at a program. zmaker.c

| #include <sys/types.h>#include <sys/wait.h>#include <unistd.h>#include <stdio.h>#include <stdlib.h>int main(){    pid_t pid;    char *message;    int exit_code;    printf("Fork program starting\n");    pid = fork();    switch(pid)    {    case -1:        exit(1);    case 0:        printf("This is the child\n");        printf("With PID : %d\n", getpid());        exit(EXIT_SUCCESS);        break;        default:        printf("\n\nThis is the parent\n");        printf("With PID : %d\n", getpid());        sleep(30);        break;    }    exit(EXIT_SUCCESS);} |

The above program forks and creates a child process. And we can identify whether the process(when the program is running) is in the parent process or the child process. If the process ID is 0, it means it is the child process. It is immediately ended. The parent is allowed to continue for 30 seconds more. Then the program exits. Why did I do this? To show you a zombie process. A zombie process is a name given to the child process if it terminates before the parent process in case the wait() call is not called by the parent.

The wait as you know returns the status of the child process to the parent. When we run this program, we get the following output.

| This is the parentWith PID : 35916This is the childWith PID : 35917 |

At the other terminal, if you type

| $ ps -al |

Among other processes, you will find an entry :

| 1 Z  1000   35917   35916  0  80   0 -     0 -      pts/0    00:00:00 |

Notice the ‘Z’ that means Zombie process and the process number 35917\. Of course, you see 35916 as well, but that is the ppid, the parent process ID. It will show this process as a Zombie until the parent process finishes.

We rectify this, using wait.

zwait.c

| #include <sys/types.h>#include <sys/wait.h>#include <unistd.h>#include <stdio.h>#include <stdlib.h>int main(){    pid_t pid;    char *message;    int exit_code;    printf("Fork program starting\n");    pid = fork();    switch(pid)    {    case -1:        exit(1);    case 0:        printf("This is the child\n");        printf("With PID : %d\n", getpid());        exit(24);/*Here, we give an exit code to see whether it can be retrieved in the parent process. */        break;        default:        printf("\n\nThis is the parent\n");        printf("With PID : %d\n", getpid());/*   From here, lines are added */        int stat_val;        pid_t child_pid;        child_pid = wait(&stat_val);/*wait is called, which returns the pid of the child and also frees up resources. The child was showing as a zombie because it’s resources weren’t freed up.*/        printf("Child has finished: PID = %d\n", child_pid);        if(WIFEXITED(stat_val))         printf("Child exited with code %d\n", WEXITSTATUS(stat_val));Here, we use WIFEXITED to see if the child process terminated normally, and if so, we continue to display with what code the child process exited with using WEXITSTATUS(stat_val)        else        printf("Child terminated abnormally\n");        sleep(30);        break;    }    exit(EXIT_SUCCESS);} |

When we run this :

| This is the parentWith PID : 36960This is the childWith PID : 36961Child has finished: PID = 36961Child exited with code 23 |

So, the child process ID and the exit code were retrieved by the parent process.

And if we check with ps -al, there is no mention of the Zombie process despite the parent process running for 30 seconds more.

A good shell command is the pstree -p command with which you can see the process tree along with the process IDs . I suggest you try this on your own while running the above programs to see which process gave rise to which process.

Signals

Lingaraj began.

“There was this incident that happened in a shopping mall. I was trying to pick up a gift for my girlfriend when I noticed a young woman trying to select jewellery for her ears. She kept on trying various jewellery and we both could see each other in the mirror. I gave her signals on what she was trying out. She was trying out a pair of earrings when I gave her the thumbs down sign.

![](image_rsrc857.jpg)

She rejected it. The same thing happened with the next two tries and then she asked me why. I asked her to wait, took a course in sign language and came back. She was still there trying to get the right look. Then I started signalling her.

“What did you signal?” asked Seema.

Here’s a set of signal messages.

The very idea of earrings is wrong.

You are taking too much time to decide.

Please stop talking on the phone and try out something.

Somebody blocking the view in the mirror.

Repeating the same thing she wore without remembering it.

Throw a big rock at the mirror and shatter it because you have been standing there for ages and she can’t decide.

“And what happened?” asked Seema.

“She made a selection of about 8 pairs of earrings, 12 necklaces and 7 studs for the nose. And promptly disappeared. I would have too, but she had told the shopkeeper that I was her husband. The shopkeeper believed since I had made the selections. I had to pay from my girlfriend’s credit card as I was living off her at that time. I stayed with my girlfriend until the credit card bill arrived. I was eating ‘onion dosei’ she had made and I had to tear myself away from the dosei. She used to make such good onion doseis.” 

Seema saw Lingaraj had a catch in his throat and she was not sure whether Lingaraj was feeling emotional for the woman or the doseis.

Lingaraj recovered and continued.

“I told you about ‘Ctrl+C’. On Linux, it sends the SIGINT . If Vijay’s being erratic in behaviour, you can stop it using Ctrl+C. Unless Vijay can catch it.”

Here’s a list of some signals.

| SIGABORT |
| SIGALRM |
| SIGFPE |
| SIGHUP |
| SIGILL |
| SIGINT |
| SIGKILL |

| kill [options] <pid> [...] |

Can you guess what a kill command can do to a process?

“It kills it.” said Seema.

“It sends a signal to a process to kill it. And the kill command can send a signal that even tells the process to continue if it’s in a good mood.

If you don’t specify a signal, the default is TERM. Meaning, true to it’s name, the kill command will send a terminate signal to the process defined by ‘pid’. If the program doesn’t listen, the option -KILL definitely kills. BTW, the kill does not work on zombie processes.

If ‘pid’ is a negative number, the positive value of ‘pid’ will be treated as a process group. If it’s positive, the process id is indicated. If it’s -1, all processes will be sent the kill signal except ‘init’ and ‘inetd’.

The signal can be specified using the name or number. To see a list of available signals, use the

| kill -l |

command.

This was the kill command. There is a kill system call as well.

| #include <sys/types.h>#include <signal.h>int kill(pid_t pid, int sig); |

As you can see, it takes the pid of the process to be done away with and the signal to be sent. You can send the kill signal to only the process with the same user ID. You cannot send it to processes with a different user id. The superuser can kill though.

‘kill’ can fail and return -1 if :

If the signal specified is not a valid one, setting the errno EINVAL

If it doesn’t have permission, in which case errno is set to  EPERM

If the specified process doesn’t exist, thereby setting errno to ESRCH

“Why is it that only killing signals are sent. So negative. Why can’t there be an encouraging signal?”

“Imagine Vijay is thinking about beer with friends while your uncle is going on and on about how he fought off rogues when he was young. Would you want to encourage that beer process or kill it?” asked Lingaraj.

“I want to kill it with a -KILL option. But how do I encourage him to listen to my uncle.”

“You can set nice for that. The nice command.

| nice options command argument |

You can set a value like between -20 to 20.”

“Okay, I will use it to set a value of 20 to the command that says listen to my uncle’s story.”

Lingaraj thought for a moment. He appeared to be in a dilemma. The he spoke.
“Setting a high value with nice, you reduce the priority of the command. Lower value means higher priority. You can use ‘renice’ to change a process priority. Example :

| renice 10 13621362 being the process id. |

The signal() system call.

| #include <signal.h>void (*signal(int sig, void (*func)(int)))(int); |

You can provide actions for signals received or catch it using the signal command, which makes the process, either ignore it, use default behaviour or run a function in the program.

So, every signal’s response can be coded using the signal system call.

But then, you can forget it, because it is no longer being used.

I will just mention about pause.

| #include <unistd.h>int pause(void); |

It makes the process pause until a signal appears. In place of signal(), we have a more robust system call.

| #include <signal.h>int sigaction(int sig, const struct sigaction *act, struct sigaction *oact); |

Return values of sigaction.

0 if there’s no error.

-1 if there is an error. This happens if the signal is invalid or if the signal cannot be caught or ignored.

The ‘sig’ is the signal.

The ‘struct sigaction’ has within it, members that deal with a signal.

Some of the members of the structure ‘sigaction’ are:

void (*) (int) sa_handler    

What happens when a signal occurs? Will a function be called, or SIG_DFL, that is default action be taken? Or SIG_IGN which will ignore the signal.

sigset_t sa_mask  

The signals to block. What we are talking about here, is this. When a signal occurs, the handler function is called and runs to completion. If within that time, another signal appears, this robust system call, ‘sigaction’ can block the fresh signal.

int sa_flags

Signal Action Modifiers. It tells whether to get back into position to catch a new signal. When you set it to SA_RESETHAND, the ‘sigaction’ system call handles the signal once.

There are other flags too which are available in the man pages.  

‘oact’ is a location which will hold the previous signal action that was made.

| #include <signal.h>int sigaddset(sigset_t *set, int signo);int sigemptyset(sigset_t *set);int sigfillset(sigset_t *set);int sigdelset(sigset_t *set, int signo); |

These are C library functions. You can tell the program to specifically deal with one signal at a time or make a broad policy to deal with signals. So, you can make a set of all these signals and specify what to do. Also, there might be situations where your program is working on a signal received and another signal comes. So, you might need to suspend the function of this and kill the process. No need of confusion. You can handle all these signals using a signal set.

The signal set is of the type

sigset_t

So, you can fill your signal set with all the available signals through the sigfillset() C library function. Likewise, you can empty the set of all signals using the sigemptyset() C library function.

You can add individual signals to a set by specifying their numbers through sigaddset()

And you can delete individual signals from a set by specifying their numbers through sigdelset()

Also, you can find out if a signal is a member of a set by enquiry.

| int sigismember( const sigset_t *set, int signum) |

This returns 1 if the signal is a member of the set, 0 if it’s not and -1 on error.

| #include <signal.h>int sigprocmask(int how, const sigset_t *set, sigset_t *oset); |

The above system call is to change the process signal mask. If a signal is blocked by a process, it won’t be delivered, but will remain pending. A program can determine which of its blocked signals are pending by calling the C library function sigpending.

| #include <signal.h>int sigpending(sigset_t *set); |

This system call writes a set of signals into the signal set pointed to by set, that are blocked from delivery.. It returns 0 if successful, otherwise, -1 with errno set to indicate the error.

| #include <signal.h>int sigsuspend(const sigset_t *sigmask); |

The sigsuspend system call replaces the process signal mask with the signal set given by sigmask and then suspends execution. It will resume after the execution of a signal handling function.

Let’s look at a program that uses sigaction.

ayyo.c

| #include <signal.h>#include <stdio.h>#include <unistd.h>void ctrlc(int sig){    printf("I advise you not to stop me, %s\n", getlogin());}void shutdown_req(int sig){    printf("I am process %d and I know who is trying to kill me. It's you, %s\n", getpid(), getlogin());}/*void finish(int sig){    printf("This function is pretty useless because it is trying to handle a SIGKILL signal.\n");}*//*We declare the above three functions, one each for a particular signal, SIGINT, SIGTERM and SIGKILL. The function that handles SIGINT, ayyo works only once Ctrl+C is pressed because we have used the SA_RESETHAND flag. We print the relevant message and that is all this function does. */int main(){    struct sigaction act;    act.sa_handler = ctrlc;    sigemptyset(&act.sa_mask);act.sa_flags = SA_RESETHAND;    sigaction(SIGINT, &act, 0);    act.sa_handler = shutdown_req;    sigemptyset(&act.sa_mask);    act.sa_flags = 0;    sigaction(SIGTERM, &act, 0);/* This is irrelevant because a SIGKILL will kill the process immediately and it cannot be handled.      act.sa_handler = finish;    sigemptyset(&act.sa_mask);    act.sa_flags = 0;    sigaction(SIGKILL, &act, 0);    *//*Then the handler function is specified and the signal set, sa_mask is made empty. We don’t want any signals to block. Because anything you put here will not be delivered to the process. The flags whether SA_RESETHAND is needed is specified. In the first case, SA_RESETHAND is specified, which means the signal will be handled only once because the signal is not reset. If you want it to work every time, you need to reset the signal by including SA_RESETHAND.*/  while(1) {  printf("I am happy in my world!\n");  sleep(1);  }}/*This is the main part where the program keeps on printing in an infinite loop until the signal is sent. */ |

The output is:

| I am happy in my world!I am happy in my world!I am happy in my world!I am happy in my world!I am happy in my world!I am happy in my world!I am happy in my world!I am happy in my world!I am happy in my world!^CI advise you not to stop me, Lingaraj!I am happy in my world!I am happy in my world!I am happy in my world!I am happy in my world!I am happy in my world!I am happy in my world!I am happy in my world!I am happy in my world!I am happy in my world!I am happy in my world!I am happy in my world!I am process 41620 and I know who is trying to kill me. It's you, LingarajI am happy in my world!I am happy in my world!I am happy in my world!I am process 41620 and I know who is trying to kill me. It's you, LingarajI am happy in my world!I am happy in my world!I am happy in my world!I am happy in my world!^C |

So, you see for the second Ctrl+C, it got killed whereas for the SIGTERM process, it used the handler everytime.

Tomorrow, we will go to this exciting place.” said Lingaraj and finished the session. Seema went and called the doctor. There was a change in Vijay’s disposition and he was showing human like tendencies and Seema was convinced that he would come back to normal soon.

Threads and mutex

The next day, they took an 8 mile hike. They passed wonderful streams, waterfalls, through foliage and over cliffs without meeting a single person.

![](image_rsrc858.jpg)

They finally reached a small settlement where a few people were making threads.

“I brought you here to set up the context. Today, we will talk about threads.”

“Are you out of your mind? I am really worried and trying to get back to Vijay at the earliest and you are behaving like ceremony Seena.” said Seema with anger in her voice. After a while, Seema apologised. Lingaraj didn’t seem like he was hurt. He spoke.

“A thread is an execution slice.”

“I don’t understand.”

“I opened a hotel once. I used to get orders from Mysore and sometimes Hubli. So I used to set up a small operation there whenever the order came. I used to go there and cook. But the orders kept pouring in. So I started a franchise model and gave them to people in various districts of Karnataka. They used to inherit my model of work. Until one fateful day.”

This was the thing about Lingaraj Seema had noticed. He had to tell his life experiences whether he was the hero of it or not. Most of the times, he was not. Lingaraj continued with his story.

“I had given a franchise in Hubli. I had to meet this woman for a marriage alliance. That day, I received a complaint from a person that the food in my particular franchise in Hubli was not up to standards. I went to the franchise with my fiance the next day itself. I wanted to show off my fiat. I told the guy who had purchased the franchisee from me that a person had complained the food was bad and that I wanted to inspect. I asked them to bring the food. They brought me the food. I asked my fiance Nagashree to eat the food. We both ate, after we had eaten, I told the hotel manager, “The food is good, but there’s some smell.”

So the manager replied, ‘Sir you had a problem with yesterday’s food. So we got you yesterday’s food.’” finished Lingaraj.

“Phew! Man you have so much of history.”

“So, I wanted more control. Also, I realised there was a lot of spending. I had to share my brand identity, the website, etc. So, I closed down the franchise system and started opening branch offices. Of course, this is not a way to run businesses. It was my particular case.”

“I don’t know why you are telling me this.”

“The first case, where I used to set up a small operation there is akin to invoking a function in a program. My process managed it alone.

The second case where I gave out franchises was creating another process, say by invoking fork. A lot of information had to be duplicated. 

The third case was opening a branch office. Only information was shared and not duplicated. This is like executing a thread.

A thread is a part of a program that executes multiple times, but not as a function. If you work on two files at the same time, it is cumbersome for the kernel to use functions and run as a monolithic block. It can have another instance of a part of the code running, but not as a process where everything is duplicated. In thread execution, the program running gets it’s own stack and the new thread of execution gets its own stack and so, local variables. But it shares (please note not duplication, but a share) global variables, file descriptors, signal handlers, and its current directory state with the process that created it.

So whereas a franchise has it’s own financial bookkeeping, salaries, the branch office shares the financial books. A process duplicates while a thread shares and duplicating involves more resources.”

“Yes, now ‘reentrant’ code. A re-entrant function is one which can run, be interrupted and then be run again.

The same routine can be reused in different instances and the value of a variable for one instance might not hold good for other. So, if a routine alters the value of a variable and it is called again, it won’t remember it’s old set of values. It takes the value being sent by the calling program. 

In our community, the drinking age is 21\. Once my friend’s father, a history teacher, Ritesh who stuck to customs like sambhar sticks to shirts, was the bar owner. Nothing wrong with that, except he would never allow us into the bar. He used to get drunk and when we presented ourselves at the bar door, this was the conversation.

![](image_rsrc859.jpg)

‘Oh Lingaraj. How are you?’ he used to ask.

‘I am good Sir. I did well at programming and….’

‘I meant to ask, how old are you?’

‘25 uncle.’

‘Don’t lie to me. You are 20\. I remember you telling that to me.’

‘That was 5 years ago, Sir.’

‘So what? A record is a record. Get out of here.’

He wouldn’t have qualified for a reentrant routine. The only re-entrance he used to do was into the bar for a refill. So a reentrant function updates for various instances.

It also means, basically work only on the data provided by the caller.

| #include <pthread.h>int pthread_create(pthread_t *thread, pthread_attr_t *attr, void*(*start_routine)(void *), void *arg); |

returns 0 on success.

The C library function pthread_create() facilitates a routine to run as a thread. It has a name that you can identify the thread with, apart from the function name. It is given by  pthread_t *thread. It is of the type pthread_t.

pthread_attr_t *attr is an attribute which I will explain later.

void *(*start_routine)(void *), void *arg) is the routine that will run as a thread and arg is it’s argument.

| #include <pthread.h>void pthread_exit(void *retval); |

This exits from the thread. And unlike functions, you cannot return a variable. Because…..?”

“The variable ceases to exist after the thread.”

“Right.”

| #include <pthread.h>int pthread_join(pthread_t th, void **thread_return); |

This C library function is like the wait system call in processes. Here, pthread_t th represents the routine identifier, remember pthread_create?

It returns a pointer to a pointer to the return value from the thread.

He opened a file on his laptop.

thread_program.c

| #include <stdio.h>#include <stdlib.h>#include <string.h>#include <pthread.h>#include <unistd.h>void *print_func(char* message){   printf("%s - Before sleep\n", message);   sleep(4);   printf("%s - After waking up\n", message);   }int main(){  pthread_t t1, t2;  printf("Main program now running\n");  pthread_create(&t1, NULL, (void *)print_func, (void *) "First call to pthread");  pthread_create(&t2, NULL, (void *)print_func, (void *) "Second call to pthread");  pthread_join(t1, NULL);  pthread_join(t2, NULL);  printf("Back to main after thread join\n");} |

And then he proceeded to explain.

| #include <stdio.h>#include <stdlib.h>#include <string.h>#include <pthread.h>#include <unistd.h>void *print_func(char* message){   printf("%s - Before sleep\n", message);   sleep(4);   printf("%s - After waking up\n", message);   } |

The above code declares the required header files and prints two messages before sleep and after sleep. This is the routine which will be used by two calls. The above function will be called twice later on in the program.

| int main(){    pthread_t t1, t2; |

Threads are declared.

|   printf("Main program now running\n"); |

Just an indicator.

| pthread_create(&t1, NULL, (void *)print_func, (void *) "First call to pthread");pthread_create(&t2, NULL, (void *)print_func, (void *) "Second call to pthread"); |

Create the thread.

To differentiate between two instances of the same function running, we have different messages that are passed on to the function in each instance. That way, it will let you see which thread is running.

As seen above, the thread is created that calls the print_func function and a different message is passed each time. Usually, the best way to pass values is to pass a structure to the thread function using pthread_create. It is of the form,

struct thread_args *args

|   pthread_join(t1, NULL);  pthread_join(t2, NULL); printf("Back to main after thread join\n");} |

Just an indicator to let us know that we are back in the main program.

So, what do you think the output will be?” Lingaraj asked.

“I think it will print the things with the first call to pthread and then the second call. Like this.

Main program now  running

First call to pthread - Before sleep

First call to pthread - After waking up

Second call to pthread - Before sleep

Second call to pthread - After waking up

Back to main after thread join

Of course, with the 4 second delay for sleep.” said Seema.

Lingaraj proceeded to run the program using

| cc -D_REENTRANT thread_program .c  -lpthread |

“You would have to compile like this :

cc -D_REENTRANT thread_program .c –o thread_program -lpthread

if NPTL(Native Posix Threads Library) is the default in your system.

” explained Lingaraj.

The output was displayed on the screen.

| Main program now  runningFirst call to pthread - Before sleepSecond call to pthread - Before sleepFirst call to pthread - After waking upSecond call to pthread - After waking upBack to main after thread join |

Now, you will notice something amiss. The sequence you predicted is not there. While the 1st execution slice was sleeping, the scheduler thought it wise to sneak in the the 2nd execution slice. It didn’t wait for the 1st thread to finish execution. There is no synchronicity.”

Lingaraj looked away and as was his habit, into the distance.

“What is it?”

“Once, I met this woman who was a believer in synchronicity. I was working in animal manure analysis at the time. She was a database analyst. She asked me over candle light dinner.

![](image_rsrc85A.jpg)

‘There is this number 7 that keeps popping up wherever I go and usually when I am doing something important. Do you have a number like that?’

‘Yes, I see number 2 everywhere.’

She got up and left.”

“No wonder!”

“What if we wanted one piece of code to be locked before the scheduler got the next one in.

Let me tell you about a scenario. When my uncle, a doctor was in the operating room in his private hospital, they locked the door in case operations were going on. Once the operation finished, they would open the door by unlocking the door.

If the door was unlocked, a film crew would go in and make videos because it was the only room which had big lights. While this was going on, they would lock the door. After their job was done, the film crew used to unlock the door.

Let’s move on to mutually exclusive threads. What are they? They are resources that can be blocked. If for example, you are with Vijay and he keeps getting distracted with a football match, how can you block his resource so neither a football match, nor wrestling can’t obtain his interest?”

“Easy, I would use a mutually exclusive thread program on him.” Seema was doing some research and fast.

“Easy? Good luck doing that, not because mutex programs are difficult, but tearing one away from football is. A mutex, short for mutually exclusive, locks a critical region of a code, so that the locking program is done with it before others can have a go at it. Remember Lock Lakshman?”  Lingaraj showed a C library function.

| #include <pthread.h>int pthread_mutex_init(pthread_mutex_t *mutex, const pthread_mutexattr_t*mutexattr); |

Initialises a mutex, ‘*mutex’ which is based on the thread function.

const pthread_mutexattr_t *mutexattr

This will take some explaining. Will save it for later.

| int pthread_mutex_lock(pthread_mutex_t *mutex)); |

This locks the resource.

| int pthread_mutex_unlock(pthread_mutex_t *mutex); |

This unlocks the resource.

| int pthread_mutex_destroy(pthread_mutex_t *mutex); |

This will destroy the mutex and clean up as well.

Let’s get into a program.”

“Ok.”

“The mutex program. Before that, the thread program we talked about.

thread_program .c

| #include <stdio.h>#include <stdlib.h>#include <string.h>#include <pthread.h>#include <unistd.h>void *print_func(char* message){   printf("%s - Before sleep\n", message);   sleep(4);   printf("%s - After waking up\n", message);   }int main(){  pthread_t t1, t2;  printf("Main program now running\n");  pthread_create(&t1, NULL, (void *)print_func, (void *) "First call to pthread");  pthread_create(&t2, NULL, (void *)print_func, (void *) "Second call to pthread");  pthread_join(t1, NULL);  pthread_join(t2, NULL); printf("Back to main after thread join\n");} |

The output was

| Main program now  runningFirst call to pthread - Before sleepSecond call to pthread - Before sleepFirst call to pthread - After waking upSecond call to pthread - After waking upBack to main after thread join |

As explained earlier, there is no synchronicity.

We use mutually exclusive threading.

Back to the program, now with a mutex.

thread_with_mutex.c

| #include <stdio.h>#include <stdlib.h>#include <string.h>#include <pthread.h>#include <unistd.h>pthread_mutex_t mutex1 = PTHREAD_MUTEX_INITIALIZER;void *print_func(char* message){   pthread_mutex_lock(&mutex1);   printf("%s - Before sleep\n", message);   sleep(4);   printf("%s - After waking up\n", message);   pthread_mutex_unlock(&mutex1);   }int main(){   pthread_t t1,t2;   pthread_mutex_t mutex1;   pthread_mutex_init(&mutex1, NULL);  pthread_create(&t1, NULL, (void *)print_func, (void *) "First call                    to pthread");  pthread_create(&t2, NULL, (void *)print_func, (void *) "Second call to pthread");   pthread_join(t1, NULL);  pthread_join(t2, NULL); printf("Back to main after thread join\n");} |

I will explain this.

| #include <stdio.h>#include <stdlib.h>#include <string.h>#include <pthread.h>#include <unistd.h>pthread_mutex_t mutex1 = PTHREAD_MUTEX_INITIALIZER;This initialises the mutex, mutex1.void *print_func(char* message){   pthread_mutex_lock(&mutex1);We lock the mutex here . What follows is the critical section of the code.   printf("%s - Before sleep\n", message);   sleep(4);   printf("%s - After waking up\n", message);   pthread_mutex_unlock(&mutex1);Here, we unlcok the mutex.   }int main(){   pthread_t t1,t2;   pthread_mutex_t mutex1;   pthread_mutex_init(&mutex1, NULL);  pthread_create(&t1, NULL, (void *)print_func, (void *) "First call                    to pthread");  pthread_create(&t2, NULL, (void *)print_func, (void *) "Second call to pthread");   pthread_join(t1, NULL);  pthread_join(t2, NULL); printf("Back to main after thread join\n");} |

So, you see, now a routine is locked and then released.

The output is

| Main program now  runningFirst call to pthread - Before sleepFirst call to pthread - After waking upSecond call to pthread - Before sleepSecond call to pthread - After waking upBack to main after thread join |

This is the sequence you had predicted for the thread program without the mutex. Now, it is synchronous. There is another way to achieve synchronicity. Let me tell you about another scenario. When my uncle, the doctor was in the operating room in his private hospital, they had a red light on in case operations were going on. Once the operation finished, they would turn off the red light.

![](image_rsrc85B.jpg)

If the red light was off, a film crew would go in, turn the red light on and make videos. After their job was done, the film crew used to switch off the red light.

![](image_rsrc85C.jpg)

So, the functioning of the light is a semaphore which allows only the doctors during the operation and closes it for film makers and the other way round.

This allowed film makers, to see the light off, enter, switch it on and shoot. Once the job was done, they would switch off the light. Same with doctors.

If the light was on, the film team or the doctors had to wait until the light was off.

“But isn’t it unfair on the patients? They have to wait till the film star finishes.”

“All my uncle’s patients were opportunists. They just signed up for operations so they could tell, ‘I shared the spotlight with Film Star Subbu.’

Also, they had to learn patience. How else would you call him a patient?”

Seema was agonised. But didn’t say anything. Lingaraj continued.

“A semaphore basically tells different threads whether a resource is available or not. A semaphore can be extended to tell even processes whether a routine is available or not. Here are some C library functions :

| #include <semaphore.h>int sem_init(sem_t *sem, int pshared, unsigned int value); |

We initialise the semaphore here.

‘sem_t *sem’ is the semaphore itself. The type is sem_t.

‘int pshared’ indicates whether the semaphore is shared across processes. If it’s only threads in the current process, this value is 0.

the ‘int’ value is the value you initialise the semaphore with.

| #include <semaphore.h>int sem_post(sem_t * sem); |

The ‘sem_post’ function atomically increases the value of the semaphore by one. Like how a good economic situation increases wealth. Atomically means, in one go without listening to other signals. Like how a King used to throw his necklace at poor artists as soon as he heard their rendition about his might and prowess.

![](image_rsrc85D.jpg)

Nobody else in the court used to dare catch those necklaces or tell the King, ‘Of course, he is lying. But you can’t tell, can you?’

| int sem_wait(sem_t * sem); |

This decreases the count of the semaphore by 1, but has the good sense to wait if it’s zero. This is like some erstwhile King’s income tax official. If the person had zero money, they were courteous enough to wait until he made money due to a good economic system and then decrease his wealth back to zero.

sem_post() and sem_wait() are coordinated in their implementation. It means, sem_wait keeps track of the semaphore and once it goes to zero, it increments it and the corresponding thread is pressed into service. The condition of the variable decides what routine will happen.

| sem_t *sem_open(const char *name, int oflag); |

sem_open()  creates  a  new  POSIX semaphore or opens an existing semaphore.  The semaphore is identified by name. It returns the address of the semaphore.

| #include <semaphore.h>int sem_destroy(sem_t * sem); |

This destroys the semaphore as the name of the function suggests. It also tidies up resources.

Coming back to the light on-off parallel. A fussy film star waiting, would keep asking the director to check for the status of the light if he’s outside and the doctors are inside. This won’t be encouraged and the actor will be kicked out of the sets, film star or not. When it turns off, the team will know. Because the program is always on the lookout for that. Like these people who are always on the lookout for a discount or a free coupon.

So, to program, you could start a thread with ‘pthread’. That will keep running. You create a semaphore and you tell the kernel, what happens when the semaphore value is 0\. This starts a routine. You can tell what happens when the semaphore has a value.  But you don’t have to tell the program, keep looking for the variable and check whether it goes to 0 or whether it is positive in the program. It’s the job of the system. Let’s modify the program naming it ‘thread_sem_program.c’, this time with semaphores. Be sure to include semaphore.h.

| #include <stdio.h>#include <stdlib.h>#include <string.h>#include <pthread.h>#include <unistd.h>#include <semaphore.h>sem_t semap1;void *print_func(char* message){     sem_wait(&semap1);   printf("%s - Before sleep\n", message);   sleep(4);   printf("%s - After waking up\n", message);   sem_post(&semap1);}int main(){  sem_init(&semap1,0,1);  pthread_t t1, t2;  printf("I am in main\n");  int iret1 = pthread_create(&t1, NULL,(void *) print_func, (void *) "First Instance");  int iret2 = pthread_create(&t2, NULL, (void *) print_func, (void *) "Second Instance");  pthread_join(t1, NULL);  pthread_join(t2, NULL);  sem_destroy(&semap1); printf("Back to main after thread join\n");} |

I will run it like this,

| cc -D_REENTRANT thread_sem_program.c  -lpthread -lrt |

The output again, is

| Main program now runningFirst Instance - Before sleepFirst Instance - After waking upSecond Instance - Before sleepSecond Instance - After waking upBack to main after thread join |

How is Vijay doing now?”

“He doesn’t remember a few things about how we spent time with each other.”

“The keyboard that you speak of, does he hand it over to anybody and everybody to let himself be programmed?”

“You are making me anxious.”

“Then you better learn fast.”

“Thanks for understanding. I need a couple of days break. I need to see Vijay.”

“Sure.”

Seema called the same cab driver and left for Bangalore. She came back after a couple of days and walked into Lingaraj’s house.

“How was your trip?” asked Lingaraj.

“It was nice to see him, he’s changed for the better. But he’s become secretive, I feel. What did you do?” she asked Lingaraj.

“I posed at the edge of a cliff to take a selfie when a strong gust of wind….”

“He hardly notices I am there. He keeps calculating football moves and tells their outcome beforehand.” Seema interrupted.

“That’s awesome!”

Seema stared at Lingaraj. Lingaraj looked away and continued.

“Thread attributes.

You throw a party and you arrange for cooks and bartenders to the party. Some of your friends might have come with their drivers, some by a cab and some running. There are people like that. After the party is over, your friends go back. You would want to know if a friend reached home. So, you call her and find out whether she reached home safe. Now, the cook who had come, you won’t call him to find out if he reached home safely. More so, if the prepared food was not good and you find out he had also partaken of some drinks without your permission.

So, if you imagine these two going back home processes to be threads, one is an attached thread and the other is a detached thread.

So, to a thread you can specify attributes that tell it to behave in a particular way.

This is the list.

| #include <pthread.h>int pthread_attr_setdetachstate(pthread_attr_t *attr, int detachstate);int pthread_attr_getdetachstate(const pthread_attr_t *attr, int *detachstate);int pthread_attr_setschedpolicy(pthread_attr_t *attr, int policy);int pthread_attr_getschedpolicy(const pthread_attr_t *attr, int *policy);int pthread_attr_setschedparam(pthread_attr_t *attr, const struct sched_param*param);int pthread_attr_getschedparam(const pthread_attr_t *attr, struct sched_param*param);int pthread_attr_setinheritsched(pthread_attr_t *attr, int inherit);int pthread_attr_getinheritsched(const pthread_attr_t *attr, int *inherit);int pthread_attr_setscope(pthread_attr_t *attr, int scope);int pthread_attr_getscope(const pthread_attr_t *attr, int *scope);int pthread_attr_setstacksize(pthread_attr_t *attr, int scope);int pthread_attr_getstacksize(const pthread_attr_t *attr, int *scope); |

This is quite a list and appears daunting. Before you start using any of them, you need to initialise a thread attribute object.

| #include <pthread.h>int pthread_attr_init(pthread_attr_t *attr);#include <pthread.h>int pthread_attr_destroy(pthread_attr_t *attr); |

The first function will initialise the thread attribute object and the second will destroy the thread attribute object.

“You hardly created the thread and so soon you are talking of destroying it.”

“Probably a complex. Whenever I enter a video game, especially a shooting game, my avatar gets destroyed instantly. And I was so stupid I used my real name to get into these games, because I thought they would ask for my id proof. It so happened that I met these guys I was playing against when we went to this gaming community meeting. They were surprised I was still alive.

| int pthread_attr_setdetachstate(pthread_attr_t *attr, int detachstate); |

It has two arguments, the attribute object pointer and the flag, detachstate. In the flag you can specify,

PTHREAD_CREATE_JOINABLE : This is the default, where you have to call the thread to join.

PTHREAD_CREATE_DETACHED : This is where you don’t care. You cannot call the thread join function.”

“So you will never find out if the cook reached home or not.”

“

| int pthread_attr_getdetachstate(const pthread_attr_t *attr, int *detachstate); |

This tells you the current state of the thread. Notice that the int detachstate was something you specified. Here, you are specifying a pointer in which will be returned the value of the current state.

| int pthread_attr_setschedpolicy(pthread_attr_t *attr, int policy); |

| int pthread_attr_getschedpolicy(const pthread_attr_t *attr, int *policy); |

In a party, there will always be speakers who want the mic. But you can specify who gets the centre stage by scheduling. Whoever comes first will get the mic first or by round robin.

Scheduling is the prerogative of the scheduler in the kernel, but you can get into the act and take even more control. You can specify which threads have more priority. Whether a thread can be pre empted by an other thread or not.”

“No equal treatment.”

“If there is a mutex lock on one resource, you can schedule which thread gets the resource, in case multiple threads are running, once the mutex is unlocked.”

The second function returns the state in *policy.

| int pthread_attr_setschedparam(pthread_attr_t *attr, const struct sched_param*param);int pthread_attr_getschedparam(const pthread_attr_t *attr, struct sched_param *param); |

This allows you to control the scheduling of threads running with schedule policy SCHED_OTHER.

| int pthread_attr_setinheritsched(pthread_attr_t *attr, int inherit);int pthread_attr_getinheritsched(const pthread_attr_t *attr, int *inherit); |

This can take two values :

PTHREAD_EXPLICIT_SCHED and

PTHREAD_INHERIT_SCHED.

This only means whether a new thread’s scheduling is set by the attributes or whether the scheduling is inherited from the thread that created it.

| int pthread_attr_setscope(pthread_attr_t *attr, int scope);int pthread_attr_getscope(const pthread_attr_t *attr, int *scope); |

This controls how the scheduling of a thread is calculated.

| int pthread_attr_setstacksize(pthread_attr_t *attr, int scope);int pthread_attr_getstacksize(const pthread_attr_t *attr, int *scope); |

This is for threads which need more stack size. And a stack size is specified for particular purposes depending upon the size of local variables or the number of routines in.

| int pthread_attr_setstackaddr( pthread_attr_t *attr, void *stackaddr); |

”

“You can specify the stack address.” replied Seema.

“Thread cancelling.

| #include <pthread.h>int pthread_cancel(pthread_t thread); |

This cancels a thread. But whether the thread can be cancelled depends on the thread. It’s something like an insult. A master once said, “The knife of insult lands near my feet. I don’t pick it up and stab myself with it.”

So, the cancellation depends on the thread. If the thread is willing to be cancelled or not, while coding, you use the following function:

| #include <pthread.h>int pthread_setcancelstate(int state, int *oldstate); |

Here, int state can be two values,

PTHREAD_CANCEL_ENABLE

or

PTHREAD_CANCEL_DISABLE

The oldstate argument procures the previous state.

“The first time I heard something of philosophy from you. Quite profound.”

“I once had a philosophy of my own.  I was working as a plumber in a skyscraper in a city and one day, I got a complaint saying the overhead tank was leaking. I climbed all the way up and saw a woman on the edge of the terrace. I sensed she was up to something and I spoke with her.

![](image_rsrc85E.jpg)

I began by talking about life and went on for half an hour. Then she said, ‘I just scaled this building to show the world the power of belief. But after listening to you, I feel like jumping.”

Seema slapped her forehead.

“Those days, I was trying to influence the world with my personality. Anyway, if a thread is open to its being cancelled, you can use the following C library function :

| #include <pthread.h>int pthread_setcanceltype(int type, int *oldtype); |

The type is either :

PTHREAD_CANCEL_ASYNCHRONOUS

This cancels the thread immediately on receipt of the cancel request.

PTHREAD_CANCEL_DEFERRED

This cancels the thread until the requisite pthread function is called.

I think we have spoken too much about threads.

Interprocess Communication

Pipes

Let’s touch upon Interprocess communication

Let me start with a story. There was this girl I liked and I wanted to know her better. So, I wrote this poem for her.

You,
seeing whom my heart meanders in playful sentiment
In calm rivers
down the slopes of childlike play
Falling from the cavalier
And jumping to meet an ocean
Can we talk some more?
About the mountains in the far north
And how it would feel to light a bonfire at the foot
About the sleeping savannahs in the south
And to sit there with a coffee cup
The stretching deserts of the east
And tying camels to the palm trees in the oasis
The lazy sea to the west
And holding a conch shell to the ear
The blue suns beyond the eastern sky
and the planet lit by its many moons
Where jewels lie on the bed
under rivers of pristine water
Where gazelles escort you
feeling one with undulated waters
Where the woods become a flute
and life is euphony
Where there is to do, nothing at all
and everything that happens
proceeds from all encompassing love, even a
leaf fall

I wanted to read this letter personally to her and so landed at her house. I rang the bell and promptly, her father, she called him ‘pop’, opened the gate. It was a big house. I told him I wanted to meet Suparna.

![](image_rsrc85F.jpg)

‘What do you want to tell her?’ he asked.

‘It’s personal.’ I replied.

‘Whatever you want to tell her, tell me, I will tell her.’

I was taken aback. I then told him about multi threading in Linux and how it is implemented for the next 1 hour.

‘I will tell her.’ he said and closed the door.

I repeated this for a week delving more into multithreading. On the eighth day, he opened the door.

‘In multithreading..’ I began

‘Whatever you want to tell her, tell her directly.’

“And that too fizzled out, I assume.”

“How, I will tell you later. So, her pop was acting like a pipe. Which brings us to the first C library function.”

| #include <stdio.h>FILE *popen(const char *command, const char *open_mode); |

So, this is usually used to pass commands to a process. The open_mode is either r or w.

The calling program can receive output from the called process using “r”.

The calling program can send it’s output to the input of the called process using “w”. said Lingaraj.

| int pclose(FILE *stream_to_close); |

This closes the pipe. If the called process is still running, pclose will wait for it to finish and then close the pipe.

It returns the exit code of the process, the file stream of which is being closed.

Here’s an example.”

Lingaraj showed her some pseudocode on the laptop and began to explain.

| Include the necessary header files.Start the main function.Declare a file stream variable of type FILE. This is for reading and it can be read_fstr.Declare a character array using a macro BUFSIZDeclare an integer to keep track of number of characters to read.Use memset to fill a block of memory with NULLs to clear any data.Call the pipe read-only using popen() and the returned file stream is assigned to read_fstr.Check if the read_fstr is not NULL. If so,Till NULL is reached or if there is any input, enclose this in a loop.{Use fread to read the characters from the FILE stream opened by popen. Store it in buffer which is the character array which was declared.If, the number of characters read is more than zero,Then print the contents of buffer which is the value of the output of the command mentioned in the popen() function.}Close the pipe.Exit |

“I get it.” said Seema.

“We have a system call:

| #include <unistd.h>int pipe(int file_descriptor[2]); |

It takes an array of 2 file descriptors and builds a pipe between them. The data written to the file_descriptor[1] can be read back by file_descriptor[0]. Previously, we used file streams, but now we use file descriptors, so we have to use read and write system calls.”

“I don’t see anything special here.” Seema commented.

“This is more helpful if you want to send data between processes.”

The pipe opens two file descriptors. The first file descriptor in the array is the reading end of the pipe and the second file descriptor is the writing end of the pipe. Now, you might have some issues with such pipes because a write might have closed, but the other process might still be trying to read because it does not know the other program has stopped writing. And more importantly, you would want to have communication between two programs.

pipe_fork.c

| #include <stdio.h>#include <stdlib.h>#include <unistd.h>#include <string.h>#include <fcntl.h>int main(){    int total_bytes;    int filed_pipe[2];    const char chars_passed[] = "Crocodile Doctor";    char buffer[BUFSIZ +1];    pid_t fork_success;    memset(buffer,'\0',sizeof(buffer));    pipe(filed_pipe);    fork_success = fork();    if (fork_success == -1)    {      fprintf(stderr,"Fork Failure");      exit(EXIT_FAILURE);    }      else if (fork_success == 0)    {        total_bytes = read(filed_pipe[0],buffer, BUFSIZ);        printf("This program has read %d bytes - %s\n",total_bytes, buffer);        exit(EXIT_SUCCESS);    }    else    {        total_bytes = write(filed_pipe[1],chars_passed, strlen(chars_passed));        printf("This program wrote %d bytes\n", total_bytes);    }exit(EXIT_SUCCESS);} |

The output is :

| This program wrote 16 bytesThis program has read 16 bytes - Crocodile Doctor |

The sequence doesn’t appear to be right only because the parent process finished before the child. So, the write was done first.

What happened in the above program was this. A child process was created using fork and we saw whether the program was now in the parent or child process using the return from fork. In the first instance, it was in the child process as the fork return was 0\. Then we read from the first file descriptor. Now, a process different from the program which is executing managed to read from the program you wrote, albeit a child process. So, some kind of communication is happening. This is easy because the child process inherited the file descriptors. But what if, the programs are completely different?

We need two programs.  Let’s call this the producer program, because it supplies the data to be passed. We will name it pipe_prod.c.

pipe_prod.c

| #include <stdio.h>#include <stdlib.h>#include <unistd.h>#include <string.h>int main(){    int total_bytes;    int filed_pipe[2];    const char chars_passed[] = "Crocodile Doctor";    char buffer[BUFSIZ + 1];    pid_t fork_success;    memset(buffer, '\0', sizeof(buffer));    pipe(filed_pipe);    fork_success = fork();    if (fork_success == -1)    {          fprintf(stderr,"Fork Failure");      exit(EXIT_FAILURE);    }      else if (fork_success == 0)    {          sprintf(buffer,"%d", filed_pipe[0]);        (void) execl("pipe_cons","pipe_cons", buffer, (char*) 0);        printf("This is the child process,but this text won't be displayed because execl finishes off the calling process.");        exit(EXIT_FAILURE);    }    else    {        total_bytes = write(filed_pipe[1],chars_passed, strlen(chars_passed));        printf("This program wrote %d bytes - %s\n", total_bytes, buffer);            }exit(EXIT_SUCCESS);} |

The first change is the sprintf function. It captures the first file descriptor in the array passed to pipe in the holder, buffer. That is, it prints the value of the file descriptor stored in filed_pipe[0] into buffer. Because the second program we call later will not inherit the file descriptors.” explained Lingaraj.

“But there is a call to fork.” said Seema.

“Yes. The logic is, if we call another program using execl, which we will, the calling process is done away with, even though the process id continues. It’s like all round Arun completely taking over my position and I not being there any longer. So, the process is finished. We call the fork, create a child process and then call execl from the child process. This way, the parent process is retained and the child process finishes. Hence, you won’t see the text in the printf statement, “This is the child process,but this text won't be displayed because execl finishes off the calling process.” after execl is called.

In execl, we call the program to be executed which is ‘pipe_cons’ and also supply two pieces of information. One, the name of the program as an argument to the program being called.  And the other, the file descriptor we had stored in buffer. So, the program being called by execl will have the information.

Let’s move on to the consumer program which receives the data. This is named pipe_cons.

pipe_cons.c

| #include <stdio.h>#include <stdlib.h>#include <unistd.h>#include <string.h>int main(int argc,char *argv[]){    int bytes_ex;    char buffer[BUFSIZ + 1];    int file_des;    memset(buffer,'\0',sizeof(buffer));    sscanf(argv[1],"%d", &file_des);    printf("The argument to the consumer program is %s\n", *argv);    bytes_ex = read(file_des, buffer, BUFSIZ);    printf("The process %d has read %d bytes. Content : %s \n", getpid(), bytes_ex, buffer);    exit(EXIT_SUCCESS);} |

This receives the data passed through sscanf. But a word about memset().

#include <string.h>

void *memset(void *s, int c, size_t n);

The  memset()  function  fills  the  first  n  bytes of the memory area

pointed to by s with the constant byte c. If you want a memory area to be filled with NULL characters, use what the above program uses.

“There was this guy we called Speech Sathya. He was a speaker. Nobody used to listen to him because he used to lie. He had a false NULL terminator. A NULL terminates a string as you know. He used to say “My speech is done.” and would go on for half an hour more. You want to meet him?

“NULL. I won’t say anything beyond this.”

Lingaraj knew she hadn’t got the point. He didn’t know how to explain this. So he moved on.

The next line prints the argument received by this consumer program, which is sent when we run the producer program. This will show in the output as this program’s name, which is ‘pipe_cons’. Then it reads from the file descriptor. What does it read? It is not reading from a file, but from a file descriptor which was written to using a pipe. Of course, you can say, rather than passing the argument and the file descriptor through the buffer, why not pass the string, ‘Crocodile Doctor’ directly. We might need to pass amounts of data which cannot be simply held in a string.”

The output, after we create the executables, name them pipe_prod and pipe_cons respectively, an important step, and run the pipe_prod program only using ./pipe_prod

| This program wrote 16 bytes -The argument to the consumer program is pipe_consThe process 53534 has read 16 bytes. Content  : Crocodile Doctor |

The 53534 is specific to this instance as I said before.”

“What if the second process isn’t started from the first program, but a totally unrelated program?” asked Seema.

“Good question. We have FIFOs for that. A FIFO as I said is First In First Out. Whatever you put into a FIFO has to be accessed in the same sequence you put it in.

| #include <sys/types.h>#include <sys/stat.h>int mkfifo(const char *filename, mode_t mode); |

This makes a FIFO with a filename and a mode you specify. Modes are important. You simply cannot use O_RDWR. It is unnecessary in the first place and secondly the results are undefined. Suppose I upload a video online and go out on a trek where there is no internet access. I ask my friend to keep track of the views. After 2 days, I call him from an old fashioned landline, and if the views are 0, he will block my call so as to not make me feel gloomy on the trek. If I call him an hour later, he will still block me. But if there is 1 view, he will answer the call and tell me the good news. If it’s a friend, I can’t enforce him to give me the report even if it’s 0 views. However, if I employ an assistant from the film industry, and pay him, he will tell me there are 0 views. Of course, he will lose respect for me and look for employment elsewhere, but that’s besides the question. I can enforce a O_NONBLOCK on  him. In the context of open when you pipe the mode, either O_RDONLY or O_WRONLY with O_NONBLOCK,

| open(const char *path, O_RDONLY); |

The open call will block; it will not return until a process opens the same FIFO for writing.” said Lingaraj.

“So, it’s like your friend blocking your call until there are views on your video.” said Seema. Lingaraj continued.

“

| open(const char *path, O_RDONLY &#124; O_NONBLOCK); |

The open call will now succeed and return immediately, even if the FIFO has not been opened for writing

by any process.”

“So, the employee who doesn’t block your calls.” said Seema.

| open(const char *path, O_WRONLY); |

In this case, the open call will block until a process opens the same FIFO for reading. I don’t have an analogy for this.” admitted Lingaraj.

“Your friend is excited to tell you that there is a view, but your phone is not reachable.” offered Seema.

“Sounds okay. The next one though is a bit strange.

| open(const char *path, O_WRONLY &#124; O_NONBLOCK); |

What do you think this will do?” asked Lingaraj.

“The employee, because it is O_NONBLOCK calls you as soon as there is a view and shares the ‘good news’ as you call it.” said Seema.

“Despite me being not reachable? Actually wrong. It returns immediately, but if no process has the FIFO open for reading, open will return

an error, –1, and the FIFO won’t be opened. If a process does have the FIFO open for reading, the file descriptor returned can be used for writing to the FIFO.”

“Okay, so the assistant calls you, but if you are not reachable, he will put it down as an error. But if you are reachable on the phone, he can communicate. Sounds lopsided. As you said, it’s strange.” said Seema.

“You won’t believe it, but this actually happened. After he called me inside the house to talk to her directly, he would not let us be alone. He used to scrutinise my every word. I got adventurous and tried to sneak in a message between all the multithreading concepts.

I said:

free()

printf(“Lunch and ice cream\n”);

somewhere between the lines. I thought only Suparna would understand it. Her dad understood it as well.

“So, where there ought to have been lunch, there was a punch and you screamed?”

“No, that guy got all dressed up and ready. He was beaming. He told his daughter, ‘This guy is offering us free lunch with ice cream. We should not deny the requests of our guests.’ Then all of us went and I had to get them both lunch and ice cream at this 5 star hotel.

![](image_rsrc85G.jpg)

He had even brought a hot box with him to get the night’s dinner packed. I told them I had no money. But they went about their eating. After he had the ice cream, the waiter came.

‘Sir, pleased to serve the owner of out hotel.’ the waiter said.

I was shocked. Suparna’s father was the owner of the 5 star hotel. So this was a trick all along. He actually liked me and this was the surprise. What Suparna’s father said next floored me.

‘Please give the bill to this young man here.’

“But…” I began. The both of them got up and left.

Then the waiter told me that Suparna’s father was the biggest miser in town.

I had to wash the dishes of course. I also found out later that the guy had been making copies of my notes on Linux threading and selling them.

Anyway, let’s move on. We can read and write to fifos after we create them and access it using a file descriptor. 

| #include <unistd.h>int access(const char *pathname, int mode); |

The above command checks to see whether a file given by the pathname exists. The mode is usually F_OK.

If the number of bytes being written is greater than PIPE_BUF defined in limits.h, let’s just say the write fails. There could be a case where many programs are writing to the FIFO and in such a scenario, rather than interleave the data, you would be safe if the size does not exceed PIPE_BUF.

Let’s look at an example program.

This is the producer program :

fifo_prod.c

| #include <unistd.h>#include <stdlib.h>#include <stdio.h>#include <string.h>#include <fcntl.h>#include <sys/types.h>#include <sys/stat.h>#define FIFO_NAME "/tmp/my_fifo"int main(){    int pipe_fd;    int res;    int bytes_sent = 0;    char buffer[100];        printf("Input text to be passed\n");                fgets(buffer, sizeof(buffer), stdin);        printf("%s", buffer);        res = mkfifo(FIFO_NAME, 0777);            if (res != 0) {            fprintf(stderr, "Could not create the FIFO %s\n", FIFO_NAME);            exit(EXIT_FAILURE);        }    printf("Process %d is opening the FIFO in O_WRONLY mode\n", getpid());    pipe_fd = open(FIFO_NAME, O_WRONLY);    if (pipe_fd != -1)    {          printf("Pipe succesful\n");        res = write(pipe_fd, buffer, sizeof(buffer));            if (res == -1) {                fprintf(stderr, "Write error on pipe\n");                exit(EXIT_FAILURE);            }               bytes_sent += res;                    (void)close(pipe_fd);    }    else {        printf("Pipe not successful\n");        exit(EXIT_FAILURE);    }    printf("Process %d finished. Bytes sent - %d\n", getpid(), bytes_sent);    exit(EXIT_SUCCESS);} |

This asks the user to print some input text that is to be passed through the FIFO. Then it makes a fifo in /tmp/my_fifo. Then it opens the FIFO and gets a file descriptor for it. Then we write to the FIFO, the user input text which we have stored in buffer. After writing, we close the FIFO. If the open is successful, we write to the pipe. All this testing the conditions from the return values. Notice that there is no fork or execl. So, we need another way to run the programs side by side. I will tell you about it in a while.

This is the consumer program fifo_cons.c.

fifo_cons.c

| #include <unistd.h>#include <stdlib.h>#include <stdio.h>#include <string.h>#include <fcntl.h>#include <sys/types.h>#include <sys/stat.h>#define FIFO_NAME "/tmp/my_fifo"#define BUFFER_SIZE PIPE_BUFint main(){    int pipe_fd;    int res;    int open_mode = O_RDONLY;    char buffer[100];    int bytes_read = 0;    memset(buffer, '\0', sizeof(buffer));    printf("Process %d opening FIFO in O_RDONLY mode.\n", getpid());    pipe_fd = open(FIFO_NAME, O_RDONLY);    printf("Process %d, the file descriptor is %d\n", getpid(), pipe_fd);    if (pipe_fd != -1)    {            res = read(pipe_fd, buffer, sizeof(buffer));            bytes_read += res;            (void)close(pipe_fd);    }    else {        exit(EXIT_FAILURE);    }    printf("Process %d finished, %d bytes were read and the message was %s\n", getpid(), bytes_read, buffer);    exit(EXIT_SUCCESS);} |

Because the consumer is a completely different program, we can use the same variable names. Only the FIFO name is known and it has to be consistent in both the programs. The FIFO is read through it’s file descriptor given by the open call. Then it is closed. The relevant message is printed along with the string that was sent through the FIFO. This is how we run it.

We create executable files for both, naming them, for instance fifo_prod and fifo_cons, after removing the file /tmp/my_fifo if it exists. Of course, we can use the access() system call also in the program to check for the existence of the file.

We run fifo_prod in one terminal. The output looks like this

| Input text to be passed |

Then we type :

Seema learns Linux.

This is printed on the screen because of the printf function.

| Seema learns Linux. |

Then, you get this message :

| Process 61178 is opening the FIFO in O_WRONLY mode |

Again, this is machine and instance specific. Now, open another terminal and run fifo_cons

As soon as you run it, you get the following message :

| Process 61182 opening FIFO O_RDONLYProcess 61182 result 3Process 61182 finished, 100 bytes read, message was Seema learns Linux. |

And the command prompt appears. In the other terminal, the whole output is :

| Input text to be passedSeema learns LinuxSeema learns LinuxProcess 61191 is opening the FIFO in O_WRONLY modePipe succesfulProcess 61191 finished. Bytes sent – 100 |

‘Seema learns Linux’ is not 100 bytes. But we have declared buffer as a character array of 100\. So, it shows 100 in both the program outputs. As an exercise, I want you to modify this program using a while loop, looking for the newline character and counting the number of bytes written which is then printed.”

“Sure.”

“A note : You cannot use system calls like lseek() to read from FIFOs.” finished Lingaraj. Seema went to work on the exercise.

IPC : Semaphores

It’s time to remember the doctor’s story of the operation theatre and the film makers. The light is of only one colour, so the different states of the light are off and on.

![](image_rsrc85B.jpg)

The switching on of the light allows access to the teams. Then the team uses the operation room and then politely toggles the light. The other team might be waiting, might not be waiting. Again the procedure repeats.”

“Procedure? Pun intended?”

“No. And of course, the teams might not be executing only in the operation room. The doctors could be in the x ray room, the film makers could be outdoors. So, the operation room is the critical region.”

“Critical? Pun intended?”

“Yes. The states of the switch. ON and OFF. This brings us to binary semaphores. Zero and one. Two scenarios.

A process waiting for a resource to be available based on the status of a variable.

A process executes using a resource when available based on the status of a variable.

A process changes the status of a variable after it’s job is done.

A process changes the status of a variable before it begins it’s job.”

“Ok.”

“In the case of the doctors vs film makers, the switch is key.”

“The bulb.” Seema tried to correct.

“They are part of one package. The switch comes free with the bulb. They have to be connected, or why else would it cause an electric shock?”

“No, the bulb has to be connected with the switch or how else would it light?”

“Good perspective.”

Now, system calls related to semaphores :

| int semget(key_t key, int num_sems, int sem_flags); |

key_t key is basically the resource identifier.

“Something like the operation room. A reference to the operation room.”

“If there is a resource num_sems is the number of semaphores. Usually 1.

sem_flags let you modify behaviour. The above system call can return the value of an existing semaphore identified by the key or if the flag is 0.

Other values of sem_flags are akin to the mode in open(). Write means the value of the semaphore can be altered. And execute permission means nothing.

The least significant 9 bits of sem_flags represent the permissions.

It returns the semaphore identifier, a non negative integer. If it fails, it sets ERRNO and returns -1.

“Like the switch. A reference to the switch rather.”

The next system call :

| int semop(int sem_id, struct sembuf *sem_ops, size_t num_sem_ops); |

sem_id is what semget returned, the semaphore identifier.

sem_ops is a pointer to an array of structures. The important members are :

struct sembuf {

short sem_num;

short sem_op;

short sem_flg;

}

sem_num is the semaphore number in terms of count. 0 if it’s only 1 semaphore.

sem_op perhaps the most important because it is the value by which the semaphore has to be changed. -1 and +1 are the ones generally used.

sem_flag is set to SEM_UNDO and it helps the OS release the semaphore in case the process terminates before it releases the semaphore.

| int semctl(int sem_id, int sem_num, int command, ...); |

This system call lets you directly control semaphore information.

The first parameter is the semaphore identifier returned by semget(). sem_num again is the semaphore number in terms of count. 0 for only 1 semaphore.

The command parameter can be :

SETVAL : Used at the beginning to initialise the semaphore to a value.

IPC_RMID : This is when you need to delete a semaphore after use.

There can exist named semaphores as well. But I will not get into it.

Let’s look at a program without a semaphore :

seema_loves_yoga.c

| #include <stdio.h>#include <stdlib.h>#include <unistd.h>int main(int argc,char *argv[]){    int i;    pid_t pid;    pid = fork();    if(pid < 0)    {        printf("Fork failed.\n");        exit(1);    }    else if(pid == 0)    {        char *ca1 = "Vijay";        char *ca2 = "loves football";             puts(ca1);            fflush(stdout);            sleep(4);            puts(ca2);        }    else    {       char *ca1 = "Seema";       char *ca2 = "loves Yoga";         puts(ca1);            fflush(stdout);            sleep(4);            puts(ca2);    }} |

Here, a fork is called and each process, the parent and the child print a character, twice in a for loop after a sleep duration. We assume that the characters in one process are printed one after the other. But, see the output.

| SeemaVijayloves Yogaloves football |

The kernel sneaked in the child process while the parent process was in the loop and tried to catch a few winks, not allowing either the parent or the child process to print 2 strings in sequence. So, we use semaphores to get the critical section committed to it. Look at this modified program with the semaphore.

seema_loves_yoga_sem.c

| #include <stdio.h>#include <stdlib.h>#include <unistd.h>#include <sys/sem.h>#define KEY 0x1254union semun{    int val;    struct semid_ds *buf;    unsigned short *array;};struct sembuf p = { 0, -1, SEM_UNDO};struct sembuf v = { 0, +1, SEM_UNDO};int main(int argc,char *argv[]){    int id = semget(KEY, 1, 0666 &#124; IPC_CREAT);    if (id < 0)    {        printf ("Couldn't create semaphore.\n");        exit(EXIT_FAILURE);    }    union semun u;    u.val = 1;    if(semctl(id,0,SETVAL, u) < 0)    {        printf("Semctl failed.\n");        exit(EXIT_FAILURE);    }    int i;    pid_t pid;    pid = fork();    if(pid < 0)    {        printf("Fork failed.\n");        exit(1);    }    else if(pid == 0)    {        char *ca1 = "Vijay";        char *ca2 = "loves football";        if(semop(id, &p, 1) < 0)            {                printf("Semop failed");                exit(EXIT_FAILURE);            }            puts(ca1);            fflush(stdout);            sleep(4);            puts(ca2);            if(semop(id, &v, 1) < 0)            {                printf("Semop failed");                exit(EXIT_FAILURE);            }    }    else    {       char *ca1 = "Seema";       char *ca2 = "loves Yoga";        if(semop(id, &p, 1) < 0)            {                printf("Semop failed");                exit(EXIT_FAILURE);            }          puts(ca1);            fflush(stdout);            sleep(4);            puts(ca2);           if(semop(id, &v, 1) < 0)            {                printf("Semop failed");                exit(EXIT_FAILURE);            }    }} |

Then Lingaraj proceeded to explain :

| #include <stdio.h>#include <stdlib.h>#include <unistd.h>#include <sys/sem.h>#define KEY 0x1254 |

KEY 0x1254 defines a semaphore identifier

| union semun{    int val;    struct semid_ds *buf;    unsigned short *array;}; |

This is a bit technical, but for all practical purposes, it will suffice to know that you need to define it. This is needed for semctl.

| struct sembuf p = { 0, -1, SEM_UNDO};struct sembuf v = { 0, +1, SEM_UNDO}; |

p and v signify the decrement and increment operations of the semaphore. Something like sem_wait and sem_post.

| int main(int argc,char *argv[]){    int id = semget(KEY, 1, 0666 &#124; IPC_CREAT); |

We create the semaphore and what follows is the testing whether it is successful or not.

|     if (id < 0)    {        printf ("Couldn't create semaphore.\n");        exit(EXIT_FAILURE);    }    union semun u;    u.val = 1;    if(semctl(id,0,SETVAL, u) < 0)    {        printf("Semctl failed.\n");        exit(EXIT_FAILURE);    }    int i;    pid_t pid;    pid = fork();    if(pid < 0)    {        printf("Fork failed.\n");        exit(1);    } |

We see whether we are in the child process or the parent process and execute the relevant code.

|     else if(pid == 0)    {        char *ca1 = "Seema";        char *ca2 = "loves Yoga"; |

We commence the semaphore decrement. It is a binary semaphore as you might have noticed.

|             if(semop(id, &p, 1) < 0)            {​ printf("Semop failed");           exit(EXIT_FAILURE);            }            puts(ca1);            fflush(stdout);            sleep(4);            puts(ca2); |

Here, enclosed within the semaphore decrement and increment processes, is the execution sequence. We again put two character string one after the other with a 4 second delay between them.

We shall  increment the semaphore.

|             if(semop(id, &v, 1) < 0)            {                printf("Semop failed");                exit(EXIT_FAILURE);            }            sleep(2);        }    }    else    {       char *ca1 = "Vijay";       char *ca2 = "loves football";        if(semop(id, &p, 1) < 0)            {                printf("Semop failed");                exit(EXIT_FAILURE);            }puts(ca1);            fflush(stdout);            sleep(4);            puts(ca2);                      if(semop(id, &v, 1) < 0)            {                printf("Semop failed");                exit(EXIT_FAILURE);            }    }} |

Let’s see the output.

| Seemaloves YogaVijay$ loves football |

A part of the output is printed after 4 because the parent process finishes before the child.

You might wonder no real communication is happening. No messages were exchanged. But if you notice, coordination is happening with respect to time. And that is good enough for it to be called Interprocess Communication.

IPC : Shared Memory

Lingaraj said,

“Think of the example I gave where we would be putting a cocktail recipe in a particular location near the rocks. The knock out rocks. You can even allow other processes to access the memory location. I also told you it was useful because whenever we put it on those stones and come back to collect it, there would be more recipes added by people who would have experimented the previous night.

![](image_rsrc84T.jpg)

The recipe paper can be thought of as the memory. And information is shared between the drunkards and we through this sheet. This is faster than creating pipes or fifos. Here care should be taken to see to it that no two processes are writing at the same time.

The system calls are

| #include <sys/shm.h>int shmget(key_t key, size_t size, int shmflg); |

The key_t key is the name of the memory segment. You can use a #define to define a key, but this key has to be known by both the processes to facilitate Inter Process Communication.

The value IPC_PRIVATE makes the shared memory private to the process. When I was down in life, I wanted to share my stories. But I could find no one. So, it used to be an IPC_PRIVATE situation.

“That’s sad.”

“It was, until I started visiting the knock out rocks.”

“No, it’s not a joke. You have told me so many stories about yourself. They are sad stories, but you make them sound funny. I laughed, I was amused, I was taken aback and I was surprised at some of your stories. I am not a psychoanalyst but I am human and I want to tell you that I admire the guy who is brave enough to laugh at himself. I am missing Vijay in this situation, but in you I have found an ally, a friend and a teacher. I have enormous respect for you. According to family tradition, when we get married, there’s this ceremony where the bride’s brother welcomes the guests with a sweet dish. That is a privilege given to the most honourable member of the family and I can’t think of anybody else but you doing it. I know I haven’t run it across with you, but I have decided that it will be you.”

Lingaraj looked into the distance. He was feeling emotional for the first time as far as Seema was concerned. Then he said,

“I would be over the ‘jamoon’ doing it.”

“And there will be a lot of people who you can connect with. It will be my responsibility to introduce you to a worthy woman and get you married.”

“Then let’s waste no time, sister. Size is the size in bytes.”

The ‘shmflag’ is something similar to mode in open. It is I_CREAT ‘OR’ed with permissions to create a new segment. And if the segment is already open, it does not say error, rather it is ignored unlike when you use semaphores.

And the return value is the memory segment identifier. -1 on error.

| void *shmat(int shm_id, const void *shm_addr, int shmflg); |

This is for telling which processes have access to the shared memory. This is like attaching a shared memory segment to a process.

shm_id is what you get from shmget(), the shared memory identifier.

shm_addr is the address at which the shared memory is attached to the process. Leave it as a null pointer and the system will handle the assignment.

But if you want to control the memory address, you can use it in conjunction with shmflg. But I would advise you against it. SHM_RND is used if you want to really control the address of the memory segment.

One of the other values of shmflg is SHM_RDONLY which makes the memory segment read only.

Some more values are :

SHM_EXEC allows the code inside the shared memory segment to be executed.

If shmat is successful, it returns a pointer to the first byte of the shared memory.

| int shmdt(const void *shm_addr); |

This deletes a shared memory segment. Not the contents though. It takes the address returned by shmat().

| int shmctl(int shm_id, int command, struct shmid_ds *buf); |

This is for control of the shared memory.

shm_id is the return from shmget.

The commands can be IPC_STAT to obtain status information for the shared memory segment.

IPC_RMID means control. It removes the shared memory segment from the system, destroys it and also the shmid_ds data structure.

The shmid_ds structure contains more details about the shared memory segment.

Let’s look at this writer program,

shm_writer_1254.c

| #include <sys/shm.h>#include <stdio.h>#define key 0x1254int main(){    int shmid = shmget(key,BUFSIZ,0666 &#124; IPC_CREAT);    char *str = (char *) shmat(shmid, (void*)0, 0);    printf("Input some data\n");    fgets(str, BUFSIZ, stdin);    printf("Data written in memory is %s", str);    shmdt(str);} |

Here, a key id defined. This has to be known by the calling program. We then create the shared memory using shmget. The BUFSIZ is usually around 8192, but it also depends on the system. Then attach the memory. Also, we assign a string pointer to the attached memory. So, the value of the string is written to the memory segment.

Next we ask the user to input the string, which is then stored in the string pointer. The next program is also a writer, but the key is changed to 2995 from 1254.

shm_writer_2995.c

| #include <sys/shm.h>#include <stdio.h>#define key 0x2995int main(){    int shmid = shmget(key,BUFSIZ,0666 &#124; IPC_CREAT);    char *str = (char *) shmat(shmid, (void*)0, 0);    printf("Input some data\n");    fgets(str, BUFSIZ, stdin);    printf("Data written in memory is %s", str);    shmdt(str);} |

Now, we look at the reader program for 1254\. The reason we are looking is, we will run these programs in sequence. You shouldn’t have any doubt that a program is writing to a particular memory segment which can only be accessed by another process that knows the key. And not that the memory segment is a default value for all programs which the next program easily reads from without bothering about key consistency.

shm_reader_1254.c

| #include <sys/shm.h>#include <stdio.h>#define key 0x1254int main(){    int shmid = shmget(key,1024,0666);    char *str = (char *) shmat(shmid, (void*)0, 0);    printf("Data read from memory is %s", str);    shmdt(str);    shmctl(shmid,IPC_RMID,NULL);    return 0;} |

In the reader, there is no need to create the memory segment, so no need of IPC_CREAT using shmget. Next, attach to the memory segment and read it into the string.

Let’s look at another reader program. Only the key is changed.

shm_reader_2995.c

| #include <sys/shm.h>#include <stdio.h>#define key 0x2995int main(){    int shmid = shmget(key,BUFSIZ,0666);    char *str = (char *) shmat(shmid, (void*)0, 0);    printf("Data read from memory is %s", str);    shmdt(str);    shmctl(shmid,IPC_RMID,NULL);    return 0;} |

We then run this program.

| $ gcc shm_writer_1254.c$ ./a.outInput some data |

Data 1254

| Data written in memory is Data 1254 |

| $ gcc shm_writer_2995.c$ ./a.outInput some data |

Data 2995

| Data written in memory is Data 2995$ gcc shm_reader_1254.c$ ./a.outData read from memory is Data 1254$ gcc shm_reader_2995.c$ ./a.outData read from memory is Data 2995 |

So, it is not that shared memory access means there is a particular place where the shared memory is stored and the contents of which can be accessed by any program subsequent to the writer program. It depends on the key.

IPC : Message Queues

Lingaraj, as usual began.

“Message queues. What are they?”

“Give me some time. Does it have to be a personal story where the joke’s on me?”

“Anything.”

“When Vijay and I visited a friend of mine, her daughter had painted a car. Vijay went on and started talking about cars. I then cut him midway through his rant and told him, ‘But don’t you think she’s painted it well?’

That was a message cue for him to change the topic.”

“That’s a cue. CUE. I am talking about queues. QUEUE.”

“Oh ok.”

Lingaraj :

| #include <sys/msg.h>int msgctl(int msqid, int cmd, struct msqid_ds *buf);int msgget(key_t key, int msgflg);int msgrcv(int msqid, void *msg_ptr, size_t msg_sz, long int msgtype, int msgflg);int msgsnd(int msqid, const void *msg_ptr, size_t msg_sz, int msgflg); |

A message queue is something like your instant messenger. If I send you messages, the messages are queued. So, when you open the app, they will be delivered.

| int msgget(key_t key, int msgflg); |

You can create or access a message queue with the above system call. key, you know can take on IPC_PRIVATE which does….?”

“Creates a message queue which can be accessible only by the process creating it. And msgflg is usually IPC_CREAT ‘OR’ed with the nine permission bits. No error if IPC_CREAT is used even if there already exists a message queue.

Returns a message queue identifier. -1 on error.” answered  Seema.

“

| int msgsnd(int msqid, const void *msg_ptr, size_t msg_sz, int msgflg); |

This is what you do to send messages.

msqid is the return from msgget.

The msg_ptr argument is a pointer to a  caller-defined structure of the following general form:

struct msgbuf {

long mtype;       /* message type, must be > 0 */

char mtext[1];   /* message data */

};

The msgflg decides what happens if the current message queue is full or the limit in the system for message queues has been reached. There are two scenarios.

| IPC_NOWAIT (Set) |
| IPC_NOWAIT (clear) |

0 on Success and -1 on failure for  msgsnd.

| int msgrcv(int msqid, void *msg_ptr, size_t msg_sz, long int msgtype, int msgflg); |

This receives messages from a message queue.

msqid is again the one returned by msgget

*msg_ptr is a pointer to the message to be received.

msg_sz is the message size.

long int msgtype specifies the type of message.

msgflg sets the priority of the message to be retrieved.

int msgctl(int msqid, int command, struct msqid_ds *buf);

This is for controlling the message queue. One of the commands can be :

IPC_RMID which deletes the message queue.

The ipcs commands.

ipcs -s, ipcs -m, ipcs -q will tell you whether any semaphores, shared memory or message queues still linger around. And if some semaphores or shared memory or message queues still linger after the processes have been completed, you can remove them using

ipcrm -s, ipcrm -m and ipcrm -q , respectively.

The message queue program works kind of the same way as the shared memory when it comes to the apparent procedure.

Let’s look at two programs, the sender first and the receiver next.

mqsender.c

| #include <stdlib.h>#include <stdio.h>#include <string.h>#include <errno.h>#include <unistd.h>#include <sys/msg.h>#define key 0x1254struct message_st {    long int msg_type;    char text[BUFSIZ];};int main(){    int loop_cond = 1;    struct message_st data_passed;    int msgid;    char buffer[BUFSIZ];    msgid = msgget((key_t)key, 0666 &#124; IPC_CREAT);    if (msgid == -1) {        fprintf(stderr, "msgget failed with error: %d\n", errno);        exit(EXIT_FAILURE);    }    while(loop_cond) {        printf("Enter text to be passed. Type 'enough' to stop: ");        fgets(buffer, BUFSIZ, stdin);        data_passed.msg_type = 1;        strcpy(data_passed.text, buffer);        if (msgsnd(msgid, (void *)&data_passed, BUFSIZ, 0) == -1) {            printf("msgsnd failed\n");            exit(EXIT_FAILURE);        }        if (strncmp(buffer, "enough", 6) == 0) {            loop_cond = 0;        }    }    exit(EXIT_SUCCESS);} |

Can you explain what’s happening?” asked Lingaraj.

Seema by now, knew a lot about programming logic and she proceeded to explain.

| #include <stdlib.h>#include <stdio.h>#include <string.h>#include <errno.h>#include <unistd.h>#include <sys/msg.h>#define key 0x1254struct message_st {    long int msg_type;    char text[BUFSIZ];}; |

“We include the necessary header files. Then we define the key which is unique to this program as well as the reader. We declare the structure that holds the message type as well as the message, in this case, a character array which will be later filled with the message input by the user.

| int main(){    int loop_cond = 1;    struct message_st data_passed;    int msgid;    char buffer[BUFSIZ];    msgid = msgget((key_t)key, 0666 &#124; IPC_CREAT);    if (msgid == -1) {        fprintf(stderr, "msgget failed with error: %d\n", errno);        exit(EXIT_FAILURE);    } |

We get into main and after the necessary initialisations, we call msget using the unique key and IPC_CREAT.

We print the relevant message to the screen in case of failure.

|     while(loop_cond) {        printf("Enter text to be passed. Type 'enough' to stop: ");        fgets(buffer, BUFSIZ, stdin);        data_passed.msg_type = 1;        strcpy(data_passed.text, buffer);        if (msgsnd(msgid, (void *)&data_passed, BUFSIZ, 0) == -1) {            printf("msgsnd failed\n");            exit(EXIT_FAILURE);        }        if (strncmp(buffer, "enough", 6) == 0) {            loop_cond = 0;        }    }    exit(EXIT_SUCCESS);} |

We open a loop based on the value of the variable we declared earlier and as long as it is 1, the loop will keep working. Of course, if a condition is met, we change the value of the variable, loop_cond.

We receive input in the loop into a buffer, which is again a character array and the user can go on until he types enough. But I am getting ahead of myself here.

Then we assign 1 to the message type in the structure we declared.

We copy the input string from buffer into the message member of the structure.

Now, we send the message using the message id that is a return from msgget we had called earlier by calling msgsnd. We also sent the structure as a message and specifying the size of the message. Does that include the message type info?”

“No. It doesn’t include the message type.”

“Ok. Then the msgflag is set to 0.

If msgsnd fails, we print that on the screen.

Before exiting the  loop, we check whether the user typed ‘enough’. If that’s the case, we exit the loop and stop receiving input.”

“Here’s the receiver.

mq_receiver.c

| #include <stdlib.h>#include <stdio.h>#include <string.h>#include <errno.h>#include <unistd.h>#include <sys/msg.h>#define key 0x1254struct message_structure {    long int my_msg_type;    char rcvd_text[BUFSIZ];};int main(){    int loop_cond = 1;    int msgid;    struct message_structure data_received;    long int msg_to_receive = 0;    msgid = msgget((key_t) key, 0666 &#124; IPC_CREAT);    if (msgid == -1) {        printf("Failed to access message queue with error: %d\n", errno);        exit(EXIT_FAILURE);    }    while(loop_cond) {        if (msgrcv(msgid, (void *)&data_received, BUFSIZ,                   msg_to_receive, 0) == -1) {            printf("Failed to receive message. The error number is : %d\n", errno);            exit(EXIT_FAILURE);        }        printf("The writer program sent this text: %s", data_received.rcvd_text);        if (strncmp(data_received.rcvd_text, "enough", 6) == 0) {            loop_cond = 0;        }    }    if (msgctl(msgid, IPC_RMID, 0) == -1) {        printf("Failed to delete message queue.\n");        exit(EXIT_FAILURE);    }    exit(EXIT_SUCCESS);} |

”

Seema again proceeded to explain.

“We use the same key, that is 0x1254 and define it.

This declares a structure of the same kind used in the writer program. Here, we make a structure data.received containing the same type of members as in the previous example.

It calls msgget supplying the key and returns the value to msgid. The result of msgget is checked through msgid and an appropriate message is printed.

We start the loop the same way we did in the writer program.

We receive the message in the loop and get it in the data.received structure. Since the message type size is not included, BUFSIZ, the size of the character array would suffice. If msgrcv fails, we print the relevant message.

We come out of the loop and print the text in the second member of the structure. If the message happens to be ‘enough’, we change the loop_cond to reflect 0 and so, it jumps out of the loop.             

We use msgctl to delete the message queue based on msgid.

Exit the program.”

“When we run the program, we run mq_sender.c on one terminal and mq_receiver in another terminal. The output is :

On terminal 1:

| $ ./mq_senderEnter text to be passed. Type 'enough' to stop: This is from the queueEnter text to be passed. Type 'enough' to stop: Going onEnter text to be passed. Type 'enough' to stop: Getting boredEnter text to be passed. Type 'enough' to stop: ByeEnter text to be passed. Type 'enough' to stop: enough |

On terminal 2:

| $ ./mq_receiverThe writer program sent this text: This is from the queueThe writer program sent this text: Going onThe writer program sent this text: Getting boredThe writer program sent this text: ByeThe writer program sent this text: enough |

Sockets

“You can talk to yourself in the context of preparing for an interview. I did that once to prepare well for an interview. I used to simulate the interview panel, consisting of three gentlemen inside my head and used semaphores, pipes and message queues to communicate with them. And shared memory when I was too lazy to answer. I once got into a bus which was empty except for me and the conductor asked for the number of tickets. I said 4 including the interview panel inside my head.”

![](image_rsrc85H.jpg)

“Oh my God! How did you get out of it?”

“Oh, the people in the interview panel I was imagining were very old. They eventually died one after the other. It was then that it stopped. Anyway, the point is, you need a different set of tools to communicate with others.

Let’s talk about communication between two processes which are on different systems. Sockets. Of course, you can use sockets to communicate on the same system, but it is usually for communication between two systems. Which are connected.

Once I was marooned on an island with a woman. This was due to a skydiving parachute malfunction. We both landed on the island. It was evening.

I asked her,

‘Would you like to have dinner?’

She was on the phone and engrossed in her social networking site.

Then she looked up and said,

‘I don’t know you.’

So I sent her a friend request which she accepted. Then she messaged me,

‘I have seen you somewhere.’

![](image_rsrc85J.jpg)

So, you open a socket connection to deal with two different systems. There is a way to build a socket.

Let me give you a context. My grandfather made a cocktail vending machine. It had 3 different dispensing outlets and additional features. The three different outlets were:

1) For the actual drink. This drink varied depending on the customer’s story. If it was a financial crisis, it was a different drink, if it was about not being able to forgive people, it was a different drink, another drink for failed relationships and so on.

2) For snacks. These were drink accompaniments and users had the option of low fat and guilt free.

3) This was for personalised messages. My grandfather used to write a lot of quotes. One particular quote of his, I liked was. “Don’t bother about how little money you made, you are still biodegradable.” So, the appropriate message depending on the customer’s situation was handed out.

Each of these vending slots were named by attaching a sticker which had a number above them and they were also accompanied by a slot for putting coins. Of course, nothing was free and if you wanted just a message and no drinks, you could pay for that alone and get it. ”

So, if I have to give you a parallel.

These dispensing slots, when he made them, were called ports. One for the drink, one for the snack and the other for messages.

He then had to organise. He had to decide some technicalities about how he was going to serve his drinks, whether he had to pour it, or offer it in small packets.

It was his idea of providing service to others and also make money.

He was an active man and did not believe in passive income, more so because he wanted to listen to stories of others. So, he didn’t automate the process. He used a notebook to assign the number of the port, the technicalities and the location of where the cocktail vending machine was placed. This made a package, the port number, the technicalities and the address. He called this package, a socket. Though we are talking about only one machine and you might question the need of the address, but he had plans to expand.

Then he began to listen behind the machine. Each of these dispensers had a button associated with them. When a new customer came and pressed a button, he would look outside and show his ear indicating that he had listened. During evenings, a lot of customers would come.

Now, my grandfather is listening  and is ready. A customer cannot walk in and start telling his sob stories. He has to put a coin first, in the relevant slot for the coin next to the dispensing outlet. My grandfather will then see the coin, and at a glance verify it’s authenticity and then tell the customer that his connection is now accepted.

After the acceptance, my grandfather would write down a number for his reference about the particular client. All of his customers had to pay a membership fee and he remembered the numbers of all his customers. He did this because he was ambitious and wanted to service many customers. So, every customer would be assigned a new socket number internally and the customer did not have to know his internal number.

On the client’s side.

All the customer needed to do was know the location of the cocktail vending machine. Because he had other vending machines that dispensed some tea. And the port number, 1, 2 or 3 for drinks,snacks and the messages respectively. The customer obviously did not know the technical description or the internal membership number. When you are in a mood to drink, you don’t remember such things as a membership number. That was my grandfather’s job.

The client would need to have awareness of what he needed, whether he needed a drink or a message or snacks and at which port they were being supplied.

Let’s look at some system calls.

| #include <sys/types.h>#include <sys/socket.h>int socket(int domain, int type, int protocol); |

A socket is something like a file descriptor.

The domain can be either AF_INET or AF_UNIX or others which we won’t go into.

AF_INET is used in networking as well as the internet.

Type is whether the socket is a stream of data, SOCK_STREAM or a datagram, SOCK_DGRAM. SOCK_DGRAM, was like my first message asking the girl on the island whether she would like to have dinner. There is no guarantee whether the message will be received. But it’s convenient. Datagrams are implemented in UDP /IP and they are unreliable.

I don’t want to give my grandfather’s story as an exact parallel, but in my grandfather’s case, the type was SOCK_STREAM for reliable communication. He could have used SOCK_DGRAM, but he wanted to offer a reliable and stable service. The other reason was that he could have used SOCK_DGRAM after the customers had had a few drinks, but not when they were sober.

The protocol can be either TCP/IP or UDP/IP.

If you are using a stream, you have to use TCP/IP which assures

sequencing, flow control, and retransmission, enabling large data transfers being received with all of the data. An error provision also exists. It is a reliable way to communicate with a guaranteed response. Unless the cable is bitten off by a crocodile.

Now that we know how to create a socket, we have to name it.

| #include <sys/socket.h>int bind(int socket, const struct sockaddr *address, size_t address_len); |

The socket is the socket number. The sockaddr structure which contains the port number, the family and the IP address of the server and the socket file descriptor is made a into a package by binding it to the socket number, so a reference to the socket file descriptor would mean we are talking about that particular port and network address.

The difference between a port and socket is this. A port is part of the socket.

Address is the structure which contains

struct sockaddr_in {

short int                    sin_family;

unsigned short int     sin_port;

struct in_addr           sin_addr;

};

sin_family can be AF_INET though there are other possibilities.

sin_port is the port number and in_addr is the IP address.

If a client has to connect across a network via sockets, it will need the IP address of the server computer. The IP address is something like this 255.255.255.255 where 255 is the maximum. This is a way of identifying the device.

sin_addr, which is the IP address structure is :

struct in_addr {

unsigned long int  s_addr;

};

It returns 0 on success, -1 on error.

Types of errors :

| EBADF | Invalid file descriptor |
| ENOTSOCK | Doesn’t refer to a socket. |
| EINVAL | There is already a socket, by the same identifier which is named. |
| EADDRNOTAVAIL | The address is not available |
| EADDRINUSE | The address has a socket bound to it. |

| #include <sys/socket.h>int listen(int socket, int backlog); |

This enables the socket to listen for incoming connections and allocates a connection queue. backlog is the maximum number of pending connections.

Once the server is ready to listen after the above call, the client side can raise requests.

The server can accept with this system call :

| #include <sys/socket.h>int accept(int socket, struct sockaddr *address, size_t *address_len); |
|  |

The accept() system call creates a new socket to communicate with this particular client and return it’s file descriptor. This is helpful if the server has to service many clients. This is an important point to remember. For every client that has connected to a server socket, there is another number assigned after accept. The address of the client is placed in the sockaddr structure.

If there are no clients, the accept call will block. But you can change this using :

| int flags = fcntl(socket, F_GETFL, 0);fcntl(socket, F_SETFL, O_NONBLOCK&#124;flags); |

Use the O_NONBLOCK setting with the flags.

On the client’s side, all we need is to connect, send or receive and close.

| #include <sys/socket.h>int connect(int socket, const struct sockaddr *address, size_t address_len); |

The socket is the client’s socket and not the server’s socket. The server’s specification is given in the structure sockaddr which has the IP address, the port number, etc.

0 on success and -1 on error. The errors can be :

| EBADF | Invalid file descriptors |
| EALREADY | Connection already in progress for the socket |
| ETIMEDOUT | Connection timeout |
| ECONNREFUSED | Connection was refused by the server. |

You can use write and read system calls to the socket like you do with file descriptors.

You will see this when we get to programming.

| int close(int socket) |

Closes the socket. This can be used both at the server end as well as the client’s end.

In the previous examples of Interprocess Communication, we had keys. A distinct key that brought processes together to cooperate using either queues or shared memory. In sockets, we need the IP address and the port number.

Let’s talk about the localhost. I have always wondered what it would be like to call myself over my phone. I haven’t attempted it yet. “

“Why?”

“What if I answer the phone and say ‘Hello’. I have a fear of parallel universes.

A localhost program allows you to talk to the same system using a network. The IP address used is 127.0.0.1

Let’s start understanding the programs with some pseudocode. I will show you a program later.

For the client1.c

| Include the header files, especially <sys/socket.h>, <netinet/in.h> and <arpa/inet.h>Start the main() function{Declare an integer type socket file descriptor for the  server.Declare a variable and assign it a numberDeclare a structure of the type sockaddr_inCreate the socket using socket( AF_INET, SOCK_STREAM,0) and use the return value for the socket file stream,Fill the details of the structure, also using the functions inet_addr() for the localhost and htons() for a port number wherever necessary. Now connect the socket using the obtained socket file descriptor from the socket() function.Check to see if there are any errors and print the relevant error message, if any.Now, write to the socket, which will go to the server running, using the socket file descriptor returned by the socket() call. You write the number that you have declared.Read from the socket. Here, the server has done an operation on the number. Read the number now.Print the message which says this was the number received from the server.Close the socket file descriptor. |

The above program is the client program.

This is the server program, server1.c

| Include the header files.Declare two integer types for the client socket fd and the server socket fd. Two because, on accept, a new socket address has to be assigned.Declare two structures of type sockaddr_in for both the server and the client addressesCall the socket function as done in the client and assign the returning file descriptor.Fill the members of the structure for the server address using the necessary functions and keeping the port number consistent.Now, bind the socket using bind using the server socket descriptor.Declare an integer variable, because a variable will be received from the client.Start listening using the listen() function using the server socket file descriptor.In a while loop,{print the message about the server statuscall the accept function and assign the new file descriptor to the client socket fd. To accept, you need the server socket fd, the client address and client length.Read the  number from the socket using the returned client socket fd from the call to the accept() function just done.Increment the number.Write the changed number to the socket from which you read.Close the client socket fd.}} |

The above program can be bettered by using fork, where a new child process is created to handle the client’s request. All it needs is a small change in the server program inside the while loop, after the accept. As an exercise, I would want you to do it whenever you are free.

The select() system call.

| #include <sys/types.h>#include <sys/time.h>struct timeval {time_ttv_sec;longtv_usec;}#include <sys/types.h>#include <sys/time.h>int select(int nfds, fd_set *readfds, fd_set *writefds,fd_set *errorfds, struct timeval *timeout); |

The select system call basically is a monitoring system. I had gone to this kung fu school to learn. We were supposed to be doing the moves and suddenly the instructor would say stop. We had to stop and hold the pose for a long time. Then he would monitor us. He would notice if anybody moved and if he did, he would immediately return to the master’s chamber and tell him that somebody moved. Sometimes the master would be doing his own practice and the instructor would have to wait for a specific time duration before he went running inside and told the master how many people had moved.

Select monitors a set of file descriptors if they are ready for reading, writing or whether they have an error condition.

The parameters are :

nfds : The maximum number of file descriptors it can monitor. It is usually the highest file descriptor number plus one.

The fd_set tells the system that it is a file descriptor set and this has to be declared.

readfds refers to the file descriptor set that we want to test are read ready, that is whether they can accept any inputs.

writefds for write ready and errorfds for the set of file descriptors we want to check for an error condition.

The timeval structure contains two members, one specifying user time and the other specifying time in microseconds.

This is the timeout value, when a period of time elapses before select returns with the activated file descriptors.

| #include <sys/types.h>#include <sys/time.h>void FD_ZERO(fd_set *fdset);void FD_CLR(int fd, fd_set *fdset);void FD_SET(int fd, fd_set *fdset);int FD_ISSET(int fd, fd_set *fdset); |

The above are a set of macros.

FD_ZERO initialises the file descriptor set, whether the readfds or writefds or errorfds.

FD_CLR removes a file descriptor from a file descriptor set.

FD_SET adds a file descriptor to a file descriptor set.

FD_ISSET checks whether a file descriptor that belongs to a particular file descriptor set is active. This is done after the return from select to see whether the file descriptor we are interested in is ready for reading or writing or has an error condition.

We will see all this at work in a program shortly.

There are a few more functions to run through.

Computers of different types agree on values for multibyte integers transmitted over a network, using network ordering. Especially port numbers. Different computers may use different ways to denote numbers that need to be used. My house number is 1\. In my mind, I think of it as

((-b) ± √(b²-4ac))

―――――――――――

​ 2a

where

a = 3

b = -6

c = 3

for some reason. If I order food from a food delivery service, I can’t put this in the address box. I have to type in 1\. So, we have functions that act as a go between, between the native host formats and the standard network.

| #include <netinet/in.h>unsigned long int htonl(unsigned long int hostlong); |

Converts host format to standard network long

| unsigned short int htons(unsigned short int hostshort); |

host format to network format short

| unisgned long int ntohl(unsigned long int netlong); |

network to host long

| unsigned short int ntohs(short int ntohs(unsigned short int netshort); |

network to host short

| #include <sys/socket.h>#include <netinet/in.h>#include <arpa/inet.h>in_addr_t inet_addr(const char *cp); |

This function converts your IP address to network form to put it bluntly.

“What if the server and client don’t know the port numbers or the addresses?”

“In such a scenario, there are functions you can use where the complete details of the computer are obtained. Example :

| #include <netdb.h>struct hostent *gethostbyaddr(const void *addr, size_t len, int type);struct hostent *gethostbyname(const char *name); |

This will return a structure

struct hostent {

char *h_name;

char **h_aliases;

int h_addrtype;

int h_length;

char **h_addr_list

};

For services and relevant port numbers :

| #include <netdb.h>struct servent *getservbyname(const char *name, const char *proto);struct servent *getservbyport(int port, const char *proto); |

It returns a structure.

struct servent {

char *s_name;

char **s_aliases;

int s_port;

char *s_proto;

};

| #include <arpa/inet.h>char *inet_ntoa(struct in_addr in) |

This converts an Internet host address to a string in dotted quad format.

| #include <unistd.h>int gethostname(char *name, int namelength); |

This will write the hostname into the string given by name.

Of course, you have to know something about the system you want to have a network with.

For UDP

Like I said, UDP is no guarantee. You construct the programs in a similar manner to TCP/IP but rather than use read and write, you use the following system calls. UDP is a less expensive way of getting some not so important data.

| int sendto(int sockfd, void *buffer, size_t len, int flags,struct sockaddr *to, socklen_t tolen); |

sendto sends to a socket.

| int recvfrom(int sockfd, void *buffer, size_t len, int flags,struct sockaddr *from, socklen_t *fromlen); |

recvfrom system call waits on a socket for a datagram from a specified address and receives it into a buffer.

Let’s look at some programs now, that use select.

The server first.

server_select.c

| #include <sys/types.h>#include <stdio.h>#include <unistd.h>#include <stdlib.h>#include <netinet/in.h>#include <errno.h>#include <string.h>#include <sys/select.h>#include <sys/socket.h>int create_tcp_server_socket(){    struct sockaddr_in saddr;        int fd, ret_val;        fd = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);        printf("Created a socket with fd : %d\n", fd);        saddr.sin_family = AF_INET;        saddr.sin_port = htons(7000);        saddr.sin_addr.s_addr = htonl(INADDR_ANY);        ret_val = bind(fd, (struct sockaddr *)&saddr, sizeof(struct sockaddr_in));        ret_val = listen(fd,5);        return(fd);}int main(){    int nread;    fd_set read_fd_set, testfds;    struct sockaddr_in client_address;    int server_fd, lc = 0, ret_val, i;    int addrlen, fd, fd1;    char buf[100];    server_fd = create_tcp_server_socket();    FD_ZERO(&read_fd_set);    FD_SET(server_fd, & read_fd_set);            while (1)        {            FD_ZERO(&testfds);            testfds = read_fd_set;            printf("Loop %d starting\n", lc);            printf("Starting select in loop %d and waiting\n", lc);    ret_val = select(FD_SETSIZE, &testfds, NULL, NULL, NULL);    printf("Return from select value is : %d\n", ret_val);        if(ret_val < 1) {            perror("server_select");            exit(1);        }    else    {        int new_lc = lc+3; for(fd = 3; fd <= new_lc; fd++){if(FD_ISSET(fd, &testfds)){    if(fd == server_fd)    {        printf("It is a new connection to the server. So grant it\n");        addrlen = sizeof(client_address);        fd = accept(server_fd, (struct sockaddr *)&client_address, &addrlen);        FD_SET(fd, &read_fd_set);        printf("Added client with fd %d\n", fd);           }    else{        printf("The client %d is an already connected one. So read data\n", fd);        read(fd, &buf, sizeof(buf));    printf("\nSize of buf is : %ld and received message: %s\n",sizeof(buf), buf);FD_CLR(fd1, &read_fd_set);    }}    }    }  lc++;    }       } |

Let me explain this :

| int create_tcp_server_socket(){    struct sockaddr_in saddr;        int fd, ret_val;        fd = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);        printf("Created a socket with fd : %d\n", fd);        saddr.sin_family = AF_INET;        saddr.sin_port = htons(7000);        saddr.sin_addr.s_addr = htonl(INADDR_ANY);        ret_val = bind(fd, (struct sockaddr *)&saddr, sizeof(struct sockaddr_in));        ret_val = listen(fd,5);        return(fd); |

The above function creates a tcp socket and passes the value of the returned file descriptor to the calling program. Of course, there is no need for a separate function and you can include this in the main program if you are talking about only one server. But if you want to scale up, this is a good option. The port number will be 7000\. And the client programs too have to stick to this.

| }int main(){    int nread;    fd_set read_fd_set, testfds; |

Here, we declare two sets of file descriptors. One for collecting data and another for testing.

|     struct sockaddr_in client_address;    int server_fd, lc = 0, ret_val, i; |

Here we declare an integer lc which will be used for counting the loop number.

|     int addrlen, fd, client_particular_fd;    char buf[100];    server_fd = create_tcp_server_socket(); |

We call the create tcp server socket function and obtain the resulting file descriptor in server_fd.

|     FD_ZERO(&read_fd_set); |

Initialise the read_fd_set of file descriptors. It is so named because we will be testing whether they are ready for reading.

|     FD_SET(server_fd, & read_fd_set); |

Add the server_fd to the set of file descriptors to be monitored.

| printf("Loop %d starting\n", lc); |

Print the loop number for reference.

|             printf("Starting select in loop %d and waiting\n", lc);while (1)        {            FD_ZERO(&testfds);            testfds = read_fd_set;            printf("Loop %d starting\n", lc);            printf("Starting select in loop %d and waiting\n", lc);    ret_val = select(FD_SETSIZE, &testfds, NULL, NULL, NULL); |

Start select and it begins to monitor to see if there is any activity. It does not tell you where exactly the activity happened when it returns, but there is a way to know. Here, since only testfds is being monitored for reading, there is no need of any other file descriptor set to be passed to select for writing or checking for exceptions . No timeout value either and so, the call will return only when some kind of activity happens. Here, we have used testfds as an extension of read_fd_set because we want to fill up values in read_fd_set, but initialise testfds in the beginning of every iteration. We want to keep the data in read_fd_set intact so to speak. This enables testfds to be altered without losing our previously set file descriptors.

|     printf("Return from select value is : %d\n", ret_val);        if(ret_val < 1) {            perror("server_select");            exit(1);        } |

In case, select fails, this will print the relevant message.

|     else    {        int new_lc = lc+3; |

To talk about the above line, we are banking on some knowledge about the system. We know that 0,1 and 2 stand for standard input, standard output and standard error respectively. If any more file descriptors are created, it will be assigned following a sequence, for the particular process, since they are unique to the process. So, we use this. So, the first file descriptor created after the process begins, is 3, in this case, that of the socket. Subsequently, client file descriptors start from 4.

|  for(fd = 3; fd <= new_lc; fd++) |

Here, we start a for loop that starts at file descriptor 3 and increments. The fd is the file descriptor number.          

| {    if(FD_ISSET(fd, &testfds)) |

We check whether the fd1 file descriptor belonging to the testfds has become active. If so, we proceed.

| {    if(fd == server_fd) |

See whether the server_fd has been activated. It will get activated only if a client has approached the server process for a new connection. As you might remember, after accepting the connection, a new file descriptor particular to the client is used.

|     {             printf("It is a new connection to the server. So grant it\n");        addrlen = sizeof(client_address);        client_particular_fd = accept(server_fd, (struct sockaddr *)&client_address, &addrlen);        FD_SET(client_particular_fd, &read_fd_set);        printf("Added client with client_particular_fd %d\n", fd);           } |

Here, we accept the connection and assign a client particular fd for communications.

|     else{        printf("The file descriptor %d is an already connected one. So read data\n", fd);        read(fd, &buf, sizeof(buf)); |

Here, if it is not a server fd that has been activated, that is, if it’s not a request for a new connection, it must mean an already connected one is trying to pass a message. We print the relevant message to the user. And then read it, using the file descriptor number, fd

|      printf("\nSize of buf is : %ld and received message: %s\n",sizeof(buf), buf);FD_CLR(fd, &read_fd_set);    } |

We print the contents of the message received from the connected client to the user. We use FD_CLR to clear the file descriptor from the set, because if we didn’t do that, it would still be set in the next iteration and it will read the message again from that particular socket. But this presents a couple of limitations, which we will talk about after seeing the output.

| }    }    }  lc++;    }       } |

To test this server’s efficiency, we need two clients. One that connects to the server and passes a message after 15 seconds. And the other that connects to the server and passes the message immediately. We run this one after the other so the server has to shift between accepting incoming messages and accepting new connections.

client_select_1.c

| #include <sys/types.h>#include <sys/time.h>#include <stdio.h>#include <fcntl.h>#include <unistd.h>#include <stdlib.h>#include <netinet/in.h>#include <arpa/inet.h>#include <errno.h>#define DATA_BUFFER "Because Seema learnt Linux"int main(){    char input[100];    struct sockaddr_in saddr;        int fd, ret_val;        struct hostent *local_host;        fd = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);        printf("Created a socket with fd : %d\n", fd);        saddr.sin_family = AF_INET;        saddr.sin_port = htons(7000);        saddr.sin_addr.s_addr = inet_addr("127.0.0.1");        ret_val = connect(fd, (struct sockaddr *)&saddr, sizeof(struct sockaddr_in));        printf("Socket is now connected.\n");        printf("Sleep 15 seconds before sending data.\n");        sleep(15);        ret_val = write(fd, DATA_BUFFER, sizeof(DATA_BUFFER));        printf("Sent data : %d length and : %s", ret_val, DATA_BUFFER);        close(fd); } |

client_select_2.c

| #include <sys/types.h>#include <sys/time.h>#include <stdio.h>#include <fcntl.h>#include <unistd.h>#include <stdlib.h>#include <netinet/in.h>#include <errno.h>#include <arpa/inet.h>#define DATA_BUFFER "Vijay has changed"int main(){    char input[100];    struct sockaddr_in saddr;        int fd, ret_val;        struct hostent *local_host;        fd = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);        printf("Created a socket with fd : %d\n", fd);        saddr.sin_family = AF_INET;        saddr.sin_port = htons(7000);        saddr.sin_addr.s_addr = inet_addr("127.0.0.1");        ret_val = connect(fd, (struct sockaddr *)&saddr, sizeof(struct sockaddr_in));        printf("Socket is now connected.\n");        ret_val = send(fd, DATA_BUFFER, sizeof(DATA_BUFFER), 0);        printf("Sent data : %d length and : %s", ret_val, DATA_BUFFER);        close(fd);        } |

We run the server_select.c first and in different terminals, run client_select_1.c and client_select_2.c

We get this output on the terminal we started the server:

| Created a socket with fd : 3Loop 0 startingStarting select in loop 0 and waitingReturn from select value is : 1It is a new connection to the server. So grant itAdded client with fd 4Loop 1 startingStarting select in loop 1 and waitingReturn from select value is : 1It is a new connection to the server. So grant itAdded client with fd 5Loop 2 startingStarting select in loop 2 and waitingReturn from select value is : 1The client 5 is an already connected one. So read dataSize of buf is : 100 and received message: Vijay has changedLoop 3 startingStarting select in loop 3 and waiting |

This is after the sleep in the client_select_1.c before the message. This waits for 15 seconds. Atleast.

| Return from select value is : 1The client 4 is an already connected one. So read dataSize of buf is : 100 and received message: Because Seema learnt LinuxLoop 4 startingStarting select in loop 4 and waiting |

Now, the limitations.

One. The maximum number of file descriptors select can monitor depends on FD_SETSIZE. If the loop count exceeds FD_SETSIZE, the program is not equipped to know and take appropriate action. So, the obvious solution would be to iterate for only a particular number of times, given by FD_SETSIZE in the for loop.

Two. If the client_select_1 process decided to send another message after the ‘Because Seema learn Linux’ waiting for another 10 seconds after the first message, it wouldn’t be read by the server. Because we have removed the fd from the read_fd_set. Until the client closes the connection, we would ideally want it to be on the read_fd_set. There are ways to get around this limitation. One way is to find out the return value of the read call on the socket. If the return value is zero on activation, it means the client has closed the connection. We then proceed to close the client socket file descriptor on the server’s side. Since we are closing only the sockets that have finished on the client’s side and not clearing those that haven’t finished on the client’s side, we will have the socket file descriptors of the open clients in the set of file descriptors to be checked for reading activity in the next iteration. The ones closed are not activated again.

Also, it said ‘Loop 0’ starting. Doesn’t look correct. So, we introduce these changes in server_select2.c

server_select2.c

| #include <sys/types.h>#include <stdio.h>#include <unistd.h>#include <stdlib.h>#include <netinet/in.h>#include <errno.h>#include <string.h>#include <sys/select.h>#include <sys/socket.h>int create_tcp_server_socket(){    struct sockaddr_in saddr;        int fd, ret_val;        fd = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);        printf("Created a socket with fd : %d", fd);        saddr.sin_family = AF_INET;        saddr.sin_port = htons(7000);        saddr.sin_addr.s_addr = htonl(INADDR_ANY);        ret_val = bind(fd, (struct sockaddr *)&saddr, sizeof(struct sockaddr_in));        ret_val = listen(fd,5);        return(fd);}int main(){    int nread;    fd_set read_fd_set, testfds;    struct sockaddr_in client_address;    int server_fd, lc = 1, ret_val, i;    int addrlen, fd;    char buf[100];    server_fd = create_tcp_server_socket();    FD_ZERO(&read_fd_set);    FD_SET(server_fd, & read_fd_set);            while (1)        {            FD_ZERO(&testfds);            testfds = read_fd_set;            printf("Loop %d starting\n", lc);            printf("Starting select in loop %d and waiting\n", lc);            ret_val = select(FD_SETSIZE, &testfds, NULL, NULL, NULL);            printf("Return from select value is : %d\n", ret_val);            if(ret_val < 1) {            perror("server5");            exit(1);        }    else    {         for(fd = 3; fd <= FD_SETSIZE; fd++){if(FD_ISSET(fd, &testfds)){    if(fd == server_fd)    {        printf("It is a new connection to the server. So grant it\n");        addrlen = sizeof(client_address);        fd = accept(server_fd, (struct sockaddr *)&client_address, &addrlen);        FD_SET(fd, &read_fd_set);        printf("Added client with fd %d\n", fd);           }           else                    {                        printf("It %d is an already connected one. So read data\n", fd);        sleep(5);    printf("Client fd is : %d", fd);    if(read(fd, &buf, sizeof(buf)) == 0)    {        printf("The client has closed the connection\n");        FD_CLR(fd, &read_fd_set);        close(fd);    }    else    {    printf("\nSize of buf is : %ld and received message: %s\n",sizeof(buf), buf);    sleep(5);    }                    }                }}    }lc++;        }    } |

And the modified client_select_twice.c looks like this.

client_twice.c

| #include <sys/types.h>#include <sys/time.h>#include <stdio.h>#include <fcntl.h>#include <unistd.h>#include <stdlib.h>#include <netinet/in.h>#include <errno.h>#include <arpa/inet.h>#define DATA_BUFFER "Because Seema learnt Linux"#define DATA_BUFFER2 "New message from connected client"int main(){    char input[100];    struct sockaddr_in saddr;        int fd, ret_val;        struct hostent *local_host;        fd = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);        printf("Created a socket with fd : %d\n", fd);        saddr.sin_family = AF_INET;        saddr.sin_port = htons(7000);        saddr.sin_addr.s_addr = inet_addr("127.0.0.1");        ret_val = connect(fd, (struct sockaddr *)&saddr, sizeof(struct sockaddr_in));        printf("Socket is now connected.\n");        printf("Sleep 15 seconds before sending data.\n");        sleep(15);        ret_val = write(fd, DATA_BUFFER, sizeof(DATA_BUFFER));        printf("Sent data : %d length and : %s", ret_val, DATA_BUFFER2);        printf("Sleep 10 seconds before sending another message\n");        sleep(10);        ret_val = write(fd, DATA_BUFFER2, sizeof(DATA_BUFFER2));        printf("Sent data : %d length and : %s", ret_val, DATA_BUFFER2);        close(fd); } |

The output after we run all the programs like we did the last time, in each terminal for the sake of clarity.

| Created a socket with fd : 3Loop 1 startingStarting select in loop 0 and waitingReturn from select value is : 1It is a new connection to the server. So grant itAdded client with fd 4Loop 2 startingStarting select in loop 1 and waitingReturn from select value is : 1It is a new connection to the server. So grant itAdded client with fd 5Loop 3 startingStarting select in loop 2 and waitingReturn from select value is : 1The client 5 is an already connected one. So read dataSize of buf is : 100 and received message: Vijay has changedLoop 4 startingStarting select in loop 3 and waitingReturn from select value is : 1The client 5 is an already connected one. So read dataThe client has closed the connectionLoop 5 startingStarting select in loop 4 and waiting |

This happens after the first sleep in client_select_twice before the first message.

| Return from select value is : 1The client 4 is an already connected one. So read dataSize of buf is : 100 and received message: Because Seema learnt LinuxLoop 6 startingStarting select in loop 5 and waiting |

After the second sleep in the client_select_twice after the first message.

| Return from select value is : 1The client 4 is an already connected one. So read dataSize of buf is : 100 and received message: New message from conn clientLoop 7 startingStarting select in loop 6 and waitingReturn from select value is : 1The client 4 is an already connected one. So read dataThe client has closed the connectionLoop 8 startingStarting select in loop 7 and waiting |

Here, if you notice, select returns even if a connection from a client closes. From our perspective, we don’t know this yet. It could be data ready also. But when we proceed to read after testing for FD_ISSET, then, we get a return value of zero on the read call for the socket. Then the relevant message gets printed on the screen.

Another solution is use the ioctl system call. This can be operated on a socket file descriptor and checked to see whether the client_particular_fd is active on the client’s side. If it is closed, then we proceed to close it on the server side and clear the file descriptor using FD_CLR(fd, &read_fd_set).

I think this will do for a start.” said Lingaraj and shut down his laptop.

Seema sensed the learning project was over. Lingaraj had made it enjoyable and she wanted to thank him. She then reasoned he had spent his time and resources teaching her and he had to be financially compensated. She did not know how to put that question. She was vacillating and Lingaraj perceived the dilemma.

“You owe me nothing. Not because I can’t do with some money, but because you are a shero. You have really come out of your comfort zone and have done things for love. It takes courage and I have seen another aspect of humanity through this episode. To some of your questions, I have retorted bordering on the insult, I have made fun of you sometimes and you didn’t complain.”

“That’s because I know where you are coming from. You have been a great friend and banter is allowed. I will miss these sessions. If I become a famous programmer, I will mention you in my speech.”

“I will take it as a compliment. Talking of compliments, there was this incident that happened with me.

I once gave a speech about how one has to be truthful. By the end of the speech, there was only one guy who was listening.

![](image_rsrc85K.jpg)

I went on for an hour more and after I had finished, I asked him why he was still lingering, even though the others had left and the program was over.

‘Oh, I played truth or dare. I chose dare. Next time, I will choose the truth.’ he said.

I took it as a compliment.” said Lingaraj.

“I can tell you it wasn’t a compliment. But you will get enough of them in your life.”

“Go ahead and get Vijay back to normal. Keep me updated.”

“Sure.”

Seema hugged Lingaraj and left. 

Epilogue

Seema had learnt enough. It was evident in the way Vijay started to behave. Seema had started using impersonal statements and slowly over a period of time, accessed his memory and reminded him of his human side. It worked. Vijay was back to normal and took Seema to his favourite Pizza joint. He began showering love on Seema and was very grateful to her.

They got married and Lingaraj was given the honour of welcoming the guests with sweets.

![](image_rsrc85M.jpg)

He was introduced to one Santrupthi by Seema and the both of them found overlapping interests.

![](image_rsrc85N.jpg)