
# RHCE:
Red Hat Certified Engineer
Study Guide

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_0_0.png)

# RHCE:
Red Hat Certified Engineer

Study Guide

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_1_0.png)

Bill McCarty

San Francisco • Paris • Düsseldorf • Soest • London
Copyright©2000 SYBEX, Inc., Alameda, CA www.sybex.com

Associate Publisher: Jordan Gold
Contracts and Licensing Manager: Kristine O'Callaghan
Acquisitions and Developmental Editor: Ellen L. Lendy
Editors: Julie Sakaoue, Suzanne Goraj, Sarah Lemaire
Production Editor: Dennis FitzGerald
Technical Editor: Randolph Russell
Book Designer: Bill Gibson
Graphic Illustrator: Tony Jonick
Electronics, Publishing Specialists: Susie Hendrick, Judy Fung, Jill Niles
Proofreaders: Carol A. Burbo, Nanette Duffy, Mae Lum, Nathan Whiteside
Indexer: Ted Laux
CD Coordinator: Kara Eve Schwartz
CD Technician: Kevin McNeil
Cover Designer: Archer Design
Cover Photographer: Tony Stone

Copyright ©2000 SYBEX, 1151 Marina Village Parkway, Alameda, CA 94501. World rights reserved. No part of this publication may be stored in a retrieval system, transmitted, or reproduced in any way, including but not limited to photocopy, photocopy, magnetic, or other record, without the prior agreement and written permission of the publisher.

Library of Congress Number: 00-106251

ISBN: 0-07821-2793-2

SYBEX and the SYLOGO are trademarks of SYBEX Inc. in the USA and other countries.

Screen reproductions produced with FullShot 99. FullShot 99 ©1991-1999 Incorporated. All rights reserved.
FullShot is a trademark of Inhibit Incorporated.

The CD interface was created using Macromedia Director, COPYRIGHT 1994, 1997-1999 Macromedia Inc. For more information on Macromedia and Macromedia Director, http://www.macromedia.com.

SYBEX is an independent entity from Red Hat, and not affiliated with Red Hat, in any manner. This publication may be used in assisting students to prepare for a Red Hat Certified Engineer exam. Neither Red Hat, Inc. nor SYBEX warrants that use of this publication that Red Hat is a registered trademark or trademark of Red Hat, Inc. in the United States or other countries. Red Hat, RPM, Linux Library, PowerTools, and all Red Hat-based trademarks and logos are trademarks or registered trademarks of Red Hat, in the United States and other countries.

TRADEMARKS: SYBEX has attempted throughout this book to distinguish proprietary trademarks from descriptive terms by following the capitalization style used by the manufacturer.

The author and publisher have made their best efforts to prepare this book, and the content is based upon final release software whenever possible. Portions of the manuscript may be used upon pre-release versions by software manufacturer(s). The author and the publisher make no representation or warranties of any kind with regard to the completeness or accuracy of the contents herein and accept no liability of any kind including but not limited to merchantability, fitness for any particular purpose, or any losses or damages of any kind caused or alleged to be caused directly or indirectly from this book.

Manufactured in the United States of America

0 9 8 7 6 5 4 3 2 1

# Software Agreement: Terms and Conditions

The media and/or other materials containing this book that are available now or in the future contains programs and/or files (the "Software") to be used in connection with the book. SYBEX grants you a license to use the Software, subject to the terms that follow. Your purchase, acceptance, or use of the Software constitutes your acceptance of such terms.

The Software compilation is property of SYBEX unless otherwise indicated and is protected by SYBEX or other copyright owner(s) in the media files (the "Owner's"). You are granted a single-user license to use the Software for your personal, non-commercial use only. You may not reproduce, sell, distribute, publish, or circulate the Software or any portion thereof, without the consent of SYBEX and the specific copyright owner(s) of any component software.

In the event that the Software or components include specific elements or other license terms, limitations, or warranties ("End-User License"), your purchase, acceptance, or use of the Software will constitute your acceptance of such terms. The End-User License supersede the terms and conditions herein for that particular Software.

By purchase, use of the Software you hereby agree to comply with all export laws and regulations of the United States and other laws that may exist from time to time.

