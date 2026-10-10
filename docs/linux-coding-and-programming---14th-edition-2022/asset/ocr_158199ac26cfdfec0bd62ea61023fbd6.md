# Using Comments

While comments may seem like a minor element to the many lines of code that combine to make a game, application or even an entire operating system, in actual fact they're probably one of the most important factors.

# THE IMPORTANCE OF COMMENTING

Comments inside code are basically human readable descriptions that detail what the code is doing at that particular point. They don't sound especially important but code without comments is one of the many frustrating areas of programming, regardless of whether you're a professional or just starting out.

In short, all code should be commented in such a manner as to effectively describe the purpose of a line, section or individual elements. You should get in to the habit of commenting as much as possible, by imagining that someone who doesn't know anything about programming can pick up your code and understand what it's going to do simply by reading your comments.

In a professional environment, comments are vital to the success of the code and ultimately, the company or project. In an organisation, many programmers work in teams alongside engineers, other developers, hardware analysts and so on. If you're a part of the team that's writing a bespoke piece of software for the company, then your comments help save a lot of time should something go wrong and another team member has to pick up and follow the trail to pinpoint the issue.

![](bbox=[0.06, 0.65, 0.47, 0.95])

> Place yourself in the shoes of someone who's job it is to find out what's wrong with a program. The program has in excess of 800,000 lines of code, spread across several different modules. You can soon appreciate the need for a little help from the original programmers in the form of a good comment.

The best comments are always concise and link the code logically, detailing what happens when the program hits a line or section. You don't need to comment on every line. Something along the lines of if x==0 doesn't require you to comment that if x equals zero then do something; that's going to be obvious to the reader. However, if x equaling zero is something that drastically changes the program for the user, such as, they've run out of lives, then it certainly needs to be commented on.

Even if the code is our own, you should write comments as if you were going to share it with others publicly. This way you can return to that code and always understand what it was you did or where it was you went wrong, or what worked brilliantly.

Comments are good practice and once you understand how to add a comment where needed, you soon do it as if it's second nature.

```
```
DEFS  240,320,328,320,320,320,0,3,328,728,720,323,728,328,329
DEFS  600,600,528,4C,4DB,328,4C3,528,4C0,4C0,2C2D,4C9,6
DEFS  32A,4C8,98C,32D,328,32C,32A,34C,37C,32A,3C9,3C2D,42B,8
DEFS  340,32B,340,32D,32B,3C2D,32B,42B,42D,32B,42B,47B,45H
DEFS  64B,47B,52B,73B,73D,44B,440,448,37B,32A,3C9,3C2B
DEFS  1,0B,0B,0,5,1B0,69B,415,32B,43B,6C8B,8FB9

THISG:
DEFS  60B,72B,4C0,64B,60B,56B,1B0,1,1,82,44B,51B,51B,5B0,54
DEFS  5B0,5B0,72B,72B,6B0,6B0,56B,5B0,56B,52B,60B,51B,51B
DEFS  52B,54B,54B,54B,60B,73B,6B0,6B0,44B,44B,55B,51B,51B
DEFS  51B,51B,5B0,5B0,56B,56B,52C,72B,6B0,82B,60D,6B0,54B,52
DEFS  54B,44B,82B,46B,46B,34B,54B,3B0

; Game restart point
START:
LD      A           ;Initial live count
LD      (SCREEN),A
LD      (SCREEN+1),A
LD      (SCREEN+2),A
LD      A,2
LD      (SCREEN+3),A
LD      HL,TASC
LD      SET,0,(HL)
LD      HL,SCRE
LD      DE,SCREEN+1
LD      BC,1777H    ;Clear screen image
LD      (DE),r
LDIR    HL,00800H   ;Title screen bitmap
LD      DE,SCREEN
LDIR    BC,4096

LD      HL,SCRE+5000+8000+1752+29
LD      DE,WINH+2C4
CALL    NINCHY
LD      HL,0F0C0H           ;Attributes for last room
LD      DE,ATTR
LDIR    BC,256
LDIR

LD      HL,0080H           ;Attributes for title screen
LD      DE    (Bottom two-attributes)
LD      A,3

DRAG1:
LOOP    5,(C)
AND     I,D2
AND     50B
JOR     HZ,36672,3D401
LD      A,1
```
```