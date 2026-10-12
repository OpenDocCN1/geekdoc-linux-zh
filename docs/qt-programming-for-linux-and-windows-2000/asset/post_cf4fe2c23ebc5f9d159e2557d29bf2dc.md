
## Contents

### Collections
- QCollection 147
- QDict 147
- QDictIterator 148
- QIntCache 148
- QIntCacheIterator 148
- QIntDict 148
- QIntDictIterator 148
- QIntValidator 148
- QList 148
- QListIterator 149
- QMap 149
- QMapConstIterator 149
- QMapIterator 149
- QPtrDict 149
- QPtrDictIterator 149
- QQueue 149
- QSortedList 149
- QStack 149
- QString and QStrList 150
- QStringListIterator 150
- QStringList 150
- QValueList 150
- QValueListConstIterator 150
- QValueListIterator 150
- QValueStack 150
- QVector 150

### Text Handling
- QChar 151
- QClipboard 151
- QConstString 151
- QCString 151
- QDoubleValidator 151
- QRegExp 151
- QString 151
- QTextCodec 151
- QTextDecoder 151
- QTextEncoder 152
- QTranslator 152
- QValidator 152

### Date and Time
- QDate 152
- QDateTime 152
- QTime 152

### Miscellaneous
- QRangeControl 153
- QGuardedPtr 153
- QMimeSource 154
- QMimeSourceFactory 154
- QPoint 154
- QPointArray 154
- QRect 154
- QSignal 154
- QSignalMapper 154
- QSize 154
- QTimer 154
- QVariant 156
- QWMatrix 156
- Summary 156

## 6 THE QT NAMESPACE AND QT EXTENSIONS 157
- Qt Class 157
- Qt Extensions 161
    - OpenGL Extension 161
    - Networking Support 162
- Summary 162

### PART III DEVELOPING PROFESSIONAL QT APPLICATIONS 163

## 7 QT DEVELOPMENT CONSIDERATIONS 165
- Internalization 166
    - Use QString 167
    - QObject::tr() 168
    - findtr Utility 169
    - msg2qm Utility 170
    - mergeqt Utility 171
    - Input Methods 171
- Platform-Independent Projects 172
    - Tmake Utility 173
- Object Reuse Considerations 173
    - Keep It Simple and to the Point 173
    - Always Consider Performance... 174
    - Know Your Compiler 174
    - Assume Nothing 174
    - Use Slots For Exposed void-return Methods 175
- Dynamic and Static Linkage 175
    - Big Programs 176
    - Compatibility 176
    - Possible Solutions 176
    - Configuration Management 177
    - Total Static Linkage 177
    - Mixed Static/Dynamic Linkage 177
- Debugging Projects 178
    - Documentation and Training Bugs 179
    - User Perception Defects 179
    - Software Defects 180
    - Defect Event Capture 180
    - Core Dump Analysis (Linux/Unix only) 188
    - Dr. Watson (Windows only) 189
    - Using A Debugger 189
- Rapid Application Development 190
    - Qt Architect 190
    - QteZ 190
    - KDevelopp 191
    - Ebuilder 191
- Summary 192

## 8 WINDOWS 2000 TOPICS 193
- DDE Server Class 193
- Multimedia Support 197
- Summary 210

## APPENDIX A 212

## APPENDIX B 266

## INDEX 269

## Foreword

In the summer of 1991, I sat together with Haavard Nord on a park bench in Trondheim, Norway. We were both working on the same medical database project at the Regional Hospital in Trondheim. We were discussing how to proceed with the user interface when Haavard said, "We need an object-oriented display system."

A year later I had made a C++ GUI toolkit because of that statement. After another year the company I had made it for (and was then working for) decided to scrap it for Motif. I thought they were crazy. Haavard called me up one night and said, "Let's build a new and better toolkit from scratch. Quit your job and start a company together with me."

Haavard first did his thesis on making the first Qt kernel. Then, for a year, we hacked day and night in a small office and lived off our wives. We had the luxury of working undisturbed. Qt gradually took form, we polished the details, designed and re-designed until things just felt right (a design rule Trolltech still follows). We then got a small consultancy contract where we used our still quite primitive version 0.60 of Qt, hired Arnt Gulbrandsen for a ridiculously low salary, and the snowball started rolling.