# Software Support

Components of the software and any offers associated with them may be supported by the specific Owner(s) of material that are not supported by SYBEX. Information regarding any available support may be obtained from the media files or listed elsewhere. Should the manufacturer(s) or other owners cease to provide support, SYBEX bears no responsibility for anything. This notice concerning support for the Software is provided for your information only. SYBEX is not the agent or representative of the Owner(s), nor is it liable for providing support.

# Warranty

SYBEX warrants the enclosed media to be free of defects for a period of ninety (90) days after purchase. The Software is not available from SYBEX in any other form than that contained herein or posted to www.syex.com. If you discover a defect in the media during this warranty period, you may obtain replacement of identical format by sending the defective media, postage prepaid, to:

SYBEX Inc
Customer Service Department
1151 Marina Village Parkway
Alameda, CA 94501
(510) 523-8233
Fax: (510) 523-2373
e-mail: info@syex.com
WEB: HTTP://WWW.SYEX.COM

# Disclaimer

SYBEX makes no warranty or representation, either expressed or implied, with respect to the Software or its contents, quality, performance, merchantability, or fitness for a particular purpose. In no event will SYBEX be liable for any loss, whether direct, indirect, consequential, or other damages arising from the use of or inability to use the Software even if advised of the possibility of such damage. The exclusion of implied warranties is permitted by some states. The above may not apply to you. This warranty provides you with specific legal rights; there may be other rights that you may have state to state. The purchase of the Software with SYBEX reflects all exclusion of warranty and limitations contained in this agreement.

# Shareware Distribution

This Software may contain various programs that are designed as shareware. Copyright laws apply to shareware and ordinary commercial software, and the Owner(s) retains all rights. If you use a program and continue using it, you are expected to register it. Individual programs or details of trials, registration, and payment. Please observe the requirements stated in applicable software.

# Copy Protection

The Software whole or in part may or not be protected or encrypted. However, in all cases, reproduction or redistributing these files without authorization is expressly forbidden except as specifically provided for the Owner(s) therein.

Copyright©2000 SYBEX, Inc., Alameda, CA

www.syex.com

# Acknowledgments

This is my tenth book, and still find writing acknowledgments to be the hardest part of writing a book. This is doubly frustrating because they're so seldom read, or so it seems to me. I'm a teacher during the day, you see, and I find that my students are only dimly and rarely aware of acknowledgments in books they've bought by my insistence. Perhaps the acknowledgments in works of fiction enjoy a gladder fate, and the pessimist in me doubts that this is so. I don't understand all this, because I'm the sort who watches the credits of a film until I see the copyright symbol go by. Okay, to be honest, I often skip out when I see the production accountants' names go by, but that's quite close to the end, isn't it?

Notwithstanding this conspiracy of obscurity that surrounds acknowledgments, I must insist that they're important. Yes, I concede it's unlikely that more a handful of people have ever purchased books on account of the acknowledgments. And, that seems to indicate that the acknowledgments are less important than what lies near the center of the book. But, not so.

After all, books are created by people and for people: People who are important. And here, in the acknowledgments, I have an opportunity to pay a debt to the many people who worked on this book. In film, many people are sometimes given a prominent place in the credits—often before the title of the film itself—including producers, directors, actors, and actresses. But in publishing, the cover of a book generally contains only the name of the publishing company and the author. (Gosh, come to think of it, I haven't seen the cover of this book: I'm merely presuming that my name will be on the cover.).

This is wrong, and I'd like to give you the chance to change it: I want you to copy this page—don't tear it out or anything like that—and tape it over the cover of your book. The result may not very visually aesthetic, but my spirit soars when I consider this act of rebellion against anonymity by the cast and crew of this book.

Now, I'd best get to the point or the names of all these folk will be on the back of this page, which would ruin the whole concept, wouldn't it? Let's start with Margot Maley-Hutchison, Literary Agent (think of her as the producer), and Ellen Dendy, Acquisitions and Developmental Editor (think of her as the director). Then, there's Russell Rust and Ultiman, Technical Editors (think of them as the screenwriters who adapted my unfirmable novel, because that approximates the enormous scope of this
