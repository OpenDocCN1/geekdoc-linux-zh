
0001011011
01010111100110110
0000010101111101100001
00000011000010111001001
00110111010010011001010110
0011011011010000100011100
0100011100001011000110101
1000111100100100000111000110
01000110010100100000011010110
01110110111010110110011001000
00000110001011001010111111001
00010110110001100101001000001
01010110010111010010100100000
000001010110111011000010110011
000001100001011101000111010011
001101101110100100110110011
00110110000101100010111001100
0100011110010010000011001101
000000111
011101
000001
000101
0101011
00000101 10101
000001100
11101 10101100
10110101100001101110
00001101000110110
1001001000001100
01110110110111110101111
00000
0001011100101101011100001100
000101101100110011001001000000110
010101101100101100101011001000
00000101011101100001001101
00
01
00
10
00
0101011011001000
00
011001011000001101
0111011011100101100101000001
0000011000101100101011100110101111010001
00010110110001
0101011100110 010011000010000001
1100110001001101
000001010 0001100001
10110111
0111010
010000
01 01 001000 011010
01 01 01 01 10
0110 011001 01 10
01 01 01 00 00
01 00 011001 011001

![](img/4aefeb2d095f688b34af6207870c5f39_48_0.png)

![](img/4aefeb2d095f688b34af6207870c5f39_48_1.png)

![](img/4aefeb2d095f688b34af6207870c5f39_48_2.png)

Developed as a prank back in '82, Elk Cloner was one of the first recorded viruses in the wild.

## Using Comments

While comments may seem like a minor element to the many lines of code that combine to make a game, application or even an entire operating system, in actual fact they're probably one of the most important factors.

### The Importance of Commenting

Comments inside code are basically human readable descriptions that detail what the code is doing at that particular point. They don't sound especially important but code without comments is one of the many frustrating areas of programming, regardless of whether you're a professional or just starting out.

In short, all code should be commented in such a manner as to effectively describe the purpose of a line, section or individual elements. You should get in to the habit of commenting as much as possible, by imagining that someone who doesn't know anything about programming can pick up your code and understand what it's going to do simply by reading your comments.

In a professional environment, comments are vital to the success of the code and ultimately, the company or project. In an organization, many programmers work in teams alongside engineers, other developers, hardware analysts and so on. If you're a part of the team that's writing a bespoke piece of software for the company, then your comments help save a lot of time should something go wrong and another team member has to pick up and follow the trail to pinpoint the issue.

![](img/4aefeb2d095f688b34af6207870c5f39_49_0.png)

Place yourself in the shoes of someone whose job is to find out what's wrong with a program. The program has in excess of 800,000 lines of code, spread across several different modules. You can soon appreciate the need for a little help from the original programmers in the form of a good comment.

The best comments are always concise and link the code logically, detailing what happens when the program hits a line or section. You don't need to comment on every line. Something along the lines of: if x==0 doesn't require you to comment that if x equals zero then do something; that's going to be obvious to the reader. However, if x equalling zero is something that drastically changes the program for the user, such as, they've run out of lives, then it certainly needs to be commented on.

Even if the code is your own, you should write comments as if you were going to share it with others publicly. This way you can return to that code and always understand what it was you did or where it was you went wrong, or what worked brilliantly.

Comments are good practise and once you understand how to add a comment where needed, you soon do it as if it's second nature.