I had never imagined that one day I would write a foreword for a book about Qt from Prentice Hall. Many of our dreams have come true, and this is another one of them.

I have had the pleasure of meeting Patric Ward, the author of this book. In addition to being a mighty fine Qt hacker, he is also a very nice guy with a good sense of humor. I think that's a perfect combination for writing a book like this one. Now sit back and enjoy the wonders of Qt, as narrated by Patric Ward. The word is yours, Pat.

Eirik Eng, 
President, Trolltech AS

## Preface

This book is a guide to writing applications for Linux, Microsoft NT 4.0, Windows 2000, Windows 95, and Windows 98, using the Qt software toolkit from Trolltech AS. As any respectable programming guide should, it provides a working knowledge of the Qt software distribution and the objects, widgets, and conveniences that the Qt toolkit provides. In addition, it explores some aspects of Qt programming for enterprise application development that are not obvious from the toolkit vendor's documentation.

### AUDIENCE

This book is for C++ programmers and students that want to write effective application software using the Qt toolkit. The focus is primarily on platform-independent software, but some platform-specific topics are unavoidably covered.

### ASSUMPTIONS

This book is not a reference manual for the Qt objects and widgets—Trolltech has done an excellent job of providing reference documentation in HTML and Adobe Postscript formats. Their documentation is included with both the Qt-Free edition and the Qt-Professional edition licenses, and is available from the Troll web site. http://www/trolltech.com/

This book is written for both the experienced C++ programmer and the knowledgeable beginner. It is assumed the reader is familiar with standard C++ data types and how new data types are created. The reader should be familiar with the basic concepts of object-oriented (OO) design and implementation, particularly the concept of object inheritance. I have avoided using multiple inheritance in my examples for purposes of clarity, but the reader is encouraged to experiment.

While the title of this book implies a focus on Linux and Windows 2000, the actual scope is much larger. Most of the examples, as well as the code provided on the CD, will compile and function correctly on virtually any platform that Qt will.

If you are an experienced Microsoft developer, some of the coding style presented here may cause mild confusion. Please remember that with a few exceptions, the code presented in this book is intended for cross-platform use. As a result, you will seldom see references to DWORD, LPVOID, and LPSTR data types because they are undefined on platforms outside the Microsoft arena, and since most of the standard Unix data types are compatible with Windows development, they are used instead. The “correctness” of either is purely subjective.

Microsoft platform-specific examples require a Qt-Professional license. Licensing can be obtained directly from Trolltech, and is discussed in some detail in Chapter 1. While Qt software development can be done using the Borland compiler and tools, it is far more common for developers to use Microsoft Visual C++. As a result, it is assumed that the Windows developer has access to Microsoft Visual Studio 6.0 and VC98 (Visual C++).

It is possible, in theory, to compile and use Qt-Frame edition applications on a Windows platform, using the Cygnus Win32 implementation, the ming32 compiler distribution, the X11R6.3 development kit for Win32, and an appropriate X server. Since this is an incredibly esoteric environment, it isn’t addressed by any of the examples in this book. However, any of the Linux examples should work, assuming you succeed in compiling the Qt-Frame edition with the Cygnus compiler distribution—something I haven’t tried yet.

Linux development can be accomplished using the Qt-Frame edition. You will need a C++ compiler. This book assumes a generic gcc/g++ distribution (gcc-2.95 was used for the examples) from the Free Software Foundation (FSF), in the assumption that it is a reasonably low common denominator.

Many other platforms are supported out-of-the-box by Troll. I have had virtually no trouble using Qt on HP/UX or AIX.

### HOW THIS BOOK IS ORGANIZED

This book is organized into three parts. Part One is an introduction to the Qt toolkit. It provides some initial programming examples, and discusses some of the unique features that set Qt development apart from other toolkits. Part Two is a detailed discussion of toolkit components. Part Three discusses project-level considerations and debugging techniques.
