
# THE BOOK OF ZOPE
HOW TO BUILD AND DELIVER WEB APPLICATIONS

![](img/43a28cce5475b2f487bf455365567fb6_0_0.png)

Beehive

LINUX JOURNAL PRESS

NO SPLINTERS AND NO STARCH!!

# THE BOOK OF ZOPE

![](img/43a28cce5475b2f487bf455365567fb6_3_0.png)

http://archive.org/details/isbn_9781886411579-

# ## THE BOOK OF ZOPE

HOW TO BUILD AND DELIVER WEB APPLICATIONS

beehive

Casey Duncan, Technical Editor

![](img/43a28cce5475b2f487bf455365567fb6_4_0.png)

An imprint of No Starch Press, Inc.
San Francisco

# THE BOOK OF ZOPE. Copyright ©2001 by dpunkt.verlag GmbH.

All rights reserved. No part of this work may be reproduced or transmitted in any form or by any means, electronic or mechanical, including photocopying, recording, or by any information storage or retrieval system, without the prior written permission of the copyright owner and publisher.

Printed in Canada

1 2 3 4 5 6 7 8 9 10-04 03 02 01

Trademed names are used throughout this book. Rather than use a trademark symbol with every occurrence of a trademark name, we are using the names only in an editorial fashion and to the benefit of the trademark owner, with no intention of infringement of the trademark.

Co-Publishers: William Pollock and Paul Hughes
Editorial Director: Karol Jurado
Assistant Editor: Nick Hoff
Technical Editor: Casey Duncan
Cover and Interior Design: Octopodus Studios

Composition: Michele O'Hagan
Copyeditor: Carol Lombardi
Proofreader: Karla Maree
Indexer: Nancy Humphreys

The Book of Zope is an English translation of ZOPE: Content-Management & Web-Application-Server, the German edition published in Germany, copyright ©2001 dpunkt.verlag GmbH. English translation prepared by Jody Byrne.

Distributed to the book trade in the United States by Publishers Group West, 1700 Fourth Street, Berkeley, CA 94170; phone: 800-778-3123 and fax: 510-528-3444.

Distributed to the book trade in Canada by Jacqueline Gross & Associates, Inc., One Atlantic Avenue, Suite 105, Toronto, Ontario M6K 3E7 Canada; phone: 416-531-6737; fax: 416-531-4259.

For information on trades or distributors outside the United States and Canada, please contact No Starch Press directly:

No Starch Press, Inc.
555 De Halo Street, San Francisco, CA 94107
phone: 415-863-9900; fax: 415-863-9950; info@nostarch.com; http://www.nostarch.com

The information in this book is distributed on an "As Is" basis, without warranty. While every precaution has been taken in the preparation of this work, neither the author nor No Starch Press, Inc. shall have any liability to any person or entity with respect to any loss or damage caused to be caused directly or indirectly by the information contained in this.

Library of Cataloging-in-Publication Data

+   Zope. English.
The book of Zope / Beehive; translated by Jody Byrne.
p. cm.
Includes index.
ISBN 1-886411-57-3 (pbk.).
1. Zope (Computer file) 2. Web site development-computer programs. 3. Internet programming-Computer programs.
I. Beehive (Internet Service Provider) II. Title.
TK105.8885.Z66 207 2001
005.7'13769-dc21

# BRIEF CONTENTS

# Preface

# Chapter 8
Some Methods for the Role.py and User.py Modules

# Chapter 1
Zope Fundamentals 5.

# Chapter 9
ZClasses 157

# Chapter 2
QuickStart 17

# Chapter 10
Working with the ZClass 179

# Chapter 3
Navigating Zope 39

# Chapter 11
The ZCatalog 205

# Chapter 4
DTML 61

# Chapter 12
Zope and MySQL 229

# Chapter 5
Working with Zope Versions 103

# Chapter 13
Programming Zope: Python in a Jiffy 249

# Chapter 6
Users, Roles, and Security 111

# Chapter 14
Scripting Zope with Python 263

# Chapter 7
Local Roles and Permissions 129

# Chapter 15
Zope Products 281

# Appendix C
Source Code for the Website Product
359

# Chapter 16
Debugging
309

# Appendix D
Some ZCatalog Module Methods
373

# Chapter 17
External Data Access
323

# Appendix E
Glossary
379

# Appendix A
DTML and Built-in Attributes
333

# Index
383

# Appendix B
The REQUEST Object
355

# CONTENTS IN DETAIL

# PREFACE

+   Who Is This Book For? 1
What Version of Zope Does It Cover? 1
How to Use This Book 2
Zope Beginners with HTML Knowledge 2
Zope Beginners with Both HTML and Python Knowledge 2
Advanced Zope Users with No Prior Knowledge of Zope 2
Advanced Zope Users With Prior Knowledge of Zope 2
Where Did Zope Come From? 3
About the Authors 3