```
DEFB    26h,30h,32h,26h,30h,32h,0,0,32h,72h,73h,32h,72h,73h,32h
        60h,61h,32h,40h,40h,32h,42h,45h,32h,42h,45h,32h,4C0
        52h,4Ch,52h,5Ch,5Dh,5Eh,5Fh,59h,5Ch,5Dh,5Eh,5Fh,5Ch
        66h,67h,32h,72h,73h,4C0,4C0,45h,45h,45h,57h,52h,50h,CC0h
        13h,80h,0,19h,80h,81h,32h,82h,80h,CC0h,0FFh

T$58C:
DEFB    80h,72h,66h,54h,56h,60h,56h,60h,51h,56h,51h,66h
        54h,56h,58h,5Ch,72h,56h,60h,56h,4Eh,54h,51h,60h,51h,51h
        5Eh,5Eh,56h,56h,50h,50h,72h,66h,60h,4Eh,5Ch,51h,56h,51h,66h
        51h,51h,54h,56h,54h,56h,56h,72h,4C0,60h,56h,4Eh,54h,60h
        56h,66h,60h,56h,56h,56h,5Eh,5Eh,56h

        ; Game restart point
        
START:  XOR     A
        LD      (RESET),A
        LD      (XEMP),A
        LD      (REDO),A
        LD      (B$458),A
        LD      (B$459),A
        LD      A,2           ;Initial lives count
        LD      (LIVES),A
        LD      HL,T$45C
        SET     0,(HL)
        LD      HL,SCREEN
        LD      DE,SCREEN+1
        LD      BC,77FB       ;Clear screen image
        LD      (HL),0
        LDIR
        LD      HL,0A000h     ;Title screen bitmap
        LD      DE,SCREEN
        LD      BC,4096
        LDIR
        LD      HL,SCREEN+80h + 1*32 + 29
        LD      DE,MAM03+44
        CALL        C,0
        LD      (EMPKP
        LD      HL,0FC00h   ;Attributes for the last room
        LD      DE,ATTR   ;top third
        LD      BC,716
        LDIR
        LD      HL,09E00h   ;Attributes for title screen
        LD      BC,512      ;(bottom two-thirds)
        LDIR
        LD      BC,31
        RET
B$6621:  XOR     A
        IN      E,(C)
        OR      E
        DJNZ    B$6621    ;8+03
        AND     230h
        JR      NZ,B$662F    ;8+07
        LD      A,1
```

## C++ Comments

Commenting in C++ involves using a double forward slash `//` or a forward slash and an asterisk `/*`. You've already seen some brief examples but this is how they work.

- **STEP 1** Using the Hello World code as an example, you can easily comment on different sections of the code using the double forward slash:

```
//My first C++ program

cout << "Hello, world!\n";
```

![](img/4aefeb2d095f688b34af6207870c5f39_50_0.png)

- **STEP 2** However, you can also add comments to the end of a line of code, to describe it in a better way what's going on:

```
cout << "Hello, world!\n"; //This line outputs the words ‘Hello, world!’. The `\n` denotes a new line.
```

Note, you don't have to put a semicolon at the end of a comment. This is because it's a line in the code that's ignored by the compiler.

![](img/4aefeb2d095f688b34af6207870c5f39_50_1.png)

- **STEP 3** You can comment out several lines by using the forward slash and asterisk:

```
/* This comment can
cover several lines
* without the need to add more slashes */
```

Just remember to finish the block comment with the opposite asterisk and forward slash.

![](img/4aefeb2d095f688b34af6207870c5f39_50_2.png)

- **STEP 4** Be careful when commenting, especially with block comments. It's very easy to forget to add the closing asterisk and forward slash and thus negate any code that falls inside the comment block.

![](img/4aefeb2d095f688b34af6207870c5f39_50_3.png)

- **STEP 5** Obviously if you try and build and execute the code it errors out, complaining of a missing curly bracket `}` to finish off the block of code. If you've made the error a few times, then it can be time consuming to go back and rectify. Thankfully, the colour coding in Geany helps identify comments from code.

![](img/4aefeb2d095f688b34af6207870c5f39_50_4.png)

- **STEP 6** With block comments, it's good practise in C++ to add an asterisk to each new line of the comment block. This also helps you to remember to close the comment block before continuing with the code:

```
/* This comment can
* cover several lines
* without the need to add more slashes */
```

Thankfully, Geany does this automatically but be aware of it when using other IDEs.

![](img/4aefeb2d095f688b34af6207870c5f39_50_5.png)
