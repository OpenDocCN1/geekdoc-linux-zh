
The single information source for Solaris system administrators who want to become certified

## Solaris™ 2.6

## ADMINISTRATOR CERTIFICATION TRAINING GUIDE, Part I

Bill Calkins

MTP
MACMILLAN TECHNICAL PUBLISHING USA

![](img/85737305a4c9aeecbcadd9986d604c02_0_0.png)

![](img/85737305a4c9aeecbcadd9986d604c02_2_0.png)

## Solaris 2.6

## ADMINISTRATOR
CERTIFICATION
TRAINING GUIDE, Part I

MTP
MACMILLAN
TECHNICAL
PUBLISHING

Bill Calkins

| Publisher | Jim LeValley |
| Executive Editor | Alicia Buckley |
| Managing Editor | Patrick Kanouse |
| Acquisitions Editor | Alicia Buckley |
| Development Editor | Tina Oldham |
| Technical Reviewer | Janice Winsor |
| Project Editor | Theresa Wehrle |
| Copy Editor | Malinda McCain |
| Proofreader | Megan Wade |
| Indexer | Chris Barrick |
| Acquisitions Coordinator | Amy Lewis |
| Manufacturing Coordinator | Brook Farling |
| Book Designer | Gary Adair |
| Cover Designer | Sandra Schroeder |
| Production Team Supervisor | Daniela Raderstorf |
| Production | Darin Crone |

## Copyright © 1999 by Macmillan Technical Publishing

FIRST EDITION

All rights reserved. No part of this book may be reproduced or transmitted in any form or by any means, electronic or mechanical, including photocopying, recording, or by any information storage and retrieval system, without written permission from the publisher, except for the inclusion of brief quotations in a review.

International Standard Book Number: 1-57870-085-X
Library of Congress Catalog Number: 98-86498

2002 01 00 99 4 3 2 1

Interpretation of the printing code: The rightmost double-digit number is the year of the book's printing; the rightmost single-digit, the number of the book's printing. For example, the printing code 99-1 shows that the first printing of the book occurred in 1999.

Composed in Times and MCPdigital by Macmillan Computer Publishing
Printed in the United States of America

## Trademark Acknowledgments

All terms mentioned in this book that are known to be trademarks or service marks have been appropriately capitalized. Macmillan Technical Publishing cannot attest to the accuracy of this information. Use of a term in this book should not be regarded as affecting the validity of any trademark or service mark.

## Warning and Disclaimer

This book is designed to provide information about Solaris 2.6. Every effort has been made to make this book as complete and as accurate as possible, but no warranty or fitness is implied.

The information is provided on an as-is basis. The authors and Macmillan Technical Publishing shall have neither liability nor responsibility to any person or entity with respect to any loss or damages arising from the information contained in this book or from the use of the discs or programs that may accompany it.

## Feedback Information

At Macmillan Technical Publishing, our goal is to create in-depth technical books of the highest quality and value. Each book is crafted with care and precision, undergoing rigorous development that involves the unique expertise of members from the professional technical community.

Readers' feedback is a natural continuation of this process. If you have any comments regarding how we could improve the quality of this book, or otherwise alter it to better suit your needs, you can contact us at alewis@mcp.com. Please make sure to include the book title and ISBN in your message.

## ABOUT THE AUTHOR

Bill Calkins is owner and president of Pyramid Design, Inc., a computer consulting firm specializing in the implementation of client-server technologies on UNIX and Windows NT operating systems. Bill has 15 years of experience in system administration and consulting at more than 75 different companies. He has worked as a trainer in both corporate and university settings. He speaks frequently at international user conferences and has written white papers on TCP/IP networking and UNIX system administration and management. Bill draws on his many years of experience in system administration and training to provide a unique approach to conducting computer training.

## ABOUT THE TECHNICAL REVIEWER

Janice Winsor is a senior technical writer with 13 years experience in documenting UNIX systems. She worked at Sun Microsystems for seven years. For the past three years, she worked at the Filoli Information Systems Company as a project leader and manager. She is now working as a freelance author. Janice has received 10 writing awards from the Society for Technical Communications. Her published works include UNIX Book of Games, Jumping JavaScript™, and the first edition of both the Solaris System Administrator’s Guide and Solaris Advanced System Administrator’s Guide, published by Sun Microsystems Press.

Janice contributed considerable practical, hands-on expertise to the entire development process for Solaris 2.6 Administrator Certification Training Guide, Part 1. As the book was being written, Janice reviewed all the material for technical content, organization, and flow. Her feedback was critical to ensuring that Solaris 2.6 Administrator Certification Training Guide, Part 1 fits our readers’ needs for the highest quality technical information.

## DEDICATION

To Glenda, for helping me maintain a balance between too much work and having fun.
To William, for keeping me company while you played computer games in the office.
To Nicole, for the great snacks and good coffee.
To Neil, well...for going to bed on time.

## INTRODUCTION

Welcome to *Solaris 2.6 Administrator Certification Training Guide, Part I*. My goal with this book is to teach you Solaris system administration and, specifically, to help you become certified. Sun offers two examinations for the Solaris system administrator. This book prepares you for Part I of the Solaris administrator examination; it is the single best reference for learning the information necessary to pass the certification exam. Each chapter opens with specific test objectives. In addition, I provide the background information you’ll need to better understand each topic.

Whether your goal is to become certified or to simply learn more about administering a Solaris system, *Solaris 2.6 Administrator Certification Training Guide, Part I* provides an easy-to-follow format. This book begins at system installation and boot up. It then takes you through the tasks of installing patches and additional software packages; setting up file systems and user accounts; customizing the CDE environment; setting up printers; and configuring the network. It will even introduce you to shell scripts. I describe each topic as though you are new to system administrating, and I walk you through the advanced topics slowly. The only assumption I make is that you have some basic UNIX experience. I assume that you know how to log in and out, copy and remove files, and perform simple tasks with the VI editor.

I am in a good position to help you get through this learning process. I have conducted UNIX training for corporations for more than seven years. I have worked with SunOS and Solaris since the early 1980s, and I have worked as a system administrator for a large site of Sun systems for 14 years. For the past six years, I have worked independently as a system administration consultant and trainer on all flavors of UNIX, helping users like you with system administration. I have spent hundreds of hours training system administrators who had no prior UNIX experience as well as administrators who had many years of experience.

Putting this book together was a great experience. I always learn something when going back over the basics, just as I do every time I teach an introductory class. I invite even the most experienced system administrator to read this book—I guarantee you’ll find something new. I also urge you to take the certification exam, if you have not done so already. Certification provides a measure and validation of your technical skills, gives you credibility in your job, and is a great way to advance your career.