# 1
ZOPE FUNDAMENTALS

+   1.1 Web Applications 5
1.1.1 The Advantages of Zope for Web Application Programmers 6
1.2 Zope As a Web Application Server 6
1.2.1 Content-by-Role 7
1.2.2 SQL = Structured Language 7
1.2.3 Python 7
1.3 Content Management Server 7
1.4 Technical Requirements 8
1.5 Installation 8
1.5.1 Windows 10
1.5.2 Windows NT 11
1.5.3 Linux 16
Summary

# 2
QUICKSTART

+   2.1 Preparations 17
2.1 Creating a User Account 18
2.2 Zope's Interface: 19
2.2.1 The Left Frame of Management 20
2.2.2 The Right Frame of Management 21
2.3 Zope-Oriented Programming 22
2.3.1 Creating a Folder 23
2.3.2 Creating Files 24
2.3.3 DTML Methods 25
2.3.4 Creating a DTML Document 26
2.4 Managing Objects 27
2.4.1 Zope 28
2.4.2 Copying Objects 29
2.4.3 Deleting Objects 30
2.4.4 Moving Objects 31
2.5 Zope Objects 32
2.5.1 Objects 33
Summary

# 3
NAVIGATING ZOPE

+   3.1 The ZCatalog 39
3.1.1 Contents 40
3.1.2 Edit Screen 41
3.1.3 The Help 42
3.1.4 The Undo 43
3.2 The Control 44
3.2.1 Shutdown 45
3.2.2 Restart 46
3.2.3 The Database 47
3.2.4 Your Database 48
3.2.5 Restoring Your Database 49
3.2.6 Your Zope 50
3.2.7 The Management 51
Summary

# 4
DTML

+   4.1 Essentials 61
4.1.1 First, Second, and Third Tags 62
4.1.2 Non-Empty Objects 63
4.2 DTML 64
4.2.1 Empty 65
4.2.2 Syntax 66
4.2.3 Attributes 67
4.3 DTML and Attributes 68
4.3.1 Variables 69
4.3.2 Server 70
4.3.3 Python 71
4.3.4 if 72
4.3.5 elif 73
4.3.6 unless 74
4.3.7 for 75
4.3.8 and 76
4.3.9 with 77
4.3.10 in 78
4.3.11 or 79
4.3.12 define 80
4.3.13 try 81
4.3.14 except 82
4.3.15 catch 83
4.3.16 finally 84
4.3.17 raise 85
4.3.18 return 86
4.3.19 break 87
4.3.20 continue 88
4.3.21 insert 89
4.3.22 delete 90
4.3.23 update 91
4.3.24 select 92
4.3.25- 93
4.3.26- 94
4.3.27- 95
4.3.28 with 96
4.3.29 with 97
4.3.30 with 98
4.3.31 with 99
4.3.32 with 100
4.3.33 with 101
4.3.34 with 102
4.3.35 with 103
4.3.36 with 104
4.3.37 with 105
4.3.38 with 106
4.3.39 with 107
4.3.40 with 108
4.3.41 with 109
4.3.42 with 110
Summary

# 5
WORKING WITH ZOPE VERSIONS

+   5.1 Creating a Zope Version 103
5.2 Upgrading a Zope Version 104
5.3 Installing a Zope Version 105
5.4 Downgrading a Zope Version 106
5.5 Managing a Zope Version 107
5.6 Backing up Zope Version 108
5.7 Restoring a Zope Version 109
Summary

# 6
USERS, ROLES, AND SECURITY

+   6.1 Zope Security 111
6.1.1 Security Model 112
6.1.2 Users 113
6.1.3 Roles 114
6.1.4 Permissions 115
6.1.5 Groups 116
6.2 Authentication 117
6.2.1 Basic Authentication 118
6.2.2 Database Authentication 119
6.2.3 LDAP Authentication 120
6.3 Authorization 121
6.3.1 Role-Based Authorization 122
6.3.2 Access Control Lists 123
Summary

# 7
LOCAL ROLES AND PERMISSIONS

+   7.1 Local Roles 129
7.1.1 Example 130
7.2 Proxy Roles 131
7.3 Permissions 132
7.3.1 Permissions for Non-Folder Objects 133
7.3.2 Permissions for Folder Objects 135
Summary

# 8
SOME METHODS FOR THE ROLE.PY AND USER.PY MODULES

+   8.1 Calling Methods 143
8.2 Methods for the Module Role.py 144
8.3 Methods for the User.py Module 147
Summary
