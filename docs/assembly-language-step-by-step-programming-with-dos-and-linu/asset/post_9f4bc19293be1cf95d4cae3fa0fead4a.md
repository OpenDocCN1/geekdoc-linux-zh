
## The Right to Assemble

The other (and more interesting) thing that operating systems do run programs. It is here that DOS seems godlike than troll-like. When you want to run a program on your computer, you type its name in the DOS command line. DOS goes out and searches for one more disk for the named program, loads it into memory at a convenient spot, sets the instruction pointer to the start of the program, and boosts the CPU in the rear to get it.

DOS then patiently waits for the program to run its course and stop. When the program stops, it hands the CPU obediently back to DOS, which again tilts a hand to its ear and listens for your next command from the command line.

So, as programmers, we use DOS two ways: One is as a sort of toolkit, an army of trolls each of which can perform some service for your program, thereby saving your program effort. The other is as a means of loading a program into memory and getting it going, and then catching the machine gracefully on the rebound when your program is through.

I mention DOS again and again in this book. Wherever you look in 16-bit assembly language, you’re going to see the old troll’s face. Used to it.

## DOS Files: Magnetic Memory

Very simply, DOS files are memory banks stored on a magnetic coating rather than inside silicon chips. A DOS file contains some number of bytes, stored in a specific order. One major difference from RAM memory is that DOS files stored on disk are sequential-access memory banks.

A disk (be it floppy or hard) is a circular platform coated with magnetic plastic of some sort. (Here, magnetic plastic is simply a polymer in which iron oxide particles or something similar is embedded.) In a floppy disk drive, the platform is a flexible disk of tough plastic; in a hard disk, the platform is a rigid platter of aluminum metal. Data is stored as little magnetic disturbances over the plastic coating in a fashion similar to that used in audio cassettes and VCRs. A sensor called a read/write head sits very close to the rotating platform and waits for the data to pass by.

A simplified illustration of a rotating disk device is shown in Figure 4.1. The area of the disk is divided into concentric circles called tracks. The tracks are further divided radially into sectors. A sector (typically con-

![](img/5af1f694a521bb214c2fd03b770b346f_105_0.png)

**Figure 4.1** Rotating disk storage.

taining 512 bytes) is the smallest unit of storage that can be read or written at one time. A DOS disk file consists of one or more sectors containing the file's data.

The read/write head is mounted on a sliding shaft that is controlled by a solenoid mechanism. The solenoid can move the head horizontally to position the head over a specific track. (In Figure 4.1, the head is positioned over track 2—counting from 0, however!) However, once the head is over a particular track, it has to count sectors until the sector it needs passes beneath it. The tracks can be accessed at random, just like bytes in the computer's memory banks, but sectors within a track must be accessed sequentially.

Perhaps the single most valuable service DOS provides is handling the headaches of distributing data onto empty sectors on a disk. Programs can hand sectors of data to DOS, one at a time, and let DOS worry where on the disk they can be placed. Each sector has a number, and DOS keeps track of what sectors belong together as a file. The first sector in a file might be stored on track 3, sector 9; the second sector might be stored on track 0, sector 4, and so on. You do not have to worry about that. When you ask for sector 0 of your file, DOS looks up its location in

its private tables and goes directly to track 3, sector 9 and brings the sec-’s data back to you.

## Binary Files

The data stored in a file are just binary bytes and can be anything at all. Like files like this, where there are no restrictions on the contents of a file, are called binary files, since they can legally contain any binary code. Like all files, a binary file consists of some number of sectors, with each sector (typically) containing 512 bytes. The least space any file on your disk occupies is 512 bytes; when you see the DOS DIR command tell you a file has 17 bytes in it, that’s the count of how many bytes were stored in that file but like a walk-in closet with only one pair of shoes in it, the rest of the sector is still there, empty but occupying space on the disk.

A binary file has no structure, but is simply a long series of binary codes divided into numbered groups of 512 and stored out on disk in a scheme that for now is best left to DOS to understand. Later on, you can study up on it, especially once you learn about Linux, in which entire file systems can be loaded as though they were just more pro-grams—which, of course, they are.

## Text Files

If you’ve ever tried to use the DOS TYPE command to display a binary file (like an .EXE or .COM file) to the screen, you’ve seen some things indeed. There’s no reason for such files to be intelligible on the screen; they’re intended for other “eyes,” typically the CPU’s.

There is a separate class of files that is specifically restricted to containing human-readable information. These are text files, because they contain the letters, digits, and symbols of which printed human information (text) is composed.

Unlike binary files, text files have a certain structure. The characters in text files are divided into lines. A line in a text file is defined not so much by what it contains as how it ends. A special series of characters called end-of-line (EOL) marker tags the end of a line. The first line in a text file runs from the first byte to the first EOL marker; the second line starts immediately after the EOL marker, and so on. The text characters falling between two EOL markers are considered a single line.

This scheme is the same for both DOS and Linux. What differs is the exact nature of the EOL marker. The EOL marker for DOS is not one character but two: the carriage return character (called CR by those who know it) followed by the linefeed character (similarly called LF). Why do two characters want to end a line in a text file? Long ago, there was (and still is, at hamfests) an incredible mechanical nightmare called Teletype machine. These were invented during World War II as robot typewriters that could send written messages over long distances through electrical signals. As was a mechanical operation to return the typing carriage to the left margin of the paper (carriage return) and another to feed the paper up to expose the next clean line of paper to the typing carriage (line feed). A separate electrical signal was required to do each of these operations, and while I don't know why that was necessary, it has carried over into the dawn of the twenty-first century in the form of those two characters, CR and LF. Not only is this a case of the tail wagging the dog, it's a case of the tail walking around 30 years after the poor dog rolled over and died.

Figure 4.2 shows how CR and LF divide what might otherwise be a single string of characters into a structured sequence of lines. It's important to understand the structure of a text file because structure dictates how some important software tools operate, as I explain a little later.

The CR is actually character 13 in the ASCII character set summarized in Appendix D. The LF character is character 10. They are two of a set of invisible characters called whitespace, indicating their role in positioning text characters ('*', etc.) within the white space of a text page. The other whitespace characters include the space character itself (32), the tab character (character 9), and the form feed character (character 12), which can optionally divide a text further into pages.

## Living Fossils

Another character, the bell character (BEL), falls in between binary and text characters. When displayed or printed, it signals that a tone should
