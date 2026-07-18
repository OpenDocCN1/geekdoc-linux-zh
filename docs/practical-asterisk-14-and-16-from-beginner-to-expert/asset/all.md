![](cover.jpeg)

![cover](cover.jpeg)

![cover-image](images/00001.jpg)

# Practical Asterisk 1.4 and 1.6

### Stefan Wintermeyer
Stephen Bosch

![image](images/00002.jpg)

Upper Saddle River, NJ • Boston • Indianapolis • San Francisco
New York • Toronto • Montreal • London • Munich • Paris • Madrid
Capetown • Sydney • Tokyo • Singapore • Mexico City

Many of the designations used by manufacturers and sellers to distinguish their products are claimed as trademarks. Where those designations appear in this book, and the publisher was aware of a trademark claim, the designations have been printed with initial capital letters or in all capitals.

The authors and publisher have taken care in the preparation of this book, but make no expressed or implied warranty of any kind and assume no responsibility for errors or omissions. No liability is assumed for incidental or consequential damages in connection with or arising out of the use of the information or programs contained herein.

The publisher offers excellent discounts on this book when ordered in quantity for bulk purchases or special sales, which may include electronic versions and/or custom covers and content particular to your business, training goals, marketing focus, and branding interests. For more information, please contact:

> U.S. Corporate and Government Sales
> (800) 382-3419
> [corpsales@pearsontechgroup.com](mailto:corpsales@pearsontechgroup.com)

For sales outside the United States, please contact:

> International Sales
> [international@pearson.com](mailto:international@pearson.com)

Visit us on the Web: [informit.com/aw](http://informit.com/aw)

**Editor-in-Chief**
Mark L. Taub

**Acquisitions Editor**
Debra Williams Cauley

**Development Editor**
Michael Thurston

**Technical Editors**
L.D. Paniak
John Kennedy

**Managing Editor**
John Fuller

**Full-Service Production Manager**
Julie B. Nahil

**Project Editor**
Kim Arney

**Copy Editor**
Keith Cline

**Indexer**
Jack Lewis

**Proofreader**
Linda Begley

**Cover Designer**
Chuti Prasertsith

**Compositor**
Kim Arney

*Library of Congress Cataloging-in-Publication Data*

Wintermeyer, Stefan.
   Practical Asterisk 1.4 and 1.6 : from beginner to expert / Stefan
Wintermeyer, Stephen Bosch.
         p.   cm.
   Includes index.
   ISBN 978-0-321-52566-6 (pbk. : alk. paper)   1\. Internet telephony.
2\. Asterisk (Computer file)   3\. Telephone—Private branch exchanges.
I. Bosch, Stephen.   II. Title.
   TK5105.8865.W56 2009
   621.385--dc22
                                                                       2009039861

> Pearson Education, Inc.
> Rights and Contracts Department
> 501 Boylston Street, Suite 900
> Boston, MA 02116
> Fax: (617) 671-3447

Copyright © 2010 by Pearson Education Deutschland GmbH

First published in the German language under the title *Asterisk 1.4 + 1.6* by Addison-Wesley, an imprint of Pearson Education Deutschland GmbH, München.

Permission is granted to copy, distribute, and/or modify this document under the terms of the GNU Free Documentation License, Version 1.3 or any later version published by the Free Software Foundation; with no Invariant Sections, no Front-Cover Texts, and no Back-Cover Texts. A copy of the license is included in the “GNU Free Documentation License” section.

ISBN-13: 978-0-321-52566-6
ISBN-10:        0-321-52566-3

Text printed in the United States on recycled paper at Edwards Brothers in Ann Arbor, Michigan.

First printing, December 2009

> *For grandaunt Helga.*

> —SW

> *For my father, who showed me how much fun tinkering could be.*

> —SB

## Contents

[Foreword](#Practical_As-sk_1.4_and_1.6_split_004.html_filepos97882)

[Preface](#Practical_As-sk_1.4_and_1.6_split_005.html_filepos101909)

[Acknowledgments](#Practical_As-sk_1.4_and_1.6_split_006.html_filepos106943)

[About the Authors](#Practical_As-sk_1.4_and_1.6_split_007.html_filepos110090)

[Chapter 1 How to Get the Most Out of This Book](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos110845)

> [1.1 What Is Asterisk?](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos111755)

> [1.2 Who Should Read This Book?](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos116003)

> [1.2.1 The Beginner](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos116458)

> [1.2.2 The Journeyman](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos120939)

> [1.2.3 The Expert](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos121781)

> [1.3 Updates and Versions of the Book](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos122564)

> [1.4 Reader Contributions and Feedback](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos123384)

> [1.5 Additional Resources](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos129022)

[Chapter 2 Installation and “Hello World”](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos131864)

> [2.1 Installing Asterisk on the Server](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos133419)

> [2.2 Calling “Hello World” from the CLI](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos135524)

> [2.2.1 Configuring Asterisk](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos135890)

> [2.2.2 Starting Asterisk and Calling “Hello World”](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos137962)

> [2.2.3 Stopping Asterisk](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos143912)

> [2.3 Calling “Hello World” with a SIP Phone](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos144380)

> [2.3.1 Configuring the SIP Phone and sip.conf](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos145500)

> [2.3.2 Starting Asterisk and the Phone](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos147840)

> [2.4 Building a Minimal Phone System with Two SIP Phones](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos152538)

> [2.4.1 Configuring Voicemail](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos154147)

> [2.5 Rights Administration with Contexts](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos157303)

> [2.5.1 The Originating Context](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos158159)

> [2.5.2 Call Destination: Contexts in extensions.conf](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos160524)

> [2.6 Calls to and from the Public Switched Telephone Network](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos161663)

> [2.6.1 Calling the PSTN](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos162071)

> [2.6.2 Taking Calls from the PSTN](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos166082)

[Chapter 3 Dialplan Fundamentals](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos167620)

> [3.1 Contexts](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos169355)

> [3.2 Extensions](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos172043)

> [3.2.1 Fundamental Applications](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos175385)

> [3.2.2 Priorities](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos179798)

> [3.3 Pattern Matching](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos183024)

> [3.3.1 Pattern Elements](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos184996)

> [3.3.2 Testing a Pattern Using dialplan show](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos190997)

> [3.3.3 Pattern-Matching Order](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos195484)

> [3.4 Include Statements](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos200760)

> [3.4.1 Order of Execution When Using Include Statements](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos201668)

> [3.4.2 Time-Conditional Include Statements](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos204611)

> [3.5 The ${EXTEN} Variable and the ${CALLERID(num)} Function](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos206433)

> [3.5.1 ${EXTEN}](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos207138)

> [3.5.2 ${CALLERID(num)}](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos208442)

[Chapter 4 Case Study: A Typical Business Telephone System](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos209393)

> [4.1 The Numbering Plan](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos214433)

> [4.2 Choosing the Infrastructure](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215219)

> [4.2.1 Network](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos217476)

> [4.2.2 Server Hardware](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos224075)

> [4.3 Base Configuration](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos230839)

> [4.3.1 A sip.conf for 100 Users](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos231223)

> [4.3.2 The Dialplan](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos233921)

> [4.4 What Next?](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos238436)

[Chapter 5 Dialplan Programming](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos239650)

> [5.1 Programming “How-To”](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos240584)

> [5.1.1 Program Structure](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos241361)

> [5.1.2 Using Set()](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos242450)

> [5.1.3 Labels and Goto()](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos245871)

> [5.1.4 While() Loops](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos247420)

> [5.1.5 GotoIf() Conditional](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos247946)

> [5.1.6 Gosub() Subroutines](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos248454)

> [5.2 Variables](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos249041)

> [5.2.1 Expanding Variables in an Extension](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos250185)

> [5.2.2 General Considerations](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos251431)

> [5.2.3 Defining Global Variables in extensions.conf](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos256167)

> [5.2.4 Defining Variables with Set()](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos256798)

> [5.2.5 Inheritance of Channel Variables](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos258138)

> [5.2.6 System Channel Variables](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos261023)

> [5.2.7 Manipulating Variables](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos266789)

> [5.3 Special Extensions](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos272152)

> [5.3.1 The h Extension](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos272453)

> [5.3.2 The i Extension](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos273604)

> [5.3.3 The o and a Extensions](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos274858)

> [5.3.4 The t and T Extensions](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos275466)

> [5.3.5 The s Extension](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos277885)

> [5.4 Macros](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos279134)

> [5.5 Deprecated Features](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos282475)

[Chapter 6 Asterisk Extension Language](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos283743)

> [6.1 CLI Commands for AEL](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos285374)

> [6.2 aelparse](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos287059)

> [6.3 Comparing extensions.conf with extensions.ael](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos289171)

> [6.3.1 Line Termination](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos290612)

> [6.3.2 Contexts, Extensions, and Priorities](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos290994)

> [6.3.3 Comments](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos293614)

> [6.3.4 Includes](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos294724)

> [6.3.5 Global Variables](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos295781)

> [6.3.6 Expressions and Variable Assignment](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos296180)

> [6.3.7 Labels, goto, and jump](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos298505)

> [6.3.8 Conditionals](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos301079)

> [6.3.9 Loops](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos307972)

> [6.3.10 Macros](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos311475)

> [6.3.11 Hints](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos312620)

> [6.3.12 Filtering by Caller ID](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos314272)

> [6.4 Choosing between extensions.ael and extensions.conf](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos315417)

[Chapter 7 Protocols](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos316793)

> [7.1 Network Protocols](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos317679)

> [7.1.1 Transmission Control Protocol](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos319937)

> [7.1.2 User Datagram Protocol](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos333187)

> [7.2 Channels](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos336446)

> [7.3 Peers, Users, and Friends](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos341626)

> [7.4 IAX Versus SIP](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos342685)

[Chapter 8 Making Connections](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos344732)

> [8.1 Codecs](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos345280)

> [8.1.1 What Does a Codec Do?](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos347708)

> [8.1.2 Performance](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos348679)

> [8.1.3 Configuring Codecs](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos350182)

> [8.1.4 Commonly Used Codecs](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos351159)

> [8.1.5 Bandwidth and Trunking](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos355371)

> [8.2 Integrated Services Digital Network](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos357160)

> [8.2.1 ISDN Basics](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos358046)

> [8.2.2 Choosing an ISDN Card](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos365559)

> [8.2.3 Media Gateways](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos376778)

> [8.3 Analog Telephony](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos379521)

> [8.3.1 Connecting Analog Devices](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos381671)

> [8.3.2 Analog Telephone Adapter](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos384600)

[Chapter 9 Voicemail](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos385837)

> [9.1 Example Implementations](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos386833)

> [9.1.1 An Example Home System](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos387262)

> [9.1.2 An Example Business System](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos389126)

> [9.3 Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos392671)

> [9.3.1 VoiceMail](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos393678)

> [9.3.2 VoiceMailMain](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos397688)

> [9.4 voicemail.conf](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos400807)

> [9.4.1 [general]](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos402038)

> [9.4.2 [zonemessages]](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos422498)

> [9.4.3 Defined Contents](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos425924)

> [9.4.4 Mailboxes](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos426614)

> [9.5 Dial-by-Name](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos437036)

> [9.6 Saving Passwords in voicemail.conf](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos440656)

[Chapter 10 Interactive Voice Response](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos442927)

> [10.1 A Simple IVR](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos445959)

> [10.1.1 Timeouts](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos448235)

> [10.1.2 Invalid Input (the i Extension)](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos450208)

> [10.1.3 Pauses](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos450891)

> [10.2 Multilevel IVR Systems](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos451610)

> [10.3 Text-to-Speech](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos454481)

> [10.3.1 Installing Cepstral TTS](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos456651)

[Chapter 11 The Asterisk Database](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos458949)

> [11.1 The Asterisk Database](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos459696)

> [11.1.1 Writing Values to the Database](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos463066)

> [11.1.2 Reading Values from the Database](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos463808)

> [11.1.3 Deleting Values from the Database](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos465444)

> [11.2 Database Access from the Command-Line Interface](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos467800)

> [11.2.1 Writing Values to the Database](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos468960)

> [11.2.2 Reading Values from the Database](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos469494)

> [11.2.3 Deleting Values from the Database](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos469997)

> [11.2.4 Displaying Database Contents](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos471545)

> [11.3 Database Access from the System Shell](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos472115)

> [11.4 Database Backup](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos473402)

> [11.5 Application Example: Call Forwarding](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos474217)

> [11.5.1 Simple Call Forwarding](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos474911)

> [11.5.2 Complex Call Forwarding](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos475720)

> [11.6 Application Example: Calling Card](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos476600)

[Chapter 12 Queues](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos478226)

> [12.1 Extension for Testing Hold Music](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos483425)

> [12.2 musiconhold.conf](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos483936)

> [12.3 queues.conf](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos493672)

> [12.3.1 Announcement Sound Files](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos516942)

> [12.4 agents.conf](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos520417)

> [12.5 Extensions](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos528234)

> [12.5.1 Sending Callers to the Queue](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos528783)

> [12.5.2 AgentLogin() and AgentCallbackLogin()](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos530403)

> [12.6 Log File](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos532625)

> [12.6.1 Importing the Queue Log into MySQL](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos541019)

[Chapter 13 Features](#Practical_As-sk_1.4_and_1.6_split_021.html_filepos543865)

> [13.1 Call Transfer](#Practical_As-sk_1.4_and_1.6_split_021.html_filepos544347)

> [13.1.1 Blind Transfer](#Practical_As-sk_1.4_and_1.6_split_021.html_filepos545408)

> [13.1.2 Attended Transfer](#Practical_As-sk_1.4_and_1.6_split_021.html_filepos546421)

> [13.2 Call Parking](#Practical_As-sk_1.4_and_1.6_split_021.html_filepos547528)

[Chapter 14 Conferencing](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos549523)

> [14.1 Installation and the Timing Device](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos550164)

> [14.2 Defining Conference Rooms](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos552027)

> [14.3 Access from the Dialplan](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos553446)

> [14.4 Announcing the Number of Conference Participants](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos554053)

[Chapter 15 External Control of Asterisk](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos554571)

> [15.1 asterisk -rx “command”](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos554962)

> [15.2 Call Files](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos555974)

> [15.2.1 Making a Call Automatically](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos557023)

> [15.2.2 Parameters](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos559604)

> [15.2.3 Hotel Wake-Up Call Example](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos563858)

> [15.3 The Asterisk Manager Interface](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos564418)

> [15.3.1 Creating an AMI User](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos565564)

> [15.3.2 Talking to the AMI](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos567322)

> [15.3.3 AMI Commands](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos572575)

> [15.3.4 Getting the Number of Voicemail Messages with Expect](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos574361)

> [15.3.5 StarAstAPI for PHP](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos576152)

> [15.3.6 Getting the Number of Mailbox Messages with PHP](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos580516)

> [15.4 The Asynchronous JavaScript Asterisk Manager](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos581624)

> [15.4.1 Getting the Number of Voicemail Messages with AJAM](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos584347)

> [15.4.2 AJAX and AJAM Considerations](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos586971)

[Chapter 16 Asterisk Gateway Interface](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos590399)

> [16.1 Data Streams](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos591217)

> [16.1.1 STDIN](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos591594)

> [16.1.2 STDOUT](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos595734)

> [16.1.3 STDERR](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos596191)

> [16.2 Examples in Various Programming Languages](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos596478)

> [16.2.1 Perl](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos597573)

> [16.2.2 PHP](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos604458)

> [16.2.3 Ruby and Adhearsion](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos606964)

> [16.2.4 Other Programming Languages](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos610739)

[Chapter 17 Fax Server](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos611815)

> [17.1 Installing IAXmodem](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos613076)

> [17.1.1 Configuring IAXmodem](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos615872)

> [17.1.2 Configuring faxgetty and Logging](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos621233)

> [17.2 Installing Hylafax](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos622864)

> [17.3 Receiving Faxes](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos626788)

> [17.4 Sending Faxes](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos630072)

> [17.5 Sending Received Faxes as E-Mail](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos632227)

[Chapter 18 Busy Lamp Field, Hints, Pickup](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos635562)

> [18.1 Controlling Indicators](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos637713)

> [18.1.1 sip.conf](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos638188)

> [18.1.2 Hints](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos640508)

> [18.2 Subscriptions](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos644806)

> [18.3 Configuring Telephones for BLF](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos646586)

> [18.3.1 BLF on the Aastra 480i](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos647900)

> [18.3.2 Polycom Soundpoint IP 501](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos654101)

> [18.4 Testing the Hints](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos658582)

> [18.5 Configuring Pickup](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos661867)

> [18.5.1 extensions.conf for Pickup](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos662618)

> [18.5.2 Configuring the Phones for Pickup](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos664688)

> [18.5.3 Configuring Group Pickup](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos668235)

> [18.6 Advanced BLF Indicators in Asterisk 1.6](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos670233)

[Appendix A Installation Instructions for Asterisk 1.4](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos679636)

> [A.1 LibPRI](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos683943)

> [A.2 DAHDI](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos684988)

> [A.3 Asterisk](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos687791)

[Appendix B Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692001)

> [B.1 AbsoluteTimeout()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos723417)

> [B.2 AddQueueMember()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos725177)

> [B.3 ADSIProg()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos728673)

> [B.4 AgentCallbackLogin()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos730987)

> [B.5 AgentLogin()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos733665)

> [B.6 AgentMonitorOutgoing()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos735682)

> [B.7 AGI()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos740308)

> [B.8 AlarmReceiver()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos745930)

> [B.9 AMD()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos748918)

> [B.10 Answer()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos757005)

> [B.11 AppendCDRUserField()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos759340)

> [B.12 Authenticate()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos761094)

> [B.13 Background()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos766468)

> [B.14 BackgroundDetect()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos770445)

> [B.15 Bridge()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos773353)

> [B.16 Busy()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos776235)

> [B.17 ChangeMonitor()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos778548)

> [B.18 ChanIsAvail()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos780643)

> [B.19 ChannelRedirect()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos786862)

> [B.20 ChanSpy()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos789899)

> [B.21 CheckGroup()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos798545)

> [B.22 ClearHash()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos800588)

> [B.23 Congestion()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos801971)

> [B.24 ContinueWhile()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos804436)

> [B.25 ControlPlayback()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos806433)

> [B.26 Curl()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos809748)

> [B.27 Cut()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos811384)

> [B.28 DAHDIBarge()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos813126)

> [B.29 DAHDIRAS()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos815292)

> [B.30 DAHDIScan()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos817463)

> [B.31 DAHDISendKeypadFacility()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos819636)

> [B.32 DateTime()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos821819)

> [B.33 DBdel()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos823608)

> [B.34 DBdeltree()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos826085)

> [B.35 DBget()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos827978)

> [B.36 DBput()](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos829785)

> [B.37 DeadAGI()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos831596)

> [B.38 Dial()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos835607)

> [B.39 Dictate()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos862493)

> [B.40 DigitTimeout()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos867232)

> [B.41 Directory()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos869332)

> [B.42 DISA()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos872538)

> [B.43 DumpChan()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos877102)

> [B.44 DUNDiLookup()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos879184)

> [B.45 EAGI()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos880861)

> [B.46 Echo()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos884750)

> [B.47 EndWhile()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos886821)

> [B.48 EnumLookup()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos888910)

> [B.49 Eval()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos890551)

> [B.50 Exec()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos892191)

> [B.51 ExecIf()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos895001)

> [B.52 ExecIfTime()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos897433)

> [B.53 ExitWhile()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos900109)

> [B.54 ExtenSpy()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos902022)

> [B.55 ExternalIVR()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos907966)

> [B.56 FastAGI()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos910187)

> [B.57 Festival()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos912594)

> [B.58 Flash()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos915867)

> [B.59 FollowMe()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos918971)

> [B.60 ForkCDR()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos920543)

> [B.61 GetCPEID()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos923308)

> [B.62 GetGroupCount()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos925448)

> [B.63 GetGroupMatchCount()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos927449)

> [B.64 Gosub()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos929505)

> [B.65 GosubIf()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos931860)

> [B.66 Goto()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos934438)

> [B.67 GotoIf()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos936925)

> [B.68 GotoIfTime()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos940203)

> [B.69 Hangup()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos944692)

> [B.70 HasNewVoicemail()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos946521)

> [B.71 HasVoicemail()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos949064)

> [B.72 IAX2Provision()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos951449)

> [B.73 ICES()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos953346)

> [B.74 ImportVar()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos955259)

> [B.75 Incomplete()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos957372)

> [B.76 JabberSend()](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos959134)

> [B.77 JabberStatus()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos961377)

> [B.78 KeepAlive()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos963807)

> [B.79 Log()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos965179)

> [B.80 LookupBlacklist()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos967831)

> [B.81 LookupCIDName()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos971058)

> [B.82 Macro()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos973726)

> [B.83 MacroExclusive()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos977396)

> [B.84 MacroExit()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos981309)

> [B.85 MacroIf()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos982885)

> [B.86 mailboxExists()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos984802)

> [B.87 Math()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos987134)

> [B.88 MD5()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos988884)

> [B.89 MD5Check()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos990738)

> [B.90 MeetMe()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos992604)

> [B.91 MeetMeAdmin()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1010250)

> [B.92 MeetMeChannelAdmin()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1014763)

> [B.93 MeetMeCount()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1017410)

> [B.94 Milliwatt()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1019843)

> [B.95 MinivmAccMess()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1021838)

> [B.96 MinivmDelete()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1025239)

> [B.97 MinivmGreet()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1027057)

> [B.98 MinivmNotify()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1030288)

> [B.99 MinivmRecord()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1032190)

> [B.100 MixMonitor()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1034188)

> [B.101 Monitor()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1038634)

> [B.102 Morsecode()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1047301)

> [B.103 MP3Player()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1048981)

> [B.104 MSet()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1051929)

> [B.105 MusicOnHold()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1054409)

> [B.106 NBScat()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1057198)

> [B.107 NoCDR()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1059127)

> [B.108 NoOp()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1060854)

> [B.109 ODBCFinish()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1063679)

> [B.110 Page()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1065131)

> [B.111 Park()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1068573)

> [B.112 ParkAndAnnounce()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1070924)

> [B.113 ParkedCall()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1074434)

> [B.114 PauseMonitor()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1076675)

> [B.115 PauseQueueMember()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1078636)

> [B.116 Pickup()](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1081388)

> [B.117 PickupChan()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1083480)

> [B.118 Playback()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1085123)

> [B.119 Playtones()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1087914)

> [B.120 PrivacyManager()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1090691)

> [B.121 Proceeding()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1094835)

> [B.122 Progress()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1096214)

> [B.123 Queue()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1098312)

> [B.124 QueueLog()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1105643)

> [B.125 RaiseException()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1107783)

> [B.126 Random()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1109659)

> [B.127 Read()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1112162)

> [B.128 ReadExten()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1115720)

> [B.129 ReadFile()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1117272)

> [B.130 RealTime()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1118970)

> [B.131 RealTimeUpdate()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1122661)

> [B.132 ReceiveFAX()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1124998)

> [B.133 Record()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1127051)

> [B.134 RemoveQueueMember()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1133610)

> [B.135 ResetCDR()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1136139)

> [B.136 ResponseTimeout()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1138171)

> [B.137 RetryDial()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1140256)

> [B.138 Return()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1143255)

> [B.139 Ringing()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1145418)

> [B.140 SayAlpha()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1147650)

> [B.141 SayDigits()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1149636)

> [B.142 SayNumber()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1151633)

> [B.143 SayPhonetic()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1157877)

> [B.144 SayUnixTime()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1159951)

> [B.145 SendDTMF()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1163154)

> [B.146 SendFAX()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1165615)

> [B.147 SendImage()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1167528)

> [B.148 SendText()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1169990)

> [B.149 SendURL()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1172603)

> [B.150 Set()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1175585)

> [B.151 SetAccount()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1179650)

> [B.152 SetAMAFlags()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1181480)

> [B.153 SetCallerID()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1184084)

> [B.154 SetCallerPres()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1186094)

> [B.155 SetCDRUserField()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1190820)

> [B.156 SetCIDName()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1193038)

> [B.157 SetCIDNum()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1194996)

> [B.158 SetGlobalVar()](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1196987)

> [B.159 SetGroup()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1200419)

> [B.160 SetLanguage()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1202410)

> [B.161 SetMusicOnHold()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1204224)

> [B.162 SetRDNIS()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1206180)

> [B.163 SetTransferCapability()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1207987)

> [B.164 SetVar()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1211255)

> [B.165 SIPAddHeader()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1212935)

> [B.166 SIPdtmfMode()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1215242)

> [B.167 SIPGetHeader()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1217665)

> [B.168 SMS()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1219369)

> [B.169 SoftHangup()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1226884)

> [B.170 Sort()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1228893)

> [B.171 StackPop()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1230605)

> [B.172 StartMusicOnHold()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1232369)

> [B.173 StopMixMonitor()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1234255)

> [B.174 StopMonitor()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1235968)

> [B.175 StopMusicOnHold()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1237867)

> [B.176 StopPlaytones()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1239641)

> [B.177 System()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1241478)

> [B.178 Transfer()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1245020)

> [B.179 TryExec()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1247614)

> [B.180 TrySystem()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1250783)

> [B.181 TXTCIDName()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1253205)

> [B.182 UnpauseMonitor()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1255085)

> [B.183 UnpauseQueueMember()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1256878)

> [B.184 UserEvent()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1259006)

> [B.185 Verbose()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1261515)

> [B.186 VMAuthenticate()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1264134)

> [B.187 VoiceMail()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1266771)

> [B.188 VoiceMailMain()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1271374)

> [B.189 Wait()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1274620)

> [B.190 WaitExten()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1276396)

> [B.191 WaitForNoise()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1278776)

> [B.192 WaitForRing()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1280776)

> [B.193 WaitForSilence()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1282679)

> [B.194 WaitMusicOnHold()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1284851)

> [B.195 WaitUntil()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1286921)

> [B.196 While()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1289713)

> [B.197 Zapateller()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1292043)

> [B.198 ZapBarge()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1294818)

> [B.199 ZapRAS()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1297160)

> [B.200 ZapScan()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1299987)

> [B.201 ZapSendKeypadFacility()](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1302126)

[Appendix C Dialplan Functions](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304221)

> [C.1 AGENT()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1309031)

> [C.2 ARRAY()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1312530)

> [C.3 BASE64_DECODE()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1315162)

> [C.4 BASE64_ENCODE()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1316584)

> [C.5 BLACKLIST](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1317987)

> [C.6 CALLERID()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1320096)

> [C.7 CDR()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1325466)

> [C.8 CHANNEL()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1333504)

> [C.9 CHECKSIPDOMAIN()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1341375)

> [C.10 CURL()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1342963)

> [C.11 CUT()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1344656)

> [C.12 DB()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1347618)

> [C.13 DB_DELETE()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1349551)

> [C.14 DB_EXISTS()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1351842)

> [C.15 DUNDILOOKUP()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1354310)

> [C.16 ENUMLOOKUP()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1356355)

> [C.17 ENV()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1359269)

> [C.18 EVAL()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1360880)

> [C.19 EXISTS()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1362686)

> [C.20 FIELDQTY()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1364091)

> [C.21 FILTER()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1365927)

> [C.22 GLOBAL()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1367514)

> [C.23 GROUP()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1369630)

> [C.24 GROUP_COUNT()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1371357)

> [C.25 GROUP_LIST()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1373176)

> [C.26 GROUP_MATCH_COUNT()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1374893)

> [C.27 IAXPEER()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1376667)

> [C.28 IF()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1381519)

> [C.29 IFTIME()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1383634)

> [C.30 ISNULL()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1386849)

> [C.31 KEYPADHASH()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1388239)

> [C.32 LANGUAGE()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1389795)

> [C.33 LEN()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1392328)

> [C.34 MATH()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1393700)

> [C.35 MD5()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1396053)

> [C.36 MUSICCLASS()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1397468)

> [C.37 ODBC_SQL()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1399399)

> [C.38 ODBC_USER_DATABASE()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1400854)

> [C.39 QUEUEAGENTCOUNT()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1401869)

> [C.40 QUEUE_MEMBER_COUNT()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1403716)

> [C.41 QUEUE_MEMBER_LIST()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1405599)

> [C.42 QUOTE()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1407089)

> [C.43 RAND()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1408531)

> [C.44 REGEX()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1410886)

> [C.45 SET()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1413100)

> [C.46 SHA1()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1414874)

> [C.47 SIPCHANINFO()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1416324)

> [C.48 SIPPEER()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1419609)

> [C.49 SIP_HEADER()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1425609)

> [C.50 SORT()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1427629)

> [C.51 STAT()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1429137)

> [C.52 STRFTIME()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1433424)

> [C.53 STRPTIME()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1435641)

> [C.54 TIMEOUT()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1437375)

> [C.55 TXTCIDNAME()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1440348)

> [C.56 URIDECODE()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1442124)

> [C.57 URIENCODE()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1443724)

> [C.58 VMCOUNT()](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1445448)

[Appendix D AGI Command Summary](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1447314)

> [D.1 ANSWER](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1448524)

> [D.2 ASYNCAGI BREAK](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1449656)

> [D.3 CHANNEL STATUS](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1450512)

> [D.4 CONTROL STREAM FILE](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1451639)

> [D.5 DATABASE DEL](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1452784)

> [D.6 DATABASE DELTREE](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1453922)

> [D.7 DATABASE GET](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1455064)

> [D.8 DATABASE PUT](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1456202)

> [D.9 EXEC](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1457340)

> [D.10 GET DATA](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1458989)

> [D.11 GET FULL VARIABLE](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1460637)

> [D.12 GET OPTION](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1461781)

> [D.13 GET VARIABLE](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1462918)

> [D.14 GOSUB](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1464512)

> [D.15 HANGUP](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1465373)

> [D.16 NOOP](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1466506)

> [D.17 RECEIVE CHAR](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1467814)

> [D.18 RECEIVE TEXT](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1468953)

> [D.19 RECORD FILE](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1470092)

> [D.20 SAY ALPHA](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1471230)

> [D.21 SAY DATE](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1472366)

> [D.22 SAY DATETIME](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1473501)

> [D.23 SAY DIGITS](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1475675)

> [D.24 SAY NUMBER](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1476812)

> [D.25 SAY PHONETIC](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1478074)

> [D.26 SAY TIME](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1479359)

> [D.27 SEND IMAGE](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1480494)

> [D.28 SEND TEXT](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1481631)

> [D.29 SET AUTOHANGUP](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1482767)

> [D.30 SET CALLERID](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1483908)

> [D.31 SET CONTEXT](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1485047)

> [D.32 SET EXTENSION](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1486665)

> [D.33 SET MUSIC](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1488291)

> [D.34 SET PRIORITY](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1489427)

> [D.35 SET VARIABLE](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1491012)

> [D.36 STREAM FILE](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1492157)

> [D.37 TDD MODE](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1493759)

> [D.38 VERBOSE](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1495115)

> [D.39 WAIT FOR DIGIT](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1496249)

[Appendix E AMI Command Summary](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1497379)

> [E.1 AbsoluteTimeout](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1497822)

> [E.2 AgentCallbackLogin](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1498963)

> [E.3 AgentLogoff](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1500029)

> [E.4 Agents](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1501063)

> [E.5 AGI](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1502092)

> [E.6 Atxfer](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1502950)

> [E.7 Bridge](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1503811)

> [E.8 Challenge](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1504672)

> [E.9 ChangeMonitor](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1505523)

> [E.10 Command](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1506559)

> [E.11 CoreSettings](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1507590)

> [E.12 CoreShowChannels](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1508458)

> [E.13 CoreStatus](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1509330)

> [E.14 CreateConfig](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1510196)

> [E.15 DAHDIDialOffhook](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1511064)

> [E.16 DAHDIDNDoff](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1512258)

> [E.17 DAHDIDNDon](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1513432)

> [E.18 DAHDIHangup](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1514602)

> [E.19 DAHDIRestart](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1515750)

> [E.20 DAHDIShowChannels](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1516927)

> [E.21 DAHDITransfer](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1518099)

> [E.22 DBDel](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1519255)

> [E.23 DBDelTree](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1520103)

> [E.24 DBGet](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1520955)

> [E.25 DBPut](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1522061)

> [E.26 Events](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1523077)

> [E.27 ExtensionState](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1524107)

> [E.28 GetConfig](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1525248)

> [E.29 GetConfigJSON](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1526409)

> [E.30 Getvar](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1527278)

> [E.31 Hangup](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1528411)

> [E.32 IAXnetstats](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1529544)

> [E.33 IAXpeerlist](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1530643)

> [E.34 IAXpeers](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1531497)

> [E.35 JabberSend](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1532606)

> [E.36 ListCategories](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1533665)

> [E.37 ListCommands](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1534498)

> [E.38 Login](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1535534)

> [E.39 Logoff](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1536382)

> [E.40 MailboxCount](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1537399)

> [E.41 MailboxStatus](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1538538)

> [E.42 MeetmeList](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1539678)

> [E.43 MeetmeMute](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1540544)

> [E.44 MeetmeUnmute](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1541590)

> [E.45 ModuleCheck](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1542638)

> [E.46 ModuleLoad](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1543505)

> [E.47 Monitor](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1544371)

> [E.48 Originate](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1545402)

> [E.49 Park](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1546538)

> [E.50 ParkedCalls](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1547591)

> [E.51 PauseMonitor](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1548613)

> [E.52 Ping](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1549674)

> [E.53 PlayDTMF](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1550805)

> [E.54 QueueAdd](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1551862)

> [E.55 QueueLog](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1552881)

> [E.56 QueuePause](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1553732)

> [E.57 QueuePenalty](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1554766)

> [E.58 QueueRemove](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1555634)

> [E.59 QueueRule](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1556656)

> [E.60 Queues](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1557508)

> [E.61 QueueStatus](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1558525)

> [E.62 QueueSummary](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1559547)

> [E.63 Redirect](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1560402)

> [E.64 Reload](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1561434)

> [E.65 SendText](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1562296)

> [E.66 SetCDRUserField](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1563160)

> [E.67 Setvar](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1564198)

> [E.68 ShowDialPlan](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1565228)

> [E.69 SIPnotify](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1566096)

> [E.70 SIPpeers](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1566961)

> [E.71 SIPqualifypeer](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1568096)

> [E.72 SIPshowpeer](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1568966)

> [E.73 SIPshowregistry](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1570207)

> [E.74 Status](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1571078)

> [E.75 StopMonitor](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1572161)

> [E.76 UnpauseMonitor](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1573196)

> [E.77 UpdateConfig](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1574259)

> [E.78 UserEvent](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1575423)

> [E.79 VoicemailUsersList](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1576481)

> [E.80 WaitEvent](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1577355)

> [E.81 ZapDialOffhook](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1578516)

> [E.82 ZapDNDoff](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1579676)

> [E.83 ZapDNDon](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1580826)

> [E.84 ZapHangup](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1581974)

> [E.85 ZapRestart](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1583098)

> [E.86 ZapShowChannels](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1584275)

> [E.87 ZapTransfer](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1585411)

[Appendix F Configuration Templates](#Practical_As-sk_1.4_and_1.6_split_036.html_filepos1586528)

> [F.1 Creating Templates](#Practical_As-sk_1.4_and_1.6_split_036.html_filepos1588122)

> [F.2 Using Templates](#Practical_As-sk_1.4_and_1.6_split_036.html_filepos1588771)

[Appendix G Upgrading from 1.4 to 1.6](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1590042)

> [G.1 AEL](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1590497)

> [G.2 Core](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1591974)

> [G.3 Voicemail](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1596326)

> [G.4 Dialplan Applications and Functions](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1597923)

> [G.5 CDR](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1604502)

> [G.6 Audio Formats](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1606310)

> [G.7 Channel Drivers](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607885)

> [G.8 Configuration](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1612594)

> [G.9 Asterisk Manager Interface](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1613644)

[Appendix H From Zaptel to DAHDI](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1615270)

> [H.1 DAHDI](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1616228)

> [H.2 Interview with Kevin P. Fleming](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1620612)

[Appendix I IAX vs. SIP](#Practical_As-sk_1.4_and_1.6_split_039.html_filepos1629095)

[Appendix J GNU Free Documentation License](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1630328)

> [0 PREAMBLE](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1630933)

> [1 APPLICABILITY AND DEFINITIONS](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1632401)

> [2 VERBATIM COPYING](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1638223)

> [3 COPYING IN QUANTITY](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1639200)

> [4 MODIFICATIONS](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1641540)

> [5 COMBINING DOCUMENTS](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1648084)

> [6 COLLECTIONS OF DOCUMENTS](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1649706)

> [7 AGGREGATION WITH INDEPENDENT WORKS](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1650579)

> [8 TRANSLATION](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1651812)

> [9 TERMINATION](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1653147)

> [10 FUTURE REVISIONS OF THIS LICENSE](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1654798)

> [11 RELICENSING](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1656160)

[Index](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1657968)

## Foreword

You are reading the English version of my second Asterisk book. I wrote the book in German, and Stephen Bosch translated it into English and adapted the content for a North American reader. Nonetheless, this book was the result of collaboration. The first version was published under the GNU Free Documentation License (GFDL), and more than 100 people contributed by sending error reports or by writing new sections. A special thanks goes to my colleague, Philipp Kempgen, who wrote many sections for this new edition. You can find the German edition at [www.das-asterisk-buch.de](http://www.das-asterisk-buch.de) and the English version at [www.the-asterisk-book.com](http://www.the-asterisk-book.com).

I encourage you to take a closer look at the current online edition, especially when it comes to hardware and driver-related information.

The past few years have been active ones in the VoIP world. My work with Asterisk has brought me to many new places, such as Huntsville, Alabama (home of Digium, the developer of Asterisk); Toronto, Canada (home of Sangoma, a manufacturer of telephony interface hardware); and Bucharest, Romania (home of the Yate project, an open source telephony engine). I learned much about Asterisk, but also a lot about Yate ([http://yate.null.ro](http://yate.null.ro)) and FreeSwitch ([www.freeswitch.org](http://www.freeswitch.org)), both interesting open source VoIP alternatives.

Asterisk has come a long way since I first used it. I didn’t use that very first installation for very long; I didn’t understand the concept, and documentation was typical for open source software (i.e., “read the source code”). The same may be said of my first experience with Linux. Today, I wouldn’t dream of being without either of them.

Asterisk has changed my way of thinking about PBXes. In the future, everyone will be more likely to think of a PBX as software rather than hardware.

The transition from the old, hardware-oriented way of doing things to the new software-oriented way is not without its challenges. In my daily work as an Asterisk consultant, I often see conflict between the former data guys and the former telephony guys. I hope to bring their respective worlds closer together with this book.

I welcome your feedback, praise, and criticism. Please send it to me at [stefan.wintermeyer@amooma.de](mailto:stefan.wintermeyer@amooma.de)

—*Stefan Wintermeyer*

It has been a special privilege to work with Stefan on the translation of this book into English. Although Stefan speaks English quite well, he knew that a competent English version would need a dedicated translator. To be entrusted with this task has been an honor. I was also charged with some of the adaptations and changes for the English edition, including the chapter on ISDN.

A technical translation is a special kind of beast. Details are critical, and there isn’t much room for nuance, so I hope that the book you have in your hands proves to be both readable and helpful. Like Stefan, I welcome your feedback. Please send it to me at [sbosch@vodacomm.ca](mailto:sbosch@vodacomm.ca).

—*Stephen Bosch*

## Preface

Perhaps it was folly to strive to make a book for everyone, but only audacious goals pave the path to excellence. This book does indeed try to be useful for both the new user and the expert.

[Chapter 1](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos110873) provides guideposts for the beginner, journeyman, and expert. [Chapter 2](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos131892) offers detailed instructions for the configuration of a basic system, with pointers to the installation instructions in the appendix. [Chapter 3](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos167648) is an introduction to the dialplan, truly the heart of Asterisk, which leads into [Chapter 4](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos209421), a practical business case example that lays out what is involved in designing a system for actual deployment.

The next chapters go into more depth for the more experienced Asterisk user. [Chapter 5](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos239678) covers the use of dialplan applications and functions for building voice applications. [Chapter 6](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos283771) looks at the new Asterisk Extensions Language, which introduces familiar programming language format to the dialplan. With it, you can build concise, readable, and maintainable dialplans. Asterisk uses a variety of network and IP telephony protocols in its work, which we review in [Chapter 7](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos316821). [Chapter 8](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos344760) looks at the audio codecs and wire transports Asterisk uses to connect to devices and telephone networks, including ISDN, and takes a brief look at the associated hardware.

Then we look at the feature set of Asterisk. Asterisk provides a fully functional voicemail system. Learn how to configure and use it in [Chapter 9](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos385865). [Chapter 10](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos442955) shows you how to build interactive voice response (IVR) systems using Asterisk. Useful applications need a database, and Asterisk provides one, the Asterisk database, covered in [Chapter 11](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos458977). Call queues, arguably the backbone of any call center, are covered in [Chapter 12](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos478254).

The very brief [Chapter 13](#Practical_As-sk_1.4_and_1.6_split_021.html_filepos543893) looks at two basic but common business telephone features: call transfer and pickup. Teleconferencing can be a powerful collaboration tool, and Asterisk has built-in conferencing functions, which are addressed in [Chapter 14](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos549551).

There are many ways to have Asterisk interact with external programs. [Chapter 15](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos554599) shows you how to control Asterisk from external applications, scripts, or the system shell with shell commands, call files, or the Asterisk Manager Interface. [Chapter 16](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos590427) introduces the Asterisk Gateway Interface, Asterisk’s principal method for interacting with external applications.

You can extend Asterisk for faxing with IAXmodem and Hylafax. Learn how to do this in [Chapter 17](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos611843).

Finally, [Chapter 18](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos635590) addresses a frequent request: setting up busy lamp field (extension monitoring) and hints for SIP telephones. We look at Aastra and Polycom examples.

The appendixes in this book are extensive and are meant to be used frequently. [Appendix A](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos679664) contains very detailed instructions for installing Asterisk on Debian Etch. [Appendices B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), [C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), [D](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1447342), and [E](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1497407) have command and function summaries for the dialplan and the AGI and AMI interfaces. [Appendix F](#Practical_As-sk_1.4_and_1.6_split_036.html_filepos1586556) provides examples for using dialplan templates.

Although Asterisk 1.4 is now the production-ready version, 1.6 is in development and can be used. [Appendix G](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1590070) tells you what you need to know to migrate successfully.

[Appendix H](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1615298) covers the renaming of Zaptel to DAHDI. This has implications for operation, which are addressed here.

Which should you choose, IAX or SIP? It’s a matter of debate. We provide some input in [Appendix I](#Practical_As-sk_1.4_and_1.6_split_039.html_filepos1629123).

You can read sequentially or follow your interests. Just remember that some of the examples build on previous examples.

## Acknowledgments

The first edition of this book was published in 2006 in Germany. In the interim, we received lots of useful feedback from the Asterisk community. We want to say a big thank you to everybody who helped us.

In the first edition, we acknowledged everybody by name, but we’ve decided not to do that this time because the e-mail addresses were harvested by spammers and many of the contributors have expressly asked to remain anonymous.

Nevertheless, we want to thank you sincerely for all your feedback and effort! Without your help, the book could not have become as good as it has.

### Acknowledgments from Stefan Wintermeyer

First and foremost, I want to thank my editor, Boris Karnikowski. Without his patience, not even the first edition would have seen the light of day. The second edition was incrementally delayed 12 months. I am also thankful that he agreed to allow the book to be published under the GNU Free Documentation License. There are few publishers and editors who have the courage to take such a step. Thanks, Boris!

I also want to thank my colleagues at AMOOMA, Peter Kozak and Sören Sprenger. Special thanks go to Philipp Kempgen. The depth and breadth of this book owes itself to your efforts.

Friederike Daenecke’s editing work was miraculous. She went through the entire manuscript in a little under three weeks.

Kevin Fleming of Digium provided very prompt and invaluable technical assistance.

The staff at Sangoma were also very helpful. In particular, thanks go to Konrad Hammel and Doug Vilim.

Special thanks go to my wife. Without her support, I wouldn’t be able to keep my head above water on these many projects.

### Acknowledgments from Philipp Kempgen

Thanks to my family, Jeannie, Coco, Kanji, and all those who get the short end of the stick a little too often.

### Acknowledgments from Stephen Bosch

Thanks to Debra Williams Cauley for your humane and generous spirit, your (apparently inexhaustible!) patience, and your persistence. You are a real professional. To you and everyone else at Pearson: I am grateful.

## About the Authors

**Stefan Wintermeyer** is the founder and director of AMOOMA GmbH, a leading provider of Asterisk telephony solutions in Europe. He was Germany’s first Digium-Certified Asterisk Professional and continues to share his knowledge in conferences, seminars, and workshops.

**Stephen Bosch** is an Asterisk consultant and writer who divides his time between Aschaffenburg, Germany, and Calgary, Alberta, Canada. When not making telephone calls with Asterisk, he sails.

## 1\. How to Get the Most Out of This Book

First, thank you for buying this book. It’s only through the interest of readers like you that a project such as this is possible.

We wrote this book because Asterisk doesn’t come with an instruction manual. Many of the resources recommended by the Asterisk community are in the form of wikis and websites, which are inconsistently updated and often contain incorrect information. We want this book to serve as that missing manual for Asterisk. In other words, we sought to create the kind of book we were looking for: a readable text that can be read in chapter order or used as a handbook.

### 1.1 What Is Asterisk?

Asterisk is a telephone system, but different. It’s not hardware. It’s software that you can download via the Internet. The only thing you need to get started is an ordinary PC, the Asterisk software, this book, and interest in doing so.

Asterisk works with a variety of telephony technologies, including analog, ISDN, and VoIP. With an Asterisk system, an employee can work at home with an IP phone and make calls in the office system as though she were in the office. The possibilities are limitless, both to extend the functionality of your system and to save money. Telephony remains somewhat complex, however, and a move to Asterisk is not without its challenges. Therefore, you need to familiarize yourself with both the general technology and with Asterisk itself.

Let’s explore the difference between Asterisk and a conventional telephone system by way of an analogy from childhood.

Most of us grew up with toys of two basic types. With the first type, everything came “ready to go” (for example, teddy bears or Hot Wheels cars). The second type offered some room for variation and creativity (for example, Lego blocks or Lincoln Logs). With the “ready to go” toys, the fun was right there when you opened the package, but you were limited to play as conceived by the toy company. With the blocks/logs, you didn’t get a finished toy. To get one, you had to come up with a design and then build it, but you could build anything you wanted, within the limitations of the pieces available.

That, in a nutshell, is exactly how it is with Asterisk. It is delivered in pieces. Think of a design, and suddenly anything is possible. Best of all, you can improve the resulting “toy” any time with new pieces.

Both Asterisk and conventional telephone systems have their pros and cons.

*The main advantages of a conventional telephone system include the following:*

> • Unpack and you’re done! You can start making calls almost immediately.

> • Limited instructions are required.

*The main disadvantages of a conventional telephone system include the following*:

> • Expansion is usually very expensive, and not all functions are supported or even available.

> • It’s a black box. You have no way to find out what’s happening inside, which can be vital when troubleshooting.

*The main advantages of a software-based Asterisk system include the following:*

> • You can build new solutions to problems any time. All you need is an appropriate design.

> • You can combine components to create new systems and solutions.

*The main disadvantages of Asterisk include the following:*

> • You start with just a bunch of components. Building them into a system requires some patience.

> • You need some skill. Success doesn’t come quickly.

### 1.2 Who Should Read This Book?

Not everybody has to start at square one, nor does every interested person want to become an Asterisk professional. This book takes that into account and presents material that will prove to be a valuable reference for beginners, novices, and experts alike.

#### 1.2.1 The Beginner

Absolute beginners should read this book in chapter order because the chapters build on each other. At a minimum, read [Chapter 2](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos131892), “[Installation and ‘Hello World,’](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos131892)” and [5](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos239678), “[Dialplan Fundamentals](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos239678),” and you’ll be able to put together increasingly complex telephone systems.

Beginners often have questions about what equipment is best to buy and which service to order, so we’ve provided this brief FAQ for those who need some guidance.

> **Q:** *How do I choose a VoIP provider? What do I need to watch out for?*

> **A:** When starting out, choose a SIP provider that offers free accounts so that you can gather some experience. Which provider you choose for the long term can depend on many factors. Here are just a few things to consider:

> • Does the provider offer only SIP or also IAX? Do you need IAX?

> • How good is the support? For VoIP, good support can be critical.

> • How are services priced? This is not always obvious.

> **Q:** *Which digital interface card should I use?*

> **A:** Get comfortable using only SIP trunks and extensions to start. Once you understand the dialplan and contexts, you can proceed to [Chapter 8](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos344760), “[Making Connections](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos344760),” where you will find tips for choosing the right digital card for your application.

> **Q:** *Which phones are standard, and what do they cost?*

> **A:** There aren’t really “standard” phones. You have several options:

> • A SIP telephone. (This is the simplest option.)

> • An analog telephone using an ATA (analog telephone adapter) connected to the network.

> • An analog telephone using an FXS port on an analog interface card.

> • A digital telephone (such as a Nortel Meridian phone) using a suitable digital telephone adapter connected to the network.

> • An ISDN phone using a port on a T1 card. These phones are sold almost exclusively in Europe where ISDN termination is much more common. Before the arrival of VoIP, they were the most feature-filled devices; currently, however, they are functionally indistinguishable from VoIP phones and can cost three times as much. If you have the option, it’s best to go with a SIP telephone.

> • Exotic constructs. You can, for example, connect a channel bank to a T1 interface card and attach analog phones to the channel bank. Such constructions generally prove useful in retrofit applications. If you’re starting from scratch, keep it simple.

As for pricing, this changes constantly. There are countless suppliers. Inquire frequently and compare. Quality VoIP hardware is becoming more and more affordable.

#### 1.2.2 The Journeyman

It is impossible to guess what an intermediate Asterisk user knows and doesn’t know. Even if you have good command of a subject, there are always aspects to it that might be new to you. If you have some practical experience, you may want to skip [Chapter 2](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos131892) or just skim it. Personally, though, we recommend that you read it anyway. After all, reviewing the fundamentals almost always pays off.

Leaf through all the other chapters afterward. When writing this book, we focused on practical examples. Just reading the sample configurations may give you some new ideas.

#### 1.2.3 The Expert

You can skip [Chapter 2](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos131892) and just go on a discovery tour of the book. You’ll find numerous practical examples you can integrate immediately into your own practice; the examples may even give you a few ideas about how to expand your system.

Beyond that, we hope this book will be a valuable reference. All the important application and function parameters are included and explained, usually with working examples. We placed particular emphasis on comparisons between the different Asterisk versions (1.2 to 1.6).

### 1.3 Updates and Versions of the Book

This book is being developed just as a typical open source project would be. What you are holding in your hands is a printed version of the stable branch. You can access updates and errata at [www.the-asterisk-book.com](http://www.the-asterisk-book.com).

You’ll find the current SVN version there. That’ll be the next edition, but for now it is on the bleeding edge. The procedures contained there may not have been tested and may not even be recommended. Therefore, a warning: Use that material only if you know what you’re doing.

### 1.4 Reader Contributions and Feedback

We intend this book to be a living text, and so have released it under the GNU Free Documentation License (see [Appendix J](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1630356), “[GNU Free Documentation License](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1630356)”). You can find the most current version of the book at [www.the-asterisk-book.com](http://www.the-asterisk-book.com).

If you have suggestions for improvements, include them in an e-mail to [stefan.wintermeyer@amooma.de](mailto:stefan.wintermeyer@amooma.de). If you have more comprehensive improvements to contribute, attach them in ASCII text format or directly in DocBook format to your e-mail.

Thanks in advance for your interest in this project!

This book will never be perfect or ever really “finished.” The subject is too complex and changes too rapidly. Remember that you can always find the most current (and most bleeding-edge) version of the book at [www.the-asterisk-book.com](http://www.the-asterisk-book.com). Accordingly, this FAQ is intended for the web version of the book. If you find an error in this book, please check the website first to see whether the error has already been fixed.

> **Q:** *I tried something from the book, but it didn’t work as described. Should I report this?*

> **A:** Yes, absolutely! When reporting, provide the URL and any relevant error messages.

> **Q:** *How can I report an error?*

> **A:** The easiest way is via e-mail to the author, Stefan Wintermeyer ([stefan.wintermeyer@amooma.de](mailto:stefan.wintermeyer@amooma.de)).

> **Q:** *In what format is the book written?*

> **A:** The source for the book is written in DocBook format. You can learn more about DocBook at [www.docbook.org](http://www.docbook.org).

> **Q:** *Why isn’t there a wiki, where anybody can make changes?*

> **A:** First, because the book is printed, a print deadline has to be set. A constantly changing text makes it impossible for the editors to keep up and maintain consistency in the resulting printed material. Second, there are already numerous Asterisk wikis on the Internet. Their chief advantage (quick and easy changes) also leads to their chief disadvantage: plenty of painfully outdated and outright incorrect information. Using DocBook and managing changes means we have a more structured, more readable text that is as accurate as human beings can make it. If the entire text were in a wiki, it would make export for printing very difficult.

> **Q:** *What editor do I need to write in DocBook format?*

> **A:** That’s almost a “religious” question. Some people like emacs, others like vi. The author and contributors use XMLmind XML Editor most of the time. You can obtain it from [www.xmlmind.com/xmleditor](http://www.xmlmind.com/xmleditor).

> **Q:** *Can I obtain the original DocBook files?*

> **A:** Yes. If you have extensive changes to make, you are welcome to work on the original files. Write an e-mail to the author, Stefan Wintermeyer ([stefan.wintermeyer@amooma.de](mailto:stefan.wintermeyer@amooma.de)).

> **Q:** *You didn’t cover XYZ! Unbelievable. It’s so important! What were you thinking?*

> **A:** Contact the author and briefly describe the subject. (If you’re willing to write a chapter and make it available under the GNU FDL, let Stefan know. He’ll send you a sample DocBook chapter.)

> **Q:** *How is the website generated?*

> **A:** A script pulls the DocBook sources from the SVN and uses them to generate the HTML pages.

### 1.5 Additional Resources

You have a problem and weren’t able to find the answer in this book? Here are your options:

> • **[www.voip-info.org](http://www.voip-info.org)**

> This site is dedicated to VoIP in general and to Asterisk, and it offers solutions to most problems. Unfortunately, many of the articles contain errors. If you find one, fix it! The next visitor will be grateful.

> • **IRC channel**

> There is an Asterisk IRC channel, #asterisk at [irc.freenode.net](http://irc.freenode.net). It’s sometimes possible to get a quick answer to your question there, but be warned: Some channel participants have a low tolerance for laziness. You improve your chances of success by thinking your question through carefully. Generally, the motto “explaining your problem is half the solution” applies.

> If you are new to IRC, you can learn more about it at [http://en.wikipedia.org/wiki/Internet_Relay_Chat](http://en.wikipedia.org/wiki/Internet_Relay_Chat).

> • **Mailing lists**

> The Digium mailing lists are not for everybody. The list has very high volume, and a new list user can be quickly overwhelmed. Still, it has a few significant advantages: It’s read by Digium staff, and they often answer questions. You can also get more detailed answers than is typical for IRC. You can find out how to subscribe to the mailing lists at [www.asterisk.org/support](http://www.asterisk.org/support) and [http://lists.digium.com](http://lists.digium.com).

> • **E-mail me**

> If all else fails, you can always try contacting Stefan ([stefan.wintermeyer@amooma.de](mailto:stefan.wintermeyer@amooma.de)). Just be warned that because of the volume of e-mail received, you might not receive a reply for several days.

## 2\. Installation and “Hello World”

Some newcomers to Asterisk say it takes at least two days of studying web pages and documentation before you can get an Asterisk server to do anything at all. If you don’t like delving into the theoretical underpinnings of a complicated piece of software like Asterisk and would rather see something practical and working as soon as possible, this chapter is the place to start. In contrast to the rest of the book, this chapter should be read, and the examples followed, in sequence.

> ### Note
> 
> The subject of this book is Asterisk, not Linux, and we assume that you have basic Linux administration skills. You should understand how to use a text editor and how to configure a network adapter. Commands are to be executed as the superuser root unless otherwise noted.

For the purposes of this introduction, it doesn’t matter whether you install Asterisk 1.4 or 1.6\. All the basics described here apply to both versions. For production installations, the more stable version is recommended, so these examples feature Asterisk 1.4.

### 2.1 Installing Asterisk on the Server

As to which Linux distribution or Asterisk version to choose, opinions differ (as is so often the case in the open source world). Some stick with distribution-specific packages (e.g., .rpm or .deb), whereas others compile Asterisk from source code. For the examples in this book, *it is best to install from source code.* The reasons are simple: The versions found in distribution packages are almost never current,^([1](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos134158)) and packages often use nonstandard configurations.

[1](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos134001). You can’t really blame the distributors for this. New versions of Asterisk come out almost every month. No distributor on Earth could match that pace.

Refer to [Appendix A](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos679664), “[Installation Instructions for Asterisk 1.4](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos679664),” and install Asterisk 1.4.x on a fresh install of Debian Linux or even KNOPPIX. For practice, you might consider doing this in an x86 virtual machine (e.g., VMware). In either case, be it a physical server or a virtual machine, the system should have a sound card and an output device (e.g., speakers) so that you can make test calls to the console to determine whether your system is working.

> ### Warning
> 
> Should you decide to try the install with a different distribution or with a different installation method and run into problems, try following the method described here first. It is often easier to work with a tested installation than it is to find the errors in an “off menu” configuration or environment.

### 2.2 Calling “Hello World” from the CLI

In this first example, we create a simple “Hello World” dialplan and call it from the Asterisk console, or CLI (command-line interface).

#### 2.2.1 Configuring Asterisk

After a standard install, you should find these files in the `/etc/asterisk` directory:

> ![image](images/00003.jpg)

That’s a long list, but don’t worry; we care about only one of them for our example`: extensions.conf`. To keep things simple, we’ll move the sample `extensions.conf` file created by **`make samples`** to `/var/tmp/asterisk-etc-backup/` (so that we can retrieve it later if required):

> ![image](images/00004.jpg)

Using your favorite console text editor^([2](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos137289)) enter the following text into `/etc/asterisk/extensions.conf:`

[2](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos137087). If you don’t have one, I recommend nano. Installing it in Debian is easy as superuser with **`apt-get -y install nano`**. Open the file you want to edit with **`nano` *`<filename>`***. The most important commands are displayed in the bottom portion of the screen.

> ![image](images/00005.jpg)

#### 2.2.2 Starting Asterisk and Calling “Hello World”

You might be surprised that just four lines are enough to configure Asterisk. Perhaps you thought Asterisk was more complicated than that. In any case, let’s give it a try. Start Asterisk with the command **`asterisk -c`** (the **`-c`** switch gives us the console):

> ![image](images/00006.jpg)

With this console, you can operate a running Asterisk server and give it commands interactively and in real time. Let’s try generating a call to our “Hello World” extension with **`console dial 1001`**:

> ![image](images/00007.jpg)

The command **`console dial 1001`** calls extension 1001\. This extension answers and plays the `hello-world.gsm` sound file from the `/var/lib/asterisk/sounds` directory.

> ### Note
> 
> **`console dial`** behaves like a very simple telephone. You can use it to call an extension and listen to it via the sound card.

##### *2.2.2.1 What Is an Extension?*

An extension is a programming unit in a dialplan. Every extension consists of at least one line, written in the following format:

> exten => *extension_name,priority,application*

Here, *priority* describes the sequence of the individual extension elements. Our extension 1001 has three priorities:

> ![image](images/00008.jpg)

The applications are self-explanatory:

> • **`Answer()`**

> Answers and opens a new Asterisk channel (see [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)”).

> • **`Playback(hello-world)`**

> Plays the file `hello-world.gsm` in the current channel (see [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)).

> • **`Hangup()`**

> Hangs up and closes the channel (see [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)).

##### *2.2.2.2 Increasing Verbosity*

When you are debugging Asterisk, you’ll often find it helpful to increase the verbosity of the console messages. When Asterisk is started with **`asterisk -c`**, the verbose level is set to 0 (the allowed range is 0 to 10). You can increase this to level 5 from the console with the command **`core set verbose 5`**, which is a good level to use for debugging:

> ![image](images/00009.jpg)

Now, when you enter the command **`console dial 1001`**, you see details about the dialplan execution:

> ![image](images/00010.jpg)

You can also set the verbose level to 5 at start time with the switch **`-vvvvv`** (five v’s).

> ### Warning
> 
> Don’t use **`core set debug`** to debug the dialplan! This is intended for developers doing Asterisk debugging. It is not very helpful for dialplan debugging, however.

#### 2.2.3 Stopping Asterisk

Enter **`stop now`**, and Asterisk stops:

> *CLI> **stop now**
> debian:/etc/asterisk#

### 2.3 Calling “Hello World” with a SIP Phone

Having tested our extension 1001 from the console, we take the next logical step and try the call from a SIP telephone. If you don’t have a hardware SIP phone, you can use a software SIP phone that you install on a client computer. Many of these are freely available on the Internet.

> ### Warning
> 
> If you want to install the software SIP phone and Asterisk on the same machine, you must set a custom port number for the SIP phone (e.g., 5061) because 5060 is already being used by Asterisk. Beginners, however, should start with a hardware SIP phone if at all possible. When starting out, minimize the potential for problems by not building unnecessary complexity into your test installation.

#### 2.3.1 Configuring the SIP Phone and sip.conf

Before you can use a SIP phone with Asterisk, you need to create an account for it in your Asterisk configuration. We will move the sample `sip.conf` file to our backup directory, `/var/tmp/asterisk-etc-backup/`, in the same way we previously moved `extensions.conf`, with the command **`mv sip.conf /var/tmp/asterisk-etc-backup/`**:

> debian:/etc/asterisk# **mv sip.conf /var/tmp/asterisk-etc-backup/**
> debian:/etc/asterisk#

Now we create a new `/etc/asterisk/sip.conf` and enter the following:

> ![image](images/00011.jpg)

Your SIP telephone must now be configured with the following account information:

> • **User:** 2000

> • **Password:** 1234

> • **SIP registrar:** IP address of your Asterisk server

> • **SIP proxy:** IP address of your Asterisk server

> ### Tip
> 
> Some phones require that every field contain information, even if it is not relevant. Unfortunately, there are no general instructions that will apply to all phones. Experiment!

#### 2.3.2 Starting Asterisk and the Phone

Now we start Asterisk in verbose level 5 with **`asterisk -vvvvvc`**:

> ![image](images/00012.jpg)

Next, we start the SIP phone and wait for the registration message in the Asterisk console:

> ![image](images/00013.jpg)

When you call extension 1001 from the SIP phone, you will hear the `hello-world.gsm` file played back to you.

##### *2.3.2.1 Calling the Phone from the Asterisk Console*

Because we can call an extension with **`console dial`** and we have successfully attached a SIP phone to the system, it should be possible to call that SIP phone from the console. To do this, we need to add an extension to `/etc/asterisk/extensions.conf:`

> ![image](images/00014.jpg)

To apply these changes, you must either restart Asterisk or reload the dialplan. To restart Asterisk, enter **`stop now`** in the Asterisk console and **`asterisk -vvvvvc`** in the Linux shell. To reload the dialplan from within the running Asterisk, enter **`dialplan reload`** in the Asterisk console. Now you can dial the SIP phone with **`console dial 2000`**:

> *CLI> **console dial 2000**

The dialplan application **`Dial()`** sets up a connection to a telephone. It uses a parameter consisting of two parts: the first, **`SIP`**, describes the technology used for establishing the connection (the SIP VoIP protocol in our example). The second part defines the target device using that technology (in this case, **`2000`**). When using **`Dial()`**, no **`Answer()`** or **`Hangup()`** is required. Because we do not know in advance whether the called station will even accept the call, **`Dial()`** has additional intelligence for opening and closing the channel.

In our example, the extension 2000 corresponds with the SIP target 2000, but this is, strictly speaking, coincidental. You could also write the extension like this:

> exten => 55,1,Dial(SIP/2000)

Reload the dialplan, and now you can call the same SIP telephone with **`console dial 55`**.

##### *2.3.2.2 Comments in the Configuration*

Because the number sign (#) corresponds to a dual-tone multi-frequency (DTMF) tone, it cannot be used as the comment character. Instead, Asterisk configuration files use the semicolon (;) for indicating comments, as follows:

> ![image](images/00015.jpg)

### 2.4 Building a Minimal Phone System with Two SIP Phones

What does the simplest possible working Asterisk system look like? Two phones and one Asterisk server.

We’ve already worked with all the individual pieces of this puzzle, and now we just have to put them together. To start, we configure two SIP phones in `/etc/asterisk/sip.conf`:

> ![image](images/00016.jpg)

Next, we have to make extensions that call the SIP phones in `/etc/asterisk/extensions.conf`. We will leave the “Hello World” example in place for testing purposes; we can verify that each phone is working by dialing 1001 and listening for the “Hello World” message. The resulting dialplan looks like this:

> ![image](images/00017.jpg)

Restart Asterisk and the phones (which you configure following the instructions in the previous section). After the phones have registered, you can call one phone from the other, or you can call the test extension from either phone.

#### 2.4.1 Configuring Voicemail

Asterisk already includes a working voicemail module. We need only configure it for use via the `/etc/asterisk/voicemail.conf` file. First, we move the existing sample file to our sample backup directory:

> debian:/etc/asterisk# **mv voicemail.conf /var/tmp/asterisk-etc-backup/**

Now we create a new `/etc/asterisk/voicemail.conf` file and enter the following:

> ![image](images/00018.jpg)

Now the mailboxes are configured (yes, it really is that easy). Each entry starts with the access password, then the full name of the user, and finally the user’s e-mail address. The final step is to add a few more lines to `/etc/asterisk/extensions.conf` to attach this voicemail functionality to our telephones. Don’t forget to add **`,20`** to **`Dial()`**:

> ![image](images/00019.jpg)

Done! Start Asterisk with **`asterisk -vvvvvc`** and call one phone from the other. (In a running Asterisk, typing **`reload`** in the Asterisk CLI is sufficient to apply any changes to the configuration files.) After 20 seconds of ringing (the reason for the **`,20`** in **`Dial()`**), you are transferred to the voice mailbox. If the called station is busy, the call goes directly to the voice mailbox. Dial 2999 from any phone and you can access the voicemail menu for that phone.

> ### Note
> 
> If your Asterisk server has a working Mail Transfer Agent (MTA) (e.g., send-mail or postfix), new voicemails are sent as e-mail attachments directly to the e-mail addresses specified in `voicemail.conf`.

If you want to secure your mailboxes with passwords, or would like to review the voicemail menus, see [Chapter 9](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos385865), “[Voicemail](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos385865).”

### 2.5 Rights Administration with Contexts

So far, we have been able to call any extension from any telephone. For a small, private system, this is sufficient. Large systems and systems connecting to other telephone networks need some way to manage calling rights (that is, the rules that determine which phones and users are allowed to make calls to where). Asterisk does this via *contexts.*

Think of a context as a kind of category. Each category contains rules about what can be dialed. To access the rules in a context, the phone must be a member of that context or have been directed to that context by another rule.

#### 2.5.1 The Originating Context

We haven’t yet specified a context for the SIP phones we configured. In this case, Asterisk assumes the `[default]` context. If we want to specify specific contexts for specific telephones, we use the following syntax in `sip.conf`:

> context = *ContextName*

We can set a context for all the phones in the `[general]` section, but this context can be overwritten on a per-telephone basis. Let’s take a look at a couple of examples.

##### *2.5.1.1 A Context Example*

ABC Co. has the SIP phones 10 and 11\. They are both in the `[internal]` context. The `sip.conf` file looks like this:

> ![image](images/00020.jpg)

You can achieve the same result more simply, though:

> ![image](images/00021.jpg)

##### *2.5.1.2 Example with Multiple Phones*

ABC Co. has the SIP phones 10, 11, 12, and 20\. The phones 10, 11, and 12 are standard staff phones in the `[abc]` context, and 20 is a courtesy phone at reception in the `[visitor]` context:

> ![image](images/00022.jpg)

#### 2.5.2 Call Destination: Contexts in extensions.conf

The dialplan, `extensions.conf`, is broken up into sections, or contexts. Each context is specified by a name in square brackets.

The following is a sample `extensions.conf` containing the three contexts, `[default]`, `[building-mgr]`, and `[apple-pie]`:

> ![image](images/00023.jpg)

If the context is not specified for a SIP phone in `sip.conf`, Asterisk assumes the `[default]` context in `extensions.conf`.

### 2.6 Calls to and from the Public Switched Telephone Network

In this section, we connect our mini-system to the public switched telephone network (PSTN). Once we’ve done that, we can make and receive calls using our attached SIP phones.

#### 2.6.1 Calling the PSTN

At this point, you have a working telephone system, which, although exciting, is not really useful, because it has no connection with the outside world. With just ten more minutes and a working Internet connection, you can have a working connection to the PSTN. To do this, you need an account with a SIP provider.

We will configure Asterisk so that you can make calls to the PSTN with the phones 2000 and 2001\. First, the provider account must be defined in `/etc/asterisk/sip.conf`:

> ![image](images/00024.jpg)

You must obtain the username (17984512232 in our example) and password (UHDZJD in our example) from the SIP provider; often you can do this through the provider’s customer website. Asterisk needs this information to register with the provider and make calls.

> ### Warning
> 
> Most SIP providers charge a per-minute rate for local calls, and many require prepayment. An advantage is that there is no monthly flat rate for most SIP accounts.

Next we need an additional dialplan rule to allow outbound calls:

> ![image](images/00025.jpg)

After these new entries have been entered, save the file and start Asterisk as before, with **`asterisk -vvvvvc`** so that we get the Asterisk console. Wait a few seconds for the SIP phones to register. Now simply dial a number.

> ### Tip
> 
> When dialing through most VoIP providers, you need to dial the complete number, including the predial digit (1 in North America) and area or city code, even if the call is a local call in your calling area. For North America, this means you dial the predial digit, followed by the full ten-digit number including area code, even in regions that do not already have ten-digit local dialing. In our example, we provide an open dialing pattern that will pass on the digits exactly as dialed to the provider. (Later on, we show you some techniques that you can use in `/etc/asterisk/extensions.conf` so that you don’t need to dial the full number for local calls in areas where it is not normally required.)

If everything is working as it should, you will hear the remote line ringing and be able to observe the call progress in the console.

It’s a bit early to explain exactly how this works, but you’ll read more about that later.^([3](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos165691))

[3](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos165585). Not too much at once! For now, all you need to know is that the `${EXTEN}` variable always contains the number dialed by the caller for the specific instance (see [Chapter 5](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos239678), “[Dialplan Programming](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos239678)”).

#### 2.6.2 Taking Calls from the PSTN

The last step is a small one: We want to be able to take incoming calls via our SIP provider on extension 2000\. To do this, we need to add another context to `/etc/asterisk/extensions.conf`:

> ![image](images/00026.jpg)

In our example, the number 17984512232 is the PSTN number (also called a DID or DN; more on that later) given to your account by your SIP provider. That the DID corresponds to the username is coincidental; it doesn’t have to.

You can, of course, configure voicemail for calls coming in from the PSTN:

> ![image](images/00027.jpg)

If you were so inclined, you could just leave things like this and start using your new mini-PBX. But what fun would that be? This chapter was only meant to show you how quickly you can build a working Asterisk system. In the coming chapters, we fill in the gaps and show you just how much you can really do with Asterisk.

## 3\. Dialplan Fundamentals

The dialplan is the heart of Asterisk, and everything it does begins here.

In Asterisk 1.4, two important files in `/etc/asterisk` make up the dialplan. The first is `extensions.conf`, which uses the original and Digium-recommended priority model. The second is `extensions.ael`, which uses the newer Asterisk Extensions Language; we’ll look at that in more detail in a separate chapter. For now, we’ll use the traditional priority model because even in 1.4 and 1.6 `extensions.ael` is converted into priority format and added to `extensions.conf` when Asterisk is started.^([1](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos168716))

[1](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos168610). The exact definition of *dialplan* is a matter of some debate in the telephony world. In this book, we use the word in its Asterisk-specific sense.

> ### Note
> 
> Should you use .conf or .ael? Digium says “.conf is the default.” For certain applications, however, AEL can make for a more readable and maintainable dialplan.

### 3.1 Contexts

The Asterisk dialplan is divided into sections, and each section is called a context. Any dialplan must begin with a `[general]` context where global configuration entries reside, but the subsequent contexts can have any name. Physical devices are bound to the dialplan through contexts. These devices are usually telephones, but can be other types of hardware (for example, SIP or Zap devices). The configuration for every device, be it a softphone, hardphone, or outgoing trunk, must specify the default context for that device. Here’s an example from a `sip.conf` file:

> ![image](images/00028.jpg)

This SIP device called 2000 always initiates calls in the `internal-phones` context. This means that if a caller uses this phone to dial a number, Asterisk will look in the `internal-phones` context for an extension matching that number. If no matching extension is present, nothing happens.

> ### Warning
> 
> A good understanding of contexts is essential for effective Asterisk programming and administration. If you’re not comfortable with contexts, follow the step-by-step example for a simple PBX system in [Chapter 2](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos131892), “[Installation and ‘Hello World.’](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos131892)”
> 
> It pays to take the time necessary to become comfortable with the concept.

Contexts are defined by a name inside square brackets ([*name*]). Ideally, the name should be relevant and help to describe the intended use for the context. This name will also be used to refer to the context elsewhere, be it in other contexts or in other Asterisk configuration files. All lines following a context name are considered part of that context, until the next context name is encountered:

> ![image](images/00029.jpg)

### 3.2 Extensions

Individual entries in `extensions.conf` are called *extensions.* Individual extensions are executed by Asterisk every time a call is initiated for that extension, but `extensions.conf` is only read into Asterisk once, at start time. This means that changes are not applied until the dialplan is reloaded or Asterisk restarted.

> ### Note
> 
> An exception is the Asterisk RealTime Architecture (ARA). In an ARA system, the dialplan is stored in a database (e.g., MySQL) and read into Asterisk for each call, not simply when Asterisk is started. Therefore, an administrator can make dialplan changes on a running Asterisk server that take effect immediately. Nevertheless, this approach is not without significant disadvantages. You can learn more about ARA at [www.voip-info.org/wiki/view/Asterisk+RealTime](http://www.voip-info.org/wiki/view/Asterisk+RealTime).

You can also refresh the dialplan during operation from the CLI (command-line interface) by entering the command **`reload now`** (which reloads all the configurations) or **`extensions reload`** (which reloads only the dialplan).

An extension consists of the following parts:

> • **Extension:** A name or number

> • **Priority:** A kind of program line number

> • **Application:** An instruction that tells Asterisk what it should do with the call

The following is a template example of how you specify an extension line in `extensions.conf`:

> exten => *extension,priority,application*

A real statement would look like this:

> exten => 123,1,Answer()

> ### Warning
> 
> The first priority in an extension must always be 1 (one); otherwise, Asterisk will never call the extension. Subsequent priorities must be incremented by 1 and not more. Asterisk does not recognize larger increments.

#### 3.2.1 Fundamental Applications

To build the dialplan examples in this chapter, we need the following basic applications (all of which are described in greater detail in [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)”):

> • **`Answer()`**

> The **`Answer()`** application does just that. It answers a call. When a channel rings, **`Answer()`** tells Asterisk to “lift the virtual receiver.”

> • **`Hangup()`**

> **`Hangup()`** is the opposite of **`Answer()`**. An active connection is terminated, and Asterisk “hangs up” the virtual receiver.

> • **`Playback(`*`soundfile`*`)`**

> This tells Asterisk to play a specified sound file. By default, it plays files found in `/var/lib/asterisk/sounds/`, but you can also specify another source directory. No file extension is specified because the directory may contain the same sound in different formats. Asterisk will select the most appropriate format (more on that later).

> • **`Wait(`*`number`*`)`**

> **`Wait()`** defines a pause; ***`number`*** indicates the number of seconds to pause.

> • **`NoOp(`*`string`*`)`**

> This application does nothing. **`NoOp`** means “no operation.” It is useful, however, when you are trying to troubleshoot the dialplan. When **`NoOp`(*`string`*)** is executed, Asterisk prints *string* on the CLI, but only if the verbosity level is set to 3\. (You can do this easily by entering the command **`set verbose 3`** in the CLI.)

> • **`VoiceMail(`*`mailbox,u`*`)`**

> Lets the caller leave a voice message in the mailbox specified.

> • **`VoiceMailMain()`**

> Provides access to the voicemail system. The mailbox owner will use this to retrieve her messages.

#### 3.2.2 Priorities

A typical extension is composed of multiple entries. Each entry has a priority so that Asterisk knows in what order it should execute the entries. If you’ve ever worked with early versions of BASIC, you might be familiar with line numbers; priorities work in much the same way, but with one important distinction. They are always executed in numeric order from smallest to largest, but there can be no skipping! If Asterisk executes an entry of priority *n,* then it will look for the next entry at *n* + 1\. If it cannot find an entry at *n* + 1, it stops executing without displaying an error in the CLI.

##### *3.2.2.1 A “Hello World” Example*

The following extension will be invoked when a phone with the default context `widgets` dials 8888.

Asterisk picks up the line, plays the `hello-world` sound file (which is installed with Asterisk), and hangs up.

> ![image](images/00030.jpg)

##### *3.2.2.2 n Priority*

To make it easier to work with priorities, Asterisk versions from 1.2 onward support the `n` priority. The `n` priority is like automatic line numbering; when Asterisk is running through the dialplan and encounters an entry with priority `n`, it simply executes it as though it were equivalent to the previous priority, plus 1\. This is useful when you have extensions with many entries and you need to add or remove an entry, because it saves you from having to renumber the entire extension. The following example illustrates what a standard extension would look like:

> ![image](images/00031.jpg)

You can define the same extension with the `n` priority:

> ![image](images/00032.jpg)

You can start using the `n` priority at any point in the extension, as long as all the subsequent entries also use it:

> ![image](images/00033.jpg)

### 3.3 Pattern Matching

In `extensions.conf`, patterns let us specify multiple number combinations in a single line.

Using what we know so far, we need to write a separate extension for each telephone number. As the system expands, this leads to unwieldy and error-prone dialplans. Suppose, for our example, we need numbers 100 to 109 to play the `hello-world` sound file. Our `extensions.conf` would look like this:

> ![image](images/00034.jpg)

> ![image](images/00035.jpg)

If we use a *pattern,* the same dialplan becomes instantly more compact and elegant:

> ![image](images/00036.jpg)

The `_10X` extension describes the number range from 100 to 109.

> ### Note
> 
> The terms *pattern* and *regular expression* are often casually interchanged. In general, what we are using in Asterisk is a *pattern,* although many programmers would use the term *regular expression* also.

#### 3.3.1 Pattern Elements

Dialplan patterns always begin with the underscore (_) character:

> exten => *_pattern,priority,application*

An Asterisk dialplan pattern can have the following elements:

> • **[abc]**

> The digits *a*, *b,* and *c.* For example, to match 34, 37, and 38

> exten => _3[478],1,NoOp(Test)

> • **[a-b]**

> Any digit in the range *a* to *b.* For example, to match any number between 31 and 35

> exten => _3[1-5],1,NoOp(Test)

> (e.g., `[25-8]` is also acceptable for the digits 2,5,6,7,8)

> • **X**

> Any digit from 0 to 9\. For example, to match any number between 300 and 399

> exten => _3XX,1,NoOp(Test)

> • **Z**

> Any digit from 1 to 9\. For example, to match any number between 31 and 39

> exten => _3Z,1,NoOp(Test)

> • **N**

> Any digit from 2 to 9\. For example, to match any number between 32 and 39

> exten => _3N,1,NoOp(Test)

> • *****

> Matches the asterisk (*) key

> exten => _*7,1,NoOp(Test)

> • **#**

> Matches the number sign or pound key (#)

> exten => _#7,1,NoOp(Test)

> • **_**

> Any number of digits of any kind. For example, to match all numbers that begin with 011

> exten => _011.,1,NoOp(Test)

> ### Warning
> 
> Don’t use the `_.` pattern! If you do, the pattern will include special extensions such as i, t, and h, and that will lead to unpredictable and probably undesirable behavior. Use `_X`. or `_X` if you need broad pattern matching.

> • **!**

> This special “wildcard” character will match as soon as the number dialed is unambiguous; i.e., when the number being dialed cannot match any other extension in the context. Once a match is made, the outgoing line is picked up and dialing proceeds in real time with direct feedback (this is known as *overlap dialing*).

> ### Warning
> 
> A common error is to forget the underscore (_) character at the beginning of the pattern. This convention is necessary because SIP devices, as configured in `sip.conf`, can have alphanumeric names. (For example, in Asterisk, 333, loadingdock, and A31 are all acceptable names for a SIP device.) It also means that if you forget to use the underscore, your extension will never match *and* you will never see an error message informing you of your mistake.

#### 3.3.2 Testing a Pattern Using dialplan show

An example dialplan looks like this:

> ![image](images/00037.jpg)

We can call **`dialplan show`** from the CLI (invoked with **`asterisk -r`** if Asterisk is already running) to verify that our dialplan has been loaded:

> ![image](images/00038.jpg)

The output includes all the dialplan rules that Asterisk knows about. Notice that there is a `parkedcalls` context that we haven’t seen before; this is activated by default in `features.conf` and needn’t concern us further. What if we are only interested in the `my-phones` context? We can make our request more specific with **`dialplan show my-phones`**:

> ![image](images/00039.jpg)

The command **`dialplan show`** can also be used to show what Asterisk will do if we dial a specific number. Suppose we want to dial 25 from a phone in the `my-phones` context. We can see what will happen with the command **`dialplan show 25@my-phones`**:

> ![image](images/00040.jpg)

Nothing happens because there is no match for 25 in the context. If we dial 23 instead, we get this output:

> ![image](images/00041.jpg)

If we want to check 23 against all the accessible contexts, we use **`dialplan show 23@`**:

> ![image](images/00042.jpg)

Let’s expand our dialplan with an additional context by editing `extensions.conf` like so:

> ![image](images/00043.jpg)

Now we go back to the CLI and, after reloading the dialplan with the **`reload`** command, run **`dialplan show 23@`**:

> ![image](images/00044.jpg)

All the matching extensions are displayed. Let’s try it with **`dialplan show 23@`**:

> ![image](images/00045.jpg)

There is only one match, in context `department-q`. In this example, if you dial 25 from a phone in the `my-phones` context, you still won’t hear the “Hello World” message. Extension 25 only works for phones in the `department-q` context.

#### 3.3.3 Pattern-Matching Order

Although very powerful, pattern matching in your Asterisk dialplan can be tricky. It is easy to assume that Asterisk runs through the dialplan in a completely sequential manner. This is generally the case, but it does prioritize patterns based on the quality of the match.

The reason for this is simple: More than one pattern might match a dialed number. If two extensions match a dialed number, Asterisk will always choose the better match. Before deciding which extension matches best, it processes the entire context.

Let’s look at an example with some ambiguous extensions:

> ![image](images/00046.jpg)

It is not immediately clear which extension is executed when we dial 12345\. To find out, we use **`dialplan show 12345@sales`**:

> ![image](images/00047.jpg)

Asterisk shows all the hits, but gives extension `12345,1,NoOP{12345}` first priority. The highest priority extension is always displayed at the top.

Let’s try it with 12346 using the command **`dialplan show 12346@sales`**:

> ![image](images/00048.jpg)

Again, the pattern with the best match to the dialed digits is listed first.

> ### Important
> 
> The order in which the patterned extensions appear in the dialplan makes no difference. Patterned extensions are matched strictly in order of match precision.

Digium changed the expected behavior for the `_.` pattern in Asterisk 1.2\. Although the pattern is the most general and should be therefore assigned the lowest priority, the behavior is opposite the expected behavior. In Asterisk 1.2, the extension `_.` always gets the highest priority!

> ### Note
> 
> Note that the **`show dialplan`** command will work in Asterisk 1.4 but is deprecated. From here on out, examples for Asterisk 1.2 use **`show dialplan`**, and **`dialplan show`** is used for examples in Asterisk 1.4.

Let’s try adding the extension `_.` to our previous dialplan example:

> ![image](images/00049.jpg)

When we try testing 12346 with **`dialplan show 12346@sales`**, we get the following output:

> ![image](images/00050.jpg)

In Asterisk 1.2, **`show dialplan 12346@sales`** gives a very different result:

> ![image](images/00051.jpg)

This is why it is preferable to use `_X.` as the wildcard pattern (if we use a wildcard pattern at all!). The following dialplan example is processed identically in Asterisk 1.2 and 1.4:

> ![image](images/00052.jpg)

The priorities appear as follows in both versions:

> ![image](images/00053.jpg)

### 3.4 Include Statements

Includes are a powerful tool for simplifying and organizing larger dialplans. Using an `include` statement, you can include other contexts in the current context. Here is a more general example:

> include => *name-of-the-other-context*

And here is how you might see an `include` statement used in a larger dialplan:

> ![image](images/00054.jpg)

#### 3.4.1 Order of Execution When Using Include Statements

Asterisk will always look for a match in the current context before referencing any included contexts. If a matching entry is found, that entry is used. If no matching entry is found, Asterisk will look for a match in the first included context, then the next, and so on. It is also possible to have nested includes; that is, includes *within* includes.

You can verify what entry Asterisk is using to handle a call by entering **`dialplan show` *`number@name-of-context`*** in the Asterisk CLI.

> ### Note
> 
> Users of Asterisk 1.2 use **`show dialplan`** rather than **`dialplan show`**.

Again, here is an example of an `include` statement:

> ![image](images/00055.jpg)

Say we want to understand how Asterisk is handling a call to 2000 in the `sales` context. To do that, we enter **`dialplan show 2000@sales`** in the CLI:

> ![image](images/00056.jpg)

If we then expand the `sales` context like so

> ![image](images/00057.jpg)

We will see this CLI output:

> ![image](images/00058.jpg)

Asterisk will play the `hello-world` sound file and not send the call to 2000, even though the `include` occurs first in the dialplan. This is because Asterisk will always look for a match in the current context before checking the included contexts.

#### 3.4.2 Time-Conditional Include Statements

An `include` statement can be made conditional upon the time of day. This makes it easy to implement different day and night behaviors. The general syntax of a time-based `include` statement is shown here:

> include => context|<*time*>|<*day*>|<*day-of-month*>|<*month*>

The day and month are specified using the first three letters of the full name. For example, weekdays are specified `mon`, `tue`, `wed`, `thu`, `fri`, `sat`, `sun`, and months are specified `jan`, `feb`, `mar`, `apr`, and so on. The time is specified in 24-hour format.

Suppose, for example, that you have a business that is open from 9:00 a.m. until 9:00 p.m. Monday to Friday and from 9:00 a.m. to 6:00 p.m. Saturday. The dialplan would look like this:

> ![image](images/00059.jpg)

### 3.5 The ${EXTEN} Variable and the ${CALLERID(num)} Function

Though we’ll examine variables (see [Chapter 5](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos239678), “[Dialplan Programming](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos239678)”) and functions (see [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), “[Dialplan Functions](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249)”) in more detail later, we want to introduce two simple and intuitive elements here: the system variable `${EXTEN}` and the function `${CALLERID(num)}`.

#### 3.5.1 ${EXTEN}

Asterisk automatically puts the dialed number in the `${EXTEN}` system variable. Instead of

> exten => 2000,1,Dial(SIP/2000)

we can use

> exten => 2000,1,Dial(SIP/${EXTEN})

and get the same result. This doesn’t make much difference for a single line, but if you use this in conjunction with pattern matching it saves a lot of time and makes for a much more readable dialplan.

To make all the SIP phones with extension numbers 2000 to 2999 dialable, only one line in `extensions.conf` is required:

> exten => _2XXX,1,Dial(SIP/${EXTEN})

#### 3.5.2 ${CALLERID(num)}

The function `${CALLERID(num)}` always returns the calling party’s number. This is especially practical when used with `VoiceMailMain()` because it can accept the mailbox number as a parameter. This way, you can make each user’s voicemail box accessible with a single line:

> exten => 99,1,VoiceMailMain(${CALLERID(num)})

You can find a more complete discussion about `${CALLERID(num)}` in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), “[Dialplan Functions](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).”

## 4\. Case Study: A Typical Business Telephone System

Building on what we covered in [Chapter 2](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos131892), “[Installation and ‘Hello World,’](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos131892)” in this chapter we put together a more comprehensive system for a fictional business. Doing so will show you how to handle the requirements you’re likely to be faced with in real installations.

Our fictional company is Widgets, Inc., a widget manufacturing business. We’ve been charged with the task of planning a phone system for the new office, which houses the following departments:

> • Management (2 people)

> • Reception (3 people)

> • Domestic sales (6 people)

> • International sales (4 people)

> • Production (50 people)

> • Shipping (10 people)

> • IT (2 people)

> • Building manager (1 person)

Every employee has his or her own phone.

What costs should Widgets, Inc. anticipate? That depends very much on management’s objectives. The following should be considered:

> • Should the Asterisk server be fault tolerant? Will a cold-standby server be sufficient, or do we need a hot standby?

> • What server hardware are we buying? For most systems, a generic computer will suffice. It doesn’t have to be the newest and most expensive.

> • Which phones are we buying? Phones can range in price from $30 to $300 and up.

Does Asterisk actually make sense for Widgets, Inc., or is this just a make-work project for the IT department? This depends on what the traditional PBX vendors are offering and Widgets, Inc. needs. Although it’s not unusual for traditional vendors to produce surprise discounts when they discover an Asterisk system is being considered, there can be hidden costs, sometimes in the form of fixed long-term contracts that force the client to buy from that vendor for several years.

One of the advantages of Asterisk (and open source software generally) is the wide choice and availability of support and consulting services. You can do it all yourself, or you can hire a consultant to do it all for you. If you find the services of your existing consultant unsatisfactory, you can switch to another. This is usually difficult with traditional vendors because they lock you in with a contract and because the proprietary nature of the product also means there is some degree of sales territory exclusivity.

Whether Asterisk makes economic sense has to be calculated on a case-by-case basis. Experience shows that it usually does. If you consider the extensibility, freedom to upgrade (or not), and scalability of Asterisk in your calculations, the mid-and long-term capital and operating costs of an Asterisk system usually prove highly affordable.

What about a packaged Asterisk system, such as FreePBX, Trixbox, PBX-in-Flash, Elastix, or Gemeinschaft? “Prerolled” Asterisk systems have their advantages (rapid installation and configuration, simple interfaces for commonly used features, a GUI) and their disadvantages (lack of transparency, configuration restrictions, smaller installed base). A well-written dialplan for a generic Asterisk installation can serve as a template for new installations, and an experienced Asterisk specialist can have new, complex systems up and running in the same time or less than it takes to set up a prerolled Asterisk. Whatever you choose, you’re better off knowing how Asterisk works under the hood before you take the prerolled route. That’s the purpose of this book!

### 4.1 The Numbering Plan

The business has 78 employees. Although it’s possible to get by with two-digit extension numbers, we’ll use three; this leaves us some breathing room in the event the company expands or we need more extensions (for example, for fax machines or for group numbers). See [Table 4.1](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos214958).

**Table 4.1** Numbering Plan for Widgets, Inc.

![image](images/00060.jpg)

### 4.2 Choosing the Infrastructure

The new building is getting a modern structured cabling system, so it makes sense to equip each workstation with a SIP phone. This saves us the grief and extra expense of running telephone wiring in parallel to the network wiring. Fax machines and cordless telephones can be connected to the system using analog telephone adapter (ATA) devices.

> ### Warning
> 
> Faxing in Asterisk is nevertheless problematic. VoIP connections, depending on how they are compressed, can have less bandwidth available than a fax connection requires. This can result in fax transmissions being only partially received, or worse, failing completely. If you are only using VoIP internally, you must ensure that the codecs you choose can adequately support fax. The better option is to use an analog telephony card to provide internal analog extensions purely for fax use, or, ideally, build fax server functionality into Asterisk.

We install the Asterisk server in a climate-controlled server room with controlled access. Only authorized personnel are to have access to the server.^([1](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos216785))

[1](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos216679). In the past, it was common for PBX and key system manufacturers to build secret backdoors into their systems, mainly for the purpose of providing timely support in the event of an outage. It was inevitable that clever but unscrupulous parties would figure out a way to exploit these backdoors to make free long-distance and international calls, mostly at the expense of public institutions too large to have a clear picture of how their systems were configured. In today’s world, the security of your systems, whether they are Asterisk or anything else, should always be a paramount concern.

#### 4.2.1 Network

The network is such a significant aspect of Asterisk’s functionality that it demands a more thorough discussion.

Telephony is a synchronous medium, which means that the receiver must accept the sender’s transmission the instant it is sent. Human beings can tolerate a delay (also known as latency) of up to 300ms (milliseconds), although the delay can be perceptible when over 100ms and distracting when over 200ms. Most people find anything over 500ms unacceptable. This is the principal challenge that IP telephony must address: In IP telephony, we are attempting to carry a synchronous data stream over an asynchronous medium. TCP/IP, developed with funding from the U.S. Defense Advanced Research Projects Agency (DARPA), was designed to maximize stability and robustness, but it achieves this at the expense of the kind of real-time performance we would expect of a telephone connection.

When an e-mail suffers an occasional pause in transmission, it is materially unaffected. A voice conversation, by contrast, is highly time dependent. If someone says “hi” to us, we expect it to be followed by something relevant and intelligible immediately (such as our name), because that is the way people speak to each other in person. That we can even carry voice traffic on an IP connection is owing to the high performance of modern network hardware. The high bandwidth of modern networks coupled with the relatively small bandwidth required by a single telephone-grade voice conversation means that voice traffic can be carried in a pseudo-real-time fashion.

Nevertheless, network conditions vary, both by site and in time. A big network with many endpoints will carry a lot of traffic; networks also tend to be busier during normal business hours (say from 8 a.m. to 6 p.m.) while employees send and receive e-mail, surf the web, download programs and documents, etc. This happens to be the time they make most of their telephone calls, and things can reach a critical point very quickly. If the available bandwidth drops below the minimum needed, we will start to see packet delay or loss. When this happens, the effect on voice conversations is drastic and immediate, resulting in dropouts, clipped words, clicks, pops, and other strange noises. Anybody who has any experience with wireless telephone service knows how distracting this can be. To deal with these eventualities, commercial-grade routers and most managed switches support some kind of traffic classification through setting a TOS (Type of Service) flag in the packet header.

By setting a TOS flag in voice packets, we can prioritize traffic passing through the router or switch. This feature is useful for managing traffic inside our network and across the network boundary, but it has no impact once the packets are on the Internet service provider’s (ISP) network or on the public Internet. Only once the ISP guarantees low latency and bandwidth for real-time traffic can we have an assurance of call quality (called quality of service, or QoS). If you will be supporting a multibranch operation and plan to connect them with VoIP, you should consider this requirement carefully and discuss it with your ISP.

The Asterisk system for Widgets, Inc. has at least 78 physical stations. In the worst case, we will have 39 simultaneous conversations (which happens if all the employees call each other). Depending on the codec used, we can expect a maximum bandwidth of 6,500kbps (kilobits per second), which should be no problem for a typical 100Mbps (megabits per second) LAN on structured, twisted-pair cable.

All the same, this network will be carrying other traffic, and a couple of big file transfers can be enough to hit performance limits. How do we get the 6,500kbps value? The standard G.711 compression standard includes two companding algorithms: u-law (used in North America and Japan) and a-law (used in Europe).^([2](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos221967))

[2](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos221861). These two algorithms are used for carrying voice traffic in ISDN channels (such as those used in T1 and T3 connections).

These provide excellent sound quality, but need at least 64kbps bandwidth. A single connection consists of an incoming and outgoing channel, each at 32kbps; 39 connections add up as follows: 2 × 39 × 32kbps = 2,496kbps. In addition to the channel bandwidth required, there will be TCP/IP network overhead, so that each channel will use about 80kbps in total. Now our total is 3,120kbps; round up, and we have 3,500kbps. While this is only a worst-case scenario, when it comes to voice systems, it is better to be safe than sorry!^([3](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos222831))

[3](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos222725). The website [www.asteriskguru.com/tools/bandwidth_calculator.php](http://www.asteriskguru.com/tools/bandwidth_calculator.php) has an Asterisk bandwidth calculator with bandwidth values for various codecs that can help you in the planning process.

> ### Tip
> 
> If you have doubts about whether you have sufficient bandwidth available to support all your extensions, consider starting with a lossier codec, such as Global System for Mobile (GSM). At between 13kbps and 15kbps per connection, it needs only a fifth of the bandwidth of u-law and delivers adequate sound quality for most applications. After you’ve verified the stability of your system, you can try switching groups of extensions over to u-law and wait to see whether you have network problems as a result. Just remember highly compressive codecs like GSM are more processor intensive, so you need to ensure you have adequate CPU resources available on your Asterisk server.

#### 4.2.2 Server Hardware

The choice of server hardware for the Asterisk server is subject to many of the same considerations. The need for synchronous, real-time data transfer requires timely handling of the necessary processes in Asterisk. Most of the computing effort comes in the coding and decoding of digital sound streams; this effort is even greater if you have equipment that uses different codecs and Asterisk has to transcode between them.^([4](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos224954)) The tremendous variety and quantity of hardware available means there is no hard-and-fast rule for calculating processor requirements. As a guide, however, we can start with [Table 4.2](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos225320).

[4](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos224636). Transcoding is the process by which an audio stream in one codec is translated into another codec. For example, a connection between a device supporting only GSM and one supporting only G.711 will have to be transcoded; this is normally done by Asterisk.

**Table 4.2** Server Hardware Benchmarks

![image](images/00061.jpg)

By *CPU,* we mean a typical CPU from an off-the-shelf PC (e.g., Intel or AMD). We’ve calculated the number of simultaneous connections based on the reasonable assumption that not all the phones will be active at one time, but rather between one-third and one-half. Note that this is just a rough estimate, with a considerable margin of safety. If little transcoding, conferencing, or echo cancellation is required, the number of simultaneous connections supported would be higher. That said, the exact limits for any given installation can be reliably determined only through direct testing and experimentation.

> ### Tip
> 
> The Linux program top provides a simple tool for monitoring processor loads on a running server, but only at the current point in time. Processor and process loads are dynamic and change dramatically from one moment to the next, so point measurements have limited usefulness. You can try monitoring the performance of your Asterisk servers using monitoring tools like Nagios ([www.nagios.org](http://www.nagios.org)). If you prefer to use native Linux tools, you can do simple monitoring with a cron job running a bash script with this content:
> 
> > w | head -n 1 >> /var/log/serverloads

By running this cron job every minute, you will build up a set of data points over time which you can use to evaluate server performance.^([5](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos227422))

[5](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos227316). This cron job would indeed be a very simple analysis tool. If you are comfortable with shell scripting, you can write more comprehensive scripts, which can give you more detailed information, by using output from tools such as top and uptime, processing it, and dumping the processed output into a comma-delimited text file that you can graph in a spreadsheet program.

Widgets, Inc. has 78 employees, and an estimate of 40 simultaneous connections is reasonable, so a computer with a reasonably current CPU (e.g., Pentium 4, AMD Athlon) at a clock speed of 1.5GHz should suffice. In general, the newer the CPU and system, the better the performance. Processor clock speed is no longer an accurate measure of CPU performance, particularly as applied to the newer dual-core processors, and your server will likely be able to handle more calls with a newer processor at the same clock speed. Dual-processor machines will improve performance correspondingly.

For the voice mailboxes, we need about 0.1MB (megabytes) of disk space per minute of message time.^([6](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos228735))

[6](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos228629). This is for wav49 or GSM format message files. If you decide to use uncompressed WAV format files, you will use many times the space (up to ten times as much). Because disk space is cheap, however, this is not normally an issue, and more installations are using uncompressed WAV because of the higher sound quality. Remember, though, that more disk space used means more storage required for backup.

If we allot 30 minutes of message storage to each user, we can expect to use a total of about 2GB (gigabytes) of disk space. Because voice message data is valuable business data and can even be critical, the storage should be redundant and backed up regularly. A RAID 1 array (two disks or disk sets in a mirror configuration) will provide the necessary redundancy.

> ### Warning
> 
> Note that software RAID burdens the CPU significantly. A professional installation should use hardware RAID if at all possible.

Memory requirements for Asterisk are not onerous, and 512MB RAM will suffice. With 1GB RAM, Asterisk can handle very large business units. Any additional steps taken to enhance the reliability and performance of the server, such as the installation of redundant network adapters, commercial-grade telephone interface cards, and uninterruptible power supplies, will go a long way to increasing user and decision-maker confidence in the system. If your background is in IT services, you are facing a whole new level of user expectations. Users will usually tolerate a brief e-mail outage; the phones, however, must always work. Readers with a background in circuit-switched telephony will know exactly what we are talking about. Hell hath no fury like an executive without a working desk set.

### 4.3 Base Configuration

We’ll configure Asterisk so that all the employees can call each other and have their own mailbox. When that’s done, the system can be extended with additional functions and modules.

#### 4.3.1 A sip.conf for 100 Users

Configuring `/etc/asterisk/sip.conf` for 100 users is no different from configuring for 2 users; there are no shortcuts here. Each SIP extension must be configured individually. What follows is an abridged version of the `sip.conf` for Widgets, Inc. Lines beginning with the semicolon (;) are treated as comments and ignored by Asterisk. The file is composed in the same way as in our simple example in [Chapter 2](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos131892). In general, we’ve avoided assigning numbers to individual users that end in 0 because we want to reserve those numbers for group phone numbers. The building manager is an exception, however, because we don’t anticipate any need for a group phone number there.

> ![image](images/00062.jpg)

> ![image](images/00063.jpg)

> ![image](images/00064.jpg)

> ![image](images/00065.jpg)

> ![image](images/00066.jpg)

You can make `sip.conf` more concise with templates. For more information, refer to [Appendix F](#Practical_As-sk_1.4_and_1.6_split_036.html_filepos1586556), “[Configuration Templates](#Practical_As-sk_1.4_and_1.6_split_036.html_filepos1586556).”

Our example `sip.conf` has two instances of the `callerid` variable. This variable sets what is displayed on the called party’s telephone:

> callerid = "Building Manager" <150>

In our example, both the building manager’s phones (150 and 151) use the caller ID 150 and the caller ID name Building Manager. This ensures that returned calls always go to extension 150.

#### 4.3.2 The Dialplan

In [Chapter 2](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos131892), we wrote a simple dialplan for two phones. In the case study in this chapter, we have more users. Writing a dialplan with 100 entries is not exactly difficult, but it is tedious, and maintenance could become a problem. It’s much better to use pattern matching in `extensions.conf` using the patterns described earlier in this book.

##### *4.3.2.1 extensions.conf*

The numbering plan^([7](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos234935)) for Widgets, Inc. translates into a readable, and maintainable `extensions.conf`, which looks like this:

[7](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos234691). With the exception of the emergency numbers. We’ll deal with those as soon as we’ve established a connection to the outside world.

> ![image](images/00067.jpg)

> ![image](images/00068.jpg)

> ![image](images/00069.jpg)

The extensions in the `[internal-calls]` context mean all calls to numbers 100 to 599 are passed to the `Dial()` application exactly as dialed, connecting the calling party to the corresponding SIP phone. If the user dials 800, she is connected to the mailbox for that phone. Only the IT department can call 801, at which point the system prompts for a mailbox number. This is done so that the IT department, which is now responsible for supporting the telephone system, can access all the mailboxes for debugging purposes.

In actual practice, our dialplan would have to be somewhat more complex. The numbering plan has number ranges (e.g., 270 to 299) that don’t contain any telephones. Our example ignores this, but this could lead to confusion in an actual deployment. If a user dials an unassigned number, the call goes straight to a voice mailbox that may or may not exist; even if it does, the user could leave messages that are never retrieved.

To prevent this from happening, the `[internal-calls]` context would look like this:

> ![image](images/00070.jpg)

For Widgets, Inc., we accept this risk for the sake of simplicity and use the following configuration:

> ![image](images/00071.jpg)

##### *4.3.2.2 voicemail.conf*

The `voicemail.conf` remains as described in [Chapter 9](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos385865), “[Voicemail](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos385865),” except with a few additional entries restricting message length and defining the server e-mail address:

> ![image](images/00072.jpg)

> ### Note
> 
> The passwords used in the preceding example are for demonstration purposes only. You’ll want to use stronger passwords in an actual production installation.

### 4.4 What Next?

The preceding configuration for Widgets, Inc. serves as a planning example for all systems of similar size. You can use this configuration to experiment with many of the configuration examples in this book.

This system allows telephone calls only and includes a simple voicemail system. A professional installation usually demands features such as teleconferencing and queues. If this is what you need, you have two basic options: You can reinvent the wheel and build a dialplan that includes those features from scratch, or you can use a standard framework such as FreePBX ([www.freepbx.com](http://www.freepbx.com)) or Gemeinschaft ([www.amooma.de/gemeinschaft](http://www.amooma.de/gemeinschaft)) and configure it according to your requirements. (At the moment, Gemeinschaft is available only in German. Volunteers willing to help internationalize it are welcome! Contact Stefan at [stefan.wintermeyer@amooma.de](mailto:stefan.wintermeyer@amooma.de).)

## 5\. Dialplan Programming

In Asterisk, functions or programs can be implemented either externally, through an Asterisk Gateway Interface (AGI) script (in much the same way that a Common Gateway Interface [CGI] script can add functionality to a web page) or internally, through functions and applications in the dialplan. This chapter focuses strictly on the internal functions; AGI is treated in depth in a separate chapter.

The dialplan is defined in the `extensions.conf` configuration file. The dialplan itself looks much like a BASIC program. The administrator can implement features and call flow using a simple scripting language.

### 5.1 Programming “How-To”

Whatever your experience level with Asterisk (whether you’re an administrator, programmer, telephone specialist, or hobbyist), you need a basic level of programming skill and a grasp of the fundamentals to take full advantage of Asterisk. This how-to should give you the basic understanding you need to make useful dialplans, through the use of plenty of examples and with frequent reference to [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029).” You will probably recognize some of the material from other chapters.

#### 5.1.1 Program Structure

Each telephone number defined in the Asterisk dialplan (`/etc/asterisk/extensions.conf`) is really a small program. In Asterisk, the program is called an *extension.* An extension looks like this:

> ![image](images/00073.jpg)

Priorities may also be numbered sequentially:

> ![image](images/00074.jpg)

The two extensions depicted here are functionally identical. If you use `n`, however, it makes adding and deleting entries in the extension much easier later on.

#### 5.1.2 Using Set()

Use the application **`Set()`** to create and change variables:

> ![image](images/00075.jpg)

Use the syntax `${VARIABLENAME}` to read and print variables. You can print variable values on the CLI with `NoOp()` (with verbosity level 3 and up):

> ![image](images/00076.jpg)

There are different kinds of variables:

> • **Global variables**

> Valid anywhere in the dialplan and created or modified with `Set(<variable>=<content>,g)`:

> ![image](images/00077.jpg)

> • **Channel variables**

> Valid only in the current channel (a channel could be a connection between two people having a phone conversation). Created or modified with `Set(<`*`variable`*`>=<`*`content`*`>)` (without the `g`):

> ![image](images/00078.jpg)

> • **System variables**

> These dynamic variables are set by Asterisk and may be called in the dialplan without needing to create them. A frequently used system variable is `${EXTEN}`:

> exten => 1006,1,NoOp(Dialed number: ${EXTEN})

For a more in-depth look at variables, see the “[Variables](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos249041)” section, later in this chapter.

> ### Note
> 
> For all the commands discussed in this chapter, you can find syntax and options in [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029).

#### 5.1.3 Labels and Goto()

**`Goto()`** lets you jump from one dialplan entry to another. If you are using `n` priorities, this can be problematic. The solution is to use labels to tag specific entries and then call the entry by label in **`Goto()`**.

You can use **`Goto()`** within an extension, between extensions, or between contexts.

> • You might use it within an extension:

> ![image](images/00079.jpg)

> • Between extensions:

> ![image](images/00080.jpg)

> • Between contexts:

> ![image](images/00081.jpg)

#### 5.1.4 While() Loops

Loops let you perform operations repeatedly, which is useful for reading out sequences. Use **`While()`** to run loops in the dialplan:

> ![image](images/00082.jpg)

#### 5.1.5 GotoIf() Conditional

You can jump to other parts of the dialplan, if a specific condition is met, with **`GotoIf()`**:

> ![image](images/00083.jpg)

#### 5.1.6 Gosub() Subroutines

With **`Gosub()`**, the call is directed to a subroutine; it can be returned to the initiating priority with **`Return()`**:

> ![image](images/00084.jpg)

### 5.2 Variables

A variable is a placeholder for an actual value. Exactly what that value is depends on the kind of variable. In Asterisk, variables can contain numbers, letters, and strings (sequences of letters and numbers). Variables are useful because they let us create rules for call flow that apply in changing circumstances and make it easier to accommodate future changes in the telephone application or system. In Asterisk, variables have varying scope. There are local variables (called *channel variables* in Asterisk), which can only set values for the current, active channel, and global variables, which set values for all channels. We should already be familiar with some of the variables Asterisk sets from our exposure to them as configuration parameters in the Asterisk configuration files (such as `sip.conf`, for example). We also have the freedom to define our own variables and use them in configuration files.

#### 5.2.1 Expanding Variables in an Extension

The value of a variable can be obtained using the syntax `${`*`VARIABLENAME`*`}`. There are variables that are automatically set by Asterisk. For example, the called number is always stored in the Asterisk system variable `${EXTEN}`. Using patterns and variables, it is often possible to dramatically compress a long dialplan.

Without variables, a set of extensions would have to be represented like this:

> ![image](images/00085.jpg)

Using a variable, however, lets us make multiple extensions succinct:

> exten => _10X,1,Dial(SIP/${EXTEN})

#### 5.2.2 General Considerations

When working with variables, you need to keep a few things in mind. First, variables are not case sensitive. String variables should be enclosed in quotes as a matter of practice. Reserved characters need to be escaped if you’re going to use them in a variable, and integer variables have size limits. Let’s explore these considerations in detail.

##### *5.2.2.1 Capitalization*

Variable names needn’t be in all uppercase as in our examples, nor are user-defined variables case sensitive. It is a good idea to use uppercase variable names nonetheless because it makes the variables easier to identify and the dialplan code easier to read. Unfortunately, this means you cannot distinguish variable names based on case. For example, `${FOO}` is considered the same as `${foo}`.

> ### Important
> 
> Asterisk system variables such as `${EXTEN}` must always be uppercase.

##### *5.2.2.2 Using Double Quotes with String Variables*

String variables (meaning variables that contain text and not numbers) should be defined using double quotes, though Asterisk will still accept them without double quotes. The following two entries are functionally identical:

> ![image](images/00086.jpg)

If the string contains commas or spaces, you must use double quotes:

> exten => 1234,1,Set(FRUITTYPES="Apple, Pear, etc.")

This is why it is a good idea to get into the habit of using them for any string variables you define.

##### *5.2.2.3 Reserved Characters*

Sometimes a variable will contain reserved characters (characters that have special functions and are interpreted differently). For example, if you want a variable to contain the underscore character (_), you must use an “escape” character to tell the dialplan interpreter that it should ignore the reserved character. The following characters must be escaped when used in a variable:

> [ ] $ " \

The escape character in `extensions.conf` is the backslash (\):

> exten => 1234,1,Set(AMOUNT="\$10.00")

Similarly, if you want to use the backslash character in a variable, you must escape it:

> exten => 1234,1,Set(ROOMNUMBER="48\\10")

##### *5.2.2.4 Limits on Integer Size*

If a variable contains an integer, it can have no more than 18 digits. Anything larger will cause an error, which will be recorded in the log file.

> ### Tip
> 
> If you need to work with larger integers or floating point numbers, you can use an AGI script (see [Chapter 16](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos590427), “[Asterisk Gateway Interface](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos590427)”).

#### 5.2.3 Defining Global Variables in extensions.conf

Global variables are defined at the beginning of `extensions.conf`. You must place them in the special `[globals]` context, which follows `[general]`:

> ![image](images/00087.jpg)

#### 5.2.4 Defining Variables with Set()

**`Set()`** is used to define a variable inside an extension (see also the application description in [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)). The general syntax is `Set(<`*`variable1`*`>=<`*`value1`*`> [,<`*`variable2`*`>=<`*`value2`*`>][,<`*`option`*`>]).`

Setting option `g` makes the variable global. Without it, the variable is treated as a local channel variable:

> ![image](images/00088.jpg)

#### 5.2.5 Inheritance of Channel Variables

If new channels are spawned while a conversation is in progress, they will have their own channel variables.

##### *5.2.5.1 Single-Level Inheritance*

Sometimes you want to have a channel variable persist into the spawned channel. You can do this by prefixing the variable with an underscore (_) character. When the variable is inherited by the spawned channel, Asterisk automatically removes the prefix. This ensures that the variable is inherited only once.

The variable in this example will be passed to any dependent channels:

> exten => 1234,1,Set(_CAKE="Marble cake")

##### *5.2.5.2 Multilevel Inheritance*

If you need unlimited inheritance of a channel variable, you can do this by prefixing the variable with two underscore characters (__). Variables prefixed in this way will always be inherited by spawned channels.

> ### Warning
> 
> Asterisk makes no distinction between variable names that are preceded with an underscore and those that are not. In the following example, a variable with multilevel inheritance (`"__CAKE"`) is rendered uninheritable by the subsequent entry:
> 
> > ![image](images/00089.jpg)
> 
> In this example, the variable `CAKE` will be inherited by any and all spawned channels:
> 
> > exten => 1234,1,Set(__CAKE="Sponge cake")

When calling an inherited variable, it doesn’t matter if it is called with a prefix or not. These entries will give the same output in the CLI:

> ![image](images/00090.jpg)

#### 5.2.6 System Channel Variables

The following list describes the more important system channel variables. These variables may be read but not overwritten by entries in `extensions.conf`, as they are predefined by Asterisk. You can find a complete list of all the predefined variables in `doc/README.variables` (Asterisk 1.2) and `doc/channelvariables.txt` (Asterisk 1.4). Deprecated variables are not included in this list. For example, the variable `${CALLERIDNUM}` (previously commonly used) is not in this list; it is preferable to use the Asterisk function `${CALLERID(num)}` instead.

> ### Tip
> 
> It is a good practice to replace dialplan code that depends on deprecated variables or functions with code that uses the recommended replacements. This will reduce the chance of an installation breaking when you upgrade Asterisk.

System variables relevant to specific Asterisk functions are covered again in their respective chapters.

Some of the “variables” described here are not really variables but in fact built-in *functions.* In practice, they often play a similar role, so they are listed here for convenience:

> • `${ANSWEREDTIME}`

> The total elapsed time for the active connection (in other words, the number of seconds since the conversation started)

> • `${BLINDTRANSFER}`

> The name of the channel on the other side of a blind transfer

> • `${CHANNEL}`

> Name of the current channel

> • `${CONTEXT}`

> Name of the current context

> • `${EPOCH}`

> Current UNIX time (total number of seconds elapsed since the beginning of the UNIX “epoch,” which began at midnight UTC, January 1, 1970)

> • `${EXTEN}`

> Currently dialed extension

> • `${ENV(`*`VARIABLENAME`*`)}`

> Environment variable *`VARIABLENAME`*

> • `${HANGUPCAUSE}`

> Cause of connection hang-up

> • `${INVALID_EXTEN}`

> Used in the `i` extension and contains the dialed extension

> • `${PRIORITY}`

> Current priority in the current extension

> • `${TRANSFER_CONTEXT}`

> Context of a transferred call

> • `${UNIQUEID}`

> The unique ID for the current connection

> • `${SYSTEMNAME}`

> The system name as defined by `systemname` in `/etc/asterisk/asterisk.conf`

#### 5.2.7 Manipulating Variables

Variables are most useful when we can change their contents at execution time. This gives us the flexibility to create complex and powerful behavior in our Asterisk system.

##### *5.2.7.1 Substrings*

In general, a string consists of a sequence of individual characters. The size of a string is determined by the number of characters contained in it. For example, the string `apple tree` has ten characters; we must include the space. Any string can be broken into substrings. For example, `apple`, `tree`, `app`, and `le tre` are all valid substrings of `apple tree`. In theory, a string can be of any length; this entire book could be contained in a single string, although it would be impractical. Manipulation of strings is an important technique in programming applications. Asterisk lets you manipulate strings and substrings using the colon (:) character. Using the colon character, you can extract a specified portion of an existing string variable:

> ${*VARIABLENAME*[:start[:length]]}

###### 5.2.7.1.1 Examples

Many telephone systems require that a prefix digit be dialed to get an outside line. (In North America, this is usually 9.) The target number, however, cannot include this prefix digit. If we dial 9-1-202-7075000, we can store the actual outside number in the `${OUTGOINGNUMBER}` using the following dialplan entry.^([1](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos269065))

[1](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos268959). For our curious readers, this is the general information number for the Library of Congress in Washington, D.C.

> exten => _0X.,1,Set(OUTGOINGNUMBER=${EXTEN:1})

If the *length* option is omitted, the rest of the string is taken automatically.

What if we only need the last seven digits of the dialed number? I this case, we use a negative number for the start parameter. The following entry would store 7075000 from our preceding example in the variable `${LOCALNUMBER}`.

> ### Note
> 
> Under the original rules of the NANP (North American Numbering Plan) the last seven digits of a number constituted the local portion of the number. That is, if your telephone number was in the same area code as the dialed number, you needed to dial only seven digits. To accommodate population growth and density, the NANP has been extended with *overlay dialplans.* In areas with overlay plans, two telephone lines on the same street, or even in the same building, may have different area codes. You are in an overlay area if you are required to dial ten digits for local calls. In this case, a local number filter as depicted above will not be appropriate. Also, many area codes covering larger areas still have portions of the number space that are treated as long distance.

> exten => _0X.,1,Set(LOCALNUMBER=${EXTEN:-7})

We can also capture just the area code:

> exten => _0X.,1,Set(AREACODE=${EXTEN:2:3})

> ### Note
> 
> Obviously, readers in other parts of the world (e.g., the United Kingdom, Australia, or elsewhere) will have different national dialplans that impact how outside numbers should be processed. Some countries have area and city codes that are variable in length; in those cases, this kind of number filtering will not be practical.

Here, then, is how we might extract useful information from a dialed number:

> ![image](images/00091.jpg)

### 5.3 Special Extensions

Because all the programming logic must occur via extensions, we need some additional system-defined extensions.

#### 5.3.1 The h Extension

The `h` is the standard “hang-up” extension. The `h` extension, if it is configured, is called when a caller hangs up the phone. Note that as soon as this happens, the content of `${EXTEN}` changes to `h`.

Suppose we want the global variable `CONNECTIONS` to reflect the number of currently active conversations at any given time. This means we need the value of `CONNECTIONS` to increase by one every time a connection is initiated and decrease by one every time someone hangs up. The following dialplan illustrates the basic idea:

> ![image](images/00092.jpg)

#### 5.3.2 The i Extension

To make a context gracefully handle every conceivable circumstance, we use the special extension `i` (which stands for invalid), which handles all dialed numbers that are not explicitly handled within the context. Again, as with the `h` extension, when the `i` extension is invoked, `${EXTEN}` will no longer contain the dialed number. To get the dialed number while in the `i` extension, use `${INVALID_EXTEN}`.

In our example business, Widgets, Inc. employees in department B can only dial extensions 100 to 199\. Callers dialing any other numbers hear this message: “I’m sorry. That is not a valid extension. Please try again.”

> ![image](images/00093.jpg)

#### 5.3.3 The o and a Extensions

If `operator=yes` is set in `voicemail.conf`, the call will be directed to the `o` extension (o is for operator, kids!) if the caller presses zero (0).

Pressing * (asterisk) will direct the call to the `a` extension (abort).

#### 5.3.4 The t and T Extensions

The `t` and `T` extensions are for handling timeouts in the context.

##### *5.3.4.1 t Extension*

If there is no input in an interactive voice response (IVR) menu within a certain time, the `t` extension is called.

> ![image](images/00094.jpg)

##### *5.3.4.2 T Extension*

The `T` extension is called after the absolute timeout has been exceeded. You can set this timeout value with `Set(TIMEOUT(absolute)=<`*`seconds`*`>)`.

> ### Warning
> 
> Be careful not to have any spaces before and after the equal sign (=) character.

The timer starts whenever the timeout value is set. (In other words, it does not automatically start with the connection; it must be started explicitly with the `Set()` command.) `Set(TIMEOUT(absolute)=0)` deactivates the absolute timeout. In the following example, the timeout is set to 120 seconds. If the call lasts longer than that, the `T` extension is called, which plays back a message that says “Thank you for calling” and hangs up:

> ![image](images/00095.jpg)

#### 5.3.5 The s Extension

The first entry in any extension is always the name or number dialed by the caller. When a call comes in from the public switched telephone network (PSTN), however, Asterisk doesn’t know what was dialed or whom the caller is trying to reach. For any scenario in which we cannot determine the number dialed, we use the `s` extension. In this example, the sound of monkeys is played back to calls that come in via the PSTN:

> ![image](images/00096.jpg)

> ### Warning
> 
> If you are using an ATA device (analog telephone adapter) you don’t need the `s` extension. You can configure the dialed number in the configuration interface (often a web interface) for the ATA.

### 5.4 Macros

A macro is a kind of subroutine. It can contain complex workflows but is called through a single entry. This reduces repetition in the dialplan and makes it cleaner and smaller. A simple example might look like this:

> ![image](images/00097.jpg)

This macro would be called like so:

> ![image](images/00098.jpg)

The effect is not quite so impressive with a two-line macro as it would be with a much longer macro, but the advantages of such an approach should be clear.

The use of macros tends to divide the Asterisk user community into two groups. One thinks that macros make the dialplan easier to understand, the other believes that they make the dialplan confusing. We encourage you to draw your own conclusions!

When defining macros, take care to note the following points:

> • When defining a macro, only one extension (the `s` extension) is allowed.

> • The original `${EXTEN}` and `${CONTEXT}` variables cannot be used inside a macro. We must use `${MACRO_EXTEN}` and `${MACRO_CONTEXT}` instead.

> • When calling a macro, additional comma- (,) or pipe-separated (|) arguments can be supplied. These arguments are called within the macro with `${ARGn}` (where `n` is a positive integer indicating which argument in the sequence).

> • A macro is defined in square brackets (`[macro-macroname]`) and is called with the `Macro()` application in an extension.

More information on macros may be found in [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029).”

> ### Tip
> 
> The application `MacroExclusive()` ensures that the specific macro can only be called once at any given time. If another channel is calling the macro, no other channel can call it until it completes (see [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)).

### 5.5 Deprecated Features

For a long time, priority jumping was a standard way of moving a call about the dialplan. Specific applications (e.g., `Dial()`) would elevate the priority by 101 under certain circumstances. This feature is now officially deprecated. Basically, this means that although it is currently still supported, eventually it *will* be removed. Those who continue to use it are making their dialplans vulnerable to failure after an upgrade.

When working with Asterisk, you will encounter dialplan configuration examples on the Internet. (It is not uncommon to stumble upon grossly outdated examples that use deprecated constructs.) In professional practice, you should use the most current code constructions and versions of Asterisk. The software is always being updated, but deprecated features are not maintained.

In summary, if you want the operation of your Asterisk systems to be as predictable as possible, keep your code current!

## 6\. Asterisk Extension Language

As of version 1.4, Asterisk offers two ways of composing the dialplan: the traditional `extensions.conf` format, and the newer AEL, or Asterisk Extension Language, which uses the filename `extensions.ael`.

AEL will be of particular interest to those Asterisk users who find large `extensions.conf` files difficult to read. AEL looks more like a real scripting language. They are not mutually exclusive, either. It’s possible to use both, defining contexts in one or the other file. If both files are present, `extensions.conf` will just overwrite identical portions of `extensions.ael` when the dialplan is loaded.

Asterisk comes packaged with a command-line utility for converting AEL files into the traditional `extensions.conf` format called `aelparse`.

> ### Note
> 
> When referring to AEL, we mean AEL2\. The first version was experimental.

### 6.1 CLI Commands for AEL

The most important Asterisk CLI command for AEL is **`ael reload`**. It reads `extensions.ael` into memory and is useful if you’ve made changes to `extensions.ael` and want to apply them without restarting Asterisk.

> *CLI> **ael reload**

The **`dialplan show`** command displays the aggregate dialplan as loaded by Asterisk from `extensions.conf` and `extensions.ael`. The source of each dialplan rule is displayed in a line, in square brackets, preceding the rule. For rules originating from `extensions.conf`, the line looks like this:

> [ Context 'office-incoming' created by 'pbx_config' ]

For rules originating from `extensions.ael`, the line looks like this:

> [ Context 'queues' created by 'pbx_ael' ]

### 6.2 aelparse

Asterisk versions as of 1.4 come packaged with the command-line utility `aelparse`. You can use this utility to quickly convert `extensions.ael` files into `extensions.conf` format, should that ever be necessary. Programmers may think of it as a kind of test compiler for AEL, a somewhat higher-level “language” than that used in `extensions.conf`.

By default, `aelparse` reads `/etc/asterisk/extensions.ael` unless called with the option `-d`, in which case it looks for `extensions.ael` in the local directory. If it is invoked without option `-n`, it will spit out a lot of information that is mostly useful to the Asterisk developers. Use `-n` for more concise output, or `-q` for output that shows only warnings and errors.

> ### Tip
> 
> `aelparse` is useful for hunting syntax errors in `extensions.ael`.

With option `-w`, `aelparse` dumps the output into the file `extensions.conf.aeldump` in the local directory:

> ![image](images/00099.jpg)

### 6.3 Comparing extensions.conf with extensions.ael

The following examples show you how AEL compares with the standard `extensions.conf`. In doing so, we’re assuming that you’re already comfortable with dialplan programming.

First, you’ll see right away that the formatting of extensions is different. The structure of `extensions.ael` is a lot more like a programming language. For example, the following two code blocks are functionally equivalent. We’ve made the equivalent portions bold to illustrate this.

Here’s a typical context, as it would be written in `extensions.conf`:

> ![image](images/00100.jpg)

The same result can be achieved in `extensions.ael` with this:

> ![image](images/00101.jpg)

#### 6.3.1 Line Termination

AEL commands must always end with the semicolon (;) character, because multiple commands may appear on a single line. For readability, however, most people put each command on a separate line.

#### 6.3.2 Contexts, Extensions, and Priorities

The description of contexts, extensions, and priorities is what makes AEL different from its predecessor. AEL uses curly braces ({ ... }). Numbered priorities (`1, n`) are no longer required, and so we are spared the dubious charms of BASIC style programming in which every line must be numbered, as well as the tedious effort of writing the same extension number for every priority. In the simple examples that follow, the AEL versions often appear longer, but its advantages can really make themselves felt with large dialplans.

Here’s a simple set of extensions in `extensions.conf`:

> ![image](images/00102.jpg)

The same extensions would look like this in `extensions.ael`:

> ![image](images/00103.jpg)

For extensions that need only a single command, you can skip one level of curly braces and your dialplan would still work:

> ![image](images/00104.jpg)

Don’t get used to this practice, though. It’s best to include them always, even when they might be superfluous:

> ![image](images/00105.jpg)

Most extensions do require multiple commands and consistency is your friend when writing code. There are only a few cases where the short form is appropriate (for example, `jump`).

> ### Warning
> 
> The opening curly brace { of a code block must appear on the same line, not on a line of its own!

#### 6.3.3 Comments

In `extensions.conf`, comments are preceded by a semicolon:

> ![image](images/00106.jpg)

Comments in AEL are denoted with two forward slashes, //, `as` follows:

> ![image](images/00107.jpg)

> ### Warning
> 
> Programmers: Don’t use the C comment style (`/* ... */`). Every comment line must begin with its own // comment marker.

#### 6.3.4 Includes

We can include contexts within contexts. A typical use of includes in `extensions.conf` would look like this:

> ![image](images/00108.jpg)

Doing the same in AEL works this way:

> ![image](images/00109.jpg)

> ### Warning
> 
> Be careful to write `includes` and not `include` in AEL!

#### 6.3.5 Global Variables

In AEL, global variables are set in a special `globals` block.

![image](images/00110.jpg)

#### 6.3.6 Expressions and Variable Assignment

AEL handles expressions in control structures (such as `if()`, `while()`, the break condition in `for()` and the right side of variable assignments) as though they were contained in a `$[...]` expression.

This seems complicated at first glance, but this behavior is common in other languages. For variable assignments in Asterisk, it is atypical, however, and can easily lead to strange errors. (AEL isn’t a full programming language yet!) For this reason, we recommend against writing variable assignments this way:

> ![image](images/00111.jpg)

For predictable results, it’s better to use `Set()`, as you might in `extensions.conf`:

> ![image](images/00112.jpg)

For constructions which use `if()`, `while()`, and so forth, however, the new behavior is nevertheless desirable because it spares having to use the clunky `$[ ... ]`. In `extensions.conf`, we would use `ExecIf()`:

> ![image](images/00113.jpg)

In `extensions.ael`, the end result is cleaner:

> ![image](images/00114.jpg)

#### 6.3.7 Labels, goto, and jump

The hardened `extensions.conf` programmer is forced to get used to moving around dialplan by jumping to priorities or predefined labels using applications such as `Goto()`, `GotoIf()`, `Gosub()`, and `GosubIf()`:

> ![image](images/00115.jpg)

In AEL, a label always appears inside an extension and on its own line. Don’t forget the colon (:) at the end of the line:

> ![image](images/00116.jpg)

In the preceding example we see a different syntax for the “goto” construction. In `extensions.conf`, we had to use the `Goto()` application, but in AEL, it’s been replaced by the command `goto`. (If you really want to keep using `Goto()`, you can, but why?)

A comparison of the syntax for `Goto()` and `goto` shows us they are functionally the same:

![image](images/00117.jpg)

The concept of jumping to a specific priority is moot in AEL because priorities aren’t used; still, you might have a need to jump to another extension, be it in the same or another context. For this purpose, AEL includes the additional command `jump`.

![image](images/00118.jpg)

In the following sections, you’ll see that AEL doesn’t really need to rely on goto statements for control flow, because it has real control structures.

#### 6.3.8 Conditionals

Conditionals are structures that let you control program execution.

AEL has both **`if`** and **`switch`** commands. This is a big advantage because it makes an AEL dialplan much more readable. The more complex your program logic, the more obvious this advantage becomes.

##### *6.3.8.1 if*

In `extensions.conf`, we have to label targets explicitly:

> ![image](images/00119.jpg)

In `extensions.ael`, the **`if`** statement has fewer parentheses:

> ![image](images/00120.jpg)

Someone used to programming in AEL will find jumping around a dialplan with `GotoIf()` cumbersome, to say nothing of the confusion caused by a statement like `GotoIf($["${DIALSTATUS}" = "BUSY"]?b:n)`. Are all the brackets closed?

> ### Warning
> 
> Again, the opening curly brace must stand on the same line as the `if` statement, not on its own line.

##### *6.3.8.2 switch*

In AEL, the **`switch`** command lets you easily build code that can handle more than one case. In `extensions.conf`, a construction which does the same thing as a **`switch`** command is a confusing mess:

> ![image](images/00121.jpg)

In `extensions.ael`, by contrast, the result is clean and elegant:

> ![image](images/00122.jpg)

Trying to do a *nested* `if` or `switch` in `extensions.conf` would be incomprehensible and impossible to maintain. Now we can really start to see the advantages of AEL!

> ### Warning
> 
> Don’t forget the `break` statements in the `case` branches! If you omit these, Asterisk will just run them sequentially, be it to the next case branch or to `default`.

In addition to case comparison, `switch` also lets you use `pattern` statements to do explicit pattern matching. Here’s what pattern matching looks like in our `extensions.conf`:

> ![image](images/00123.jpg)

In `extensions.ael`, the pattern syntax is the same, but it is preceded by a `pattern` statement and treated just like a case:

> ![image](images/00124.jpg)

##### *6.3.8.3 ifTime*

The standard application `GotoIfTime()` (see [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)”) is replaced with the `ifTime` command in AEL:

> ![image](images/00125.jpg)

The time syntax is the same as for `GotoIfTime()`. You can accomplish the same thing with the `IFTIME()` function (see [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), “[Dialplan Functions](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249)”), although the result is not as readable:

> ![image](images/00126.jpg)

##### *6.3.8.4 random*

The `random(){...}` command takes a value from 1 to 99\. This value is the percentage chance that the subsequent code block will be executed:

> ![image](images/00127.jpg)

You can accomplish the same objective with an `if` command and the `RAND()` function with slightly more code:

> ![image](images/00128.jpg)

#### 6.3.9 Loops

Like conditionals, loops are control structures.

AEL has classic **`for`** and **`while`** loops, which behave just as they do in other programming languages.

##### *6.3.9.1 while*

A `while` command in AEL is used in much the same way as the `While()` and `EndWhile()` applications.

The `break` and `continue` statements found in some other languages can also be used in AEL loops. This corresponds to the `ExitWhile()` and `ContinueWhile()` in `extensions.conf`:

> ![image](images/00129.jpg)

In `extensions.ael`, the `break` statement jumps to the end of the loop block, `continue` to the start. In this example, we use `break`:

> ![image](images/00130.jpg)

> ### Note
> 
> In this example, we needed more lines in AEL; if we had added another command to the `if` condition in our `while` loop, `ExecIf()` would not be enough anymore and we would be forced to use a more complex construction with `GotoIf()`. Our `extensions.conf` would be a lot longer.

##### *6.3.9.2 for*

AEL also gives us `for` loops. This has no corresponding application in the `extensions.conf` format, though every `for` loop may be written as a `while` loop:

> ![image](images/00131.jpg)

Even here, `extensions.ael` is more compact:

> ![image](images/00132.jpg)

#### 6.3.10 Macros

In `extensions.conf`, macros or macro-like functions can be achieved with `Macro()` or `Gosub()`. Our example uses `Macro()`:

> ![image](images/00133.jpg)

In AEL, we don’t have to choose. It has the `macro` command:

> ![image](images/00134.jpg)

The AEL compiler converts `macro` into a `Gosub()` subroutine internally; fortunately, it’s not one we have to maintain.

#### 6.3.11 Hints

We cover the implementation of hints in AEL in depth in [Chapter 18](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos635590), “[Busy Lamp Field, Hints, Pickup](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos635590).” Here’s a simple example to demonstrate the proper syntax. In `extensions.conf`, hints look like this:

> ![image](images/00135.jpg)

In AEL, the hint can encapsulate a reference to the device:

> ![image](images/00136.jpg)

Here is a similar example, this time using a pattern. In `extensions.conf`, that would look like this:

> ![image](images/00137.jpg)

In `extensions.ael`, it would look like this:

> ![image](images/00138.jpg)

Notice that the pattern is now outside the hint parentheses.

#### 6.3.12 Filtering by Caller ID

In `extensions.conf`, the ever-popular ex-girlfriend extension looks like this:

> ![image](images/00139.jpg)

The AEL syntax that accomplishes the same thing looks like this:

> ![image](images/00140.jpg)

If a call comes in from the ex-girlfriend (with the caller ID 6135303122), it is routed to `Busy()`. Everybody else gets connected to Dave’s phone.

Patterns are allowed here too. With `/_613`, you can match the entire area code.

### 6.4 Choosing between extensions.ael and extensions.conf

Asterisk application developers are left to decide which format is the right one. The development road map once hinted that AEL would replace `extensions.conf`, but since then Digium has been careful about declaring in favor of one over the other. One thing is certain: You cannot understand Asterisk well unless you understand `extensions.conf`, not least because the bulk of the documentation available on the Web is written for `extensions.conf`.

If you don’t spend a lot of time doing dialplan programming, you’re probably better off sticking with `extensions.conf`, at least for the foreseeable future. For application developers who work with Asterisk a lot, however, AEL has too many time- and headache-saving features to justify not trying it out. Even if Digium were to end support for AEL (which is highly unlikely), there is always `aelparse` to enable a return to the old `.conf` world.

## 7\. Protocols

This chapter covers the techniques by which we actually get voice data from one point to another. The session protocols for this purpose are really a kind of “grammar” that governs this transmission, and are in turn built upon the transport layer protocols that make up the TCP/IP protocol stack: namely TCP and UDP. You should have a fundamental understanding of these protocols when troubleshooting certain problems, which is why we are describing them in some detail here. This understanding is not strictly necessary to implement Asterisk, but is nevertheless valuable. As such, this chapter is intended as a reference for the event it is needed.

### 7.1 Network Protocols

TCP is a protocol that ensures that all the information transmitted by the sender arrives at the receiver complete and in the correct order. This reliability is at the cost of relatively higher transmission overhead, which, during times of congestion, is more likely to lead to interruptions or delays in transmission. By contrast, its sister protocol UDP invests almost nothing in ensuring that everything is received; instead, it merely sends out every packet as soon as it is ready to be delivered without regard to whether it arrives intact or even in the right sequence. TCP ensures a secure, complete transfer of data by calculating a checksum on each packet and comparing the checksums when the packet is received, as well as attaching a sequence number to each packet and asking for receipt confirmation from the destination host. The destination host can ask for a retransmit if a packet is corrupt or missing. This is how HTTP (World Wide Web) traffic is transmitted.

By contrast, streaming data (as used in video and audio transmission) doesn’t actually need this level of rigor because it is time sensitive. If a video packet is missed, there is no sense in retransmitting it because by the time it arrives, the video will have played on past the point of the missing data. For this reason, UDP is used for streaming data. There is no delivery guarantee, but the transport overhead is much less than in TCP. As a general guideline, you can define the two protocols this way: TCP is for “when it absolutely has to get there intact, no matter how long it takes” and UDP is for “when it has to get there fast and we don’t care if we lose a few packets.”

Both protocols are of importance in VoIP applications, because connections are established using TCP, whereas the voice data itself is transmitted using UDP. Particularly where audio data packets are concerned, quantity is indeed more important than quality.

#### 7.1.1 Transmission Control Protocol

The Transmission Control Protocol (TCP) is a protocol governing the transmission of data between computers. The operating systems of all modern computers understand and support TCP and use it to exchange data with other computers on a network. It is a reliable, connection-oriented transport protocol, and forms part of the Internet Protocol family.

TCP was developed by Robert E. Kahn and Vinton G. Cerf, beginning initially as a research project in 1973 and culminating in the publication, in 1981, of the Internet standards document RFC^([1](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos321058)) 793, which forms the basis for all the TCP standards documents which followed, and, like many of its companion protocols, remains a “living” protocol that is always being extended and updated, through new RFC documents, to meet new needs and circumstances.

[1](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos320683). Request For Comments. These documents begin as simple proposals addressed to peers in the Internet engineering community and subject to revision; when a draft proposal has been accepted it is annotated and becomes part of the body of standards.

TCP sets up a virtual connection between two endpoints in a network. Data may be transmitted in either direction. TCP is almost always encapsulated in IP (Internet Protocol); for this reason, you will often hear the term TCP/IP used. It allows bidirectional data transmission, no matter which endpoint originated the connection; it automatically detects and corrects data loss, and automatically adjusts the data transmission rate to accommodate network conditions. These features, along with the fact the standard is open, have made TCP the most widely used data transmission protocol, and today it is used for the World Wide Web, e-mail, peer-to-peer file sharing, and other popular network services.

##### *7.1.1.1 TCP Connections*

TCP is an end-to-end (circuit-like), full-duplex (meaning it allows the transmission of data in both directions at the same time) connection. Alternatively, connections may be assembled as two, half-duplex connections in which information may travel in both directions, albeit not at the same time; data may be returned for the purpose of connection management. Connection management itself is handled by the TCP protocol stack, software that is typically attached to, or forms part of, the core of the operating system. In the case of Linux, the TCP stack is in the kernel itself; this stack is accessed by network software such as e-mail clients, web browsers, and servers.

Each TCP connection consists of two endpoints, with each endpoint establishing a pair of identifying characteristics: namely, the unique IP address of the endpoint, and the port. This pair forms a software interface that allows bidirectional data transfer, and is sometimes called a socket. The computers participating in the connection are identified by their IP addresses, while the particular connection is identified by the port number. As a result, it is possible for a web server, for example, to have multiple connections to a remote endpoint from its port 80; it keeps track of these multiple connections because each connection uses a different port on the remote endpoint.

Ports are 16-bit numbers, and so range from 0 to 65535\. The ports from 0 to 1023 are reserved and assigned by Internet Assigned Numbers Authority (IANA) for specific applications. For example, web traffic, which uses HTTP, travels over the port reserved for HTTP traffic, port 80\. The use of particular ports is not binding; an administrator may operate an FTP server on a port other than 21\. For publicly accessible services, however, client software will expect to find its specific service on the IANA-specified port, and special, private services are usually operated on unassigned ports above 1024.

##### *7.1.1.2 Connection Setup and Teardown*

A web server publishing a service to the outside world sets up a socket consisting of its IP address and a port, and waits for clients to initiate connections to this socket. A socket in this state is said to be listening, and indeed a display of the active sockets (typically through a command such as **`netstat -an`**) will show some in the LISTEN state. If a client wants to connect, it sets up a socket of its own with its IP address and a randomly selected, unused port number, and uses this socket to connect to the listening socket on the server. When the connection is established, the roles of client and server are indistinguishable and basically symmetrical. Either side may terminate the connection. (When done gracefully, this is sometimes called teardown.) Data may still be transferred by the opposite endpoint while the connection is being torn down.

The three-way handshake is the manner by which two TCP endpoints establish and maintain a connection so as to minimize data loss.

The client initiating a connection sends the server a TCP SYN (synchronize, identified with the SYN flag bit set to 1) packet with a sequence number *x.* Sequence numbers are used to set the correct order for packets, ensure that no packets are missing, and check for duplicates when the packet stream is reassembled at the server.

The type of packet (SYN) and the sequence number are set in the TCP header and the sequence number is selected randomly (how this is done depends on the TCP implementation). The server replies with a SYN/ACK (synchronize-acknowledge, identified with both SYN and ACK flags set to 1) packet having a (similarly randomly selected) sequence number *y.* At the same time, it increments the sequence number of the initiating SYN packet by one (*x* + 1) and places this number in the acknowledgment field of the packet’s TCP header.

Finally, the client completes the handshake by replying to the SYN/ACK with an ACK packet of its own, incrementing the sequence number by one (*y* + 1). This process is also called forward acknowledgment. For extra security, the client also wraps the received *x* + 1 sequence number in this ACK reply. If all goes well, the connection is established.

Graceful teardown follows a similar process. Instead of packets with SYN flag bits set, the FIN (finish) flag bit is set. This indicates to the receiver that the sender will not be transmitting any further data. This is acknowledged with an ACK packet. The recipient of the initial FIN packet then responds with an ACK packet of its own, which is likewise acknowledged. Although four packets are exchanged, this is still treated as a three-way handshake because the FIN-ACK combination from the server to the client is considered a “one-way” operation. (The FIN and ACK message can also be contained in a single packet.)

The maximum segment lifetime (MSL) is the maximum time that a TCP segment may exist in the network before it is discarded (normally 2 minutes). After the transmission of the last ACK, the client enters a wait state equal to two MSL periods; during this time, all late-arriving segments are discarded. This is to ensure that no late-arriving segments are misinterpreted as the initiation of new connections. This also ensures that the connection is indeed closed gracefully; if the ACK *y* + 1 goes missing, a wait timer on the server expires and the LAST_ACK segment is retransmitted.

##### *7.1.1.3 TCP Header Structure*

A TCP segment consists of two parts: the header, containing the transmission information such as port and sequence number; and the payload, which is the real information we want to send (see [Figure 7.1](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos329170)), which usually includes application layer protocol information (such as HTTP or SSH). The values are transmitted in network (big endian) byte order.

**Figure 7.1** TCP header structure.

![image](images/00141.jpg)

##### *7.1.1.4 Data Transmission*

A TCP segment is typically no larger than 1,500 bytes. It must be small enough to fit in the protocol data unit^([2](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos330465)) of the protocol layer immediately beneath it in the stack, in this case, IP. An IP packet may be as large as 64 kilobytes, but because IP is practically always transmitted over Ethernet, most IP packets are smaller than the maximum Ethernet frame size of 1,500 bytes. Both TCP and IP specify a header of 20 bytes, respectively, so the payload is limited to 1,460 bytes. Some connections (particularly some forms of DSL service) use PPP (Point-to-Point Protocol), which requires an additional 8 bytes of header information, meaning that the TCP/IP packet can be a maximum of 1,492 bytes, leaving a maximum segment size (or MSS) of 1,452 bytes. This corresponds to about 3.2% overhead.

[2](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos329675). *Protocol data unit* is a term used to refer to the unit of transmission corresponding to a given network layer. In the session layer, the PDU is called a segment (TCP segment); in the network layer, it is a packet (IP packet); in the link layer, it is a frame (Ethernet frame).

The sender and receiver negotiate the maximum segment size before data transmission begins, using the options field in the TCP header. The application wanting to send data (for example, a web server) places a data block of 10 kilobytes in the transmit buffer. To send this 10kB data block, it is divided into multiple packets, each with its own TCP header, and transmitted as TCP segments, a process called segmentation.

Segments usually leave in sequential order, though this is not strictly necessary, because the sequence numbering allows the receiver to reassemble them in the correct order. Received segments are checked for integrity by calculating a checksum. If it is correct, the packet is acknowledged. If it is incorrect, the acknowledgment is withheld and the sender retransmits the packet.

##### *7.1.1.5 Data Integrity and Reliability*

TCP allows a bidirectional, byte-oriented, reliable data stream between two endpoints. The underlying network layer protocol (IP) is packet switched, and packets can get lost, mangled, or arrive in the wrong order. TCP was designed to deal with these inherent uncertainties, and so it verifies data integrity using a checksum provided in the packet header, establishes the correct packet order using sequence numbers, and discards duplicate packets. The sender retransmits packets that are not acknowledged within a certain time. The received packets are assembled in the correct order in the receive buffer to form a data stream which is passed to the appropriate application.

Of course, the data transfer can be interrupted, corrupted, or terminated at any time. The connection will expire after a timeout has been exceeded. The successful establishment of a connection does not guarantee that a lasting and reliable transfer will follow. Network speed and stability may be sufficient for negotiating the connection while being insufficient to sustain it. Network conditions can also change such that they cause a working connection to fail.

#### 7.1.2 User Datagram Protocol

In contrast to TCP, the User Datagram Protocol (UDP) is a minimal, connectionless session layer protocol. Development of UDP began in 1977, after the limits of TCP for the transmission of time-sensitive data became apparent. A protocol that handled only addressing was needed, without the overhead that went with guaranteed delivery.

##### *7.1.2.1 Operation*

To ensure that data sent via UDP reaches the appropriate application, source and destination ports are specified in the UDP header. This process-to-process communication is called application *multiplexing* and *de-multiplexing* (sometimes muxing and demuxing).

##### *7.1.2.2 Characteristics*

UDP establishes a connectionless, potentially unreliable transfer service. This means that neither transmission nor order of reception is guaranteed; that is, UDP sends data on a “best effort” basis. Applications that use UDP must take these characteristics into account and implement data correction where it is appropriate and necessary. Because no connection setup is required prior to data transmission (as is the case with TCP), the endpoints can begin exchanging data more quickly. This relatively low overhead makes UDP particularly useful for applications that exchange only small amounts of data, such as Domain Name System (DNS).

In addition, the absence of handshaking means that there is less variation in latency, or jitter. If a packet is lost in a TCP transaction, precious time is needed while the recipient waits for the sender to retransmit it, and the momentary latency can increase dramatically. This is important for multimedia applications that are sensitive to delay. In Voice over IP (VoIP) applications, these kinds of delays lead to sound artifacts and dropouts.

Connectionless protocols like UDP do not stop the flow of data if packets go missing. It is up to the receiving end to make sense of the gaps in the data stream when packets are lost, and most do this by momentarily reducing the resolution or quality of the resulting audio or video.

UDP, like TCP, is constrained by the protocol data unit size of the underlying network stack layers. IP packets cannot be larger than 65,535 bytes, of which the IP and UDP headers consume at least 28 bytes, leaving a maximum of 65,507 bytes for the actual payload. Such datagrams are usually fragmented in IP. In practice, UDP packets are rarely more than a few kilobytes in size. IP will discard packets in the case of transmission error or overflow, so datagrams can go missing.

### 7.2 Channels

In Asterisk, a channel is the connection between two endpoints (usually human beings in conversation). The following channel types exist:

> • **Agent**

> An automatic call distribution (ACD) agent channel

> • **CAPI**

> An ISDN channel

> • **Console**

> A Linux console channel driver for sound cards that can be manipulated through OSS and ALSA

> • **H.323**

> A VoIP protocol

> • **IAX**

> A VoIP protocol

> ### Note
> 
> In principle, there are two versions of IAX (1 and 2). Today, anyone referring to IAX is almost certainly speaking about IAX2 (in other words, IAX version 2). IAX version 1 has been deprecated and is no longer used.

> • **Local**

> A loopback into another context

> • **MGCP**

> A VoIP protocol

> • **mISDN**

> An ISDN channel

> • **NBS**

> Network Broadcast Sound

> • **phone**

> Linux Telephony channel

> • **SIP**

> A VoIP protocol

> • **Skinny**

> A VoIP protocol (also called SCCP, or Skinny Client Control Protocol)

> • **vISDN**

> An ISDN channel

> • **VOFR**

> Voice over frame relay Adtran style

> • **VPB**

> Voicetronix hardware channel driver for PSTN connections

> • **Zap**

> Digium hardware channel driver for PSTN connections; also used for hardware from competing manufacturers

Most examples in this book assume SIP connections. The reason for this is simple: At the moment, there are more SIP-capable VoIP telephones than telephones for any other VoIP protocol. The other significant VoIP protocol for Asterisk is IAX. This chapter covers these two important protocols in some further detail, but may also be used as parameter reference for configuration.

### 7.3 Peers, Users, and Friends

When you configure IP connections in Asterisk, you will have to specify whether the connected device is a peer, user, or friend. The distinction between the classifications is not always clear in the Asterisk documentation.

Simply put, the classifications work like this. Asterisk...

> • *Accepts calls from* a user

> • *Makes calls to* a peer

> • *Makes calls to* and *accepts calls from* a friend

In practice, friend is used the most.

### 7.4 IAX Versus SIP

Every Asterisk administrator is eventually faced with the question of whether to build primarily on SIP or IAX. Although the dispute over protocol has a religious tone at times, we think that from a purely technical standpoint, IAX is, in certain important respects, at least slightly superior to SIP. In many installations, IAX will mean many fewer implementation problems than one would expect with SIP. The primary reason for this is the way that SIP handles Network Address Translation (NAT). SIP connections are problematic because they require the opening of an entire range of ports in the firewall to work. The ability of IAX to multiplex conversations over a single connection (IAX trunk) is also more efficient because it reduces overhead. SIP, by contrast, establishes a separate connection for each conversation.

If IAX is available and possible (that is, the sets support it), IAX should be used; otherwise, you should use SIP.

Mark Spencer, the inventor of Asterisk, wrote an e-mail to the Asterisk users mailing list in 2004 that attempts to address the question ([Figure 7.2](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos344119)).

**Figure 7.2** Mark Spencer’s e-mail on IAX.

![image](images/00142.jpg)

![image](images/00143.jpg)

In the intervening years, IAX has itself become a well-documented and open protocol. IAX 2 was accepted as informational (nonstandards track) RFC 5456 in February 2009.

## 8\. Making Connections

Asterisk finds its real power when you connect it to other systems, telephone devices, and networks. It accomplishes this through audio codecs and a variety of transport media, such as digital trunks (T1, E1) and traditional analog lines. In this chapter, we look more closely at codecs, ISDN, and analog telephony.

### 8.1 Codecs

A discussion of codecs, as they are used in telephony, will put someone on one of two sides of a large mountain. On one side of the mountain, we have the situation in North America, which has very little ISDN penetration, at least at the retail level. The average North American telephone customer has only ever used analog telephones, and so the stack of digital codecs is seen from the base of a mountain yet to be scaled: At the summit is an appealing array of digital codecs that offer exceptional sound quality, but represent the unknown.

On the other side of the mountain, we have the situation in Europe, where ISDN has been ubiquitous for so long that analog seems like the dark ages and nobody thinks twice about codecs or call quality. The average European telephone customer under the age of 35 has only ever used digital telephones, and so the stack of digital codecs is seen from a mountain she has already been to: The summit was nice, we took some pictures, now let’s make phone calls.

In either case, the codecs are far from the surface of anyone’s consciousness. Nevertheless, choice of codecs has implications for Asterisk implementation. Whether you are in North America, Europe, or elsewhere in the world, you will still be faced with this choice.

As a general guideline, the most common digital codec used in telephony is the ISDN codec G.711 (a-law or u-law companding; u-law^([1](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos347169)) is used in the United States and Japan, while a-law is the standard in Europe).

[1](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos346983). Actually, this is μ-law (the Greek letter mu, used in physics as a prefix meaning “micro”).

The limited use of digital telephony in the United States is at least part of the reason why Voice over IP (VoIP) has caught on much more than in Europe. The sound quality offered by a clean, IP-based connection is often vastly superior to that of the aging analog infrastructure.

#### 8.1.1 What Does a Codec Do?

Simply put, a codec takes an analog audio signal and converts it into a digital bitstream. This consists of a series of steps. First, the signal is digitized into a time-coded bitstream, and then this bitstream is compressed using a compression algorithm so that it uses less bandwidth when transmitted. This compression can be nearly lossless (e.g., G.711) or lossy (e.g., GSM). Without a codec, no audio can be transmitted. Which codec one ought to choose depends on the bandwidth available and the available processing capacity. Use of any codec is always a compromise between these two considerations.

This chapter does not cover the function of codecs in too much detail. For our purposes, an overview will suffice.

#### 8.1.2 Performance

The biggest problem with high-compression codecs is the processing they require. Using the Asterisk console, enter the command **`core show translation`** to see a table of the actual transcoding times required for the various codecs:

![image](images/00144.jpg)

![image](images/00145.jpg)

Codecs not available on your system are marked with a dash (-). It is easy to see which codec demands the most processing resources: `speex`.

To minimize load, use the minimum possible number of codecs. If set A and set B both use the same codec in a call to each other, Asterisk need only pass through the packets. If set A and set B use different codecs, Asterisk has to transcode each packet, which involves decoding the incoming packet and then encoding it using the other codec before sending it out to the destination set, and it has to do this in *each direction.* You can see how this becomes onerous quickly.

#### 8.1.3 Configuring Codecs

How codecs are configured depends on the technology. IAX sets are configured in `iax.conf`, and SIP sets are configured in `sip.conf`. If you want to set all SIP sets to use G.711, you would write the following in `sip.conf`:

> ![image](images/00146.jpg)

If you have a specific telephone (call it 2000) that should use only GSM, you can set this as follows:

> ![image](images/00147.jpg)

#### 8.1.4 Commonly Used Codecs

The CLI command **`core show translation`**, which displays the table shown earlier, will show you which codecs are available on your system (namely, all those with numbers in their respective columns). The following list briefly examines the most commonly used codecs in Asterisk:

> • **GSM**

> An Asterisk “classic” and familiar to anyone with GSM mobile phone service. The bandwidth is 13.3kbps, and the quality is acceptable, if not exactly overwhelming.

> • **iLBC**

> iLBC is a sort of secret weapon for use in low-bandwidth situations. The sound quality is excellent, and the bandwidth is limited to between 13.3kbps and 15kbps (depending on frame size). Skype uses a variant of this codec. The problem with iLBC is that it is processor intensive; that is also why it is not implemented in very many hardphones.

> • **G.711**

> Another classic, from the suite of ISDN codecs. This codec offers superb sound quality and requires 64kbps of bandwidth. This is standard for most calls traveling in corporate intranets and is also widely used for calls over the public Internet.

> • **G.722**

> The chances are good that G.722 will eventually replace G.711; at the highest resolution, it offers a much better sound quality than G.711, but while requiring the same bandwidth (only 64kbps). Unfortunately, it not, as yet, supported by many telephones.

> • **G.726**

> Offers the same sound quality as G.711 while needing only half the bandwidth (32kbps). In contrast to G.711, only the data that has changed relative to the previous voice packet is transmitted (similar to the way MPEG video works). The result is the same information transmitted with half the bandwidth. G.726 is not too burdensome, but still requires more processing than G.711.

> • **G.729a**

> G.729a is a patented codec that needs only 8kbps and offers sound quality comparable to GSM. Licenses for Asterisk can be purchased from Digium ([www.digium.com](http://www.digium.com)). It is not exceptional either in voice quality or performance, but offers a fair balance and is implemented in many VoIP telephones. As such, it is a good option when you need to conserve bandwidth.

> • **G.729.1**

> G.729.1 is an extension offering bitstream interoperability with existing G.729 codecs, as well as a high level of configurability (it supports 8kpbs to 32kbps streams). Of particular interest are the wide-band extensions, which can offer very close to CD-quality sound; as yet, only a few phones support them. To use the wideband extensions, all the devices in the media path must support them.

#### 8.1.5 Bandwidth and Trunking

Anyone wanting to pass multiple simultaneous calls over a network connection (e.g., when two Asterisk systems are connected to each other) will soon have a bandwidth problem. Depending on the constellation of codec and frame size, it is easily possible for the IP overhead to exceed the payload. For example, using SIP and GSM on a 2Mbps data connection, you can support a maximum of 35 simultaneous calls, which isn’t exactly a lot. In such a case, you would be better served by an ISDN PRI, where the sound quality will be significantly better.

Trunking is great because it lets you wrap multiple voice chunks in a single connection, so that you are not incurring an overhead penalty for each call. In our example above using the same 2Mbps connection, we can support 77 simultaneous GSM calls. If we want to improve the sound quality, we can do this and still support 44 G.726 calls.

Trunking is supported only in IAX2 (see [Chapter 7](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos316821), “[Protocols](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos316821)”) and should only be used with at least two simultaneous calls, because the overhead for a single call would be measurably higher than without trunking.

If you want to assess your bandwidth requirements more closely, see the bandwidth calculator at [www.asteriskguru.com/tools/bandwidth_calculator.php](http://www.asteriskguru.com/tools/bandwidth_calculator.php) and try out various scenarios.

### 8.2 Integrated Services Digital Network

ISDN is a twisted-pair, digital multiplexing standard for PSTN and data applications. Although used widely around the world, it is not well known in North America. For most data applications, ISDN has been displaced by ADSL, coaxial cable, and FTTH (fiber-to-the-home) technologies, which offer much larger bandwidth at competitive rates. It remains in use for voice and video applications. We’ll look at those here.

ISDN itself is a giant topic, and because it is an older technology, it is well covered in other texts. Do not expect much depth here. We discuss ISDN only in the context of its relevance to Asterisk.

#### 8.2.1 ISDN Basics

An ISDN connection provides two basic channel types: B and D. (More specialized channel types exist but are not in wide use, and are not covered here.) A single B (bearer) channel can be equated, roughly, with a single analog telephone line: You can carry on one conversation on that channel. Where it differs is that a single physical line pair can carry multiple B channels, making better use of the existing wiring. The data is transported in digital and not analog format, which means you can’t connect an analog telephone to the line and expect to hear anything. The digital transport usually delivers better sound quality when everything is properly configured.

The D (data) channel carries signaling information about the B channels on the circuit.

The differences between the B and D channels are as follows:

> • The B channel is, for our purposes, a voice channel. (In a non-Asterisk installation, it could carry data.) A B channel provides 64kbps of bandwidth.

> • The D channel is data only, but is dedicated for signaling purposes. Depending on the interface type, the D channel can be 16kbps or 64kbps. The ISDN device—be it a telephone, PBX, or interface card—uses the D channel for call setup and teardown.

The following sections cover the two major types of ISDN connection: the basic rate interface and primary rate interface.

##### *8.2.1.1 ISDN Basic Rate Interface*

The entry-level ISDN service is called basic rate interface, or BRI, and is used in homes (in the world outside of North America) and small businesses. It provides two 64kbps B channels and one 16kbps D channel (which is why some refer to it as 2B+D) over a single line pair (two wires). You can attach ISDN phones, BRI ports on PBX devices, ISDN-BRI terminal adapters (which provide FXS ports for analog telephones), or ISDN-BRI adapter cards to a BRI.

To install and use BRI, you need to know what signaling type the carrier expects. There are two types:

> • **2B1Q**

> This (2 binary, 1 quaternary) is the signaling type used in North America. It is a linear coding type that supports a loop length of up to 5,500 meters (about 18,000 feet).

> • **4B3T**

> This (4 binary, 3 ternary) is the signaling type used in the rest of the world, including Europe. It is a block coding type that supports a loop length of up to 4,200 meters (about 13,700 feet).

##### *8.2.1.2 BRI in the United States*

ISDN never really caught on at the subscriber level in North America. Although there are many opinions why, the most common explanation given is that the size of the existing network made implementing ISDN to the suburbs prohibitively expensive. In North America, average loop lengths are much longer when compared to Europe, where ISDN circuits now make up more than 80% of installations.

Still, sometimes BRI makes sense, and in most jurisdictions it is a tariffed service, which means that some carrier (usually the incumbent telephone company) must provide it if it is technically feasible. Here are some reasons why you might consider BRI:

> • You are faxing and your analog lines are poor quality.

> Faxing does not work well over IP (see [Chapter 17](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos611843), “[Fax Server](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos611843)”). Analog is an option, but if your analog lines are noisy, you should consider BRI.

> • You need the sound quality and call-signaling features that only ISDN provides, but don’t need enough channels to justify PRI.

> Features such as Explicit Call Transfer, DNIS (Dialed Number Identification Service), and COLP (COnnected Line identification Presentation) are ISDN services that can’t easily be replicated on analog lines. If you need these but don’t need more than six to ten channels, BRI is a real option. One thing is beyond dispute: In the circuit-switched, PSTN world, ISDN offers unparalleled sound quality.

Of course, the economics will vary depending on your location and the carrier. Be warned that most carriers that offer BRI don’t actively market it, so you may face challenges in getting anyone in the sales department to acknowledge that the service exists.

##### *8.2.1.3 ISDN Primary Rate Interface*

You can think of the PRI as the bigger, flashier brother of the BRI. In North America, PRI is provided over a T1 (23 B channels, 1 64kbps D channel) with 2 or 3 pairs (4 or 6 wires); in Europe, the E1 (30 B channels, 1 64kbps D channel). Again, you can only connect ISDN devices to a PRI circuit. Examples include the PRI interface on a PBX, a channel bank (which provides FXS ports for analog telephones), or an ISDN-PRI interface card. The PRI is intended for larger installations.

Nothing says a PRI must use all 24 channels. Some carriers provide partial PRI service (usually ten channels), sometimes at considerable cost savings.

PRI always implies ISDN. PRI service is supplied via a T1, but not all T1 circuits are PRI. Non-ISDN T1 circuits (also called in-band T1) can still be found in North America. In such circuits, call setup and teardown signaling is sent in the channel (CAS, or channel associated signaling) instead of via a separate D channel. This steals some bandwidth from each channel but makes all 24 channels available.

For voice applications, PRI is on its way to replacing non-PRI T1 connections completely. Its broad support and extremely fast signaling make it the easy choice.

#### 8.2.2 Choosing an ISDN Card

This is a difficult question, and the answer depends on your specific circumstances and requirements. Here are some things you need to consider:

> • A card that’s excellent today may be mediocre tomorrow, particularly when compared with newer product in the marketplace.

> • Card performance can depend heavily on the driver software, which can change over time.

> • Support quality is subjective.

> • Performance requirements will depend on the intended use. Some products that would not be a good choice for the business market may be perfectly acceptable for the residential market.

Actually *using* an ISDN card in an Asterisk server is really quite simple, even if installation and configuration aren’t always trivial. There are a few different ways to get an ISDN card running with Asterisk. We touch on a few variations below.

> ### Important
> 
> All the installation examples in this book use a Debian Linux system. The installation procedure will differ on other Linux systems and may not work at all on BSD systems. If you are starting out, we recommend you follow the instructions completely and begin with a fresh Debian installation.

##### *8.2.2.1 Determining Your Quality Needs*

Most private Asterisk users are not hung up on sound quality and availability. Cost is likely the primary consideration here. If you aren’t planning to fax over the card, and you only need two B channels, any generic HFC-based BRI card will do. The cards are cheap and widely available. You’ve been warned, however: Installation can be challenging with these cards, and you shouldn’t expect amazing sound quality. If you can live with these limitations, this is a real option.

For business systems, the bar rises substantially. If you are replacing an older system you must at least match it in quality, unless you like doing battle with users and clients. If you value your career in this business, you’d best steer clear of generic cards.

###### 8.2.2.1.1 Hardware Echo

Sadly, the echo problem remains. Any professional system connected to the outside world must have the highest-quality echo cancellation available, and this is generally achieved through a hardware echo canceler integrated into the card itself. The advantage over software echo cancellation is clear: The performance of hardware echo cancelers is historically better, and they don’t need to steal CPU cycles to achieve it.

Because echo cancellation is not easy to do well, these modules are accordingly more expensive. Nevertheless, in business applications, hardware echo cancellation is not negotiable for any system you intend to connect to the PSTN. Cards providing PRI to internal servers can get away without it because echo in local trunks is rare, but if you’re buying a card anyway, spend the extra money. You never know how you might need to use the card in the future.

Tail length is a performance parameter to consider when evaluating hardware echo cancelers. It determines the length of the reference sample when calculating echo cancellation. The rule of thumb is that the longer the tail length, the better the echo cancellation. In practice, it’s difficult to hear a difference beyond 128 milliseconds.

###### 8.2.2.1.2 Server Load and Interrupts

In the early years of Asterisk, there was no affordable echo cancellation, so Mark Spencer and others wrote software to perform the cancellation. This necessitated breaking the in- and outbound audio streams into 1ms chunks. For this reason, all the standard ISDN cards in use today set interrupts at 1ms intervals for each B channel.

This historical artifact can lead to problems in some applications. You probably won’t notice this if you use a single PRI or BRI connected to modern server hardware. If you’re using a compact, embedded system, however, even a simple BRI with two B channels can cause problems under load. If you have a large system with multiple PRIs and interface cards, similar problems can occur. Enough interrupts can bring the most powerful system to its knees.

If you are faced with either of these circumstances, you have these options:

> • Find out how much a single system can handle and cluster them.

> • Install an ISDN-SIP gateway. These are black-box systems with an ISDN interface on one side and a SIP interface on the other, which connects to your Asterisk server. Be careful, though: Some of these systems are just Asterisk boxes themselves! You want real, dedicated translation.

> • Buy an ISDN card that solves the interrupt problem at the driver level. For example, Sangoma produced a special driver for its cards that sets an interrupt at 10ms intervals on a by-port, rather than by-B-channel, basis.

###### 8.2.2.1.3 Internal Analog Fax Devices

If you’re connected to the PSTN via an ISDN connection but still use analog fax devices internally, you might run into another timing problem, particularly with long faxes. This is caused by different clock timings on the audio channels. The ISDN cards use the PSTN for their clock source; the analog interface cards use their own, usually internal (and often cheap and unstable) clock source. The result is a clock differential that is managed using a buffer. After two pages (on average), the buffer empties, and you lose a bit of audio, often enough to overwhelm the fax error correction. The result is usually a black line or gap in the fax image. In the best case, nothing is visible; in the worst case, the transmission ends prematurely.

Here are some things you can do to address faxing problems:

> • If you can do without a fax machine, going to software faxing on the server is a cost-effective alternative (see an in-depth explanation in [Chapter 17](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos611843)).

> • An ISDN terminal adapter attached to the same ISDN card as the incoming service will also solve the problem. If you attach the device to a different ISDN card in the same machine, you need to verify that the cards will operate in sync.

> • Cards from some manufacturers can be synced to each other via an internal cable that provides the clock signal from the ISDN card to the analog card.

##### *8.2.2.2 Manufacturers and Drivers*

There seem to be as many ISDN card manufacturers as people with an opinion about them. The products described here are a subjective selection, but have been chosen because they are used widely. Further exploration of the subject could fill another book.

> ### Important
> 
> Hardware and driver information provided here was current at the time of printing. Check this book’s website ([www.the-asterisk-book.com](http://www.the-asterisk-book.com)), where we will post updates.

###### 8.2.2.2.1 Digium

As the parent company and home of Asterisk, Digium ([www.digium.com](http://www.digium.com)) has offered digital interface cards for several years now. (The early cards were analog only.) The advantage for the Digium cards is obvious: You always have drivers updated for the most current Asterisk release. In the past, these drivers have been middling in quality and there have been problems. With the new DAHDI driver generation, Digium is promising better performance.

###### 8.2.2.2.2 Sangoma

Sangoma ([www.sangoma.com](http://www.sangoma.com)) is a popular alternative manufacturer in North America, and was, until recently, purely a hardware company. They make both analog and ISDN interface cards and have a reputation for good technical support.

Open source purists may take exception to Sangoma’s use of a binary-only ISDN stack (for BRI). Sangoma’s response is that the commercial stack is certified for ISDN and has demonstrably fewer issues than the open source mISDN stack.

###### 8.2.2.2.3 Generic HFC-Based BRI Cards

These cards have been sold in Europe for many years now, usually at bargain-basement prices. Support is rarely if ever provided, and at $100 to $150, it can hardly be expected. They are almost always used with mISDN.

#### 8.2.3 Media Gateways

Just as you might use an ATA in place of an analog interface card for regular phones, you could use a “media gateway” for ISDN connections. This gateway converts an ISDN connection into one or more SIP accounts and vice versa. These are usually “black box” solutions, which are configured via a web GUI or over SSH.

Purely analog media gateways are simply ATAs (analog telephone adapters).

##### *8.2.3.1 Advantages*

One major advantage is that a media gateway is often easier to configure than an interface card. You don’t have to open up the server and install the card, either. Configuring Asterisk is simpler because you only have to configure SIP. Finally, you don’t have to run telephone lines of any kind to the server; you install the gateway device in the wire room, connect it to the network patch panel, and put the server anywhere on the network that is practical.

##### *8.2.3.2 Disadvantages*

Media gateways are generally sold on price and not on the quality of installed components, so manufacturers are tempted to use lower-quality interface cards, which can be problematic (see the “[Choosing an ISDN Card](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos365559)” section, earlier in this chapter). Asterisk works best when using the ISDN clock; the clock signal is very stable, and a stable clock signal is vital, especially for conferencing. A media gateway does not pass this signal over Ethernet; the Asterisk server must rely on the system clock, which will vary in stability. Updating a media gateway is also more difficult, if it’s possible at all.

Whether one should choose an interface card or a media gateway is a regular topic of discussion in the Asterisk community. Both sides make good arguments, and you can run a successful system with either. What is best for you depends on the circumstances. If you need stable clock (you are conferencing or you have existing ISDN cards in your system), you’ll need an ISDN card. If you have physical access problems, or you need to maximize the simplicity of the system, go with a media gateway.

### 8.3 Analog Telephony

In spite of the increasing adoption of digital and IP transports, the classic analog line pair still plays a huge role in communications. Most residential land lines in North America are still analog, and many businesses rely on analog lines to connect their small PBXes and key systems. Analog can have a place in installations that have fax devices, which work poorly over IP.

Two types of device can be attached to a telephone line:

> ### Note
> 
> The name describes what the device is attaching to, which can be counterintuitive.

> • **FXO:** Foreign Exchange Office

> A Foreign Exchange Office (FXO) device is any end-user device that attaches to a line and *does not* provide its own line battery voltage. The standard telephone we are all familiar with qualifies as an FXO device, but fax machines and modems are also FXO devices. A phone is an FXO device because it attaches to a Foreign Exchange Office, also called a telephone exchange.

> • **FXS:** Foreign Exchange Station

> A Foreign Exchange Station (FXS) is any device that provides line battery voltage. This almost always means a dial tone and ringing voltage also. You need an FXS device if you need to provide service to analog phones, fax machines, and modems. The telephone outlet on the wall is a typical FXS “device.”

#### 8.3.1 Connecting Analog Devices

FXS devices provide significant voltage; a telephone line in the “on-hook” state can have a voltage as high as 52 volts DC, and a ringing line can have a voltage between 90 volts and 110 volts AC! Keep the AC ringing voltage in mind when you are working on an exposed, active line pair with bare fingers. While the ringing signal is unlikely to do you any harm, the bite can make you quite uncomfortable! If you want to avoid this, wear gloves.

> ### Warning
> 
> If you attach an FXS module on an interface card to a telephone outlet, it can permanently damage your card or even cause the interruption of service from the telephone company! Use caution when connecting your card to the line. Make absolutely sure you are connecting an FXO device to your incoming phone line pair. Some interface cards actually light up the port with a colored LED to indicate whether the port is FXS (usually green) or FXO (usually red). Failing that, mark the ports with a label or marker before you install the interface card in the server.

In the telephony world, polarity is described by the terms *tip* and *ring,* which correspond to the parts of the plug used by telephone operators in the early days of the telephone system.

> • **Tip**

> This is the positive (+), or ground (the tip of the plug).

> • **Ring**

> This is the negative (−), or battery (the ring, just behind the tip). Ring voltage against ground can vary from −48 VDC to −52 VDC.

If the polarity between the device and the line is reversed, it can cause problems in some cases. For example, if you have an older dual-tone multi-frequency (DTMF) phone (such as a Western Electric model 2500), you won’t be able to dial out; reversed polarity has been known to cause noise problems also. Even if most newer devices ignore polarity, it is good practice to keep polarity consistent throughout your wiring system. This way, you can be guaranteed that your phone system will work properly with any standard device.

#### 8.3.2 Analog Telephone Adapter

The analog telephone adapter (ATA) allows you to connect an analog telephone device to an IP network (either SIP or IAX2, and almost always Ethernet). The advantages are the simplicity and low cost when compared with FXS modules on analog interface cards (as little as $50). Also, FXS modules can suffer from noise caused by nearby components in the Asterisk server; an ATA does not suffer from this problem. A major disadvantage of an ATA is that it won’t work any better with fax.

An ATA has one Ethernet port and at least one RJ-11/RJ-12 telephone port, sometimes two. An ATA can be configured via an attached telephone or through a web interface. ATAs may connect directly to a phone or be connected to the building wiring to support multiple extensions sharing a single line.

A SIP ATA is treated just like any other SIP telephone, and you’ll need to create an entry for it in `sip.conf`.

## 9\. Voicemail

In this chapter, we review the capabilities of Asterisk’s built-in voicemail system. Note that this is different from an interactive voice response (IVR) system, which is covered in depth in [Chapter 10](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos442955), “[Interactive Voice Response](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos442955).”

Voicemail is an essential component of any professional telephone system.^([1](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos386549))

[1](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos386443). As a humorous homage to the popular Nortel Meridian PBX voicemail system called Meridian Mail, the Asterisk developers have named the Asterisk voicemail system *Comedian Mail*.

### 9.1 Example Implementations

The examples that follow should give you a quick overview of typical configurations. Specifics and special features are covered in [section 9.3](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos392671), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos392671).”

#### 9.1.1 An Example Home System

In the course of modernizing their home, the Robinson family has decided to install an Asterisk system, including a voicemail system with a mailbox for every family member.

Each family member needs a mailbox. The extension numbers and mailbox parameters are shown in [Table 9.1](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos387836).

**Table 9.1** The Robinson Family Mailboxes

![image](images/00148.jpg)

The `voicemail.conf` looks like this:

> ![image](images/00149.jpg)

In `extensions.conf`, we send an unanswered call to voicemail like so:

> ![image](images/00150.jpg)

> ![image](images/00151.jpg)

A more elegant implementation can use a macro:

> ![image](images/00152.jpg)

#### 9.1.2 An Example Business System

A business like Widgets, Inc. will need a more comprehensive voicemail system. In this example, you’ll be able to see how much you can do with Comedian Mail.

The default settings for each voice mailbox are as follows:

> • Voicemails are saved in WAV format.

> • Each mailbox is limited to a maximum of 200 messages.

> • The maximum length of a voice message is 5 minutes.

> • Voice messages are stored on the system and also sent to the user as an e-mail attachment.

Beyond these default settings, individual departments have additional needs and wants for their mailboxes, as you can see in [Table 9.2](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos390435).

**Table 9.2** Widgets, Inc. Mailboxes

![image](images/00153.jpg)

The `voicemail.conf` for Widgets, Inc. looks like this:

> ### Warning
> 
> Statements in all the code examples are to be entered on a single line unless otherwise indicated. Lines are wrapped in the book due to space limitations, and are designated with an arrow.

> ![image](images/00154.jpg)

Calls are sent to voicemail in `extensions.conf` like so:

> ![image](images/00155.jpg)

> ![image](images/00156.jpg)

> ![image](images/00157.jpg)

The `extensions.conf` for Widgets, Inc. is already starting to look a bit more complicated. This is because we are using different mailbox features for different users and departments. There are normal individual mailboxes for some staff and group mailboxes for sales and reception; on top of that, sales staff must be able to access messages without having to enter a password. This must be as easy and transparent as possible for individual staff members, so we set the standard voice mailbox access number to 800 for everyone.

### 9.3 Dialplan Applications

We can use two voicemail applications in the dialplan (`extensions.conf`):

> • **`VoiceMail()`**

> This application sends a caller to the voicemail system, where she will be asked to leave a message.

> • **`VoiceMailMain()`**

> This application lets recipients check their voice messages and record new voicemail prompts.

#### 9.3.1 VoiceMail

This command prompts the caller to leave a voice message.

The **`VoiceMail()`** command is always called from the dialplan (`extensions.conf`), as in this example:

> exten => 2000,2,VoiceMail(2000,u)

The command uses the following syntax:

> VoiceMail(*mailbox*[@*context*][,u|b|s])

> • *`mailbox`*

> This is the mailbox number. This does not have to be the same as the extension the caller dialed; nevertheless, this is a sensible practice, particularly in larger installations.

> • `@`*`context`*

> Mailboxes may be implemented in a specific context. If no context is provided, the [default] context is used.

> If the caller presses 0 while listening to the prompt, the application will jump to extension o (the small letter o) in the specified context.

> If the caller presses * while listening to the prompt, the application will jump to extension a (the small letter a) in the specified context.

> • `[u|b|s]`

> • `u`

> Causes the “unavailable” message to be played. The pathname for this message is `/var/lib/asterisk/sounds/vm-isunavail.gsm`.^([2](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos396455))

[2](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos396336). If you are using a prepackaged Asterisk, the path may be different (for example, `/usr/share/asterisk/sounds`).

> • `b`

> Causes the “busy” to be played. The pathname for this message is `/var/lib/asterisk/sounds/vm-rec-busy.gsm`.

> • `s`

> Suppresses playback of the “unavailable” or “busy” notifications, plays a beep, and begins recording.

If there is no mailbox configured in `voicemail.conf` for the given number but there is an *n*+101 priority, Asterisk jumps to this priority and continues executing there.

#### 9.3.2 VoiceMailMain

This command gives users access to their messages and lets them record prompts.

The **`VoiceMailMain()`** command is always called from the dialplan (`extensions.conf`). For example:

> ![image](images/00158.jpg)

> • *`mailbox`*

> This is the mailbox number. If no mailbox number is provided, Asterisk prompts for it.

> • `@`*`context`*

> Specifies the voicemail context (in `voicemail.conf`) for the mailbox.

> • `[s|p|g(#)]`

> • `s`

> Disables the password requirement.

> • `p`

> The user is asked for a mailbox number. The number entered is attached as a suffix to the contents of `[mailbox]`; for example, if the user enters 123, [mailbox]123 is called. This lets you easily configure mailbox groups.

> • `g(#)`

> Adjusts the gain (in decibels) when recording voicemail prompts.

A complete description of the voice menus for **`VoiceMailMain()`** is difficult because they depend on the installed prompts. The main functions are described in [Table 9.3](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos400544).

**Table 9.3** Menu Structure for VoiceMailMain()

![image](images/00159.jpg)

### 9.4 voicemail.conf

Voicemail is configured in `voicemail.conf`. The file has three sections, which are described in detail in this section:

> • `[general]`

> Global configuration options go here.

> • `[zonemessages]`

> For organizations spread across time zones, time-zone-specific options go here.

> • Defined contexts

> If the organization has multiple divisions or departments, you can maintain them in separate voicemail contexts.

#### 9.4.1 [general]

Global configurations for the voicemail system go here. The available options for this section are described in detail here:

> • `attach = [yes|no]`

> Sets whether voice message files are attached to e-mail notifications. Default: yes. The format defined by the first entry in the format= line is used.

> • `callback=[`*`context`*`]`

> Specifies the context through which callbacks from the voicemail system are made. If unset, callbacks cannot be made from voicemail. Default: unset.

> • `charset=[`*`charset`*`]`

> Specifies the character set used to encode the text of the e-mail. In this example, ISO Latin-1 is set:

> charset=ISO-8859-1

> • `delete=[yes|no]`

> Sets whether messages are deleted once the e-mail notification with attachment has been sent. This saves hard disk space on the server if users are only to receive messages via e-mail.

> • `directoryintro=[`*`filename`*`]`

> Specifies the filename of a sound file (found in the default sound file directory `/var/lib/asterisk/sounds`) to be used rather than the default sound file for the Dial-by-Name system.

> • `emailsubject=[`*`subject`*`]`

> Specifies the subject line to be used in e-mail notifications. For information about variables, see `emailbody`. The text need not be enclosed in quotation marks:

> emailsubject=New message from ${VM_CALLERID}

> • `pbxskip=[yes|no]`

> Asterisk prefixes [PBX] to the subject line of every e-mail notification. This is intended to make filtering e-mail notifications into a specific folder more straightforward, but can be suppressed with yes if undesired.

> • `emailbody=[`*`email_text`*`]`

> This specifies the body text of the e-mail notifications and is limited to 512 characters.

> You may use variables in the subject and body of e-mail notifications:

> • `${VM_NAME}`

> Name of mailbox owner

> • `${VM_DUR}`

> Message length

> • `${VM_MSGNUM}`

> Message number

> • `${VM_MAILBOX}`

> Mailbox number

> • `${VM_CALLERID}`

> Name and number of caller

> • `${VM_CIDNUM}`

> Number of caller

> • `${VM_CIDNAME}`

> Name of caller

> • `${VM_DATE}`

> Date and time of call

> • `${VM_MESSAGEFILE}`

> Name of the sound file that contains the voice message

All the text needs to be on one line. If you need carriage returns, use the `\n` combination:

> ![image](images/00160.jpg)

> • `serveremail=[`*`fromaddress`*`]`

> This specifies the e-mail address that appears in the From field of e-mail notifications. Here is an example:

> serveremail=voicemail@widgets-inc.biz

> • `fromstring=[`*`fromname`*`]`

> Specifies the envelope sender (From header) in e-mail notifications. This is useful for mail filtering and sorting.

> • `mailcmd=[`*`mailer`*`]`

> Specifies the application (including absolute path) to be used for sending e-mail notifications. Here are two more common examples; note that you can append options:

> ![image](images/00161.jpg)

> • `externnotify=[`*`application`*`]`

> Specifies the application (including absolute path) called by Asterisk when a new message arrives. You can use it to call custom scripts:

> externnotify=/usr/bin/local/send-sms.sh

> • `externpass=[`*`application`*`]`

> Specifies the application (including absolute path) called by Asterisk when a user changes his password. You can use it to call custom scripts:

> externpass=/usr/bin/local/password-notify.sh

> • `forcegreetings=[yes|no]`

> Sets whether the user will be forced to record a new greeting when logging in to the system for the first time. The default is no.

> • `forcename=[yes|no]`

> Sets whether the user will be forced to record her name when logging in to the system for the first time. The default is no.

> • `format=[gsm|wav|wav49]`

> Defines the codecs used to save voicemail messages. If more than one codec is specified, the message is stored once in each of the formats specified. This can lead to a shortage of available disk space but means further transcoding will not be needed if a user using a different codec is retrieving the messages.

> If `attach=yes`, the first format specified is used for the attachment to the e-mail notification.

> format=gsm|wav

> To save messages only in WAV format, use:

> format=wav

> ### Caution
> 
> If this setting is changed during operation, existing files in other formats must be deleted manually by the system administrator.

> • `searchcontexts=[yes|no]`

> Asterisk only looks for mailboxes in the specified context. Setting `searchcontexts=yes` makes Asterisk search in all contexts. The default is `no`.

> • `maxmsg=[`*`number_of_messages`*`]`

> Defines the maximum number of messages a single mailbox may hold. When this limit is reached, no further messages can be recorded, and the caller hears the message `/var/lib/asterisk/sounds/vm-mailboxfull.gsm`. The default is `100`.^([3](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos415404))

[3](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos415285). The path depends on the installation; some packages install the sounds in `/usr/share/asterisk/sounds`.

> • `maxmessage=[`*`length_in_seconds`*`]`

> Sets the maximum duration of a message. There is no limit by default.

> • `minmessage=[`*`length_in_seconds`*`]`

> Sets the minimum duration of a message. The default is `0`.

> Example:

> minmessage=5

> • `maxgreet=[`*`length_in_seconds`*`]`

> Sets the maximum duration of greeting messages. There is no limit by default.

> • `maxsilence=[`*`length_in_seconds`*`]`

> Sets the number of seconds of silence that the system will allow before it assumes that the caller has finished.

> • `silencethreshold=[`*`threshold`*`]`

> Specifies the maximum sound level that Asterisk considers silence when measuring `maxsilence=`. The lower the number, the more sensitive the detection. The default is `128`.^([4](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos418183))

[4](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos418064). There is no indication in the Asterisk source code what the range or unit for this value is. The only way to set the value sensibly is through trial and error.

> • `maxlogins=[`*`no_of_login_attempts`*`]`

> Sets the maximum number of failed login attempts (e.g., the user enters an incorrect password) before Asterisk hangs up. The default is `3`.

> • `skipms=[`*`milliseconds`*`]`

> Sets the number of milliseconds the “skip forward” and “rewind” keys will jump forward or back during message playback. The default is `3000`.

> • `usedirectory=[yes|no]`

> Gives callers access to the Dial-by-Name system. The default is `no`.

> • `saycid=[yes|no]`

> Sets whether the telephone number of the caller is announced when the message is heard. The default is `no`.

> • `cidinternalcontexts=[`*`contextA`*,*`contextB`*`,...]`

> Defines (through a comma-separated list) which contexts are treated as internal when the originating telephone number is announced as per `saycid=`. For contexts defined as internal only the caller’s extension is announced. There is no default.

> • `pagerfromstring=[`*`sendername`*`]`

> Indicates the sender for pager notifications. See `fromstring=`.

> • `pagersubject=[`*`subject`*`]`

> Specifies the subject for pager notifications. See `emailsubject=`.

> • `pagerbody=[`*`body_text`*`]`

> Specifies the message body for pager notifications. See `emailbody=`.

There are other parameters in addition to those documented here; nevertheless, these are those most frequently used. A complete listing of the available parameters, with brief descriptions, may be found in the sample version of `voicemail.conf`.

#### 9.4.2 [zonemessages]

In larger enterprises, voicemail users can be spread across time zones; the `[zonemessages]` section allows for time announcements that correspond to the user’s time zone.^([5](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos422950))

[5](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos422844). Note that time zones defined here must still be activated for individual users.

> *zonename*=*timezone* | *format*

> • *`zonename`*

> This is an arbitrary identifier used to identify the time zone. Only small letters (a–z), numbers (0–9), dash (-), and underscore (_) characters are allowed.

> • *`timezone`*

> Time zone information is stored in `/usr/share/zoneinfo` for most Linux distributions. Typically, the time zone files are sorted by continent, then region or city, separated by a /.

> Examples:

> ![image](images/00162.jpg)

> • *`format`*

> Defines the format for time announcements. This is done with the variables, which are described in [Table 9.4](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos424834).

**Table 9.4** Time Format Variables in voicemail.conf

![image](images/00163.jpg)

> Other allowed variables include `${ANY_VARIABLE}` (the contents of the variable are entered) and `'sound_filename'`. When specifying a sound file, be careful not to add a file extension (e.g., .wav, .gsm); the specified sound file in `/var/lib/asterisk/sounds` is then played. The single quotation marks are mandatory.

Here are some sample formats as they would be used in `voicemail.conf`:

> ![image](images/00164.jpg)

#### 9.4.3 Defined Contexts

As in the dialplan (`extensions.conf`), we can define contexts in `voicemail.conf`. This is useful when there is a need to separate voicemail access by department, branch, or city, and makes it possible to define separate Dial-by-Name directories as well.

The `default` context is mandatory. For most installations, this is all that is required.

#### 9.4.4 Mailboxes

You can configure as many mailboxes as you like in a given context. The proper syntax is as follows:

> mailbox => password,name[,e-mail[,pager-e-mail[,options]]]

The following example sets the voicemail attachment format as WAV and deletes the message once it has been attached to an e-mail and sent:

> 202 => 1234,Gina Smart,gina@widgets-inc.biz,,attachfmt=wav|delete=yes

Here are the parameters, explained:

> • *`mailbox`*

> Mailbox number (digits).

> • *`password`*

> Password for the mailbox (may be letters or numbers). Generally, numbers are more practical as they are more likely to be enterable from a standard telephone set.

> • *`e-mail`*

> E-mail address to which to send e-mail notifications.

> • *`pager-e-mail`*

> E-mail address for the pager to which pager notifications should be sent.^([6](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos428892))

[6](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos428773). Note that such notifications are still, in essence, e-mail notifications. If you want to send SMS notifications, you can do so with a number of external applications that may be invoked through Asterisk.

> • `options`

> Multiple options must be separated by the pipe character (`|`); these options can override global options set in `[general]`. Note that there cannot be any spaces between the parameter name, the = sign, and the value, nor between the options and the pipe character.

> The most important options applied here are as follows:

> • `tz=[`*`timezone`*`]`

> Sets the time zone previously defined in `[zonemessages]`.

> Example:

> tz=alberta

> • `attach=[yes|no]`

> If defined, sets whether voice message files are attached to e-mail notifications.

> • `attachfmt=[gsm|wav|wav49]`

> If defined, overrides the `format=` value set in `[general]` for message attachments to e-mail notifications.

> • `saycid=[yes|no]`

> Sets whether the telephone number of the caller is announced when the message is heard.

> • `sayduration=[yes|no]`

> Sets whether the length of the message will be announced. The default is `yes`.

> • `saydurationm=[`*`length_in_minutes`*`]`

> Defines the minimum duration for a message to be before the duration is announced. The default is `0`.

> • `dialout=[`*`context`*`]`

> Specifies the context to be used for dialing out from a message. Calls cannot be made out of voice mail unless this parameter is set.

> • `sendvoicemail=[yes|no]`

> Sets whether a user may send messages to other voicemail users.

> • `callback=[`*`context`*`]`

> Specifies the context to be used for dialing out from a message. If defined, this makes it possible to return a call to someone who has left a message.

> • `review=[yes|no]`

> Sets whether callers leaving a message may listen to the message before sending it. The default is `no`.

> • `operator=[yes|no]`

> Sets whether callers can connect to the operator before, during, or after recording a message by pressing 0 (zero). In Asterisk, the operator is always the o (small letter o) extension in the current context. The default is `no`.

> • `envelope=[yes|no]`

> Sets whether message envelope information is announced before the message is heard. Setting this parameter to no overrides other parameters (for example, `tz`). The default is `yes`.

> • `delete=[yes|no]`

> Sets whether messages are deleted after they have been attached to an e-mail notification. The default is `no`.

> • `nextaftercmd=[yes|no]`

> Sets whether the system jumps to the next message after the current message has been saved or deleted. The default is `no`.

> • `forcename=[yes|no]`

> If set to `yes`, forces a system user to record her name when accessing the system for the first time. The default is `no`.

> • `forcegreetings=[yes|no]`

> If set to `yes`, forces a system user to record a personal greeting when accessing the system for the first time. The default is `no`.

> • `hidefromdir=[yes|no]`

> Sets whether the mailbox for this user will be hidden from the Dial-by-Name directory. The default is `no`.

### 9.5 Dial-by-Name

Although not part of the voicemail system per se, we discuss the Dial-by-Name directory here because it was developed along with Comedian Mail and gets its configuration from `voicemail.conf`.

The caller is asked to enter the first three letters of the person’s last name (if option `f` is specified, the first name is used) using the telephone keypad. The application searches for the entry in the directory and connects the caller after checking that the entry is the correct one.

Returning to our example for the Robinson family, we make the following small changes:

> ![image](images/00165.jpg)

From here it is a simple matter to generate a Dial-by-Name directory. We use the Asterisk application **`Directory()`** in `extensions.conf`:

> exten => 800,1,Directory(default,from-internal)

The general syntax for **`Directory()`** is as follows:

> Directory(*vm-context*[,*dial-context*[,*options*]])

> • *`vm-context`*

> The directory is always generated from a specific context; that is, only the entries in this defined context are entered in the directory. In most cases, the `default` context is sufficient. In a larger enterprise, you may want to separate directories by department; in this case, you will need additional contexts.

> • *`dial-context`*

> The directory is used to call to a specific person; `dial-context` defines which context is used for the call. If undefined, `vm-context` is used instead.

> If the caller presses 0 (zero), the call will be sent to the o (small letter o) extension in this context. If he presses * (asterisk, or star), the call will be sent to the a (small letter a) context.

> • *`options`*

> Option `f` sets searching by first name rather than last name.

### 9.6 Saving Passwords in voicemail.conf

The `voicemail.conf` file need not serve only as a directory source; it can also be used as a general storage file for passwords. You may encounter situations where users must authenticate for reasons other than retrieving voicemail (for example, call agents logging in at a call center).

As a result, it is sometimes necessary to create `voicemail.conf` entries for users, even if they have no need for a mailbox. Don’t worry about callers accidentally leaving messages in an unattended mailbox; only mailboxes explicitly referenced through an extension using **`VoiceMail()`** or **`VoiceMailMain()`** in `extensions.conf` will be accessible to callers.

For example, you might make two entries in the context `[call-center-agents]` in `voicemail.conf:`

> ![image](images/00166.jpg)

You can use these entries to authenticate a user with the dialplan application **`VMAuthenticate()`** (see [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)”):

> ![image](images/00167.jpg)

Don’t let this example limit your creativity, however. There are many ways to authenticate users, of which this is only one. Saving passwords in AstDB or another database (such as MySQL, for example) is usually preferable.

## 10\. Interactive Voice Response

An interactive voice response (IVR) system lets computer systems interact with telephone callers, who provide input to the system either by pressing the keypad on their telephone set (dual-tone multi-frequency [DTMF] keying, a.k.a. Touch-Tone) or by saying something (natural language speech recognition). Most IVR systems provide selection menus for routing calls without requiring operator intervention, but modern IVR systems can also be very complex applications that handle information or control equipment.

The basic principle common to all IVR systems, however, is that the caller is read a menu and chooses options from that menu to perform actions, or, alternatively, enters information (in numeric format, through pressing the keypad). IVRs can be used to obtain stock quotations, train schedules, and weather reports; they can also be used for automated purchasing systems, such as for concert tickets. The potential applications are limited only by your imagination.

Systems vary in their complexity. The most advanced generate spoken text on-the-fly using text-to-speech (TTS) systems and accept spoken user input with speech recognition. When properly implemented they can provide a high level of user friendliness, but implementation is so complex that they are rarely used, except in larger organizations.

The simplest form of IVR is also the most common. Pre-recorded messages are played to the caller; the caller responds with DTMF keypad input, which Asterisk can recognize easily in the default install.

Public opinion on IVRs is divided. Some people find them a helpful form of automation, whereas others find them exceedingly frustrating. This is usually the result of poor menu design or speech recognition with a high failure rate. A well-functioning IVR can be pleasant for the customer, but a poorly implemented one can scare her away.^([1](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos445308))

[1](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos445202). The increasingly multiethnic nature of society everywhere means that speech recognition should be implemented with caution, as accents can be problematic.

Take care when planning an IVR system. Pay special attention to menu design and allow adequate time for a clean development and deployment. Aggressive testing and post-deployment monitoring of premature hangups should be part of your routine. Remember that IVR systems are not an end in themselves, nor are they a panacea. Think of your customer!

### 10.1 A Simple IVR

The standard Asterisk sound set includes a file called `marryme.gsm`, containing the announcement “Will you marry me? Press 1 for yes or 2 for no.”^([2](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos446390))

[2](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos446284). Allison Smith is a Canadian voice professional who is the “Voice of Asterisk.” Its growing popularity has given her a considerable cult following.

(Using this IVR for an actual marriage proposal is strongly discouraged.) To build a “marriage proposal” application, the following dialplan will suffice:

> ![image](images/00168.jpg)

If the caller dials extension 30, Asterisk answers and plays the file `marryme.gsm`. Through use of the **`Background()`** application, the user is allowed to enter input at any time during playback. The input is interpreted as an extension and the call is passed to that extension. If the caller presses 1, he hears “Thank you for your cooperation,” after which Asterisk hangs up.

> ### Note
> 
> **`Playback()`** (see [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)”) only plays back sound files; input is ignored. **`Background()`** (see [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)) plays sound files back while listening for caller input, which is interpreted as an extension as though it had been dialed as one.

#### 10.1.1 Timeouts

If you have multiple extensions beginning with the same digits, you need to allow sufficient time for the IVR to recognize all possible combinations. Let’s examine the following example:

> ![image](images/00169.jpg)

**`Background()`** waits a set time after each digit in order to distinguish between 1, 10, and 100. Once this time `(TIMEOUT)` has expired, input is deemed to be complete.

> ### Tip
> 
> `TIMEOUT` lets you set other timeouts. For more information, enter **`show function TIMEOUT`** in the Asterisk CLI, or see [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), “[Dialplan Functions](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).”

`TIMEOUT` is defined in seconds and may be set in the dialplan as follows:

> exten => 123,1,Set(TIMEOUT(digit)=3)

In this dialplan, Asterisk will proceed immediately if 2 is pressed, but only after the timeout has expired if 1 is pressed. Asterisk intelligently determines whether a digit entered can match multiple extensions and behaves accordingly.

#### 10.1.2 Invalid Input (the i Extension)

An invalid entry (any entry for which no extension in the dialplan matches) can be handled by the `i` extension. In the following example, the IVR plays an apology to the caller and hangs up. (A real IVR should probably bring the caller back to the main menu in the event of an invalid entry.)

> ![image](images/00170.jpg)

#### 10.1.3 Pauses

The easiest way to create pauses for input is to play back empty sound files. A series of silent sound files of between 1 and 9 seconds in length may be found in `/var/lib/asterisk/sounds/silence`. If we need to allow 5 seconds following the prompt (a marriage proposal requires careful consideration, after all), here’s how we can accomplish that:

> ![image](images/00171.jpg)

### 10.2 Multilevel IVR Systems

The problem with multilevel IVRs is that the caller has to enter single digits multiple times (oftentimes the same digit), but gets a different response depending on the menu level. In Asterisk, a number can only be used once in a given context. If we need multiple menus that provide different responses for the same digits, we must place the submenus in different contexts (`[cafeteria]` in our example). We jump between these contexts using the application **`Goto()`** (see [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)). Let’s assume you have some custom sound files stored in `/var/lib/asterisk/sounds`. Here are the files followed by brief descriptions of what they contain:

> • `mainmenu.gsm`

> “Press 1 for sales, 2 for service, or 3 for the cafeteria.”

> • `cafeteria.gsm`

> “Press 1 to hear the menu for this week or 2 to hear the menu for next week.”

> • `cafeteria-menu-this-week.gsm`

> “Monday: Noodles with pesto sauce. Tuesday: Pork chops....”

> • `cafeteria-menu-next-week.gsm`

> “Monday: Stew, featuring noodles, basil and, um, pork chops....”

If sales is at extension 100 and the service department is at 150, the dialplan for this IVR would look like this:

> ![image](images/00172.jpg)

Even though it is technically possible to support an unlimited number of IVR levels, in practice it is advisable to keep the number of menu levels to a maximum of three. Many callers hang up after the third menu level.

### 10.3 Text-to-Speech

Text-to-speech (TTS) is simply the conversion of written text into a spoken word, using speech synthesis. In our Asterisk system, this means that an external program generates a sound file using a given text file (usually in ASCII format) as the source. The resulting sound file is played back as any other sound file would be, and the caller hears the text spoken out.

Quality of TTS engines varies widely. As a rule of thumb, the open source engines are not as sophisticated as the commercial ones.

> ### Tip
> 
> Sometimes you can test high-quality engines through web portals. IBM offers a test portal for its TTS engine at [www.ibm.com/software/pervasive/tech/demos/tts.shtml](http://www.ibm.com/software/pervasive/tech/demos/tts.shtml). Like IBM, Cepstral has a demo portal at [www.cepstral.com/demos](http://www.cepstral.com/demos).

The TTS engine Festival ([www.cstr.ed.ac.uk/projects/festival](http://www.cstr.ed.ac.uk/projects/festival)) is a widely used open source version, but the voices included with it often lack the quality necessary for professional implementation, particularly if you need voices in languages other than English.

Many Asterisk developers use the engine and voices sold commercially by Cepstral ([www.cepstral.com](http://www.cepstral.com)). As of this writing, the pricing was reasonable. The solution described here builds on the Cepstral engine. If you want to work with the open source Festival instead, these instructions are easily modified to work with it. This applies to other TTS engines, too. The implementation model is the same.

#### 10.3.1 Installing Cepstral TTS

Download the voice from [www.cepstral.com/downloads](http://www.cepstral.com/downloads). The file (`Cepstral_ David_i386-linux_4.2.0.tar.gz` in this example) is installed with the following commands:

> ![image](images/00173.jpg)

The engine installs to `/opt/swift/bin/swift` unless otherwise specified. You can test the installation from the command line as follows:

> ![image](images/00174.jpg)

You can play the resulting file with any audio player, or through Asterisk. To do this, just add a few lines to `extensions.conf`:

> ![image](images/00175.jpg)

To generate some speech output from within Asterisk, we use the **`System()`** application in the dialplan. Here is an example:

> ![image](images/00176.jpg)

Cepstral uses SSML (Speech Synthesis Markup Language) in its engine. You can add speech pauses to the output by specifying them as in this example:

> ![image](images/00177.jpg)

You can learn more about the SSML standard at [www.w3.org/TR/speech-synthesis](http://www.w3.org/TR/speech-synthesis).

## 11\. The Asterisk Database

The problem with using variables in the dialplan is that it is vulnerable to a system crash or a restart of Asterisk. If either of these things happens, the variable is either erased or reset to its default value. This limitation precludes certain implementations entirely. In call forwarding or a calling card application, some values (the remaining balance, for example) need to be stored in a persistent manner so that they can be recalled after a restart. The Asterisk database (AstDB) serves this purpose.

### 11.1 The Asterisk Database

Those needing a database for Asterisk applications often ask how well the AstDB performs. The answer, to the extent there’s a simple one, is that it depends on what you are doing. If you are working with small amounts of data, as you might in a redial or call forwarding scenario, the AstDB performs admirably and you needn’t look further. If you are working with large, complex datasets, you should consider whether an external SQL server would be better.

In the overwhelming majority of applications, however, this discussion is purely theoretical. The Asterisk database is built on the Berkeley DB (BDB), which is already a very fast database engine. When handling key/value pairs, BDB is among the fastest of databases. The question of database choice should be raised, therefore, when speed of the database is proven to be the source of problems, or when you want to build a larger system with greater functionality than may be met by a simple key/value database.

In a default installation, Asterisk comes packaged with a database built on BDB. BDB is a simple, high-performance, embedded database library with application programming interfaces (APIs) for C, C++, Java, Perl, Python, Tcl, and many other programming languages. It stores key/value pairs and places no constraints on how data is stored in a record. It does not support SQL or any other query language and allows access only through in-process API calls. This database stores information in the form of key/value pairs, and keys are grouped into families.

> ### Warning
> 
> Up to and including Asterisk Version 1.2, these applications were used for database access:
> 
> > DBput(*family*/*key*=*value*)
> 
> To save a value in the database.
> 
> > DBget(*var*=*family*/*key*)
> 
> To retrieve a value from the database. If the called key cannot be found, Asterisk jumps to priority 101 in the current extension.
> 
> These commands are no longer supported as of Asterisk 1.4\. For this reason, only the new method, using the **`DB()`** function is mentioned here, which also works in 1.2.

Information in this database can be manipulated using the **`DB()`** function (see [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), “[Dialplan Functions](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).”)

#### 11.1.1 Writing Values to the Database

The **`DB()`** function can be called from within the **`Set()`** application. To give the `apple` entry in the `fruit` family the value `20`, write the extension as follows:

> exten => 1234,1,Set(DB(fruit/apple)=20)

#### 11.1.2 Reading Values from the Database

Values may be called from the database using **`DB()`** in the form `${DB(`*`family`*`/`*`key`*`)}`. To print the contents of `apple` in the `fruit` family on the console, use the following command:

> ![image](images/00178.jpg)

> ### Warning
> 
> In all the code examples, everything is written on one line, without breaks, unless otherwise noted. The limited space for text requires that we wrap the lines in the book.

You can also store the value from this database field in a variable using **`Set()`**:

> exten => 1234,1,Set(applequantity=${DB(fruit/apple)})

#### 11.1.3 Deleting Values from the Database

The applications **`DBdel()`** and **`DBdeltree()`** are used to delete database entries.

##### *11.1.3.1 DBdel() and ${DB_DELETE()}*

In Asterisk 1.2, individual entries are deleted using `DBdel()`. Delete the key `apple` in the family `fruit` as follows:

> exten => 1234,1,DBdel(fruit/apple)

**`DBdel()`** is deprecated in Asterisk 1.4; use the **`DB_DELETE()`** function instead. This is called like so:

> exten => 1234,1,NoOp(${DB_DELETE(fruit/apple)})

See also [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029),” and [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), “[Dialplan Functions](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).”

##### *11.1.3.2 DBdeltree()*

If you need to delete an entire key family, use **`DBdeltree()`**. The `fruit` family is deleted as follows:

> exten => 1234,1,DBdeltree(fruit)

See [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029).

### 11.2 Database Access from the Command-Line Interface

The system administrator can access the database from the CLI.

> ### Tip
> 
> If you have trouble remembering a command or the exact syntax, you can get help at the CLI with **`help database`**:
> 
> > ![image](images/00179.jpg)

For the following examples, remember that if your family, key, or value contain any blank spaces, the entire name must be enclosed in double quotes (“ ”); for example, **`database put test entry "Hello world"`**.

#### 11.2.1 Writing Values to the Database

You write values to the database with **`database put`** *`family key value`*:

> ![image](images/00180.jpg)

#### 11.2.2 Reading Values from the Database

Read values from the database with `database get` *`family key`*:

> ![image](images/00181.jpg)

#### 11.2.3 Deleting Values from the Database

Both **`database del`** *`family key`* and **`database deltree`** *`family`* delete values from the database.

##### *11.2.3.1 database del*

To delete only the key `apple` from the `fruit` family, use **`database del`**:

> ![image](images/00182.jpg)

##### *11.2.3.2 database deltree*

You can delete an entire key family with **`database deltree`**:

> ![image](images/00183.jpg)

#### 11.2.4 Displaying Database Contents

The commands **`database show`** and **`database showkey`** display database contents in the CLI:

> ![image](images/00184.jpg)

### 11.3 Database Access from the System Shell

Using the command **`asterisk -rx '`*`command`*`'`**, you can execute any CLI command via a shell script. The following example shows how a database is populated, read, and then finally deleted through external commands:

> ![image](images/00185.jpg)

> ### Important
> 
> Remember that if the family, key, or value contains any blank spaces, you must use double quotes (“) around the string, as follows:
> 
> > big-island:~# **asterisk -rx 'database put test entry "Hello World"'**

### 11.4 Database Backup

The AstDB is stored in `/var/lib/asterisk/astdb` by default. You can copy that directory as long as Asterisk is stopped.

You can also back up the database from the system shell during operation with the following command:

> asterisk -rx "database show" > /tmp/backup-asterisk-database.txt

Of course, restoring the database from this kind of backup is more difficult.

### 11.5 Application Example: Call Forwarding

Anybody who wants, when she’s not in, to have calls to her local number passed on to her mobile phone needs call forwarding. This can be achieved either through the local SIP phone or centrally through Asterisk. In practice, we prefer that latter approach because it frees us from dependency on end devices, which could be disconnected, fail, or be swapped with others. It also means that the call forwarding setting is not lost in the event of a power failure or system restart.

#### 11.5.1 Simple Call Forwarding

All the staff at Widgets, Inc. can forward calls to their locals to any number they choose. To activate this forwarding, the internal extension 44, followed by the target number, is dialed. To deactivate this forwarding, 44 is dialed again (this time without a target number following it). You can implement this with the following dialplan. (The text wraps in this code example, but remember that every extension must be entered on a single line!)

> ![image](images/00186.jpg)

#### 11.5.2 Complex Call Forwarding

In this example, all the employees of Widgets, Inc. should be able to activate call forwarding. In addition, however, there must be global forwarding for the whole branch, so that calls can be forwarded to another branch when all the head office staff are away on a team-building exercise. This global forwarding is activated via extension 55 (followed by the destination number). The global forwarding must have a higher priority than the individual forwarding. One way to accomplish this is shown here:

> ![image](images/00187.jpg)

### 11.6 Application Example: Calling Card

According to Widgets, Inc. policy, personal calls must be made via a virtual calling card. These cards are charged by the building manager via his phone (by calling extension 88, followed by the three-digit user extension and then the desired cash amount in cents).^([1](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos477125))

[1](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos477019). To keep this example as simple as possible, we don’t consider the case of a card with an existing balance to which more money is added (in other words, in which an addition operation is performed). We are also ignoring the very real possibility that an employee could make personal calls from someone else’s extension.

Such calls are billed at a per-call rate of 1 cent per call. To make a personal call, the user dials 99, followed by the number being called. Of course, we don’t want anything to be deducted from the account in the event of a busy signal. Also, users may call up the account balance by dialing 98:

> ![image](images/00188.jpg)

> ![image](images/00189.jpg)

## 12\. Queues

A call queue lets you place callers on hold automatically if you don’t have someone available to answer the phone right away. (Most of us call this “being on hold.”) Many customers detest queues. Sadly, there is scarcely a business around these days that does not make use of them; perhaps they are better than the alternative, which is to not take the call at all. Whatever your opinion about them, they are part of communications reality, so we will describe the configuration and operation of queues in Asterisk here.^([1](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos479040))

[1](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos478934). An example queue setup using AEL (Asterisk Extension Language) is described in `doc/queues-with-callback-members.txt` in Asterisk 1.4.

Four files are important for queues:

> • `queues.conf`

> Defines the queues.

> • `agents.conf`

> Defines agents; these are the staff who take calls.

> • `musiconhold.conf`

> Defines the hold music.

> • `extensions.conf`

> The dialplan. Calls are directed to the queue using **`Queue()`**, and agents are added using **`AgentLogin()`** or **`AgentCallbackLogin()`**.

A common cause of misunderstanding is the confusion of “queue members” with callers. Queue members are always and only agents or queue devices, never callers.

> ### Tip
> 
> For simplicity’s sake, we use the term *agents* primarily. You call queue members agents. For someone who comes from the call center business, that’s a bit confusing, because queue members can also be normal SIP extensions.
> 
> You are not required to use agents; instead, you can simply assign specific SIP devices to the queue. You do this by writing `member => SIP/1001` to `queues.conf`, for example; alternatively, you can assign the interface dynamically in the dialplan with the command **`AddQueueMember()`**. See [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029).”

Agents may belong to more than one queue, and we want our agents to be able to log in at any station (also called hot-desking).

You configure agents in the `agents.conf` file:

> ![image](images/00190.jpg)

Configured agents are added to specific queues in the `queues.conf` file:

> ![image](images/00191.jpg)

The queue itself is invoked through an extension line in `extensions.conf`:

> ![image](images/00192.jpg)

This is how it works: Agents log in by dialing extension 25, hear pleasant music, and await callers. Calls to extension 20 are passed into the queue and are answered on a first-in, first-out basis. The agent hears a tone, and the first caller is connected.

### 12.1 Extension for Testing Hold Music

We add the following extension to `extensions.conf` for testing to see that the music-on-hold is functioning as we expect:

> ![image](images/00193.jpg)

### 12.2 musiconhold.conf

Let’s begin with the simplest part: setting up music-on-hold.

> ### Keeping Your Hold Music Legal
> 
> Note that the music you use for music-on-hold may be subject to licensing fees. If you want to be sure you are using music lawfully, you can obtain use licenses from the performer’s rights organization in your country.
> 
> In the United States, contact the following:
> 
> > • The American Society of Composers, Authors, and Publishers (ASCAP), [www.ascap.com](http://www.ascap.com)
> 
> > • Broadcast Music, Inc. (BMI), [www.bmi.com](http://www.bmi.com)
> 
> > • SESAC, [www.sesac.com](http://www.sesac.com)
> 
> In Canada, contact the following:
> 
> > • The Society of Composers, Authors, and Music Publishers of Canada (SOCAN) [http://www.socan.ca](http://www.socan.ca)
> 
> In the United Kingdom, contact the following:
> 
> > • PRS for Music, [www.prsformusic.com](http://www.prsformusic.com)
> 
> In Australia and New Zealand, contact the following:
> 
> > • The Australasian Performing Right Association and Australasian Mechanical Copyright Owners Society, [www.apra-amcos.com.au/](http://www.apra-amcos.com.au/)
> 
> > • The Australasian Performing Right Association (NZ), [www.apra.co.nz](http://www.apra.co.nz)
> 
> Generally, license fees for use of music in waiting areas and on telephone systems are quite reasonable, so this option is worth considering. Alternatively, you can obtain royalty-free music from a variety of Internet sources. Finally, you may use the three tracks provided with Asterisk.

Allowed configuration settings are described in the sample `musiconhold.conf`. Additional information on MP3 music support through **mpg123** may be found in `doc/README.mp3` (1.2) / `doc/mp3.txt` (1.4). The optimum sample rate for MP3 files is 8000Hz, mono.

Here is the simplest possible configuration, using only one music class (`default`):

> ![image](images/00194.jpg)

Now we stop and start Asterisk, for example, using **`asterisk -rx "restart now"`**, to activate the new extension and the audio streams. (A reload is not sufficient.) Now, if you call extension 222 (as defined above), you should hear music-on-hold.

Still, the following is a better configuration, for which we create another music directory `moh-native` in `/var/lib/asterisk`:

> ![image](images/00195.jpg)

For this, it is necessary to convert the source MP3 files into an Asterisk compatible format, which can be accomplished using **`sox`** and **`lame`**.

**`sox`** ([http://sox.sourceforge.net](http://sox.sourceforge.net)) is available as a Debian package, and is installed as follows:

> $ apt-get install sox

For Mac OS X, if you have installed Darwinports ([http://darwinports.opendarwin.org](http://darwinports.opendarwin.org) or [http://darwinports.com](http://darwinports.com)), there is also a package:

> $ port install sox

Many other distributions have **`sox`** packages; in the absence of packages, you must install it from source.

**`lame`** ([http://lame.sourceforge.net](http://lame.sourceforge.net)) is not available as a Debian package, so we must download and install it using the familiar **`./configure`**, **`make`**, and **`make install`** commands.

For Mac OS X, there is a Darwinports package (see **`sox`**):

> $ port install lame

Or via Fink ([http://fink.sourceforge.net/](http://fink.sourceforge.net/)):

> $ fink install lame

Of course, you can do this with the FinkCommander GUI also.

After you’ve installed the necessary applications, you can create the music files this way:

> ![image](images/00196.jpg)

This converts our (dummy, only for demonstration) `music.mp3` file into WAV, and then into RAW and GSM formats (with a sample rate of 8kHz). We can also make versions of the file in a-law and u-law formats (by using the `.al` and `.ul` file extensions with **`sox`**); Asterisk will automatically choose the sound file requiring the least processing. The important common factor is that the sample rate always be 8000Hz.

> ### Important
> 
> If you do not specify `autoload` in `modules.conf`, you must ensure that the modules for the formats you wish to use here are loaded before `res_musiconhold`.

For our test, we copied the WAV files provided in `moh/` to `moh-native/`, transcoded them to RAW and GSM formats using **`sox`**, and then deleted the WAV files (which caused us problems) from the directory:

> ![image](images/00197.jpg)

For CPU-critical installations (e.g., large installations), you should take time to read `contrib/utils/README.rawplayer`, which may be found in the Asterisk source directory.

Additional music classes may be defined. For example, in addition to `[default]`, you might choose to classify by genre (e.g., `[rock]`) and provide a different file path (perhaps a subpath) where files of that genre are located. You might also classify by intended audience, particularly if you have custom files with announcements directed at specific types of customer. As always, don’t forget to **`reload`**!

### 12.3 queues.conf

Queues are defined and configured in `queues.conf`. This file is—as you are already familiar—divided into sections.

Under `[general]`, we always set `persistentmembers=yes`, so that agents are re-added to their respective queues when Asterisk is started.

Every queue goes in its own section. In our example, we are configuring a support queue in its own section `[support]`. The following parameters are available to us:

> • `musiconhold`

> Sets the music class of the queue. We choose the above-configured `default`:

> musiconhold=default.

> • `announce`

> Defines an audio file that is played back to the agent before a call is answered. This is so that an agent working in more than one queue will know which queue the incoming call is coming from and be able to answer appropriately.

> ;announce=queue-support

> If you use this option, remember to place a corresponding announcement audio file in the `sounds` directory (e.g., `queue-support.gsm`).

> • `strategy`

> Sets the call distribution strategy (that is, the method used to decide how incoming calls are distributed to agents):

> • `ringall`

> Ring all agents until one answers (default).

> • `roundrobin`

> Ring agents in order, until one answers.

> • `leastrecent`

> Ring the agent who has been idle the longest.

> • `fewestcalls`

> Ring the agent who has taken the least number of calls in this queue.

> • `random`

> Ring a random agent.

> • `rrmemory`

> Round-robin with memory. Begins the round-robin starting with the agent who is next in line after the last call.

> ### Note
> 
> Asterisk 1.6 is expected to do away with the current `roundrobin` method; `rrmemory` will be renamed `roundrobin`.

> Agents with a lower penalty will always be preferred in all strategies.

> strategy=ringall

> The appropriate setting depends on the circumstances; `ringall` can be extremely annoying for agents, while other values can lead to longer wait times for callers, if agents fail to answer.

> • `servicelevel`

> Sets the service level threshold (that is, sets the maximum wait time for callers). This is only really useful for statistical analysis (for example, in asking the question “How many calls were answered within the service level threshold of *x* seconds?”).

> servicelevel=60

> • `context`

> If set, this is the context we pass the caller to if she presses a single digit while waiting in the queue. This digit is treated as an extension and the call is taken out of the queue and routed to the extension in that context.

> ![image](images/00198.jpg)

> • `timeout`

> Sets the maximum time a telephone may ring before we treat it as unattended.

> timeout=15

> • `retry`

> Sets the interval (in seconds) before we ring all the agents again.

> retry=5

> • `weight`

> The relative importance of the queue compared to other queues. If an agent is a member of multiple queues, calls from higher-weight queues are connected first. For example, you might give an emergency queue higher weight.

> weight=0

> • `wrapuptime`

> The time interval after an agent has finished a call before the system will pass another call to the agent (default: `0`).

> ![image](images/00199.jpg)

> • `maxlen`

> Maximum number of callers allowed to be waiting in the queue (default: `0`, meaning unlimited).

> maxlen=0

> • `announce-frequency`

> Sets how often a caller will hear an announcement indicating her position in the queue or the estimated wait time. (`0` turns this completely off.)

> announce-frequency=90

> • `announce-holdtime`

> Sets whether the estimated wait time will be announced after the queue position. Possible values are `yes`, `no`, or `once`.

> announce-holdtime=yes

> • `announce-round-seconds`

> Rounding level for wait-time announcements. If `0`, only minutes, not seconds, are announced; other possible values are `0`, `1`, `5`, `10`, `15`, `20`, and `30`.^([2](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos504568))

[2](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos504449). Older versions accepted other values, which could result in confusing announcements. See Bug 9514.

> For example, when set to `30`, a wait time of 2:34 will be rounded to 2:30.

> announce-round-seconds=0

> • `periodic-announce-frequency`

> Sets the interval, in seconds, for periodic announcements (`periodic-announce`; e.g., “We thank you for your patience; all our agents are currently serving other callers. Please continue to hold.”).

> periodic-announce-frequency=60

> • `monitor-format`

> When set, recording (as with the **`Monitor()`** application) is turned on and the recording format defined. (If not defined, recording is off.) You may specify `gsm`, `wav` (caution: huge files!), or `wav49`.

> ![image](images/00200.jpg)

> By default, files are named (one `-in` and one `-out`) according to `${UNIQUEID}`. You can change this as needed by putting `Set (MONITOR_FILENAME= filename) before Queue()` in `extensions.conf`. We leave it unset in our example.

> • `monitor-join`

> Combines the ...`-in` and ...`-out` files of a recording into one file. Allowed values: `yes` or `no`.

> monitor-join=yes

> • `joinempty`

> Sets whether callers can be placed in a queue with no agents.

> • `yes`

> Callers may be placed in queues without active agents. (The queue may have no agents logged in, or agents may be logged in but unavailable.)

> • `no`

> Callers may not be placed in queues without active agents.

> • `strict`

> Callers may not be placed in a queue without agents, but *may* be placed in a queue with *unavailable* agents.

> Unavailable should not be confused with busy (that is, on a call). An agent is unavailable if he is a member of the queue but not currently registered on the system.

> ### Warning
> 
> Statically defined queue members are always considered available. If you’re not mindful, callers could end up in an active queue that is never answered (and that’s probably bad for business).

> If the caller is not accepted into a queue, **`Queue()`** ends and execution continues in the next priority in the dialplan.

> joinempty=no ; we don't want our callers waiting in empty queues.

> • `leavewhenempty`

> Sets whether waiting callers are removed from the queue when all the agents have logged out. Allowed values are the same as for `joinempty`. After leaving the queue, execution continues in the next priority in the dialplan.

> leavewhenempty=strict ; don't make 'em wait

> • `eventwhencalled`

> Sets whether events are created in the Manager interface: `AgentCalled`, `AgentDump`, `AgentConnect`, `AgentComplete`. Possible values are `yes` and `no`.

> eventwhencalled=yes

> • `eventmemberstatus`

> Sets whether QueueMemberStatus events are created in the Manager interface. (Use with caution; this can generate a lot of events.) Possible values are `yes` and `no`.

> eventmemberstatus=no

> • `reportholdtime`

> Sets whether the wait time for the incoming caller will be announced to the agent before the call is patched. Some people like to know how long a caller has been waiting, because that caller might be irate. Possible values are `yes` and `no`.

> reportholdtime=no

> • `memberdelay`

> Sets the interval of silence (in seconds) that the caller hears before she is connected with an agent.

> memberdelay=1

> • `timeoutrestart`

> Sets whether the answer-timeout of an agent is reset after a `BUSY` or `CONGESTION` signal. This can be useful for agents who are allowed to refuse calls.

> timeoutrestart=yes

> • `autopause`

> Sets whether an agent who has failed to answer is automatically paused or not.

> autopause=no

> • `ringinuse`

> Sets whether agents who are in a call will be rung. So far, the only channel driver that provides this information is SIP.

> ringinuse=no

> • `member`

> It is possible to statically define agents in `queues.conf` like so:

> member => technology/resource[,penalty]

> An example using a Zap channel would look like this:

> member => Zap/2

> This may be used more than once. It should be employed with caution with `joinempty` and `leavewhenempty`, because these queue members are always treated as available, even if the telephone is unattended. The other disadvantage is that an agent is always bound to a specific workstation and cannot log in at another workstation.

> In our example, we prefer to use the dynamic agents and add agents in the following format:

> member => Agent/agentID

> For two agents `1001` and `1002`, the configuration looks like this:

> ![image](images/00201.jpg)

> These agents must still be defined in `agents.conf` (see below). The agent number is a freely selectable number that uniquely identifies each agent. The number has nothing to do with the extensions that the agent may eventually use.

#### 12.3.1 Announcement Sound Files

The following parameters define which sound files are used for which announcement types. Usually there is no need to change this. For example, *queue-youarenext=sound_filename* sets the filename for the “you are first in line” message to *sound_filename*.

If these parameters are not provided, the default values (shown below) apply:

> • `queue-youarenext=queue-youarenext`

> “You are now first in line.”

> • `queue-thereare=queue-thereare`

> “There are...”

> • `queue-callswaiting=queue-callswaiting`

> “Calls waiting.”

> • `queue-holdtime=queue-holdtime`

> “The current estimated hold time is...”

> • `queue-minutes=queue-minutes`

> “Minutes.”

> • `queue-seconds=queue-seconds`

> “Seconds.”

> • `queue-thankyou=queue-thankyou`

> “Thank you for your patience.”

> • `queue-lessthan=queue-less-than`

> “Less than.”

> • `queue-reporthold=queue-reporthold`

> “Hold time.”

> • `periodic-announce=queue-periodic-announce`

> “All reps busy, wait for next available.”

### 12.4 agents.conf

Agents (who are also called queue members) are defined in `agents.conf`; additional configurations for the agents are also placed here. Like the other configuration files, it too is divided into sections.

We set `persistentagents=yes` in the `[general]` section, so that agent logins persist (meaning they are stored in the Asterisk database) even if Asterisk is restarted.

We set additional parameters in the `[agents]` section, where we also define the agents. The following parameters are available:

> • `autologoff`

> Sets the maximum time a telephone may ring before the agent is automatically logged off.

> Note that agents will not be logged out if the `autologoff` interval is longer than the queue timeout! We set that to 15 seconds, so we set `autologoff` to 14.

> autologoff=14

> • `ackcall`

> Sets whether agents who have logged in with `AgentCallbackLogin()` must press number sign (#) to accept a call. Be aware that the voice prompt in previous Asterisk versions did not indicate that the agent has to press #. Possible values are `yes` and `no`.

> ackcall=no

> • `endcall`

> Sets whether agents may end calls by pressing number sign (#). Possible values are `yes` and `no`.

> endcall=yes

> • `wrapuptime`

> Sets (same as `wrapuptime` in queues.conf; why this appears in both files is not clear) the wait time, this time in *milliseconds,* before an agent can be sent another call. Default: `5000`.

> wrapuptime=5000        ; 5 seconds to clear your throat

> • `musiconhold`

> Sets the music-on-hold class for the agents.

> musiconhold=default

> • `updatecdr`

> Adds agent information to the CDR so that we can see which agent answered the call. Possible values are `yes` and `no`.

> updatecdr=yes

> • `recordagentcalls`

> Record agent calls. Possible values are `yes` and `no`. Default: `no`.

> recordagentcalls=no

> • `recordformat`

> Format for call recordings. Possible values are `gsm`, `wav` (caution, huge files!), or `wav49`. Default: `wav`.

> recordformat=gsm

> • `createlink`

> Sets whether the filename of the call recording will be written to the user field of the CDR, so that the call recording can be matched to the CDR later. Possible values are `yes` and `no`.

> createlink=yes

> • `urlprefix`

> If `createlink=yes`, the filename can be prefixed with a URL where the recording is made available on a web server.

> ![image](images/00202.jpg)

> • `savecallsin`

> Defines the path where recordings are saved. Default: `/var/spool/asterisk/monitor`

> ![image](images/00203.jpg)

> • `agent`

> Defines individual agents. Can appear more than once.

> ![image](images/00204.jpg)

### 12.5 Extensions

Both agent and caller access to the queue are configured in the dialplan. Agents log in as queue members via particular extensions, and callers are placed into the queue with the **`Queue()`** application (see [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)”).

#### 12.5.1 Sending Callers to the Queue

A minimal extension, which places callers in the queue, might look like this:

> ![image](images/00205.jpg)

We prefer something more complete and use this extension:

> ![image](images/00206.jpg)

If we call this extension now, we hear the “nobody is available” message because no agents are logged in.

> ### Tip
> 
> If you want to pretend you have active agents for testing purposes, set `joinempty=yes` and `leaveempty=no` in `queues.conf`.

Now we need to create an extension through which agents can log in:

> ![image](images/00207.jpg)

#### 12.5.2 AgentLogin() and AgentCallbackLogin()

**`AgentLogin()`** establishes an active channel, and incoming calls are simply switched into this active channel. This is analogous to having the phone off the hook and calls simply coming in without the agent actually having to pick up. If the agent hangs up, she is logged out. This also means that an agent cannot be logged in and make outgoing calls at the same time. As a result, `AgentLogin()` is only really appropriate for purely inbound call center groups.

**`AgentCallbackLogin()`** has the advantage of letting agents log in, and then having the system call back with calls from the queue. They remain logged in after hanging up and can make outgoing calls. This application is, however, deprecated as of Version 1.4\. The example in `doc/queues-with-callback-members.txt` uses AEL (which can easily be converted into regular dialplan format) to identify agents, **`AddQueueMember()`** to dynamically add members to the queue and `Dial()` to call agents back.

If **`AgentCallbackLogin()`** were to disappear without a replacement, real functionality and ease of configuration would be lost.

> ### Tip
> 
> Try out what you’ve learned. Write a dialplan which brings callers to an IVR menu first; for example, “For sales, press 1; for returns, press 2.” And then pass callers to two separate queues, one for each department, depending on the input the caller gives.

### 12.6 Log File

Events that happen in queues are written in a detailed format to the queue log (usually `/var/log/asterisk/queue_log`) in addition to the regular call detail recording. Events are recorded in `queue_log` on a line-by-line basis in the following format:

> *timestamp*|*call_id*|*queue*|*channel*|*event*|*parameter1*[|*parameter2*[|*parameter3*]]

> • *`timestamp`*

> The UNIX time of the event.

> • *`call_id`*

> The unique ID of the call (alphanumeric). Can be `NULL` or `NONE` (e.g., in the case of `QUEUESTART` events).

> • *`queue`*

> The name of the queue (e.g., `support`). Can be `NULL` or `NONE`.

> • *`channel`*

> The name of the bridged channel (e.g., `Agent/1001`). Can be `NULL` or `NONE`.

> • *`event`*

> The name (type) of the event (see next page). The parameters that follow depend on the event type.

Possible events are, among others (see also `doc/queuelog.txt`):

> • ABANDON

> The caller abandoned the queue by hanging up. Parameters: position, entry position, wait time.

> • AGENTDUMP

> The agent dumped the caller while listening to the queue announcement.

> • AGENTLOGIN

> An agent logged in. Parameters: channel (e.g., `SIP/127.0.0.1-0181ac00`).

> • AGENTCALLBACKLOGIN

> A callback agent logged in. Parameters: login_extension[@context].

> • AGENTLOGOFF

> An agent logged out. Parameters: channel, login time.

> • AGENTCALLBACKLOGOFF

> An agent was logged out. Parameters: login_extension[@context], login time, cause (e.g., autologoff).

> • COMPLETEAGENT

> Call between caller and agent was ended by agent. Parameters: wait time, call time, queue entry position.

> • COMPLETECALLER

> Call between caller and agent was ended by caller. Parameters: wait time, call time, queue entry position.

> • CONFIGRELOAD

> Configuration was reloaded (e.g., with **`asterisk -rx "reload"`**).

> • CONNECT

> Caller was connected to an agent. Parameters: Wait time.

> • ENTERQUEUE

> Caller was placed in the queue. Parameters: URL (if available), caller ID.

> • EXITEMPTY

> Caller was exited from the queue because no members were available. Parameters: queue position, entry position, wait time.

> • EXITWITHKEY

> Caller left the key by pressing a key. Parameters: key, queue position.

> • EXITWITHTIMEOUT

> Caller was in the queue too long and the timeout expired. Parameters: queue position.

> • QUEUESTART

> The queue was started. The `call_id`, `queue`, and channel fields are set `NULL`.

> • RINGNOANSWER

> An available agent was called, but did not answer within the timeout. Parameters: ring time (in milliseconds).

> • SYSCOMPAT

> The agent accepted a call, but the channels were not compatible and the call was ended.

> • TRANSFER

> Caller was transferred to another extension. Parameters: extension, context.

Some commercial queue log analysis tools include QueueMetrics ([http://queuemetrics.loway.it](http://queuemetrics.loway.it)) and Easy PABX ([http://www.easypabx.com](http://www.easypabx.com)). See also [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029).

#### 12.6.1 Importing the Queue Log into MySQL

As yet, Asterisk cannot write the queue log directly into a SQL database. Unfortunately, all the widely used statistical tools assume and expect data to be in a SQL database. A variety of scripts seek to mitigate this problem (some may be found at [www.voip-info.org/wiki/view/Asterisk+queue_log+on+MySQL](http://www.voip-info.org/wiki/view/Asterisk+queue_log+on+MySQL)) or are provided with the analysis tools. They all follow the same principle: the `queue_log` is replaced with a named pipe (FIFO); as soon as Asterisk attempts to write to the log, the log entry is converted and entered into the database.

> ### Warning
> 
> This method works in 99% of cases. There remains the risk, however, that the script fails to start before Asterisk or terminates unexpectedly and stops reading from the named pipe, such that Asterisk receives a `SIGPIPE` when trying to write to the logs and crashes!

Because there is no alternative without native Asterisk SQL support, we provide a sample Perl script from William Lloyd despite the associated risk:^([3](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos542654))

[3](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos542548). wlloyd at [slap.net](http://slap.net), released through the Digium `asterisk-users` mailing list. See [http://lists.digium.com/pipermail/asterisk-users/2005-July/109892.html](http://lists.digium.com/pipermail/asterisk-users/2005-July/109892.html).

> ![image](images/00208.jpg)

> ![image](images/00209.jpg)

> ![image](images/00210.jpg)

QueueMetrics (the free demo version) comes packaged with a Perl script called `queueLoader.pl` that will also load the queue log into mySQL. (Again, heed the warning above: If you do this in real time, there is a risk that Asterisk will crash.)

## 13\. Features

Asterisk is powerful, but some features routinely used in office environments are either not enabled by default or simply very well hidden. This chapter covers those features, which are configured in the `features.conf` file.

### 13.1 Call Transfer

If you use the **`Dial()`** application without any flags or options, you won’t be able to transfer a current call to another extension. This feature must be explicitly enabled in **`Dial()`** via the `t`, `T`, or `tT` options. This is described in detail in [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029).” If you want to give both the caller and called party rights to transfer the call, you must use the `tT` options:

> exten => _2XXX,1,Dial(SIP/${EXTEN},tT)

#### 13.1.1 Blind Transfer

The expression *blind transfer* describes transfers that occur without an interaction between the transferer (the original recipient of the call) and the transferee (the new intended recipient). By default, this is done by entering `#1` followed by the new destination number. If you want to transfer the current call to extension 2323, you dial `#12323`.

You can change the feature code for blind transfers in `/etc/asterisk/features.conf` in the context `[featuremap]`:

> ![image](images/00211.jpg)

#### 13.1.2 Attended Transfer

In contrast to the blind transfer, the original recipient can discuss the call in private with the intended recipient using attended transfer; the call is only transferred once the original recipient hangs up. By default, attended transfers are initiated with the `*2` key combination, followed by the new destination number.

You can change the feature code for attended transfers in `/etc/asterisk/features.conf` in the context `[featuremap]`:

> ![image](images/00212.jpg)

If you are using call limits in your devices, be aware that attended transfers temporarily use two channels.

### 13.2 Call Parking

To park a call is to place an active call in a virtual parking lot where it can be retrieved from any other extension by dialing the parking position number. For call parking to work in Asterisk, the `parkedcalls` context must be included (using `include`) in the current context, as follows:

> ![image](images/00213.jpg)

Only once this context has been included can calls be parked by dialing `#700` during an active call. Asterisk will read back the parking position to the caller. (Be sure to note it!) Calling this park position number (e.g.,`701`) retrieves the call from any telephone in a context that includes the `parkedcalls` context.

> ### Warning
> 
> Parking positions are not secured in any way. If person A parks a call at position 705 and person B dials 705 by accident, she will connect to the parked call.

Feature codes, the number of available parking positions, and the name of the parking context can all be changed in `/etc/asterisk/features.conf` in the `[general]` context:

> ![image](images/00214.jpg)

## 14\. Conferencing

Asterisk offers an excellent built-in conferencing system. Nevertheless, the same applies here as elsewhere when it comes to Asterisk: There is no perfect solution! You still need to build some functionality in a modular fashion. A good example is three-way calling. Asterisk does not include true three-way calling. To achieve it, you must take a regular conference and limit the number of participants to three.

### 14.1 Installation and the Timing Device

A default Asterisk installation such as the one we performed in the first chapter of this book isn’t able to handle conferencing. The problem is the lack of a timing device. To mix channel audio properly, Asterisk needs a stable and common clock source. For that clock source, there are two options:

> • **Telephony interface card and driver**

> Installing a hardware interface card (be it analog or digital ISDN) and its driver automatically provides Asterisk with a clock source.

> • **ztdummy module without hardware**

> If you neither have nor need a hardware interface card, you can use the ztdummy kernel module in combination with a 2.6 kernel.^([1](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos551476))

[1](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos551357). It is possible to make the ztdummy module work with a 2.4 kernel, but this assumes special USB hardware and is therefore not the best option.

To determine whether your Asterisk installation actually provides conferencing service, go into the Asterisk CLI and enter **`show application MeetMe`**. If the help text appears, conferencing is installed.

### 14.2 Defining Conference Rooms

In Asterisk, conferences always take place in virtual conference rooms. These must be defined in `/etc/asterisk/meetme.conf`, in the `[rooms]` context, and the syntax is simple and consistent with other Asterisk configuration files: `conf => room_number[,PIN][,administrator-PIN]`.

To create a conference room with the number 1234 that is freely available to any caller, make an entry in `meetme.conf` as follows:

> ![image](images/00215.jpg)

You can secure a conference room with an access number (sometimes called a personal identification number, or PIN). Suppose you want to add rooms 700 to 705, all with the same PIN 5678\. The `meetme.conf` would look like this:

> ![image](images/00216.jpg)

### 14.3 Access from the Dialplan

Conferences are accessed easily using the **`MeetMe()`** application. Say that any caller dialing 5555 is to be placed into the conference room 1234\. The corresponding dialplan entries would look like this:

> ![image](images/00217.jpg)

### 14.4 Announcing the Number of Conference Participants

The number of participants in the conference may be announced using the **`MeetMeCount()`** application:

> ![image](images/00218.jpg)

## 15\. External Control of Asterisk

One of Asterisk’s biggest advantages is the ability it gives the administrator to control it from the shell or through external applications.

### 15.1 asterisk -rx “command”

The simplest way to control Asterisk from an external shell or application is to issue the command **`asterisk`** with the option `-rx` followed by the CLI command. Any CLI command may be entered from the system shell in this fashion.

Say you want to see the dialplan for extension 23 in the context `[my-phones]`; you would do this with **`asterisk -rx "dialplan show 23@my-phones`**” entered in the shell:

> ![image](images/00219.jpg)

### 15.2 Call Files

Call files are like a shell script for Asterisk. A user or application writes a call file into `/var/spool/asterisk/outgoing`, where Asterisk processes it immediately.

> ### Tip
> 
> A **`mv`** (move) is an atomic operation (an operation which does not take effect until it is 100% complete) and as such is ideally suited for `.call` files (provided it is done on the same partition). With **`cp`** (copy), the file is copied line by line, which could lead to Asterisk processing an incomplete file.

#### 15.2.1 Making a Call Automatically

Let’s demonstrate the `.call` file principle with an example. Assume that we have a SIP phone registered with the number 2000 in Asterisk. In addition, we have the following extension in the dialplan:

> ![image](images/00220.jpg)

We create a call file called `a-test.call` in `/tmp` with the following content:

> ![image](images/00221.jpg)

Now we move this file with **`mv /tmp/a-test.call /var/spool/asterisk/outgoing/`**:

> root@molokai:~>mv /tmp/a-test.call /var/spool/asterisk/outgoing/

The following happens:

> • Asterisk polls the `/var/spool/asterisk/outgoing` for new call files and processes any it finds.

> • Asterisk opens a connection to device `SIP/2000`. If the device is in use or not answered, Asterisk tries two more times (see `MaxRetries`).

> • If someone answers `SIP/2000`, Asterisk begins processing extension `10` in the context `[call-file-test]`. In this case, Asterisk plays `hello-world` to the answering party.

When executing a call file, Asterisk compares the change time with the current time. If the change time is in the future, Asterisk ignores the call file. This is an easy way to implement time-based call files.

#### 15.2.2 Parameters

These parameters may be used in call files:

> • `Channel: <channel>`

> The channel upon which to initiate the call. Uses the same syntax as the **`Dial()`** command (see [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)”).

> • `Callerid: <callerid>`

> The caller ID to be used for the call.

> • `WaitTime: <number>`

> Number of seconds the system waits for the call to be answered. If not specified, defaults to 45 seconds.

> • `MaxRetries: <number>`

> Maximum number of dial retries (if an attempt fails because the device is busy or not reachable). If not specified, defaults to 0 (only one attempt is made).

> • `RetryTime: <number>`

> Number of seconds to wait until the next dial attempt. If not specified, defaults to 300 seconds.

> • `Account: <account>`

> The account code for the CDR.

> • `Context: <context>`

> The destination context.

> • `Extension: <exten>`

> The destination extension, in which dialplan execution begins if the device is answered.

> • `Priority: <priority>`

> The destination priority. If not specified, defaults to 1.

> • `Setvar: <var=value>`

> Lets you set one or more channel variables.

> • `Archive: <yes|no>`

> By default, call files are deleted immediately upon execution. If `Archive: yes` is set, they are copied into `/var/spool/asterisk/outgoing_done` instead. Asterisk adds a line to the call file that describes the result:

> Status: <Expired|Completed|Failed>

#### 15.2.3 Hotel Wake-Up Call Example

A hotel wants to implement a simple wake-up call system. Clients must be able to set a wake-up call by dialing *77*, whereupon they hear a prompt asking for the date and time of the wake-up call:

> ![image](images/00222.jpg)

### 15.3 The Asterisk Manager Interface

The Asterisk Manager Interface (AMI) is a powerful tool that lets external applications communicate with and control Asterisk.

Activate the AMI by setting `enabled=yes` in the `[general]` section in `manager.conf`

> ### Caution
> 
> Never do this on a publicly accessible server unless you have taken steps to protect it with packet filters such as **`iptables`**, **`ipfw`**, an external firewall, or an SSH tunnel. A malicious person could easily use it to take over your phone system.

#### 15.3.1 Creating an AMI User

To access AMI, we need to create a user account. To do this, we add a user entry called `admin` at the end of `manager.conf`:

> ![image](images/00223.jpg)

The options following `read` and `write` define the allowed command types for this user.^([1](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos566379))

[1](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos566273). Learn the rights levels needed for commands by entering **`manager show commands`** (or **`show manager commands`** in Asterisk 1.2) in the CLI.

> ### Caution
> 
> This generous rights assignment is for test purposes only! The `command` rights level means the user can stop Asterisk. As of Asterisk 1.4, it is even possible to make dialplan changes through the AMI, which also means it is possible to run shell commands with root privileges using **`System()`**.

#### 15.3.2 Talking to the AMI

After restarting Asterisk, we can connect to the AMI on port 5038 from the system shell using **`telnet`**:^([2](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos567729))

[2](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos567623). Here we use **`telnet`** as an interface only, and not in the traditional, interactive fashion.

> ![image](images/00224.jpg)

Now you can enter commands, usually consisting of multiple lines, by hand. For example:

> ![image](images/00225.jpg)

> ### Note
> 
> All command packets are closed with two carriage returns.

After entering the commands and closing them, you’ll receive a response:

> ![image](images/00226.jpg)

Of course, we are most interested in automating this interaction with scripts.

> ### Note
> 
> The Manager API is not exactly famous for its ability to handle multiple simultaneous connections gracefully (even though this has improved immensely in version 1.4). If you anticipate this kind of load, it is worth considering an AMI proxy, which can handle many connections and bundles them in a single connection. This is completely transparent to the script accessing the AMI. Of course, for the purposes of playing around, it isn’t strictly necessary.

Following a successful authentication, packets can be sent in both directions. The packet type is always determined by the first line. The client sends `Action` packets, the server answers with `Response` or can send `Event` packets. Otherwise the order of the lines in a packet is irrelevant. Lines are terminated with a carriage return (decimal ASCII 13) and line feed (decimal ASCII 10) (CR LF) combination. The entire packet is terminated with an additional CR LF combination. An AMI client normally sends a randomized but unique `ActionID` with every `Action`,^([3](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos570716)) which the server uses in its response for the purpose of managing overlapping packet streams.

[3](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos570516). This can be, for example, the name of the script, a timestamp, and a sequence number (e.g., `testscript.php-1169405408-1`).

The server sends the client `Event` packets, which can refer to any events; there are also events that occur as the result of a client-initiated `Action`. In this case, the server sends `Response: Follows` followed by the events (which will contain the `ActionID` of the initiating action) and a closing event (usually `actionnameComplete`).

If your client has no need for events, it can turn off these notifications by including `Events: off` in the authentication packet. Once set, the AMI sends only responses to actions initiated by the client.

The events that Asterisk sends are, as of this writing, effectively undocumented. You can find a list with sparse details at [www.voip-info.org/wiki/view/asterisk+manager+events](http://www.voip-info.org/wiki/view/asterisk+manager+events). A few additional explanations may be found at [http://asterisk-java.sourceforge.net/apidocs/net/sf/asterisk/manager/event/package-frame.html](http://asterisk-java.sourceforge.net/apidocs/net/sf/asterisk/manager/event/package-frame.html).^([4](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos572435))

[4](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos572329). This is primarily Asterisk-Java documentation.

#### 15.3.3 AMI Commands

The list of available commands can be called up in the CLI with **`manager show commands`** (or **`show manager commands`**), while information about a specific command can be obtained with **`manager show command`** *`command`* (or **`show manager command`** *`command`*):

> ![image](images/00227.jpg)

> ![image](images/00228.jpg)

These commands are almost always a direct translation of dialplan applications, except in the case of `Originate`, used to initiate an outgoing call, and `Command`, which executes a command directly on the CLI. Because our test user `admin` has all the rights levels (see above), he can execute all commands. The following example shows how we learn how a command is used:

> ![image](images/00229.jpg)

#### 15.3.4 Getting the Number of Voicemail Messages with Expect

Suppose we want to get the number of messages in a given voice mailbox via the Manager interface. This is easily done using an **`expect`** script. **`expect`** is an extended Tcl interpreter used for automating interfaces with interactive shell programs. (See **`expect`**’s home page at [http://expect.nist.gov](http://expect.nist.gov).)

The following **`expect`** script connects to the AMI, logs in, then returns the number of new and old messages in the specified mailbox:

> ![image](images/00230.jpg)

> ![image](images/00231.jpg)

We save the script as `vmcount.exp` and set it executable with **`chmod a+x vmcount.exp`**. We run it with the mailbox as an option and see how many messages we have:

> ![image](images/00232.jpg)

#### 15.3.5 StarAstAPI for PHP

A disclaimer: Keep your expectations modest. StarAstAPI hasn’t been actively maintained for some time.

There are now numerous, more-or-less good APIs for the AMI in a variety of programming languages (PHP, Perl, Python, Ruby, and so on), which we, because of space and time limitations, can’t explore here. You can find examples with comments at [www.voip-info.org/wiki/view/Asterisk+manager+Examples](http://www.voip-info.org/wiki/view/Asterisk+manager+Examples). If the API for your favorite language doesn’t work, we’re confident you can figure it out.

In this short example, we test the StarAstAPI (you can obtain this from [http://freshmeat.net](http://freshmeat.net) and other code repositories) in PHP, which assumes a PHP 5 that was compiled with `--enable-sockets`. You can check this from the shell with **`php -m`**.

(The API is easily ported to PHP 4, although the code is cluttered and poorly formatted.) When in doubt, just remedy the parse errors.

Unfortunately, the StarAstAPI *files still* contain the obsolete “short open tags” `(<?)`. If you encounter them, replace them with the correct syntax `(<?php)`. Four demo scripts are included with the API: `sLogin.php` attempts a login, `sCommand.php` executes `reload` on the CLI, `sDial.php` tries a connection to SIP/120, and `sEvents.php` receives events. (If you have followed the examples from [voip-info.org](http://voip-info.org), you will need to adapt the user name and password.)

If we connect to Asterisk using **`asterisk -vvvr`** and simultaneously run **`php -q sLogin.php`** to open a connection to the AMI using a deliberately incorrect user and password, we will see output like this on the CLI:

> ![image](images/00233.jpg)

This failed because the user did not exist, but the demo script still reports success:

> ![image](images/00234.jpg)

The response packet, however, will show the failure:

> ![image](images/00235.jpg)

The StarAstAPI is, as you can see, not completely clean, but is simple enough that it can be improved easily. If we call **`php -q sEvents.php`** (this time with the correct user) we see the following:

> ![image](images/00236.jpg)

As a test, we execute a `reload` in the CLI, which is reflected in the PHP script output:

> ![image](images/00237.jpg)

Give your creativity free reign! Write a small script that calls all your friends (in the middle of the night, of course).

#### 15.3.6 Getting the Number of Mailbox Messages with PHP

Let’s retrieve the number of mailbox messages for an account using PHP and StarAstAPI. Here is the PHP script:

> ![image](images/00238.jpg)

> ![image](images/00239.jpg)

We save this script as `vmcount.php` and make it executable with **`chmod a+x vmcount.exp`**, and then invoke it with the mailbox name as an option:

> ![image](images/00240.jpg)

### 15.4 The Asynchronous JavaScript Asterisk Manager

As of version 1.4, Asterisk comes packaged with a small web server called Asynchronous JavaScript Asterisk Manager (AJAM), which may be used to access the Asterisk Manager Interface (AMI) via HTTP. The name AJAM derives from AJAX (Asynchronous JavaScript and XML).

Setup assumes the steps from [section 15.3](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos564418) have been carried out, plus some additional parameters. You must set `webenabled` to `yes` in the `[general]` section of `manager.conf`. Pay attention to `httptimeout`, which defines the inactivity timeout after which the user is automatically logged out of the web interface. To activate the web server, set these parameters in `http.conf`:

> ![image](images/00241.jpg)

`enablestatic` need only be activated if the AJAM will be serving static files from `/var/lib/asterisk/static-http`. Normally you would set this to no, but it is needed for the purposes of the Asterisk-AJAM demo.

Don’t forget to restart!

> ### Warning
> 
> Our assessment is that it almost never makes sense to serve other web applications (that is, those intended strictly for administrator access) through the AJAM interface. It is also doubtful that it was intended to, because the rights assignments through `read` and `write` (see [Appendix E](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1497407), “[AMI Commands](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1497407)”) just don’t offer sufficient granularity. Always assume that a user can initiate actions other than those you have made available on the web page. It is much better to let your application use a PHP script containing only the specific AMI commands it needs to do its job, and to restrict the AMI rights for the accessing user as extra insurance.

#### 15.4.1 Getting the Number of Voicemail Messages with AJAM

Again, we are solving the problem addressed in the **`expect`** and PHP examples: We want to find out the number of messages in a specified mailbox. The AJAM offers us a few ways to do this.

##### *15.4.1.1 HTML*

The AMI waits for queries at

> http://localhost:8088/asterisk/manager

Packet fields are tacked on the end of the URL. Try these addresses in your web browser:

> ![image](images/00242.jpg)

The response follows in the form of an HTML page, so it’s not really suitable for access via a script.

##### *15.4.1.2 Plain Text*

If we replace `manager` in the URL with `rawman`, we get plain text output. To log in and get a message count from the mailbox, just enter the following:

> ![image](images/00243.jpg)

This text output is more script friendly.

##### *15.4.1.3 XML*

If we want XML instead, we call `mxml` instead. The XML output is presented formatted for better readability. In practice, AJAM does not put line breaks inside the XML tags. Either way, a compliant XML parser won’t care.

> ![image](images/00244.jpg)

#### 15.4.2 AJAX and AJAM Considerations

AJAX applications (as the name Asynchronous JavaScript and XML might suggest) use XML as the standard format, even though it is often criticized for its bloated structure. There are alternatives, such as JSON, for example. JSON (JavaScript Object Notation) is (the name gives it away) well suited for JavaScript applications, because the data structure can be converted into an object natively and with little overhead using **`eval()`**. There are countless implementations for PHP, Perl, and so on, but a JSON implementation for AJAM does not yet exist. One can, however, convert the plain-text output into JSON on the client side, if that turns out to be easier or if it’s easily done using available JavaScript libraries. Here’s an example to get you thinking:

> ![image](images/00245.jpg)

##### *15.4.2.1 Ping*

When accessing the AJAM with an AJAX application, the **`ping`** command is particularly useful for keeping authenticated connections alive:

> ![image](images/00246.jpg)

##### *15.4.2.2 AJAM Demo*

A small sample application demonstrating AJAM access may be run at

> http://localhost:8088/asterisk/static/ajamdemo.html

This uses the highly practical JavaScript library prototype ([www.prototypejs.org](http://www.prototypejs.org)) for AJAX access and displays to get the `Status` of the currently active channels. You can use the AJAM demo as a basis for your own AJAX applications.

##### *15.4.2.3 Apache*

The Asterisk web server is a minimal implementation and cannot be seen as a wholesale replacement for a “proper” web server that can run PHP scripts or use modules, such as Apache. To unify a system that uses both, you can use Apache as a proxy for AJAM by adding

> ProxyPass /ajam http://localhost:8088/asterisk

in the appropriate place in `httpd.conf`, so that all requests for `/ajam` are passed on to AJAM instead of being served by Apache.

## 16\. Asterisk Gateway Interface

The Asterisk Gateway Interface (AGI) may be compared with CGI (Common Gateway Interface) on a web server. These are external programs called from the within the dialplan (`extensions.conf`). AGI scripts can interact with Asterisk and execute commands. In principle, an AGI script may be written in any programming or script language that can use the UNIX system sockets. The following are simply implementation examples. For a command reference, see [Appendix D](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1447342), “[AGI Commands](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1447342).”

### 16.1 Data Streams

To use AGI scripts, understanding the UNIX system’s data stream model is an absolute requirement. You can find more information about this model in [Appendix D](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1447342).

#### 16.1.1 STDIN

The AGI script receives some information from Asterisk via standard input (STDIN). The format looks like this:

> ![image](images/00247.jpg)

This is followed by an empty line, by which Asterisk indicates to the AGI script that the transmission is complete.

Here is a list of all the headers Asterisk can transmit via AGI:

> • `agi_request`

> The filename of the called AGI program

> • `agi_channel`

> The channel

> • `agi_language`

> The language (e.g., `en` for English or `de` for German)

> • `agi_type`

> The channel type (e.g., `sip` for SIP or `zap` for ISDN)

> • `agi_uniqueid`

> The unique ID for this call

> • `agi_callerid`

> The caller ID (e.g., `Charlie Farquharson <2000>`)

> • `agi_context`

> The originating context

> • `agi_extension`

> The originating extension

> • `agi_priority`

> The current priority in the extension

> • `agi_accountcode`

> Account code

> • `agi_calleridname`

> Name field from the caller ID (e.g., `Jerry Lewis`)

> • `agi_callingpres`

> Caller ID in the ZAP channel

#### 16.1.2 STDOUT

Once the AGI script has received information from Asterisk, it issues commands via standard out (STDOUT) back to Asterisk. To monitor this communication, enter **`set verbose 5`** in the CLI to increase the verbosity level.

#### 16.1.3 STDERR

Standard error (STDERR) is the stream used to bring error or debug messages to the Asterisk console (CLI).

### 16.2 Examples in Various Programming Languages

By default, Asterisk looks for AGI scripts in `/var/lib/asterisk/agi-bin`.

Ensure that Asterisk is actually allowed to run the script you want it to run. You can guarantee this with the system shell command **`chmod 755` *`script_name`***.

AGI scripts are called by the **`AGI()`** application, like so:

> ![image](images/00248.jpg)

A few AGI programs in various programming languages are described below.

#### 16.2.1 Perl

The standard Asterisk install comes packaged with a test AGI script called `agi-test.agi`^([1](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos598078)) located in the `/var/lib/asterisk/agi-bin` directory. Through this sample, we’ll explain how AGI scripts work.

[1](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos597822). The .agi extension is not strictly necessary. You could name the file agi-test.pl if so desired.

The script is called in `extensions.conf` as follows:

> ![image](images/00249.jpg)

Here we describe the operation by line or section.

> ![image](images/00250.jpg)

The first line indicates to the shell that this is a Perl script and is to be run by the Perl interpreter located at `/usr/bin/perl`. The directive `use strict` tells the interpreter to force the declaration of variables before use and to handle subs and strings in a way that prevents confusion:

> $|=1;

This short line tells Perl not to buffer text. This ensures that any output is passed to Asterisk immediately:

> ![image](images/00251.jpg)

Variables are defined here. The hash `%AGI` accepts the initial inputs from Asterisk. The remaining variables count the total number of tests, the number of failed tests, and the number of passed tests:

> ![image](images/00252.jpg)

The values which have just been stored are fed to STDERR for debugging purposes, and then passed to the CLI:

> ![image](images/00253.jpg)

Then comes the `checkresult` subroutine:

> ![image](images/00254.jpg)

The `checkresult` subroutine reads the result of a command to Asterisk and determines whether that test was successful. The variables `$fail` and `$pass` are incremented depending on the result. After this basic function has been established, the individual tests can proceed. The `beep.gsm` sound file is played:

> ![image](images/00255.jpg)

The text hello world is transmitted to the caller. This works only if the protocol and the device support text:

> ![image](images/00256.jpg)

The image `asterisk-image` is transmitted to the caller. This is also protocol and device dependent:

> ![image](images/00257.jpg)

The number 192837465 is played to the caller:

> ![image](images/00258.jpg)

This command waits for dual-tone multi-frequency (DTMF) input from the caller for 1,000ms:

> ![image](images/00259.jpg)

A 3,000ms GSM file named `testagi.gsm` is recorded. Recording can be interrupted by the caller by pressing 1, 2, 3, or 4:

> ![image](images/00260.jpg)

The resulting sound file is played back:

> ![image](images/00261.jpg)

Finally, output is sent to the CLI indicating how many tests succeeded and failed:

> ![image](images/00262.jpg)

> ### Warning
> 
> In many AGI commands you will see the following construction:
> 
> > ![image](images/00263.jpg)
> 
> The indicated part of this line (between `$value` and `)`;) is an absolute requirement, to ensure that the command is executed correctly. This is because we have an empty argument established by two double quotes, which must be escaped. The entire command is closed with a line feed, `\n`.

#### 16.2.2 PHP

PHP has become one of the most popular programming languages for web applications. Because current versions of PHP support calling applications from the command line, it is also well suited for AGI scripts. To demonstrate this, we’ll use a small PHP program (`lotto.php`), which chooses 6 random numbers from 1 and 49 and plays them back to the caller. A description of the individual steps follows in the program code here:

> ![image](images/00264.jpg)

> ![image](images/00265.jpg)

> ![image](images/00266.jpg)

The `lotto.php` program must be saved in `/var/lib/asterisk/agi-bin` and is called from `extensions.conf` as follows:

> ![image](images/00267.jpg)

If you use PHP with AGI but don’t want to reinvent the wheel, you can use the ready-made phpAGI PHP class. You can find the required files and more information on the project home page at [http://phpagi.sourceforge.net](http://phpagi.sourceforge.net).

The following program, which is provided with phpAGI, will give you a quick overview of the function calls.^([2](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos606572))

[2](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos606466). To use `text2wav`, you need to have a text-to-speech system (e.g., Festival) installed.

> ![image](images/00268.jpg)

#### 16.2.3 Ruby and Adhearsion

Although Ruby is an older (by IT standards) programming language, it has grown tremendously in popularity in the past few years, mainly as the result of Ruby on Rails ([http://rubyonrails.org](http://rubyonrails.org)). Adhearsion ([http://adhearsion.com](http://adhearsion.com)) is a kind of Ruby on Rails for Asterisk. The subject is exciting and deep enough that one could write a dedicated book on it. In the future, we will try to expand and update the coverage of Adhearsion on this book’s website.

##### *16.2.3.1 Installation*

Like any good open source project, Adhearsion has fragmented and occasionally incomplete documentation. Fortunately, the installation is relatively easy because there is a Ruby *gem* available. (For Ruby Newbies, gem is Ruby’s package management system.) Installing Adhearsion is just a matter of entering **`gem install adhearsion`** in the system shell.

##### *16.2.3.2 Easy Setup*

When you use Adhearsion, the Asterisk dialplan becomes short and easy to read. Each inbound context needs only the following line:

> exten => _.,1,AGI(agi://127.0.0.1)

With this line, Adhearsion takes over control of all calls happening in this context. You can, of course, mix a traditional dialplan with Adhearsion if you want.

An Adhearsion application has to be generated first, just as in Ruby on Rails. This is done with the `ahn` program, called with **`ahn create application_name`**, as follows:

> ![image](images/00269.jpg)

The application is then started with **`ahn start`** . (And, yes, this command ends with the blank space, as shown here and in the following code snippet.)

> ![image](images/00270.jpg)

From this point forward, Adhearsion can control calls. You can monitor progress on the screen.

##### *16.2.3.3 Sample Program*

The Adhearsion dialplan, or rather the Ruby program, is defined in `dialplan.rb`. Here is a simple example:

> ![image](images/00271.jpg)

`internal` is, in this example, the context from which Adhearsion was called.

#### 16.2.4 Other Programming Languages

Remember, you can write AGI programs in any language. There are already libraries for many of the most popular languages, including the following:

> • Java

> • Perl

> • PHP

> • Python

> • Ruby

> • C

The easiest way to start is with a web search using the keywords AGI and the name of the language you want to use.

## 17\. Fax Server

Many attempts have been made to cleanly integrate Asterisk with faxing, with inconsistent results. For a long time, app_rxfax, available at [www.soft-switch.org](http://www.soft-switch.org) was the accepted convention. Unfortunately it is error prone and unreliable. Faxes often arrive piecemeal, or worse, not at all.

For that reason, we describe a more robust solution using IAXmodem here (see [http://iaxmodem.sourceforge.net](http://iaxmodem.sourceforge.net)).

The IAXmodem application emulates a fax modem, which may be operated by a fax application of the administrator’s choosing. We’ll use the popular Hylafax. For simplicity and consistency, the installation platform will be the same Debian Linux and Asterisk 1.4 we have used for the other examples (see [Appendix A](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos679664), “[Installation Instructions for Asterisk 1.4](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos679664)”).

### 17.1 Installing IAXmodem

IAXmodem simulates a fax modem and makes it available to Asterisk via IAX2\. All the steps in this chapter must be performed as the root user.

To install IAXmodem, we need some additional Debian packages, which may be installed with the command **`apt-get -y install g++ libtiff-tools libtiff4 libtiff4-dev`**.

> ![image](images/00272.jpg)

We switch into the appropriate directory with **`cd /usr/src`** to install the IAXmodem source code:

> ![image](images/00273.jpg)

The sources for IAXmodem can be downloaded with any typical web browser from [http://iaxmodem.sourceforge.net](http://iaxmodem.sourceforge.net) (the version used in this example is 0.3.0). After downloading the archive, copy it to `/usr/src` and unpack it with **`tar -xvzf iaxmodem-0.3.0.tar.gz`**:

> ![image](images/00274.jpg)

Change into the unpacked directory with **`cd iaxmodem-0.3.0:`**

> ![image](images/00275.jpg)

Now compile the sources with **`./configure && make`**:

> ![image](images/00276.jpg)

Copy the resulting binary into `/usr/bin` with **`cp iaxmodem /usr/bin/`**:

> ![image](images/00277.jpg)

#### 17.1.1 Configuring IAXmodem

Now we can configure the modem. IAXmodem expects to find configuration files in `/etc/iaxmodem`. Create it with **`mkdir /etc/iaxmodem`**:

> ![image](images/00278.jpg)

Create the configuration file with **`touch /etc/iaxmodem/ttyIAX0`**:

> ![image](images/00279.jpg)

This file must contain the following parameters:

> • `device`

> The device node to be created in `/dev`. This is the device Hylafax uses to connect to IAXmodem. You can choose any name you like, but we prefer to adhere to the convention and so choose a device name appropriate for a serial interface, ttyIAX0.

> • `owner`

> This is the owner of the device (in the form *`user:group`*). It is best to use the same user and group under which Hylafax runs.

> • `port`

> The port that IAXmodem listens on. Asterisk uses 4569 to listen for IAX2 connections, so you must choose something else (e.g., 4570).

> • `refresh`

> This sets how long IAXmodem waits between registrations with Asterisk. If this number is 0, the modem does not register at all.

> • `server`

> IP address of the server running Asterisk. If this is on the same machine as IAXmodem, use the localhost address 127.0.0.1.

> • `peername`

> The name under which IAXmodem registers with Asterisk.

> • `secret`

> The password used for Asterisk registration.

> • `codec`

> The codec used by IAXmodem. Allowed codecs are `alaw`, `ulaw`, and `slinear`. Compressed codecs are not appropriate for faxing; fax transmissions are themselves compressed and don’t tolerate further compression; moreover, most compressed codecs are lossy and a fax transmission will not tolerate losses. This is one of the major reasons why faxing over VoIP remains problematic.

Using an appropriate editor (e.g., vi), we write the following configuration in the file `/etc/iaxmodem/ttyIAX0:`

> ![image](images/00280.jpg)

IAXmodem is now configured and can be started. The best way to do this is with **`init`**. Add a line to start IAXmodem to `/etc/inittab` with **`echo "IA00:23: respawn:/usr/bin/iaxmodem ttyIAX0" >> /etc/inittab`**:

> ![image](images/00281.jpg)

The device name ttyIAX0 is the same device name as specified in `/etc/iaxmodem`.

#### 17.1.2 Configuring faxgetty and Logging

To receive faxes, we need a getty that listens for connections on the IAXmodem. This is accomplished through an additional entry in `/etc/inittab`. Add it with **`echo "mo00:23:respawn:/usr/sbin/faxgetty ttyIAX0" >> /etc/inittab`**:

> mo00:23:respawn:/usr/local/sbin/faxgetty ttyIAX0

Create a log directory for IAXmodem with **`mkdir /var/log/iaxmodem/`** and the log files with **`touch /var/log/iaxmodem/ttyIAX0`** and **`touch /var/log/iaxmodem/iaxmodem`**:

> ![image](images/00282.jpg)

To make sure everything will start as expected at boot time, reboot the system with **`shutdown -r now`**:

> ![image](images/00283.jpg)

### 17.2 Installing Hylafax

We’ll install Hylafax from the Debian Repository to simplify installation. Do this with **`apt-get -y install hylafax-server.`** Dependencies are automatically resolved:

> ![image](images/00284.jpg)

The next step is the configuration of the fax server. Do this with **`faxsetup`**:

> ![image](images/00285.jpg)

Simply press Enter after the following 2 or 3 questions:

> ![image](images/00286.jpg)

We confirm restart of the server processes with `yes` and are asked if we want to install a modem. Our IAXmodem is already set up so we can proceed and confirm again with `yes`.

Specify the modem and confirm with Enter:

> ![image](images/00287.jpg)

Many questions follow, but only a few of them are really important. This is where you set international dialing codes, the fax number, country and area code, and the CSID (call subscriber ID), which is printed on the top line of the fax page on the receiver’s end. Confirm with `yes`.

> ![image](images/00288.jpg)

A confirmation page follows where you can double-check your entries:

> ![image](images/00289.jpg)

Answering `yes` brings us to modem detection:

> ![image](images/00290.jpg)

> ![image](images/00291.jpg)

The modem was detected and we are asked if it is a Class 1 modem, and we confirm this because it is exactly what we want. The default reset commands are also acceptable. Confirm with `yes`.

Answer the first question In the next dialog with `no`, because we don’t need to configure any further modems. The second question is confirmed with by pressing Enter, which starts the fax server:

> ![image](images/00292.jpg)

Hylafax is now configured for sending faxes.

### 17.3 Receiving Faxes

Our fax solution still has to be integrated into Asterisk. To do this, we configure the IAXmodem as an IAX2 peer by adding a section to `/etc/asterisk/iax.conf`:

> ![image](images/00293.jpg)

Global settings are defined in the `general` section. In this example we are binding the standard IAX2 port of 4569\. The `bindaddr` defines the IP address (and thereby the interface) on which the IAX2 channel driver listens for connections; in this case, it is set to listen on all interfaces.

The IAXmodem is set to type `friend`, which allows both incoming and outgoing connections. The `secret` and `port` parameters match those in the IAXmodem configuration we did above, and `context` defines the entry context for outgoing connections.

Enter **`iax2 show peers`** in the Asterisk console to see our new IAXmodem:

> ![image](images/00294.jpg)

We are, of course, not done yet. Asterisk still needs an extension so that it knows what to do with an incoming fax. Our objective is to ensure that any incoming faxes are passed on to Hylafax. In this example, we assume that all faxes come in through a SIP provider. A real configuration will have to reflect the installation and account settings of the SIP provider you use; for the sake of example, a configuration in `sip.conf` might look like this:

> ![image](images/00295.jpg)

The corresponding context in `extensions.conf` would look like this:

> ![image](images/00296.jpg)

Any faxes coming in will now be routed to Hylafax via IAXmodem and ultimately e-mailed to the user address defined in the `faxmaster` alias.

> ### Note
> 
> By default, Hylafax saves incoming faxes in `/var/spool/hylafax/recvq`.

### 17.4 Sending Faxes

The next obvious step is configuring our system to send faxes. Here, too, we need a context (this time it is `[fax-out]`) in `extensions.conf`. If IAXmodem wants to send a fax, it will automatically land in this context. If the faxes are to go out our hypothetical SIP connection 123456, the entry in `extensions.conf` will look like this:

> ![image](images/00297.jpg)

We can test sending of faxes with **`sendfax -n -d <faxnumber> <file.txt>:`**

> debian:~# sendfax -n -d 6045557977 /etc/issue.net

We should see this in the CLI:

> ![image](images/00298.jpg)

If we issue the command **`faxstat -s`** during the transmission, we will see the following:

> ![image](images/00299.jpg)

Done! Now you can send and receive faxes via Asterisk using Hylafax.

The Hylafax website, [www.hylafax.org](http://www.hylafax.org), has numerous examples and how-tos that will help you integrate your Hylafax installation with your existing office infrastructure effectively.

### 17.5 Sending Received Faxes as E-Mail

The following steps illustrate how we can configure Hylafax to transmit incoming faxes to a predefined e-mail address.^([1](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos632604))

[1](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos632498). Our example assumes a properly configured MTA (e.g., Sendmail, Postfix, or a lightweight SMTP engine such as ssmtp).

The recipient will receive the fax as an e-mail attachment.

To do this, the configuration file `/var/spool/hylafax/etc/FaxDispatch` must contain the following parameters:

> • `SENDTO`

> The destination e-mail address for incoming faxes.

> • `FILETYPE`

> The format of the attachment. In addition to `pdf`, `tiff` (Tagged Image File Format) and `ps` (Postscript) are also acceptable options.

The parameters are set with an equal sign, just as in Asterisk configuration files:

> ![image](images/00300.jpg)

After the file has been saved, you must restart the fax server with **`/etc/init.d/hylafax restart`**:

> ![image](images/00301.jpg)

We can test e-mail transmission by sending ourselves a fax with **`sendfax -n -d <faxnumber> <file.txt>`**:

> debian:~# sendfax -n -d 6045557977 /etc/issue.net

After a short time, your target e-mail address should receive an e-mail in the following format:

> ![image](images/00302.jpg)

The attachment will be a PDF file. In this example, the PDF is named `fax000000016.pdf`.

Now you can not only send and receive faxes, but received faxes are also received as e-mail attachments.

## 18\. Busy Lamp Field, Hints, Pickup

*Philipp Kempgen*
*Stephen Bosch*

The Busy Lamp Field, or BLF, is a common feature of many modern telephone systems. The BLF can be colored LED lamps or LCD indicators that allow a user to monitor the status of other users on the system, almost always next to a button that performs an operation on the monitored station depending on the status of the indicator. Although it is most frequently seen at reception switchboards, it can also be found on regular desktop sets.

The indicator tells the operator the status of the line. A line can have many states:

> • Ringing

> • Busy or “in use” (which usually includes active “Do not disturb” states)

> • On hold

> • Available

The states can be indicated with LED lights (which may change color or blink, depending on the state) or LCD icons (which change appearance; for example, by providing a “do not enter” sign for a line that is in use). Not all models of telephone provide all the states.

If the system is so configured, the button can be configured to “pick up” a call when a station is ringing. (For some sets, this is done by entering a feature code.)

We cover the configuration of these features for Asterisk and a selection of SIP phones here.

### 18.1 Controlling Indicators

The BLF is implemented through hints and subscriptions. A hint tells Asterisk to monitor the state of a SIP channel. SIP devices can subscribe to those hints, and when the state changes, Asterisk sends an event package to the subscribed devices to inform them of the state change.

#### 18.1.1 sip.conf

To make BLF work, some additional entries must be added to the `[general]` section of `sip.conf`:

> ![image](images/00303.jpg)

Individual SIP accounts need the entries `subscribecontext` and `call-limit`. The first, `subscribecontext`, tells Asterisk which context to check whether this user wants to subscribe to the hint of another user. Most often, this is the same as the context for all the other internal users. The second, `call-limit`, limits the number of simultaneous calls that this user is allowed (when this is greater than zero). This is important because it tells Asterisk how to set the state of the station in question. For example, if the call limit is set to 2, and the station has an active call, Asterisk will treat the station as available. If there are already two active calls, then Asterisk treats the station as busy. A setting of at least 2 is best; lower settings can cause problems with call transfers.

For call pick-up functions, the additional parameters, `callgroup` and `pickupgroup` are important. For example, a SIP user with `pickupgroup=2` can only pick up calls from other users with `callgroup=2`. This can be used to manage rights; because there are only 64 possible groups, however (0 to 63), this works in small to medium environments only. For larger installations, all the users are set to the same group and rights are handled through another mechanism. (We hint at how later.)

> ![image](images/00304.jpg)

#### 18.1.2 Hints

Asterisk does not know how to correlate dialplan extensions to specific users or devices unless we tell it how. This is done in the dialplan using *hints.* If you want to think in terms of dialplan priorities, a hint is a special kind of priority that precedes priority 1\. The hint for a device must be in the same context as that specified in `sip.conf` using `subscribecontext`, or the status information will not be relayed. This is to prevent a station from monitoring all the other stations without permission.

The following examples show how to define hints. Here is a simple example in `.conf` format:

> ![image](images/00305.jpg)

The same is accomplished in AEL like this:

> ![image](images/00306.jpg)

Let’s take a look at the typical example of a group of extensions beginning with a common digit, here in `extensions.conf`:

> ![image](images/00307.jpg)

In `extensions.ael`, the same dialplan section would look like this:

> ![image](images/00308.jpg)

You may want to try using patterns to reduce the maintenance overhead for your dialplan. Unfortunately, in Asterisk 1.4, this doesn’t work.

> ### Warning
> 
> In Asterisk 1.4, hints may not use patterns, so these hints would not be allowed (`extensions.conf, extensions.ael` respectively):
> 
> > ![image](images/00309.jpg)
> 
> As of Asterisk 1.6, you can use patterns in this way, although the early implementations were buggy. Be careful, however: When hints are processed, there is no channel yet, so no channel variables will be available for the hint definition to use (with the exception of `${EXTEN})`.

You can also combine multiple users in a single hint, as in this example:

> ![image](images/00310.jpg)

To accomplish the same thing in `extensions.ael`, a similar pattern is followed:

> ![image](images/00311.jpg)

> ### Tip
> 
> You can also place all your hints in a dedicated context and then `include` it if you need it in another context.

You must reload the dialplan in order to apply hints (**`asterisk -rx 'module reload'`**).

### 18.2 Subscriptions

This section provides the technical background for subscriptions for those who are interested. It’s not really required for configuration purposes. If you just want to configure your phones, proceed to the next section.

SIP provides more than one method for subscribing to a station’s status. The customary method is described in RFC 4235, “Dialog Event Package,” which is based on RFC 3265, “SIP Event Notification.” With this method, a monitoring device sends a separate `SUBSCRIBE` message to the phone system for each station it wants to monitor. The system replies with a `NOTIFY` message whenever the status of subscribed station changes. (Asterisk does not yet support `PUBLISH`.)

The main difference between the subscription standards is the XML they use in the body of the notification. The standards supported by Asterisk are described in [Table 18.1](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos646144).

**Table 18.1** Subscription Methods Supported by Asterisk

![image](images/00312.jpg)

The `xpidf+xml` and `cpim-pidf+xml` formats are very similar.

### 18.3 Configuring Telephones for BLF

To actually use BLF, you have to configure BLF on the phone you want to use for monitoring. This will vary for every model of phone you use. We briefly cover two commonly used phones here, to get you started. Be warned that the firmware, and thus the configuration parameters, can change at any time. For the last word, consult the documentation for the phone you are configuring.

> ### Note
> 
> *Central provisioning* is the term used for configuration of telephones through configuration files distributed through a central server, whether by TFTP, FTP, HTTP, or some other means. The setup for central provisioning is beyond the scope of this chapter. Because central provisioning is a very common way to configure phones and an absolute must for large installations, most manufacturers provide instructions for this in the administration guide (as opposed to the user’s guide) for the phone.

#### 18.3.1 BLF on the Aastra 480i

Aastra telephones, like most IP telephones, can be configured via a web interface or through a configuration file, which the phone loads from a configuration server (nearly always the Asterisk server itself).

##### *18.3.1.1 Configuring via a Web Browser*

Find the IP address for the phone. You can do this on the phone by pressing the Options key and scrolling to Network Setup. (The default password is 22222.)

Enter the IP address into a web browser on a computer on the same network. When you do this, you’ll be prompted for a username and password. By default, the username is admin, and the password is 22222. Once you are logged in, click Softkeys and XML in the Operation section of the configuration menu on the left. [Figure 18.1](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos649155) shows the Softkeys Configuration page.

**Figure 18.1** Aastra 480i Busy Lamp Field web configuration.

![image](images/00313.jpg)

Choose the key you would like to configure and set the type to BLF. The Aastra phones automatically condense softkeys on the idle screen. For example, if you only configure key 5, it will appear as key 1 on your phone.

The Label field sets the display name for the BLF, and the value is the number of the extension you want to monitor. The check boxes on the right (Idle, Connected, Incoming, and Outgoing) determine in which states the key will display. (This is because the keys can be set to perform a variety of functions and you may not need them in every state.) The defaults usually suffice.

Once you have entered all the BLF settings you want, you have to save the settings before restarting the phone. The Save Settings button is in the lower-left corner of the window. (It’s not visible in the figure above because you have to scroll down to see it.) Restart the phone by going to Operation on the left and clicking Reset and then Restart.

##### *18.3.1.2 Configuring with a Configuration File*

Another way to configure BLF is by provisioning the phone through a central server.

Aastra phones can be configured globally through the `aastra.cfg` file, or on a per-phone basis through a configuration file with a filename containing the phone’s MAC address, as in, for example, `00085D1840D1.cfg`.

An example BLF configuration for an Aastra 480i would look like this:

> ![image](images/00314.jpg)

Note that this is not the entire configuration file. Although you can put these lines wherever you want in the file, it makes sense to keep them together for clarity.

You need at least three parameters in the configuration file to activate BLF; four are listed here. All the parameters are preceded by *softkeyN*, where *N* is the number of the softkey:

> • `type`

> This sets the key type. Aastra sets have highly configurable softkeys. You need to specify what type of function you want the key to perform. In this case, we want the type `blf`, as in this example:

> softkey1 type: blf

> • `label`

> This sets the display name for the softkey. You can set it to whatever you like, but generally this is set to the name of the user whose phone you want to monitor. This is a short field which can only contain up to 9 characters. You must enclose it in quotes:

> softkey1 label: "S. Smart"

> • `value`

> Sets the extension you want to monitor, usually by number:

> softkey1 value: 112

> • `line`

> You can specify a line number for the softkey; softkeys configured in this way will automatically dial the monitored extension when pressed.

> softkey1 line: 2

#### 18.3.2 Polycom Soundpoint IP 501

You can only configure Busy Lamp Field on the Soundpoint IP 501 through central provisioning. On Polycom phones, BLF is called Buddy Watch.

> ### Warning
> 
> The Polycom phones use XML configuration files. You must be extremely careful with spacing and formatting when editing these files. All tags must be closed; typographical errors, extra lines, and extra spaces have been known to cause boot problems.

The BLF is a phone-specific setting made in the directory file for the phone you want to configure. The filename for the directory file follows the convention `mac_address-directory.xml`. For example, `0004f2047ff5-directory.xml` is a valid directory filename. A directory file with presence configured for two extensions might look like this:

> ![image](images/00315.jpg)

All the fields for a given entry must be enclosed in the `<item></item>` tags. These are the fields you’ll need to set:

> • `<ct>extension</ct>`

> This sets the extension you want to monitor and is usually a number:

> <ct>201</ct>

> • `<sd>number</sd>`

> This sets the speed dial number for the entry. The Soundpoint IP 501 has three line buttons, which can be line appearances, speed dial buttons, or BLF indicators. Line appearances always take priority. For example, if you configure three line appearances, no buttons or fields will remain on the idle screen for BLF (although you can still check the states of monitored extensions by pressing the Buddies softkey). If you have a single line appearance, it will occupy the first button. If you set `<sd>` to 1, the entry will occupy the next available line button.

> • `<bw>[0,1]</bw>`

> This is the Buddy Watch parameter (essentially, another Polycom name for BLF). Allowed values are 0 and 1\. If this is set to 1, the extension specified in `<ct></ct>` will be monitored. When this is set, the Buddy icon appears next to the button if the line is available; the Do Not Enter icon appears when the line is in use for any other reason.

> • `<bb>[0,1]</bb>`

> This is the Buddy Block parameter. Allowed values are 0 and 1\. If this is set to 1, it blocks the extension defined in this entry from monitoring this phone.

Configuring BLF for SIP phones is generally straightforward. The different terminology used by different phone manufacturers can be a source of confusion. Equivalent terms include *presence, buddy watch, extension monitoring,* and *subscription.* As with all the hardware-specific examples, consult with the manufacturer’s documentation if you are not sure. Things change frequently.

### 18.4 Testing the Hints

Now we can test to see that things are working.

> ### Note
> 
> Output in the following examples has been truncated to save space.

Enter **`core show hints`** in the Asterisk CLI:

> ![image](images/00316.jpg)

We can see that extensions we want to monitor (`SIP/21` and `SIP/22`) have not yet contacted the Asterisk server (`"Status: Unavailable"`), nor have the monitoring extensions subscribed to the hints for the unavailable extensions (`"Watchers 0"`). We can confirm this with an additional command, **`sip show subscriptions`**:

> ![image](images/00317.jpg)

Once the monitoring extension has contacted the server, we run the command again:

> ![image](images/00318.jpg)

Now we can see that extension 21 is monitoring extension 22\. Once the extension 22 contacts the Asterisk server, we will see this in the CLI:

> Extension Changed 22 new state Idle for Notify User 21

Now we enter **`core show hints`** again:

> ![image](images/00319.jpg)

In contrast to the first output of this command, we can see that the phones have a defined setting (Idle) and at least one phone is monitoring extension 22 (Watchers 1). Configuration is now complete, and Asterisk will send an event to the monitoring extensions as soon as the monitored extension changes state. How this is manifested will depend on the phone. Some phones have an icon on an LED display, others have LED indicators that blink, change color, or both. Status changes are also reported in the CLI:

> ![image](images/00320.jpg)

### 18.5 Configuring Pickup

The Busy Lamp Field only tells us the status of a monitored extension, but it doesn’t let us do anything about it. If we want to be able to pick up a call intended for another extension, we have to do some additional configuration.

There are two basic kinds of call pickup. Pickup of calls for a single user is sometimes called *directed pickup;* pick up of calls for a call group is known as *group pickup.* Let’s start with the directed pickup, which is simpler.

#### 18.5.1 extensions.conf for Pickup

We need to add additional entries to `extensions.conf` to make pickup work:

> ![image](images/00321.jpg)

To accomplish the same thing in `extensions.ael`, we make the following entries:

> ![image](images/00322.jpg)

Now we have defined an Asterisk extension that picks up a call to *<extension>* in the `internal-users` context if `*8`*<extension>* (e.g. `*821`) is dialed, provided that `<extension>` (e.g., 21) is ringing but has not yet been answered. (See also [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029).”)

> ### Warning
> 
> The **`Pickup()`** application should not be confused with similar applications packaged with bristuff (such as **`PickUp()`**, **`DPickup()`**, **`PickUp2()`**). You might find these in the form of patches when doing Internet searches on the topic.

#### 18.5.2 Configuring the Phones for Pickup

Some phones support BLF + directed call pickup. In this configuration, when a monitored phone is ringing, the user can pick up the call simply by pressing the adjacent associated button. We will set this up here. Because Polycom sets do not support BLF + directed call pickup with Asterisk, we provide only the Aastra instructions.

> ### Tip
> 
> This behavior can be replicated on Polycom phones by having Asterisk do the state detection. In such a scenario, if the device is idle, dialing the extension will ring the extension. If the extension is already ringing, and a phone in the correct context dials it, that phone will pick up the extension. This way, the button adjacent to the “watched buddy” can be used to do call pickup, even though it is simply a speed dial button.

Early on, Aastra sets relied on the SIP subscription event package to determine what to dial in order to do call pickup. This meant that, in theory, it was only necessary to enable directed call pickup in the web configuration to make this feature work.

Unfortunately, Asterisk does not transmit this information by default. To do this, Asterisk must be patched using the patch provided at [https://issues.asterisk.org/view.php?id=5014](https://issues.asterisk.org/view.php?id=5014). This is still an option for you if recompiling and installing Asterisk is not too bothersome; then you need only to activate directed call pickup in the Aastra web configuration. Log in to the phone, find Basic Settings on the left, and click Preferences. Scroll to the bottom of the screen and find the Directed Call Pickup Settings section. Check the box next to Directed Call Pickup to enable it, as shown in [Figure 18.2](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos666960).

**Figure 18.2** Activating directed call pickup on the Aastra 480i.

![image](images/00323.jpg)

Click Save Settings, then restart the phone by going to Operation on the left, clicking Reset and then Restart.

Another way to do this, which does not require patching and recompiling Asterisk, is to tell the Aastra phone what the pickup prefix is. Currently, this can be done only via the Aastra configuration file, not through the web interface. For the purposes of our example, add the following lines to the configuration file (as mentioned before, in the form `mac_address.cfg`):

> ![image](images/00324.jpg)

Force the phone to restart so that it loads the configuration. Pressing the softkey associated with the BLF indicator of a ringing extension should now pick up the call.

#### 18.5.3 Configuring Group Pickup

Group pickup is very similar in operation to directed call pickup. One way is to make pickup extensions, such as in this example:

> ![image](images/00325.jpg)

To monitor this extension, you set `20` as the value in the Softkeys and XML configuration page of the Aastra.

The `PICKUPMARK` functionality of the **`Pickup()`** application ([Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)) provides a bit more flexibility:

> ![image](images/00326.jpg)

Advanced users who want to avoid using up an extra extension (`20` in the example above) for the pickup group can try this configuration:

> ![image](images/00327.jpg)

We mentioned earlier that pickup rights could be handled through another mechanism; the comment lines above show where you would perform an authentication test, which could be done either in the dialplan or through an external AGI script.

On the monitoring extension, you set the monitored extension to `**200`.

### 18.6 Advanced BLF Indicators in Asterisk 1.6

**DEVICE_STATE()**

You already know how to monitor the status of SIP users. Here is a quick review for the sake of comparison. In `extensions.conf`, a user hint looks like this:

> exten => 21,hint,SIP/21

In `extensions.ael`, the same hint looks like this:

> hint(SIP/21) 21 => {}

As of Asterisk 1.6, you can monitor the state of MeetMe conferences using hints. Assume a MeetMe conference room of 885, which you want to tie to Asterisk extension 881\. In `extensions.conf`, this would look like this:

> ![image](images/00328.jpg)

In `extensions.ael`, it would look like this:

> ![image](images/00329.jpg)

The hint in the preceding example ties the status of extension 881 to the status of MeetMe room 885\. The numbers are deliberately different, for the sake of clarity; in practice, they are often the same. You can now configure a BLF softkey with the extension 881, and it will indicate the status of the conference (that is, active or not).

Even more interesting, though, is that Asterisk 1.6 lets you tie hints to virtual devices. In `extensions.conf`, this looks like this:

> exten => 99,**hint,Custom:my-status**

In `extensions.ael`, the same construction looks like this:

> **hint(Custom:my-status)** 99 => {}

The status of such a custom device can be set to anything you like using the **`DEVICE_STATE()`** function from elsewhere in the dialplan.

> ### Warning
> 
> For a time, this function was called **`DEVSTATE()`**, which is the same as **`DEVICE_STATE()`**. This function is not to be confused with the application **`DevState()`** or other applications and functions with similar names, even if they work similarly. You might see these alternates mentioned in list archives and Internet forums.

The function uses this construction:

> Set (DEVICE_STATE (Custom:my-status)=INUSE);

The status is then transmitted to any phones that have subscribed to the hint. The possible values are as follows:

> • `UNKNOWN`

> Unknown; the device cannot be contacted.

> • `UNAVAILABLE`

> The device is unavailable.

> • `NOT_INUSE`

> The device is available.

> • `INUSE`

> The device is in a call.

> • `BUSY`

> The device is in a call and will not take additional calls. (The device is busy.)

> • `RINGING`

> The device is ringing.

> • `RINGINUSE`

> The device is in use, but is also ringing. (An additional caller is calling and the device is receiving call waiting notification.)

> • `ONHOLD`

> The device has a call on hold.

> • `INVALID`

> The status is invalid. (You might use this if the device status cannot be determined because it doesn’t exist; for example, for a dynamic conference room.)

How this status is actually manifested on a monitoring extension depends on the device manufacturer. Not all devices distinguish between all the status types.

The default status is `UNKNOWN`, which would be the case after an Asterisk restart before the status is set.

Once a phone has subscribed to the status of `Custom:my-status` at extension 99 in the above example, you can test whether it works by adding these statements to the dialplan (shown here in AEL format):

> ![image](images/00330.jpg)

You can now set the device status by dialing the configured extensions accordingly. (Again, how each model of phone indicates those states will vary.) Most of the extensions are self-explanatory; `*94` toggles between `INUSE` and `NOT_INUSE`. After you’ve figured out the basic operation, there are no limits on what you can do with indicators of this type. For example, you could use it to indicate whether you are logged into a queue, or even if your sprinkler system is currently watering the lawn.

Of course, this hint will appear in the output of **`core show hints`** along with all the other more conventional hints:

> ![image](images/00331.jpg)

The CLI command **`devstate list`** lets you find the status of all your Custom hints:

> ![image](images/00332.jpg)

Finally, **`devstate change device state`** lets you set the status from the CLI:

> ![image](images/00333.jpg)

## A. Installation Instructions for Asterisk 1.4

These instructions install the components necessary to use all the features covered in this book (except where otherwise indicated). As a result, it is a little more comprehensive than a typical installation but offers the advantage that you won’t have to install additional components in the future.

> ### Tip
> 
> If you don’t want to install a new operating system on the computer, you can try installing using a KNOPPIX Live System.

We assume a freshly installed Debian GNU/Linux 5.0 (Lenny). You can find an ISO image for the installation CD at [www.debian.org/releases/lenny/debian-installer](http://www.debian.org/releases/lenny/debian-installer). We recommend the 150MB network install image. (You will most likely need the one for the i386 architecture.) You can find installation instructions for Debian GNU/Linux at [www.debian.org/releases/lenny/i386](http://www.debian.org/releases/lenny/i386).

Before continuing, please log in as root.

> ### Tip
> 
> Some users will undoubtedly want to install an SSH server immediately, in order to work on the server from their regular workstation. The installation command to do this is **`aptitude install ssh`**. We will assume you are comfortable with SSH or will be working directly at the server console.

Begin by making sure that your package lists are current:

> ![image](images/00334.jpg)

Also, make sure that any already installed packages are the most current:

> ![image](images/00335.jpg)

Just in case the updates installed a new kernel, we restart the system with **`shutdown -r now`** (or reboot):

> ![image](images/00336.jpg)

After boot, log in again as root.

> ### Tip
> 
> It is a good idea to install NTP (Network Time Protocol); this keeps the system time accurate and current:
> 
> > debian:~# **aptitude -y install ntp ntpdate**

First, we must install a working build environment (i.e., compiler, linker, autoconf, and so on and any necessary dependencies) so that we can compile and install Asterisk:

> ![image](images/00337.jpg)

The Linux kernel headers are also required:

> ![image](images/00338.jpg)

### A.1 LibPRI

The LibPRI library contains the PRI stack, which includes some functions used for BRI connections. This is not required for all types of installations, but won’t do any harm, either. Obtain the package this way:

> ![image](images/00339.jpg)

Then, unpack it with tar:

> ![image](images/00340.jpg)

Finally, compile and install it:

> ![image](images/00341.jpg)

### A.2 DAHDI

DAHDI handles telephony adapter card (both analog and digital) communications, and until Asterisk 1.4.21 was known as Zaptel (see [Appendix H](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1590070), “[From Zaptel to DAHDI](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1590070)”). Even if you have no such cards installed, you should install this package because it performs other important functions, such as providing a time source for conferences.

Get the DAHDI package like so:

> ![image](images/00342.jpg)

Unpack the tar.gz archives:

> ![image](images/00343.jpg)

Now, install the dependencies:

> ![image](images/00344.jpg)

Finally, compile and install DAHDI and the tools:

> ![image](images/00345.jpg)

> ![image](images/00346.jpg)

To install init scripts and configuration files, run **`make config`**:

> ![image](images/00347.jpg)

There is no harm in leaving the defaults in place. If you have no cards installed, you can safely comment out all the modules in `/etc/dahdi/modules`. To avoid a reboot, we simply restart DAHDI:

> ![image](images/00348.jpg)

As there are no built-in cards in our example, `dahdi_dummy` (formerly `ztdummy`) is loaded so that we have a timing source.

### A.3 Asterisk

Now it’s time to install Asterisk itself. You can obtain the necessary source files at the Asterisk home page, [www.asterisk.org](http://www.asterisk.org). Make sure to get a stable (not a development) version:

> ![image](images/00349.jpg)

Now, unpack the sources:

> ![image](images/00350.jpg)

Next, install the required dependencies:

> ![image](images/00351.jpg)

> ![image](images/00352.jpg)

To prepare for compilation, run the configure script with the Asterisk sources:

> ![image](images/00353.jpg)

Now you can begin compiling:

> ### Tip
> 
> Experienced users can interactively select specific modules by invoking **`make menuselect`**.

> ![image](images/00354.jpg)

Finally, install the compiled sources by invoking **`make install`**:

> ![image](images/00355.jpg)

All the binaries and libraries are now installed, but the configuration directory `/etc/asterisk` is completely empty. Because we don’t want to start completely from scratch, we want the sample configuration files. Get those by invoking **`make samples`**:

> ![image](images/00356.jpg)

To set up Asterisk so that it starts and stops automatically at boot time and shutdown, we need the init scripts. We get those with **`make config`**:

> ![image](images/00357.jpg)

We’re almost done. Unfortunately, the Asterisk installer sets the init sequence incorrectly for a Debian Linux system. We correct that as follows:

> ![image](images/00358.jpg)

Done! Asterisk is now installed. You can determine the installed version by running **`asterisk -V`** (uppercase V):

> ![image](images/00359.jpg)

## B. Dialplan Applications

This appendix describes the use of dialplan applications (in other words, `/etc/asterisk/extensions.conf`) in detail. Applications are contained within modules, so only the applications contained in the modules you’ve actually loaded into Asterisk will be available to your dialplan. You can define which modules will be loaded through the `[modules]` section of the `/etc/asterisk/modules.conf` configuration file, either with the blanket `autoload=yes` statement or by explicitly loading specific modules with `load => app_`*`application_name`*`.so`. You can determine which applications are available to you by invoking the command **`core show applications`** in the Asterisk CLI. Detailed information about a specific application can be viewed by invoking **`core application` *`application_name`***.

> ### Tip
> 
> The commands **`core application xyz`** and **`core applications`** work only beginning with Asterisk version 1.4\. If you’re using Asterisk 1.2, you can get the same result with the commands **`show application xyz`** and **`show applications`**. The old commands will work in Asterisk 1.4, but are deprecated.

Be careful not to confuse applications with functions. Functions are called as parameters to applications.

> ### Note
> 
> Asterisk configuration files use the poorly defined INI format made famous by Microsoft, for which there is no consistently applied grammar, let alone a published one. Asterisk’s config file parser also doesn’t follow the conventional process of lexical analysis, tokenization, and syntactical analysis. This is why the developers of the Asterisk fork OpenPBX switched to the Mac OS X “property list” (`.plist`) configuration file format.
> 
> This is just to say that, due to the lack of a specification, it’s not always clear where and whether spaces are allowed, or where quotation marks are expected. Usually, multiple formats are accepted. If a syntax isn’t working for your specific Asterisk version, the only way to find out for sure is to make changes and test it.
> 
> As always, we welcome feedback. Should you find any errors in the book, please let the authors know.

In many cases, parameters may be omitted; you will still have to include the commas to indicate the empty fields (which usually means Asterisk will assume a default value), as follows:

> exten => s,1,Dial(IAX2/User:password@example.com/123,,tT)

In general, failure results in a return code of −1; success returns 0\. A return code of −1 means that Asterisk hangs up the channel and stops processing the dialplan for that call.

> ### Note
> 
> The parameter delimiter is a comma (,) or pipe (|) depending on the Asterisk version. This book uses the comma.

Experienced Asterisk users may wonder why some applications have been omitted. The reason is simple: Some were already deprecated in Asterisk 1.2 and don’t exist at all in 1.4\. Those applications are not described here; you can find the corresponding functions that replaced them in **[Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), “[Dialplan Functions](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).”** The file compares (“diffs”) of the internal help always compare the newer 1.4 to the older 1.2.

The examples use the hypothetical and arbitrarily chosen extension `123` and the priority `1`; in practice this will not always be practical.

Prior to Asterisk 1.2, many applications jump to priority n+101 (if it exists and where n is the current priority). This old behavior (known as “priority jumping”) can be enabled with the option `j` (jump) with some commands or by setting `priorityjumping=yes` in the `[general]` section of `extensions.conf`. This behavior is deprecated, however. The accepted method is to query channel variables.

The applications are listed in alphabetic order, under their functional purpose:

**Call management (answering, patching, hanging up, and so on)**

> **answer**—Answering

> **busy**—Indicate busy

> **chanisavail**—Test to see whether a channel is available

> **channelredirect**—Redirect a channel to another extension

> **congestion**—Indicate congestion

> **dial**—Initiate a call, patch a call, or connect a channel

> **disa**—DISA (Direct Inward System Access)

> **followme**—“Follow me” functionality

> **hangup**—Hang up the channel

> **page**—Page (one-way communications) to a group of devices

> **park**—Park the call

> **pickup**—Pick up a call in a pickup group

> **retrydial**—**`Dial()`** with retry

> **ringing**—Indicate ringing

**Flow control and timeouts**

> **continuewhile**—Return to the beginning of a `while` loop

> **endwhile**—End a `while` loop

> **exec**—Execute an application

> **execif**—Conditionally execute an application

> **execiftime**—Execute an application if a time condition is met

> **exitwhile**—Exit a `while` loop

> **gosub**—Jump to a subroutine

> **gosubif**—Conditionally jump to a subroutine

> **goto**—Jump to the given priority, extension, or context

> **gotoif**—Conditional **`Goto()`**

> **gotoiftime**—Time conditional **`Gosub()`**

> **random**—Jump to a random point in the dialplan

> **return**—Return from a **`Gosub()`** or **`GosubIf()`**

> **tryexec**—Check to see whether an application will run

> **while**—Begin a `while` loop

**Macros**

> **macro**—Call a macro

> **macroexclusive**—Call a macro; allow only one instance of that macro to run

> **macroexit**—Exit a macro

> **macroif**—Conditionally call a macro

**Caller identification**

> **lookupblacklist**—Look up caller ID in the blacklist

> **lookupcidname**—Look up caller ID name in the database

> **privacymanager**—Request input of the caller’s number if caller ID cannot be obtained

> **setcallerpres**—Set caller ID presentation flags

> **softhangup**—Hang up the channel but return 0

> **zapateller**—Block telemarketers

**Call detail records (CDRs)**

> **appendcdruserfield**—Append a value to the CDR user field

> **forkcdr**—Break the CDR into two entries

> **nocdr**—Deactivate CDR for this call

> **resetcdr**—Reset CDR

> **setamaflags**—Set AMA flags

> **setcdruserfield**—Set CDR user field

**Voicemail**

> **directory**—Provide dial-by-name directory

> **mailboxexists**—Check if mailbox exists

> **voicemail**—Voicemail

> **voicemailmain**—Administer voicemail

> **vmauthenticate**—Authenticate the caller using records in `voicemail.conf`

**Conferencing**

> **meetme**—Conference call

> **meetmeadmin**—Administer conference

> **meetmecount**—Count participants in a conference

**Change variables**

> **importvar**—Import variables from a channel

> **read**—Read digits dialed by caller into a variable

> **readfile**—Read a file into a variable

> **realtime**—Read data from the real-time system into a variable

> **realtimeupdate**—Change variables in the real-time system

> **set**—Set a channel variable

> **setglobalvar**—Set a global variable

**Music and sound output**

> **background**—Begin playing a sound and advance to the next priority immediately

> **backgrounddetect**—**`Background()`** with speech detection

> **controlplayback**—**`Playback()`** with shuttle controls (forward, reverse, exit)

> **datetime**—Say date and time (“speaking clock”)

> **echo**—Echo audio back to caller

> **festival**—Say text with Festival text-to-speech engine

> **milliwatt**—Generate milliwatt test tone

> **mp3player**—Play MP3 file or stream

> **musiconhold**—Play hold music

> **nbscat**—Play Network Broadcast Sound stream

> **playback**—Play sound file

> **playtones**—Play tones

> **progress**—Indicate call progress in-band

> **sayalpha**—Spell out text alphanumerically

> **saydigits**—Say digits

> **saynumber**—Say number

> **sayphonetic**—Spell out text using NATO alphabet

> **sayunixtime**—Say time in UNIX format

> **setmusiconhold**—Set music-on-hold class

> **stopplaytones**—Stop **`Playtones()`**

**Recording and monitoring**

> **agentmonitoroutgoing**—Record outgoing calls of an agent

> **changemonitor**—Change the recording file for **`Monitor()`**

> **chanspy**—Eavesdrop on a channel

> **dial**—Enable in-call recording with `w` or `W` parameters

> **dictate**—Take and play back dictation

> **extenspy**—Eavesdrop on an extension

> **mixmonitor**—Like **`Monitor()`**, but mixes into a single file

> **monitor**—Records a call

> **pausemonitor**—Pauses recording of a call

> **record**—Records incoming audio

> **stopmonitor**—Stop **`Monitor()`**

> **unpausemonitor**—Unpause recording of a call

> **zapbarge**—Eavesdrop on a ZAP channel

> **zapscan**—Scan through ZAP channels for eavesdropping

**Database**

> **dbdel**—Delete a database entry

> **dbdeltree**—Delete a database branch

**General**

> **authenticate**—Authenticate a caller

> **senddtmf**—Send dual-tone multi-frequency (DTMF) tones

> **sendimage**—Send an image

> **sendtext**—Send a text

> **sendurl**—Send a URL

> **transfer**—Transfer a call

> **vmauthenticate**—Authenticate a caller using account information from `voicemail.conf`

> **wait**—Wait a specified time

> **waitexten**—Wait for the caller to dial an extension

> **waitforring**—Wait for ring

> **waitforsilence**—Wait for silence

> **waitmusiconhold**—Wait and play music-on-hold

**Scripts**

> **agi**—Run an AGI application

> **deadagi**—Run **`AGI()`** on a hung-up channel

> **dumpchan**—Dump channel information to the CLI

> **eagi**—See **`AGI()`**

> **externalivr**—Run an external IVR

> **log**—Log an event at the specified verbosity level

> **macro**—Call a macro

> **noop**—Do nothing, but write the event to the CLI or logs

> **read**—Read caller input (digits) into a variable

> **system**—Execute a command in the system shell

> **trysystem**—Like **`System()`**, but always returns 0

> **userevent**—Send an event to the Manager interface

> **verbose**—Write a message to the CLI at the specified verbosity level

**SIP**

> **sipdtmfmode**—Change DTMF mode during SIP connection

> **sipaddheader**—Add a SIP header to an outgoing call

**ZAP**

> **flash**—Perform a switchhook “flash” on a ZAP trunk

> **zapbarge**—Eavesdrop on a ZAP channel

> **zapras**—Starts the Zaptel ISDN RAS (Remote Access Server) on a ZAP channel

> **zapscan**—Scan through ZAP channels for eavesdropping

**Queues**, **call center functions**

> **addqueuemember**—Dynamically add an interface to the queue

> **agentcallbacklogin**—Log in a call agent (with callback)

> **agentlogin**—Log out a call agent

> **agentmonitoroutgoing**—Record outgoing calls of an agent

> **parkandannounce**—Park the call and announce

> **parkedcall**—Take a parked call

> **pausequeuemember**—Pause a call agent

> **queue**—Queue the incoming call

> **queuelog**—Write a message to the queue log

> **removequeuemember**—Remove an interface from the queue

> **unpausequeuemember**—Reactivate a paused call agent

**ADSI**

> **adsiprog**—Load an ADSI script into the phone

> **getcpeid**—Query an ADSI device for ADSI CPE ID

**Miscellaneous**

> **amd**—Answering machine detection

> **alarmreceiver**—Emulate an alarm or fire panel receiver

> **iax2provision**—Provision an IAXy device

> **morsecode**—Send text in Morse code

> **settransfercapability**—Set ISDN transfer capability

> **sms**—Send or receive SMS (Short Message System) messages

### B.1 AbsoluteTimeout()

Sets the absolute maximum time allowed for a call:

> AbsoluteTimeout(*seconds*)

> ### Warning
> 
> `AbsoluteTimeout()` is removed as of Asterisk 1.4 and has been replaced with the `TIMEOUT()` (see [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249)) function:
> 
> > Set(TIMEOUT(absolute)=seconds)

**Asterisk versions:**

![image](images/00360.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [`digittimeout`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos867232), [`responsetimeout`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1138171), and [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), “[Dialplan Functions](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).”**

### B.2 AddQueueMember()

Dynamically adds an interface into the queue:

> AddQueueMember(*queue*[,*interface*[,*penalty*[|,*options*]]])

Dynamically adds the specified interface to the specified queue, which is configured in `queues.conf`. The penalty setting, if provided, will influence the priority assigned to the interface in the queue. Agents with lower penalty values will receive calls before agents with higher penalty values.

If the specified interface is already in the queue and the n+101 priority exists (where n is the current priority), the call jumps to that priority; otherwise an error code (−1) is returned. (Depending on the version of Asterisk, you may need to provide the j option to enable priority jumping.)

If **`AddQueueMember()`** is called without the interface parameter, the current user’s active interface is used.

Some versions of Asterisk allow commas as an option separator.

This application sets the channel variable `${AQMSTATUS}` to `ADDED`, `MEMBERALREADY` (member exists in the queue) or `NOSUCHQUEUE` (queue does not exist) depending on circumstance:

> ![image](images/00361.jpg)

**Asterisk versions:**

![image](images/00362.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00363.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00364.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00365.jpg)

**See also [`queue`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1098312), [`removequeuemember`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1133610), `queues.conf`.**

### B.3 ADSIProg()

Loads an ADSI script into an ADSI-capable phone:

> ADSIProg([*script*])

Programs an ADSI (Analog Display Services Interface) phone with the provided script. If no script is provided, the default `asterisk.adsi` is used. The pathname for the script is relative to the default Asterisk configuration directory, which is usually `/etc/asterisk`. The absolute path is also accepted.

Use **`GetCPEID()`** to obtain the CPE (customer premises equipment) ID and other information about the ADSI device.

> ![image](images/00366.jpg)

**Asterisk versions:**

![image](images/00367.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00368.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`getcpeid`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos923308), `adsi.conf`.**

### B.4 AgentCallbackLogin()

Allows call agent login with callback:

> AgentCallbackLogin([*agentid*][,*options*[,extension@contex*t*]])

Allows an agent identified through the agent ID to log in to the queue. A call in the queue will cause the agent’s phone to ring. (This is in contrast to **`AgentLogin()`**, in which the agent’s phone is off-hook and new calls are indicated by a tone.)

For an incoming call for the specified agent, the specified extension (at the specified context, if provided) is called.

The option `s` makes the login silent; the agent login is not reported:

> ![image](images/00369.jpg)

Numerous examples are available at [www.voip-info.org/wiki/index.php?page=Asterisk+cmd+AgentCallbackLogin](http://www.voip-info.org/wiki/index.php?page=Asterisk+cmd+AgentCallbackLogin).

**Asterisk versions:**

![image](images/00370.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00371.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

**See also [`agentlogin`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos733665).**

### B.5 AgentLogin()

Allows call agent login:

> AgentLogin([*agentid*][,*options*])

Logs the current caller (optionally identified through `agentid`) into the queue as a call agent. Once logged in, the agent can take calls with the phone off-hook; each call is preceded by a warning tone. Calls are ended by pressing the star (*) key.

The option `s` makes the login silent:

> ![image](images/00372.jpg)

**Asterisk versions:**

![image](images/00373.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00374.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00375.jpg)

### B.6 AgentMonitorOutgoing()

Records all the outgoing calls of an agent.

> AgentMonitorOutgoing([*options*])

This application attempts to determine the ID of an agent making an outgoing call by comparing the caller ID of the agent with a global variable set by the **`AgentCallbackLogin()`** application. As such, it should be used with **`AgentCallbackLogin()`**, and always in a later priority. This application uses monitoring functions in `chan_agent` rather than **`Monitor()`**, so call recording must be configured in `agents.conf`.

By default, recordings are saved in `/var/spool/asterisk/monitor`. You can override this behavior with the parameter `savecallsin` in `agents.conf`.

> ### Warning
> 
> Be aware that recording of calls may be subject to freedom of information and privacy legislation in your jurisdiction. As a matter of professional practice, you should know the terms under which it is lawful to record telephone calls. In most jurisdictions, it is illegal to record a call without the knowledge of the participants.

If the caller ID and/or agent ID for the agent cannot be determined, the call jumps to priority n+101, if it exists.

Unless the options specify otherwise, the application returns 0.

The following options may be used:

> • **`d`**

> forces the return of −1 in the event of error if there is no n+101 priority.

> • **`c`**

> changes the call detail record so that the source of the call is `agent/agentid` rather than the caller ID.

> • **`n`**

> suppresses error messages if the caller/agent ID cannot be determined. This is useful if a common context for agent and nonagent calls is desired.

> ![image](images/00376.jpg)

**Asterisk versions:**

![image](images/00377.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00378.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00379.jpg)

### B.7 AGI()

Runs an AGI-compliant application (similar to **`EAGI()`**, **`FastAGI()`**, **`DeadAGI()`**):

> AGI(program[,*arguments*])

It also runs an AGI-compliant program called `program` on the current channel. AGI scripts or programs can be implemented in almost any conceivable language (e.g., Perl, PHP) and may be used to manipulate the channel, play sound files, interpret DTMF tones, and so on. Asterisk communicates with the AGI program over `stdin` and `stdout`. The arguments are passed directly to the AGI program at execution time.

The AGI program must be flagged as executable in the file system. The path is relative to the Asterisk AGI directory, which is at `/var/lib/asterisk/agi-bin` by default, or may be specified as an absolute path.

To run a program or script on another server, invoke it using a URL in the form `agi://`*`host`*`[:`*`port`*`[/`*`program`*`]]`. This way the script, program, or daemon can be running at all times and be ready to accept connections, which improves the performance of your applications. This method, known as FastAGI, is similar in function and purpose to FastCGI as used in web servers. The default port is 4573 if no port number is provided. If *`program`* is specified, it is provided as an environment variable `agi_network_script` to the FastAGI program. There is a sample FastAGI Perl script in the `agi` folder (`fastagi-test`). Use this as a starting point for your own FastAGI scripts.

For a list of commands an AGI script can send to Asterisk, see [**agi-commands**](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos740308), or enter **`agi show`** in the Asterisk CLI.

To run AGI programs on inactive channels (as in the case of an `h` extension, where the channel is on-hook), used **`DeadAGI()`** instead. Should your AGI program need access to the incoming audio stream, use **`EAGI()`** rather than **`AGI()`**. The incoming audio stream is provided on file descriptor 3.^([1](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos743820))

[1](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos743714). A reminder: 0: `stdin`, 1: `stdout`, 2: `stderr`. File descriptor 3 is freely assignable.

It returns −1 on hangup or if the program requests a hangup; returns 0 if not.

> ![image](images/00380.jpg)

**Asterisk versions:**

![image](images/00381.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00382.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00383.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00384.jpg)

> ![image](images/00385.jpg)

**See also [`deadagi`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos831596), [`fastagi`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos910187).**

### B.8 AlarmReceiver()

Receives alarm reports from a burglar or fire alarm panel:

> AlarmReceiver()

It emulates an alarm receiver and allows Asterisk to receive and process alarm reports in proprietary alarm panel signaling formats from burglar and fire alarm panels. Only Ademco Contact ID formatted alarm reports are supported at this time.

When **`AlarmReceiver()`** is called, Asterisk performs a handshake with the connected alarm panel, waits for it to transmit events, then validates and stores them. When the panel has hung up, **`AlarmReceiver()`** runs the system command specified in the `eventcmd` of `alarmreceiver.conf`. The `alarmreceiver.conf` also contains DTMF timing settings and acknowledgment tone volume.

This application has not been certified for use in critical environments where it is the only means of polling alarm events. Use it at your own risk! Before implementing, be sure to test it thoroughly.

It always returns 0.

> ![image](images/00386.jpg)

**Asterisk versions:**

![image](images/00387.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00388.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00389.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`alarmreceiver.conf`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos745930).**

### B.9 AMD()

Answering machine detection. Attempts to detect an answering machine at the remote end of a call.

> ![image](images/00390.jpg)

If a call is initiated through a `.call` file, you can use **`AMD()`** to sense an answering machine at the remote end. Defaults are set in `amd.conf`:

> • **`initialSilence`**

> Maximum duration of silence preceding the remote announcement. If this is exceeded, sets `${AMDSTATUS}` to `MACHINE`.

> • **`greeting`**

> Maximum duration of an announcement. If this is exceeded, sets `${AMDSTATUS}` to `MACHINE`.

> • **`afterGreetingSilence`**

> Maximum duration of silence following the remote announcement. If this is exceeded, sets `${AMDSTATUS}` to `HUMAN`.

> • **`totalAnalysisTime`**

> Maximum duration **`AMD()`** is allowed to determine whether remote end is `HUMAN` or `MACHINE`.

> • **`minWordsSilence`**

> Minimum allowed duration of a sound for it to be considered a word.

> • **`betweenWordsSilence`**

> Minimum allowed duration of silence between words.

> • **`maxNumberOfWords`**

> Maximum number of words in the announcement. If this is exceeded, sets `${AMDSTATUS}` to `MACHINE`.

> • **`silenceThreshold`**

> The silence threshold.

This application delivers its output in the channel variables `AMDSTATUS` and `AMDCAUSE`.

`AMDSTATUS` can be assigned the following values:

> • `MACHINE`

> The remote end is a machine.

> • `HUMAN`

> The remote end is a human.

> • `NOTSURE`

> Threshold cases are indicated with `NOTSURE`.

> • `HANGUP`

> The remote end has hung up.

`AMDCAUSE` can be assigned the following values:

> • `TOOLONG`-*<%d total_time>*

> • `INITIALSILENCE`-*<%d silenceDuration>-<%d initialSilence>*

> • `HUMAN`-<%d silenceDuration>-*<%d afterGreetingSilence>*

> • `MAXWORDS`-*<%d wordsCount>-<%d maximumNumberOfWords>*

> • `LONGGREETING`-*<%d voiceDuration>-<%d greeting>*

> ![image](images/00391.jpg)

**Asterisk versions:**

![image](images/00392.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00393.jpg)

> ![image](images/00394.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00395.jpg)

> ![image](images/00396.jpg)

**See also `call-file`.**

### B.10 Answer()

Answers a ringing channel.

> Answer([*delay*])

Instructs Asterisk to answer the channel if it is ringing. If the channel is not ringing, this application has no effect.

It is generally recommended that the channel be answered before other applications are called, unless there is a specific reason for not doing so. Most applications require that the channel be answered before they are run; if this is not done, the behavior may be unexpected.

The optional delay parameter specifies how long Asterisk should wait, in milliseconds, before answering the channel.

Returns 0 upon success.

> ![image](images/00397.jpg)

**Asterisk versions:**

![image](images/00398.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00399.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`hangup`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos944692).**

### B.11 AppendCDRUserField()

Appends a string to the user field in the CDR.

> AppendCDRUserField(*string*)

This application has been deprecated in favor of the **`CDR(userfield)`** function.

**Asterisk versions:**

![image](images/00400.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00401.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00402.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.12 Authenticate()

Requires that the caller enter a password before proceeding to the next priority.

> Authenticate(*password*[,*options*[,maxDigits]])

Requires that the caller enters the specified password correctly before proceeding to the next priority. Allows the caller three chances to enter the password correctly before hanging up.

If `password` begins with forward slash (/), Asterisk will assume it is a filename to a file containing a list of valid passwords (exactly one per line). Passwords may also be stored in the Asterisk database (AstDB); see option **`d`** below.

The following options are allowed (also in combination):

> • **`a`**

> (accountcode) Sets the CDR `accountcode` field and the channel variable `ACCOUNTCODE` to the entered password.

> • **`d`**

> (database) Interprets the entered password as a key in the Asterisk database. If a database key is used, the value in the associated record is ignored and can be arbitrary.

> • **`r`**

> (remove) Removes the database key after successful password entry (valid only with option **`d`**).

> • **`j`**

> (jump) In the event of three failed attempts, jump to priority n+101 (if it exists) instead of hanging up.

> ### Warning
> 
> When using option `d`, note that Asterisk looks for a *key* with a name equivalent to the password: as in *`/passwords/1234`*. The value in the record itself is irrelevant. A more logical implementation is to place the password as a value in the record, as in `/passwords/type => 1234`.

If `maxDigits` is set, input is ended as soon as the user has entered enough digits; this saves having to enter pound sign (`#`). (Default: 0; no limits on input.)

Returns 0 if the user enters the correct password within three attempts, otherwise hangs up the channel and returns −1.

> ![image](images/00403.jpg)

**Asterisk versions:**

![image](images/00404.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00405.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00406.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00407.jpg)

**See also [`vmauthenticate`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1264134).**

### B.13 Background()

Plays a sound file while listening for DTMF input from the caller.

> Background(*soundfile1*[&*soundfile2*...][,*options*[,*language*]])

Plays the specified sound files while waiting for the caller to dial an extension. Playback stops the moment the first digit is pressed. Filenames must be provided without file extensions; Asterisk chooses the file format with the minimum transcoding cost.

Allowed options may not be combined:

> • **`skip`**

> Playback is skipped if the channel is not in the up state when the application is run. If skip is specified, the application ends immediately when the channel is hung up.

> • **`noanswer`**

> The channel is answered only after the specified sound file has been played. The default behavior is to answer the channel automatically before playing the sound file. Note that not all channel types allow playback of a message before being answered.

The `language` parameter can be used to specify a language for the sound files played, in the event this should be different than the language currently specified for the channel.

Returns −1 if hung up or if the specified sound file does not exist, otherwise returns 0.

> ![image](images/00408.jpg)

**Asterisk versions:**

![image](images/00409.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00410.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00411.jpg)

> ![image](images/00412.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00413.jpg)

**See also [`playback`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1085123), [`backgrounddetect`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos770445), `show translation`.**

### B.14 BackgroundDetect()

Plays a sound file while listening for sound from the caller.

> BackgroundDetect(*soundfile*[,*silence*[,*min*[,*max*]]])

Similar to **`Background()`**, but listens for sound also.

During playback of the sound file, the application monitors audio on the incoming audio channel. If it detects a sound longer than *min* milliseconds in duration but shorter than *max* milliseconds, followed by a period of silence of at least *silence* milliseconds, it stops playback and passes the call to the `talk` extension, if it exists.

If *silence*, *min*, and *max* are not specified, the defaults are used: 1,000ms, 100ms, and unlimited, respectively.

Returns −1 on hangup, otherwise returns 0 (such as when playback is interrupted due to input).

> ![image](images/00414.jpg)

**Asterisk versions:**

![image](images/00415.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00416.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00417.jpg)

**See also [`playback`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1085123), [`background`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos766468).**

### B.15 Bridge()

Connects the active channel with a specified channel.

> Bridge(*channel*,*options*)

Success or failure is signaled through the `BRIDGERESULT` variable.

> • **`SUCCESS`**

> Connection successful.

> • **`LOOP`**

> You have attempted to connect a channel to itself.

> • **`NONEXISTENT`**

> The target channel does not exist.

> • **`INCOMPATIBLE`**

> The channel uses an incompatible technology.

> • **`FAILURE`**

> Other error.

**Asterisk versions:**

![image](images/00418.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00419.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [`dial`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos835607).**

### B.16 Busy()

Sets the channel as “busy.”

> Busy([*timeout*])

Instructs the channel to indicate busy and waits until the caller hangs up or the timeout expires (*timeout*, in seconds).

This application indicates a busy state only on the bridged channel. Every channel type has its own way of indicating that a device is busy. To play an actual busy tone, use **`Playtones (busy)`**.

Always returns −1.

> ![image](images/00420.jpg)

**Asterisk versions:**

![image](images/00421.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00422.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`congestion`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos801971), [`progress`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1096214), [`playtones`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1087914).**

### B.17 ChangeMonitor()

Changes the monitoring filename of a channel.

> ChangeMonitor(*filename-prefix*)

Changes the filename prefix for sound files written while recording the channel with **`Monitor()`**. This application has no effect if the affected channel is not being monitored.

> ![image](images/00423.jpg)

**Asterisk versions:**

![image](images/00424.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00425.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00426.jpg)

**See also [`monitor`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1038634), [`stopmonitor`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1235968).**

### B.18 ChanIsAvail()

Indicates whether the specified channel is available.

> ChanIsAvail(*technology1*/*resource1*[&*technology2*/*resource2*...][,*options*])

Verifies that the one or more of the queried channels is available, in the order specified. Returns 0 on success or −1 on failure.

If the `s` (state) option is given, Asterisk will treat the channel as unavailable if it is in use, even if it is capable of taking another call. Option `j` sets priority jumping to n+101 if the channel is unavailable.

> ### Note
> 
> The mere fact of a channel being available does not automatically mean that it is free for use or that the device on the channel will accept a call. That is determined using a **`Dial()`** to the channel.

**`ChanIsAvail()`** sets the following channel variables:

> • **`${AVAILCHAN}`**

> The name of the accessible channel, including the session number of the call.

> • **`${AVAILORIGCHAN}`**

> The canonical channel name (i.e., the channel name without session number).

> • **`${AVAILSTATUS}`**

> Status code of the channel:

> • **`AST_DEVICE_UNKNOWN (0)`**

> Status of the channel is unknown. It is a valid channel, but we don’t know about its state.

> • **`AST_DEVICE_NOT_INUSE (1)`**

> The channel is not in use.

> • **`AST_DEVICE_IN_USE (2)`**

> The channel is in use.

> • **`AST_DEVICE_BUSY (3)`**

> The channel is busy.

> • **`AST_DEVICE_INVALID (4)`**

> The channel is unknown.

> • **`AST_DEVICE_UNAVAILABLE (5)`**

> The channel is not available and not registered.

> • **`AST_DEVICE_RINGING (6)`**

> The channel is ringing.

> ### Note
> 
> This application does not behave as expected on MGCP channels.

> ![image](images/00427.jpg)

**Asterisk versions:**

![image](images/00428.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00429.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00430.jpg)

### B.19 ChannelRedirect()

Redirects a channel to another extension and priority.

> ChannelRedirect(*channel*,[*context*,]*extension*,*priority*)

Redirects the specified channel to another extension and priority.

> • **`Channel`**

> Name of the channel to be redirected

> • **`Context`**

> Context to which the channel should be redirected

> • **`Extension`**

> Extension to which the channel should be redirected

> • **`priority`**

> Priority in the new extension

**Asterisk versions:**

![image](images/00431.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00432.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00433.jpg)

**See also [`goto`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos934438), [`transfer`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1245020).**

### B.20 ChanSpy()

Enables eavesdropping on a channel.

> ChanSpy([*channelprefix*[,*options*]])

Allows eavesdropping on a conversation on any specified channel. (This is different from **`ZapBarge()`**/**`ZapScan()`**, which are bound to Zap channels only.) Note that this application only listens on single channels, rather than the conversation per se, even though it does capture incoming and outgoing audio on the channel.

> ### Warning
> 
> Be aware that listening to calls may be subject to freedom of information and privacy legislation in your jurisdiction. As a matter of professional practice, you should know the terms under which it is lawful to eavesdrop on telephone calls. In most jurisdictions it is illegal to eavesdrop on a call without the knowledge of the participants.

If *channelprefix* is specified, only channels with a name beginning with that string are available for listening.

Options may be combined:

> • **`b`**

> (bridged) Restrict to bridged (i.e., connected) channels.

> • **`g(`*`grp`*`)`**

> (group) Restrict to channels whose `${SPYGROUP}` channel variable contains the value *`grp`* in a colon-delimited (:) list.

> • **`q`**

> (quiet) Do not play beep tones (or announce the channel name) when switching channels.

> • **`r([`*`name`*`])`**

> (record) Record the spying session in a file in the `/var/spool/asterisk/monitor` directory. The default filename prefix is `chanspy`.

> • **`v[(value)]`**

> (volume) Set the initial volume. The range of allowed values is from −4 (quiet) to 4 (loud).

> • **`w`**

> (whisper) Activate whisper mode. Allows the user on the spying channel to speak to the channel user on the spied-on channel, without the remote user hearing. (This option is available as of Asterisk 1.4.)

> • **`W`**

> (private whisper) Private whisper mode. Like `w`, except that the spying channel cannot hear the spied-on channel. (It’s not immediately clear where this would be useful, but Asterisk has found myriad applications!)

While listening, the following keypad input is accepted:

> • **`#`**

> Increases volume stepwise (from −4 to 4).

> • **`*`**

> Switches to another channel.

> • ***`X..X#`***

> A set of digits of arbitrary length, ended with `#`, is attached to *`channelprefix`*. For example, if the extension invokes **`ChanSpy(Agent)`** and the user on the spying channel dials `1234#`, the spying channel will begin spying on the channel `Agent/1234`.

> ![image](images/00434.jpg)

**Asterisk versions:**

![image](images/00435.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00436.jpg)

> ![image](images/00437.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00438.jpg)

> ![image](images/00439.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00440.jpg)

> ![image](images/00441.jpg)

> ![image](images/00442.jpg)

> ![image](images/00443.jpg)

**See also [`extenspy`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos902022), [`zapbarge`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1294818), [`zapscan`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1299987), [`monitor`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1038634).**

### B.21 CheckGroup()

Limits the number of channels in a group.

> CheckGroup(*maximum*[@*category*][|*options*])

> ### Warning
> 
> **`CheckGroup()`** is removed as of Asterisk 1.4 and has been replaced by the **`GROUP_COUNT()`** function.

**Asterisk versions:**

![image](images/00444.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00445.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [`setgroup`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1200419); and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`group_count`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1371357), [`getgroupcount`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos925448), [`getgroupmatchcount`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos927449).**

### B.22 ClearHash()

Clears all the key/value pairs from the specified hashname.

> ClearHash(*hashname*)

For more information, see [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).

**Asterisk versions:**

![image](images/00446.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00447.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.23 Congestion()

Indicates congestion (insufficient resources available) on the channel.

> Congestion([*timeout*])

Indicates congestion on the channel and waits until the caller hangs up or until the specified timeout *`timeout`* has expired.

This application indicates congestion in the system but does not indicate this to the caller. Should you wish to notify the caller, use **`Playtones(congestion)`**.

Returns −1.

> ![image](images/00448.jpg)

**Asterisk versions:**

![image](images/00449.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00450.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00451.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`busy`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos776235), [`progress`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1096214), [`playtones`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1087914).**

### B.24 ContinueWhile()

Returns to the beginning of a `while` loop.

> ContinueWhile()

The **`ContinueWhile()`** application can interrupt a while loop while in progress. Asterisk returns to the beginning of the loop and evaluates the condition.

**Asterisk versions:**

![image](images/00452.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00453.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00454.jpg)

**See also [`while`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1289713), [`exitwhile`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos900109), [`ael`](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1590497).**

### B.25 ControlPlayback()

Plays a sound file with fast forward and rewind controls.

> ControlPlayback(*soundfile*[,*skipms*[,*ffchar*[,*rewchar*[,*stopchar*[,*pausechar*]]]]])

Plays the specified file; the caller can manipulate playback by pressing the defined keys *`ffchar`* and *`rewchar`*. The defaults are # (forward) and * (backward). Playback is stopped when *`stopchar`* is pressed (if it is defined). If the file does not exist, the application jumps to priority n+101, if it exists.

The *`pausechar`* option is similar in behavior to *`stopchar`* except that playback can be resumed by pressing *`pausechar`* a second time.

The *`skipms`* defines how far forward or backward **`ControlPlayback()`** will skip in the file when *`ffchar`* or *`rewchar`* is pressed.

Returns −1 if the caller hangs up during playback.

> ![image](images/00455.jpg)

**Asterisk versions:**

![image](images/00456.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00457.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00458.jpg)

**See also [`playback`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1085123), [`background`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos766468).**

### B.26 Curl()

Loads a URL.

> Curl (*URL*|*postdata*)

> ### Warning
> 
> **`Curl()`** is removed as of Asterisk 1.4 and was replaced by the **`CURL()`** function.

**Asterisk versions:**

![image](images/00459.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00460.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.27 Cut()

Cuts a variables contents using the specified delimiter.

> Cut(*newvariable*=*variable*,*delimiter*,*fieldnumber*)

> ### Warning
> 
> **`Cut()`** is removed as of Asterisk 1.4 and has been replaced by the **`CUT()`** function.

**Asterisk versions:**

![image](images/00461.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00462.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.28 DAHDIBarge()

Monitor a DAHDI channel.

> DAHDIBarge([*channel*])

> ### Note
> 
> This application came out of the renaming of Zaptel to DAHDI.^([2](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos813764))
> 
> [2](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos813658). For a complete description, see [`zapbarge`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1294818).

**Asterisk versions:**

![image](images/00463.jpg)

(* different name)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00464.jpg)

**Diff of the internal help from Asterisk 1.2 (zapbarge) to 1.4 (zapbarge):**

None

**Diff of the internal help from Asterisk 1.4 (zapbarge) to 1.6:**

> ![image](images/00465.jpg)

**See also [`zapbarge`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1294818).**

### B.29 DAHDIRAS()

Executes a DAHDI ISDN Remote Access Server.

> DAHDIRAS(*arguments*)

> ### Note
> 
> This application came out of the renaming of Zaptel to DAHDI.^([3](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos815945))
> 
> [3](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos815839). For a complete description, see [`zapras`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1297160).

**Asterisk versions:**

![image](images/00466.jpg)

(* different name)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00467.jpg)

**Diff of the internal help from Asterisk 1.2 (zapras) to 1.4 (zapras):**

None

**Diff of the internal help from Asterisk 1.4 (zapras) to 1.6:**

> ![image](images/00468.jpg)

**See also [`zapras`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1297160).**

### B.30 DAHDIScan()

Scans DAHDI channels for monitoring purposes.

> DAHDIScan([*channel_group*])

> ### Note
> 
> This application came out of the renaming of Zaptel to DAHDI.**^([4](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos818150))**
> 
> [4](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos818031). For a complete description, see [`zapscan`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1299987).

**Asterisk versions:**

![image](images/00469.jpg)

(* different name)

**Internal help for this application in Asterisk 1.6:**

![image](images/00470.jpg)

**Diff of the internal help from Asterisk 1.2 (zapscan) to 1.4 (zapscan):**

None

**Diff of the internal help from Asterisk 1.4 (zapscan) to 1.6:**

> ![image](images/00471.jpg)

**See also [`zapscan`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1299987).**

### B.31 DAHDISendKeypadFacility()

Sends digits out-of-band on an ISDN PRI connection.

> DAHDISendKeypadFacility(*digits*)

> ### Note
> 
> This application came out of the renaming of Zaptel to DAHDI.^([5](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos820324))
> 
> [5](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos820218). For a complete description, see [`zapsendkeypadfacility`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1302126).

**Asterisk versions:**

![image](images/00472.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00473.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 (zapsendkeypadfacility) to 1.6:**

> ![image](images/00474.jpg)

**See also [`zapsendkeypadfacility`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1302126).**

### B.32 DateTime()

Say the current time.

> DateTime([unixtime[,timezone[,format]]])

Says the current time. It is not yet deprecated but is now only an alias to **`SayUnixTime()`**; see the description there for use instructions.

**Asterisk versions:**

![image](images/00475.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00476.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00477.jpg)

**See also [`sayunixtime`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1159951).**

### B.33 DBdel()

Deletes a key from the Asterisk database (AstDB).

> DBdel(family/key)

Deletes the specified key from the Asterisk database.

Returns 0.

> ![image](images/00478.jpg)

> ### Warning
> 
> **`DBdel()`** is deprecated as of Asterisk 1.4; use the **`DB_DELETE()`** function instead.

**Asterisk versions:**

![image](images/00479.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00480.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00481.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`dbdeltree`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos826085), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`db`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1347618), [`db_delete`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1349551).**

### B.34 DBdeltree()

Deletes a family or branch from the Asterisk database.

> DBdeltree(family[/branch])

Deletes the specified branch from the Asterisk database.

Returns 0.

> ![image](images/00482.jpg)

**Asterisk versions:**

![image](images/00483.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00484.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`dbdel`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos823608), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`db`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1347618).**

### B.35 DBget()

Reads a value from the Asterisk database (AstDB).

> DBget(variable=family/key|options)

> ### Warning
> 
> **`DBget()`** is removed as of Asterisk 1.4 and has been replaced by the **`DB()`** function.

**Asterisk versions:**

![image](images/00485.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00486.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [`dbput`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos829785), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`db`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1347618).**

### B.36 DBput()

Stores a value in the Asterisk database (AstDB).

> DBput(*family/key=value*)

> ### Warning
> 
> **`DBput()`** is removed as of Asterisk 1.4 and has been replaced by the **`DB()`** function.

**Asterisk versions:**

![image](images/00487.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00488.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [`dbget`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos827978), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`db`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1347618).**

### B.37 DeadAGI()

Runs an AGI compliant program on an inactive channel.

> ![image](images/00489.jpg)

Runs an AGI-compliant program on an inactive (on hook) channel. With AGI (Asterisk Gateway Interface), you can manipulate channels with programs written in practically any conceivable language. AGI programs can control a channel, play audio, interpret and store DTMF tones; AGI programs exchange data with Asterisk on `stdin` and `stdout`. The specified arguments are passed unadulterated to the AGI program.

This application was developed for use on inactive (on hook) channels, because the standard AGI interface will not work on a channel after it is hung up. It is not necessary for the channel to be “dead” at the time of execution, however!

Returns −1 if the application causes a hangup, or returns 0 on exit without hangup.

> ![image](images/00490.jpg)

> ### Warning
> 
> The channel will be treated as active as long as the AGI program is running. This can have implications for CDRs.
> 
> Note also that DeadAGI applications receive a `SIGHUP` signal when the channel is hung up, and it may need to be explicitly ignored in your AGI program:
> 
> ![image](images/00491.jpg)

It is also important for the AGI program to stop communicating after the hangup, or it will receive a `SIGPIPE` signal and end (unless the signal is explicitly ignored as in the example above).

**Asterisk versions:**

![image](images/00492.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00493.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00494.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00495.jpg)

> ![image](images/00496.jpg)

**See also [`agi`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos740308), [`fastagi`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos910187).**

### B.38 Dial()

Connects channels.

> ![image](images/00497.jpg)

Connects two channels together.^([6](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos836110))

[6](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos836004). Generally, channels of any type supported by Asterisk may be connected (for example, IAX, SIP, H.323, Skinny, PRI, FXO, FXS, Local).

**`Dial()`** is perhaps the most important application in Asterisk. We recommend you read this section carefully and more than once if necessary.

**`Dial()`** accepts every valid channel type (e.g., SIP, IAX2, H.323, MGCP, Local, or Zap) but the allowable parameters are channel-specific; i.e., what parameters a channel requires or will accept depends on the nature of the channel technology. For example, a SIP channel will require an IP address and user information, whereas a ZAP channel requires a telephone number.

When a network-based channel type is specified, the parameters (such as IP address, user name, password, and remote extension) can be supplied as options to **`Dial()`** or, alternatively, be included in a host configuration section in the appropriate `.conf` file. If this second approach is used, all the required configuration information must be present.

Here’s an example:

> exten => s,1,Dial(SIP/richard:secret@widgets.biz)

This extension would accomplish the same thing:

> exten => s,1,Dial(SIP/a_SIP_friend)

... as long as `a_SIP_friend` is defined as a channel in `sip.conf`:

> ![image](images/00498.jpg)

Sometimes an extension is attached to the address information, as in this example:

> exten => s,1,Dial(IAX2/user:secret@widgets.biz/500)

The remote system is asked to connect the call to extension 500 in the incoming channel. This extension is not required because the channel configuration on the remote system is used, or, alternatively, the call is passed to the default `s` extension in the incoming context.

In the end, the remote host decides how the call will be processed; all you can do is request special call handling.

If no `timeout` is specified, the channel will ring indefinitely. This behavior is not necessarily undesirable and so it’s not automatically necessary to set this parameter. Just be aware that “indefinite” can end up being a very long time.

The `timeout` is specified in seconds. It always follows the device information:

> exten => s,1,Dial(IAX2/user:secret@widgets.biz/500,20)

With **`Dial()`**, you can ring multiple channels simultaneously. The call is handled on a “first come, first served” basis; the first extension to pick up answers the call, and all the other extensions stop ringing and become available:

> exten => s,1,Dial(SIP/2000&SIP/2001&SIP/2303)

A big part of the power in the **`Dial()`** application is in the options, which always follow the device and timeout information, like so:

> exten => s,1,Dial(IAX2/user:secret@widgets.biz/500,60,options)

> ### Warning
> 
> If you want to provide options, you still need to provide a comma-delimited space for the timeout value even if it is empty:
> 
> > exten => s,1,Dial(IAX2/user:secret@widgets.biz/500,,options)

Here are the valid options to the **`Dial()`** application:

> • **`d`**

> Allows the caller to dial another single-digit extension while waiting for the current extension to answer. (For example, a caller dials 4 while the phone is ringing and the call is immediately passed to the 4 extension. The extension is in the current context unless `${EXITCONTEXT}` is set.)

> • **`t`**

> Blind transfer initiated by the *called* party. Allows the called party to transfer the call by pressing the blind transfer key (normally #). Reinvites are not possible when this option is selected because Asterisk must monitor the connection to detect when the called party presses the # key.

> • **`T`**

> Blind transfer initiated by the *calling* party. Allows the calling party to transfer the call by pressing the blind transfer key (normally #). Reinvites are not possible when this option is selected because Asterisk must monitor the connection to detect when the called party presses the # key.

> • **`w`**

> Allows the *called* party to start recording the call by pressing the `automon` key sequence (as defined in `features.conf`). If the `TOUCH_MONITOR` variable is set, its value is passed to **`Monitor()`** as a parameter when recording starts. If it is not set, `WAV,,m` is passed to **`Monitor()`**.

> • **`W`**

> Allows the *calling* party to start recording the call by pressing the `automon` key sequence (as defined in `features.conf`).

> • **`f`**

> Sets the caller ID as the number of the line making or redirecting the outgoing call. Some PSTNs don’t allow IDs from extensions other than those assigned to you. For example, if you have a PRI, you would use `f` to overwrite the caller ID provided by a SIP extension to that belonging to the outgoing Zap channel on the PRI.

> • **`o`**

> Uses the caller ID received on the incoming leg of a call as the caller ID for the outgoing leg. This is useful if a call is accepted and then transferred; in the normal case, the caller ID of the initial recipient is used for the outgoing leg, which can be confusing to the ultimate recipient. For example, say Joe calls Mary; Mary decides that Joe really needs to speak to Don and transfers the call. If option o is set, Don will see Joe’s number on his display when Mary transfers him, instead of Mary’s number.

> • **`r`**

> Generate a ringing tone for the calling party. Normally Asterisk will generate a ringing tone when it is appropriate. Option `r` forces it to do so no matter the circumstance. Sometimes called devices don’t provide useful call progress information (or none at all) and `r` is needed; however, this can also lead to strange behavior, such as initial ringing interrupted by a busy signal.

> • **`m[class]`**

> Plays music to the caller until the call is answered. Optionally you can provide the Music-on-Hold class (as defined in `musiconhold.conf`).

> • **`M(x[^arg])`**

> Runs the macro x when the call is answered, optionally passing `^` (caret) separated arguments. The macro may set the `MACRO_RESULT` channel variable to one of the following values:

> • **`ABORT`**

> Hangs up both ends of the call.

> • **`CONGESTION`**

> Indicates congestion on the line.

> • **`BUSY`**

> Indicates that the line is busy (and jumps to n+101).

> • **`CONTINUE`**

> Hangs the called end up and continues in the dialplan.

> • **`GOTO:<context>^<extension>^<priority>`**

> Jumps to the specified point in the dialplan.

> • **`h`**

> Allows the *called* party to hang up by pressing *.

> • **`H`**

> Allows the *calling* party to hang up by pressing *.

> • **`C`**

> Resets the Call Detail Record (CDR) for this call. Normally, the CDR clock is reset from the moment the call is answered by Asterisk; if CDRs are being used for billing purposes, sometimes it is appropriate to reset the timer when the connection between two parties is actually established.

> • **`P[(x)]`**

> Uses the Privacy Manager if no caller ID is present, where the optional variable x is a family in the AstDB. The Privacy Manager asks the caller to enter a ten-digit telephone number if no caller ID is provided, providing a simple way to screen for telemarketers and solicitors blocking their caller ID. See also [`LookupBlacklist()`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos967831).

> • **`g`**

> Proceeds in the context when the target channel has been hung up.

> • **`G(context^extension^priority)`**

> Drops both channels into the specified *context*, *extension*, and *priority* when the call is answered.

> • **`A(x)`**

> Plays an announcement to the called party, where x is the sound file prefix. For example, A(confirm) would play the most efficient version of confirm (such as `confirm.gsm`, or `confirm.wav`) that can be found in the `/var/lib/asterisk/sounds` directory.

> • **`D([called][:`*`calling`*`])`**

> Sends DTMF digits after the call is answered but before it is bridged. The `called` digits are transmitted to the called party, the `calling` digits to the calling party. One or both parameters may be set.

> • **`L(x[:y][:z])`**

> Limits call duration to `x` milliseconds. At `y` ms before the maximum allowed duration, and thereafter every `z` ms until the end of the call, a warning is given. The *x* must be defined, *y* and *z* are optional. The behavior can be further controlled with the following variables:

> • **`LIMIT_PLAYAUDIO_CALLER=`*`yes|no`***

> Sets whether the calling party should hear announcements.

> • **`LIMIT_PLAYAUDIO_CALLEE=`*`yes|no`***

> Sets whether the called party should hear announcements.

> • **`LIMIT_TIMEOUT_FILE=`*`filename`***

> Specifies the sound file to be played after the maximum duration is reached and the call is ended.

> • **`LIMIT_CONNECT_FILE=`*`filename`***

> Specifies the sound file to be played when the call is connected.

> • **`LIMIT_WARNING_FILE=`*`filename`***

> Specifies the sound file to be played for the warning signal when *y* is set.

> • **`j`**

> Turns priority jumping on. That is, the call jumps to priority n+101 (where n is the current priority) if all the channels respond busy.

> A call may be parked instead of transferred (which is the case when `t` or `T` is used). By default, calls are parked by transferring them to extension 700, but this behavior may be configured in `features.conf`.

> • **`n`**

> Privacy Manager setting. Caller introductions are not to be saved in the priv-callerintros directory.

> • **`N`**

> Privacy Manager setting. Calls are not screened if caller ID information is provided.

When **`Dial()`** completes, the following variables are set:

> • **`DIALEDTIME`**

> The total elapsed time from the time the Dial() command is executed until its completion.

> • **`ANSWEREDTIME`**

> The time elapsed during conversation.

> • **`NOANSWER`**

> The channel was not answered before the ring timeout had expired.

> • **`BUSY`**

> The called channel is currently busy.

> • **`ANSWER`**

> The called channel was answered.

> • **`CANCEL`**

> The call was interrupted before it could be completed.

> ![image](images/00499.jpg)

**Asterisk versions:**

![image](images/00500.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00501.jpg)

> ![image](images/00502.jpg)

> ![image](images/00503.jpg)

> ![image](images/00504.jpg)

> ![image](images/00505.jpg)

> ![image](images/00506.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00507.jpg)

> ![image](images/00508.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00509.jpg)

> ![image](images/00510.jpg)

> ![image](images/00511.jpg)

> ![image](images/00512.jpg)

> ![image](images/00513.jpg)

> ![image](images/00514.jpg)

> ![image](images/00515.jpg)

**See also [`retrydial`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1140256).**

### B.39 Dictate()

Virtual dictation machine.

> Dictate*([path[,filename]]*)

Starts a virtual dictation machine. The options define the base directory (default: `/var/spool/asterisk/dictate/`) and (numerical) filename. The files are recorded in RAW format.

The user can control dictation with these keys:

> • **`0`**

> Help

> • **`1`**

> Switches between playback and record modes

> • **`*`**

> Pause / continue

> • **`#`**

> Select file / enter new filename (e.g., 1234#)

In playback mode:

> • **`2`**

> Switches the playback speed by increments (1x, 2x, 3x, 4x)

> • **`7`**

> Jumps back a set time interval

> • **`8`**

> Jumps forward a set time interval

In record mode:

> • **`8`**

> Erase recording and start over

> ![image](images/00516.jpg)

To provide every system user her own dictation machine, you might set the path to `/var/spool/asterisk/dictate/${EXTEN}`.

**Asterisk versions:**

![image](images/00517.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00518.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00519.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00520.jpg)

**See also [`record`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1127051).**

### B.40 DigitTimeout()

Sets the maximum timeout between digits when the caller is dialing.

> DigitTimeout(*seconds*)

> ### Warning
> 
> **`DigitTimeout()`** is removed as of Asterisk 1.4 and has been replaced by the **`TIMEOUT()`** function:
> 
> > Set(TIMEOUT(digit)=*seconds*)

**Asterisk versions:**

![image](images/00521.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00522.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [`absolutetimeout`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos723417), [`responsetimeout`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1138171), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`timeout`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1437375).**

### B.41 Directory()

Provides a directory of users or user voicemail box numbers. (For more on system directories and Dial-by-Name, see [Chapter 9](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos385865), “[Voicemail](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos385865).”)

> Directory(*voicemail-context[,dialplan-context[,options]]*)

Lets callers search a directory by the user’s name. The list of names and extensions is configured in `voicemail.conf`. The *voicemail-context* parameter is required.

The dialplan-context defines the context to be used when dialing the user’s extension. If this is not provided, *voicemail-context* is assumed. The only option currently accepted is `f`, which allows dialing by first name.

If the user dials 0 (zero) and the extension o exists in the current context, the call goes to this extension. Likewise, pressing * sends the call to the extension a, if it exists. This behavior is similar to that found in **Voicemail()**.

Returns 0 unless the caller hangs up.

> ![image](images/00523.jpg)

**Asterisk versions:**

![image](images/00524.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00525.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00526.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00527.jpg)

> ![image](images/00528.jpg)

**See also [`voicemail.conf`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1266771).**

### B.42 DISA()

Direct Inward System Access lets outside callers enter the system and provides them with an internal dial tone.

> ![image](images/00529.jpg)

Provides an internal dial tone to outside callers such that they can make calls as though calling from an internal extension. Upon hearing the dial tone, an access code must be entered followed by the # key. If it is correct, the caller hears another dial tone; this is the system dial tone and the caller can now dial and initiate calls.

> ### Caution
> 
> This type of access represents a serious and real security risk and should be planned and considered carefully before use, if it must be used at all!

The *password* option is a numeric access code that must be entered for the caller to be able to make calls out. Following this particular syntax, all the users that call in will use the same access code. If you want to allow unsecured access, enter the string `no-password` instead of an actual password.

The *context* option specifies the context in which the initiated call will be placed. If it is not provided, **`DISA()`** assumes the context named disa.

The *callerid* option sets the mailbox number (and the optional *voicemail-context*) of a mailbox. If the mailbox contains new messages the caller will hear a stuttered dial tone to indicate this.

Alternatively, you may use password-file to define multiple access passwords. Each line of this file can contain either an access code or a combination of an access code and a context, separated by the pipe (|) character. If no context is specified, `disa` is assumed.

If the caller successfully authenticates with a valid access code, **`DISA()`** will start the call in the specified context.

> ![image](images/00530.jpg)

**Asterisk versions:**

![image](images/00531.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00532.jpg)

> ![image](images/00533.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00534.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00535.jpg)

> ![image](images/00536.jpg)

> ![image](images/00537.jpg)

### B.43 DumpChan()

Prints information about the calling channel on the console.

> DumpChan*([min_verbose_level]*)

Shows information about the calling channel and the contents of all the channel variables. If *min_verbose_level* is set, only messages at the same or higher verbosity level are printed.

Returns 0.

> ![image](images/00538.jpg)

**Asterisk versions:**

![image](images/00539.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00540.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`noop`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1060854), [`log`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos965179), [`verbose`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1261515).**

### B.44 DUNDiLookup()

Looks up a number using DUNDi.

> DUNDiLookup(*number[|DUNDi-context[|options]]*)

> ### Warning
> 
> **`DUNDiLookup()`** is removed as of Asterisk 1.4 and has been replaced by the **`DUNDILOOKUP()`** function.

**Asterisk versions:**

![image](images/00541.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00542.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.45 EAGI()

Calls an AGI-compliant application.

> EAGI(*program[,argument1[,argument2[,...]]]*)

(Similar to **`AGI(), FastAGI(), DeadAGI()`**)

**`EAGI()`** (Extended AGI) works just like regular **`AGI()`** (agi), but also provides access to the incoming audio stream. The incoming audio stream is provided on file descriptor 3.^([7](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos881808))

[7](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos881702). A reminder: 0: stdin, 1: stdout, 2:stderr. File descriptor 3 is freely assignable.

AGI scripts or programs can be implemented in almost any conceivable language (e.g., Perl, PHP) and may be used to manipulate the channel, play sound files, interpret DTMF tones, and so on. Asterisk communicates with the AGI program over `stdin` and `stdout`. The arguments are passed directly to the AGI program at execution time.

The AGI program must be flagged as executable in the filesystem. The path is relative to the Asterisk AGI directory, which is at `/var/lib/asterisk/agi-bin` by default, or it may be stated as an absolute path.

To run AGI programs on inactive channels (as in the case of an `h` extension, where the channel is on-hook), use **`DeadAGI()`** instead.

Returns −1 on hangup or if the AGI program requests a hangup; returns 0 if no hangup is requested.

> ![image](images/00543.jpg)

**Asterisk versions:**

![image](images/00544.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00545.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00546.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00547.jpg)

> ![image](images/00548.jpg)

**See also [`agi`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos740308).**

### B.46 Echo()

Repeats incoming audio to the caller.

> Echo()

Takes any incoming audio and returns it on the same channel. This application is used primarily for troubleshooting and testing of delay (latency) and sound quality on VoIP connections. The caller can end the call by pressing #.

Returns 0 if the caller ends the call with # or −1 if the caller hangs up.

> ![image](images/00549.jpg)

**Asterisk versions:**

![image](images/00550.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00551.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00552.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`milliwatt`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1019843).**

### B.47 EndWhile()

Ends a while loop.

> EndWhile()

Returns to the previously called **`While()`** statement. For a complete description of while loops in Asterisk, see [`while`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1289713).

> ![image](images/00553.jpg)

**Asterisk versions:**

![image](images/00554.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00555.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00556.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00557.jpg)

**See also [`while`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1289713), [`gotoif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos936925).**

### B.48 EnumLookup()

Looks up a number using ENUM.

> EnumLookup(*number*)

> ### Warning
> 
> **`EnumLookup()`** is removed as of Asterisk 1.4 and was replaced by the **`ENUMLOOKUP()`** function.

**Asterisk versions:**

![image](images/00558.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00559.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.49 Eval()

Evaluates a variable twice.

> Eval(*result_variable=expression*)

> ### Warning
> 
> **`Eval()`** is removed as of Asterisk 1.4 and has been replaced by the **`EVAL()`** function.

**Asterisk versions:**

![image](images/00560.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00561.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.50 Exec()

Executes an Asterisk application dynamically.

> Exec(*application(arguments)*)

Allows the execution of an arbitrary dialplan application, even if this application is not hardcoded into the dialplan. Returns the value returned by the application or −2 if the application cannot be found. The *arguments* are passed to the called application.

This application enables the calling of applications out of a database or other external source.

> ![image](images/00562.jpg)

> ### Warning
> 
> A negative return value will mean that execution of the dialplan ends. If this is not desired, use **`TryExec()`**.

**Asterisk versions:**

![image](images/00563.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00564.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00565.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00566.jpg)

**See also [`execif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos895001), [`tryexec`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1247614), [`system`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1241478).**

### B.51 ExecIf()

Executes an Asterisk application under specific conditions.

> ExecIf(*expression,application,arguments*)

If expression evaluates to `true`, the defined application is executed with the provided arguments, and the return value is returned. See `doc/README.variables` (1.2) `/doc/channelvariables.txt` (1.4) for more information about standard expressions for Asterisk.

If expression evaluates to `false`, execution moves to the next priority in the extension.

> ![image](images/00567.jpg)

**Asterisk versions:**

![image](images/00568.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00569.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00570.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00571.jpg)

**See also [`exec`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos892191).**

### B.52 ExecIfTime()

Executes an application based on the current time.

> ExecIf(*times|daysofweek|daysofmonth|months?application[,arguments]*)

If the current time is in the time window defined, *application* is executed with *arguments* and the result returned. The time window is defined the same way as it is for `include`, **`GotoIfTime()`** (see [`gotoiftime`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos940203)) or **`IFTIME()`** (see [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249)).

If the current time is not in the time window defined, execution continues in the next priority.

**Asterisk versions:**

![image](images/00572.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00573.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00574.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00575.jpg)

**See also [`exec`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos892191), [`execif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos895001), [`gotoiftime`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos940203), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`iftime`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1383634).**

### B.53 ExitWhile()

Exits a `while` loop, irrespective of whether its condition has been satisfied.

> ExitWhile()

With **`ExitWhile()`**, you can interrupt further execution whether or not the while condition has been satisfied.

**Asterisk versions:**

![image](images/00576.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00577.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00578.jpg)

**See also [`while`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1289713), [`endwhile`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos886821).**

### B.54 ExtenSpy()

Eavesdrop on a channel attached to a specific extension and whisper to it if desired.

> ExtenSpy(*extension[@context][,options]*)

**`ExtenSpy()`** can listen to incoming and outgoing audio on channels used by the specified extension. The options:

> • **`b`**

> Only listens to channels that belong to a bridged call.

> • **`g(grp)`**

> Only listens to channels where the channel variable `${SPYGROUP}` is set to `grp. ${SPYGROUP}` can contain a colon-separated list of values.

> • **`q`**

> Do not play a tone or say the channel name when listening starts on a channel.

> • **`r([name])`**

> Records the listening session to the spool directory. A filename may be specified if desired; `chanspy` is the default.

> • **`v([value])`**

> Sets the initial volume. The value may be between −4 and 4.

> • **`w`**

> Enables “whisper” mode. Lets the spying channel talk to the spied-on channel.

> • **`W`**

> Enables “private whisper mode.” The “spying” channel can whisper to the spied-on channel, but cannot listen.

The following key controls are available while listening:

> • **`#`**

> Stepwise volume adjustment (−4 to 4)

> • **`*`**

> Switch to another channel

**Asterisk versions:**

![image](images/00579.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00580.jpg)

> ![image](images/00581.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00582.jpg)

> ![image](images/00583.jpg)

> ![image](images/00584.jpg)

> ![image](images/00585.jpg)

**See also [`chanspy`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos789899), [`zapbarge`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1294818), [`zapscan`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1299987), [`monitor`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1038634).**

### B.55 ExternalIVR()

Start an external IVR application.

> ExternalIVR(*shell-command[,arg1[,arg2[,...]]]*)

Forks a process and starts an external IVR^([8](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos908801)) application. This application then receives all DTMF events and responds accordingly. The application receives notification if the channel is hung up but must shutdown on its own. The protocol for this interface is described in `doc/externalivr.txt.`

[8](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos908411). Interactive voice response.

**Asterisk versions:**

![image](images/00586.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00587.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00588.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00589.jpg)

> ![image](images/00590.jpg)

### B.56 FastAGI()

Calls an AGI-compliant application over a network connection.

> FastAGI(*agi://hostname[:port][/script],arguments*)

(Similar to **`AGI()`**, **`DeadAGI()`**, **`EAGI()`**.)

Runs an AGI-compliant program on the current channel, but calls the application from another host on the network. The intent is to help distribute the load of processor-intensive AGI scripts or programs to remote servers and reduce startup latency of those programs. (A FastAGI script can be started before it is actually needed, much like a FastCGI script on a web server.)

**`FastAGI()`** attempts to connect directly to a running FastAGI program listening for connections on the specified port on the server hostname. The default port is 4573 if it is not specified. If script is defined, it is used to populate the variable `agi_network_script` and passed to the FastAGI program. The arguments are also passed to the program.

A sample FastAGI script can be found at `agi/fastagi-test`. Use this as a starting point for writing your own FastAGI applications.

Returns −1, if the application ends and requests a hangup; returns 0 if it ends without requesting a hangup.

> ![image](images/00591.jpg)

**See also [`agi`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos740308), [`deadagi`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos831596).**

### B.57 Festival()

Uses the free Festival text-to-speech (TTS) engine to read text to the caller.

> Festival(*text[,keys]*)

Connects to the locally running Festival server (which must be installed separately), sends it the specified text and plays the resulting audio back to the caller. If *keys* are defined, pressing of the defined keys will interrupt playback and return the value of the key depressed; if any is provided as the value to keys, all *keys* will be recognized and the call will be passed to the appropriate extension in the dialplan.

Festival must be started *before* Asterisk, and the channel must be answered with **`Answer()`**, in order for this application to work.

> ![image](images/00592.jpg)

As an alternative to the application **`Festival()`**, you may also use the **`System()`** command to call Festival’s command-line program **`text2wave`** and play back the resulting audio stream with **`Background()`** or **`Playback()`**, like so (for example only; pay attention to pathnames!):

> ![image](images/00593.jpg)

**Asterisk versions:**

![image](images/00594.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00595.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00596.jpg)

**See also `contrib/README.festival.`**

### B.58 Flash()

Performs a “flash hook” on a Zap (DAHDi) channel.

> Flash()

Performs a flash on a Zap (DAHDi) channel.

> ### Note
> 
> A flash (also called a switchhook-flash, flash hook, or link) is simply a short depressing of the hook switch on an analog telephone for between 80 and 500 milliseconds (depending on the carrier), used primarily as a signaling method to provide feature control for simple analog telephone sets (such as for call waiting, three-way calling, call transfer, and similar services).

Returns 0 upon success, or −1 if the channel is not a Zap channel.

> exten => 123,1,Flash()

If an outgoing line supports flash-transfer (usually an extra service), you might use it on a Zap channel like so:

> ![image](images/00597.jpg)

Sometimes it is necessary to adjust the flash duration; ask your carrier for the specification in your area. This can be done in `zapata.conf` with a parameter; e.g., `flash=200` (the value is in milliseconds).

**Asterisk versions:**

![image](images/00598.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00599.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00600.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00601.jpg)

### B.59 FollowMe()

Follow-Me/Find-Me functionality.

> FollowMe(*followMeID,options*)

Read the configuration file `followme.conf` for a complete explanation.

**Asterisk versions:**

![image](images/00602.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00603.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00604.jpg)

### B.60 ForkCDR()

Generates an additional CDR in the current call.

> ForkCDR()

Generates an additional CDR beginning from the moment the **`ForkCDR()`** command is called. Used for the purpose of distinguishing between total call duration and actual conversation duration for billing purposes. Option `v` will pass all the CDR variables to the new CDR.

> exten => 123,n,ForkCDR()

**Asterisk versions:**

![image](images/00605.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00606.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00607.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00608.jpg)

> ![image](images/00609.jpg)

> ![image](images/00610.jpg)

> ![image](images/00611.jpg)

**See also [`nocdr`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1059127), [`resetcdr`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1136139).**

### B.61 GetCPEID()

Retrieve the CPE-ID (customer premises equipment ID) of an ADSI-capable telephone.

> GetCPEID()

Retrieves the CPE-ID and additional information, displaying it on the Asterisk CLI. This information is often needed to properly configure `zapata.conf` to support ADSI features.

Returns −1 on hangup.

> exten => 123,1,GetCPEID()

**Asterisk versions:**

![image](images/00612.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00613.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00614.jpg)

**See also [`adsiprog`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos728673), `adsi.conf`, `zapata.conf`.**

### B.62 GetGroupCount()

Returns the number of channels in a channel group.

> GetGroupCount(*group[@category]*)

> ### Warning
> 
> **`GetGroupCount()`** is removed as of Asterisk 1.4 and has been replaced by the **`GROUP_COUNT()`** function.

**Asterisk versions:**

![image](images/00615.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00616.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [`setgroup`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1200419), [`checkgroup`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos798545), [`getgroupmatchcount`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos927449), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`group_count`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1371357).**

### B.63 GetGroupMatchCount()

Returns the number of channels in all the groups that match the supplied pattern.

> GetGroupMatchCount(*pattern[@category]*)

> ### Warning
> 
> **`GetGroupMatchCount()`** is removed as of Asterisk 1.4 and has been replaced by the **`GROUP_MATCH_COUNT()`** function.

**Asterisk versions:**

![image](images/00617.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00618.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [`setgroup`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1200419), [`checkgroup`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos798545), [`getgroupcount`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos925448), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`group_match_count`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1374893).**

### B.64 Gosub()

Jumps to the specified priority, extension, and context and allows return.

> ![image](images/00619.jpg)

Like **`Goto()`** but allows the dialplan subroutine to return with **`Return()`**.

Returns 0, or −1 if the target is invalid.

> ![image](images/00620.jpg)

**Asterisk versions:**

![image](images/00621.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00622.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00623.jpg)

**See also [`gosubif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos931860), [`goto`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos934438), [`gotoif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos936925), [`return`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1143255), [`macro`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos973726).**

### B.65 GosubIf()

Jumps to the specified priority if a condition is satisfied and allows return.

> GosubIf(*condition*?*labeliftrue*:*labeliffalse*)

Jumps to the specified priority if a condition is satisfied (similar to **`GotoIf()`**) but allows the subroutine to return with **`Return()`**.

Returns 0 or −1 if the target is invalid.

> ![image](images/00624.jpg)

**Asterisk versions:**

![image](images/00625.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00626.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00627.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00628.jpg)

**See also [`gosub`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos929505), [`goto`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos934438), [`gotoif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos936925), [`return`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1143255), [`macro`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos973726).**

### B.66 Goto()

**Jumps to a specified priority, extension, and context.**

> ![image](images/00629.jpg)

Hands the currently active channel to the specified priority (and optionally, extension and context).

Optionally, a named priority may be specified to access a labeled priority. Named priorities work only in the current extension.

Always returns 0, even if the target is invalid.

> ![image](images/00630.jpg)

**Asterisk versions:**

![image](images/00631.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00632.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00633.jpg)

**See also [`gotoif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos936925), [`gotoiftime`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos940203), [`gosub`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos929505), [`gosubif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos931860), [`macro`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos973726).**

### B.67 GotoIf()

Jumps to a specified priority, extension, and context if a condition is satisfied.

> GotoIf(condition?labeliftrue:labeliffalse)

Hands the currently active channel to the priority specified by *labeliftrue* if the condition is true, or to the priority specified in *labeliffalse* if the condition is false. Either *labeliftrue* or *labeliffalse* may be omitted (in which case execution continues with the next priority) but not both! You must include the colon delimiter (:).

In this case, a priority can be

> • A single priority (e.g., `10`)

> • an extension and a priority (e.g., `123,10`)

> • a context, extension, and priority (e.g., `incoming,123,10`)

> • a named priority in the same extension (e.g., `ok`)

> ![image](images/00634.jpg)

**Asterisk versions:**

![image](images/00635.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00636.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00637.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`goto`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos934438), [`gotoiftime`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos940203), [`gosub`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos929505), [`gosubif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos931860), [`macro`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos973726).**

### B.68 GotoIfTime()

Jumps to the specified priority if the time condition is met.

> ![image](images/00638.jpg)

Jumps to the specified priority if the current time falls within the specified time window. Each element may be defined with a * (always) or a − (range).

The arguments for this application are as follows:

> • **`times`**

> Time interval, in 24-hour format with hours and minutes (e.g., `9:00-17:00`)

> • **`daysofweek`**

> Weekdays (`mon`, `tue`, `wed`, `thu`, `fri`, `sat`, `sun`) (e.g., `mon–fri)`

> • **`daysofmonth`**

> Days of the month (`1–31`) (e.g., `1-15`

> • **`months`**

> Months of the year (`jan`, `feb`, `mar`, `apr`, `mai`, `jun`, `jul`, `aug`, `sep`, `oct`, `nov`, `dec`) (e.g., `apr-oct`)

> ![image](images/00639.jpg)

**Asterisk versions:**

![image](images/00640.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00641.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00642.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00643.jpg)

**See also [`gotoif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos936925), [`execiftime`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos897433), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`iftime`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1383634).**

### B.69 Hangup()

Hangs up the active channel.

> Hangup()

Hangs up the active channel unconditionally.

Returns −1.

> ![image](images/00644.jpg)

**Asterisk versions:**

![image](images/00645.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00646.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00647.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`answer`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos757005).**

### B.70 HasNewVoicemail()

Checks to see whether there are new messages in the specified voice mailbox.

> HasNewVoicemail(*mailbox*[/*folder*][@*context*][,*variable*,[*options*]])

> ### Warning
> 
> **`HasVoicemail()`** is removed as of Asterisk 1.6 and was already superfluous in 1.2\. The same thing can be achieved with the **`VMCOUNT()`** function:
> 
> > Set(number=${VMCOUNT(4000|0)})
> 
> New messages reside in folder 0.

**Asterisk versions:**

![image](images/00648.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00649.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00650.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

**See also [`hasvoicemail`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos949064), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`vmcount`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1445448).**

### B.71 HasVoicemail()

Checks to see whether there are messages in the specified voice mailbox.

> HasVoicemail(*mailbox[/folder][@context][,variable,[options]]*)

> ### Warning
> 
> **`HasVoicemail()`** is removed as of Asterisk 1.6 and was already superfluous as of 1.2\. The same thing can be achieved using the **`VMCOUNT()`** function:
> 
> > Set(number=${VMCOUNT(4000)})

**Asterisk versions:**

![image](images/00651.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00652.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00653.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

**See also [`hasnewvoicemail`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos946521), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`vmcount`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1445448).**

### B.72 IAX2Provision()

Provision a calling IAXy device, optionally using the specified template.

> IAX2Provision*([template]*)

Provisions a calling IAXy device with template. If no template is used, the default is used. IAXy templates are defined in `iaxprov`*`.`*`conf`.

Returns 0 on success or −1 on failure.

> exten => 123,1,IAX2Provision(default)

**Asterisk versions:**

![image](images/00654.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00655.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### B.73 ICES()

Streams the active channel to IceCast server.

> ICES(*config_file.xml*)

Sends an audio stream of the active channel to an IceCast server.^([9](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos953899))

[9](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos953793). [http://en.wikipedia.org/wiki/Icecast](http://en.wikipedia.org/wiki/Icecast)

For a sample *config_file.xml,* see `contrib/asterisk-ices.xml`.

**Asterisk versions:**

![image](images/00656.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00657.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00658.jpg)

### B.74 ImportVar()

Sets a variable with the contents of a channel variable from another channel.

> ImportVar(*newVariable=channel,variable*)

Sets the variable `newVariable` to the value contained in `variable` in the specified channel. If `newVariable` begins with _, single inheritance is used; if it begins with __, unlimited inheritance is used.

> ![image](images/00659.jpg)

**Asterisk versions:**

![image](images/00660.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00661.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00662.jpg)

**See also [`set`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1175585).**

### B.75 Incomplete()

Indicates that the extension as dialed thus far is incomplete.

> Incomplete(options)

Indicates to the calling channel that the dialed extension is not complete; that is, Asterisk needs more digits to make a match. If the option n is set, it will not answer the channel.

> ![image](images/00663.jpg)

**Asterisk versions:**

![image](images/00664.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00665.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [`progress`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1096214), [`proceeding`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1094835).**

### B.76 JabberSend()

Sends a message via Jabber.

> JabberSend(jabber_id,recipient,message)

Sends an instant message message via Jabber (XMPP, Google Talk) using a Jabber identity *jabber_id* defined in `jabber`*`.`*`conf` to the *recipient* Jabber account.

> ![image](images/00666.jpg)

**Asterisk versions:**

![image](images/00667.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00668.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00669.jpg)

**See also [`jabberstatus`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos961377), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see `jabber_status`, `jabber.conf`.**

### B.77 JabberStatus()

Returns the status of a Jabber user.

> JabberStatus(*jabber_id,jabber_account,variable*)

Checks the status of the Jabber user *jabber_account* and sets *variable* accordingly. The Jabber identity *jabber_id* as configured in `jabber`*`.`*`conf` is used for the connection.

For more information, see [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249)..

> ![image](images/00670.jpg)

**Asterisk versions:**

![image](images/00671.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00672.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00673.jpg)

**See also [`jabbersend`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos959134), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see `jabber_status`, `jabber.conf.`**

### B.78 KeepAlive()

Internal helper function.

> KeepAlive()

> ### Warning
> 
> This application is used internally by Asterisk. Do not run it in your dialplans!

**Asterisk versions:**

![image](images/00674.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00675.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### B.79 Log()

Sends a specified message to the specified log level.

> Log(*level,message*)

Delivers a specified message to a defined log level.

> • **`level`**

> One of the following target levels: `ERROR`, `WARNING`, `NOTICE`, `DEBUG`, `VERBOSE`, `DTMF`

> • **`message`**

> The message to be written to the log

**Asterisk versions:**

![image](images/00676.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00677.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00678.jpg)

**See also [`noop`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1060854), [`dumpchan`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos877102), [`verbose`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1261515).**

### B.80 LookupBlacklist()

Checks the caller ID of a call against the local number blacklist in the Asterisk database (AstDB).

> LookupBlacklist([options])

Searches for the caller ID number (or name) of the active channel in the `blacklist` family of the AstDB. If the option `j` is given, the number exists in the AstDB and the priority n+101 exists, the channel is handed to that priority. If no caller ID is available, the application does nothing.

Sets the channel variable `LOOKUPBLSTATUS` to `FOUND` or `NOTFOUND`.

To add numbers to the blacklist from the CLI, enter `database put blacklist` “`number`” “`1`”; similarly `database del blacklist` “*`number`*” to delete the entry and `database` show `blacklist` for a listing of all the entries in the database.

> ![image](images/00679.jpg)

You can accomplish the same effect as **`LookupBlacklist()`** with the following dialplan entries:

> ![image](images/00680.jpg)

**Asterisk versions:**

![image](images/00681.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00682.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00683.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

### B.81 LookupCIDName()

Looks up a caller ID name in the AstDB.

> LookupCIDName()

Looks up the caller ID number in the AstDB (family `cidname`), and, if it exists, sets the corresponding caller ID name. This application does nothing if no caller ID is present. **`LookupCIDName()`** can be useful if you receive number information but no names, or if you want to change the caller ID information certain incoming calls.

Returns 0.

To add entries to the list from the CLI enter `database put cidname` “*`number`*” “*`name`*”; similarly enter `database del cidname` “*`number`*” to delete entries and `database show cidname` to print a list of all the entries in the database.

> ![image](images/00684.jpg)

**Asterisk versions:**

![image](images/00685.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00686.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00687.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

### B.82 Macro()

Executes a previously defined macro.

> Macro(macroname[,arg1[,arg2[,...]]])

Executes a macro defined in the context `macro`-`macroname` by handing the channel over to the s extension in the macro and returning after the macro has finished running.

The called extension, context, and priority are passed to the macro in the variables `$`{`MACRO`_`EXTEN`}, `$`{`MACRO`_`CONTEXT`} and `$`{`MACRO`_`PRIORITY`}. The arguments are passed to the macro in `${ARG1}`, `${ARG2}`, and so on.

**`Macro()`** returns −1 if any step in the macro returns −1, otherwise it returns 0\. If the variable `${MACRO_OFFSET}` is set when the macro finishes, the application will continue executing at priority *`n`*`+1+MACRO_OFFSET` if it exists, otherwise it will continue at *n*+1.

If **`Goto()`** is called from within the macro, macro execution ends and the call continues in the priority specified in **`Goto()`**.

> ![image](images/00688.jpg)

**Asterisk versions:**

![image](images/00689.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00690.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00691.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00692.jpg)

**See also [`goto`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos934438), [`gosub`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos929505).**

### B.83 MacroExclusive()

Executes a previously defined macro but allows only a single instance of the macro to execute at any given point in time.

> MacroExclusive(*macroname[,arg1[,arg2[,...]]]*)

Executes, same as **`Macro()`**, a macro defined in `macro`-`macroname`, by handing the channel over to the `s` extension in the macro and returning after the macro has finished running, but allows only a single instance to run at any given time! If the same macro is called at the same time from elsewhere in the dialplan, this second instance must wait until the first instance has completed.

The called extension, context and priority are passed to the macro in the variables `${MACRO_EXTEN}`, `${MACRO_CONTEXT}`, and `${MACRO_PRIORITY}.` The arguments are passed to the macro in `${ARG1}`, `${ARG2}`, and so on.

**`Macro()`** `returns` −1 if any step in the macro returns −1, otherwise it returns 0\. If the variable `${MACRO_OFFSET}` is set when the macro finishes, the application will continue executing at priority `n+1+MACRO_OFFSET` if it exists, otherwise it will continue at n+1.

If **`Goto()`** is called from within the macro, macro execution ends and the call continues in the priority specified in **`Goto()`**.

> ![image](images/00693.jpg)

**Asterisk versions:**

![image](images/00694.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00695.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00696.jpg)

**See also [`macro`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos973726), [`goto`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos934438), [`gosub`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos929505), `doc`/`macroexclusive.txt`.**

### B.84 MacroExit()

Interrupts execution of a macro.

> MacroExit()

May be used within a macro to end execution of the macro as though there were no further priorities remaining.

**Asterisk versions:**

![image](images/00697.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00698.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`macro`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos973726).**

### B.85 MacroIf()

Conditionally starts different macros.

> MacroIf(*expression?macronameA[,argA1][:macronameB[,argB1]]*)

Calls a macro depending on a condition (defined in the same way as in **`GotoIf()`**).

**Asterisk versions:**

![image](images/00699.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00700.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00701.jpg)

**See also [`macro`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos973726), [`gotoif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos936925), [`gosubif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos931860).**

### B.86 mailboxExists()

Checks to see whether the specified voicemail box exists.

> mailboxExists(*mailbox[@context][,options]*)

Checks to see whether the voicemail box defined in *mailbox* exists. A voicemail context may be specified if the mailbox being checked is not in the default context.

Sets the channel variable `VMBOXEXISTSSTATUS to SUCCESS` (mailbox found) or `FAILED` (mailbox not found).

Option `j` enables jumping to priority n+101 on success.

> ![image](images/00702.jpg)

**Asterisk versions:**

![image](images/00703.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00704.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00705.jpg)

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.87 Math()

Performs simple mathematical operations.

> Math(*output*_*variable*,*number1*<*operator*>*number2*)

> ### Warning
> 
> **`Math()`** is removed as of Asterisk 1.4 and has been replaced by the **`MATH()`** function.

**Asterisk versions:**

![image](images/00706.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00707.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.88 MD5()

Computes the MD5 checksum of a string.

> MD5(*output*_*variable*=*string*)

> ### Warning
> 
> The application **`MD5()`** is removed as of Asterisk 1.4 and has been replaced by the **`MD5()`** function.

**Asterisk versions:**

![image](images/00708.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00709.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [`md5check`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos990738), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`md5`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1396053).**

### B.89 MD5Check()

Verifies the MD5 checksum against a supplied string.

> MD5Check(*MD5checksum*|*string*|*options*)

> ### Warning
> 
> **`MD5Check()`** is removed as of Asterisk 1.4 and has been replaced by the **`MD5()`** function.

**Asterisk versions:**

![image](images/00710.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00711.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [`md5`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos988884), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`md5`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1396053).**

### B.90 MeetMe()

Places the caller in a MeetMe conference.

> MeetMe([*conference*][,*options*[,*PIN*]])

Connects the caller in the current channel to a MeetMe conference defined by *conference.* If this is not specified, the application asks the caller to enter a conference number.

If `PIN` is correctly set to the PIN (personal identification number) of the conference (set statically in `meetme.conf` or dynamically by the conference operator) the caller is placed directly into the conference; otherwise, the caller must enter the PIN first.

> ### Warning
> 
> MeetMe conferences require a Zaptel interface to be installed in the Asterisk server; these provide a time source for synchronization of the participating channels. If no Zaptel interface is available, the `ztdummy` driver may be used.
> 
> MeetMe conferences always use the ul-aw codec internally. The more conference participants use other codecs such as GSM or a-law, the higher the processor load due to transcoding.

Valid options include the following:

> • **`a`**

> Sets admin mode.

> • **`A`**

> Marks the joining user as a special participant (see `w` and `x`).

> • **`b`**

> Starts the AGI script defined in `${MEETME_AGI_BACKGROUND}`, `conf-background` by default. (Works only if all the channels in the conference are Zap channels.) The script is passed all DTMF key-presses; will not work in combination with options that also capture DTMF (such as `p`).

> • **`c`**

> Announces the number of participants to a joining user.

> • **`d`**

> Dynamically allocates a new conference.

> • **`D`**

> Dynamically allocates a new conference but asks the user to set a PIN. (If no PIN is desired, the user must press #.)

> • **`e`**

> Selects an empty conference.

> • **`E`**

> Selects an empty conference that does not require a PIN.

> • **`i`**

> Announces join and exit of new participants with review (works only with Zap channels).

> • **`I`**

> Announces join and exit of new participants without review (works only with Zap channels).

> • **`m`**

> Listen-only mode.

> • **`M`**

> Music-on-hold mode. Plays music-on-hold if there is only one participant in the conference.

> • **`o`**

> Sets talker optimization. Improves conference quality and reduces transcoding overhead by muting participants who are not currently speaking.

> • **`p`**

> Participants may leave by pressing #.

> • **`P`**

> Requests a PIN even if it is provided in the command.

> • **`q`**

> Quiet mode. Does not play entry/exit notification tones.

> • **`r`**

> Records a conference. File: `${MEETME_RECORDINGFILE}`, format: `${MEETME_RECORDINGFORMAT}`. Default filename is `meetme-conf-rec-${`*`conference`*`}-${`*`uniqueID`*`}`. The default format is WAV. (Works only with Zap channels.)

> • **`s`**

> Switches to menu (user or admin) * is pressed.

> • **`t`**

> Talk-only mode.

> • **`T`**

> Talker detection. (Information is sent to the Manager interface and displayed in the MeetMe list in the CLI.)

> • **`v`**

> Video mode (not yet implemented).

> • **`w`**

> Wait until the marked participant joins the conference. Until this point, the other participants will hear music-on-hold.

> • **`x`**

> Ends the conference when the last marked participant exits (see `A`).

> • **`X`**

> Participants may exit the conference by dialing a single-digit extension in the `${MEETME_EXIT_CONTEXT}` context, or the current context if this variable is not defined. Option `X` does not work with `p` or `s`.

> • **`1`**

> Does not play the “You are currently the only person in this conference” message when the first conference participant enters.

You can use `e` (or `E`) together with `d` (or `D`) to dynamically open a new conference. This means you will have to find a way of distributing the conference number to the other users, or employ some dialplan logic to accomplish the same objective.

> ### Note
> 
> The options `d` or `D` *dynamically* open conferences; conferences are defined *statically* in `meetme.conf`.

> ![image](images/00712.jpg)

**See also [`meetmeadmin`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1010250), [`meetmecount`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1017410).**

#### B.90.1 Commands in the CLI

The following commands are for administering conferences from the CLI. (The value *participant* is the number of participant as displayed in the participant list):

> • **`MeetMe`**

> List all conferences

> • **`MeetMe list` *`conference`***

> List the participants in the specified conference

> • **`MeetMe kick` *`conference participant`***

> Kicks a participant out of the conference

> • **`MeetMe kick` *`conference`***

> Kicks all participants out of the conference

> • **`MeetMe lock` *`conference`***

> Locks a conference to new participants

> • **`MeetMe unlock` *`conference`***

> Unlocks a previous lock (see above)

> • **`MeetMe mute` *`conference participant`***

> Mute a conference participant

> • **`MeetMe unmute` *`conference participant`***

> Unmute a conference participant (see above)

**Asterisk versions:**

![image](images/00713.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00714.jpg)

> ![image](images/00715.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00716.jpg)

> ![image](images/00717.jpg)

> ![image](images/00718.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00719.jpg)

> ![image](images/00720.jpg)

> ![image](images/00721.jpg)

**See also [`meetmecount`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1017410), [`meetmeadmin`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1010250), [`meetmechanneladmin`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1014763), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see `meetme_info`.**

### B.91 MeetMeAdmin()

Administers a MeetMe conference.

> MeetMeAdmin(*conference*,*command*[,*participant*])

Executes a command in the specified conference. The command may be one of the following (the *`participant`* is required only for the kick command (*`k`*)):

> • **`K`**

> Kicks all participants out of the conference

> • **`k`**

> Kicks *`participant`* out of the conference

> • **e**

> Kicks the last participant who joined out of the conference

> • **L**

> Locks the conference to new participants

> • **l**

> Unlocks the conference

> • **M**

> Mutes a conference participant

> • **m**

> Unmutes a muted participant

> • **N**

> Mutes everyone except the conference administrator

> • **n**

> Unmutes everyone mute by `N`

> ![image](images/00722.jpg)

**Asterisk versions:**

![image](images/00723.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00724.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00725.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`meetme`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos992604), [`meetmecount`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1017410).**

### B.92 MeetMeChannelAdmin()

Channel-specific MeetMe conference administration.

> MeetMeChannelAdmin(*channel*,*command*)

Executes the supplied MeetMe command for the specified channel. Works similar to **`MeetMeAdmin()`** but on a specific channel instead of a conference.

The command *command* can be one of the following:

> • **`k`**

> Kicks the participant on the channel from the conference

> • **`M`**

> Mutes the participant on the channel

> • **`m`**

> Unmutes the participant on the channel

**Asterisk versions:**

![image](images/00726.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00727.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [`meetme`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos992604), [`meetmeadmin`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1010250).**

### B.93 MeetMeCount()

Counts the number of participants in a MeetMe conference.

> MeetMeCount(*conference*[,*variablename*])

Announces the number of participants in the conference. If the variable name is provided, the announcement is skipped and the count written to this variable.

Returns 0 on success, −1 on error.

This example counts the participants in conference 501 and stores the number in `${COUNT}`.

> ![image](images/00728.jpg)

**Asterisk versions:**

![image](images/00729.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00730.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00731.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00732.jpg)

**See also [`meetme`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos992604), [`meetmeadmin`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1010250).**

### B.94 Milliwatt()

Generates a 1,000Hz test tone on a channel.

> Milliwatt()

Milliwatt tone lines are used by telecommunications carriers for testing and measuring line characteristics. They can be used to check for echo, excessive or inadequate volume, or some kinds of line noise. Standard milliwatt test tones are 1,004Hz at 0 dbm (u-law).

> ![image](images/00733.jpg)

**Asterisk versions:**

![image](images/00734.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00735.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00736.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`echo`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos884750).**

### B.95 MinivmAccMess()

Records messages for the Mini-Voicemail system.

> MinivmAccMess(*user@domain*,*option*)

Records messages for the given user account in the Mini-Voicemail system (`minivm`). If the account-specific directories do not exist, they are created.

Possible values for *option*:

> • **`u`**

> Record unavailable message

> • **`b`**

> Record busy message

> • **`t`**

> Temporary away message to be played prior to regular unavailable or busy messages; see [`minivmgreet`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1027057)

> • **`n`**

> Account name

> ![image](images/00737.jpg)

**Asterisk versions:**

![image](images/00738.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00739.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [`minivmdelete`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1025239), [`minivmgreet`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1027057), [`minivmnotify`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1030288), [`minivmrecord`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1032190), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see `minivmaccount`, `minivmcounter`.**

### B.96 MinivmDelete()

Delete message in Mini-Voicemail.

> MinivmDelete(*filename*)

Deletes the file *filename* in Mini-VoiceMail (`minivm`).

**Asterisk versions:**

![image](images/00740.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00741.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [`minivmaccmess`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1021838), [`minivmgreet`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1027057), [`minivmnotify`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1030288), [`minivmrecord`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1032190), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see `minivmaccount`, `minivmcounter`.**

### B.97 MinivmGreet()

Play back Mini-VoiceMail greeting.

> MinivmGreet(*user@domain*[,*option*])

Plays the default or user-specific greeting (see [`minivmaccmess`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1021838)) for Mini-VoiceMail (`minivm`).

Possible *option* settings:

> • **`b`**

> Play busy message

> • **`u`**

> Play unavailable message

> • **`s`**

> Skip the playback of instructions for leaving a message

Combinations are allowed but `b` and `u` together are nonsensical. If a temporary message has been set, it is played and `b` or `u` is ignored.

**Asterisk versions:**

![image](images/00742.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00743.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [`minivmaccmess`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1021838), [`minivmdelete`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1025239), [`minivmnotify`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1030288), [`minivmrecord`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1032190), [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249): `minivmaccount`, and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see `minivmcounter`.**

### B.98 MinivmNotify()

Sends e-mail notification of new Mini-Voicemail messages.

> MinivmNotify(*user@domain*,*template*)

Provides e-mail notification of new Mini-VoiceMail (`minivm`) messages to the specified e-mail address.

**Asterisk versions:**

![image](images/00744.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00745.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [`minivmaccmess`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1021838), [`minivmdelete`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1025239), [`minivmgreet`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1027057), [`minivmrecord`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1032190), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see `minivmaccount`, `minivmcounter`.**

### B.99 MinivmRecord()

Record a voicemail in Mini-VoiceMail.

> MinivmRecord(*user@domain*[,*option*])

Records the caller’s voicemail message in the Mini-Voicemail (`minivm`) system. This is more or less the equivalent to `VoiceMail()` (`voicemail`).

**Asterisk versions:**

![image](images/00746.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00747.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [`minivmaccmess`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1021838), [`minivmdelete`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1025239), [`minivmgreet`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1027057), [`minivmnotify`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1030288), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see `minivmaccount`, `minivmcounter`.**

### B.100 MixMonitor()

Records the audio on the current channel but mixes it before writing it to a file.

> MixMonitor(*fileprefix*.*format*[,*options*[,*command*]])

Starts recording the audio on the current channel. Instead of recording each direction in a separate file the way **`Monitor()`** would, mixes the two audio streams on-the-fly and writes the result to the specified file.

Options:

> • **`a`**

> Appends the audio stream to an existing file.

> • **`b`**

> Saves audio to the file only while the channel is bridged; i.e., once a conversation has actually begun, and only until it is hung up.

> • **`v(`*`x`*`)`**

> Adjusts the heard volume by an increment of `x` (range −4 to 4).

> • **`V(`*`x`*`)`**

> Adjusts the spoken volume by an increment of `x` (range −4 to 4).

> • **`W(`*`x`*`)`**

> Adjusts both heard and spoken volume by an increment of `x` (range −4 to 4).

The *command* (if provided) is executed after recording. The variable `${MIXMONITOR_FILENAME}` is set to the filename used for the recording.

**See also additional information in the description of Monitor().**

**Asterisk versions:**

![image](images/00748.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00749.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00750.jpg)

**See also [`monitor`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1038634).**

### B.101 Monitor()

Records the current channel in two separate files.

> Monitor([*format*[,*fileprefix*[,*options*]]])

Starts audio recording on the current channel. Incoming and outgoing audio packets are written to separate files until the channel is hung up or monitoring is stopped with **`StopMonitor()`**.

The parameter *format* sets the file format. If this is not specified, `wav` is used.

The parameter *fileprefix* specifies the filename without extension. If this is not specified, the filename is assembled out of the channel name and a number, for example, `IAX2[foo@bar]-3`. Incoming audio is written to *`fileprefix-in.format`*, outgoing audio in *`fileprefix-out.format`*, both in `/var/spool/asterisk/monitor`.

Two options may be specified:

> • **`m`**

> After recording is complete, mixes the incoming and outgoing audio files into a single file and deletes the originals. Requires that **`soxmix`** from the **`sox`** package be installed on the server.^([10](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1040814))

[10](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1040694). [http://sox.sourceforge.net/](http://sox.sourceforge.net/); see also an explanation in `musiconhold.conf`, version 12.17.7 or newer. You may check your installed version with **`soxmix –help.`**

> If the variable `${MONITOR_EXEC}` is defined, this application is executed instead of **`soxmix`** and the original incoming and outgoing audio files are not deleted.^([11](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1041607))

[11](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1041487). Depends on Asterisk version; older versions do not delete automatically. It’s best to check with a proper test.

> **`soxmix`** (or `${MONITOR_EXEC}` if specified) is passed three values: the names of the incoming and outgoing audio files and the name of the mixed file, which is the fileprefix without `-in/-out`. If `${MONITOR_EXEC_ARGS}` is set, the contents are used as arguments to `${MONITOR_EXEC}`.

> ### Warning
> 
> Note that **`soxmix`** attempts to determine the file type based on the file extension. Formats such as GSM and WAV are normally not a problem, but for other formats such as a-law and u-law, it expects the file extensions .al and .ul, respectively. To resolve this, read the manual pages for **`sox`** (**`/soxmix`**) and use `${MONITOR_EXEC_ARGS}` or write a small wrapper script that reads the format parameter and call it in `${MONITOR_EXEC}`.

> ### Note
> 
> If you wanted a single mixed sound file, **`MixMonitor()`** is usually the better option, as it mixes on-the-fly and thereby avoids a spike in CPU load at the end of the recording.

> • **`b`**

> Saves audio to the file only while the channel is bridged; i.e., once a conversation has actually begun, and only until it is hung up.

Returns 0 on success, or −1 on failure (such as a failure to open the audio files for writing, or the channel is already being monitored, and so on).

> ![image](images/00751.jpg)

> ### Warning
> 
> Before recording conversations, make sure you are complying with the relevant legislation in your jurisdiction. In most cases, both parties must be aware they are being recorded.^([12](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1044871))
> 
> [12](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1044764). See also [www.voip-info.org/wiki/view/Monitor+Recording+Legal+Issues](http://www.voip-info.org/wiki/view/Monitor+Recording+Legal+Issues).

> ### Note
> 
> Some Asterisk users who routinely need to record many conversations (50 to 500) report much better performance if call recordings are written to a RAM disk (fewer and shorter seek operations) before being copied to a hard disk when the conversation is over.

**Asterisk versions:**

![image](images/00752.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00753.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00754.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00755.jpg)

**See also [`changemonitor`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos778548), [`stopmonitor`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1235968), [`pausemonitor`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1076675), [`unpausemonitor`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1255085), [`mixmonitor`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1034188), [`record`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1127051).**

### B.102 Morsecode()

Transmits the provided string as Morse code.

> Morsecode(*string*)

Plays back the provided string in Morse code.

> ![image](images/00756.jpg)

**Asterisk versions:**

![image](images/00757.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00758.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00759.jpg)

### B.103 MP3Player()

Plays an MP3 file or stream.

> MP3Player(*filename*)

Uses `mpg123`^([13](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1049625)) to play back an MP3 to the caller. The filename may also be a URL. The caller may interrupt playback by pressing any key.

[13](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1049396). [http://mpg123.org/](http://mpg123.org/), [http://sourceforge.net/projects/mpg123/](http://sourceforge.net/projects/mpg123/); for Mac OS X, see also [http://sourceforge.net/projects/mosx-mpg123/](http://sourceforge.net/projects/mosx-mpg123/).

Asterisk is sensitive to the version of `mpg123` used. At the time of this writing the most stable version was 0.59r; using other versions may produce unexpected results.

> ### Note
> 
> The popular alternative to `mpg123`, `mpg321`, does *not* work reliably with Asterisk.

Returns −1 if the channel is hung up, otherwise returns 0.

> ![image](images/00760.jpg)

**Asterisk versions:**

![image](images/00761.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00762.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00763.jpg)

### B.104 MSet()

Sets one or more variables simultaneously.

> MSet(*variable* = *value*)

Asterisk 1.2 and 1.4 used **`Set()`** to set multiple variables. This functionality was removed from **`Set()`** in 1.6 and **`MSet()`** was added to provide it.

> exten => 123,1,MSet(var1=value1,var2=value2)

> ### Warning
> 
> **`MSet()`** isn’t really necessary. If you have to convert your dialplan anyway, we recommend you use multiple **`Set()`** statements:
> 
> > ![image](images/00764.jpg)

**Asterisk versions:**

![image](images/00765.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00766.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [`set`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1175585), [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.105 MusicOnHold()

Plays music on the channel.

> MusicOnHold(*class*[,*duration*])

Plays music belonging to the specified *`class`*, as configured in `musiconhold.conf`. If *`class`* is not specified, the default class for the channel is used. To set the default class for the channel, use the function **`MUSICCLASS()`**.

The *`duration`* parameter was added in Asterisk 1.6\. If it is omitted, music plays until the channel is hung up. If you want to fix the duration in Asterisk 1.4, use **`WaitMusicOnHold()`**.

Returns only −1 when the channel is hung up.

> ![image](images/00767.jpg)

**Asterisk versions:**

![image](images/00768.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00769.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00770.jpg)

**See also [`waitmusiconhold`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1284851), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`musicclass`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1397468).**

### B.106 NBScat()

Plays back a local NBS stream.

> NBScat()

Uses `nbscat8k` to retrieve a local NBS (Network Broadcast Sound) stream. (Take a look at the `nbs` module in Digium’s Asterisk CVS for more information.) The caller can exit by pressing any key.

Returns only −1 when the channel is hung up.

> ![image](images/00771.jpg)

**Asterisk versions:**

![image](images/00772.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00773.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00774.jpg)

### B.107 NoCDR()

Suppresses generation of a Call Detail Record for the call on the current channel.

> NoCDR()

Suppresses generation of a CDR for the current call.

> ![image](images/00775.jpg)

**Asterisk versions:**

![image](images/00776.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00777.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`forkcdr`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos920543).**

### B.108 NoOp()

Does nothing.

> NoOp(*text*)

This application does absolutely nothing (well, not *exactly*). You can use **`NoOp()`** to print text to the Asterisk CLI, which can be very useful.

The text need not be between quotation marks. If they are entered, they will be printed on the CLI along with the rest of the text.

> ### Warning
> 
> Text from **`NoOp()`** appears on the CLI at verbose level 3 or higher. You can set this in the CLI with **`set verbose 3`** or by invoking the Asterisk CLI with **`asterisk -vvvr.`**
> 
> > exten => 123,1,NoOp(Caller-ID: ${CALLERID})

**Asterisk versions:**

![image](images/00778.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00779.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00780.jpg)

**See also [`dumpchan`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos877102), [`log`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos965179), [`verbose`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1261515).**

### B.109 ODBCFinish()

Clears the resultset of a multirow ODBC (Open Database Connectivity) query.

> ODBCFinish(*resultset_id*)

Clears the resultset of an ODBC query (see [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249)) that returned multiple rows.

**Asterisk versions:**

![image](images/00781.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00782.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.110 Page()

Pages an extension.

> Page(*technology*/*resource*[&*technology2*/*resource2*[&...]][,*options*])

The designated devices are dropped into a dynamically generated conference room with their microphones muted. The only device that can send audio is that of the person paging. When the page is finished the room is struck. Options:

> • **`d`**

> Activates full-duplex audio.

> • **`q`**

> Suppresses the notification tone at the beginning of the page.

> • **`r`**

> The page is recorded to a file.

> exten => 123,1,Page(SIP/2000&SIP/2001&SIP/2002)

> ### Tip
> 
> Most devices treat a page like any other call. If the device is not explicitly instructed to auto-answer, it will simply ring, and the intended recipient will not hear the message. SIP devices can be told to auto-answer, often by setting a SIP header. Every device is different; review the administration manuals for your SIP phone.

**Asterisk versions:**

![image](images/00783.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00784.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00785.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00786.jpg)

### B.111 Park()

Parks the current call.

> Park(*extension*)

Parks the active call, typically in combination with an attended transfer so that you can know where the call has been parked. This application is registered internally, so it shouldn’t be necessary to add it into the dialplan, though you should make sure it is enabled in `features.conf`. You may include the context with the `include => parkedcalls` statement.

> ![image](images/00787.jpg)

**Asterisk versions:**

![image](images/00788.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00789.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00790.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00791.jpg)

**See also [`parkandannounce`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1070924), [`parkedcall`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1074434).**

### B.112 ParkAndAnnounce()

Parks the current call and announces the parking space on the specified channel.

> ParkAndAnnounce(*template*,*timeout*,*channel*[,*return*-*context*])

Parks the current call in the parking lot, but announces the parking space on another, specified channel. The *`template`* specifies a colon-delimited list of sound files to be played; the word `PARKED` in the example below is replaced with the parking space number assigned to the parked call. The *`timeout`* sets the maximum time the call may be parked before it is placed back in the *`return`*-*`context`*. The *`channel`* denotes the channel on which the announcement is to be made (in our example, Console/dsp prints the announcements to the Asterisk console). The *`return`*-*`context`* is a label in **`GoTo()`** format that determines the context to return the call to if it is not retrieved from the parking lot by a user within the defined *`timeout`* window. The default return priority is *n*+1 in *`return`*-*`context`*.

> ![image](images/00792.jpg)

**Asterisk versions:**

![image](images/00793.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00794.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00795.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00796.jpg)

**See also [`park`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1068573), [`parkedcall`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1074434).**

### B.113 ParkedCall()

Retrieves a parked call.

> ParkedCall(*extension*)

Connects the channel to a parked call identified by *`extension`*. This application is registered internally so it shouldn’t be necessary to add it into the dialplan, though you should make sure it is enabled in `features.conf`. You may include the context with the `include => parkedcalls` statement.

> ![image](images/00797.jpg)

**Asterisk versions:**

![image](images/00798.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00799.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00800.jpg)

**See also [`park`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1068573), [`parkandannounce`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1070924).**

### B.114 PauseMonitor()

Stops monitoring of a channel.

> PauseMonitor()

Stops recording of a channel until it is resumed with **`UnpauseMonitor()`**.

**Asterisk versions:**

![image](images/00801.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00802.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00803.jpg)

**See also [`monitor`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1038634), [`unpausemonitor`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1255085), [`stopmonitor`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1235968), [`changemonitor`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos778548).**

### B.115 PauseQueueMember()

Pauses a queue device so that it cannot take calls from the queue.

> PauseQueueMember([*queue*],*interface*[,*options*])

Blocks calls for a queue member until expressly reenabled, either with **`UnpauseQueueMember()`** or through the Manager interface. If no queue is specified, the device is paused in every queue in which it is a member. If a queue is specified but the device is not a member in it, or if no queue is specified and the device does not belong to any queues *and* option `j` is set, execution proceeds at priority n+101 if it exists.

Returns 0 on success, otherwise returns −1 if the interface cannot be found or the jump priority does not exist. Sets the channel variable `PQMSTATUS` to `PAUSED` or `NOTFOUND`.

> ![image](images/00804.jpg)

**Asterisk versions:**

![image](images/00805.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00806.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00807.jpg)

**See also [`unpausequeuemember`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1256878).**

### B.116 Pickup()

Answer a call directed at another extension.

> Pickup(*extension*[@*context*][&*extension2*@*context2*[&...]])

**`Pickup()`** allows a user to answer a channel that is ringing another extension.

> exten => 1234,1,Pickup(2000@sales)

**Asterisk versions:**

![image](images/00808.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00809.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00810.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00811.jpg)

**See also [`pickupchan`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1083480).**

### B.117 PickupChan()

Answer a call to a ringing channel.

> PickupChan(*channel*[&*channel*[...]])

**`Pickup()`** allows a call directed to another extension to be answered. **`PickupChan()`** works similarly but it can answer any ringing channel irrespective of extension.

**Asterisk versions:**

![image](images/00812.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00813.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [`pickup`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1081388).**

### B.118 Playback()

Plays a sound file to the caller.

> Playback(*filename*[,*options*])

Plays *`filename`* (in the directory `/var/lib/asterisk/sounds`) to the caller. The filename does not include an extension; Asterisk automatically selects the format with the lowest transcoding cost. Options may be specified.

The option `skip` causes the message to be skipped if the channel is not in the up state.

Answers the channel before the audio file is played, unless `noanswer` is specified. Note that not all channels support playback when “on hook.”

Returns −1 when the channel is hung up. If the file cannot be found, jumps to priority n+101 if it exists.

> ![image](images/00814.jpg)

**Asterisk versions:**

![image](images/00815.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00816.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00817.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00818.jpg)

**See also [`background`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos766468).**

### B.119 Playtones()

Plays back one or more tones.

> Playtones(*tones*)

Plays a list of one or more tones. **`Playtones()`** runs in the background; i.e., it will continue to play tones while execution of the dialplan continues. The argument *`tones`* is either a tone name as defined in `indications.conf` or a list of tone frequencies and durations. For an explanation on how to define your own tones, see `indications.conf.`

Use **`StopPlaytones()`** to stop playing tones.

> ![image](images/00819.jpg)

**Asterisk versions:**

![image](images/00820.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00821.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00822.jpg)

**See also [`stopplaytones`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1239641), `indications.conf`, [`busy`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos776235), [`congestion`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos801971), [`progress`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1096214), [`ringing`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1145418).**

### B.120 PrivacyManager()

Requests the input of the caller’s telephone number, if caller ID cannot be obtained.

> PrivacyManager([*maxRetries*[,*minLength*[,*options*]]])

If no caller ID is received, the channel is answered and the caller is asked to enter his own telephone number. If caller ID is present on the line, **`PrivacyManager()`** has no effect.

The caller has *`maxRetries`* (default is 3) number of attempts to provide a valid number of at least *`minLength`* (default is 10) digits in length. The default values are set in `privacy.conf`, which may contain the following entries:

> • **`maxretries`**

> The maximum number of times the caller can attempt to enter a number complying with the length limit set by *`minLength`* (usually 3).

> • **`minlength`**

> The minimum number of digits a number entered must have to be accepted (usually 10).

If you want to prevent **`PrivacyManager()`** from reading from the configuration file every time it is called, you can set values in the command in the dialplan.

If option `j` is set, it jumps to n+101 if the caller fails to provide a valid number within the number of allowed attempts.

The channel variable `PRIVACYMGRSTATUS` is set to `SUCCESS` or `FAILED` and indicates whether the privacy manager was able to get a valid phone number from the caller.

> ![image](images/00823.jpg)

**Asterisk versions:**

![image](images/00824.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00825.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00826.jpg)

**See also [`zapateller`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1292043).**

### B.121 Proceeding()

Indicates call is proceeding.

> Proceeding()

Sends a message to the calling channel indicating that the call is proceeding.

**Asterisk versions:**

![image](images/00827.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00828.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [`progress`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1096214).**

### B.122 Progress()

Indicates call progress.

> Progress()

Provides in-band progress indication, if available, to the caller (... so that she knows that “something is happening”).

Returns 0.

> ![image](images/00829.jpg)

**Asterisk versions:**

![image](images/00830.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00831.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`busy`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos776235), [`congestion`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos801971), [`playtones`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1087914), [`ringing`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1145418), [`proceeding`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1094835).**

### B.123 Queue()

Places a call in the specified queue.

> Queue(*queue[,options[,URL[,announcement[,timeout[,AGI]]]]]*)

Passes an incoming call into the specified queue (predefined in `queues.conf`).

The following options are available and may be combined:

> • **`t`**

> Allow the called party to transfer the call.

> • **`T`**

> Allow the calling party to transfer the call.

> • **`d`**

> Data-quality (modem) call (minimizes delay).

> • **`h`**

> Called party may end the call by pressing *.

> • **`H`**

> Calling party may end the call by pressing *.

> • **`n`**

> No retries on timeout; proceeds to the next priority.

> • **`r`**

> Rings instead of playing music-on-hold.

> • **`i`**

> Ignore call forward requests from queue members; instead do nothing.

> • **`w`**

> Allow the called party to record the conversation via **`Monitor()`**.

> • **`W`**

> Allow the calling party to record the conversation via **`Monitor()`**.

If a call is transferable, it may also be parked and retrieved by another user.

The argument *`announcement`* specifies a wait announcement to be played back to the caller at intervals until a queue member answers the call; the default announcement, if there is one, is defined in `queues.conf`.

The optional `URL` is sent to the caller if the calling channel supports it. This could be used on compatible SIP phones to provide queue information to the phone’s display panel.

The *`timeout`* argument causes the call to fail out of the queue after *`timeout`* number of seconds. The default is 300 seconds (or 5 minutes).

Returns −1 if the originating channel is hung up or if the call is connected to a queue member and ended by one of the parties. If the queue is full, does not exist, or has no member, returns 0; execution continues in the next priority in the dialplan.

> ![image](images/00832.jpg)

**Asterisk versions:**

![image](images/00833.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00834.jpg)

> ![image](images/00835.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00836.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00837.jpg)

> ![image](images/00838.jpg)

> ![image](images/00839.jpg)

> ![image](images/00840.jpg)

**See also [`queuelog`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1105643) and [Chapter 12](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos478254), “[Queues](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos478254).”**

### B.124 QueueLog()

Writes an entry to the queue log.

> QueueLog(*queue*,*uniqueID*,*agent*,*event*[,*additionalinfo*])

Writes an entry to the queue log (usually `/var/log/asterisk/queue_log`). Lets you define custom events. See [Chapter 12](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos478254) for a more complete explanation.

> QueueLog(support,${UNIQUEID},${AGENT},LUNCH,Bon appetit)

**Asterisk versions:**

![image](images/00841.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00842.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00843.jpg)

**See also [`queue`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1098312), [Chapter 12](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos478254).**

### B.125 RaiseException()

Raises an exception.

> RaiseException(*reason*)

**`RaiseException()`** raises an exception; this causes execution to jump to extension `e` in the current context where the exception may be handled by using the **`EXCEPTION()`** function. If no `e` extension has been defined, the channel is hung up.

> ![image](images/00844.jpg)

**Asterisk versions:**

![image](images/00845.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00846.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.126 Random()

Jumps to a priority randomly.

> Random([*probability*]:[[*context*,]*extension*,]*priority*)

Jumps to the specified priority, extension and context based on the *`probability`* provided, which must be a whole number between 1 and 100; in *`probability`* percent of cases, the call will jump to the specified priority.

> ![image](images/00847.jpg)

> ### Warning
> 
> This application is deprecated as of 1.4; use the Asterisk function **`RAND()`** instead.

**Asterisk versions:**

![image](images/00848.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00849.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00850.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.127 Read()

Reads DTMF input from a caller and assigns the result to a variable.

> Read(variable[,*filename*[,*maxDigits*[,*option*[,*attempts*[,*timeout*]]]]])

Reads a DTMF sequence ending in # from the caller and places it in the specified variable.

If *`filename`* is specified (without file extension!), this audio file is played back to the caller before input is read.

The argument *`maxDigits`* defines the maximum number of digits allowed. If provided, the application stops reading when this number of digits has been entered, without the caller having to enter # to end the call. The default setting is 0 and means there is no preset limit and # is expected; the absolute maximum number of digits allowed is 255.

The option `skip` causes the application to end immediately if the channel is inactive. The option `noanswer` enables reading even if the channel is inactive.

The caller has up to *`attempts`* attempts within *`timeout`* seconds to enter a sequence. A *`timeout`* of zero means there is no time limit.

Returns −1 if the channel is hung up, otherwise returns 0.

> ![image](images/00851.jpg)

**Asterisk versions:**

![image](images/00852.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00853.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00854.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00855.jpg)

**See also [`senddtmf`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1163154).**

### B.128 ReadExten()

Read DTMF extension.

> ReadExten(*variable*[,*prompt*_*filename*[,*context*[,*option*[,*timeout*]]]])

Prompts the caller to input an extension, listens for DTMF and stores the entered digits in the specified variable.

**Asterisk versions:**

![image](images/00856.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00857.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [`read`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1112162).**

### B.129 ReadFile()

Reads a file.

> ReadFile(*variable*=*filename*,*length*)

Reads the contents of *`filename`* up to *`length`* characters into the variable *`variable`*.

**Asterisk versions:**

![image](images/00858.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00859.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00860.jpg)

### B.130 RealTime()

Gets configuration information from the realtime configuration database.

> RealTime(*family*,*column*,*value*[,*prefix*])

Retrieves configuration settings from the realtime configuration database into channel variables. All unique column names are set as channel variables. Optionally, the argument *`prefix`* is prepended to the column name to form the variable name. (In the example in the internal help, the prefix `var_` to the column name `test` results in the variable `${var_test}`.`)`.\

Sets the channel variable `REALTIMECOUNT` to the number of values read.

In `extconfig.conf`:

> ![image](images/00861.jpg)

In `extensions.conf`:

> exten => 123,1,RealTime(sipusers,ext,5678,var_)

This executes the following SQL query in the database `asterisk`:

> SELECT * FROM sip_users WHERE ext = 5678

Assuming the table has the columns `firstname` and `lastname`, we can print those values to the CLI this way:

> ![image](images/00862.jpg)

**Asterisk versions:**

![image](images/00863.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00864.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00865.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

**See also [`realtimeupdate`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1122661).**

### B.131 RealTimeUpdate()

Updates a value in the realtime configuration database.

> RealTimeUpdate(*family*,*column*,*value*,*columnUpdate*,*valueUpdate*)

Updates a value in the realtime configuration database. Updates the field *`columnUpdate`* with the value *`valueUpdate`* in the record matching *`family`*, *`column`*, and *`value`*.

> ![image](images/00866.jpg)

**Asterisk versions:**

![image](images/00867.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00868.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00869.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

**See also [`realtime`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1118970).**

### B.132 ReceiveFAX()

Receives a fax.

> ReceiveFAX(*filename*[,*options*])

**`SendFax()`** and **`ReceiveFax()`** replace the well-known fax patch commands **`TxFax()`** and **`RxFax()`** and, like them, they use the SpanDSP library.

**`ReceiveFax()`** receives an incoming fax and stores it as a TIFF file.

> ![image](images/00870.jpg)

**Asterisk versions:**

![image](images/00871.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00872.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [`sendfax`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1165615).**

### B.133 Record()

Records audio from a channel to a file.

As of Asterisk 1.2:

> Record(basename[.*format*[,*maxSilence*[,*maxDuration*[,*options*]]]])

Records audio from the channel and saves it in the file base`name.format`. If the file exists, it is overwritten.

Allowed options are as follows:

> • **`format`**

> Specifies the file format of the recording (`g723`, `g729`, `gsm`, `h263`, `ulaw`, `alaw`, `wav`, ...).

> • **`maxSilence`**

> Defines the maximum duration of silence allowed before the recording is ended.

> • **`maxDuration`**

> Defines the maximum duration of the recording. If not provided or if 0, there is no limit.

> • **`options`**

> One or more of the following option flags may be set:

> • **`s`**

> Does not record if the call has not been answered.

> • **`n`**

> Does not answer but records even if the call has not been answered.

> • **`a`**

> Appends the recording to an existing file instead of overwriting it.

> • **`t`**

> The * DTMF key ends the call instead of the default # key.

> • **`q`**

> Does not play a beep tone before recording.

> • **`x`**

> Records all DTMF tones, including # and *. The call ends when `maxDuration` is reached or the caller hangs up.

If `basename` contains `%d`, it is replaced by a number incremented by 1 for each new recording.

The caller may end recording by pressing the # key; if the caller hangs up before recording is complete, the recording is discarded.

Returns −1 on hangup, otherwise returns 0.

> ![image](images/00873.jpg)

Note the warnings regarding privacy under **`Monitor()`**.

**Asterisk versions:**

![image](images/00874.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00875.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00876.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00877.jpg)

**See also [`dictate`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos862493), [`monitor`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1038634), [`mixmonitor`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1034188).**

### B.134 RemoveQueueMember()

Removes queue members dynamically.

> RemoveQueueMember(*queue*[,*interface*[,*options*]])

Removes a member from the queue dynamically. If *`interface`* is not provided, the application removes the current interface (*i.e.*, the interface that is active in the current priority) from the specified queue.

If the interface is not in the specified queue and priority n+101 exists, the application jumps to this priority; otherwise returns an error.

Returns −1 on error, otherwise returns 0.

> ![image](images/00878.jpg)

**Asterisk versions:**

![image](images/00879.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00880.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00881.jpg)

**See also [`addqueuemember`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos725177), [`queue`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1098312), `queues.conf.`**

### B.135 ResetCDR()

Resets the Call Detail Record.

> ResetCDR([*options*])

Resets the Call Detail Record for the active call. If option `w` is given, the existing CDR is stored before the reset.

Returns 0.

> ![image](images/00882.jpg)

**Asterisk versions:**

![image](images/00883.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00884.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00885.jpg)

**See also [`forkcdr`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos920543), [`nocdr`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1059127).**

### B.136 ResponseTimeout()

Sets the maximum time to wait for a response on a channel.

> ResponseTimeout(*seconds*)

> ### Warning
> 
> **`ResponseTimeout()`** is removed as of Asterisk 1.4 and has been replaced by the **`TIMEOUT()`** function:
> 
> > Set(TIMEOUT(response)=seconds)

**Asterisk versions:**

![image](images/00886.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00887.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [`absolutetimeout`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos723417), [`digittimeout`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos867232), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`timeout`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1437375).**

### B.137 RetryDial()

Attempts to dial and retries if the attempt fails.

> ![image](images/00888.jpg)

Attempts, like **`Dial()`**, to call a device. Plays the file *`announcement`* (without file extension!) if no device can be reached, then waits *`sleep`* seconds before trying again. The default sleep interval is 10 seconds. After *`retries`* retries, the call is handed to the next priority in the dialplan. If *`retries`* is set to 0 or −1, the application retries indefinitely.

A single-digit extension may be dialed by the caller during the sleep interval. If this extension exists in the context defined by `${EXITCONTEXT}` or in the current context, the call is passed to that extension.

All arguments following retries are passed directly to **`Dial()`**.

> ![image](images/00889.jpg)

**Asterisk versions:**

![image](images/00890.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00891.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00892.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00893.jpg)

**See also [`dial`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos835607).**

### B.138 Return()

Returns from a subroutine.

> Return()

Returns from a subroutine called by **`Gosub()`** or **`GosubIf()`** to the priority immediately following the **`Gosub()`** or **`GosubIf()`** that called the subroutine.

> ![image](images/00894.jpg)

**Asterisk versions:**

![image](images/00895.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00896.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00897.jpg)

**See also [`gosub`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos929505), [`gosubif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos931860).**

### B.139 Ringing()

Indicates ringing to the caller.

> Ringing()

Indicates ringing to the caller. What form this indication takes depends on the channel driver. Note that this does not necessarily result in ringing tones; if you absolutely need those, use **`Playtones()`**.

Returns 0.

> ![image](images/00898.jpg)

**Asterisk versions:**

![image](images/00899.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00900.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`busy`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos776235), [`congestion`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos801971), [`progress`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1096214), [`ringing`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1145418), [`playtones`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1087914).**

### B.140 SayAlpha()

Spells out a string to the caller.

> SayAlpha(*string*)

Spells out the specified string to the caller according to the language setting for that channel. The language may be set with the Asterisk function `LANGUAGE()`.

> exten => 123,1,SayAlpha(ABC123)

**Asterisk versions:**

![image](images/00901.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00902.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`saydigits`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1149636), [`saynumber`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1151633), [`sayphonetic`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1157877).**

### B.141 SayDigits()

Says a sequence of digits to the caller.

> SayDigits(*digits*)

Says the provided sequence of digits to the caller according to the language settings for the channel. The language may be set with the Asterisk function `LANGUAGE()`.

> exten => 123,1,SayDigits(1234)

**Asterisk versions:**

![image](images/00903.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00904.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`sayalpha`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1147650), [`saynumber`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1151633), [`sayphonetic`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1157877).**

### B.142 SayNumber()

Says a number.

> SayNumber(*number*[,*gender*])

Says the provided number according to the language settings for the channel. The language may be set with the Asterisk function **`LANGUAGE()`**.

Whole numbers from one to 99,999,999 are supported in the following languages:

> • **`da`**

> Danish

> • **`de`**

> German

> • **`en`**

> English

> • **`es`**

> Spanish

> • **`fr`**

> French

> • **`it`**

> Italian

> • **`nl`**

> Dutch

> • **`no`**

> Norwegian

> • **`pl`**

> Polish

> • **`pt`**

> Portuguese

> • **`se`**

> Swedish

> • **`tw`**

> Mandarin (Taiwanese)

The gender is optional and depends on the language.

For continental languages such as German, French, Spanish and Portuguese, use `f` for feminine, `m` for masculine, and `n` for neuter.

For Scandinavian languages such as Danish, Swedish and Norwegian, use `c` for common (en, enn) and `n` for neuter (et, ett).

To count in German plural, use `p`.

For these other languages to work, their respective sound files must be present `/var/lib/asterisk/sounds/digits` (in subdirectories by language; e.g., `de/`).

> ![image](images/00905.jpg)

**Asterisk versions:**

![image](images/00906.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00907.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`sayalpha`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1147650), [`saydigits`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1149636), [`sayphonetic`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1157877).**

### B.143 SayPhonetic()

Spells a string using the NATO phonetic alphabet.

> SayPhonetic(*string*)

Spells out the provided string using the NATO phonetic alphabet or its linguistic variations. The language may be set with the Asterisk function `LANGUAGE()`. Umlauts and other special characters are not yet supported.

> ![image](images/00908.jpg)

**Asterisk versions:**

![image](images/00909.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00910.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`sayalpha`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1147650), [`saydigits`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1149636), [`saynumber`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1151633).**

### B.144 SayUnixTime()

Announce the time in a custom format.

> SayUnixTime([*unixtime*][,*timezone*[,*format*]])

Announces the current time according to the specified time zone and format. Allowed options are as follows:

> • **`unixtime`**

> The time in UNIX time format; that is, the number of seconds that have passed since the start of the epoch, which began at 0:00 UTC, January 1, 1970\. Accepts negative values. The default value is the current time.

> • **`timezone`**

> The time zone. A list may be found in `/usr/share/zoneinfo`. The default is the system time zone.

> • **`format`**

> The time format of the announcement. A list of allowed formats may be found in `voicemail.conf` from the default installation. The default time format is `ABdY 'digits/at' IMp`.

Returns 0 or −1 if the channel is hung up.

> exten => 123,1,SayUnixTime(,,IMp)

**Asterisk versions:**

![image](images/00911.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00912.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00913.jpg)

### B.145 SendDTMF()

Send DTMF digits on the channel.

> SendDTMF(*digits*[,*timeout*_*ms*])

Sends the specified DTMF sequence on the channel. Permitted symbols are *`0-9`*, *`*`*, *`#`*, and *`A-D`*. Additionally *`w`* is allowed; it indicates a pause of 500ms. The argument *`timeout_ms`* sets the pause in milliseconds between tones. If not specified, defaults to 250ms.

Returns 0, or −1 if the channel is hung up.

> exten => 123,1,SendDTMF(123w456w789,200)

**Asterisk versions:**

![image](images/00914.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00915.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00916.jpg)

**See also [`read`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1112162).**

### B.146 SendFAX()

Sends a fax.

> SendFAX(*filename*[,*options*])

Sends a TIFF file as a fax.

**`SendFax()`** and **`ReceiveFax()`** replace the well-known fax patch commands **`TxFax()`** and **`RxFax()`** and, like them, they use the SpanDSP library.

> ![image](images/00917.jpg)

**Asterisk versions:**

![image](images/00918.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/00919.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [receivefax](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1124998).**

### B.147 SendImage()

Sends an image file to the channel.

> SendImage(*filename*[,*options*])

Sends an image file to the channel. If images are supported and the transmission fails, the application hangs up; otherwise it continues on the next priority. If option `j` is set, the application jumps to priority n+101, if it exists.

Returns 0 on successful transmission of the image or if the channel does not support images, otherwise returns −1\. Sets the channel variable `SENDIMAGESTATUS` to `OK` or `NOSUPPORT`.

> exten => 123,1,SendImage(logo.jpg)

**Asterisk versions:**

![image](images/00920.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00921.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00922.jpg)

**See also [`sendtext`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1169990), [`sendurl`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1172603).**

### B.148 SendText()

Sends text to the channel.

> SendText(*text*[,*option*])

Sends text to the channel (e.g., to print on the display) if the transmission of text is supported by the channel and the device. The channel is handed to the next priority afterwards. If text transmission is not supported, option `j` makes the channel jump to priority n+101 if it exists.

The text is 7-bit ASCII for most channels.

Returns 0 if the text is transmitted without errors, otherwise −1. Sets the channel variable `SENDTEXTSTATUS` to `SUCCESS`, `FAILURE`, or `UNSUPPORTED`.

> exten => 123,1,SendText(Welcome to Asterisk)

**Asterisk versions:**

![image](images/00923.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00924.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00925.jpg)

**See also [`sendimage`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1167528), [`sendurl`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1172603).**

### B.149 SendURL()

Sends a URL to the channel.

> SendURL(*URL*[,*options*])

Sends the channel a URL for the device to call up, and then hands the channel to the next priority.

If the channel does not support URL transmission, option `j` makes the channel jump to priority n+101 if it exists. Option `wait` makes the application wait for confirmation that the URL was loaded before continuing to the next priority.

Returns 0 if the URL is transmitted without errors, otherwise −1. Sets the channel variable `SENDURLSTATUS` to `SUCCESS`, `FAILURE`, `UNSUPPORTED`, or `NOLOAD` (requires option `wait`; the client could not load the URL successfully).

> exten => 123,1,SendURL([http://www.mobileweather.org/index.xml,wait](http://www.mobileweather.org/index.xml,wait))

**Asterisk versions:**

![image](images/00926.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00927.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00928.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00929.jpg)

**See also [`sendimage`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1167528), [`sendtext`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1169990).**

### B.150 Set()

Sets a variable to the specified value.

> Set(*variable*=*value*)

Sets the variable to the specified value. If the variable name starts with _, single inheritance is set (i.e., the variable is inherited by any channels opened from this channel); if it begins with __, unlimited inheritance is set (i.e., all children of this channel, regardless of generation, inherit the variable). Up to 24 variables may be set. Variables are valid only in the channel and are canceled when the channel is hung up. Option `g` sets a global variable (not a function! see note below) in Asterisk 1.2; in 1.4 this is accomplished with the Asterisk function **`GLOBAL()`**.

> ![image](images/00930.jpg)

> ### Note
> 
> Whether global variables are cleared upon **`reload`** depends on the setting of `clearglobalvars` in `extensions.conf`.

**`Set()`** is also used to write to functions (see [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249)).

> ![image](images/00931.jpg)

> ### Note
> 
> The option `g` in Asterisk 1.2 applies *only* to variables; the behavior of a function depends on the function itself.

**Asterisk versions:**

![image](images/00932.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00933.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00934.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00935.jpg)

> ![image](images/00936.jpg)

**See also importvar, `doc/README.variables (1.2)/doc/channelvariables.txt (1.4)`, and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`global`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1367514).**

### B.151 SetAccount()

Sets the account code field in the CDR for billing purposes.

> SetAccount(*account*)

> ### Warning
> 
> **`SetAccount()`** is removed as of Asterisk 1.4 and has been replaced by the **`CDR()`** function:
> 
> > Set(CDR(accountcode)=account)

**Asterisk versions:**

![image](images/00937.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00938.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.152 SetAMAFlags()

Sets AMA-Flags in the Call Detail Record (CDR).

> SetAMAFlags(*flags*)

Sets AMA (Automatic Message Accounting)^([14](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1182296)) flags in the CDR. Overrides any settings found in channel configuration files. Valid settings are `default`, `omit`, `billing`, and `documentation`.

[14](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1181908). In North America, Automatic Message Accounting has been used for billing in Direct Distance Dialing since it was introduced in the mid-twentieth century. The system was originally used to provide the toll system with information about the originating circuit so that the subscriber could be billed for a long-distance call.

Returns 0.

> exten => 123,1,SetAMAFlags(billing)

**Asterisk versions:**

![image](images/00939.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00940.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00941.jpg)

> ![image](images/00942.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### B.153 SetCallerID()

Sets the caller ID.

> SetCallerID(*caller*_*id*[,*options*])

> ### Warning
> 
> **`SetCIDName()`** has been replaced with the **`CALLERID()`** function:
> 
> > Set(CALLERID(all)=Name <number>)

**Asterisk versions:**

![image](images/00943.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00944.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.154 SetCallerPres()

Sets caller ID presentation flags.

> SetCallerPres(*presentation*)

Sets caller ID presentation flags for Q.931 PRI (Primary Rate Interface) connections. Similar to **`CallerPres()`**, but using words instead of a bitmask.

Valid presentations are as follows:

> • **`allowed_not_screened`**

> Presentation allowed, not screened

> • **`allowed_passed_screen`**

> Presentation allowed, passed screen

> • **`allowed_passed_screen`**

> Presentation allowed, failed screen

> • **`allowed`**

> Presentation allowed, network number

> • **`prohib_not_screened`**

> Presentation prohibited, not screened

> • **`prohib_passed_screen`**

> Presentation prohibited, passed screen

> • **`prohib_failed_screen`**

> Presentation prohibited, failed screen

> • **`prohib`**

> Presentation prohibited, network number

> • **`unavailable`**

> Number unavailable

Returns 0.

> ![image](images/00945.jpg)

You may need to set `usecallingpres=yes` in `zapata.conf` for this to work.

**Asterisk versions:**

![image](images/00946.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00947.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### B.155 SetCDRUserField()

Sets the value of the “user” in the CDR.

> SetCDRUserField(*string*)

Sets the value of the “user” in the CDR. This field allows nonstandard information to be recorded in the CDR.

**Asterisk versions:**

![image](images/00948.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00949.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00950.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

> ### Warning
> 
> Although it is not noted in the internal help, this application is deprecated. See the source code:
> 
> > ![image](images/00951.jpg)

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.156 SetCIDName()

Sets the caller-id NAME.

> SetCIDName(n*ame*)

> ### Warning
> 
> **`SetCIDName()`** is no longer available as of Asterisk 1.4 and has been replaced by the **`CALLERID()`** function:
> 
> > Set(CALLERID(name)=Bob)

**Asterisk versions:**

![image](images/00952.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00953.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [`setcidnum`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1194996), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`callerid`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1320096).**

### B.157 SetCIDNum()

Sets the caller ID number.

> SetCIDNum(n*umber*,*options*)

> ### Warning
> 
> **`SetCIDNum()`** is no longer available as of Asterisk 1.4 and was replaced by the **`CALLERID()`** function:
> 
> > ![image](images/00954.jpg)

**Asterisk versions:**

![image](images/00955.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00956.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [`setcidname`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1193038), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`callerid`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1320096).**

### B.158 SetGlobalVar()

Sets the value of a global variable.

> SetGlobalVar(variable=*value*)

Sets the value of a global variable. If the variable does not exist, it is created.

> ### Warning
> 
> **`SetGlobalVar()`** is removed as of Asterisk 1.6 and should not be used in 1.4 either. A global variable is set through the application **`Set()`** (`set`) via the **`GLOBAL()`** function:
> 
> > Set(GLOBAL(variable)=value)
> 
> Use **`Set()`** with the option `g` in Asterisk 1.2 and **`the GLOBAL()`** function for Asterisk 1.4 and up.

**Asterisk versions:**

![image](images/00957.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00958.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00959.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

> ### Warning
> 
> Although it is not noted in the internal help, this application is deprecated. See the source code:
> 
> > ![image](images/00960.jpg)

**See also [`set`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1175585), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`global`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1367514).**

### B.159 SetGroup()

Sets the group for the active channel.

> SetGroup(*group*_*name*)

> ### Warning
> 
> **`SetGroup()`** is removed as of Asterisk 1.4 and has been replaced by the **`GROUP()`** function.

**Asterisk versions:**

![image](images/00961.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00962.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [`checkgroup`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos798545), [`getgroupcount`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos925448), [`getgroupmatchcount`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos927449), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`group`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1369630).**

### B.160 SetLanguage()

Sets the language of the active channel.

> SetLanguage(*language*)

> ### Warning
> 
> **`SetLanguage()`** is removed as of Asterisk 1.4 and has been replaced by the **`CHANNEL()`** function:
> 
> > Set(CHANNEL(language)=de)

**Asterisk versions:**

![image](images/00963.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00964.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.161 SetMusicOnHold()

Sets the default class for Music On Hold (MOH).

> SetMusicOnHold(*class*)

Sets the default class for Music On Hold (MOH).

**Asterisk versions:**

![image](images/00965.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00966.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00967.jpg)

> ### Warning
> 
> Superseded by the Asterisk function `CHANNEL(musicclass)` in 1.4 and above.

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.162 SetRDNIS()

Sets the RDNIS number on the active call.

> SetRDNIS(*number*)

> ### Warning
> 
> **`SetRDNIS()`** is removed as of Asterisk 1.4 and has been replaced by the **`CALLERID()`** function:
> 
> > Set(CALLERID(rdnis)=number)

**Asterisk versions:**

![image](images/00968.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00969.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.163 SetTransferCapability()

Sets the ISDN transfer capability.

> SetTransferCapability(*transferCapability*)

Allowed values:

> • **`SPEECH`**

> 0x00 - Speech (default, voice calls)

> • **`DIGITAL`**

> 0x08 - Unrestricted digital information (data calls)

> • **`RESTRICTED_DIGITAL`**

> 0x09 - Restricted digital information

> • **`3K1AUDIO`**

> 0x10 - 3.1 kHz Audio (fax calls)

> • **`DIGITAL_W_TONES`**

> 0x11 - Unrestricted digital information with tones/announcements

> • **`VIDEO`**

> 0x18 - Video

**Asterisk versions:**

![image](images/00970.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00971.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/00972.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

### B.164 SetVar()

Sets a variable.

> SetVar(*variable*=*value*)

> ### Warning
> 
> **`SetVar()`** is removed as of Asterisk 1.4 and has been replaced by the **`Set()`** function.

**Asterisk versions:**

![image](images/00973.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00974.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [`set`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1175585).**

### B.165 SIPAddHeader()

Adds a SIP header to the SIP dialog.

> SIPAddHeader(*header*: *value*)

Adds a SIP header as specified to SIP calls initiated using **`Dial()`**. Nonstandard SIP headers should be preceded with an `X-` as in `X-Asterisk-Accountcode:`.

Should be used with caution as different SIP devices expect different headers and respond differently to them. May produce unexpected behavior.

Returns 0.

> ![image](images/00975.jpg)

**Asterisk versions:**

![image](images/00976.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00977.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00978.jpg)

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.166 SIPdtmfMode()

Changes the DTMF mode for SIP calls.

> SIPdtmfMode(*mode*)

Changes the DTMF mode for outgoing SIP calls. DTMF can be signaled out-of-band using `rfc2833`, in-band using `inband` (RTP), or out-of-band using `info` (RFC 2976).

> exten => 123,n,SIPdtmfMode(rfc2833)

**Asterisk versions:**

![image](images/00979.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00980.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00981.jpg)

**See also RFC 2833,^([15](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1217304)) RFC 2976.^([16](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1217492))**

[15](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1217134). [www.ietf.org/rfc/rfc2833.txt](http://www.ietf.org/rfc/rfc2833.txt)

[16](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1217184). [www.ietf.org/rfc/rfc2976.txt](http://www.ietf.org/rfc/rfc2976.txt)

### B.167 SIPGetHeader()

Retrieves a SIP header from an incoming call.

> SIPGetHeader(*variable=header_name|options*)

> ### Warning
> 
> **`SIPGetHeader()`** is removed as of Asterisk 1.4 and has been replaced by the **`SIP_HEADER()`** function.

**Asterisk versions:**

![image](images/00982.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00983.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.168 SMS()

Sends or receives SMS (Short Message System) messages.

> SMS(*queue*[,*options*])

Manages the exchange of SMS messages with an SMS-capable telephone or through an SMS service center supporting ETSI^([17](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1220245)) ES 201 912 SMS protocol on analog or ISDN lines. Because the shell client **`smsq`** uses FSK^([18](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1220409)) this is unlikely to work over compressed codecs such as GSM.

[17](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1219890). ETSI (European Telecommunications Standards Institute)

[18](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1220077). Frequency Shift Keying

Options:

> • **`a`**

> Act as recipient

> • **`s`**

> Act as transmitter (SMS service center) to communicate with a telephone set

All send and receive queues are stored in `/var/spool/asterisk/sms/:` message coming from the service center to the device in `sc-me.`*`queue`*`/`, the message from the device to the service center in `me-sc.`*`queue`*`/`. A log is written to `/var/log/asterisk/sms`.

When connecting as a recipient `(a)`, messages residing in `me-sc.`*`queue`*`/` are sent and then deleted; received messages are written to `sc-me.`*`queue`*`/` with a timestamp in the filename. When connecting as a transmitter (SMS service center), the reverse is true.

Message files are in the format described below. Absent parameters imply a default:

> *oa=Originating Address (sender's number)*

This contains the complete national direct-dial number, including country code and preceded by the +. For example, +19255554101 would be a valid number.

> *da=Destination Address (recipient's number)*

Again, a complete national direct-dial number with preceding +.

> *scts=Service Centre Time Stamp (timestamp)*

Uses the format YYYY-MM-DD HH:MM:SS

> ![image](images/00984.jpg)

If characters other than 10, 13, 32-126, 128-255 (decimal) occur in the message, `ud=` is replaced by `ud#` and the message contents are coded in hexadecimal.

> ![image](images/00985.jpg)

When sending to an SMSC, only `da` and `ud` are used; `oa` is ignored. When sending to a device, only `oa` and `ud` are necessary; `da` is ignored.

An extension for receiving SMS messages might look like this (where 4165553331 is the number of our SMSC):

> ![image](images/00986.jpg)

where `handleincomingsms` might be a wrapper or command containing; for example, `smsq--process=queue--queue=me-incoming` which is executed for each incoming message.

Outgoing messages are written to files, but may also be generated with the following (outdated) sequence (4165553331 is the number of the SMSC):

> ![image](images/00987.jpg)

Further information and many additional examples may be found at [www.voip-info.org/wiki/view/Asterisk+cmd+Sms](http://www.voip-info.org/wiki/view/Asterisk+cmd+Sms). With the extremely wide variation in SMS implementation, it is best not to expect **`SMS()`** to work right “out of the box.”

**Asterisk versions:**

![image](images/00988.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00989.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00990.jpg)

### B.169 SoftHangup()

Hangs up the specified channel.

> SoftHangup(*technology*/*resource*[,*options*])

Hangs up the specified channel. Returns 0\. Allowed *`options`* include `a`, which hangs up all channels on the specified device, not just a single resource.

> ![image](images/00991.jpg)

**Asterisk versions:**

![image](images/00992.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00993.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00994.jpg)

**See also `hangup`.**

### B.170 Sort()

Sorts a list of keys and values.

> Sort(*key1*:*value1*[,*key2*:*value2*[,...]])

> ### Warning
> 
> **`Sort()`** is removed as of Asterisk 1.4 and has been replaced by the **`SORT()`** function.

**Asterisk versions:**

![image](images/00995.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/00996.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.171 StackPop()

Removes a return address from the **`Gosub()`** stack.

> StackPop()

Removes a return address from a stack of nested **`Gosub()`** calls.

**Asterisk versions:**

![image](images/00997.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/00998.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/00999.jpg)

**See also [`gosub`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos929505).**

### B.172 StartMusicOnHold()

Starts playing music.

> StartMusicOnHold([*class*])

Plays music from the specified *class* as defined in `musiconhold.conf`. If *class* is not specified, the default class for the channel is used.

**Asterisk versions:**

![image](images/01000.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01001.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01002.jpg)

**See also [`stopmusiconhold`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1237867), [`musiconhold`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1054409).**

### B.173 StopMixMonitor()

Stops recording of a call.

> StopMixMonitor()

Stops recording initiated by `MixMonitor()` of a call on the active channel.

**Asterisk versions:**

![image](images/01003.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01004.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01005.jpg)

**See also [`mixmonitor`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1034188).**

### B.174 StopMonitor()

Stops recording of a channel.

> StopMonitor()

Stops recording of a channel. Has no effect if the channel is not currently monitored.

> ![image](images/01006.jpg)

**Asterisk versions:**

![image](images/01007.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01008.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01009.jpg)

**See also [`monitor`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1038634), [`pausemonitor`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1076675).**

### B.175 StopMusicOnHold()

Stops playing music.

> StopMusicOnHold()

Stops playing music that was started by **`StartMusicOnHold()`**.

**Asterisk versions:**

![image](images/01010.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01011.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01012.jpg)

**See also [`startmusiconhold`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1232369), [`musiconhold`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1054409).**

### B.176 StopPlaytones()

Interrupts playback of a tone list.

> StopPlaytones()

Stops playback of a currently playing tone list.

> ![image](images/01013.jpg)

**Asterisk versions:**

![image](images/01014.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01015.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01016.jpg)

**See also [`playtones`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1087914), `indications.conf.`**

### B.177 System()

Executes a shell command.

> System(*command*)

Uses the C **`system()`** function to execute a command on the system shell (**`sh`** or its equivalents).

This is very similar to **`TrySystem()`** except that it returns −1 if it is unable to run the system command where as **`TrySystem()`** always returns 0.

Sets the channel variable `SYSTEMSTATUS` to `SUCCESS`, `FAILURE`, or `APPERROR`. (This is undocumented; the command was executed but returned an exit code other than zero.)

> ![image](images/01017.jpg)

**See also** [`trysystem`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1250783).

> ### Note
> 
> An alternative is **`Backticks()`** application or the function **`BACKTICKS()`** from the `app_backticks` module.^([19](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1243580))
> 
> [19](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1243473). From [www.pbxfreeware.org/archives/2005/06/index.html](http://www.pbxfreeware.org/archives/2005/06/index.html) or [www.pbxfreeware.org/](http://www.pbxfreeware.org/)
> 
> This returns the output of the command.

**Asterisk versions:**

![image](images/01018.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01019.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01020.jpg)

### B.178 Transfer()

Transfers the call to another extension.

> Transfer([*technology*/]*destination*[,*options*])

Requests transfer of the caller to the specified extension or device. If the technology is specified (e.g., SIP, IAX2), only calls using the same technology will be transferred. In the case of SIP channels that have not yet been answered, this happens via a 302-REDIRECT message to the caller; if the call has already been answered, through a REFER message. The destination may also be a specific address, such as 8885551212@sip.provider.tld.

If option `j` is set, jumps to priority n+101 if the transfer fails.

Sets the channel variable `TRANSFERSTATUS` to `SUCCESS`, `FAILURE`, or `UNSUPPORTED` (meaning the channel driver does not support transfers).

> ![image](images/01021.jpg)

**Asterisk versions:**

![image](images/01022.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01023.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01024.jpg)

### B.179 TryExec()

Tries to execute a dialplan application.

> TryExec(*application*(*arguments*))

Tries, like **`Exec()`**, to execute a dialplan application, but does not terminate the call if the attempt fails (either because the application does not exist or because it returned an error code). Instead, the channel variable `TRYSTATUS` is set to one of the following values:

> • **`SUCCESS`**

> The application returned 0.

> • **`FAILED`**

> The application returned a value other than 0.

> • **`NOAPP`**

> The application could not be found.

For more information, see [`exec`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos892191).

**Asterisk versions:**

![image](images/01025.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01026.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01027.jpg)

**See also [`exec`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos892191), [`execif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos895001), [`trysystem`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1250783).**

### B.180 TrySystem()

Tries to execute a shell command.

> TrySystem(*command*)

Like **`System()`**, it executes a command on the shell (**`sh`** or its equivalents), but always returns 0\. In contrast, **`System()`** returns −1 on error.

Sets the channel variable `SYSTEMSTATUS` to `SUCCESS`, `FAILURE`, or `APPERROR` (command was run but returned an exit code other than 0).

> exten => 123,1,TrySystem(echo 'Hey World' > /tmp/hey.txt)

**Asterisk versions:**

![image](images/01028.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01029.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01030.jpg)

**See also [`system`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1241478).**

### B.181 TXTCIDName()

Looks up the caller name via a DNS TXT record.

> TXTCIDName(*caller_id_number*|*options*)

If the option `j` is set, the call jumps to priority n+101 if the lookup fails.

> ### Warning
> 
> **`TXTCIDName()`** is removed as of Asterisk 1.4 and has been replaced by the **`TXTCIDNAME()`** function.

**Asterisk versions:**

![image](images/01031.jpg)

**Internal help for this application in Asterisk 1.2:**

> ![image](images/01032.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.4

**See also [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249).**

### B.182 UnpauseMonitor()

Resumes recording of a channel.

`UnpauseMonitor()`

Resumes recording of a channel after it has been paused with **`PauseMonitor()`**.

**Asterisk versions:**

![image](images/01033.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01034.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01035.jpg)

**See also [`monitor`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1038634), [`pausemonitor`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1076675).**

### B.183 UnpauseQueueMember()

Resumes calls to a paused member of a queue.

> UnpauseQueueMember([*queue*,]*interface*[,*options*])

“Unpauses” a queue member previously “paused” with **`PauseQueueMember()`** (see an example there) so that the member can receive calls again.

Sets the channel variable `UPQMSTATUS` to `UNPAUSED` or `NOTFOUND`.

**Asterisk versions:**

![image](images/01036.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01037.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01038.jpg)

**See also [`pausequeuemember`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1078636).**

### B.184 UserEvent()

Sends an arbitrary event to the manager interface.

> UserEvent(*eventname*[,*body*])

Sends an event of your choosing to the manager interface. The resulting event packet has the following format:

> ![image](images/01039.jpg)

Additional lines in the form `fieldname:` value may be specified in the body. Multiple lines are separated with the pipe (|) character (in older versions of Asterisk, with , or ^).

Returns 0.

> ![image](images/01040.jpg)

**Asterisk versions:**

![image](images/01041.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01042.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01043.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01044.jpg)

**See also `manager.conf`, Asterisk Manager interface.**

### B.185 Verbose()

Sends arbitrary text to the CLI at the verbose level specified.

> Verbose([*level*,]*message*)

Sends the specified message to the CLI. The *level* is an integer; the message will only appear at verbose levels equal to or greater than this number.^([20](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1262210))

[20](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1262103). e.g., **`asterisk -vvvr`** for verbose level 3 - or enter **`set verbose 3`** in the CLI

If level is not specified, 0 is assumed.

Returns 0.

> ![image](images/01045.jpg)

**Asterisk versions:**

![image](images/01046.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01047.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01048.jpg)

**See also [`noop`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1060854), [`log`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos965179), [`dumpchan`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos877102).**

### B.186 VMAuthenticate()

Authenticates the caller using the voicemail password of the specified mailbox.

> VMAuthenticate([*mailbox*][@*context*][,*options*])

Behaves just like **`Authenticate()`** except that the passwords are taken from the configuration (and optional context) in `voicemail.conf`.

If a mailbox is specified, only the password for that mailbox will be accepted. If it is not provided, any voicemail password will be accepted! The channel variable `${AUTH_MAILBOX}` is then populated with the name of the authenticated mailbox.

Option `s` suppresses the prompt.

> ![image](images/01049.jpg)

**Asterisk versions:**

![image](images/01050.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01051.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01052.jpg)

**See also [`authenticate`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos761094), [`voicemail.conf.`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1266771)**

### B.187 VoiceMail()

Allows the caller to leave a voice mail message in the specified mailbox.

> VoiceMail(*mailbox*[@*context*][&*mailbox*[@*context*][&...]],*options*)

Old syntax:

> VoiceMail([s|u|b]*mailbox*[@*context*][&*mailbox*[@*context*][&...]])

Allows the caller to leave a voice mail message in the specified mailbox. The mailbox must already be configured in `voicemail.conf`. If more than mailbox is listed, the greeting from the first mailbox is the one that is played. If the mailbox does not exist, dialplan execution ends.

The option `s` (silent) suppresses the prompt. The option `u` plays the “unavailable” message, if it exists. The option `b` plays (busy) message, if it exists (file `busy` instead of `unavail`).

> ### Warning
> 
> You cannot mix syntax types. If you do, the application will fail as though the mailbox does not exist. We recommend always using the new syntax.

If option `j` is set, jumps to extension n+101, if it exists, on failure.

If the caller presses `0` during the prompt, the call goes to extension `o` (small letter o, for operator) in the current context.

If the caller presses `*` during the prompt, the call goes to extension `a` (small letter a, for assistant) in the current context.

Returns −1 in case of error (the mailbox could not be found or the caller hung up) otherwise returns 0\. Sets the channel variable `VMSTATUS` to `SUCCESS`, `USEREXIT` (the caller canceled the message) or `FAILED`.

> ![image](images/01053.jpg)

**Asterisk versions:**

![image](images/01054.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01055.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01056.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01057.jpg)

**See also [`voicemailmain`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1271374), `voicemail.conf.`**

### B.188 VoiceMailMain()

Allows the caller to check voice mail messages.

> VoiceMailMain([*mailbox*][@*context*][,*options*])

Old syntax:

> VoiceMailMain([[s|p]*mailbox*][@*context*])

Allows access to the mailbox for listening to messages. If the mailbox number is not specified, the system prompts the caller for the mailbox number.

Option `s` skips the password prompt. Option `p` (prefix) prompts the caller to enter a mailbox number; the number specified in the command is then used as a prefix to the number provided by the caller and the resulting string is used as the mailbox number. This can be useful with virtual mailbox hosting. Option a (*`folder`*) sends the caller directly to the specified folder (default: `INBOX`).

If a context is specified, only mailboxes in the specified context are accessible.

Returns −1 if the caller hangs up, otherwise 0.

> ![image](images/01058.jpg)

**Asterisk versions:**

![image](images/01059.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01060.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01061.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01062.jpg)

**See also [`voicemail`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1266771), `voicemail.conf.`**

### B.189 Wait()

Waits for the specified number of seconds.

> Wait(*seconds*)

Waits the specified number of seconds, then returns 0\. Fractions are allowed (for example, `1.5`).

> ![image](images/01063.jpg)

**Asterisk versions:**

![image](images/01064.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01065.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`waitexten`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1276396).**

### B.190 WaitExten()

Waits for an extension to be dialed.

> WaitExten([*seconds*][,*options*])

Waits the specified number of seconds for the caller to dial a new extension, then returns 0\. Fractions are allowed (for example, `1.5`). If no time is specified, the default extension timeout is used.

Option `m` plays music-on-hold to the caller while waiting for input. The music-on-hold class may be specified in parentheses (e.g., `m (rock)`).

> ![image](images/01066.jpg)

**Asterisk versions:**

![image](images/01067.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01068.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01069.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01070.jpg)

**See also [`wait`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1274620).**

### B.191 WaitForNoise()

Waits for noise on the active channel.

> WaitForNoise(*duration*[,*iterations*[,*timeout*]])

Waits for noise of *`duration`* milliseconds. If *`iterations`* are specified, it will wait for that number of noise events of *`duration`* milliseconds, otherwise waits for one instance. If *`timeout`* is specified, call is hung up after that number of seconds.

> ![image](images/01071.jpg)

**Asterisk versions:**

![image](images/01072.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/01073.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [`waitforsilence`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1282679).**

### B.192 WaitForRing()

Waits the specified number of seconds for a ring signal.

> WaitForRing(*timeout*)

Waits a maximum of *`timeout`* seconds for a ring signal, which is only treated as valid until the second ring has completed.

Returns 0 on success, or −1 if the channel is hung up.

> ![image](images/01074.jpg)

**Asterisk versions:**

![image](images/01075.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01076.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01077.jpg)

### B.193 WaitForSilence()

Waits for silence of a specified duration.

> WaitForSilence(*duration*[,*repeats*[,*timeout*]])

Waits for *`duration`* milliseconds of silence. If *`repeats`* are specified, the application waits until it hears at least that many instances of silence of the specified duration. If *`timeout`* is specified, the call terminates after that many seconds.

> ![image](images/01078.jpg)

**Asterisk versions:**

![image](images/01079.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01080.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01081.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01082.jpg)

### B.194 WaitMusicOnHold()

Play music-on-hold while waiting for the specified number of seconds.

> WaitMusicOnHold(*duration*)

Plays music-on-hold while waiting for the specified number of seconds. If no hold music is available, it waits anyway, but without playing music.

Returns 0 on completion, or −1 if the channel is hung up.

> ![image](images/01083.jpg)

**Asterisk versions:**

![image](images/01084.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01085.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01086.jpg)

**See also [`musiconhold.conf.`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1054409)**

### B.195 WaitUntil()

Waits until the specified time.

> WaitUntil(*unix_time*)

Waits until the specified number of seconds from the start of the epoch (also called “UNIX time”).

Sets the channel variable `WAITUNTILSTATUS` to one of the following values:

> • **`OK`**

> Time elapsed.

> • **`FAILURE`**

> Invalid time specification.

> • **`HANGUP`**

> Time elapsed.

> • **`PAST`**

> Time elapsed.

> ![image](images/01087.jpg)

**Asterisk versions:**

![image](images/01088.jpg)

**Internal help for this application in Asterisk 1.6:**

> ![image](images/01089.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

**See also [waituntil](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos886821).**

### B.196 While()

Starts a while loop.

> While(*expression*)

Starts a while loop. The application returns to this point if **`EndWhile()`** is encountered as long as expression is true; if it is false, execution continues after **`EndWhile()`**.

> ![image](images/01090.jpg)

**Asterisk versions:**

![image](images/01091.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01092.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01093.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01094.jpg)

**See also [`endwhile`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos886821), [`exitwhile`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos900109), [`continuewhile`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos804436), [`gotoif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos936925).**

### B.197 Zapateller()

Generates the “Special Information Tone” to block advance dialing telemarketing systems.

> Zapateller(*options*)

Generates the “Special Information Tone” to indicate the number is not valid or reachable. Some predictive dialing systems will automatically delete a number from the calling list if they receive this tone.

The following pipe-delimited options are accepted:

> • **`answer`**

> Answers the line before playing the tone sequence.

> • **`nocallerid`**

> Plays the tone only if no caller ID information is received.

> ![image](images/01095.jpg)

**Asterisk versions:**

![image](images/01096.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01097.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01098.jpg)

**See also [`privacymanager`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1090691).**

### B.198 ZapBarge()

Allows eavesdropping on a Zap channel.

> ZapBarge([*channel*])

Allows eavesdropping on a Zap channel. Other participants in the call do not hear the eavesdropper and do not receive any indication that the channel is being monitored.

If the channel is not provided, the user is prompted to enter it, following by the # key. In this case, to barge on Zap/4, press 4 and #.

Returns −1, if the caller hangs up, whether or not a channel is being monitored.

> ![image](images/01099.jpg)

**Asterisk versions:**

![image](images/01100.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01101.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6 (dahdibarge):**

> ![image](images/01102.jpg)

**See also [`zapscan`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1299987), [`chanspy`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos789899).**

### B.199 ZapRAS()

Starts the Zaptel ISDN Remote Access Server.

> ZapRAS(*args*)

Starts an ISDN RAS Server using **`pppd`** on the current channel. The channel must be available and a Zap channel. There is no modem emulation.

The point-to-point daemon **`pppd`** must be configured to recognize a Zap interface. The *`args`* are a pipe-delimited list of parameters.^([21](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1298135))

[21](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1298028). The list is long and complex and would not be appropriate in this summary. For more details, see [www.voip-info.org/wiki/view/Asterisk+cmd+ZapRAS](http://www.voip-info.org/wiki/view/Asterisk+cmd+ZapRAS).

Returns −1.

This application is only intended for use with ISDN lines, and your kernel must be patched and configured to support **`ZapRAS()`**, as well as be configured to support PPP.

> ![image](images/01103.jpg)

**Asterisk versions:**

![image](images/01104.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01105.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6 (dahdiras):**

> ![image](images/01106.jpg)

### B.200 ZapScan()

Scans through Zap channels for eavesdropping.

> ZapScan([*group*])

Enables a call center manager to monitor Zap channels quickly and conveniently. Press # to switch to the next channel or * to exit. You may limit the available channels by specifying group.

> exten => 123,1,ZapScan()

**Asterisk versions:**

![image](images/01107.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01108.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6 (dahdiscan):**

> ![image](images/01109.jpg)

**See also [`zapbarge`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1294818), [`chanspy`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos789899), and in [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), see [`group`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1369630).**

### B.201 ZapSendKeypadFacility()

Sends digits out-of-band on an ISDN PRI connection.

> ZapSendKeypadFacility(*digits*)

Sends the supplied digits (`0-9`, `*`, `#`) out-of-band using the Q.931 “keypad facility” information element on a PRI connection.

> exten => 123,1,ZapSendKeypadFacility(*456)

**Asterisk versions:**

![image](images/01110.jpg)

**Internal help for this application in Asterisk 1.4:**

> ![image](images/01111.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6 (dahdisendkeypadfacility):**

> ![image](images/01112.jpg)

**See also [`dahdisendkeypadfacility`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos819636).**

## C. Dialplan Functions

In addition to dialplan applications, which have been part of Asterisk almost from the very beginning, Asterisk supports functions as of Asterisk 1.2\. This is part of a long-standing effort to make Asterisk behave more like a programming environment. In contrast to applications, functions may not be called directly. Instead, they are called inside applications and return a value, or—in a departure from the classical definition of a function—they may even be written to using the application **`Set()`** (see [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)”). Function names are always written in uppercase letters. Surprisingly, functions are written in the same way as variables, inside curly braces and preceded by a $ character (`${}`). This is necessary because strings are not always bounded by quotation marks.

We could be forgiven for criticizing the less-than-intuitive distinction between Asterisk applications, functions, and even variables. Nor is there a consistently applied naming convention: for example, **`SIP_HEADER()`** is broken by an underscore (_) but **`SIPCHANINFO()`** is not. This is a problem with many programming languages and environments; these differences in convention add no useful information but make learning more difficult. In addition to this, the use of the delimiters—comma (,), ampersand (&), and pipe (|)—appears arbitrary. The concept of writing to a function in the same way one might write to a variable goes counter to the basic definition of a function in nearly every other programming language and continues to cause confusion, particularly among new Asterisk users with programming backgrounds.

A better way to imagine a function in Asterisk is as an associative array^([1](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1306681)) (a hash table is a form of associative array). For example:

[1](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1306515). [http://en.wikipedia.org/wiki/Associative_array](http://en.wikipedia.org/wiki/Associative_array)

> ![image](images/01113.jpg)

would look like this in PHP:

> ![image](images/01114.jpg)

Many functions allow the key in our associative array analogy to be empty. For example:

> Set(GROUP()=outgoing);

Despite considerable improvements in Version 1.4, the dialplan programming remains rather inflexible when compared with “real” programming languages. If this proves bothersome, you might consider exploring Asterisk Extension Language (AEL) in more depth. It uses the same functions and applications but has a more robust structure and is often easier to interpret.

To find out which functions are currently available in your installation, enter **`core show functions`** and **`core show function`** *`FUNCTIONNAME`* (or **`show functions`** and **`show function`** *`FUNCTIONNAME`* for Asterisk 1.2) in the CLI.^([2](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1308648))

[2](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1308542). Command-line interface. This may be invoked with **`asterisk –r.`**

Note that these commands are case sensitive. Function names must be written entirely in uppercase letters.

### C.1 AGENT()

AGENT(*agent_number[:field]*)

Returns information about an agent identified by `agentNumber`. The following fields may be queried:

> • **`status`**

> (default) The status of the agent, either `LOGGEDIN` or `LOGGEDOUT`.

> • **`password`**

> The agent’s password.

> • **`name`**

> The agent’s name.

> • **`mohclass`**

> The music-on-hold class.

> • **`exten`**

> The callback extension for the agent. This is used by **`AgentCallbackLogin()`**.

> • **`channel`**

> The name of the agent’s active channel (used by **`AgentLogin()`**).

> ![image](images/01115.jpg)

**Asterisk versions:**

![image](images/01116.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01117.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.2 ARRAY()

ARRAY(*var1*[,*var2*[,...]])

Sets multiple variables simultaneously. (The name is misleading; programmers should note that this does not behave the way an array normally would.) **`ARRAY()`** can only be used for writing, not reading. Remember to separate values with commas *and* to escape the commas with a backslash (`\`), or Asterisk will treat the following characters as an additional parameter for **`Set()`**!

> ![image](images/01118.jpg)

> ### Important
> 
> **`ARRAY()`** is a misleading function that you don’t actually need. Use multiple **`Set()`** statements instead:
> 
> > ![image](images/01119.jpg)

**Asterisk versions:**

![image](images/01120.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01121.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01122.jpg)

### C.3 BASE64_DECODE()

BASE64_DECODE(base64_string)

Decodes a base64-encoded string.

> exten => 123,1,Set(foo=${BASE64_DECODE("SGFsbG8gV2VsdA==")})

**Asterisk versions:**

![image](images/01123.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01124.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.4 BASE64_ENCODE()

BASE64_ENCODE(string)

Encodes a string in base64.

> exten => 123,1,Set(foo=${BASE64_ENCODE("Hey World")})

**Asterisk versions:**

![image](images/01125.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01126.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.5 BLACKLIST

BLACKLIST()

This function checks to see whether the caller ID on the channel is on the blacklist. The Asterisk database (AstDB) is used. The caller ID (NAME) or caller ID (NUMBER) must be stored in the database in the `blacklist` family. The key name is irrelevant.

**`BLACKLIST()`** only tests, it does not perform any operations. If the caller ID is found to match, it returns 1, otherwise it returns 0.

> ![image](images/01127.jpg)

**Asterisk versions:**

![image](images/01128.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01129.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`lookupblacklist`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos967831) in [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029).**

### C.6 CALLERID()

CALLERID(*field*)

Returns or sets information about the caller. The *field* is one of the following:

> • **`name`**

> Name of the caller, as an alphanumeric string. Keeping this string short is recommended (e.g., 15 characters).

> • **`num`**

> Number of the caller, digits only. (Sometimes also found in field `number`, perhaps depending on the Asterisk version.)

> • **`all`**

> Name and number with the number in angle brackets (e.g., `"Robert Cossack <2125558721>"`).

> • **`ani`**

> ANI,^([3](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1321942)) for outgoing calls.

[3](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1321803). Automatic Number Identification

> • **`dnid`**

> DNID^([4](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1322496)) number. Corresponds to the dialed number. (Sometimes also found in field dnis, perhaps depending on the Asterisk version.)

[4](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1322254). Dialed/Destination Number Identification Service

> • **`rdnis`**

> RDNIS^([5](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1323131)) number. The number which was forwarded to the current extension. (This is useful, for example, if the number of the active mailbox does not correspond to that of the dialed extension.)

[5](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1322827). Redirected Dialed Number Identification Service

The old channel variable `${CALLERIDNUM}` is replaced by the function `${CALLERID(num)}` as of Asterisk 1.4 (Similarly, `${RDNIS}` is replaced by `$(CALLERID (rdnis))` etc.). The application **`SetCIDName()`** is replaced by **`Set(CALLERID(name)=`*`Name`*`)`** (Similarly, **`SetCallerID()`** is replaced by **`Set(CALLERID(all)=`*`Name <Number>`*`)`** and so on).

> ![image](images/01130.jpg)

**Asterisk versions:**

![image](images/01131.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01132.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01133.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01134.jpg)

### C.7 CDR()

CDR(*field*)

Reads or sets CDR^([6](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1325928)) fields. The *field* is one of the following (only reading is possible unless otherwise noted):

[6](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1325713). Call Data Record

> • **`clid`**

> Caller ID

> • **`src`**

> The source number (caller ID number)

> • **`dst`**

> The call destination

> • **`dcontext`**

> Destination context

> • **`channel`**

> Channel name

> • **`dstchannel`**

> Destination channel, if applicable

> • **`lastapp`**

> The last executed application

> • **`lastdata`**

> The arguments to the last executed application

> • **`start`**

> Time the call started

> • **`answer`**

> Time the call was answered

> • **`end`**

> Time the call ended

> • **`duration`**

> Duration of the call in seconds

> • **`billsec`**

> Duration of the call since the call was answered (in other words, the billable duration) in seconds

> • **`disposition`**

> Status of the call: `ANSWERED`, `NO ANSWER`, `BUSY`, or `FAILED`

> • **`amaflags`**

> The AMA^([7](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1330908)) flags. Possible flags are `DEFAULT`, `BILLING`, `DOCUMENTATION`, and `OMIT`. (Sometimes `BILLING` and `OMIT` are replaced by `BILL` and `IGNORE`, perhaps depending on the Asterisk version.)

[7](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1330335). Automated Message Accounting

> • **`accountcode`**

> The alphanumeric ID of the billing account, maximum 20 characters. May be set as well as read.

> • **`uniqueid`**

> The unique ID of the channel (maximum 32 characters).

> • **`userfield`**

> A user field for storing arbitrary information (maximum 255 characters). May be set as well as read.

> ![image](images/01135.jpg)

**Asterisk versions:**

![image](images/01136.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01137.jpg)

> ![image](images/01138.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01139.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01140.jpg)

### C.8 CHANNEL()

CHANNEL(*field*)

Reads/sets specific channel parameters. The *field* is one of the following (only reading is possible unless otherwise noted):

> • **`audioreadformat`**

> The format for incoming audio on the channel.

> • **`audionativeformat`**

> The native audio format of the channel.

> • **`audiowriteformat`**

> The format for outgoing audio on the channel.

> • **`callgroup`**

> Extensions in Asterisk can be sorted into call groups numbered from 0 to 63 (e.g., as a client number).^([8](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1335253))

[8](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1335134). This limit of 64 call groups appears to be completely arbitrary and may not be sufficient for all users.

> • **`channeltype`**

> The channel driver, or “technology,” of the current channel (e.g., IAX or SIP).

> • **`language`**

> The language for voice prompts. May be set as well as read.

> • **`musicclass`**

> The music-on-hold class, as defined in `musiconhold.conf`. May be set as well as read.

> • **`state`**

> State of the channel (`Down`, `Rsrvd`, `OffHook`, `Dialing`, `Ring`, `Ringing`, `Up`, `Busy`, `Dialing Offhook`, `Pre-ring`, `Unknown`).

> • **`tonezone`**

> The “tone zone” defines the standard tone indications (dialing, ringing, busy, etc.) for specific regions and countries. This is set in the configuration file for the channel driver (e.g., `zaptel.conf`) with the parameters `loadzone` and `defaultzone`. Possible values are (as defined in `indications.conf`): `at`, `au`, `be`, `br`, `ch`, `cl`, `cn`, `cz`, `de`, `dk`, `ee`, `es`, `fi`, `fr`, `gr`, `hu`, `it`, `lt`, `mx`, `ml`, `no`, `nz`, `pl`, `pt`, `ru`, `se`, `sg`, `uk`, `us`, `us-old`, `tw`, `ve`, `za`.

> • **`videonativeformat`**

> The native video format of the channel.

In addition to the field described above, specific channel drivers can make others available. To learn more about these, look in the documentation for the specific channel driver. Fields that are unavailable on the current channel return an empty string.

> ![image](images/01141.jpg)

**Asterisk versions:**

![image](images/01142.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01143.jpg)

> ![image](images/01144.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01145.jpg)

> ![image](images/01146.jpg)

### C.9 CHECKSIPDOMAIN()

CHECKSIPDOMAIN(domain)

Checks to see whether the specified SIP domain name (may also be an IP address) is local (see [`sip.conf`](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos638188)). Returns the domain name, IP address, or empty string.

> exten => 123,1,Set(foo=${CHECKSIPDOMAIN(123.45.67.89)})

**Asterisk versions:**

![image](images/01147.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01148.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.10 CURL()

CURL(URL [|POST-data])

Loads a web page from the specified *URL* using `GET`. If `POST-data` are provided, these are sent with `POST`. Returns the page as a string.

> ![image](images/01149.jpg)

**Asterisk versions:**

![image](images/01150.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01151.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01152.jpg)

### C.11 CUT()

CUT(*variablename, delimiter, field*)

(As of Asterisk 1.2.8, use a pipe (|) character rather than commas as a parameter delimiter.)

Processes a string in a variable according to a specified delimiter (default: `–`) and returns the requested fields. The *field* may also be a range of fields (e.g., `2-4`) or multiple fields and ranges, separated with & (e.g., `2–4&6`; ranges such as `3-` (everything from field 3 on), or `–3` (everything up to field 3) is possible.

If a comma is used as a delimiter, it must first be escaped with a backslash; e.g., `CUT(var,\,,2)`.

> ![image](images/01153.jpg)

> ### Important
> 
> The parameter `variablename` must be the name of a variable, and not a string. If `foo` is the variable name and `bar` the contents, the following example would be incorrect: `CUT(${bar},,3)`

**See also [`fieldqty`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1364091).**

**Asterisk versions:**

![image](images/01154.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01155.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.12 DB()

DB(*family/key*)

Reads/sets a value in the Asterisk DB (AstDB). When reading, either a value is returned, or an empty string if the key does not exist. The output can be found in the variable `DB_RESULT`.

> ![image](images/01156.jpg)

**Asterisk versions:**

![image](images/01157.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01158.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`db_exists`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1351842), [`db_delete`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1349551), and in [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), see [`dbdeltree`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos826085).**

### C.13 DB_DELETE()

DB_DELETE(*family/key*)

Deletes a value from the AstDB. Upon completion, the variable `DB_RESULT` is set to this value, if it exists.

> ![image](images/01159.jpg)

> ### Note
> 
> For versions prior to Asterisk 1.4, use the application **`DBdel()`**.

**Asterisk versions:**

![image](images/01160.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01161.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`db`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1347618), [`db_exists`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1351842), and in [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), see [`dbdel`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos823608), [`dbdeltree`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos826085).**

### C.14 DB_EXISTS()

DB_EXISTS(*family/key*)

Tests to see whether a key exists in the AstDB. Returns 1 or 0\. Sets the variable `DB_RESULT` to the value of the key, if it exists.

> ![image](images/01162.jpg)

This is one way to replace the application **`LookupBlacklist()`**. This code example causes Asterisk to jump to the context `blacklisted`, extension `s`, priority `1`, if the CID can be found in the blacklist:

> ![image](images/01163.jpg)

**Asterisk versions:**

![image](images/01164.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01165.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`db`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1347618), [`db_delete`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1349551), and in [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), see [`dbdeltree`](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos826085).**

### C.15 DUNDILOOKUP()

DUNDILOOKUP(*number[|DUNDi-context[|options]]*)

Looks up a telephone number with DUNDi. If `DUNDi-context` is specified, `e164` is assumed. The option `b` (bypass) will cause Asterisk to bypass the internal DUNDi cache. Returns the found entry in the form `technology/resource`, if it exists, otherwise returns an empty string.

> ![image](images/01166.jpg)

**Asterisk versions:**

![image](images/01167.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01168.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01169.jpg)

**See also `dundi.conf`.**

### C.16 ENUMLOOKUP()

**Asterisk 1.2:**

> ENUMLOOKUP(number [, service [, optionsANDentrynumber [, zone-suffix]]])

**Asterisk 1.4:**

> ENUMLOOKUP(number [, service [, options, entrynumber [, zone-suffix]]])

Looks up a number with ENUM. The *service* can be `sip` (default), `iax2`, `h323`, `tel`, or `ALL`. The option `c` returns the number of entries. The *entrynumber* (default `1`) selects the entry from the list of results. The *zone-suffix* (default: `e164.arpa`) is the ENUM zone. Comprehensive descriptions and examples may be found in `doc/README.enum` (1.2) / `doc/enum.txt` (1.4).

> ![image](images/01170.jpg)

**Asterisk versions:**

![image](images/01171.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01172.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01173.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01174.jpg)

**See also `enum.conf.`**

### C.17 ENV()

ENV(variable)

Reads/sets an environment variable (a variable in the operating system environment; these can be viewed from the shell with **`echo $variable`**). Environment variables are case sensitive and are almost always written all uppercase.

> ![image](images/01175.jpg)

**Asterisk versions:**

![image](images/01176.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01177.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.18 EVAL()

EVAL(variable)

Evaluates a variable twice. An example is useful: If the variable `${VAR}` contains a string “`${VAR2}`”, that is what is returned when `${VAR}` is called. If **`Eval()`** is used, the nested variable is also evaluated, and the contents of `${VAR2}` are also returned.

> ![image](images/01178.jpg)

**Asterisk versions:**

![image](images/01179.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01180.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.19 EXISTS()

EXISTS(variable)

Checks to see whether a variable is defined. Returns 1 or 0.

> ![image](images/01181.jpg)

**Asterisk versions:**

![image](images/01182.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01183.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.20 FIELDQTY()

FIELDQTY(*variablename, delimiter*)

Returns the number of fields which exist if *variablename* is partitioned using *delimiter.*

> ![image](images/01184.jpg)

**Asterisk versions:**

![image](images/01185.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01186.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01187.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01188.jpg)

**See also [`cut`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1344656).**

### C.21 FILTER()

FILTER(*allowed_characters, string*)

Filters *string* so that only the allowed characters are returned.

> ![image](images/01189.jpg)

**Asterisk versions:**

![image](images/01190.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01191.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01192.jpg)

### C.22 GLOBAL()

GLOBAL(*variablename*)

Used to declare a variable global; i.e., valid beyond the active life of the current channel. Asterisk 1.2 users use **`Set()`** (see [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)) with the option `g`.

> ![image](images/01193.jpg)

> ### Note
> 
> Whether global variables persist through a **`reload`** on the Asterisk console depends whether `clearglobalvars` is set in `extensions.conf`.

**Asterisk versions:**

![image](images/01194.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01195.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.23 GROUP()

GROUP([category])

Reads/sets the group for the channel. (Channels may be grouped as required.)

> ![image](images/01196.jpg)

**Asterisk versions:**

![image](images/01197.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01198.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`group_count`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1371357), [`group_list`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1373176), [`group_match_count`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1374893).**

### C.24 GROUP_COUNT()

GROUP_COUNT(*[group[@category]]*)

Returns the number of channels in the specified group. If no group is specified, the group of the current channel is assumed.

> ![image](images/01199.jpg)

**Asterisk versions:**

![image](images/01200.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01201.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`group`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1369630), [`group_list`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1373176), [`group_match_count`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1374893).**

### C.25 GROUP_LIST()

GROUP_LIST()

Returns a space-separated list of all the groups set for the current channel.

> exten => 123,1,Set(foo=${GROUP_LIST()})

**Asterisk versions:**

![image](images/01202.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01203.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`group`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1369630), [`group_count`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1371357), [`group_match_count`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1374893).**

### C.26 GROUP_MATCH_COUNT()

GROUP_MATCH_COUNT(*pattern [@ category]*)

Returns the number of channels in groups matching the specified pattern.

> ![image](images/01204.jpg)

**Asterisk versions:**

![image](images/01205.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01206.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`group`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1369630), [`group_count`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1371357), [`group_list`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1373176).**

### C.27 IAXPEER()

IAXPEER(*peername[:field]*)

Returns information about an IAX peer. The *peername* can be replaced with `CURRENTCHANNEL` to specify the current channel. The *field* is one of the following:

> • **`ip`**

> (default) The IP address of the peer

> • **`status`**

> Peer status (when `qualify=yes`)

> • **`mailbox`**

> The configured mailbox

> • **`context`**

> The configured context

> • **`expire`**

> The expiry time (in UNIX time) for the connection

> • **`dynamic`**

> Whether the connection is dynamic (`yes|no`).

> • **`callerid_name`**

> The configured CID name

> • **`callerid_num`**

> The configured CID number

> • **`codecs`**

> The accessible codecs

> • **`codec[x]`**

> Preferred codec number `x` (beginning with 0)

> ![image](images/01207.jpg)

**Asterisk versions:**

![image](images/01208.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01209.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01210.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01211.jpg)

**See also [`sippeer`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1419609).**

### C.28 IF()

IF(*expression?trueVal:falseVal*)

Returns a value depending on a condition. If the condition is true, the value following `?` is returned, otherwise the value following `:` is returned.

> ![image](images/01212.jpg)

**Asterisk versions:**

![image](images/01213.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01214.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01215.jpg)

**See also [`iftime`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1383634), and in [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), see [`execif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos895001), [`gotoif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos936925), [`gotoiftime`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos940203).**

### C.29 IFTIME()

IFTIME(*time-condition?trueVal:falseVal*)

Returns a value depending on the time condition.

The *time-condition* follows the format *`time|dayofweek|date|month`*; each parameter may also be a range separated by `-`, or contain the wildcard `*`. Time is given in 24-hour format (e.g., `08:00-18:00`), weekdays and month names are three-letter English language abbreviations (`mon`, `tue`, `wed`, `thu`, `fri`, `sat`, `sun` and `jan`, `feb`, `mar`, `apr`, `may`, `jun`, `jul`, `aug`, `sep`, `oct`, `nov`, `dec`)

> ![image](images/01216.jpg)

**Asterisk versions:**

![image](images/01217.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01218.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01219.jpg)

**See also [`if`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1381519), and in [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), see [`execif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos895001), [`gotoif`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos936925), [`gotoiftime`](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos940203).**

### C.30 ISNULL()

ISNULL(*value*)

Returns 1 if value is null, otherwise returns 0.

> exten => 123,1,Set(foo=${ISNULL(${Var1})})

**Asterisk versions:**

![image](images/01220.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01221.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.31 KEYPADHASH()

KEYPADHASH(*string*)

Transforms an alphabetic string to digits according to the standard telephone keypad letter assignments. This enables quick conversion of vanity numbers to actual numbers; e.g., 1-800-BADHAIR (1-800-2234247).

![image](images/01222.jpg)

**Asterisk versions:**

![image](images/01223.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01224.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.32 LANGUAGE()

LANGUAGE()

Reads/sets the language of the current channel. This setting determines, among other things, which audio files are played. If the language is set to `de` and **`Playback(tt-weasels)`** is run in the dialplan, Asterisk will play `de/tt-weasels`, if it exists, and similarly for **`SayDigits()`** and other applications which rely on prerecorded audio files.

> ![image](images/01225.jpg)

> ### Important
> 
> **`LANGUAGE()`** is removed as of Asterisk 1.6 and was replaced with the **`CHANNEL()`** function:
> 
> > Set(CHANNEL(language)=de)

**Asterisk versions:**

![image](images/01226.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01227.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01228.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

### C.33 LEN()

LEN(*string*)

Returns the length of *string.*

> ![image](images/01229.jpg)

**Asterisk versions:**

![image](images/01230.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01231.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.34 MATH()

MATH(*number1 operator number2 [, typeofresult]*)

Calculates simple mathematical expressions. Allowed operators are `+`, `-`, `/`, `*`, `<`, `>`, `<=`, `> =`, `==`, `%` (modulo). The *typeofresult* may be `f`, `float` (default), `i`, `int` (integer), `h`, `hex` (hexadecimal), `c`, `char` (byte output).

> ![image](images/01232.jpg)

**Asterisk versions:**

![image](images/01233.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01234.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01235.jpg)

### C.35 MD5()

MD5(*string*)

Calculates the MD5 hash (checksum) of a string (returns in hexadecimal format).

> exten => 123,1,Set(foo=${MD5(${string})})

**Asterisk versions:**

![image](images/01236.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01237.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.36 MUSICCLASS()

MUSICCLASS(*class*)

Reads/sets the music-on-hold class.

> ![image](images/01238.jpg)

> ### Important
> 
> Deprecated as of Asterisk 1.4\. Use **`Set(CHANNEL(musicclass)= default)`** instead. See [`channel`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1333504).

**Asterisk versions:**

![image](images/01239.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01240.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01241.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

### C.37 ODBC_SQL()

ODBC_SQL(*SQL-query*)

Executes the specified SQL query and returns the result, if any.

> ![image](images/01242.jpg)

**Asterisk versions:**

![image](images/01243.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01244.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.38 ODBC_USER_DATABASE()

ODBC_USER_DATABASE(*var1[,var2[,...]]*)

Runs the SQL query defined in `func_odbc`.conf and returns the result, if any. The values defined in `func_odbc.conf`, such as `${VAL1}`, `${VAL2}`, `...`, `${ARG1}`, `${ARG2}`, `...` are replaced by the corresponding values provided when the function is called.

> ![image](images/01245.jpg)

### C.39 QUEUEAGENTCOUNT()

In Asterisk 1.2\. Asterisk 1.4 users see **[`QUEUE_MEMBER_COUNT()`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1403716)**.

> QUEUEAGENTCOUNT(*queue*)

Returns the number of agents (as opposed to number of callers) in the specified *queue.*

> ![image](images/01246.jpg)

**Asterisk versions:**

![image](images/01247.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01248.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01249.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

### C.40 QUEUE_MEMBER_COUNT()

In Asterisk 1.4\. Asterisk 1.2 users see **[`QUEUEAGENTCOUNT()`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1401869)**.

> QUEUE_MEMBER_COUNT(*queue*)

Returns the number of agents (and/or members, which may be devices rather than logged-in users) in the specified *queue*.

> ![image](images/01250.jpg)

**Asterisk versions:**

![image](images/01251.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01252.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01253.jpg)

### C.41 QUEUE_MEMBER_LIST()

QUEUE_MEMBER_LIST(*queue*)

Returns a comma-delimited list of the members in the specified *queue.*

> ![image](images/01254.jpg)

**Asterisk versions:**

![image](images/01255.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01256.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.42 QUOTE()

QUOTE (*string*)

Quotes a string exactly, escaping embedded quotation marks if necessary.

> ![image](images/01257.jpg)

**Asterisk versions:**

![image](images/01258.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01259.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.43 RAND()

RAND(*min, max*)

Returns a randomly generated number between `min` and `max` inclusive. The default for `min` is 0, for `max` the default is the largest integer supported by the system (usually 2147483647).

> ![image](images/01260.jpg)

> ### Note
> 
> If you are using versions prior to Asterisk 1.4, use the application **`Random()`**.

**Asterisk versions:**

![image](images/01261.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01262.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01263.jpg)

**See also [`random`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1109659) in [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029).**

### C.44 REGEX()

REGEX(*"expression" string*)

Returns 1, if *string* matches the regular *expression* expression, otherwise returns 0\. The regular expression may include `^` (matches the beginning) and `$` (matches the end). Variables are evaluated first.

The parser in Asterisk 1.2 does not behave consistently and can be confused by expressions containing special characters such as `$` or angle brackets. An ugly workaround is to define a variable (for example `${dollar})` and have it contain the special character (for example, `$`).

> ![image](images/01264.jpg)

**Asterisk versions:**

![image](images/01265.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01266.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01267.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.45 SET()

SET(*variablename = expression*)

Can be used inside nested expressions to set variables to the desired value. (Not to be confused with the application **`Set()`** ! This is the cause of much grief!)

> ![image](images/01268.jpg)

**Asterisk versions:**

![image](images/01269.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01270.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`set`](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1175585) in [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029).**

### C.46 SHA1()

SHA1(*string*)

Calculates the SHA1 hash (checksum) of a string (returns hexadecimal).

> ![image](images/01271.jpg)

**Asterisk versions:**

![image](images/01272.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01273.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.47 SIPCHANINFO()

SIPCHANINFO (*field*)

Returns information about the current SIP channel. The field may be one of the following:

> • **`peerip`**

> The IP address of the peer

> • **`recvip`**

> The source IP address of the peer

> • **`from`**

> The URI from the `From`: header

> • **`uri`**

> The URI from the `Contact`: header

> • **`useragent`**

> The user agent

> • **`peername`**

> The name of the peer

> ![image](images/01274.jpg)

**Asterisk versions:**

![image](images/01275.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01276.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01277.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.48 SIPPEER()

SIPPEER(*peername[,field]*)

Returns information about a SIP peer. The *`field`* may be one of the following:

> • **ip**

> The IP address of the peer (default)

> • **mailbox**

> The configured mailbox

> • **context**

> The configured context

> • **expire**

> The expiry time (in UNIX time) for the connection

> • **dynamic**

> Whether `dynamic` is set (`yes|no`).

> • **callerid_name**

> The configured CID name

> • **callerid_num**

> The configured CID number

> • **codecs**

> Available codecs

> • **status**

> The status (when `qualify=yes` is set)

> • **regexten**

> The registration extension

> • **limit**

> Maximum number of calls

> • **curcalls**

> Number of current calls (only if a limit is set)

> • **language**

> The default language for this peer

> • **useragent**

> The useragent of the peer

> • **codec[x]**

> Preferred codec number `x` (beginning with 0)

> • **accountcode**

> The billing account code in the CDR for conversations with this peer

> ![image](images/01278.jpg)

**Asterisk versions:**

![image](images/01279.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01280.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01281.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01282.jpg)

**See also [`iaxpeer`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1376667).**

### C.49 SIP_HEADER()

SIP_HEADER(*headername[,number]*)

Retrieves the specified SIP header. You are not likely to need this unless you have a thorough understanding of the SIP protocol. Because some headers can appear more than once in a SIP packet (such as `Via,` for example) you can specify which instance of the header you want to see with *number.*

> ![image](images/01283.jpg)

**Asterisk versions:**

![image](images/01284.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01285.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01286.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

**See also [`sipaddheader`](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1212935) in [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029).**

### C.50 SORT()

SORT(*key1:value1[,key2:value2 [,...]]*)

Processes a list of keys and values and returns a comma-separated list of the keys sorted based on their floating-point values.

> ![image](images/01287.jpg)

**Asterisk versions:**

![image](images/01288.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01289.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.51 STAT()

STAT(*flag, filename*)

Returns status information about a file (compare the shell commands **`test`** and **`stat`**). The *`filename`* refers to an inode, so it can be a directory or a specific file. The *`flag`* can be one of the following:

> • **`d`**

> Tests to see whether *filename* is a directory.

> • **`e`**

> Tests if the file exists.

> • **`f`**

> Tests if *filename* is a regular file (as opposed to a special file, such as a block special file, character special file, symbolic link, named pipe, or socket).

> • **`m`**

> Returns the mode of *filename* (octal); i.e. the permissions (e.g., 0754).

> • **`s`**

> Returns the file size in bytes.

> • **`A`**

> Returns the last access time (in UNIX time).

> • **`C`**

> Returns the last inode change time (in UNIX time).

> • **`M`**

> Returns the last modified time (in UNIX time).

> ![image](images/01290.jpg)

**Asterisk versions:**

![image](images/01291.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01292.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.52 STRFTIME()

STRFTIME*([unixtime][,[timezone][, format]]*)

Returns a date and time in the specified format. If *unixtime* is not provided, the current time is used. The default *timezone* is the system default time zone. Possible time zones may be found in `/usr/share/zoneinfo`. The format placeholders are the same as those for the C function **`strftime()`** (see **[`man strftime`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1433424)**), the default is `%c`; i.e., the locale-dependent date-time format.

> ![image](images/01293.jpg)

**Asterisk versions:**

![image](images/01294.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01295.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01296.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01297.jpg)

### C.53 STRPTIME()

STRPTIME(*datetime|timezone|format*)

Converts a formatted date and time string into a UNIX timestamp.

> ![image](images/01298.jpg)

**Asterisk versions:**

![image](images/01299.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01300.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01301.jpg)

**See also [`strftime`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1433424).**

### C.54 TIMEOUT()

TIMEOUT(*type*)

Reads/sets a timeout on the channel. The following types are permitted:

> • **absolute**

> The absolute, maximum duration of a call. Once reached, the call is passed to the extension T, if it exists, or hung up. A value of 0 is the same as no timeout. When this function is called, the existing setting is reset and overwritten. The timeout counter starts when this function is called, not when the call begins.

> • **digit**

> The maximum time allowed between entry of digits. If exceeded, user input is deemed to have finished. If the resulting extension does not exist, the call is passed to the extension i (invalid), if it exists, or hung up. The default is 5 seconds.

> • **response**

> The maximum time to wait for input from a user. If the user does not enter an extension, the call is passed to extension `t` (timeout), if it exists, or the call is hung up. Default: 10 seconds.

> ![image](images/01302.jpg)

**Asterisk versions:**

![image](images/01303.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01304.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01305.jpg)

### C.55 TXTCIDNAME()

TXTCIDNAME(*number[,zone-suffix]*)

Looks up the CID name of the caller in DNS (via a TXT-Record).

> exten => 123,1,Set(callername=${TXTCIDNAME(9755557346)})

The `zone-suffix` option was added in Asterisk 1.6\. If not provided, the default is `e164.arpa`.

**Asterisk versions:**

![image](images/01306.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01307.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01308.jpg)

### C.56 URIDECODE()

URIDECODE(*string*)

Decodes a URI encoded string. See **[`URIENCODE()`](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1443724)**.

> ![image](images/01309.jpg)

**Asterisk versions:**

![image](images/01310.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01311.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01312.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.57 URIENCODE()

URIENCODE(*string*)

URI-encodes a string, so that characters not normally allowed in a URL are replaced with escape sequences following the format `%XX`, where `XX` is the hexadecimal bytecode of the character.

> ![image](images/01313.jpg)

**Asterisk versions:**

![image](images/01314.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01315.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01316.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### C.58 VMCOUNT()

VMCOUNT(*VM-box [@ context][| folder]*)

Returns the number of voicemail messages in the specified mailbox. The default context is `default`, the default folder is `INBOX`.

> ![image](images/01317.jpg)

**Asterisk versions:**

![image](images/01318.jpg)

**Internal help for this function in Asterisk 1.4:**

> ![image](images/01319.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01320.jpg)

**See also [`mailboxexists`](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos984802) in [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029).**

## D. AGI Command Summary

The following commands, which enable an Asterisk Gateway Interface (AGI) script (see [Chapter 16](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos590427), “[Asterisk Gateway Interface](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos590427)”) to interact with Asterisk, are taken from the Asterisk internal help and provided here for your convenience. Additional information is provided for commands that merit it. Most of the command names derive from their application (see [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029)”) or function (see [Appendix C](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249), “[Dialplan Functions](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304249)”) equivalents. Remember that you must enclose empty parameters in double quotation marks (“ ”). The help detail `Runs Dead: Yes|No` indicates whether the command can be used on a dead (i.e., unanswered or hung-up) channel. For more information, see [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029).

### D.1 ANSWER

**Asterisk versions:**

![image](images/01321.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01322.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01323.jpg)

### D.2 ASYNCAGI BREAK

**Asterisk versions:**

![image](images/01324.jpg)

**Internal help for this AGI command in Asterisk 1.6:**

> ![image](images/01325.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### D.3 CHANNEL STATUS

**Asterisk versions:**

![image](images/01326.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01327.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01328.jpg)

### D.4 CONTROL STREAM FILE

**Asterisk versions:**

![image](images/01329.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01330.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01331.jpg)

### D.5 DATABASE DEL

**Asterisk versions:**

![image](images/01332.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01333.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01334.jpg)

### D.6 DATABASE DELTREE

**Asterisk versions:**

![image](images/01335.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01336.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01337.jpg)

### D.7 DATABASE GET

**Asterisk versions:**

![image](images/01338.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01339.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01340.jpg)

### D.8 DATABASE PUT

**Asterisk versions:**

![image](images/01341.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01342.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01343.jpg)

### D.9 EXEC

Executes a dialplan application. The arguments (called options below) are passed to the application. Multiple arguments are separated with a pipe (|) character.

Here is a simple example using **`Dial()`**:

> EXEC Dial Zap/g1/4035551212

**Asterisk versions:**

![image](images/01344.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01345.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01346.jpg)

### D.10 GET DATA

This is comparable to the **`Background()`** application in `extensions.conf`. Plays the audio file with the name *filename* and waits for DTMF input. This may be limited with *`max_digits`*; the maximum wait time is set with *`timeout`*.

**Asterisk versions:**

![image](images/01347.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01348.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

**None**

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01349.jpg)

### D.11 GET FULL VARIABLE

**Asterisk versions:**

![image](images/01350.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01351.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01352.jpg)

### D.12 GET OPTION

**Asterisk versions:**

![image](images/01353.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01354.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01355.jpg)

### D.13 GET VARIABLE

Similar to `GET FULL VARIABLE`, but does not understand complex or system variables.

> ### Tip
> 
> If in doubt, use `GET FULL VARIABLE`.

**Asterisk versions:**

![image](images/01356.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01357.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01358.jpg)

### D.14 GOSUB

**Asterisk versions:**

![image](images/01359.jpg)

**Internal help for this AGI command in Asterisk 1.6:**

> ![image](images/01360.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### D.15 HANGUP

**Asterisk versions:**

![image](images/01361.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01362.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01363.jpg)

### D.16 NOOP

Does nothing, but appended text (`NoOP` [*text*]) will be printed out in the CLI. Always returns 0.

**Asterisk versions:**

![image](images/01364.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01365.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01366.jpg)

### D.17 RECEIVE CHAR

**Asterisk versions:**

![image](images/01367.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01368.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01369.jpg)

### D.18 RECEIVE TEXT

**Asterisk versions:**

![image](images/01370.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01371.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01372.jpg)

### D.19 RECORD FILE

**Asterisk versions:**

![image](images/01373.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01374.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01375.jpg)

### D.20 SAY ALPHA

**Asterisk versions:**

![image](images/01376.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01377.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01378.jpg)

### D.21 SAY DATE

**Asterisk versions:**

![image](images/01379.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01380.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01381.jpg)

### D.22 SAY DATETIME

This command follows this format:

> SAY DATETIME *timestamp [escape_digits] [format] [timezone]*

It speaks the date specified. The timestamp is the number of seconds since January 1, 1970, at 00:00:00\. The format can include the following values:

![image](images/01382.jpg)

The *timezone* is in the same format as that used in /`etc/asterisk/voicemail.conf`.

Output can be interrupted with `escape_digits`. If you omit these parameters, you must use placeholders in the form of double quotes (“ ”).

**Asterisk versions:**

![image](images/01383.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01384.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01385.jpg)

### D.23 SAY DIGITS

**Asterisk versions:**

![image](images/01386.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01387.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01388.jpg)

### D.24 SAY NUMBER

Says a number (e.g., 123 is spoken as one hundred and twenty-three).

**Asterisk versions:**

![image](images/01389.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01390.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01391.jpg)

### D.25 SAY PHONETIC

Says a given string using the NATO phonetic alphabet (e.g., a is said alpha, b as bravo).

**Asterisk versions:**

![image](images/01392.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01393.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01394.jpg)

### D.26 SAY TIME

**Asterisk versions:**

![image](images/01395.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01396.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01397.jpg)

### D.27 SEND IMAGE

**Asterisk versions:**

![image](images/01398.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01399.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01400.jpg)

### D.28 SEND TEXT

**Asterisk versions:**

![image](images/01401.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01402.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01403.jpg)

### D.29 SET AUTOHANGUP

**Asterisk versions:**

![image](images/01404.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01405.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01406.jpg)

### D.30 SET CALLERID

**Asterisk versions:**

![image](images/01407.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01408.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01409.jpg)

### D.31 SET CONTEXT

Sets the context to go to after the AGI script has finished.

> ### Warning
> 
> This does not check to see whether the context exists. If you provide an invalid context, the call will be terminated after the AGI script finishes.

**Asterisk versions:**

![image](images/01410.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01411.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01412.jpg)

### D.32 SET EXTENSION

Sets the extension to go to after the AGI script has finished.

> ### Warning
> 
> This does not check to see whether the extension exists. If you provide an invalid extension, the call will be terminated after the AGI script finishes.

**Asterisk versions:**

![image](images/01413.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01414.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01415.jpg)

### D.33 SET MUSIC

**Asterisk versions:**

![image](images/01416.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01417.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01418.jpg)

### D.34 SET PRIORITY

Sets the priority to go to after the AGI script has finished.

> ### Warning
> 
> This does not check to see whether the priority exists. If you provide an invalid priority, the call will be terminated after the AGI script finishes.

**Asterisk versions:**

![image](images/01419.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

![image](images/01420.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01421.jpg)

### D.35 SET VARIABLE

**Asterisk versions:**

![image](images/01422.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> Usage: SET VARIABLE <variablename> <value>

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01423.jpg)

### D.36 STREAM FILE

> ### Important
> 
> `STREAM FILE` does not always work properly with languages other than English. In this case, you may use `EXEC Playback` *`filename`*.

**Asterisk versions:**

![image](images/01424.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01425.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01426.jpg)

### D.37 TDD MODE

Activates or deactivates the transmission and reception of Telephone Device for the Deaf (TDD) signals on the active channel. So far, only Zap channels support TDD.

**Asterisk versions:**

![image](images/01427.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01428.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01429.jpg)

### D.38 VERBOSE

**Asterisk versions:**

![image](images/01430.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01431.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01432.jpg)

### D.39 WAIT FOR DIGIT

**Asterisk versions:**

![image](images/01433.jpg)

**Internal help for this AGI command in Asterisk 1.4:**

> ![image](images/01434.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01435.jpg)

## E. AMI Command Summary

These command summaries, taken from the Asterisk internal help, are provided here for your convenience. Commands go in the `Action` field when transmitted to the AMI interface.

### E.1 AbsoluteTimeout

**Asterisk versions:**

![image](images/01436.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01437.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01438.jpg)

### E.2 AgentCallbackLogin

**Asterisk versions:**

![image](images/01439.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01440.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

### E.3 AgentLogoff

**Asterisk versions:**

![image](images/01441.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01442.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.4 Agents

**Asterisk versions:**

![image](images/01443.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01444.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.5 AGI

**Asterisk versions:**

![image](images/01445.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01446.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.6 Atxfer

**Asterisk versions:**

![image](images/01447.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01448.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.7 Bridge

**Asterisk versions:**

![image](images/01449.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01450.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.8 Challenge

**Asterisk versions:**

![image](images/01451.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01452.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.9 ChangeMonitor

**Asterisk versions:**

![image](images/01453.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01454.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.10 Command

**Asterisk versions:**

![image](images/01455.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01456.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.11 CoreSettings

**Asterisk versions:**

![image](images/01457.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01458.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.12 CoreShowChannels

**Asterisk versions:**

![image](images/01459.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01460.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.13 CoreStatus

**Asterisk versions:**

![image](images/01461.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01462.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.14 CreateConfig

**Asterisk versions:**

![image](images/01463.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01464.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.15 DAHDIDialOffhook

**Asterisk versions:**

![image](images/01465.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01466.jpg)

**Diff of the internal help from Asterisk 1.2 (zapdialoffhook) to 1.4 (zapdialoffhook):**

None

**Diff of the internal help from Asterisk 1.4 (zapdialoffhook) to 1.6:**

> ![image](images/01467.jpg)

### E.16 DAHDIDNDoff

**Asterisk versions:**

![image](images/01468.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01469.jpg)

**Diff of the internal help from Asterisk 1.2 (zapdndoff) to 1.4 (zapdndoff):**

None

**Diff of the internal help from Asterisk 1.4 (zapdndoff) to 1.6:**

> ![image](images/01470.jpg)

### E.17 DAHDIDNDon

**Asterisk versions:**

![image](images/01471.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01472.jpg)

**Diff of the internal help from Asterisk 1.2 (zapdndon) to 1.4 (zapdndon):**

None

**Diff of the internal help from Asterisk 1.4 (zapdndon) to 1.6:**

> ![image](images/01473.jpg)

### E.18 DAHDIHangup

**Asterisk versions:**

![image](images/01474.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01475.jpg)

**Diff of the internal help from Asterisk 1.2 (zaphangup) to 1.4 (zaphangup):**

None

**Diff of the internal help from Asterisk 1.4 (zaphangup) to 1.6:**

> ![image](images/01476.jpg)

### E.19 DAHDIRestart

**Asterisk versions:**

![image](images/01477.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01478.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 (zaprestart) to 1.6:**

> ![image](images/01479.jpg)

### E.20 DAHDIShowChannels

**Asterisk versions:**

![image](images/01480.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01481.jpg)

**Diff of the internal help from Asterisk 1.2 (zapshowchannels) to 1.4 (zapshowchannels):**

None

**Diff of the internal help from Asterisk 1.4 (zapshowchannels) to 1.6:**

> ![image](images/01482.jpg)

### E.21 DAHDITransfer

**Asterisk versions:**

![image](images/01483.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01484.jpg)

**Diff of the internal help from Asterisk 1.2 (zaptransfer) to 1.4 (zaptransfer):**

None

**Diff of the internal help from Asterisk 1.4 (zaptransfer) to 1.6:**

> ![image](images/01485.jpg)

### E.22 DBDel

**Asterisk versions:**

![image](images/01486.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01487.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.23 DBDelTree

**Asterisk versions:**

![image](images/01488.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01489.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.24 DBGet

**Asterisk versions:**

![image](images/01490.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01491.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01492.jpg)

### E.25 DBPut

**Asterisk versions:**

![image](images/01493.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01494.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.26 Events

**Asterisk versions:**

![image](images/01495.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01496.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.27 ExtensionState

**Asterisk versions:**

![image](images/01497.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01498.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01499.jpg)

### E.28 GetConfig

**Asterisk versions:**

![image](images/01500.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01501.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01502.jpg)

### E.29 GetConfigJSON

**Asterisk versions:**

![image](images/01503.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01504.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.30 Getvar

**Asterisk versions:**

![image](images/01505.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01506.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01507.jpg)

### E.31 Hangup

**Asterisk versions:**

![image](images/01508.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01509.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01510.jpg)

### E.32 IAXnetstats

**Asterisk versions:**

![image](images/01508.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01511.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01512.jpg)

### E.33 IAXpeerlist

**Asterisk versions:**

![image](images/01513.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01514.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.34 IAXpeers

**Asterisk versions:**

![image](images/01515.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01516.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01517.jpg)

### E.35 JabberSend

**Asterisk versions:**

![image](images/01518.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01519.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.36 ListCategories

**Asterisk versions:**

![image](images/01520.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

![image](images/01521.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.37 ListCommands

**Asterisk versions:**

![image](images/01522.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01523.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.38 Login

**Asterisk versions:**

![image](images/01524.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01525.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.39 Logoff

**Asterisk versions:**

![image](images/01526.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01527.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.40 MailboxCount

**Asterisk versions:**

![image](images/01528.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01529.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01530.jpg)

### E.41 MailboxStatus

**Asterisk versions:**

![image](images/01531.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01532.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01533.jpg)

### E.42 MeetmeList

**Asterisk versions:**

![image](images/01534.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01535.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.43 MeetmeMute

**Asterisk versions:**

![image](images/01536.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01537.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.44 MeetmeUnmute

**Asterisk versions:**

![image](images/01538.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01539.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.45 ModuleCheck

**Asterisk versions:**

![image](images/01540.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01541.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.46 ModuleLoad

**Asterisk versions:**

![image](images/01542.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01543.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.47 Monitor

**Asterisk versions:**

![image](images/01544.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01545.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.48 Originate

**Asterisk versions:**

![image](images/01546.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01547.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01548.jpg)

### E.49 Park

**Asterisk versions:**

![image](images/01549.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01550.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.50 ParkedCalls

**Asterisk versions:**

![image](images/01551.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01552.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.51 PauseMonitor

**Asterisk versions:**

![image](images/01553.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01554.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.52 Ping

**Asterisk versions:**

![image](images/01555.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01556.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01557.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.53 PlayDTMF

**Asterisk versions:**

![image](images/01558.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01559.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.54 QueueAdd

**Asterisk versions:**

![image](images/01560.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01561.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.55 QueueLog

**Asterisk versions:**

![image](images/01562.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01563.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.56 QueuePause

**Asterisk versions:**

![image](images/01564.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01565.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.57 QueuePenalty

**Asterisk versions:**

![image](images/01566.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01567.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.58 QueueRemove

**Asterisk versions:**

![image](images/01568.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01569.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.59 QueueRule

**Asterisk versions:**

![image](images/01570.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01571.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.60 Queues

**Asterisk versions:**

![image](images/01572.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01573.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.61 QueueStatus

**Asterisk versions:**

![image](images/01574.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01575.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.62 QueueSummary

**Asterisk versions:**

![image](images/01576.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01577.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.63 Redirect

**Asterisk versions:**

![image](images/01578.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01579.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.64 Reload

**Asterisk versions:**

![image](images/01580.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01581.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.65 SendText

**Asterisk versions:**

![image](images/01582.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01583.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.66 SetCDRUserField

**Asterisk versions:**

![image](images/01584.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01585.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.6

### E.67 Setvar

**Asterisk versions:**

![image](images/01586.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01587.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.68 ShowDialPlan

**Asterisk versions:**

![image](images/01588.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01589.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.69 SIPnotify

**Asterisk versions:**

![image](images/01590.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01591.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.70 SIPpeers

**Asterisk versions:**

![image](images/01592.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01593.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01594.jpg)

### E.71 SIPqualifypeer

**Asterisk versions:**

![image](images/01595.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01596.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.72 SIPshowpeer

**Asterisk versions:**

![image](images/01597.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01598.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

> ![image](images/01599.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01600.jpg)

### E.73 SIPshowregistry

**Asterisk versions:**

![image](images/01601.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01602.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.74 Status

**Asterisk versions:**

![image](images/01603.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

![image](images/01604.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01605.jpg)

### E.75 StopMonitor

**Asterisk versions:**

![image](images/01606.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01607.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.76 UnpauseMonitor

**Asterisk versions:**

![image](images/01608.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01609.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.77 UpdateConfig

**Asterisk versions:**

![image](images/01610.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01611.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01612.jpg)

### E.78 UserEvent

**Asterisk versions:**

![image](images/01613.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01614.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

None

### E.79 VoicemailUsersList

**Asterisk versions:**

![image](images/01615.jpg)

**Internal help for this AMI command in Asterisk 1.6:**

> ![image](images/01616.jpg)

**Diff of the internal help from Asterisk 1.4 to 1.6:**

Not available in Asterisk 1.4

### E.80 WaitEvent

**Asterisk versions:**

![image](images/01617.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01618.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6:**

> ![image](images/01619.jpg)

### E.81 ZapDialOffhook

**Asterisk versions:**

![image](images/01620.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01621.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6 (dahdidialoffhook):**

> ![image](images/01622.jpg)

### E.82 ZapDNDoff

**Asterisk versions:**

![image](images/01623.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01624.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6 (dahdidndoff):**

> ![image](images/01625.jpg)

### E.83 ZapDNDon

**Asterisk versions:**

![image](images/01626.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01627.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6 (dahdidndon):**

> ![image](images/01628.jpg)

### E.84 ZapHangup

**Asterisk versions:**

![image](images/01629.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01630.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6 (dahdihangup):**

> ![image](images/01631.jpg)

### E.85 ZapRestart

**Asterisk versions:**

![image](images/01632.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01633.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

Not available in Asterisk 1.2

**Diff of the internal help from Asterisk 1.4 to 1.6 (dahdirestart):**

> ![image](images/01634.jpg)

### E.86 ZapShowChannels

**Asterisk versions:**

![image](images/01635.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01636.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6 (dahdishowchannels):**

> ![image](images/01637.jpg)

### E.87 ZapTransfer

**Asterisk versions:**

![image](images/01638.jpg)

**Internal help for this AMI command in Asterisk 1.4:**

> ![image](images/01639.jpg)

**Diff of the internal help from Asterisk 1.2 to 1.4:**

None

**Diff of the internal help from Asterisk 1.4 to 1.6 (dahditransfer):**

> ![image](images/01640.jpg)

## F. Configuration Templates

Configuration files such as `sip.conf`, `iax.conf`, and so on can have hundreds of entries; such files are difficult to maintain.

Take a typical `sip.conf`, for example:

> ![image](images/01641.jpg)

There is another way. Asterisk offers the little-known support for templates! Using a template, our `sip.conf` would look like this instead:

> ![image](images/01642.jpg)

This is particularly useful when you have groups or classes of stations with very similar characteristics; that is, in cases where it isn’t possible to put all the common parameters in the `[general]` section. Even in this small and simple example, we’ve managed to save a few lines and centralize future changes to the “class” `my-phones`.

### F.1 Creating Templates

In principle, any section can serve as a template for other entries; using the tag (!) tells the parser that this section is to be used *exclusively* as a template. Note that no spaces are permitted between the square brackets or the parentheses. Templates may also be based on other templates.

> ![image](images/01643.jpg)

### F.2 Using Templates

Use templates by entering the template name (*without* spaces) immediately after the section title. The contents of the template are interpreted first, then the other lines in the section. Sections can inherit multiple templates, as follows:

> ![image](images/01644.jpg)

Parameters in the template may be overwritten with parameters in the section, if necessary.

#### F.2.1 Example

> ![image](images/01645.jpg)

You can find additional examples at [www.voip-info.org/wiki/index.php?page=Asterisk+config+template](http://www.voip-info.org/wiki/index.php?page=Asterisk+config+template).

## G. Upgrading from 1.4 to 1.6

This appendix explains, using the contents of `UPGRADE-1.6.txt` along with some additional examples and commentary, what you need to consider when upgrading from Asterisk 1.4 to 1.6.

### G.1 AEL

> • Macros are now implemented underneath with the **`Gosub()`** application. (Heaven help you if you wrote code depending on any aspect of this!) Prior to 1.6, macros were implemented with the **`Macro()`** app, which provided a nice feature of autoreturning. The compiler will do its best to insert a **`Return()`** app call at the end of your macro if you did not include it, but really, you should make sure that all execution paths within your macros end in `return;` (as in the following example):

> ![image](images/01646.jpg)

> • The `conf2ael` program is introduced in this release; it is in a rather crude state, but deemed useful for making a first pass at converting `extensions.conf` code into Asterisk Extensions Language (AEL). The application will become more intelligent as it is developed.

### G.2 Core

> • The `languageprefix` option in `asterisk.conf` is now deprecated, and the default sound file layout for non-English sounds is the “new style” layout introduced in Asterisk 1.4 (and used by the automatic sound file installer in the Makefile).

> • The `ast_expr2` stuff has been modified to handle floating-point numbers. Numbers of the format D.D are now acceptable input for the expr parser, where D is a string of base-10 digits. All math is now done in “long double,” if it is available on your compiler/architecture. This was halfway between a bug fix (because the MATH func returns fp by default) and an enhancement. Also, for those counting on, or needing, integer operations, a series of functions were also added to the expr language, to allow several styles of rounding/truncation, along with a set of common floating-point operations, like sin, cos, tan, log, pow, and so on. The ability to call external functions such as `CDR()` and so forth was also added, without having to use the `${...}` notation.

> • The delimiter passed to applications has been changed to the comma (,), because that is what people are used to using within `extensions.conf`. If you are using real-time extensions, you will need to translate your existing dialplan to use this separator. To use a literal comma, you need merely to escape it with a backslash (\). Another possible side effect is that you may need to remove the obscene level of backslashing that was necessary for the dialplan to work correctly in 1.4 and earlier versions. This should make writing dialplans less painful in the future, albeit with the pain of a one-time conversion. If you would like to avoid this conversion immediately, set `pbx_realtime=1.4` in the `[compat]` section of `asterisk.conf`. After transitioning, `set pbx_realtime=1.6` in the same section.

> • For the same reason as above, you may set `res_agi=1.4` in the `[compat]` section of `asterisk.conf` to continue to use the `|` delimiter in the `EXEC` arguments of Asterisk Gateway Interface (AGI) applications. After converting to use the `,` delimiter, change this option to `res_agi=1.6`.

> • As a side-effect of the application delimiter change, many places that used to need quotes in order to get the proper meaning are no longer required. You now only need to quote strings in configuration files if you literally want quotation marks within a string.

> • The `logger.conf` option `rotatetimestamp` has been deprecated in favor of `rotatestrategy`. This new option supports a rotate strategy that more closely mimics the system logger in terms of file rotation.

> • The concise versions of various CLI commands are now deprecated. We recommend using the manager interface (AMI) for application integration with Asterisk instead of using **`asterisk -rx "`*`command`*`"`**.

### G.3 Voicemail

> • The voicemail configuration values `maxmessage` and `minmessage` have been changed to `maxsecs` and `minsecs` to clarify their purpose and to make them more distinguishable from `maxmsgs`, which sets folder size. The old variables will continue to work in this version, albeit with a deprecation warning.

> • If you use any interface for modifying voicemail aside from the built-in dialplan applications, the option `pollmailboxes` must be set in the `general` section of `voicemail.conf` for message waiting indication (MWI) to work properly; the polling frequency is set with `pollfreq`. This is because voicemail notification is now event based rather than polling based. The channel drivers are no longer responsible for constantly manually checking mailboxes for changes so that they can send MWI information to users. Examples of situations that would require this option are web interfaces to voicemail or an e-mail client in the case of using Internet Message Access Protocol (IMAP) storage.

### G.4 Dialplan Applications and Functions

> • **`ChanIsAvail()`** now has a `t` option, which allows the specified device to be queried for state without consulting the channel drivers. This performs mostly a `ChanExists` sort of function.

> • **`ChannelRedirect()`** will not terminate the channel that fails to do a channelredirect as it has done previously. Instead, `CHANNELREDIRECT_STATUS` will reflect if the attempt was successful.

> • **`SetCallerPres()`** has been replaced with the **`CALLERPRES()`** dialplan function and is now deprecated.

> • **`DISA()`**’s fifth argument is now an options argument. If you have previously used `NOANSWER` in this argument, you’ll need to convert that to the new option `n`.

> • **`Macro()`** is now deprecated. If you need subroutines, you should use the **`Gosub()`**/**`Return()`** applications. To replace **`MacroExclusive()`**, we have introduced dialplan functions **`LOCK()`**, **`TRYLOCK()`**, and **`UNLOCK()`**. You may use these functions in any location where you desire to ensure that only one channel is executing that path at any one time. The **`Macro()`** applications are deprecated for performance reasons. However, because **`Macro()`** has been around for a long time and so many dialplans depend heavily on it, for the sake of backward compatibility it will not be removed. It is also worth noting that using both **`Macro()`** and **`GoSub()`** at the same time is *heavily* discouraged.

> • **`Read()`** now sets a `READSTATUS` variable on exit. It does *not* automatically return `-1` (and hang up) anymore on error. If you want to hang up on error, you need to do so explicitly in your dialplan.

> • **`Privacy()`** no longer uses `privacy.conf`, so any options must be specified directly in the application arguments.

> • **`MusicOnHold()`** application now has duration parameter which allows specifying timeout in seconds.

> • **`WaitMusicOnHold()`** application is now deprecated in favor of extended MusicOnHold.

> • **`SetMusicOnHold()`** is now deprecated. You should use `Set(CHANNEL (musicclass)=...)` instead.

> • The arguments in **`ExecIf()`** changed a bit, to be more like other applications. The old syntax is

> ExecIf(expression,application,arguments)

> The new syntax is

> ![image](images/01647.jpg)

> • The behavior of the **`Set()`** application now depends on a compatibility option, set in `asterisk.conf`. To use the old 1.4 behavior, which allowed **`Set()`** to take multiple key/value pairs, set `app_set=1.4` in `[compat]` in `asterisk.conf`. To use the new behavior, which permits variables to be set with embedded commas, set `app_set=1.6` in `[compat]` in `asterisk.conf`. Note that you can have both behaviors at the same time, if you switch to using `MSet()` if you want the old behavior.

> • The function **`QUEUE_MEMBER_COUNT()`** has been deprecated in favor of the **`QUEUE_MEMBER()`** function. For more information, issue a **`show function QUEUE_MEMBER`** from the CLI.

### G.5 CDR

> • The `cdr_sqlite` module has been marked as deprecated in favor of `cdr_sqlite3_custom`. It will potentially be removed from the tree after Asterisk 1.6 is released.

> • The `cdr_odbc` module now uses `res_odbc` to manage its connections. The username and password parameters in `cdr_odbc.conf`, therefore, are no longer used. The `dsn` parameter now points to an entry in `res_odbc.conf`.

> • The `uniqueid` field in the core Asterisk structure has been changed from a maximum 31-character field to a 149-character field, to account for all possible values the `systemname` prefix could be. In the past, if the `systemname` was too long, the `uniqueid` would have been truncated.

> • The `cdr_tds` module now supports all versions of FreeTDS that contain the `db-lib` front end. It will also now log the `userfield` variable if the target database table contains a column for it.

### G.6 Audio Formats

> • `format_wav`: The GAIN preprocessor definition and source code that used it is removed. This change was made in response to user complaints of choppiness or the clipping of loud signal peaks. To increase the volume of voicemail messages, use the `volgain` option in `voicemail.conf`.

> • Previously, the Asterisk source code distribution included the iLBC encoder/decoder source code, from Global IP Solutions ([http://www.gipscorp.com](http://www.gipscorp.com)). This code is not licensed for distribution, and therefore has been removed from the Asterisk source code distribution. If you want to use `codec_ilbc` to support iLBC channels in Asterisk, you can run the `contrib/scripts/get_ilbc_source.sh` script to download the source and put it in the proper place in the Asterisk build tree. Once that is done, you can follow your normal steps of building Asterisk. You will need to run `menuselect` and enable the iLBC codec in the Codec Translators category, then `make` and `make install`.

### G.7 Channel Drivers

> • **SIP:** A small upgrade to support the Record button on the SNOM360, which sends a sip INFO message with a Record: on or Record: off header. If Asterisk is set up (through the `automon` parameter in `features.conf`) to accept One Touch Monitor requests (by default, via *1), the user-configured dialpad sequence is generated, and recording can be started and stopped via this button. The filenames and formats are all controlled via the normal mechanisms. If the user has not configured the automon feature, the normal `415 Unsupported media type` is returned, and nothing is done.

> • The `call-limit` option in `sip.conf` is marked as deprecated. It still works in this version of Asterisk, but will be removed in the following version. Please use the **`GROUP()`**, **`GROUP_COUNT()`**, and **`GROUP_MATCH_COUNT()`** functions in the dialplan to enforce call limits. The `limitonpeer` configuration option is now renamed to `counteronpeer`.

> • The `username` option is now renamed to `defaultuser` to match `defaultip`. These are used only before registration to call a peer with the URI `sip:defaultuser@defaultip`. The `username` setting still works, but is deprecated and will not work in the next version of Asterisk.

> • **`chan_local.c`:** The comma delimiter inside the channel name has been changed to a semicolon, to make the Local channel driver compatible with the comma-delimiter change in applications.

> • **H323:** The `tos` setting has changed name to `tos_audio` and `cos` to `cos_audio` to be compatible with settings in `sip.conf`. The `tos` and `cos` configuration is deprecated and will stop working in the next release of Asterisk.

> • **Console:** A new console channel driver, `chan_console`, has been added to Asterisk. This new module can not be loaded at the same time as `chan_alsa` or `chan_oss`. The default `modules.conf` loads only one of them (`chan_oss` by default). So, unless you have modified your `modules.conf` to not use the autoload option, you will need to modify `modules.conf` to add another `noload` line to ensure that only one of these three modules gets loaded.

> • **DAHDI:** The `chan_zap` module that supported public switched telephone network (PSTN) interfaces using Zaptel has been renamed to `chan_dahdi`, and only supports the DAHDI telephony driver package for PSTN interfaces. See the `Zaptel-to-DAHDI.txt` file for more details on this transition.

> • The `msdstrip` option has been deprecated because it provides no value over the method of stripping digits in the dialplan using variable substring syntax.

### G.8 Configuration

> • **`dundi.conf:`** The `tos` parameter changed to use new values. Old values like `lowdelay`, `lowcost`, and `other` are not acceptable now. Look into `doc/tex/qos.tex` for more information about this parameter.

> • **`queues.conf`:** The `queue-lessthan` sound file option is no longer available, and the `queue-round-seconds` option no longer takes `1` as a valid parameter.

### G.9 Asterisk Manager Interface

> • Manager has been upgraded to version 1.1 with a lot of changes. Check `doc/manager_1_1.txt` for information.

> • The **`IAXpeers`** command output has been changed to more closely resemble the output of the **`SIPpeers`** command.

> • The `cdr_manager` module now reports at the `cdr` level, not at `call` as it was before. You may need to change your `manager.conf` to add the level to existing AMI users, if they want to see the CDR events generated.

> • The **`Originate`** command now requires `write` permission. For **`Originate`** with the `Application` parameter, you need the additional `system` privilege if you want to do anything that calls out to a subshell.

## H. From Zaptel to DAHDI

Digium has used the name Zaptel for its pubic switched telephone network (PSTN) drivers for some time. In 2006, the trademark owner notified Digium that the name was, in fact, trademarked. In response, Digium has renamed the driver package to DAHDI as of 2008\. Kevin Fleming, Digium’s director of software development, explained this in the following blog posted in May 2008.

> ![image](images/01648.jpg)

> ![image](images/01649.jpg)

### H.1 DAHDI

#### H.1.1 Dial()

Anybody using DAHDI, be it in Asterisk 1.6 or Asterisk 1.4.22 and above, should note that any references to **`Dial(Zap/...)`** in the dialplan must be changed to **`Dial(DAHDI/...)`**.

This behavior can be configured for the sake of backward compatibility of dialplans. To use the old terms, set the following in the `[options]` section of `/etc/asterisk/asterisk.conf:`

> dahdichanname = no

#### H.1.2 Kernel Modules (.ko)

All the former Zaptel kernel modules are also getting new names, as shown in [Table H.1](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1617587).

**Table H.1** Kernel Module Renaming

![image](images/01650.jpg)

The names for the kernel modules for individual interface cards have not changed.

#### H.1.3 Files

The configuration files and directories have changed accordingly, as shown in [Table H.2](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1618274).

**Table H.2** Configuration File Renaming

![image](images/01651.jpg)

> ### Warning
> 
> Setting `dahdichanname = no` as described previously will make Asterisk read the configuration from `zapata.conf` rather than `chan_dahdi.conf`.

#### H.1.4 Shell Programs

The new shell programs and scripts have these corresponding names, as shown in [Table H.3](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1619296).

**Table H.3** Shell Programs

![image](images/01652.jpg)

#### H.1.5 Asterisk Modules

Similarly, the corresponding Asterisk modules, which provide the **`Zap...()`** applications, have new names, as shown in [Table H.4](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1619945).

**Table H.4** Asterisk Modules

![image](images/01653.jpg)

For dialplan backward compatibility, the commands **`Zap...()`** and the new **`DAHDI...()`** are interchangeable. You can find more information about the applications in [Appendix B](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029), “[Dialplan Applications](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692029).”

### H.2 Interview with Kevin P. Fleming

In January 2009, Stefan Wintermeyer interviewed Kevin P. Fleming, Digium’s director of software development, on the transition from Zaptel to DAHDI and the evolution of ISDN support in Asterisk:

> **Q:** *Does DAHDI still need mISDN for the B410P card or does it come with support for Euro-ISDN BRI by itself now?*

> **A:** You are confusing two different things; DAHDI is the same layer as Zaptel was. It provides hardware drivers and a limited amount of signaling abstraction (along with some other features), but is not at all involved in protocol-level work. `chan_dahdi` is the channel driver (which used to be called `chan_zap`), which contains protocol level support, including analog signaling, CAS, PRI, and SS7 (in Asterisk 1.6).

> Zaptel and mISDN were not at all related, and the same is true of DAHDI and mISDN. The only reference to mISDN in Zaptel was a Makefile target called `b410p`, which allowed people to download, build, and install the mISDN and mISDNuser packages in an automated fashion, but this was just a convenience for users, it was not related to Zaptel. In DAHDI, this is no longer present, and mISDN users must follow normal processes to obtain and install mISDN.

> Now, when it gets to the channel driver layer, things get a little more complicated. Asterisk 1.4 had `chan_zap`, which talks to Zaptel, and `chan_misdn`, which talks to mISDN. They don’t support any hardware in common, so for Asterisk 1.4 users, support of EuroISDN BRI is still handled by `chan_misdn`. This is still true even in recent Asterisk 1.4 releases where `chan_zap` has been renamed to `chan_dahdi`, and now talks to DAHDI instead of Zaptel. Even though DAHDI now contains a driver for Digium’s B410P BRI card, the Asterisk 1.4 `chan_dahdi` channel driver does not support EuroISDN BRI.

> In Asterisk 1.6 the picture is a little different: The `chan_misdn` channel driver is still present, and users who prefer mISDN or have hardware only supported by mISDN are still welcome to use it. The Asterisk 1.6 `chan_dahdi` channel driver works only with DAHDI, *and* it contains protocol-level support for EuroISDN BRI. This means that Asterisk 1.6 users can use `chan_dahdi` for their EuroISDN BRI connections, over any BRI card with a DAHDI driver (see below for more details).

> **Q:** *Would you call it stable and ready for production?*

> **A:** There are two answers to that question: The EuroISDN BRI protocol support in `chan_dahdi` (which actually comes from `libpri`) is both stable and ready for production. It has been through extensive telecom certification testing and will be supported for BRI interoperability just as it has always been for PRI interoperability.

> The DAHDI driver for the Digium B410P is very new, and is working quite well for a large number of users. However, some open issues are being worked on (visible in our open source issue tracker on [bugs.digium.com](http://bugs.digium.com)), primarily related to ISDN L1 layer behavior with various telco operators in Europe. It is certainly stable and fully supported by Digium’s development team, but there are probably environments where it is not yet ready for production until these issues are resolved.

> **Q:** *Will Euro-ISDN BRI support be available in 1.4 and Zaptel, too, or only in 1.6 and DAHDI?*

> **A:** The B410P driver will never be part of Zaptel (as there will be no more Zaptel releases anyway), and the EuroISDN BRI support in `chan_dahdi` will not be added to Asterisk 1.4, as we don’t add new features to that release branch. However, the `chan_dahdi` changes required to provide EuroISDN BRI support are relatively minor, so I expect that one or more community members will publish “backport” patches so that users can use the DAHDI B410P driver and the libpri EuroISDN BRI support in Asterisk 1.4.

> **Q:** *Will DAHDI and Zaptel support generic Cologne HFC-S BRI cards or is it B410P specific?*

> **A:** The DAHDI driver for the B410P card was written specifically for that card, but because the card is based on an HFC-4S, of course the driver could be modified to support cards from other manufacturers. We would be happy to accept patches through our normal patch submission process (on [bugs.digium.com](http://bugs.digium.com)) that add support for generic or manufacturer-specific versions of the HFC-S cards, if community members wish to provide them.

> **Q:** *Why do I need the libpri PRI stack for a BRI card (as it has been announced on asterisk-users)?*

> **A:** Because ISDN PRI (both ANSI and Euro) and EuroISDN BRI are very nearly the same protocol; in essence, `libpri` has the wrong name, and it should instead be something like `libisdn`, signifying that it is really an ISDN protocol stack (Q.921 and Q.931, among others), not specific to a particular interface type.

> **Q:** *Does the BRI support in DAHDI include both PtP (point to point) / PtmP (point to multipoint) and TE/NT mode? If the limitation is not in DAHDI, does libpri support all of these modes?*

> **A:** The B410P driver in DAHDI supports TE and NT mode on the HFC4-S chip, but at that level there is no difference (the hardware layer) between PtP and PtMP. `libpri` currently supports being a TE over either PtP or PtMP links, or being an NT over PtP links. It does not currently support acting as an NT over PtMP links, but of course patches are welcome.

> **Q:** *Will Asterisk continue to support* `chan_misdn`*?*

> **A:** Yes, we will continue to support it (as will the community members who help support it now), but our primary ISDN-related development efforts will continue to be on `libpri`/`chan_dahdi`.

## I. IAX vs. SIP

One question you need to answer, especially when it comes to the question of connecting two Asterisk servers through a trunk, is whether to use IAX or SIP. Opinion is divided over which is the better option, but IAX was written to overcome some of the limitations of SIP. For your convenience, we include an e-mail to the Asterisk users list from Mark Spencer, in which he describes the advantages of IAX:

> ![image](images/01654.jpg)

> ![image](images/01655.jpg)

In defense of SIP, Mark later wrote:

> ![image](images/01656.jpg)

## J. GNU Free Documentation License

Version 1.3, 3 November 2008

Copyright © 2000, 2001, 2002, 2007, 2008 Free Software Foundation, Inc. <http://fsf.org/>

Everyone is permitted to copy and distribute verbatim copies of this license document, but changing it is not allowed.

### 0 PREAMBLE

The purpose of this License is to make a manual, textbook, or other functional and useful document “free” in the sense of freedom: to assure everyone the effective freedom to copy and redistribute it, with or without modifying it, either commercially or noncommercially. Secondarily, this License preserves for the author and publisher a way to get credit for their work, while not being considered responsible for modifications made by others.

This License is a kind of “copyleft”, which means that derivative works of the document must themselves be free in the same sense. It complements the GNU General Public License, which is a copyleft license designed for free software.

We have designed this License in order to use it for manuals for free software, because free software needs free documentation: a free program should come with manuals providing the same freedoms that the software does. But this License is not limited to software manuals; it can be used for any textual work, regardless of subject matter or whether it is published as a printed book. We recommend this License principally for works whose purpose is instruction or reference.

### 1 APPLICABILITY AND DEFINITIONS

This License applies to any manual or other work, in any medium, that contains a notice placed by the copyright holder saying it can be distributed under the terms of this License. Such a notice grants a world-wide, royalty-free license, unlimited in duration, to use that work under the conditions stated herein. The “Document”, below, refers to any such manual or work. Any member of the public is a licensee, and is addressed as “you”. You accept the license if you copy, modify or distribute the work in a way requiring permission under copyright law.

A “Modified Version” of the Document means any work containing the Document or a portion of it, either copied verbatim, or with modifications and/or translated into another language.

A “Secondary Section” is a named appendix or a front-matter section of the Document that deals exclusively with the relationship of the publishers or authors of the Document to the Document’s overall subject (or to related matters) and contains nothing that could fall directly within that overall subject. (Thus, if the Document is in part a textbook of mathematics, a Secondary Section may not explain any mathematics.) The relationship could be a matter of historical connection with the subject or with related matters, or of legal, commercial, philosophical, ethical or political position regarding them.

The “Invariant Sections” are certain Secondary Sections whose titles are designated, as being those of Invariant Sections, in the notice that says that the Document is released under this License. If a section does not fit the above definition of Secondary then it is not allowed to be designated as Invariant. The Document may contain zero Invariant Sections. If the Document does not identify any Invariant Sections then there are none.

The “Cover Texts” are certain short passages of text that are listed, as Front-Cover Texts or Back-Cover Texts, in the notice that says that the Document is released under this License. A Front-Cover Text may be at most 5 words, and a Back-Cover Text may be at most 25 words.

A “Transparent” copy of the Document means a machine-readable copy, represented in a format whose specification is available to the general public, that is suitable for revising the document straightforwardly with generic text editors or (for images composed of pixels) generic paint programs or (for drawings) some widely available drawing editor, and that is suitable for input to text formatters or for automatic translation to a variety of formats suitable for input to text formatters. A copy made in an otherwise Transparent file format whose markup, or absence of markup, has been arranged to thwart or discourage subsequent modification by readers is not Transparent. An image format is not Transparent if used for any substantial amount of text. A copy that is not “Transparent” is called “Opaque”.

Examples of suitable formats for Transparent copies include plain ASCII without markup, Texinfo input format, LaTeX input format, SGML or XML using a publicly available DTD, and standard-conforming simple HTML, PostScript or PDF designed for human modification. Examples of transparent image formats include PNG, XCF and JPG. Opaque formats include proprietary formats that can be read and edited only by proprietary word processors, SGML or XML for which the DTD and/or processing tools are not generally available, and the machine-generated HTML, PostScript or PDF produced by some word processors for output purposes only.

The “Title Page” means, for a printed book, the title page itself, plus such following pages as are needed to hold, legibly, the material this License requires to appear in the title page. For works in formats which do not have any title page as such, “Title Page” means the text near the most prominent appearance of the work’s title, preceding the beginning of the body of the text.

The “publisher” means any person or entity that distributes copies of the Document to the public.

A section “Entitled XYZ” means a named subunit of the Document whose title either is precisely XYZ or contains XYZ in parentheses following text that translates XYZ in another language. (Here XYZ stands for a specific section name mentioned below, such as “Acknowledgements”, “Dedications”, “Endorsements”, or “History”.) To “Preserve the Title” of such a section when you modify the Document means that it remains a section “Entitled XYZ” according to this definition.

The Document may include Warranty Disclaimers next to the notice which states that this License applies to the Document. These Warranty Disclaimers are considered to be included by reference in this License, but only as regards disclaiming warranties: any other implication that these Warranty Disclaimers may have is void and has no effect on the meaning of this License.

### 2 VERBATIM COPYING

You may copy and distribute the Document in any medium, either commercially or noncommercially, provided that this License, the copyright notices, and the license notice saying this License applies to the Document are reproduced in all copies, and that you add no other conditions whatsoever to those of this License. You may not use technical measures to obstruct or control the reading or further copying of the copies you make or distribute. However, you may accept compensation in exchange for copies. If you distribute a large enough number of copies you must also follow the conditions in [section 3](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1639200).

You may also lend copies, under the same conditions stated above, and you may publicly display copies.

### 3 COPYING IN QUANTITY

If you publish printed copies (or copies in media that commonly have printed covers) of the Document, numbering more than 100, and the Document’s license notice requires Cover Texts, you must enclose the copies in covers that carry, clearly and legibly, all these Cover Texts: Front-Cover Texts on the front cover, and Back-Cover Texts on the back cover. Both covers must also clearly and legibly identify you as the publisher of these copies. The front cover must present the full title with all words of the title equally prominent and visible. You may add other material on the covers in addition. Copying with changes limited to the covers, as long as they preserve the title of the Document and satisfy these conditions, can be treated as verbatim copying in other respects.

If the required texts for either cover are too voluminous to fit legibly, you should put the first ones listed (as many as fit reasonably) on the actual cover, and continue the rest onto adjacent pages.

If you publish or distribute Opaque copies of the Document numbering more than 100, you must either include a machine-readable Transparent copy along with each Opaque copy, or state in or with each Opaque copy a computer-network location from which the general network-using public has access to download using public-standard network protocols a complete Transparent copy of the Document, free of added material. If you use the latter option, you must take reasonably prudent steps, when you begin distribution of Opaque copies in quantity, to ensure that this Transparent copy will remain thus accessible at the stated location until at least one year after the last time you distribute an Opaque copy (directly or through your agents or retailers) of that edition to the public.

It is requested, but not required, that you contact the authors of the Document well before redistributing any large number of copies, to give them a chance to provide you with an updated version of the Document.

### 4 MODIFICATIONS

You may copy and distribute a Modified Version of the Document under the conditions of [sections 2](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1638223) and [3](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1639200) above, provided that you release the Modified Version under precisely this License, with the Modified Version filling the role of the Document, thus licensing distribution and modification of the Modified Version to whoever possesses a copy of it. In addition, you must do these things in the Modified Version:

> A. Use in the Title Page (and on the covers, if any) a title distinct from that of the Document, and from those of previous versions (which should, if there were any, be listed in the History section of the Document). You may use the same title as a previous version if the original publisher of that version gives permission.

> B. List on the Title Page, as authors, one or more persons or entities responsible for authorship of the modifications in the Modified Version, together with at least five of the principal authors of the Document (all of its principal authors, if it has fewer than five), unless they release you from this requirement.

> C. State on the Title page the name of the publisher of the Modified Version, as the publisher.

> D. Preserve all the copyright notices of the Document.

> E. Add an appropriate copyright notice for your modifications adjacent to the other copyright notices.

> F. Include, immediately after the copyright notices, a license notice giving the public permission to use the Modified Version under the terms of this License, in the form shown in the Addendum below.

> G. Preserve in that license notice the full lists of Invariant Sections and required Cover Texts given in the Document’s license notice.

> H. Include an unaltered copy of this License.

> I. Preserve the section Entitled “History”, Preserve its Title, and add to it an item stating at least the title, year, new authors, and publisher of the Modified Version as given on the Title Page. If there is no section Entitled “History” in the Document, create one stating the title, year, authors, and publisher of the Document as given on its Title Page, then add an item describing the Modified Version as stated in the previous sentence.

> J. Preserve the network location, if any, given in the Document for public access to a Transparent copy of the Document, and likewise the network locations given in the Document for previous versions it was based on. These may be placed in the “History” section. You may omit a network location for a work that was published at least four years before the Document itself, or if the original publisher of the version it refers to gives permission.

> K. For any section Entitled “Acknowledgements” or “Dedications”, Preserve the Title of the section, and preserve in the section all the substance and tone of each of the contributor acknowledgements and/or dedications given therein.

> L. Preserve all the Invariant Sections of the Document, unaltered in their text and in their titles. Section numbers or the equivalent are not considered part of the section titles.

> M. Delete any section Entitled “Endorsements”. Such a section may not be included in the Modified Version.

> N. Do not retitle any existing section to be Entitled “Endorsements” or to conflict in title with any Invariant Section.

> O. Preserve any Warranty Disclaimers.

If the Modified Version includes new front-matter sections or appendices that qualify as Secondary Sections and contain no material copied from the Document, you may at your option designate some or all of these sections as invariant. To do this, add their titles to the list of Invariant Sections in the Modified Version’s license notice. These titles must be distinct from any other section titles.

You may add a section Entitled “Endorsements”, provided it contains nothing but endorsements of your Modified Version by various parties—for example, statements of peer review or that the text has been approved by an organization as the authoritative definition of a standard.

You may add a passage of up to five words as a Front-Cover Text, and a passage of up to 25 words as a Back-Cover Text, to the end of the list of Cover Texts in the Modified Version. Only one passage of Front-Cover Text and one of Back-Cover Text may be added by (or through arrangements made by) any one entity. If the Document already includes a cover text for the same cover, previously added by you or by arrangement made by the same entity you are acting on behalf of, you may not add another; but you may replace the old one, on explicit permission from the previous publisher that added the old one.

The author(s) and publisher(s) of the Document do not by this License give permission to use their names for publicity for or to assert or imply endorsement of any Modified Version.

### 5 COMBINING DOCUMENTS

You may combine the Document with other documents released under this License, under the terms defined in [section 4](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1641540) above for modified versions, provided that you include in the combination all of the Invariant Sections of all of the original documents, unmodified, and list them all as Invariant Sections of your combined work in its license notice, and that you preserve all their Warranty Disclaimers.

The combined work need only contain one copy of this License, and multiple identical Invariant Sections may be replaced with a single copy. If there are multiple Invariant Sections with the same name but different contents, make the title of each such section unique by adding at the end of it, in parentheses, the name of the original author or publisher of that section if known, or else a unique number. Make the same adjustment to the section titles in the list of Invariant Sections in the license notice of the combined work.

In the combination, you must combine any sections Entitled “History” in the various original documents, forming one section Entitled “History”; likewise combine any sections Entitled “Acknowledgements”, and any sections Entitled “Dedications”. You must delete all sections Entitled “Endorsements”.

### 6 COLLECTIONS OF DOCUMENTS

You may make a collection consisting of the Document and other documents released under this License, and replace the individual copies of this License in the various documents with a single copy that is included in the collection, provided that you follow the rules of this License for verbatim copying of each of the documents in all other respects.

You may extract a single document from such a collection, and distribute it individually under this License, provided you insert a copy of this License into the extracted document, and follow this License in all other respects regarding verbatim copying of that document.

### 7 AGGREGATION WITH INDEPENDENT WORKS

A compilation of the Document or its derivatives with other separate and independent documents or works, in or on a volume of a storage or distribution medium, is called an “aggregate” if the copyright resulting from the compilation is not used to limit the legal rights of the compilation’s users beyond what the individual works permit. When the Document is included in an aggregate, this License does not apply to the other works in the aggregate which are not themselves derivative works of the Document.

If the Cover Text requirement of [section 3](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1639200) is applicable to these copies of the Document, then if the Document is less than one half of the entire aggregate, the Document’s Cover Texts may be placed on covers that bracket the Document within the aggregate, or the electronic equivalent of covers if the Document is in electronic form. Otherwise they must appear on printed covers that bracket the whole aggregate.

### 8 TRANSLATION

Translation is considered a kind of modification, so you may distribute translations of the Document under the terms of [section 4](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1641540). Replacing Invariant Sections with translations requires special permission from their copyright holders, but you may include translations of some or all Invariant Sections in addition to the original versions of these Invariant Sections. You may include a translation of this License, and all the license notices in the Document, and any Warranty Disclaimers, provided that you also include the original English version of this License and the original versions of those notices and disclaimers. In case of a disagreement between the translation and the original version of this License or a notice or disclaimer, the original version will prevail.

If a section in the Document is Entitled “Acknowledgements”, “Dedications”, or “History”, the requirement ([section 4](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1641540)) to Preserve its Title ([section 1](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1632401)) will typically require changing the actual title.

### 9 TERMINATION

You may not copy, modify, sublicense, or distribute the Document except as expressly provided under this License. Any attempt otherwise to copy, modify, sublicense, or distribute it is void, and will automatically terminate your rights under this License.

However, if you cease all violation of this License, then your license from a particular copyright holder is reinstated (a) provisionally, unless and until the copyright holder explicitly and finally terminates your license, and (b) permanently, if the copyright holder fails to notify you of the violation by some reasonable means prior to 60 days after the cessation.

Moreover, your license from a particular copyright holder is reinstated permanently if the copyright holder notifies you of the violation by some reasonable means, this is the first time you have received notice of violation of this License (for any work) from that copyright holder, and you cure the violation prior to 30 days after your receipt of the notice.

Termination of your rights under this section does not terminate the licenses of parties who have received copies or rights from you under this License. If your rights have been terminated and not permanently reinstated, receipt of a copy of some or all of the same material does not give you any rights to use it.

### 10 FUTURE REVISIONS OF THIS LICENSE

The Free Software Foundation may publish new, revised versions of the GNU Free Documentation License from time to time. Such new versions will be similar in spirit to the present version, but may differ in detail to address new problems or concerns. See [http://www.gnu.org/copyleft/](http://www.gnu.org/copyleft/).

Each version of the License is given a distinguishing version number. If the Document specifies that a particular numbered version of this License “or any later version” applies to it, you have the option of following the terms and conditions either of that specified version or of any later version that has been published (not as a draft) by the Free Software Foundation. If the Document does not specify a version number of this License, you may choose any version ever published (not as a draft) by the Free Software Foundation. If the Document specifies that a proxy can decide which future versions of this License can be used, that proxy’s public statement of acceptance of a version permanently authorizes you to choose that version for the Document.

### 11 RELICENSING

“Massive Multiauthor Collaboration Site” (or “MMC Site”) means any World Wide Web server that publishes copyrightable works and also provides prominent facilities for anybody to edit those works. A public wiki that anybody can edit is an example of such a server. A “Massive Multiauthor Collaboration” (or “MMC”) contained in the site means any set of copyrightable works thus published on the MMC site.

“CC-BY-SA” means the Creative Commons Attribution-Share Alike 3.0 license published by Creative Commons Corporation, a not-for-profit corporation with a principal place of business in San Francisco, California, as well as future copyleft versions of that license published by that same organization.

“Incorporate” means to publish or republish a Document, in whole or in part, as part of another Document.

An MMC is “eligible for relicensing” if it is licensed under this License, and if all works that were first published under this License somewhere other than this MMC, and subsequently incorporated in whole or in part into the MMC, (1) had no cover texts or invariant sections, and (2) were thus incorporated prior to November 1, 2008.

The operator of an MMC Site may republish an MMC contained in the site under CC-BY-SA on the same site at any time before August 1, 2009, provided the MMC is eligible for relicensing.

## Index

### A

[a-b] dialplan pattern, [31](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos185045)

a-law codecs, [46](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos221706), [416](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos995492)

Aastra 480i telephone, [232–234](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos647207), [238–240](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos662667)

`aastra.cfg` file, [233](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos650591)

[a,b,c] dialplan pattern, [31](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos185045)

Absolute timeout, `TIMEOUT()` dialplan function, [640–641](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1437424)

`AbsoluteTimeout` command, AMI, [673–674](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1497472)

`AbsoluteTimeout()` dialplan application, [263–264](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos719381)

`Account`, call files, [185](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos559338)

Account information, SIP phone, [14](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos145224)

ACK packets, TCP connections, [92](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos325176)

`ackcall`, `agents.conf`, [166](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos519005)

`Action` packets, AMI, [188](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos568686)

`AddQueueMember()` dialplan application, [170](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos531167), [264–266](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos723850)

Adhearsion, using AGI with, [209–210](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos607013)

Administration

> conferencing, [418–423](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1004725)

> creating AMI user rights, [187](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos565613)

> `MeetMeAdmin()` application, [423–425](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1009831)

> `MeetMeChannelAdmin()` application, [425–426](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1014336)

> using contexts for rights, [18–20](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos156125)

ADSI, dialplan applications

> `ADSIProg()`, [266–267](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos728090)

> `GetCPEID()`, [266–267](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos728090), [381–382](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos923078)

ADSL, replacing ISDN in North America, [105](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos354773)

AEL (Asterisk Extension Language), [73–89](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos283836)

> `aelparse` utility, [74](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos286065)

> CLI commands for, [73–74](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos283836)

> defined, [73](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos283836)

> defining hints in, [229](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos640557)

> `extensions.conf` vs. `extensions.ael`. *See* [`extensions.conf` vs. `extensions.ael`](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1857290)

> upgrading from 1.4 to 1.6, [725](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1590135)

`ael parse` command, AEL, [74](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos286065)

`ael reload` command, AEL, [73](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos283836)

`aelparse` utility, [74](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos286065)

`agent, agents.conf`, [168](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos527307)

Agent channel, [95](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos334030)

`AGENT()` dialplan function, [576–577](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1306437)

`AgentCallbackLogin` command, AMI, [674](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1498667)

`AgentCallbackLogin()` dialplan application

> configuring call recording, [270–272](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos735731)

> defined, [169–170](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos529506)

> overview of, [267–268](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos729872)

`AgentLogin()` dialplan application

> `AgentCallbackLogin()` vs., [267](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos729872)

> defined, [169](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos529506)

> overview of, [268–269](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos732316)

`AgentLogoff` command, AMI, [674–675](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1498667)

`AgentMonitorOutgoing()` dialplan application, [270–272](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos735731)

Agents

> call queues and, [155–156](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos478319)

> configuring in `queues.conf`, [165](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos515133)

> defining in `agents.conf`, [156](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos480722), [166–168](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos519005)

`Agents` command, AMI, [675](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1500381)

`agents.conf`

> call queues, [166–168](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos519005)

> configuring call recording in, [270–272](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos735731)

> defined, [155](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos478319)

Aggregation with independent works, GNU Free Documentation License, [752](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1649755)

AGI (Asterisk Gateway Interface)

> data streams, [201–203](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos590492)

> `DeadAGI()` application, [322–325](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos831104)

> `EAGI()` application, [353–356](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos880515)

> `FastAGI()` application, [372](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos910236)

> with other programming languages, [211](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos610788)

> overview of, [201](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos590492)

> with Perl, [203–206](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos596240)

> with PHP, [206–209](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos603283)

> with Ruby and Adhearsion, [209–210](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos607013)

> working with large integers or floating point numbers, [62](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos252395)

AGI (Asterisk Gateway Interface), command summary, [647–671](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1447407)

> `ANSWER`, [647–648](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1447407)

> `ASYNCAGI BREAK`, [648](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1449167)

> `CHANNEL STATUS`, [648–649](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1449167)

> `CONTROL STREAM FILE`, [649](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1451163)

> `DATABASE DEL`, [650](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1452833)

> `DATABASE DELTREE`, [650](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1452833)

> `DATABASE GET`, [651](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1455113)

> `DATABASE PUT`, [651–652](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1455113)

> `EXEC`, [652](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1456851)

> `GET DATA`, [653](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1459038)

> `GET FULL VARIABLE`, [653–654](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1459038)

> `GET OPTION`, [654](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1461292)

> `GET VARIABLE`, [654–655](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1461292)

> `GOSUB`, [655](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1463501)

> `HANGUP`, [656](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1465422)

> `NOOP`, [656–657](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1465422)

> `RECEIVE CHAR`, [657](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1467863)

> `RECEIVE TEXT`, [657–658](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1467863)

> `RECORD FILE`, [658](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1469603)

> `SAY ALPHA`, [659](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1471279)

> `SAY DATE`, [659–660](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1471279)

> `SAY DIGITS`, [661–662](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1474890)

> `SAY NUMBER`, [662](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1476861)

> `SAY PHONETIC`, [662–663](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1476861)

> `SAY TIME`, [663–664](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1478574)

> `SAYDATETIME`, [660](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1473205)

> `SEND IMAGE`, [664](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1480543)

> `SEND TEXT`, [664–665](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1480543)

> `SET AUTOHANGUP`, [665](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1482278)

> `SET CALLERID`, [665–666](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1482278)

> `SET CONTEXT`, [666](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1484262)

> `SET EXTENSION`, [667](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1486714)

> `SET MUSIC`, [667–668](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1486714)

> `SET PRIORITY`, [668](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1488938)

> `SET VARIABLE`, [669](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1491061)

> `STREAM FILE`, [669–670](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1491061)

> `TDD MODE`, [670](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1493463)

> `VERBOSE`, [670–671](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1493463)

> `WAIT FOR DIGIT`, [671](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1495464)

`AGI` command, AMI, [675–676](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1500381)

`agi-commands`, [273](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos742929)

`AGI()` dialplan application, [272–275](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos740357)

`agi show command`, [273](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos742929)

`agi-test.agi`, [203](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos596240)

`ahn` program, Adhearsion, [209–210](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos607013)

AJAM (Asynchronous JavaScript Asterisk Manager), [195–199](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos581182)

> accessing AMI via HTTP, [195](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos581182)

> accessing AMI with AJAX, [197–199](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos586401)

> getting number of mailbox messages, [196–197](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos584396)

AJAX (Asynchronous JavaScript and XML), [197–198](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos586401)

`AlarmReceiver()` dialplan application, [276–277](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos745979)

`alarmreceiver.conf`, [276](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos745979)

AMA flags, `SetAMAFlags()` dialplan application, [513–514](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1181134)

`AMD()` dialplan application, [277–281](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos748258)

`AMDCAUSE` channel variable, [278–281](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos750546)

`amd.conf`, [277–278](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos748258)

`AMDSTATUS` channel variable, [278–281](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos750546)

AMI (Asterisk Manager Interface)

> activating, [186](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos563907)

> commands for, [189–190](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos572624)

> creating user, [187](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos565613)

> getting number of mailbox messages with PHP, [193–195](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos578978)

> getting number of voicemail messages with `expect`, [190–192](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos573669)

> overview of, [186](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos563907)

> StarAstAPI for PHP, [192–193](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos575692)

> talking to, [187–188](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos565613)

> upgrading CLI from 1.4 to 1.6, [727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

> upgrading from 1.4 to 1.6, [731](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1612643)

AMI (Asterisk Manager Interface), command summary

> `AbsoluteTimeout`, [673–674](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1497472)

> `AgentCallbackLogin`, [674](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1498667)

> `AgentLogoff`, [674–675](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1498667)

> `Agents`, [675](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1500381)

> `AGI`, [675–676](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1500381)

> `Atxfer`, [676](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1502436)

> `Bridge`, [676–677](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1502436)

> `Challenge`, [677](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1504158)

> `ChangeMonitor`, [677–678](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1504158)

> `Command`, [678](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1506173)

> `CoreSettings`, [678–679](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1506173)

> `CoreShowChannels`, [679](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1508240)

> `CoreStatus`, [679](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1508240)

> `CreateConfig`, [680](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1510245)

> `DAHDIDialOffhook`, [680](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1510245)

> `DAHDIDNDoff`, [681](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1512307)

> `DAHDIDNDon`, [681–682](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1512307)

> `DAHDIHangup`, [682](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1514295)

> `DAHDIRestart`, [682–683](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1514295)

> `DAHDIShowChannels`, [683](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1516104)

> `DAHDITransfer`, [684](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1518148)

> `DBDel`, [684](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1518148)

> `DBDelTree`, [685](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1520152)

> `DBGet`, [685](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1520152)

> `DBPut`, [686](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1522110)

> `Event`s, [686](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1522110)

> `ExtensionState`, [687](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1524156)

> `GetConfig`, [687–688](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1524156)

> `GetConfigJSON`, [688](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1525895)

> `GetVar`, [689](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1527327)

> `Hangup`, [689](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1527327)

> `IAXnetstats`, [690](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1529055)

> `IAXpeerlist`, [690–691](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1529055)

> `IAXpeers`, [691](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1530996)

> `JabberSend`, [691](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1530996)

> `ListCategories`, [692](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1533254)

> `ListCommands`, [692–693](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1533254)

> `Login`, [693](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1535148)

> `Logoff`, [693](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1535148)

> `MailboxCount`, [694](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1537448)

> `MailboxStatus`, [695](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1538587)

> `MeetmeList`, [695–696](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1538587)

> `MeetmeMute`, [696](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1540326)

> `MeetmeUnmute`, [696–697](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1540326)

> `ModuleCheck`, [697](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1542445)

> `ModuleLoad`, [697–698](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1542445)

> `Monitor`, [698](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1544153)

> `Originate`, [698–699](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1544153)

> `Park`, [699–700](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1545753)

> `ParkedCalls`, [700](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1547180)

> `PauseMonitor`, [700–701](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1547180)

> `Ping`, [701](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1549263)

> `PlayDTMF`, [702](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1550854)

> `QueueAdd`, [702](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1550854)

> `QueueLog`, [703](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1552930)

> `QueueParse`, [703](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1552930)

> `QueuePenalty`, [703–704](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1552930)

> `QueueRemove`, [704](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1555416)

> `QueueRule`, [704](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1555416)

> `Queues`, [704–705](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1555416)

> `QueueStatus`, [705](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1557856)

> `QueueSummary`, [705–706](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1557856)

> `Redirect`, [706](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1560184)

> `Reload`, [706–707](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1560184)

> `SendText`, [707](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1562078)

> `SetCDRUserField`, [707](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1562078)

> `SetVar`, [708](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1564247)

> `ShowDialPlan`, [708](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1564247)

> `SIPnotify`, [709](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1566145)

> `SIPpeers`, [709–710](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1566145)

> `SIPqualifypeer`, [710](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1568145)

> `SIPshowpeer`, [710–711](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1568145)

> `SIPshowregistry`, [711](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1569615)

> `Status`, [712](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1571127)

> `StopMonitor`, [712–713](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1571127)

> `UnpauseMonitor`, [713](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1572810)

> `UpdateConfig`, [713–714](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1572810)

> `UserEvent`, [714–715](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1574909)

> `VoiceMailUsersList`, [715](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1576070)

> `WaitEvent`, [715–716](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1576070)

> `ZapDialOffhook`, [716](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1578002)

> `ZapDNDoff`, [717](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1579725)

> `ZapDNDon`, [717–718](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1579725)

> `ZapHangup`, [718](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1581665)

> `ZapRestart`, [718–719](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1581665)

> `ZapShowChannels`, [719](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1583450)

> `ZapTransfer`, [720](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1585460)

AMI proxy, [188](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos568686)

analog telephone adapters. *See* [ATA (analog telephone adapters)](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1709227)

Analog telephony

> ATA, [114](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos384174)

> connecting devices, [113–114](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos380837)

> digital codecs vs., [101](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos344825)

> huge role in North America of, [112](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos377750)

> types of devices used by, [112–113](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos377750)

> using ATA, [3](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos116052)

> using FXS port, [4](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos119540)

> VoIP superior to, [102](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos346330)

`announce-frequency`, `queues.conf`, [162](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos501680)

`announce-holdtime`, `queues.conf`, [162](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos501680)

`announce`, `queues.conf`, [160](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos493721)

`announce-round-seconds`, `queues.conf`, [162](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos501680)

`announcement` argument`, Queue()`, [468–469](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1096955)

Announcement sound files, `queues.conf`, [165–166](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos515133)

`ANSWER` command, AGI, [647–648](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1447407)

`Answer ()` dialplan application

> defined, [12](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos139227), [27](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos172669)

> overview of, [281–282](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos756870)

`ANSWER` variable, `Dial()`, [330](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos854267)

`ANSWEREDTIME` variable, `Dial()`, [330](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos854267)

Answering machine detection, [277–281](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos748258)

Apache, as proxy for AJAM, [198–199](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos587667)

`AppendCDRUserField()` dialplan application, [282–283](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos758795)

`aptitude install ssh` command, [247–248](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos679729)

ARA (Asterisk RealTime Architecture), [27](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos172669)

`Archive,` call files, [185](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos559338)

Arguments, calling macros using, [70](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos278723)

`ARRAY()` function, [578–579](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1312579)

AstDB (Asterisk database), [145–153](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos459042)

> accessing from CLI, [147–149](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos464564)

> accessing from system shell, [149](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos471433)

> application example, call forwarding, [150–152](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos473451)

> application example, calling card, [152–153](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos476649)

> backup, [150](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos473451)

> defined, [145](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos459042)

> deleting family or branch, [319–320](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos824186)

> deleting key, [318–319](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos822659)

> deleting values, [147](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos464564), [595–596](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1348514)

> displaying contents, [149](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos471433)

> `LookupBlacklist()` application, [402–404](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos966495)

> `LookupCIDName()` application, [404–405](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos970544)

> overview of, [145–146](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos459042)

> reading values, [146–147](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos460765), [320–321](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos826465)

> resetting values, [594–595](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1346713)

> storing values, [321–322](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos828997)

> testing key, [596–597](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1350718)

> writing values, [146](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos460765)

`AST_DEVICE_BUSY` variable, `ChanlsAvail()`, [295](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos780692)

`AST_DEVICE_IN_USE` variable, `ChanlsAvail()`, [295](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos780692)

`AST_DEVICE_INVALID` variable, `ChanlsAvail()`, [296](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos784516)

`AST_DEVICE_NOT_INUSE` variable, `ChanlsAvail()`, [295](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos780692)

`AST_DEVICE_RINGING` variable, `ChanlsAvail()`, [296](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos784516)

`AST_DEVICE_UNAVAILABLE` variable, `ChanlsAvail()`, [296](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos784516)

`AST_DEVICE_UNKNOWN` variable, `ChanlsAvail()`, [295](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos780692)

Asterisk

> 1.4 installation. *See* [Installation, Asterisk 1.4](#Practical_As-sk_1.4_and_1.6_split_042.html_filepos1899056)

> debugging, [12–13](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos139227)

> economics of implementing, [42](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos211266)

> prerolled systems, [42](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos211266)

> starting, [11](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos136368)

> stopping, [13](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos142885)

> upgrading to 1.6\. *See* [Upgrading from 1.4 to 1.6](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos2045518)

`asterisk -c` command, [11–13](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos136368)

Asterisk database. *See* [AstDB (Asterisk database)](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1700219)

Asterisk Extension Language. *See* [AEL (Asterisk Extension Language)](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1661919)

Asterisk Gateway Interface. *See* [AGI (Asterisk Gateway Interface)](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1667122)

Asterisk, getting the most out of this book

> additional resources, [6–7](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos126171)

> reader contributions and feedback, [5–6](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos122613)

> understanding, [1–2](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos110938)

> updates and versions, [5](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos122613)

> who should read it, [3–4](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos116052)

`asterisk-image` command, [205](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos601014)

Asterisk key (*) dialplan pattern, [31](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos185045)

Asterisk Manager Interface. *See* [AMI (Asterisk Manager Interface)](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1678598)

`asterisk -r` command, [32](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos189215)

`asterisk -rc 'command'`, [149](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos471433)

Asterisk RealTime Architecture (ARA), [27](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos172669)

`asterisk -rx` command, [183](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos554664)

`asterisk -V` command, [255](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos690282)

`asterisk -vvvr` command, [447](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1061462)

`asterisk -vvvvc` command, [14–15](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos145224), [17–18](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos153858)

`asterisk.conf`, upgrading from 1.4 to 1.6, [726](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

`ASYNCAGI BREAK` command, AGI, [648](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1449167)

Asynchronous JavaScript Asterisk Manager. *See* [AJAM (Asynchronous JavaScript Asterisk Manager)](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1676726)

ATA (analog telephone adapters)

> analog media gateways as, [111](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos374542)

> connecting fax machines and cordless phones using, [44](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215268)

> no need for `s` extension when using, [70](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos278723)

> overview of, [114](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos384174)

`attach`, `voicemail.conf`, [125](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos401738)

attended transfers, [176](#Practical_As-sk_1.4_and_1.6_split_021.html_filepos546032)

`Atxfer` command, AMI, [676](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1502436)

Audio formats, upgrading from 1.4 to 1.6, [729](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1604551)

Australia, legalities for hold music, [157](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos483985)

`Authenticate()` dialplan application

> overview of, [283–286](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos760452)

> `VMAuthenticate()vs.`, [551–552](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1262596)

Authors of Document, GNU Free Documentation License, [749](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1640433), [751](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1646833)

`autologoff`, `agents.conf`, [166](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos519005)

`autopause`, `queues.conf`, [164](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos510671)

`${AVAILCHAN}` variable, `ChanlsAvail()`, [295](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos780692)

`${AVAILORIGCHAN}` variable, `ChanlsAvail()`, [295](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos780692)

`${AVAILSTATUS}` variable, `ChanlsAvail()`, [295](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos780692)

### B

B (bearer) channel, ISDN, [106](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos358095)

Back-Cover Text, GNU Free Documentation License

> aggregation with independent works, [752](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1649755)

> copying and distributing Modified Version, [751](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1646833)

> defined, [747](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1634621)

> enclosing when copying in quantity, [748](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1637794)

`Background()` dialplan application

> overview of, [287–290](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos766517)

> simple IVR, [138–139](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos444860)

`BackgroundDetect()` dialplan application, [290–291](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos770151)

Backslashes, upgrading from 1.4 to 1.6, [726](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

`Backticks()` dialplan application, [540](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1241527)

`BACKTICKS()` function, [540](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1241527)

Backup, database, [150](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos473451)

Bandwidth

> Asterisk calculator for, [46](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos221706)

> business telephone system case study, [45–46](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos218334)

> of commonly used codecs, [104–105](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos351208)

> ensuring sufficient, [46](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos221706)

> modern networks carrying voice traffic, [45](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos218334)

> packet delay/loss for real-time traffic, [45](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos218334)

> trunking and, [105](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos354773)

`BASE64_DECODE()` function, [579–580](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1314866)

`BASE64_ENCODE()` function, [580](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1316391)

basic rate interface. *See* [BRI (basic rate interface), ISDN](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1718890)

BDB (Berkeley DB), [145–146](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos459042)

bearer (B) channel, ISDN, [106](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos358095)

`beep.gsm` file, [205](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos601014)

Beginners, how to use this book, [3–4](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos116052)

Berkeley DB (BDB), [145–146](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos459042)

Bidirectional data transmission, TCP, [90–91](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos318644)

Blacklists

> `BLACKLIST()` function, [580–581](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1316391)

> `LookupBlacklist()` application, [402–404](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos966495)

BLF (Busy Lamp Field)

> advanced indicators in 1.6, [242–247](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos669776)

> configuring pickup, [237–242](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos660150)

> configuring telephones, Aastra 480i, [232–234](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos647207)

> configuring telephones, overview, [231–232](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos644855)

> configuring telephones, Soundpoint IP 501, [234–236](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos651700)

> controlling indicators, [228](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos637762)

> hints, [229–230](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos640557), [236–237](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos656856)

> overview of, [227](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos635655)

> subscriptions, [229–230](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos640557)

blind transfers, [175–176](#Practical_As-sk_1.4_and_1.6_split_021.html_filepos543958)

`break` statement, AEL, [82](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos302897), [85](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos308520)

BRI (basic rate interface), ISDN

> choosing ISDN card, [108–111](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos364379)

> overview of, [106–107](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos358095)

> support in DAHDI, [739](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1627456)

> in United States, [107–108](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos361159)

`Bridge` command, AMI, [676–677](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1502436)

`Bridge()` dialplan application, [292](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos773402)

`BRIDGERESULT` variable, `Bridge()`, [292](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos773402)

Buddy Watch, [234–236](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos651700)

Business telephone system case study, [41–55](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos209486). *See also* [Widgets, Inc](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos2067436).

> base configuration, [48–52](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos228287)

> choosing infrastructure, [44](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215268)

> choosing network, [44–46](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215268)

> choosing server hardware, [46–48](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos221706)

> numbering plan, [43](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos214482)

> overview of, [41–42](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos209486)

> voicemail system example, [117–121](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos388734)

> writing dialplan, [52–55](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos232968)

`Busy()` dialplan application, [293](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos776284)

Busy Lamp Field. *See* [BLF (Busy Lamp Field)](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1717075)

`BUSY` variable, `Dial()`, [330](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos854267)

### C

`C system()` function, [540–541](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1241527)

Call center applications. *See* [Queues (call center functions), dialplan applications](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos1976107)

Call files, [184–186](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos556023)

Call forwarding example, [150–152](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos473451)

`call-limit`, Busy Lamp Field, [228](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos637762)

`call-limit`, `sip.conf`, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934)

Call limits, upgrading from 1.4 to 1.6, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934)

Call management, dialplan applications

> `Answer()`, [281–282](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos756870)

> `Busy()`, [293](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos776284)

> `ChanIsAvail()`, [295–297](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos780692)

> `ChannelRedirect()`, [297–298](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos786359)

> `Congestion()`, [307–308](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos801625)

> `DIAL()`. *See* [`Dial()` dialplan application](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1775300)

> `DISA()`, [346–351](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos872246)

> `FollowMe()`, [376–377](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos919020)

> `Hangup()`, [392](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos944741)

> overview of, [259](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos698046)

> `Page()`, [448–450](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1063380)

> `Park()`, [450–452](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1067981)

> `Pickup()`, [238](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos662667), [458–460](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1080907)

> `RetryDial()`, [492–494](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1139673)

> `Ringing()`, [495](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1145189)

Call transfers, [175–176](#Practical_As-sk_1.4_and_1.6_split_021.html_filepos543958)

`callback`, `voicemail.conf`, [125](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos401738)

Caller ID

> filtering by, [88](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos314321)

> `SET CALLERID` command, AGI, [665–666](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1482278)

Caller ID, dialplan applications

> `LookupBlacklist()`, [402–403](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos966495)

> `LookupCIDName()`, [404–405](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos970544)

> overview of, [260](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos703911)

> `PrivacyManager()`, [464–467](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1089698)

> `SetCallerPres()`, [515–516](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1186143)

> `SetCIDName()`, [517–518](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1191918)

> `SetCIDNum()`, [517–518](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1191918)

> `SoftHangup()`, [532–533](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1226381)

> `Zapateller()`, [567–568](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1291662)

`callerid: <callerid>,.call` files, [185](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos559338)

`CALLERID()` function

> with `num` field, [40](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos207187), [582](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1320855)

> overview of, [581–583](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1318544)

> replacing `SetCIDNum()`, [517–518](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1191918)

> replacing `SetRDNIS()`, [523](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1205240)

`callerid` variable

> defined, [52](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos232968)

> `DISA()` application option, [347–351](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos872992)

`callgroup`, Busy Lamp Field, [228](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos637762)

`call_id, queue_log`, [170](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos531167)

Canada, legalizing hold music in, [157](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos483985)

`CANCEL` variable, `Dial()`, [330](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos854267)

CAPI channel, [95](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos334030)

Cards, choosing ISDN, [108–111](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos364379)

Case branches, `break` statements in, [82](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos302897)

Case studies

> business telephone system. *See* [Business telephone system case study](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1720180)

> variables, [61–62](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos249331)

CC-BY-SA (Creative Commons Attribution-Share Alike) 3.0 license, [754–755](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1654847)

CDR (Call Detail Record)

> resetting for this call, [329](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos849385)

> `SetCDRUserField` command, AMI, [707](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1562078)

> upgrading from 1.4 to 1.6, [729](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1604551)

CDR (Call Detail Record), dialplan applications, [410–411](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos981819)

> `AppendCDRUserField()`, [282–283](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos758795)

> `ForkCDR()`, [377–381](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos920592)

> `NoCDR()`, [446](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1059176)

> `ResetCDR()`, [490–491](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1135855)

> `SetAMAFlags()`, [513–514](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1181134)

> `SetCDRUserField()`, [516–517](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1190138)

`CDR ()` function, [282–283](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos758795), [584–587](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1325515)

`cdr_manager` module, [731](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1612643)

`cdr_odbc` module, [729](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1604551)

`cdr_sqlite` module, [729](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1604551)

`cdr_tds` module, [729](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1604551)

Central provisioning, [232](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos647207)

Cepstral TTS, installing, [142–143](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos454530)

CGI (Common Gateway Interface), AGI vs., [201](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos590492)

`Challenge` command, AMI, [677](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1504158)

`chan_console` channel driver, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934)

`chan_dahdi` channel driver, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934), [737](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1620661)

Change variables, dialplan applications

> `ImportVar()`, [396–397](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos953395)

> overview of, [260](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos703911)

> `Read()`, [476–479](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1110679)

> `ReadFile()`, [481](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1117321)

> `RealTime()`, [482–483](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1119019)

> `RealTimeUpdate()`, [483–484](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1121980)

> `Set()`, [509–512](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1175351)

> `SetGlobalVar()`, [518–519](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1193434)

`ChangeMonitor` command, AMI, [677–678](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1504158)

`ChangeMonitor()` dialplan application, [293–294](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos776284)

`ChanIsAvail()` dialplan application, [295–297](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos780692), [727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

`chan_local.c`, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934)

`chan_misdn` channel driver, [737](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1620661), [739](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1627456)

`Channel: <channel>,.call` files, [185](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos559338)

Channel drivers

> DAHDI, mISDN and, [737](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1620661)

> upgrading from 1.4 to 1.6, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934)

`CHANNEL()` function

> defined, [65](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos262382)

> overview of, [588–591](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1333553)

> replacing `SetLanguage()`, [521–522](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1200468)

`channel, queue_log`, [170](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos531167)

`CHANNEL STATUS` command, AGI, [648–649](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1449167)

Channel variables

> inheritance of, [63–65](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos256216)

> overview of, [58](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos241410), [61](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos249331)

channelprefix, `ChanSpy()`, [299](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos789948)

`ChannelRedirect()` dialplan application, [297–298](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos786359), [727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

Channels

> defined, [95](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos334030)

> ISDN, [106–107](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos358095)

> PRI, [107–108](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos361159)

> recording current channel in two separate files, [436–440](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1037985)

> types of, [95–97](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos334030)

`ChanSpy()` dialplan application, [299–305](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos789948)

`chan_zap` channel driver, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934), [737](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1620661)

`charset`, `voicemail.conf`, [125](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos401738)

`CheckGroup()` dialplan application, [305–306](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos798045)

`checkresult` subroutine, [204–205](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos599360)

`CHECKSIPDOMAIN()` function, [591–592](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1341424)

`chmod 755` *`script_name`*, [203](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos596240)

`chmod a+x vmcount.exp`, [192](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos575692)

`cidinternalcontexts, voicemail.conf`, [128](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos414275)

Classes, defining for hold music, [159](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos490727)

`ClearHash()` dialplan application, [306–307](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos799925)

CLI (command-line interface)

> for AEL, [73–74](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos283836)

> AMI commands, [189](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos572624)

> calling “Hello World” from, [10–13](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos133735)

> conferencing commands in, [418–423](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1004725)

> database access from, [147–149](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos464564)

> refreshing dialplan during operation from, [27](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos172669)

> setting text from `NoOp()` in, [447](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1061462)

> upgrading from 1.4 to 1.6, [727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

> using `Verbose()` dialplan application, [550–551](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1261053)

Clock source, and conferencing, [179–180](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos549616)

Coaxial cable, replacing ISDN, [105](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos354773)

`codec /etc/iaxmodem/ttyiaxo`, [216](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos617821)

Codecs

> bandwidth and trunking, [105](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos354773)

> commonly used, [104–105](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos351208)

> configuring, [103](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos349293)

> overview of, [101–102](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos344825)

> performance and, [102–103](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos346330)

> what they do, [102](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos346330)

Collections of documents, GNU Free Documentation License, [752](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1649755)

Colon(:), AEL labels, [79–80](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos298217)

Comedian Mail, [117–121](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos388734)

Comma(,) delimiter

> calling macros, [70](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos278723)

> as parameter used in this book, [258](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos694389)

> upgrading from 1.4 to 1.6, [726](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

`Command`, AMI command, [678](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1506173)

command-line interface. *See* [CLI (command-line interface)](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1741824)

Commands

> AGI. *See* [AGI (Asterisk Gateway Interface), command summary](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1668844)

> AMI. *See* [AMI (Asterisk Manager Interface), command summary](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1680251)

> CLI. *See* [CLI (command-line interface)](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1741824)

Comments, [16](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos151991), [76–77](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos292069)

Common Gateway Interface (CGI), AGI vs., [201](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos590492)

Conditionals, [81–84](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos300859)

`conf2ael` program, [725](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1590135)

Conferencing

> accessing with dialplan, [180](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos551711)

> announcing number of participants, [181](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos554102)

> CLI commands for, [418–423](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1004725)

> defining conference rooms, [180](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos551711)

> determining if installation provides, [180](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos551711)

> installation and timing device, [179](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos549616)

> monitoring status using hints, [242](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos669776)

Conferencing, dialplan applications

> `MeetMe()`, [415–417](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos992113)

> `MeetMeAdmin()`, [423–425](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1009831)

> `MeetMeChannelAdmin()`, [425–426](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1014336)

> `MeetMeCount()`, [426–427](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1016436)

Configuration files

> Asterisk, [258](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos694389)

> business telephone system case study, [48–52](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos228287)

> configuring BLF on Aastra 480i, [233–234](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos650591)

> difficulty of maintaining, [721–722](#Practical_As-sk_1.4_and_1.6_split_036.html_filepos1586621)

> renaming Zaptel as DAHDI, [735](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1617310)

> upgrading from 1.4 to 1.6, [731](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1612643)

Configuration templates, [721–723](#Practical_As-sk_1.4_and_1.6_split_036.html_filepos1586621)

`Congestion()` dialplan application, [307–308](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos801625)

Connections

> AMI, [188–189](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos568686)

> TCP, [91–92](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos321884)

> using analog telephony, [112–114](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos377750)

> using codecs, [101–105](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos344825)

> using ISDN, [105–112](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos354773)

Console channel

> defined, [96](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos337268)

> upgrading from 1.4 to 1.6, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934)

`console dial`, [11–13](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos136368), [15](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos148331)

Console text editor, [11](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos136368)

`Context`, call files, [185](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos559338)

`context`, `DISA()`, [347–351](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos872992)

`context`, `queues.conf`, [161](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos497987)

`${CONTEXT}` variable, [70](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos278723)

`@context`, `VoiceMail()` command, [122](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos393727)

`@context`, `VoiceMailMain()` command, [122](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos393727)

Contexts

> defined, [18](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos156125)

> defining in `voicemail.conf`, [131](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos425599)

> dialplans using, [25–26](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos167713)

> in `extensions.conf` vs. `extensions.ael`, [75–76](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos289802)

> multilevel IVR systems placing submenus in, [140](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos450940)

> rights administration using, [18–20](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos156125)

> taking calls from PSTN using, [23](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos166131)

> using `GoTo()` between, [59–60](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos244785)

`continue` statement, AEL, [85](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos308520)

`ContinueWhile()` dialplan application, [308–309](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos803941)

`CONTROL STREAM FILE` command, AGI, [649](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1451163)

`ControlPlayback()` dialplan application, [309–311](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos805839)

Copying Document, GNU Free Documentation License

> Modified Version of Document, [749–751](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1640433)

> in quantity, [748–749](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1637794)

> verbatim, [748](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1637794)

Copyleft, GNU Free Documentation License

> CC-BY-SA 3.0 license, [754](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1654847)

> defined, [745](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1630421)

Copyright notices, GNU Free Documentation License

> aggregation with independent works, [752](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1649755)

> copying and distributing Modified Version, [749–750](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1640433)

> translations, [752–753](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1649755)

> verbatim copying using, [748](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1637794)

`core application` command, [257](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692094)

`core set debug`, [13](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos142885)

`core set verbose 5`, [12–13](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos139227)

`core show applications`, [257](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692094)

`core show function FUNCTIONNAME`, [576](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1306437)

`core show functions`, [575](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304314)

`core show hints`, [236–237](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos656856), [245](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos678312)

`core show translation`, [102–105](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos346330)

Core, upgrading from 1.4 to 1.6, [726–727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

`CoreSettings` command, AMI, [678–679](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1506173)

`CoreShowChannels` command, AMI, [679](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1508240)

`CoreStatus` command, AMI, [679](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1508240)

Costs

> implementing Asterisk system, [42](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos211266)

> ISDN cards, [108–111](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos364379)

Cover Texts, GNU Free Documentation License

> aggregation with independent works, [752](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1649755)

> copying and distributing Modified Version, [750–751](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1643329)

> defined, [746](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1631869)

> enclosing when copying in quantity, [748](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1637794)

`cp` operation, `.call` files, [184](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos556023)

CPE-ID (customer premises equipment ID), retrieving, [381–382](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos923078)

CPU, choosing, [46–48](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos221706)

`CreateConfig` command, AMI, [680](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1510245)

`createlink, agents.conf`, [167](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos522834)

Creative Commons Attribution-Share Alike (CC-BY-SA) 3.0 license, [754–755](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1654847)

Cron jobs, [47](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos225320)

`Curl()` dialplan application, [311](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos809513)

`CURL()` function, [311](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos809513), [592–593](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1342284)

Curly braces ({ }), AEL extensions, [76](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos292069)

customer premises equipment ID (CPE-ID), retrieving, [381–382](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos923078)

`Cut()` dialplan application, [312](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos811433)

`CUT()` function, [312](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos811433), [593–594](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1344180)

### D

D (data) channel, ISDN, [106](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos358095)

DAHDI (Digium Asterisk Hardware Device Interface)

> asterisk modules, [736](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1619023)

> `Dial()`, [734](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1616103)

> files, [735](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1617310)

> interview with Kevin P. Fleming, [738](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1624026)

> kernel modules `(.ko)`, [735](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1617310)

> overview of, [111](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos374542)

> shell programs, [736](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1619023)

> stability and readiness of, [738](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1624026)

> upgrading from 1.4 to 1.6, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934)

> Zaptel project renamed to, [733–734](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1615363)

`DAHDIBarge()` dialplan application, [312–313](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos811433)

`DAHDIDialOffhook` command, AMI, [680](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1510245)

`DAHDIDNDoff` command, AMI, [681](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1512307)

`DAHDIDNDon` command, AMI, [681–682](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1512307)

`DAHDIHangup` command, AMI, [682](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1514295)

`DAHDIRAS()` dialplan application, [314–315](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos815341)

`DAHDIRestart` command, AMI, [682–683](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1514295)

`DAHDIScan()` dialplan application, [315–316](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos817304)

`DAHDISendKeypadFacility()` dialplan application, [316–317](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos818957)

`DAHDIShowChannels` command, AMI, [683](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1516104)

`DAHDITransfer` command, AMI, [684](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1518148)

DARPA (Defense Advanced Research Projects Agency), [44–45](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215268)

Darwinports package, [158–159](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos486769)

data (D) channel, ISDN, [106](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos358095)

Data integrity, TCP, [94](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos330257)

data streams

> defined, [201](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos590492)

> STDERR (standard error), [203](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos596240)

> STDIN (standard input), [201–202](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos590492)

> STDOUT (standard out), [202](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos592035)

Data transmission

> TCP, [90–91](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos318644), [93–94](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos328611)

> UDP, [95](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos334030)

Database. *See also* [AstDB (Asterisk database)](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1700219)

> `DBdel()` dialplan application, [318–319](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos822659)

> `DBdeltree()` dialplan application, [319–320](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos824186)

`DATABASE DEL` command, AGI, [650](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1452833)

`database del` command, CLI, [148](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos468120)

`DATABASE DELTREE` command, AGI, [650–651](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1452833)

`database deltree` command, CLI, [148–149](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos468120)

`DATABASE GET` command, AGI, [651](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1455113)

`database get` command, CLI, [148](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos468120)

`DATABASE PUT` command, AGI, [651–652](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1455113)

`database put` command, CLI, [148](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos468120)

`database show` command, CLI, [148–149](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos468120)

`database showkey` command, CLI, [148–149](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos468120)

Dates

> `SAY DATE` command, AGI, [660](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1473205)

> `SAYDATETIME` command, AGI, [660–661](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1473205)

> `STRFTIME()` function, [637–638](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1433473)

> `STRPTIME()` function, [638–639](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1435345)

`DateTime()` dialplan application, [317–318](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos820811)

`DB()` function

> overview of, [594–595](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1346713)

> reading values from database, [146–147](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos460765)

> replacing `DBput()`, [321–322](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos828997)

> writing values to database, [146](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos460765)

`DBDel` command, AMI, [684](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1518148)

`DBdel()` dialplan application, [147](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos464564), [318–319](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos822659)

`DB_DELETE()` function, [147](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos464564), [595–596](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1348514)

`DBDelTree` command, AMI, [685](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1520152)

`DBdeltree()` dialplan application, [147](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos464564), [319–320](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos824186)

`DB_EXISTS()` function, [596–597](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1350718)

`DBGet` command, AMI, [685](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1520152)

`DBget()` dialplan application, [145–146](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos459042), [320–321](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos826465)

`DBPut` command, AMI, [686](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1522110)

`DBput()` dialplan application, [145–146](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos459042), [321–322](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos828997)

De-multiplexing (demuxing), UDP, [95](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos334030)

`DeadAGI()` dialplan application, [322–323](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos831104)

Debian Linux

> Asterisk 1.4 installation and, [247–249](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos679729)

> IAXModem installation using, [213](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos611908)

> installation examples in this book using, [108](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos364379)

Defense Advanced Research Projects Agency (DARPA), [44–45](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215268)

Delay (latency)

> IP telephony and, [44–45](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215268)

> testing with `EAGI()`, [356–357](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos884594)

`delete`, `voicemail.conf`, [125](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos401738)

Deleting values from database, [147–148](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos464564)

Deprecated code

> locating applications in this book with, [258](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos694389)

> programming dialplan without using, [70](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos278723)

> replacing in dialplan, [64](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos258772)

`device`, `/etc/iaxmodem/ttyIAXO`, [215](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos615490)

`DEVICE_STATE()` function, [243–244](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos671921)

`DevState()` application, [243](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos671921)

`devstate change device state` command, CLI, [245](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos678312)

`DEVSTATE()` function, [243](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos671921)

`devstate list` command, CLI, [245](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos678312)

Dial-by-Name directory, [133–134](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos433667)

`Dial()` dialplan application, [323–341](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos833819)

> connecting to telephone, [15](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos148331)

> defined, [325](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos835255)

> enabling call transfer, [175](#Practical_As-sk_1.4_and_1.6_split_021.html_filepos543958)

> internal help from Asterisk 1.2 to 1.4, [335–336](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos860521)

> internal help from Asterisk 1.4 to 1.6, [337–341](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos861009)

> internal help in Asterisk 1.4, [331–335](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos858970)

> options, [327–330](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos840494)

> `RetryDial()`, [492–494](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1139673)

> understanding, [326](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos836591)

> variables set in, [330–331](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos854267)

`DIALEDTIME` variable, `Dial()`, [330](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos854267)

Dialplan

> accessing conferencing from, [180](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos551711)

> applying hints by reloading, [230](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos642545)

> building minimal phone system, [16–17](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos151991)

> business telephone system case study, [52–55](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos232968)

> call queues, [155–156](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos478319), [168–170](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos527307)

> calling AGI from within, [201](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos590492)

> removing backslashes in 1.6, [726](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

> upgrading from 1.4 to 1.6, [727–728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

> using PSTN for outbound calls, [22](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos163371)

> voicemail applications called from, [121–124](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos392052)

Dialplan applications, use of, [257–417](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692094)

> `AbsoluteTimeout()`, [263–264](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos719381)

> `AddQueueMember()`, [264–266](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos723850)

> ADSI. *See* [ADSI, dialplan applications](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1661305)

> `ADSIProg()`, [266–267](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos728090)

> `AgentCallbackLogin()`, [267–268](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos729872)

> `AgentLogin()`, [268–269](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos732316)

> `AgentMonitorOutgoing()`, [270–272](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos735731)

> `AGI()`, [272–275](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos740357)

> `AlarmReceiver()`, [276–277](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos745979)

> `AMD()`, [277–281](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos748258)

> `Answer()`, [281–282](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos756870)

> `AppendCDRUserField()`, [282–283](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos758795)

> `Authenticate()`, [283–284](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos760452)

> `Background()`, [283–286](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos760452)

> `BackgroundDetect()`, [290–291](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos770151)

> `Bridge()`, [292](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos773402)

> `Busy()`, [293](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos776284)

> call management. *See* [Call management, dialplan applications](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1723134)

> caller ID. *See* [Caller ID, dialplan applications](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1726652)

> CDR. *See* [CDR (Call Detail Record), dialplan applications](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1731911)

> change variables. *See* [Change variables, dialplan applications](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1734738)

> `ChangeMonitor()`, [293–294](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos776284)

> `ChanIsAvail()`, [295–297](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos780692)

> `ChannelRedirect()`, [297–298](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos786359)

> `ChanSpy()`, [299–305](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos789948)

> `CheckGroup()`, [305–306](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos798045)

> `ClearHash()`, [306–307](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos799925)

> conferencing. *See* [Conferencing, dialplan applications](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1748209)

> conferencing commands in CLI, [418–423](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1004725)

> `Congestion()`, [307–308](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos801625)

> `ContinueWhile()`, [308–309](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos803941)

> `ControlPlayback()`, [309–311](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos805839)

> `Curl()`, [311](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos809513)

> `Cut()`, [312](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos811433)

> `DAHDIBarge()`, [312–313](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos811433)

> `DAHDIRAS()`, [314–315](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos815341)

> `DAHDIScan()`, [315–316](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos817304)

> `DAHDISendKeypadFacility()`, [316–317](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos818957)

> database, [262](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos714427)

> `DateTime()`, [317–318](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos820811)

> `DBdel()`, [318–319](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos822659)

> `DBget()`, [320–321](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos826465)

> `DBput()`, [321–322](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos828997)

> `DeadAGI()`, [322–323](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos831104)

> `Dial()`. *See* [`Dial()` dialplan application](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1775300)

> `Dictate()`, [341–342](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos862331)

> `DigitTimeout()`, [343](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos867281)

> `Directory()`, [344–346](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos869381)

> `DISA()`, [346–351](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos872246)

> `DumpChan()`, [351–352](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos877151)

> `DUNDiLookup()`, [352–353](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos878503)

> `EAGI()`, [353–354](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos880515)

> `Echo()`, [356–357](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos884594)

> `EndWhile()`, [357–358](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos886170)

> `EnumLookup()`, [358–359](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos887594)

> `Eval()`, [359–360](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos889696)

> `Exec()`, [360–362](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos891549)

> `ExecIf()`, [362–363](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos894701)

> `ExecIfTime()`, [363–364](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos896980)

> `ExitWhile()`, [364–365](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos899096)

> `ExtenSpy()`, [365–369](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos900982)

> `ExternalIVR()`, [369–371](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos907303)

> `FastAGI()`, [372](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos910236)

> `Festival()`, [372–374](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos910236)

> `Flash()`, [374–375](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos915718)

> flow control and timeouts. *See* [Flow control and timeouts, dialplan applications](#Practical_As-sk_1.4_and_1.6_split_042.html_filepos1867684)

> `FollowMe()`, [376–377](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos919020)

> `ForkCDR()`, [377–381](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos920592)

> general, [262](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos714427)

> `GetCPEID()`, [381–382](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos923078)

> `GetGroupCount()`, [381–382](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos923078)

> `GetGroupMatchCount()`, [383](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos926789)

> `Gosub()`, [384](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos929554)

> `GosubIf()`, [385–386](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos931909)

> `Goto()`, [386–388](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos933707)

> `GotoIf()`, [388–389](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos936483)

> `GotoIfTime()`, [390–391](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos940252)

> `Hangup()`, [392](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos944741)

> `HasNewVoiceMail()`, [393–394](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos946570)

> `HasVoiceMail()`, [394–395](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos948560)

> `IAX2Provision()`, [395](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos950942)

> `ICES()`, [396](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos953395)

> `ImportVar()`, [396–397](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos953395)

> `Incomplete()`, [398](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos957421)

> `JabberSend()`, [398–399](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos957421)

> `JabberStatus()`, [399–400](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos959501)

> `KeepAlive()`, [401](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos963856)

> `Log()`, [401–402](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos963856)

> `LookupBlacklist()`, [402–403](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos966495)

> `LookupCIDName()`, [404–405](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos970544)

> `Macro()`, [405–408](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos973212)

> `MacroExclusive()`, [408–409](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos977170)

> `MacroExit()`, [409–410](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos979884)

> `MacroIf()`, [410–411](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos981819)

> macros, [259](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos698046)

> `mailboxExists()`, [411–412](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos984014)

> `Math()`, [413](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos987183)

> `MD5()`, [413–414](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos987183)

> `MD5Check()`, [414–415](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos989720)

> `MeetMe()`, [415–417](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos992113)

> `MeetMeAdmin()`, [423–425](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1009831)

> `MeetMeChannelAdmin()`, [425–426](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1014336)

> `MeetMeCount()`, [426–427](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1016436)

> `Milliwatt()`, [428–429](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1019892)

> `MinivmAccMess()`, [429–430](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1021488)

> `MinivmDelete()`, [430–431](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1024183)

> `MinivmGreet()`, [431–432](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1026296)

> `MinivmNotify()`, [432–433](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1029487)

> `MinivmRecord()`, [433–434](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1031429)

> miscellaneous, [263](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos719381)

> `MixMonitor()`, [434–436](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1033427)

> `Monitor()`, [436–440](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1037985)

> `Morsecode()`, [440–441](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1046762)

> `MP3Player()`, [441–442](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1048685)

> `MSet()`, [442–443](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1050918)

> music and sound output, [261](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos708602)

> `MusiconHold()`, [443–445](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1053474)

> `NBScat()`, [445–446](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1056906)

> `NoCDR()`, [446](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1059176)

> `NoOp()`, [446–447](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1059176)

> `ODBCFinish()`, [448](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1063380)

> overview of, [257–258](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692094)

> `Page()`, [448–450](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1063380)

> `Park()`, [450–452](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1067981)

> `ParkAndAnnounce()`, [452–454](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1070682)

> `ParkedCall()`, [454–455](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1073907)

> `PauseMonitor()`, [456](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1076724)

> `PauseQueueMember()`, [456–458](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1076724)

> `Pickup()`, [458–460](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1080907)

> `PickupChan()`, [460–461](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1083317)

> `Playback()`, [461–463](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1084746)

> `Playtones()`, [463–464](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1087751)

> `PrivacyManager()`, [464–467](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1089698)

> `Proceeding()`, [467](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1094672)

> `Progress()`, [467–468](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1094672)

> `Queue()`, [468–473](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1096955)

> `QueueLog()`, [473](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1105266)

> queues. *See* [Queues (call center functions), dialplan applications](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos1976107)

> `RaiseException()`, [474–475](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1107072)

> `Random()`, [475–476](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1108791)

> `Read()`, [476–479](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1110679)

> `ReadExten()`, [480](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1115769)

> `ReadFile()`, [481](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1117321)

> `RealTime()`, [482–483](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1119019)

> `RealTimeUpdate()`, [483–484](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1121980)

> `ReceiveFax()`, [484–486](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1123801)

> `Record()`, [486–488](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1126673)

> recording and monitoring. *See* [Recording and monitoring, dialplan applications](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos1982644)

> `RemoveQueueMember()`, [489–490](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1133659)

> `ResetCDR()`, [490–491](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1135855)

> `ResponseTimeout()`, [491–492](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1137453)

> `RetryDial()`, [492–494](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1139673)

> `Return()`, [494–495](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1143098)

> `Ringing()`, [495](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1145189)

> `SayAlpha()`, [496](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1147699)

> `SayDigits()`, [496–497](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1147699)

> `SayNumber()`, [497–499](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1150416)

> `SayPhonetic()`, [499–500](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1156660)

> `SayUnixTime()`, [500–501](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1158736)

> scripts. *See* [Scripts, dialplan applications](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos1997160)

> `SendDTMF()`, [502–503](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1163203)

> `SendFAX()`, [503–504](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1165458)

> `SendImage()`, [504–505](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1167182)

> `SendText()`, [505–506](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1169269)

> `SendURL()`, [507–509](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1172652)

> `Set()`, [509–512](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1175351)

> `SetAccount()`, [512–513](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1179336)

> `SetAMAFlags()`, [513–514](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1181134)

> `SetCallerID()`, [514–515](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1183766)

> `SetCallerPres()`, [515–516](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1186143)

> `SetCDRUserField()`, [516–517](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1190138)

> `SetCIDName()`, [517–518](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1191918)

> `SetCIDNum()`, [517–518](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1191918)

> `SetGlobalVar()`, [518–519](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1193434)

> `SetGroup()`, [521](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1200468)

> `SetLanguage()`, [521–522](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1200468)

> `SetMusicOnHold()`, [522–523](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1203356)

> `SetRDNIS()`, [523–524](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1205240)

> `SetTransferCapability()`, [524–525](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1207119)

> `SetVar()`, [526](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1211304)

> SIP, [262](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos714427)

> `SIPAddHeader()`, [526–527](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1211304)

> `SIPdtmfMode()`, [527–528](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1214103)

> `SIPGetHeader()`, [528–529](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1216089)

> `SMS()`, [529–530](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1218501)

> `SoftHangup()`, [532–533](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1226381)

> `Sort()`, [534](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1228942)

> `StackPop()`, [534–535](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1228942)

> `StartMusicOnHold()`, [535–536](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1231426)

> `StopMixMonitor()`, [536–537](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1233523)

> `StopMonitor()`, [537–538](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1235291)

> `StopMusicOnHold()`, [538–539](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1237142)

> `StopPlaytones()`, [539–540](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1239397)

> `System()`, [540–541](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1241527)

> `Transfer()`, [541–543](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1244531)

> `TryExecute()`, [543–544](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1247663)

> `TrySystem()`, [544–545](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1249969)

> `TXTCIDName()`, [545–546](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1252557)

> `UnpauseMonitor()`, [546–547](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1254217)

> `UnpauseQueueMember()`, [547–548](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1256128)

> `UserEvent()`, [548–550](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1258348)

> `Verbose()`, [550–551](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1261053)

> `VMAuthenticate()`, [550–551](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1261053)

> voicemail, [260](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos703911)

> `VoiceMail()`, [553–555](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1266820)

> `VoiceMailMain()`, [555–557](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1271157)

> `Wait()`, [557–558](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1274111)

> `WaitExten()`, [558–559](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1275848)

> `WaitForNoise()`, [559–560](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1278027)

> `WaitForRing()`, [560–561](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1280095)

> `WaitForSilence()`, [561–563](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1282190)

> `WaitMusicOnHold()`, [563–564](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1284555)

> `WaitUntil()`, [564–565](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1285741)

> `While()`, [566–567](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1289762)

> ZAP, [263](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos719381)

> `Zapateller()`, [567–568](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1291662)

> `ZapBarge()`, [568–569](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1294162)

> `ZapRAS()`, [570–571](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1297209)

> `ZapScan()`, [571–572](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1299680)

> `ZapSendKeypadFacility()`, [572–573](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1301274)

Dialplan functions, [575–646](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304314)

> `AGENT()` function, [576–577](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1306437)

> `ARRAY()` function, [578–579](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1312579)

> `BASE64_DECODE()`, [579–580](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1314866)

> `BASE64_ENCODE()`, [580](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1316391)

> `BLACKLIST()`, [580–581](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1316391)

> `CALLERID()`, [581–583](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1318544)

> `CDR ()`, [584–587](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1325515)

> `CHANNEL()`, [588–591](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1333553)

> `CHECKSIPDOMAIN()`, [591–592](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1341424)

> `CURL ()`, [592–593](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1342284)

> `CUT ()`, [593–594](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1344180)

> `DB()`, [594–595](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1346713)

> `DB_DELETE()`, [595–596](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1348514)

> `DB_EXISTS()`, [596–597](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1350718)

> `DUNDILOOKUP()`, [597–598](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1353054)

> `ENUMLOOKUP()`, [598–600](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1355437)

> `ENV()`, [600–601](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1358838)

> `EVAL()`, [601–602](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1359863)

> `EXISTS()`, [602–603](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1362007)

> `FIELDQTY()`, [603–604](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1363705)

> `FILTER()`, [604–605](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1365475)

> finding available installed, [576](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1306437)

> `GLOBAL()`, [605–606](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1367218)

> `GROUP()`, [606–607](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1368939)

> `GROUP_COUNT()`, [607–608](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1370652)

> `GROUP_LIST()`, [608](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1373225)

> `GROUP_MATCH()`, [608–609](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1373225)

> `IAXPEER()`, [609–611](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1375681)

> `IF()`, [611–612](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1381076)

> `IFTIME()`, [612–613](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1382722)

> `ISNULL()`, [613–614](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1385941)

> `KEYPADHASH()`, [614–615](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1387853)

> `LANGUAGE()`, [615–616](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1389602)

> `LEN()`, [616–617](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1392110)

> `MATH()`, [617–618](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1393507)

> `MD5()`, [618](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1396102)

> `MUSICCLASS()`, [619](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1397517)

> `ODBC_SQL()`, [620](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1399448)

> `ODBC_USER_DATABASE()`, [620–621](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1399448)

> overview of, [575–576](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304314)

> `QUEUEAGENTCOUNT()`, [621–622](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1401122)

> `QUEUEMEMBERCOUNT()`, [622–623](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1403202)

> `QUEUEMEMBERLIST()`, [623–624](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1405303)

> `QUOTE()`, [624](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1407138)

> `RAND()`, [624–625](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1407138)

> `REGEX()`, [626–627](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1410935)

> `SET()`, [627–628](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1412907)

> `SHA1()`, [628](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1414484)

> `SIPCHANINFO()`, [629–630](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1416373)

> `SIP_HEADER()`, [633–634](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1425449)

> `SIPPEER()`, [630–633](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1419120)

> `SORT()`, [634–635](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1426934)

> `STAT()`, [635–636](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1428458)

> `STRFTIME()`, [637–638](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1433473)

> `STRPTIME()` function, [638–639](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1435345)

> `TIMEOUT()`, [640–642](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1437424)

> `TXTCIDNAME()`, [642–643](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1440397)

> upgrading from 1.4 to 1.6, [727–728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

> `URIDECODE()`, [643–644](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1442173)

> `URIENCODE()`, [644–645](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1443531)

> `VMCOUNT()`, [645–646](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1445255)

Dialplan, fundamentals, [25–40](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos167713)

> `${EXTEN}` variable `${CALLERID(num)}` function, [39–40](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos204238)

> contexts, [25–26](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos167713)

> extensions, [26–27](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos169755)

> fundamental applications, [27–29](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos172669)

> `include` statements, [37–39](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos200489)

> pattern matching. *See* [Pattern matching](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos1955750)

Dialplan, programming, [57–71](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos239743)

> deprecated features, [71](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos281786)

> how-to do, [57–60](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos239743)

> macros, [70–71](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos278723)

> overview of, [57](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos239743)

> replacing code depending on deprecated variables or functions, [64](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos258772)

> special extensions, [67–70](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos270412)

> variables. *See* [Variables](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos2049732)

`dialplan reload`, [15](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos148331)

`dialplan show` command, [34–37](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos193924), [74](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos286065)

`Dictate()` dialplan application, [341–342](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos862331)

Digit timeouts, [640–641](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1437424)

Digital interface cards, choosing, [3](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos116052)

Digital telephone, choosing, [4](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos119540)

Digits

> `SAY DIGITS` command, AGI, [660–661](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1473205)

> `SayDigits()` application, [496–497](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1147699)

> sending out-of-band on ISDN PRI connection, [572–573](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1301274)

> transforming alphabetic strings using `KEYPADHASH()`, [614–615](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1387853)

`DigitTimeout()` dialplan application, [343](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos867281)

Digium Asterisk Hardware Device Interface. *See* [DAHDI (Digium Asterisk Hardware Device Interface)](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1761545)

Digium, ISDN cards, [111](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos374542)

Directed pickup, [237–240](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos660150)

Directories, moving from Zaptel to DAHDI, [735](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1617310)

`Directory()` dialplan application, [344–346](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos869381)

`directoryintro`, `voicemail.conf`, [125](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos401738)

`DISA()` dialplan application, [346–351](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos872246), [727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

Disk space, choosing server hardware, [47–48](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos225320)

DNS (Domain Name Service), using UDP, [95](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos334030)

DocBook format, [5–6](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos122613)

Domain Name Service (DNS), using UDP, [95](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos334030)

Double quotes (“ ”), strings, [62](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos252395), [149](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos471433)

Drivers, ISDN, [110–111](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos371159)

DTMF (dual-tone multi-frequency) keying

> calling AGI from Perl, [205](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos601014)

> inputting IVR, [137](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos443020)

> `PlayDTMF` command, [702](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1550854)

> `Read()` dialplan application and, [476–479](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1110679)

> `SendDTMF()` dialplan application, [502–503](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1163203)

`DumpChan()` dialplan application, [351–352](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos877151)

`dundi.conf`, [731](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1612643)

`DUNDiLookup()` dialplan application, [352–353](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos878503)

`DUNDILOOKUP()` function, [597–598](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1353054)

### E

E-mail attachments

> sending faxes received as, [224–225](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos631462)

> sending new mini-voicemails as, [432–433](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1029487)

> sending new voicemails as, [18](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos156125)

`EAGI()` dialplan application, [353–356](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos880515)

EAGI (Extended AGI), [353–356](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos880515)

Easy PABX, [172](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos538929)

Eavesdropping

> `ChanSpy()` enabling, [299–305](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos789948)

> `ExtenSpy()` enabling, [365–369](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos900982)

> `ZapBarge()` enabling Zap channel, [568–569](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1294162)

> `ZapScan()` scanning Zap channels, [571–572](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1299680)

Echo cancellation, [109](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos367864)

`Echo()` dialplan application, [356–357](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos884594)

Elements, pattern matching, [31](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos185045)

`[emailbody]`, `voicemail.conf`, [126](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos405883)

`emailsubject`, `voicemail.conf`, [125](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos401738)

Emergency numbers, adding international, [43](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos214482)

`endcall`, `agents.conf`, [167](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos522834)

Endpoints, TCP connections, [91–93](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos321884)

`EndWhile()` dialplan application, [357–358](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos886170)

Entitled Acknowledgements section, GNU Free Documentation License

> combining documents, [751](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1646833)

> copying and distributing Modified Version, [750](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1643329)

> translations, [753](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1652303)

Entitled Dedications section, GNU Free Documentation License

> copying and distributing Modified Version, [750](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1643329)

> translations, [753](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1652303)

Entitled Endorsements section, GNU Free Documentation License

> copying and distributing Modified Version, [750–751](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1643329)

> deleting when combining documents, [751](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1646833)

Entitled History section, GNU Free Documentation License

> combining documents, [751](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1646833)

> copying and distributing Modified Version, [750](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1643329)

> translations, [753](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1652303)

Entitled XYZ section of Document, GNU Free Documentation License, [747](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1634621)

`EnumLookup()` dialplan application, [358–359](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos887594)

`ENUMLOOKUP()` function, [358](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos887594), [598–600](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1355437)

`ENV()` function, [600–601](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1358838)

Errors

> hunting in `extensions.ael`, [74](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos286065)

> reporting, [5](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos122613)

`/etc/asterisk` directory, [10–11](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos133735)

`/etc/asterisk/features.conf`, [175–177](#Practical_As-sk_1.4_and_1.6_split_021.html_filepos543958)

`/etc/asterisk/meetme.conf`, [180](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos551711)

`/etc/asterisk/sip.conf`. *See* [`sip.conf`](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos2015616)

`/etc/asterisk/voicemail.conf`. *See* [`voicemail.conf`](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos2059851)

`/etc/iaxmodem/ttyIAXO`, [215–216](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos615490)

`/etc/inittab`, [216–217](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos617821)

EuroISDN BRI protocol, and DAHDI, [737–739](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1620661)

`Eval()` dialplan application, [359–360](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos889696)

`EVAL()` function, [359](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos889696), [601–602](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1359863)

Event packets, AMI, [188](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos568686)

`event, queue_log`, [170–172](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos531167)

`eventmemberstatus`, `queues.conf`, [164](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos510671)

Events

> connecting to AMI, [188](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos568686)

> recording log file queue, [170–172](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos531167)

> `UserEvent()`, [548–550](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1258348)

`Event`s command, AMI, [686](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1522110)

`eventwhencalled`, `queues.conf`, [164](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos510671)

`EXEC` command, AGI, [652](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1456851)

`Exec()` dialplan application

> overview of, [360–362](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos891549)

> `TryExecute()`, [543–544](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1247663)

`ExecIf()` dialplan application, [362–363](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos894701)

> `TryExecute()`, [543–544](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1247663)

> upgrading from 1.4 to 1.6, [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

`ExecIfTime()` dialplan application, [363–364](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos896980)

`EXISTS()` function, [602–603](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1362007)

`ExitWhile()` dialplan application, [364–365](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos899096)

`expect` script, AMI, [190–192](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos573669)

Experts, how to use this book, [4](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos119540)

Expressions, `extensions.conf` vs. `extensions.ael`, [78–79](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos295482)

`${EXTEN}` variable

> defined, [22](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos163371)

> dialplans, [40](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos207187)

> not using in macros, [70](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos278723)

> programming dialplan, [67–70](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos270412)

> as system variable, [59](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos244785)

Extended AGI (EAGI), [353–356](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos880515)

Extensions

> building minimal phone system with two, [16](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos151991)

> calling “Hello World” from CLI, [12](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos139227)

> calling SIP phone from Asterisk console, [15](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos148331)

> defining macros with, [70](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos278723)

> defining with *n* priority, [28–29](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos176857)

> dialplan, [26–27](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos169755)

> expanding variables in, [61](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos249331)

> `extensions.conf` vs. `extensions.ael`. *See* [`extensions.conf` vs. `extensions.ael`](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1857290)

> order of patterned, [35](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos195782)

> programming dialplan using, [67–70](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos270412)

> receiving faxes, [222–223](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos626837)

> testing hold music, [156–157](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos480722)

> using `GoTo()`, [59](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos244785)

`extensions reload command`, [27](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos172669)

`extensions.ael`. *See also* [`extensions.conf` vs. `extensions.ael`](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1857290)

> converting into `extensions.conf`, [74](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos286065)

> defining hints in, [229–230](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos640557)

> monitoring status of conferences using hints, [242–243](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos669776)

> monitoring status of SIP users, [242](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos669776)

> tying hints to virtual devices in 1.6, [243](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos671921)

`extensions.conf`

> building minimal phone system with two SIP phones, [16](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos151991)

> calling AGI from Perl, [203](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos596240)

> calling AGI from within, [201](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos590492)

> calling SIP phone from Asterisk console, [15](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos148331)

> configuring Asterisk, [11](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos136368)

> configuring voicemail, [17](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos153858)

> contexts in, [20](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos160573)

> converting into AEL with `conf2ael`, [725](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1590135)

> defining global variables in, [62](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos252395)

> defining hints in, [229–230](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos640557)

> dialplan, [121–124](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos392052)

> escape character in, [62](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos252395)

> example business voicemail system, [119–121](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos391399)

> example home voicemail system, [116](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos387630)

> monitoring status of conferences using hints, [242–243](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos669776)

> monitoring status of SIP users, [242](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos669776)

> pattern matching. *See* [Pattern matching](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos1955750)

> for pickup, [238](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos662667)

> programming dialplan, [58](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos241410)

> queues, [155–157](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos478319), [168–170](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos527307)

> receiving faxes, [222–223](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos626837)

> sending faxes, [223–224](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos629217)

> taking calls from PSTN, [23](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos166131)

> tying hints to virtual devices in 1.6, [243](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos671921)

> use of dialplan applications. *See* [Dialplan applications, use of](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1778885)

> writing dialplan, [52–54](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos232968)

`extensions.conf` vs. `extensions.ael`, [74–88](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos286065)

> choosing between, [88](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos314321)

> comments, [76](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos292069)

> conditionals, [81–84](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos300859)

> contexts, [75–76](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos289802)

> expressions, [78–79](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos295482)

> extensions, [75–76](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos289802)

> filtering by caller ID, [88](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos314321)

> global variables, [78](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos295482)

> `Goto`, [79–81](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos298217)

> hints, [87](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos312669)

> includes, [77](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos294239)

> jump, [79–81](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos298217)

> labels, [79–81](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos298217)

> line termination, [75](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos289802)

> loops, [84–86](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos306534)

> macros, [86](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos311190)

> overview of, [74–75](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos286065)

> priorities, [75–76](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos289802)

> variable assignment, [78–79](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos295482)

`ExtensionState` command, AMI, [687](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1524156)

`ExtenSpy()` dialplan application, [365–369](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos900982)

External control of Asterisk, [183–199](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos554664)

> AMI. *See* [AMI (Asterisk Manager Interface)](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1678598)

> `asterisk -rx` command, [183](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos554664)

> Asynchronous JavaScript Asterisk Manager, [195–199](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos581182)

> call files, [184–186](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos556023)

`ExternalIVR()` dialplan application, [369–371](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos907303)

`externnotify`, `voicemail.conf`, [127](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos410130)

`externpass`, `voicemail.conf`, [127](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos410130)

### F

FAQs, for this book, [3–5](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos116052)

FastAGI, [272](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos740357)

`FastAGI()` dialplan application, [372](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos910236)

`faxgetty`, IAXModem, [217](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos621282)

Faxing

> difficulties integrating Asterisk with, [44](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215268), [213](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos611908)

> ISDN problems, [110](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos371159)

> `ReceiveFax()` dialplan application, [484–486](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1123801)

> `SendFAX()` dialplan application, [503–504](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1165458)

> using BRI, [107](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos361159)

> using IAXModem. *See* [IAXModem](#Practical_As-sk_1.4_and_1.6_split_042.html_filepos1894067)

`faxsetup`, Hylafax, [218–219](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos623461)

`faxstat -s` command, [224](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos631462)

`features.conf`

> call parking, [177](#Practical_As-sk_1.4_and_1.6_split_021.html_filepos549074)

> call transfer, [175–176](#Practical_As-sk_1.4_and_1.6_split_021.html_filepos543958)

> enabling `Park()`, [450](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1067981)

> enabling `ParkedCall()`, [454](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1073907)

`Festival()` dialplan application, [372–374](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos910236)

`ffchar` key, `ControlPlayback()`, [309–310](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos805839)

fiber-to-the-home (FTTH), [105](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos354773)

`FIELDQTY()` function, [603–604](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1363705)

Fields, dialplan function

> `AGENT()`, [576–577](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1306437)

> `CALLERID()`, [581–582](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1318544)

> `CDR ()`, [584–587](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1325515)

> `CHANNEL()`, [588](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1333553)

> `IAXPEER()`, [609–611](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1375681)

> `SIPCHANINFO()`, [629](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1416373)

> `SIPPEER()`, [630–631](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1419120)

`FILTER()` function, [604–605](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1365475)

Filtering, by caller ID, [88](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos314321)

FIN packet, TCP, [92](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos325176)

Fink, [158](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos486769)

FinkCommander GUI, [159](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos490727)

Flags, `STAT()` function, [635–636](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1428458)

`Flash()` dialplan application, [374–375](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos915718)

Fleming, interview with Kevin P., [737–739](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1620661)

Floating-point numbers, [634–635](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1426934), [726](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

Flow control and timeouts, dialplan applications, [179](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos549616)

> `ContinueWhile()`, [308–309](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos803941)

> `EndWhile()`, [357–358](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos886170)

> `Exec()`, [360–362](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos891549)

> `ExecIf()`, [362–363](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos894701)

> `ExecIfTime()`, [363–364](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos896980)

> `ExitWhile()`, [364–365](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos899096)

> `Gosub()`, [384](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos929554)

> `GosubIf()`, [385–386](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos931909)

> `Goto()`, [386–388](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos933707)

> `GotoIf()`, [388–389](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos936483)

> `GotoIfTime()`, [390–391](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos940252)

> overview of, [259](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos698046)

> `Random()`, [475–476](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1108791)

> `Return()`, [494–495](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1143098)

> `TryExec()`, [543–544](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1247663)

> `While()`, [566–567](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1289762)

`FollowMe()` dialplan application, [376–377](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos919020)

`followme.conf` file, [376](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos919020)

`for` loops, [85–86](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos308520)

`forcegreetings`, `voicemail.conf`, [127](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos410130)

`forcename`, `voicemail.conf`, [127](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos410130)

Foreign Exchange Office (FXO) device, [112–113](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos377750)

Foreign Exchange Station (FXS) device, [113–114](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos380837)

Format

> for this book, [5](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos122613)

> `voicemail.conf` variables, [130](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos423739)

`format` option, `Record()`, [486–487](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1126673)

`format` option, `SayUnixTime()`, [500–501](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1158736)

Formats, for Transparent copies of Document, [747](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1634621)

`format_wav`, [729](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1604551)

Forward slashes (//), comments, [76–77](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos292069)

4B3T signaling type, BRI, [107](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos361159)

Free Software Foundation, [754](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1654847)

`fromstring=[fromname]`, `voicemail.conf`, [126](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos405883)

Front-Cover Text, GNU Free Documentation License

> aggregation with independent works, [752](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1649755)

> copying and distributing Modified Version, [751](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1646833)

> defined, [747](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1634621)

> enclosing when copying in quantity, [748](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1637794)

FTTH (fiber-to-the-home), [105](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos354773)

Functions

> `${CALLERID(num)}` function, [40](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos207187)

> dialplan. *See* [Dialplan functions](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1818664)

> system channel variables as, [65](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos262382)

Future revisions, GNU Free Documentation License, [754](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1654847)

FXO (Foreign Exchange Office) device, [112–113](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos377750)

FXS (Foreign Exchange Station) device, [113–114](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos380837)

### G

G.711 codec

> bandwidth requirements, [46](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos221706)

> defined, [104](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos351208)

> as most common telephony codec, [102](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos346330)

G.722 codec, [104](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos351208)

G.726 codec, [104](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos351208)

G.729.1 codec, [105](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos354773)

G.729a codec, [104](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos351208)

`gem install adhearsion`, [209](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos607013)

`[general]` context, [25](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos167713)

General dialplan applications, [262](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos714427)

`[general]` section, `voicemail.conf`, [124–129](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos400544)

`GET DATA` command, AGI, [653](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1459038)

`GET FULL VARIABLE` command, AGI, [653–654](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1459038)

`GET OPTION` command, AGI, [654](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1461292)

`GET VARIABLE` command, AGI, [654–655](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1461292)

`GetConfig` command, AMI, [687–688](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1524156)

`GetConfigJSON` command, AMI, [688](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1525895)

`GetCPEID()` dialplan application, [266–267](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos728090), [381–382](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos923078)

`GetGroupCount()` dialplan application, [382–383](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos924704)

`GetGroupMatchCount()` dialplan application, [383](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos926789)

getty, IAXModem, [217](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos621282)

`GetVar` command, AMI, [689](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1527327)

Global call forwarding, [151–152](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos475769)

`GLOBAL()` function, [518–519](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1193434), [605–606](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1367218)

Global System for Mobile. *See* [GSM (Global System for Mobile)](#Practical_As-sk_1.4_and_1.6_split_042.html_filepos1886288)

Global variables

> defining in `extensions.conf`, [62](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos252395)

> `extensions.conf` vs. `extensions.ael`, [78](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos295482)

> overview of, [58](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos241410)

> setting, [518–519](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1193434)

GNU Free Documentation License

> aggregation with independent works, [752](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1649755)

> applicability and definitions, [746–748](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1631869)

> collections of documents, [752](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1649755)

> combining documents, [751](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1646833)

> copying in quantity, [748–749](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1637794)

> future revisions of, [754](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1654847)

> modifications, [749–751](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1640433)

> purpose of, [745–746](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1630421)

> relicensing, [754–755](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1654847)

> termination, [753](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1652303)

> for this book, [5](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos122613)

> translation, [752–753](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1649755)

> verbatim copying, [748](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1637794)

GNU General Public License, [745](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1630421)

`GOSUB` command, AGI, [655](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1463501)

`Gosub()` dialplan application

> achieving macros with, [86](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos311190)

> overview of, [384](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos929554)

> removing return address from, [534–535](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1228942)

> replacing `Macro()` with, [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

> subroutines, [60](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos247469), [494–495](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1143098)

> upgrading macros to 1.6 in AEL, [725](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1590135)

`GosubIf()` dialplan application, [385–386](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos931909), [494–495](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1143098)

`Goto()` dialplan application

> calling from within macro, [405–406](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos973212)

> in `extensions.conf` vs. `extensions.ael`, [79–81](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos298217)

> multilevel IVR systems using, [140–141](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos450940)

> overview of, [386–388](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos933707)

> using, [59–60](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos244785)

GOTO:<context> ^<extension> ^<priority>, `Dial()`, [328](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos844986)

`GotoIf()` dialplan application, [60](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos247469), [388–389](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos936483)

`GotoIfTime()` dialplan application, [83–84](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos305035), [390–391](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos940252)

`GROUP()` function, [521](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1200468), [606–607](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1368939)

Group pickup

> configuring, [240–242](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos668284)

> defined, [237](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos660150)

`GROUP_COUNT()` function

> overview of, [607–608](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1370652)

> replacing `CheckGroup()`, [305](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos798045)

> replacing `GetGroupCount()`, [382](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos924704)

`GROUP_LIST()` function, [608](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1373225)

`GROUP_MATCH_COUNT()` function, [383](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos926789), [608–609](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1373225)

GSM (Global System for Mobile)

> codec, [104](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos351208)

> ensuring sufficient bandwidth using, [46](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos221706)

> MeetMe conferences using, [416](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos995492)

### H

`h` option, programming dialplan, [67–68](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos270412)

H.323 channel

> defined, [96](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos337268)

> upgrading from 1.4 to 1.6, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934)

`HANGUP` command, AGI, [656](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1465422), [665](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1482278)

`Hangup` command, AMI, [689–690](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1527327)

`Hangup()` dialplan application, [12](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos139227), [27](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos172669), [392](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos944741)

Hardware

> choosing server, [46–48](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos221706)

> echo cancellation, [109](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos367864)

> interface card as clock source for conferencing, [179](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos549616)

`HasNewVoiceMail()` dialplan application, [393–394](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos946570)

`HasVoiceMail()` dialplan application, [394–395](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos948560)

Header structure, TCP, [93](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos328611)

“Hello World”

> calling from CLI, [10–13](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos133735)

> calling with SIP phone, [13–16](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos142885)

> priorities, [29](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos181396)

> using two SIP phones, [16–18](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos151991)

`help` database command, CLI, [148](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos468120)

HFC-BRI cards, [111](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos374542)

HFC-S BRI cards, DAHDI, [738](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1624026)

Hints

> defining, [229–230](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos640557)

> `extensions.conf` vs. `extensions.ael`, [87](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos312669)

> implementing BLF, [228](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos637762)

> monitoring status of conferences, [242–243](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos669776)

> testing, [236–237](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos656856)

> tying to virtual devices in 1.6, [243–245](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos671921)

Hold music, call queues, [156–159](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos480722)

Home voicemail system, [115–117](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos385930)

HTML, [196](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos584396)

Hylafax

> configuring fax server, [218–219](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos623461)

> confirmation page, [220–221](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos625200)

> installing, [217–218](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos621282)

> installing IAXModem, [219–220](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos624094)

> receiving faxes, [222–223](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos626837)

> sending faxes, [223–224](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos629217)

> sending received faxes as e-mail, [224–225](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos631462)

> starting fax server, [221](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos625827)

### I

`i` option

> handling invalid input in IVR, [139–140](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos448284)

> programming dialplan, [68](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos273653)

IANA (Internet Assigned Numbers Authority), port numbers, [91](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos321884)

IAX

> configuring codecs, [103](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos349293)

> defined, [96–97](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos337268)

> SIP vs., [97–99](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos341191), [741–743](#Practical_As-sk_1.4_and_1.6_split_039.html_filepos1629188)

> trunking in IAX2, [105](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos354773)

`IAX2Provision()` dialplan application, [395](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos950942)

IAXModem

> configuring, [215–216](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos615490)

> configuring faxgetty and logging, [217](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos621282)

> installing, [213–215](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos611908)

> installing Hylafax, [217–221](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos621282)

> overview of, [213](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos611908)

> receiving faxes, [222–223](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos626837)

> sending faxes, [223–224](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos629217)

> sending received faxes as e-mail, [224–225](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos631462)

`IAXnetstats` command, AMI, [690](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1529055)

`IAXPEER()` function, [609–611](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1375681)

`IAXpeerlist` command, AMI, [690–691](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1529055)

`IAXpeers` command, AMI, [691](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1530996), [731](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1612643)

IceCast server, `ICES()` application, [396](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos953395)

`ICES()` dialplan application, [396](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos953395)

`if` command, [81](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos300859), [83–84](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos305035)

`IF()` function, [611–612](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1381076)

`ifTime` command, AEL, [83–84](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos305035)

`IFTIME()` function, [612–613](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1382722)

iLBC codec, [104](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos351208), [729](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1604551)

Images

> `SEND IMAGE` command, AGI, [664](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1480543)

> `SendImage()` application, [504–505](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1167182)

`ImportVar()` dialplan application, [396–397](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos953395)

`include` statements

> `extensions.conf` vs. `extensions.ael`, [77](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos294239)

> overview of, [37–39](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos200489)

`Incomplete()` dialplan application, [398](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos957421)

`indications.conf`, [463](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1087751)

Indicators

> 1.6 advanced, [236–237](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos656856)

> Busy Lamp Field. *See* [BLF (Busy Lamp Field)](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1717075)

Inheritance, channel variables, [63–65](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos256216)

Installation, [9–23](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos131957)

Installation, Asterisk 1.4, [247–256](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos679729)

> install Asterisk, [252–256](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos687096)

> install DAHDI, [250–252](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos685037)

> install LIBPRI library, [249](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos683679)

> overview of, [9–10](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos131957), [247–249](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos679729)

Integers, size limit in variables, [62](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos252395)

interactive voice response. *See* [IVR (interactive voice response)](#Practical_As-sk_1.4_and_1.6_split_042.html_filepos1904847)

`internal-calls` context, [54](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos235650)

`internal-phones` context, [26](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos169755)

Internet Assigned Numbers Authority (IANA), port numbers, [91](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos321884)

Internet Protocol (IP), TCP, [90](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos318644)

Internet service provider (ISP), [45](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos218334)

Interrupts, choosing ISDN card, [109](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos367864)

Invalid input (`i` extension), IVR, [139–140](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos448284)

Invariant Sections of Document, GNU Free Documentation License

> combining documents, [751](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1646833)

> copying and distributing Modified Version, [750](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1643329)

> defined, [746](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1631869)

> replacing with translations, [752–753](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1649755)

IP addresses

> finding for phones, [232](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos647207)

> TCP connections, [91](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos321884)

IP (Internet Protocol), TCP, [90](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos318644)

IP telephony, latency of, [44–45](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215268)

IRC channel, website resources, [7](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos129801)

ISDN, [105–112](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos354773). *See also* [PRI (Primary Rate Interface), ISDN](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos1965577)

> BRI. *See* [BRI (basic rate interface), ISDN](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1718890)

> channels, [106](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos358095)

> choosing card, [108–111](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos364379)

> choosing phone, [4](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos119540)

> codecs, [101–105](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos344825)

> defined, [105](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos354773)

> media gateways for connections, [111–112](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos374542)

> PRI. *See* [PRI (primary rate interface), ISDN](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos1965577)

> `SetTransferCapability()`, [524–525](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1207119)

> starting Zaptel RAS, [570–571](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1297209)

ISDN clock, [112](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos377750)

ISDN-SIP gateway, [110](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos371159)

`ISNULL()` function, [613–614](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1385941)

ISO image, Asterisk 1.4 installation, [247](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos679729)

ISP (Internet service provider), [45](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos218334)

IVR (interactive voice response)

> `ExternalIVR()` dialplan application, [369–371](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos907303)

> multilevel systems, [140–141](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos450940)

> overview of, [137–138](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos443020)

> pauses, [140](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos450940)

> simplest form of, [138–140](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos444860)

> text-to-speech (TTS), [142–143](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos454530)

> timeouts, [68–69](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos273653)

### J

`j` (jump) option, [258](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos694389), [283–286](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos760452)

`JabberSend` command, AMI, [691–692](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1530996)

`JabberSend()` dialplan application, [398–399](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos957421)

`JabberStatus()` dialplan application, [399–400](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos959501)

JavaScript Object Notation (JSON), [197–198](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos586401)

`join-empty`, `queues.conf`, [163](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos506521)

Journeymen, how to use this book, [4](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos119540)

JSON (JavaScript Object Notation), [197–198](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos586401)

`jump` command, [79–81](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos298217), [140](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos450940)

### K

`KeepAlive()` dialplan application, [401](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos963856)

Kernel module `(.ko)`, [735](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1617310)

`KEYPADHASH()` function, [614–615](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1387853)

KNOPPIX Live System, [247–256](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos679729)

### L

`label, aastra.cfg`, [234](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos651700)

Labels

> `extensions.conf` vs. `extensions.ael`, [79–80](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos298217)

> using `GoTo()`, [59–60](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos244785)

`LANGUAGE()` function

> overview of, [615–617](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1389602)

> `SayAlpha()`, [496](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1147699)

> `SayNumber()`, [497–499](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1150416)

> `SayPhonetic()`, [499–500](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1156660)

> `SetLanguage()`, [521–522](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1200468)

`languageprefix` option, `asterisk.conf`, [726](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

LAST_ACK, TCP teardown, [92](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos325176)

Latency (delay)

> IP telephony and, [44–45](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215268)

> testing with `EAGI()`, [356–357](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos884594)

LCD indicators. *See* [BLF (Busy Lamp Field)](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1717075)

`leavewhenempty`, `queues.conf`, [163](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos506521)

Legal issues

> eavesdropping, [299](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos789948)

> recording conversations, [438](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1044512)

`LEN()` function, [616–617](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1392110)

LIBPRI library, [249](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos683679)

License notice, GNU Free Documentation License, [750](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1643329)

Licensee, GNU Free Documentation License, [746](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1631869)

Licensing. *See* [GNU Free Documentation License](#Practical_As-sk_1.4_and_1.6_split_042.html_filepos1879668)

`line, aastra.cfg`, [234](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos651700)

Line termination, [75](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos289802)

`ListCategories` command, AMI, [692](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1533254)

`ListCommands` command, AMI, [692–693](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1533254)

LISTEN state, sockets, [91–92](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos321884)

Local channel, [96](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos337268)

`LOCK()` function, [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

`Log()` dialplan application, [401–402](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos963856)

Log directory, IAXModem, [217](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos621282)

Log files, queues, [170–174](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos531167)

`logger.conf`, [726](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

`Login` command, AMI, [693](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1535148)

`Logoff` command, AMI, [693](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1535148)

`LookupBlacklist()` dialplan application, [402–404](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos966495)

`LookupCIDName()` dialplan application, [404–405](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos970544)

Loops, [84–86](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos306534)

### M

`macro` command, AEL, [86](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos311190)

`Macro()` dialplan application

> as deprecated, [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

> `extensions.conf` vs. `extensions.ael`, [86](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos311190)

> overview of, [405–408](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos973212)

`MacroExclusive()` dialplan application

> defined, [71](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos281786)

> as deprecated, [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

> overview of, [408–409](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos977170)

`MacroExit()` dialplan application, [409–410](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos979884)

`MacroIf()` dialplan application, [410–411](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos981819)

`MACRO_RESULT` channel variable, `Dial()`, [328](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos844986)

Macros

> defining in dialplan, [70–71](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos278723)

> example home voicemail system using, [117](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos388734)

> `extensions.conf` vs. `extensions.ael`, [86](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos311190)

> upgrading to 1.6 in AEL, [725](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1590135)

Macros, dialplan applications

> `Macro()`, [405–408](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos973212)

> `MacroExclusive()`, [408–409](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos977170)

> `MacroExit()`, [409–410](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos979884)

> `MacroIf()`, [410–411](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos981819)

> overview of, [259](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos698046)

Mail Transfer Agent (MTA), configuring voicemail, [18](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos156125)

`mailbox`, `VoiceMail()` command, [122](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos393727)

`mailbox`, `VoiceMailMain()` command, [123](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos397413)

`MailboxCount` command, AMI, [694](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1537448)

Mailboxes

> configuring in `voicemail.conf`, [131–132](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos425599)

> getting number of messages with AJAM, [196–197](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos584396)

> getting number of messages with PHP, [193–195](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos578978)

`mailboxExists()` dialplan application, [411–412](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos984014)

`MailboxStatus` command, AMI, [695](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1538587)

`mailcmd`, `voicemail.conf`, [127](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos410130)

Mailing lists, Digium, [7](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos129801)

`make config` command, [251–252](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos686317), [255–256](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos690282)

`make install` command, [254–255](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos689032)

`make menu select` command, [254](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos689032)

`make samples` command, [255](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos690282)

`manager show command`, [189–190](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos572624)

`manager show commands`, [189](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos572624)

`manager.conf`, AMI, [186–189](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos563907)

Manufacturers, ISDN card, [110–111](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos371159)

`marryme.gsm` file, [138](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos444860)

Massive Multiauthor Collaboration Site (MMC Site), relicensing, [754–755](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1654847)

`Math()` dialplan application, [413](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos987183)

`MATH()` function

> overview of, [617–618](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1393507)

> replacing `Math()` dialplan application, [413](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos987183)

> upgrading from 1.4 to 1.6, [726](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

`maxDigits`, `Authenticate()`, [283–286](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos760452)

`maxDuration`, `Record()`, [486](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1126673)

`maxgreet`, `voicemail.conf`, [128](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos414275)

maximum segment lifetime (MSL), TCP, [92](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos325176)

`maxlen`, `queues.conf`, [162](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos501680)

`maxlogins`, `voicemail.conf`, [128](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos414275)

`maxmessage`, `voicemail.conf`, [128](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos414275), [727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

`maxmsg`, `voicemail.conf`, [128](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos414275)

`maxretries`, `PrivacyManager()`, [464–467](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1089698)

`MaxRetries,` call files, [185](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos559338)

`maxsecs` value, voicemail, [727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

`maxSilence`, `Record()`, [486](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1126673)

`maxsilence,voicemail.conf`, [128](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos414275)

`MD5()` dialplan application, [413–414](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos987183)

`MD5()` function, [413–414](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos987183), [618](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1396102)

`MD5Check()` dialplan application, [414–415](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos989720)

`MeetMe` commands, CLI, [418–423](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1004725)

`MeetMe()` dialplan application

> conferencing using, [180](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos551711)

> monitoring status using hints, [242](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos669776)

> overview of, [415–417](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos992113)

`MeetMeAdmin()` dialplan application, [423–425](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1009831)

`MeetMeChannelAdmin()` dialplan application, [425–426](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1014336)

`meetme.conf`, [180](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos551711)

`MeetMeCount()` dialplan application, [180](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos551711), [426–427](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1016436)

`MeetmeList` command, AMI, [695–696](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1538587)

`MeetmeMute` command, AMI, [696](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1540326)

`MeetmeUnmute` command, AMI, [696–697](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1540326)

`member`, `queues.conf`, [164–165](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos510671)

`memberdelay`, `queues.conf`, [164](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos510671)

Memory, Asterisk requirements, [48](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos228287)

MGCP channel, [96](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos337268)

`Milliwatt()` dialplan application, [428–429](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1019892)

Mini-Voicemail system

> deleting message, [430–431](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1024183)

> e-mail notification of new messages, [432–433](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1029487)

> play back greeting, [431–432](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1026296)

> record voicemail, [433–434](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1031429)

> recording messages, [429–430](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1021488)

`MinivmAccMess()` dialplan application, [429–430](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1021488)

`MinivmDelete()` dialplan application, [430–431](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1024183)

`MinivmGreet()` dialplan application, [431–432](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1026296)

`MinivmNotify()` dialplan application, [432–433](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1029487)

`MinivmRecord()` dialplan application, [433–434](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1031429)

`minlength`, `PrivacyManager()`, [464–467](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1089698)

`minmessage`, `voicemail.conf`, [128](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos414275), [727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

`minsecs` value, voicemail, [727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

mISDN

> defined, [96](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos337268)

> HFC-based BRI cards used with, [111](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos374542)

> moving from Zaptel to DAHDI and, [737](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1620661)

`MixMonitor()` dialplan application

> overview of, [434–436](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1033427)

> `StopMixMonitor()`, [536–537](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1233523)

`${MIXMONITOR_FILENAME}`, [435](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1035762)

`mkdir/etc/iaxmodem`, [215](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos615490)

MMC Site (Massive Multiauthor Collaboration Site), relicensing, [754–755](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1654847)

Modified Version of Document, GNU Free Documentation License

> copying and distributing, [749–751](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1640433)

> defined, [746](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1631869)

> translations, [752–753](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1649755)

`ModuleCheck` command, AMI, [697](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1542445)

`ModuleLoad` command, AMI, [697–698](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1542445)

Modules

> defining for dialplan applications, [257](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692094)

> renaming Zaptel as DAHDI, [736](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1619023)

`[modules] section, modules.conf`, [257](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692094)

`modules.conf`, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934)

`Monitor` command, AMI, [698](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1544153)

`Monitor()` dialplan application

> `ChangeMonitor()`, [293–294](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos776284)

> overview of, [436–440](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1037985)

`monitor-format`, `queues.conf`, [162–163](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos501680)

`monitor-join`, `queues.conf`, [163](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos506521)

`${MONITOR_EXEC}` variable, [437–440](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1041230)

Monitoring

> dialplan applications for. *See* [Recording and monitoring, dialplan applications](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos1982644)

> processor loads on server, [47](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos225320)

`Morsecode()` dialplan application, [440–441](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1046762)

MP3 music, [158–159](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos486769)

`MP3Player()` dialplan application, [441–442](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1048685)

`mpg123`, [441](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1048685)

`mpg321`, [441](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1048685)

`msdstrip`, channel drivers, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934)

`MSet()` dialplan application, [442–443](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1050918)

MSL (maximum segment lifetime), TCP, [92](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos325176)

MTA (Mail Transfer Agent), configuring voicemail, [18](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos156125)

Multilevel inheritance, channel variables, [64–65](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos258772)

Multilevel IVR systems, [140–141](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos450940)

Multiplexing (muxing), UDP, [95](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos334030)

Music and sound output, dialplan applications

> `Background()`, [283–286](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos760452)

> `BackgroundDetect()`, [290–291](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos770151)

> `ControlPlayback()`, [309–311](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos805839)

> `DateTime()`, [317–318](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos820811)

> `Echo()`, [356–357](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos884594)

> `Festival()`, [372–374](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos910236)

> `Milliwatt()`, [428–429](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1019892)

> `MP3Player()`, [441–442](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1048685)

> `MusiconHold()`, [443–445](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1053474)

> `NBScat()`, [445–446](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1056906)

> overview of, [261](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos708602)

> `Playback()`, [461–463](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1084746)

> `Playtones()`, [463–464](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1087751)

> `Progress()`, [467–468](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1094672)

> `SayAlpha()`, [496](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1147699)

> `SayDigits()`, [496–497](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1147699)

> `SayNumber()`, [497–499](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1150416)

> `SayPhonetic()`, [499–500](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1156660)

> `SayUnixTime()`, [500–501](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1158736)

> `SetMusicOnHold()`, [522–523](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1203356)

> `StopPlaytones()`, [539–540](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1239397)

Music-on-Hold

> `SetMusicOnHold()`, [522–523](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1203356)

> `StartMusicOnHold()`, [535–536](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1231426)

> `StopMusicOnHold()`, [538–539](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1237142)

> `WaitMusicOnHold()`, [563–564](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1284555)

`MUSICCLASS()` function, [443](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1053474), [619](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1397517)

`musiconhold, agents.conf`, [167](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos522834)

`MusicOnHold()` dialplan application, [443–445](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1053474), [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

`musiconhold`, `queues.conf`, [160](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos493721)

`musiconhold.conf`

> defined, [155](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos478319)

> defining Music-on-Hold class in, [328](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos844986)

> keeping hold music legal, [157](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos483985)

> setting up, [157–159](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos483985)

`mv` operation, call files, [184](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos556023)

MWI (message waiting indication), upgrading voicemail to 1.6, [727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

`mxml`, voicemail with AJAM, [197](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos586401)

`myphones` context, `dialplan show`, [33](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos191875)

MySQL, importing queue log into, [172–174](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos538929)

### N

[N] dialplan pattern, [31](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos185045)

*n* priority, [29](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos181396)

Naming conventions

> contexts, [26](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos169755)

> dialplan functions, [575](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1304314)

> variables, [61–62](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos249331)

Nano text editor, [11](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos136368)

NANP (North American Numbering Plan)

> emergency number for, [43](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos214482)

> using overlay dialplans, [66–67](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos266838)

NAT (Network Address Translation), IAX vs. SIP, [97](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos341191)

NATO phonetic alphabet, [499–500](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1156660), [662–663](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1476861)

NBS (Network Broadcast Sound) channel, [96](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos337268)

`NBScat()` dialplan application, [445–446](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1056906)

Network Address Translation (NAT), IAX vs. SIP, [97](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos341191)

Network Broadcast Sound (NBS) channel, [96](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos337268)

Network, choosing, [44–46](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215268)

Network protocols, [89–90](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos316886), [94–95](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos330257)

Network Time Protocol (NTP), Asterisk 1.4 installation, [248](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos681742)

New Zealand, legalizing hold music in, [157](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos483985)

9-1-1 emergency number, NANP, [43](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos214482)

9-9-9 emergency number, UK, [43](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos214482)

`noanswer` option, `Background()`, [287](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos766517)

`NOANSWER` variable, `Dial()`, [330](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos854267)

`NOOP` command, AGI, [656–657](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1465422)

`NoOp()` dialplan application

> defined, [28](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos176857)

> overview of, [446–447](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1059176)

> printing variable values with, [58](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos241410)

North American Numbering Plan (NANP)

> emergency number for, [43](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos214482)

> using overlay dialplans, [66–67](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos266838)

`NOTIFY` message, [231](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos644855)

NTP (Network Time Protocol), Asterisk 1.4 installation, [248](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos681742)

Numbering plan

> business telephone system case study, [43](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos214482), [52–54](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos232968)

> overlay dialplans, [66–67](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos266838)

Numbers

> looking up with `EnumLookup()`, [358–359](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos887594)

> returning randomly generated with `RAND()`, [624–625](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1407138)

> `SAY NUMBER` command, AGI, [662](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1476861)

> saying with `SayNumber()`, [497–499](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1150416)

> upgrading from 1.4 to 1.6, [726](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

### O

`o` option, programming dialplan, [68](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos273653)

`ODBCFinish()` dialplan application, [448](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1063380)

`ODBC_SQL()` function, [620](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1399448)

`ODBC_USER_DATABASE()` function, [620–621](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1399448)

1-1-2 emergency number, Europe, [43](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos214482)

Opaque copies of Document, GNU Free Documentation License, [749](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1640433)

Options

> `Authenticate()`, [283–286](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos760452)

> `Background()`, [287–290](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos766517)

> `ChanSpy()`, [299–300](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos789948)

> `Dial()`, [327–330](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos840494)

> `ExtenSpy()`, [365–366](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos900982)

> `MeetMe()`, [415–417](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos992113)

> `MixMonitor()`, [434–435](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1033427)

> `Monitor()`, [436–437](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1037985)

> `Queue()`, [468–469](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1096955)

> `Record()`, [486–488](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1126673)

> `SayUnixTime()`, [500–501](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1158736)

> `SMS()`, [529](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1218501)

> `Zapateller()`, [567–568](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1291662)

Order, pattern matching, [34–37](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos193924)

`Originate` command, AMI, [698–699](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1544153), [731](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1612643)

overlay dialplans, [66–67](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos266838)

`owner`, `/etc/iaxmodem/ttyIAXO`, [215](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos615490)

### P

Packets

> connecting to AMI, [189](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos572624)

> TCP connections, [91–94](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos321884)

> UDP characteristics, [95](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos334030)

`Page()` dialplan application, [448–450](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1063380)

`pagerbody`, `voicemail.conf`, [128](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos414275)

`pagerfromstring`, `voicemail.conf`, [128](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos414275)

`pagersubject`, `voicemail.conf`, [128](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos414275)

Parameter delimiter, used in this book, [258](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos694389)

`Park` command, AMI, [699–700](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1545753)

`Park()` dialplan application, [450–452](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1067981)

`ParkAndAnnounce()` dialplan application, [452–454](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1070682)

`ParkedCall()` dialplan application, [454–455](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1073907)

`ParkedCalls` command, AMI, [700](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1547180)

`parkedcalls` context, [32–33](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos189215), [176–177](#Practical_As-sk_1.4_and_1.6_split_021.html_filepos546032)

Passwords

> with `Authenticate()`, [283–286](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos760452)

> calling PSTN, [21](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos162120)

> `DISA()` application option, [347–351](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos872992)

> saving in `voicemail.conf`, [135](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos440705)

> using strong, [54](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos235650)

Pattern matching, [29–37](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos181396)

> elements, [31](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos185045)

> `extensions.conf` vs. `extensions.ael`, [83](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos305035)

> order, [34–37](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos193924)

> overview of, [29–30](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos181396)

> testing using `dialplan show`, [32–34](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos189215)

Patterns, regular expressions as, [30](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos183949)

`pausechar` key, `ControlPlayback()`, [309–310](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos805839)

`PauseMonitor` command, AMI, [700–701](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1547180), [713](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1572810)

`PauseMonitor()` dialplan application, [456](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1076724), [546–547](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1254217)

`PauseQueueMember()` dialplan application, [456–458](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1076724), [547–548](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1256128)

pauses, IVR, [140](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos450940)

Payload, TCP header, [93](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos328611)

`pbxskip`, `voicemail.conf`, [125](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos401738)

PDU (protocol data unit), [93](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos328611)

`peername /etc/iaxmodem/ttyIAXO`, [216](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos617821)

Peers, IP connections, [97](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos341191)

Performance

> Asterisk database, [145–146](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos459042)

> monitoring processor loads on server, [47–48](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos225320)

> preventing latency, [44–46](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215268)

`periodic-announce-frequency`, `queues.conf`, [162](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos501680)

Perl, using AGI with, [203–206](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos596240)

Phone channel, [96](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos337268)

Phones, choosing, [3–4](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos116052)

PHP, StarAstAPI for, [192–195](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos575692)

PHP, using AGI with, [206–209](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos603283)

Pickup

> configuring group, [240–242](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos668284)

> configuring phones, [238–240](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos662667)

> `extensions.conf` for, [238](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos662667)

> overview of, [237](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos660150)

`Pickup()` dialplan application, [238](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos662667), [458–460](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1080907)

`PickupChan()` dialplan application, [460–461](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1083317)

`pickupgroup`, implementing BLF, [228](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos637762)

`PICKUPMARK, Pickup()`, [241–242](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos668727)

`ping` command, accessing AJAM with AJAX, [198](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos587667)

`Ping` command, AMI, [701](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1549263)

Pipe (|) delimiter

> calling macros, [70](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos278723)

> upgrades from 1.4 to 1.6, [726](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

Plain text, AJAM, [196](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos584396)

Playback

> `ControlPlayback()` application, [309–311](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos805839)

> simple IVR, [138](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos444860)

`Playback()` dialplan application

> defined, [28](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos176857)

> extension priority, [12](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos139227)

> overview of, [461–463](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1084746)

`PlayDTMF` command, AMI, [702](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1550854)

`Playtones()` dialplan application, [293](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos776284), [463–464](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1087751)

`.plist` configuration file format, [258](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos694389)

Point-to-Point Protocol (PPP), [93–94](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos328611)

Polarity, and analog telephony, [113–114](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos380837)

`pollfreq`, upgrading to 1.6, [727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

`pollmailboxes`, upgrading to 1.6, [727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

Polycom phones, [234–236](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos651700)

`port`, `/etc/iaxmodem/ttyIAXO`, [216](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos617821)

Port numbers

> AMI connections, [187](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos565613)

> installing Asterisk on same machine as SIP phone, [13–14](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos142885)

> TCP connections, [91](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos321884)

Pound key (#) dialplan pattern, [31](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos185045)

PPP (Point-to-Point Protocol), [93–94](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos328611)

Predial digits, VoIP providers, [22](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos163371)

Prerolled Asterisk systems, [42](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos211266)

Preserve the Title of Entitled XYZ section, GNU Free Documentation License

> copying and distributing Modified Version, [750](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1643329)

> defined, [747](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1634621)

PRI (primary rate interface), ISDN

> choosing ISDN card, [108–111](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos364379)

> `DAHDISendKeypadFacility()` and, [316–317](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos818957)

> overview of, [107–108](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos361159)

> support in DAHDI, [738–739](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1624026)

> `ZapSendKeypadFacility()` and, [572–573](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1301274)

PRI stack, Asterisk 1.4 installation, [249](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos683679)

Primary Rate Interface. *See* [PRI (primary rate interface), ISDN](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos1965577)

Printing variables, [58](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos241410)

Priorities

> defined, [27](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos172669)

> `extensions.conf` vs. `extensions.ael`, [75–76](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos289802)

> introduction to, [12](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos139227)

> overview of, [28–29](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos176857)

> pattern matching order based on, [34–37](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos193924)

`Priority,` call files, [185](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos559338)

Priority jumping

> as deprecated, [70](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos278723)

> enabling, [258](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos694389)

Privacy issues, eavesdropping and, [299](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos789948)

Privacy Manager, `Dial()` options, [329–330](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos849385)

`Privacy()`, upgrading to 1.6, [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

`privacy.conf`, [464–467](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1089698)

`PrivacyManager()` dialplan application, [464–467](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1089698)

`Proceeding()` dialplan application, [467](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1094672)

program structure, [58](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos241410)

`Progress()` dialplan application, [467–468](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1094672)

protocol data unit (PDU), [93](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos328611)

Protocols

> friends, [97](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos341191)

> IAX vs. SIP, [97–99](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos341191)

> peers, [97](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos341191)

> users, [97](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos341191)

Protocols, network, [90–96](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos318644)

> overview of, [89–90](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos316886)

> TCP, [90–94](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos318644)

> UDP, [94–96](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos330257)

Providers, SIP, [21–22](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos162120)

PSTN number (also DID or DN), [23](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos166131)

PSTN (Public Switched Telephone Network)

> calling, [21–22](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos162120)

> ISDN standard for. *See* [ISDN](#Practical_As-sk_1.4_and_1.6_split_042.html_filepos1902488)

> taking calls from, [23](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos166131)

> using `s` extension, [69–70](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos276361)

> from Zaptel to DAHDI. *See* [DAHDI (Digium Asterisk Hardware Device Interface)](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1761545)

Public Switched Telephone Network. *See* [PSTN (Public Switched Telephone Network)](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos1970946)

Publisher of Document, GNU Free Documentation License

> copying and distributing Modified Version, [749](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1640433), [751](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1646833)

> defined, [747](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1634621)

### Q

QoS (quality of service), [45](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos218334)

`QueueAdd` command, AMI, [702](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1550854)

`QUEUEAGENTCOUNT()` function, [621–622](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1401122)

`queue_log`, [170–174](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos531167)

`QueueLog` command, AMI, [703](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1552930)

`QUEUEMEMBER()` function, [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

`QUEUEMEMBERCOUNT()` function, [622–623](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1403202), [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

`QUEUEMEMBERLIST()` function, [623–624](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1405303)

QueueMetrics, [172](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos538929), [174](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos543417)

`QueueParse` command, AMI, [703](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1552930)

`QueuePenalty` command, AMI, [703–704](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1552930)

`QueueRemove` command, AMI, [704](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1555416)

`QueueRule` command, AMI, [704](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1555416)

Queues, [155–174](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos478319)

> `agents.conf`, [166–168](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos519005)

> announcement sound files, [165–166](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos515133)

> extension for testing hold music, [156–157](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos480722)

> `extensions.conf`, [168–170](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos527307)

> log file, [170–174](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos531167)

> members vs. callers, [156](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos480722)

> `musiconhold.conf`, [157–159](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos483985)

> overview of, [155–156](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos478319)

> `queues.conf`, [160–165](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos493721)

Queues (call center functions), dialplan applications

> `AddQueueMember()`, [264–266](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos723850)

> `AgentCallbackLogin()`, [267–268](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos729872)

> `AgentLogin()`, [268–269](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos732316)

> `AgentMonitorOutgoing()`, [270–272](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos735731)

> overview of, [263](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos719381)

> `ParkAndAnnounce()`, [452–454](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1070682)

> `ParkedCall()`, [454–455](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1073907)

> `PauseQueueMember()`, [456–458](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1076724)

> `Queue()`, [468–473](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1096955)

> `QueueLog()`, [473](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1105266)

> `RemoveQueueMember()`, [489–490](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1133659)

> `UnpauseQueueMember()`, [547–548](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1256128)

`Queues` command, AMI, [704–705](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1555416)

`queues.conf`, [155–156](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos478319), [160–165](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos493721)

`QueueStatus` command, AMI, [705](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1557856)

`QueueSummary` command, AMI, [705–706](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1557856)

`QUOTE()` function, [624](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1407138)

Quotes, upgrading to 1.6, [726](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

### R

RAID, software vs. hardware, [48](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos228287)

RAM

> Asterisk requirements, [48](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos228287)

> recording many conversations to, [438](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1044512)

`RAND()` function, [84](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos306534), [624–625](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1407138)

`random()` command, [84](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos306534)

`Random()` dialplan application, [475–476](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1108791)

RDNIS number, setting, [523–524](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1205240)

`Read()`, upgrading to 1.6, [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

Reader contributions/feedback, for this book, [5](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos122613)

`ReadExten()` dialplan application, [480](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1115769)

`ReadFile()` dialplan application, [481](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1117321)

Reading values from database, [146–148](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos460765)

`RealTime()` dialplan application, [482–483](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1119019)

`RealTimeUpdate()` dialplan application, [483–484](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1121980)

`RECEIVE CHAR` command, AGI, [657](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1467863)

`RECEIVE TEXT` command, AGI, [657–658](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1467863)

`ReceiveFax()` dialplan application, [484–486](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1123801)

`Record()` dialplan application, [486–488](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1126673)

`RECORD FILE` command, AGI, [658](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1469603)

`recordagentcalls`, `agents.conf`, [167](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos522834)

`recordformat`, `agents.conf`, [167](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos522834)

Recording and monitoring, dialplan applications

> `AgentMonitorOutgoing()`, [270–272](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos735731)

> `ChangeMonitor()`, [293–294](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos776284)

> `ChanSpy()`, [299–305](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos789948)

> `Dial()`. *See* [`Dial()` dialplan application](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1775300)

> `Dictate()`, [341–342](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos862331)

> `ExtenSpy()`, [365–369](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos900982)

> `MixMonitor()`, [434–436](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1033427)

> `Monitor()`, [436–440](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1037985)

> overview of, [261](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos708602)

> `PauseMonitor()`, [456](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1076724)

> `Record()`, [486–488](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1126673)

> `StopMixMonitor()`, [536–537](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1233523)

> `StopMonitor()`, [537–538](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1235291)

> `UnpauseMonitor()`, [546–547](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1254217)

> `ZapBarge()`, [568–569](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1294162)

> `ZapScan()`, [571–572](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1299680)

`Redirect` command, AMI, [706](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1560184)

`refresh /etc/iaxmodem/ttyIAXO`, [216](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos617821)

`REGEX()` function, [626–627](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1410935)

Relicensing, GNU Free Documentation License, [754–755](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1654847)

`Reload` command, AMI, [706–707](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1560184)

`reload now command`, [27](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos172669)

`RemoveQueueMember()` dialplan application, [489–490](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1133659)

`reportholdtime`, `queues.conf`, [164](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos510671)

Reporting errors, [5](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos122613)

`res_agi=1.4`, [726](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

Reserved characters, and variables, [62](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos252395)

`ResetCDR()` dialplan application, [490–491](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1135855)

Resources, additional

> Adhearsion, [209](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos607013)

> `AgentCallbackLogin()`, [268](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos732316)

> AJAM demo, [198](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos587667)

> AMI events, [188](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos568686)

> APIs for AMI in variety of languages, [192](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos575692)

> Asterisk bandwidth calculator, [46](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos221706)

> Asterisk RealTime Architecture, [27](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos172669)

> Cepstral TTS installation, [142–143](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos454530)

> configuration template examples, [722](#Practical_As-sk_1.4_and_1.6_split_036.html_filepos1587241)

> IAXModem source code, [214](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos613850)

> legalizing hold music, [157](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos483985)

> most current version of this book, [5](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos122613)

> MP3 file conversion into compatible format, [158–159](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos486769)

> MP3 music support, [158](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos486769)

> Nagios server monitoring tool, [47](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos225320)

> overview of, [6–7](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos126171)

> queue log analysis tools, [172](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos538929)

> revisions of GNU Free Documentation License, [754](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1654847)

> Ruby on Rails, [209](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos607013)

> Speech Synthesis Markup Language (SSML), [143](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos457634)

> StarAstAPI for PHP, [192](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos575692)

> testing TTS engines, [142](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos454530)

`Response` packets, AMI, [188](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos568686)

Response timeouts, [640–642](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1437424)

`ResponseTimeout()` dialplan application, [491–492](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1137453)

`retry`, `queues.conf`, [161](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos497987)

`RetryDial()` dialplan application, [492–494](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1139673)

`RetryTime`, call files, [185](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos559338)

`Return()` app call, for macros, [725](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1590135)

Return code of 0, [258](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos694389)

Return code of –1, [258](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos694389)

`Return()` dialplan application, [494–495](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1143098), [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

Revisions, GNU Free Documentation License future, [754](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1654847)

`rewchar` key, `ControlPlayback()`, [309–310](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos805839)

Rights administration

> with contexts, [18–20](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos156125)

> creating AMI user, [187](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos565613)

Ring, analog telephony polarity, [113–114](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos380837)

`Ringing()` dialplan application, [495](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1145189)

`ringinuse`, `queues.conf`, [164](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos510671)

`rotatestrategy`, `logger.conf`, [726](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

`rotatetimestamp`, `logger.conf`, [726](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

`roundrobin` method, `queues.conf`, [160–161](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos493721)

`rrmemory` method, `queues.conf`, [160–161](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos493721)

Ruby, using AGI with, [209–210](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos607013)

`RxFax()` command, [485](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1125377)

### S

`s` option, programming dialplans, [69–70](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos276361)

Sangoma, ISDN cards, [111](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos374542)

`savecallsin, agents.conf`, [168](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos527307)

`SAY ALPHA` command, AGI, [659](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1471279)

`SAY DATE` command, AGI, [659–660](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1471279)

`SAY DIGITS` command, AGI, [661–662](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1474890)

`SAY NUMBER` command, AGI, [662](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1476861)

`SAY PHONETIC` command, AGI, [662–663](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1476861)

`SAY TIME` command, AGI, [663–664](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1478574)

`SayAlpha()` dialplan application, [496](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1147699)

`saycid`, `voicemail.conf`, [128](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos414275)

`SAYDATETIME` command, AGI, [660–661](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1473205)

`SayDigits()` dialplan application, [496–497](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1147699)

`SayNumber()` dialplan application, [497–499](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1150416)

`SayPhonetic()` dialplan application, [499–500](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1156660)

`SayUnixTime()` dialplan application, [317](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos820811), [500–501](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1158736)

Scripts, dialplan applications

> `AGI()`, [272–275](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos740357)

> `DeadAGI()`, [322–323](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos831104)

> `DumpChan()`, [351–352](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos877151)

> `EAGI()`, [353–354](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos880515)

> `ExternalIVR()`, [369–371](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos907303)

> `Log()`, [401–402](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos963856)

> `Macro()`, [405–408](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos973212)

> `NoOp()`, [446–447](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1059176)

> overview of, [262](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos714427)

> `Read()`, [476–479](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1110679)

> `System()`, [540–541](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1241527)

> `TrySystem()`, [544–545](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1249969)

> `UserEvent()`, [548–550](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1258348)

> `Verbose()`, [550–551](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1261053)

`searchcontexts`, `voicemail.conf`, [128](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos414275)

Secondary Section of Document, GNU Free Documentation License, [746](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1631869)

`secret /etc/iaxmodem/ttyiaxo`, [216](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos617821)

Security

> `DISA()` application risk, [347](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos872992)

> server room, [44](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215268)

Semicolon(;)

> AEL commands, [75](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos289802)

> indicating comments, [16](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos151991), [76](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos292069)

`SEND IMAGE` command, AGI, [664](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1480543)

`SEND TEXT` command, AGI, [664–665](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1480543)

`SendDTMF()` dialplan application, [502–503](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1163203)

`SendFAX()` dialplan application, [503–504](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1165458)

`SendImage()` dialplan application, [504–505](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1167182)

`SendText` command, AMI, [707](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1562078)

`SendText()` dialplan application, [505–506](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1169269)

`SendURL()` dialplan application, [507–509](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1172652)

Server

> choosing hardware, [46–48](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos221706)

> installing Asterisk on, [9–10](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos131957)

`server /etc/iaxmodem/ttyIAXO`, [216](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos617821)

`serveremail, voicemail.conf`, [126](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos405883)

`servicelevel`, `queues.conf`, [161](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos497987)

`SET AUTOHANGUP` command, AGI, [665](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1482278)

`SET CALLERID` command, AGI, [665–666](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1482278)

`Set()` command

> creating and changing variables, [58–59](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos241410)

> defining variables, [63](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos256216)

> expression handling in AEL, [76](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos292069)

> setting timeout value, [69](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos276361)

`SET CONTEXT` command, AGI, [666](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1484262)

`Set()` dialplan application

> overview of, [512–513](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1179336)

> `SET()` function vs., [512–513](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1179336)

> upgrading from 1.4 to 1.6, [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

`SET EXTENSION` command, AGI, [667](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1486714)

`SET()` function, [627–628](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1412907)

`SET MUSIC` command, AGI, [667–668](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1486714)

`SET PRIORITY` command, AGI, [668](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1488938)

`Set()` statements, [442](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1050918)

`SET VARIABLE` command, AGI, [669](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1491061)

`set verbose 3`, [447](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1061462)

`set verbose 5`, [202](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos592035)

`SetAccount()` dialplan application, [512–513](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1179336)

`SetAMAFlags()` dialplan application, [513–514](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1181134)

`SetCallerID()` dialplan application, [514–515](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1183766), [582](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1320855)

`SetCallerPres()` dialplan application, [515–516](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1186143)

`SetCallerPres()` dialplan application, [727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

`SetCDRUserField` command, AMI, [707](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1562078)

`SetCDRUserField()` dialplan application, [516–517](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1190138)

`SetCIDName()` dialplan application, [517–518](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1191918), [582](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1320855)

`SetGlobalVar()` dialplan application, [518–519](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1193434)

`SetGroup()` dialplan application, [521](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1200468)

`SetLanguage()` dialplan application, [521–522](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1200468)

`SetMusicOnHold()` dialplan application, [522–523](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1203356), [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

`SetRDNIS()` dialplan application, [523–524](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1205240)

`SetTransferCapability()` dialplan application, [524–525](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1207119)

`SetVar` command, AMI, [708](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1564247)

`SetVar()` dialplan application, [526](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1211304)

`SHA1()` function, [628](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1414484)

Shell

> executing commands with `System()`, [540–541](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1241527)

> renaming Zaptel as DAHDI, [736](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1619023)

Short Message System (SMS) messages, managing exchange of, [529–532](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1218501)

`show 23@` context, `dialplan show`, [33–34](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos191875)

`show application MeetMe` command, [180](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos551711)

`show application xyz` command, [257](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692094)

`show applications` command, [257](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos692094)

`show dialplan` command, [36](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos198477)

`show function FUNCTIONNAME`, [576](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1306437)

`show function QUEUEMEMBER`, [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

`show functions`, [576](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1306437)

`show manager command`, [189–190](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos572624)

`show manager commands`, [189](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos572624)

`ShowDialPlan` command, AMI, [708](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1564247)

`shutdown -r now`, [248](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos681742)

`SIGHUP` signal, DeadAGI, [322–325](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos831104)

`SIGPIPE` message, [172](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos538929)

`SIGPIPE` signal, DeadAGI, [323](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos833819)

`silencethreshold`, `voicemail.conf`, [128](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos414275)

Single-level inheritance, channel variables, [63–64](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos256216)

SIP

> choosing IAX vs., [97–99](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos341191), [741–743](#Practical_As-sk_1.4_and_1.6_split_039.html_filepos1629188)

> defined, [96–97](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos337268)

> upgrading driver from 1.4 to 1.6, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934)

`SIP/2000`, [184](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos556023)

SIP, dialplan applications

> defined, [262](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos714427)

> `SIPAddHeader()`, [526–527](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1211304)

> `SIPdtmfMode()`, [527–528](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1214103)

> `SIPGetHeader()`, [528–529](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1216089)

SIP phones

> building minimal phone system, [16–18](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos151991)

> business telephone case study, [44–48](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215268)

> calling “Hello World,” [13–16](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos142885)

> calling PSTN, [21–22](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos162120)

> choosing, [3](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos116052)

> choosing provider, [3](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos116052)

> installing Asterisk on same machine as, [13–14](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos142885)

> rates charged by providers, [22](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos163371)

> rights administration with contexts, [18–20](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos156125)

> taking calls from PSTN, [23](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos166131)

`sip show subscriptions`, [236–237](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos656856)

`SIPAddHeader()` dialplan application, [526–527](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1211304)

`SIPCHANINFO()` function, [629–630](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1416373)

`sip.conf`

> business telephone system case study, [49](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos231272)

> calling “Hello World” with SIP phone, [14](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos145224)

> calling PSTN, [21](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos162120)

> configuring codecs, [103](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos349293)

> configuring two SIP phones, [16](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos151991)

> implementing BLF, [228](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos637762)

> rights administration with contexts, [18–20](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos156125)

> upgrading channel drivers to 1.6, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934)

> using templates, [721–723](#Practical_As-sk_1.4_and_1.6_split_036.html_filepos1586621)

`SIPdtmfMode()` dialplan application, [527–528](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1214103)

`SIPGetHeader()` dialplan application, [528–529](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1216089)

`SIP_HEADER()` function, [528](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1216089), [633–634](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1425449)

`SIPnotify` command, AMI, [709](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1566145)

`SIPpeers` command, AMI, [709–710](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1566145)

`SIPqualifypeer` command, AMI, [710](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1568145)

`SIPshowpeer` command, AMI, [710–711](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1568145)

`SIPshowregistry` command, AMI, [711](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1569615)

`skip` option

> `Background()`, [287](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos766517)

> `Playback()`, [461–463](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1084746)

`skipms`, `ControlPlayback()`, [309–310](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos805839)

`skipms`, `voicemail.conf`, [128](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos414275)

Skype, using ILBC codec, [104](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos351208)

`SMS()` dialplan application, [529–532](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1218501)

SMS (Short Message System) messages, managing exchange of, [529–532](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1218501)

Sockets, TCP connections, [91–93](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos321884)

`SoftHangup()` dialplan application, [532–533](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1226381)

Software RAID, burdening CPU, [48](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos228287)

`Sort()` dialplan application, [534](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1228942)

`SORT()` function, [634–635](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1426934)

Sound files, layout for non-English sounds in 1.6, [726](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

Sound output. *See* [Music and sound output, dialplan applications](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos1935564)

Soundpoint IP 501, BLF on, [234–236](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos651700)

Source code

> installing Asterisk from, [10](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos133735)

> installing IAXModem, [214](#Practical_As-sk_1.4_and_1.6_split_025.html_filepos613850)

sox, [158–159](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos486769)

sox package, [437](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1041230)

soxmix, [437](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1041230)

Speech Synthesis Markup Language (SSML), [143](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos457634)

Spencer, Mark, [98–99](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos344119)

`[s|p|g#]`, `VoiceMail()` command, [122](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos393727)

Square brackets [ ], macros, [70](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos278723)

SSH server, Asterisk 1.4 installation, [247–248](#Practical_As-sk_1.4_and_1.6_split_027.html_filepos679729)

SSML (Speech Synthesis Markup Language), [143](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos457634)

`StackPop()` dialplan application, [534–535](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1228942)

standard error (STDERR), [203–204](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos596240)

standard input (STDIN), [201–202](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos590492), [204](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos599360)

standard out (STDOUT), [202](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos592035)

StarAstAPI for PHP, [192–195](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos575692)

Starting Asterisk, [11](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos136368)

`StartMusicOnHold()` dialplan application, [535–536](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1231426)

`STAT()` function, [635–636](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1428458)

States, Busy Lamp Field indicators, [227](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos635655)

`Status` command, AMI, [712](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1571127)

STDERR (standard error), [203–204](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos596240)

STDIN (standard input), [201–202](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos590492), [204](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos599360)

STDOUT (standard out), [202](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos592035)

`stop now` command, [13](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos142885)

`stopchar` key, `ControlPlayback()`, [309–310](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos805839)

`StopMixMonitor()` dialplan application, [536–537](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1233523)

`StopMonitor` command, AMI, [712–713](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1571127)

`StopMonitor()` dialplan application, [436](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1037985), [438–439](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1044512), [537–538](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1235291)

`StopMusicOnHold()` dialplan application, [538–539](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1237142)

`StopPlaytones()` dialplan application, [539–540](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1239397)

`strategy`, `queues.conf`, [160–161](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos493721)

`STREAM FILE` command, AGI, [669–670](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1491061)

Streaming data, using UDP, [90](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos318644)

`STRFTIME()` function, [637–638](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1433473)

String variables, [62](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos252395), [66](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos266838)

Strings

> quoting with `QUOTE()`, [624](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1407138)

> returning length of using `LEN()`, [616–617](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1392110)

> spelling with `SayAlpha()`, [496](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1147699)

> spelling with `SayPhonetic()`, [499–500](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1156660)

`STRPTIME()` function, [638–639](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1435345)

`SUBSCRIBE` message, [231](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos644855)

`subscribecontext`, BLF, [228](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos637762)

Subscriptions, [231](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos644855)

Substrings, manipulating variables, [66](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos266838)

`[support]` section, `queues.conf`, [160–165](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos493721)

`switch` command, [82–83](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos302897)

SYN packet, TCP connection, [92](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos325176)

Synchronous data streams, and IP telephony, [44–45](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215268)

System channel variables, [65](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos262382)

`System()` command, [373](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos913277)

`System()` dialplan application, [540–541](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1241527), [544–545](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1249969)

System shell, database access from, [149](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos471433)

System variables, [59](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos244785)

### T

`t` option, programming dialplan, [68–69](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos273653)

`T` option, programming dialplan, [69](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos276361)

Tail length, evaluation hardware echo cancellers, [109](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos367864)

TCP/IP (Transmission Control Protocol/Internet Protocol), [44–45](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215268), [90](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos318644)

TCP SYN, [92](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos325176)

TCP (Transmission Control Protocol)

> connections, [91–92](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos321884)

> data integrity and reliability, [94](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos330257)

> data transmission, [93–94](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos328611)

> header structure, [93](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos328611)

> UDP vs., [89–90](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos316886)

> understanding, [90–91](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos318644)

`TDD MODE` command, AGI, [670](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1493463)

Teardown, TCP connection, [92](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos325176)

Telephony technologies, [1–2](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos110938)

`telnet`, connecting to AMI, [187](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos565613)

Templates, configuration, [721–723](#Practical_As-sk_1.4_and_1.6_split_036.html_filepos1586621)

Ten-digit local dialing, [22](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos163371)

Termination of rights under GNU Free Documentation License, [753](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1652303)

`testagi.gsm` file, [205](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos601014)

Testing

> calling AGI from Perl, [205–206](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos601014)

> hints, [236–237](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos656856)

> hold music for call queues, [156–157](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos480722)

> pattern matching, [32–34](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos189215)

> TTS engines, [142](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos454530)

Text

> sending using `SendText()`, [505–506](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1169269)

> using `NoOp()`, [447](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1061462)

text-to-speech. *See* [TTS (text-to-speech)](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos2041127)

Three-way handshakes, TCP, [92](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos325176)

Time

> `DateTime()` application, [317–318](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos820811)

> format variables in `voicemail.conf`, [130](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos423739)

> `SAY TIME` command, AGI, [663–664](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1478574)

> `SAYDATETIME` command, AGI, [660–661](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1473205)

> `SayUnixTime()` application, [500–501](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1158736)

> `STRFTIME()` function, [637–638](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1433473)

> `STRPTIME()` function, [638–639](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1435345)

time-conditional `include` statements, [39](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos204238)

`timeout`, `Dial()` application, [326](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos836591)

`TIMEOUT()` function

> overview of, [640–642](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1437424)

> replacing `DigitTimeout()`, [343](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos867281)

> replacing `ResponseTimeout()`, [491–492](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1137453)

> setting timeouts with, [139](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos448284)

`timeout`, `queues.conf`, [161](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos497987)

`timeoutrestart`, `queues.conf`, [164](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos510671)

Timeouts

> dialplan applications for. *See* [Flow control and timeouts, dialplan applications](#Practical_As-sk_1.4_and_1.6_split_042.html_filepos1867684)

> extensions for handling, [68–69](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos273653)

> interactive voice response, [139](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos448284)

`timestamp, queue_log`, [170](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos531167)

`timezone`, `SayUnixTime()`, [500–501](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1158736)

`timezone`, `voicemail.conf`, [130](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos423739)

Timing device, conferences, [179–180](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos549616)

Tip, analog telephony polarity, [113–114](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos380837)

Title Page of Document, GNU Free Documentation License

> copying and distributing Modified Version, [749](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1640433)

> defined, [747](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1634621)

Tones

> blocking advance dialing telemarketing, [567–568](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1291662)

> `Playtones()` dialplan application, [463–464](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1087751)

> `StopPlaytones()`, [539–540](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1239397)

`tos` setting, H323, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934)

TOS (Type of Service) flag, packet header, [45](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos218334)

Touch-Tone, inputting IVR, [137](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos443020)

Transcoding, [46](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos221706)

`Transfer()` dialplan application, [541–543](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1244531)

Translation, GNU Free Documentation License, [752–753](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1649755)

Transmission Control Protocol. *See* [TCP (Transmission Control Protocol)](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos2029548)

Transmission Control Protocol/Internet Protocol (TCP/IP), [44–45](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos215268), [90](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos318644)

Transparent copies of Document, GNU Free Documentation License, [747](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1634621), [749](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1640433), [750](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1643329)

Troubleshooting, using `EAGI()` application, [356–357](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos884594)

Trunking, bandwidth and, [105](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos354773)

`TryExecute()` dialplan application, [543–544](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1247663)

`TRYLOCK()` function, [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

`TrySystem()` dialplan application

> overview of, [544–545](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1249969)

> `System()` vs., [540](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1241527)

> `TryExecute()`, [543–544](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1247663)

`tT`, `Dial()` application, [175](#Practical_As-sk_1.4_and_1.6_split_021.html_filepos543958)

TTS (text-to-speech)

> defined, [137](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos443020)

> `Festival()` dialplan application, [372–374](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos910236)

> installing Cepstral, [142](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos454530)

> overview of, [142–143](#Practical_As-sk_1.4_and_1.6_split_018.html_filepos454530)

`25@my-phones` context, `dialplan show`, [33](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos191875)

2BIQ signaling type, BRI, [106](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos358095)

`TxFax()` command, [485](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1125377)

`TXTCIDName()` dialplan application, [545–546](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1252557)

`TXTCIDNAME()` function, [545](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1252557), [642–643](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1440397)

`type, aastra.cfg`, [234](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos651700)

Type of Service (TOS) flag, packet header, [45](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos218334)

### U

U-law, [46](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos221706)

`[u|b|s]`, `VoiceMail()` command, [122](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos393727)

UDP (User Datagram Protocol), [89–90](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos316886), [94–95](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos330257)

Underscore(_) character

> dialplan patterns beginning with, [31–32](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos185045)

> inheritance of channel variables, [63–64](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos256216)

`uniqueid field`, CDR, [729](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1604551)

United Kingdom, legalizing hold music in, [157](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos483985)

United States, legalizing hold music in, [157](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos483985)

`unixtime`, `SayUnixTime()`, [500–501](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1158736)

`UNLOCK()` function, [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

`UnpauseMonitor` command, AMI, [713](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1572810)

`UnpauseMonitor()` dialplan application, [456](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1076724), [546–547](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1254217)

`UnpauseQueueMember()` dialplan application, [456](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos1076724), [547–548](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1256128)

`updatecdr, agents.conf`, [167](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos522834)

`UpdateConfig` command, AMI, [713–714](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1572810)

Updates, of this book, [5](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos122613)

Upgrading from 1.4 to 1.6, [725–731](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1590135)

> AEL, [725](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1590135)

> AMI, [731](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1612643)

> audio formats, [729](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1604551)

> CDR, [729](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1604551)

> channel drivers, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934)

> configuration, [731](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1612643)

> core, [726–727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1592023)

> dialplan applications and functions, [727–728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

> voicemail, [727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

`URIDECODE()` function, [643–644](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1442173)

`URIENCODE()` function, [644–645](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1443531)

`urlprefix, agents.conf`, [167](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos522834)

URLs, sending, [507–509](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1172652)

`use strict` directive, [203](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos596240)

`usedirectory`, `voicemail.conf`, [129](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos419486)

User Datagram Protocol (UDP), [89–90](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos316886), [94–95](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos330257)

`UserEvent` command, AMI, [714–715](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1574909)

`UserEvent()` dialplan application, [548–550](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1258348)

`username`

> calling PSTN, [21](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos162120)

> upgrading channel drivers to 1.6, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934)

Users

> combining in single hint, [230](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos642545)

> configuring IP connections, [97](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos341191)

> monitoring status of SIP, [242](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos669776)

### V

`value, aastra.cfg`, [234](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos651700)

`/var/lib/asterisk/agi-bin`, [203](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos596240), [208](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos605605)

`$[VARIABLENAME]`, [58](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos241410), [61](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos249331)

Variables, [60–67](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos247469). *See also* [Change variables, dialplan applications](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1734738)

> calling AGI from Perl, [204–205](#Practical_As-sk_1.4_and_1.6_split_024.html_filepos599360)

> capitalizing, [61–62](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos249331)

> checking for defined, [602–603](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1362007)

> creating and changing, [58–59](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos241410)

> defining, [63](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos256216)

> defining global, [63](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos256216)

> `Dial()`, [330–331](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos854267)

> in e-mail notifications, [126](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos405883)

> expanding in extension, [61](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos249331)

> `extensions.conf` vs. `extensions.ael`, [78–79](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos295482)

> inheritance of channel, [63–65](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos256216)

> limits on integer size, [62](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos252395)

> manipulating, [66–67](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos266838)

> overview of, [60–61](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos247469)

> reserved characters, [62](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos252395)

> setting multiple simultaneously, [578–579](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1312579)

> setting with `Set()`, [509–512](#Practical_As-sk_1.4_and_1.6_split_031.html_filepos1175351)

> setting with `SetVar()`, [526](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1211304)

> `SetVar` command, AMI, [708](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1564247)

> time format, in `voicemail.conf`, [130–131](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos423739)

> types of, [58–69](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos241410)

> using double quote with string, [62](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos252395)

> using `${eXTEN}`, [40](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos207187)

`VERBOSE` command, AGI, [670–671](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1493463)

`Verbose()` dialplan application, [550–551](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1261053)

Verbosity

> debugging by increasing, [12–13](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos139227)

> starting Asterisk and SIP phone, [14–15](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos145224)

Versions

> GNU Free Documentation License, [754](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1654847)

> installing Asterisk on server, [9–10](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos131957)

> of this book, [5](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos122613)

vISDN channel, [96](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos337268)

`VMAuthenticate()` dialplan application, [135](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos440705), [551–552](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1262596)

`VMCOUNT()` function, [645–646](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1445255)

`VMCOUNT()` function

> replacing `HasNewVoiceMail()`, [393](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos946570)

> replacing `HasVoiceMail()`, [394](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos948560)

`vmcount.exp`, [192](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos575692)

VOFR channel, [96](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos337268)

Voicemail, [115–135](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos385930). *See also* [Mini-Voicemail system](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos1927144); [`voicemail.conf`](#Practical_As-sk_1.4_and_1.6_split_043.html_filepos2059851)

> [zonemessages], [129–133](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos419486)

> configuring, [17–18](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos153858)

> configuring calls from PSTN, [23](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos166131)

> Dial-by-Name directory, [133–134](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos433667)

> disk space requirements, [48](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos228287)

> example business system, [117–121](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos388734)

> example home system, [115–117](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos385930)

> getting number of messages with AMI, [190–192](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos573669)

> upgrading from 1.4 to 1.6, [727](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1595909)

> `VMCOUNT()` function, [645–646](#Practical_As-sk_1.4_and_1.6_split_033.html_filepos1445255)

`VoiceMail()` command, [121–123](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos392052)

`VoiceMail()` dialplan application, [28](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos176857), [553–555](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1266820)

Voicemail, dialplan applications

> `Directory()`, [344–346](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos869381)

> `HasNewVoiceMail()`, [393–394](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos946570)

> `HasVoiceMail()`, [394–395](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos948560)

> `MailboxExists()`, [411–412](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos984014)

> overview of, [260](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos703911)

> `VMAuthenticate()`, [551–552](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1262596)

> `VoiceMail()`, [121–123](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos392052), [553–555](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1266820)

> `VoiceMailMain()`, [123–124](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos397413), [555–556](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1271157)

`voicemail.conf`

> [zonemessages], [129–133](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos419486)

> business telephone dialplan case study, [54–55](#Practical_As-sk_1.4_and_1.6_split_012.html_filepos235650)

> configuring Asterisk voicemail, [17–18](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos153858)

> configuring voicemail in, [124–129](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos400544)

> `Directory()` application, [344–346](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos869381)

> example business voicemail system, [118–119](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos390435)

> example home voicemail system, [116](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos387630)

> saving passwords in, [135](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos440705)

`VoiceMailMain()` dialplan application

> defined, [28](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos176857), [121](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos392052)

> overview of, [123–124](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos397413)

> understanding, [555–557](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1271157)

> using `${CALLERID(num)}` with, [40](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos207187)

`VoiceMailUsersList` command, AMI, [715](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1576070)

VoIP (Voice over IP)

> calling PSTN through provider, [22](#Practical_As-sk_1.4_and_1.6_split_010.html_filepos163371)

> choosing provider, [3](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos116052)

> as superior to analog telephony, [102](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos346330)

> website resource for, [7](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos129801)

Voltage, FXS, [113](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos380837)

VPB channel, [96](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos337268)

### W

`Wait()` dialplan application, [28](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos176857), [557–558](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1274111)

`WAIT FOR DIGIT` command, AGI, [671](#Practical_As-sk_1.4_and_1.6_split_034.html_filepos1495464)

`WaitEvent` command, AMI, [715–716](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1576070)

`WaitExten()` dialplan application, [558–559](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1275848)

`WaitForNoise()` dialplan application, [559–560](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1278027)

`WaitForRing()` dialplan application, [560–561](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1280095)

`WaitForSilence()` dialplan application, [561–563](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1282190)

`WaitMusicOnHold()` dialplan application, [563–564](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1284555), [728](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1599552)

`WaitTime,` call files, [185](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos559338)

`WaitUntil()` dialplan application, [564–565](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1285741)

Wake-up call example, [186](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos563907)

Warranty Disclaimers, GNU Free Documentation License

> combining documents, [751](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1646833)

> defined, [748](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1637794)

> preserving in Modified Version, [750](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1643329)

> translations, [753](#Practical_As-sk_1.4_and_1.6_split_040.html_filepos1652303)

Web browser, BLF on Aastra 480i, [232–233](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos647207)

`weight`, `queues.conf`, [161](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos497987)

`while` command, AEL, [85](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos308520)

`While()` dialplan application, [566–567](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1289762)

`While()` loop

> ending with `EndWhile()` application, [357–358](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos886170)

> exiting with `ExitWhile()` application, [364–365](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos899096)

> `extensions.conf` vs. `extensions.ael`, [85](#Practical_As-sk_1.4_and_1.6_split_014.html_filepos308520)

> programming dialplan using, [60](#Practical_As-sk_1.4_and_1.6_split_013.html_filepos247469)

> starting with `While()` application, [566–567](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1289762)

Wide-band extensions, G.729.1 codec, [105](#Practical_As-sk_1.4_and_1.6_split_016.html_filepos354773)

Widgets, Inc.

> business telephone case study. *See* [Business telephone system case study](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1720180)

> call forwarding example, [150–152](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos473451)

> calling card example, [152–153](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos476649)

> example business voicemail system, [117–121](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos388734)

Wiki, why there is not one for this book, [6](#Practical_As-sk_1.4_and_1.6_split_009.html_filepos126171)

Wildcard character (!), [32](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos189215), [722](#Practical_As-sk_1.4_and_1.6_split_036.html_filepos1587241)

`wrapuptime, agents.conf`, [167](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos522834)

`wrapuptime`, `queues.conf`, [162](#Practical_As-sk_1.4_and_1.6_split_020.html_filepos501680)

Writing values to database, [146](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos460765), [148](#Practical_As-sk_1.4_and_1.6_split_019.html_filepos468120)

### X

[X] dialplan pattern, [31](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos185045)

XML, [197](#Practical_As-sk_1.4_and_1.6_split_023.html_filepos586401), [234–236](#Practical_As-sk_1.4_and_1.6_split_026.html_filepos651700)

### Z

[Z] dialplan pattern, [31](#Practical_As-sk_1.4_and_1.6_split_011.html_filepos185045)

ZAP channel driver, [96](#Practical_As-sk_1.4_and_1.6_split_015.html_filepos337268)

ZAP dialplan applications

> `Flash()`, [374–375](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos915718)

> overview of, [263](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos719381)

> `ZapBarge()`, [568–569](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1294162)

> `ZapRAS()`, [570–571](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1297209)

> `ZapScan()`, [571–572](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1299680)

> `ZapSendKeypadFacility()`, [572–573](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1301274)

`Zapata.conf`, [374–375](#Practical_As-sk_1.4_and_1.6_split_029.html_filepos915718)

`Zapateller()` dialplan application, [567–568](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1291662)

`ZapBarge()` dialplan application, [568–569](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1294162)

`ZapDialOffhook` command, AMI, [716](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1578002)

`ZapDNDoff` command, AMI, [717](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1579725)

`ZapDNDon` command, AMI, [717–718](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1579725)

`ZapHangup` command, AMI, [718](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1581665)

`ZapRAS()` dialplan application, [570–571](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1297209)

`ZapRestart` command, AMI, [718–719](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1581665)

`ZapScan()` dialplan application, [571–572](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1299680)

`ZapSendKeypadFacility()` dialplan application, [317](#Practical_As-sk_1.4_and_1.6_split_028.html_filepos820811), [572–573](#Practical_As-sk_1.4_and_1.6_split_032.html_filepos1301274)

`ZapShowChannels` command, AMI, [719](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1583450)

Zaptel

> defined, [733–739](#Practical_As-sk_1.4_and_1.6_split_038.html_filepos1615363)

> MeetMe conferences requiring, [416](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos995492)

> renamed as DAHDI. *See* [DAHDI (Digium Asterisk Hardware Device Interface)](#Practical_As-sk_1.4_and_1.6_split_041.html_filepos1761545)

> upgrading from 1.4 to 1.6, [730](#Practical_As-sk_1.4_and_1.6_split_037.html_filepos1607934)

`ZapTransfer` command, AMI, [673–720](#Practical_As-sk_1.4_and_1.6_split_035.html_filepos1497472)

`[zonemessages]`, `voicemail.conf`, [124](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos400544), [129–133](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos419486)

`zonename`, `voicemail.conf`, [129](#Practical_As-sk_1.4_and_1.6_split_017.html_filepos419486)

`ztdummy` driver, MeetMe conferencing, [416](#Practical_As-sk_1.4_and_1.6_split_030.html_filepos995492)

`ztdummy` module without hardware, [179](#Practical_As-sk_1.4_and_1.6_split_022.html_filepos549616)