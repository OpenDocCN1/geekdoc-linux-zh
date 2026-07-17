![](images/cover.jpg)

Copyright © 2020 by John Wiley & Sons, Inc.., Indianapolis, Indiana

Published simultaneously in Canada

ISBN: 978-1-119-61109-7

ISBN: 978-1-119-61114-1 (ebk.)

ISBN: 978-1-119-61113-4 (ebk.)

Manufactured in the United States of America

No part of this publication may be reproduced, stored in a retrieval system or transmitted in any form or by any means, electronic, mechanical, photocopying, recording, scanning or otherwise, except as permitted under Sections 107 or 108 of the 1976 United States Copyright Act, without either the prior written permission of the Publisher, or authorization through payment of the appropriate per-copy fee to the Copyright Clearance Center, 222 Rosewood Drive, Danvers, MA 01923, (978) 750-8400, fax (978) 646-8600\. Requests to the Publisher for permission should be addressed to the Permissions Department, John Wiley & Sons, Inc., 111 River Street, Hoboken, NJ 07030, (201) 748-6011, fax (201) 748-6008, or online at [http://www.wiley.com/go/permissions](http://www.wiley.com/go/permissions).

Limit of Liability/Disclaimer of Warranty: The publisher and the author make no representations or warranties with respect to the accuracy or completeness of the contents of this work and specifically disclaim all warranties, including without limitation warranties of fitness for a particular purpose. No warranty may be created or extended by sales or promotional materials. The advice and strategies contained herein may not be suitable for every situation. This work is sold with the understanding that the publisher is not engaged in rendering legal, accounting, or other professional services. If professional assistance is required, the services of a competent professional person should be sought. Neither the publisher nor the author shall be liable for damages arising herefrom. The fact that an organization or Web site is referred to in this work as a citation and/or a potential source of further information does not mean that the author or the publisher endorses the information the organization or Web site may provide or recommendations it may make. Further, readers should be aware that Internet Web sites listed in this work may have changed or disappeared between when this work was written and when it is read.

For general information on our other products and services or to obtain technical support, please contact our Customer Care Department within the U.S. at (877) 762-2974, outside the U.S. at (317) 572-3993 or fax (317) 572-4002.

Wiley publishes in a variety of print and electronic formats and by print-on-demand. Some material included with standard print versions of this book may not be included in e-books or in print-on-demand. If this book refers to media such as a CD or DVD that is not included in the version you purchased, you may download this material at [http://booksupport.wiley.com](http://booksupport.wiley.com). For more information about Wiley products, visit [www.wiley.com](http://www.wiley.com).

**Library of Congress Control Number:** 2019949012

TRADEMARKS: Wiley, the Wiley logo, and the Sybex logo are trademarks or registered trademarks of John Wiley & Sons, Inc. and/or its affiliates, in the United States and other countries, and may not be used without written permission. ITIL is a registered trademark of Axelos Limited. All other trademarks are the property of their respective owners. John Wiley & Sons, Inc. is not associated with any product or vendor mentioned in this book.

# Acknowledgments

Book writing tends to take attention away from other things in life. As I write this and look at the overgrown jungle that is my backyard, it's time to reflect and to find another project so I don't have to deal with whatever type of vine has taken over my shed and is creeping towards the house.

Thank you first to Kenyon Brown and Carole Jelen for this (and other) projects. Thank you also to the editors for this book, Kezia Endsley and David Clinton. Their expertise and diligence is essential in order to make the book the best it can be. Thank you to my family for their continued support. My colleagues at University of Wisconsin- Stevens Point help provide guidance and comic relief at times too.

As is the case for many books now, thank you to Jim, Patti, Tim, and Rob at Partners Pub. Thank you also to Kent Laabs for his generosity and continued help.

# About the Author

**Steve Suehring** is an assistant professor of computing and new media technologies at University of Wisconsin—Stevens Point. Prior to joining the faculty in 2015, Steve gained 20 years of field experience in a variety of technical engineering, system and network administration, and system architectural roles. Steve has written several books and has served as an editor for *LinuxWorld* magazine.

## Guide

1.  [Cover](fcover.xhtml)
2.  [Table of Contents](#ftoc.xhtml)
3.  [Introduction](#f05.xhtml)

## Pages

1.  [i](#f01.xhtml_Page_i)
2.  [ii](#f02.xhtml_Page_ii)
3.  [iii](#f03.xhtml_Page_iii)
4.  [iv](#f04.xhtml_Page_iv)
5.  [vii](#f05.xhtml_Page_vii)
6.  [viii](#f05.xhtml_Page_viii)
7.  [ix](#f05.xhtml_Page_ix)
8.  [x](#f05.xhtml_Page_x)
9.  [1](#p01.xhtml_Page_1)
10.  [3](#c01.xhtml_Page_3)
11.  [4](#c01.xhtml_Page_4)
12.  [5](#c01.xhtml_Page_5)
13.  [6](#c01.xhtml_Page_6)
14.  [7](#c01.xhtml_Page_7)
15.  [8](#c01.xhtml_Page_8)
16.  [9](#c01.xhtml_Page_9)
17.  [10](#c01.xhtml_Page_10)
18.  [11](#c01.xhtml_Page_11)
19.  [12](#c01.xhtml_Page_12)
20.  [13](#c01.xhtml_Page_13)
21.  [14](#c01.xhtml_Page_14)
22.  [15](#c01.xhtml_Page_15)
23.  [16](#c01.xhtml_Page_16)
24.  [17](#c01.xhtml_Page_17)
25.  [18](#c01.xhtml_Page_18)
26.  [19](#c01.xhtml_Page_19)
27.  [20](#c01.xhtml_Page_20)
28.  [21](#c02.xhtml_Page_21)
29.  [22](#c02.xhtml_Page_22)
30.  [23](#c02.xhtml_Page_23)
31.  [24](#c02.xhtml_Page_24)
32.  [25](#c02.xhtml_Page_25)
33.  [26](#c02.xhtml_Page_26)
34.  [27](#c02.xhtml_Page_27)
35.  [28](#c02.xhtml_Page_28)
36.  [29](#c02.xhtml_Page_29)
37.  [30](#c02.xhtml_Page_30)
38.  [31](#c02.xhtml_Page_31)
39.  [32](#c02.xhtml_Page_32)
40.  [33](#c02.xhtml_Page_33)
41.  [34](#c02.xhtml_Page_34)
42.  [35](#c02.xhtml_Page_35)
43.  [36](#c02.xhtml_Page_36)
44.  [37](#c02.xhtml_Page_37)
45.  [38](#c02.xhtml_Page_38)
46.  [39](#c02.xhtml_Page_39)
47.  [41](#c03.xhtml_Page_41)
48.  [42](#c03.xhtml_Page_42)
49.  [43](#c03.xhtml_Page_43)
50.  [44](#c03.xhtml_Page_44)
51.  [45](#c03.xhtml_Page_45)
52.  [46](#c03.xhtml_Page_46)
53.  [47](#c03.xhtml_Page_47)
54.  [48](#c03.xhtml_Page_48)
55.  [49](#c03.xhtml_Page_49)
56.  [50](#c03.xhtml_Page_50)
57.  [51](#c03.xhtml_Page_51)
58.  [52](#c03.xhtml_Page_52)
59.  [53](#c03.xhtml_Page_53)
60.  [54](#c03.xhtml_Page_54)
61.  [55](#c03.xhtml_Page_55)
62.  [56](#c03.xhtml_Page_56)
63.  [57](#c03.xhtml_Page_57)
64.  [58](#c03.xhtml_Page_58)
65.  [59](#c03.xhtml_Page_59)
66.  [60](#c03.xhtml_Page_60)
67.  [61](#c03.xhtml_Page_61)
68.  [63](#c04.xhtml_Page_63)
69.  [64](#c04.xhtml_Page_64)
70.  [65](#c04.xhtml_Page_65)
71.  [66](#c04.xhtml_Page_66)
72.  [67](#c04.xhtml_Page_67)
73.  [68](#c04.xhtml_Page_68)
74.  [69](#c04.xhtml_Page_69)
75.  [70](#c04.xhtml_Page_70)
76.  [71](#c04.xhtml_Page_71)
77.  [72](#c04.xhtml_Page_72)
78.  [73](#c04.xhtml_Page_73)
79.  [74](#c04.xhtml_Page_74)
80.  [75](#c04.xhtml_Page_75)
81.  [76](#c04.xhtml_Page_76)
82.  [77](#c04.xhtml_Page_77)
83.  [78](#c04.xhtml_Page_78)
84.  [79](#c04.xhtml_Page_79)
85.  [80](#c04.xhtml_Page_80)
86.  [81](#c04.xhtml_Page_81)
87.  [83](#p02.xhtml_Page_83)
88.  [85](#c05.xhtml_Page_85)
89.  [86](#c05.xhtml_Page_86)
90.  [87](#c05.xhtml_Page_87)
91.  [88](#c05.xhtml_Page_88)
92.  [89](#c05.xhtml_Page_89)
93.  [90](#c05.xhtml_Page_90)
94.  [91](#c05.xhtml_Page_91)
95.  [92](#c05.xhtml_Page_92)
96.  [93](#c05.xhtml_Page_93)
97.  [94](#c05.xhtml_Page_94)
98.  [95](#c05.xhtml_Page_95)
99.  [96](#c05.xhtml_Page_96)
100.  [97](#c05.xhtml_Page_97)
101.  [98](#c05.xhtml_Page_98)
102.  [99](#c05.xhtml_Page_99)
103.  [100](#c05.xhtml_Page_100)
104.  [101](#c05.xhtml_Page_101)
105.  [103](#c06.xhtml_Page_103)
106.  [104](#c06.xhtml_Page_104)
107.  [105](#c06.xhtml_Page_105)
108.  [106](#c06.xhtml_Page_106)
109.  [107](#c06.xhtml_Page_107)
110.  [108](#c06.xhtml_Page_108)
111.  [109](#c06.xhtml_Page_109)
112.  [110](#c06.xhtml_Page_110)
113.  [111](#c06.xhtml_Page_111)
114.  [112](#c06.xhtml_Page_112)
115.  [113](#c06.xhtml_Page_113)
116.  [114](#c06.xhtml_Page_114)
117.  [115](#c06.xhtml_Page_115)
118.  [116](#c06.xhtml_Page_116)
119.  [117](#c06.xhtml_Page_117)
120.  [118](#c06.xhtml_Page_118)
121.  [119](#c06.xhtml_Page_119)
122.  [121](#c07.xhtml_Page_121)
123.  [122](#c07.xhtml_Page_122)
124.  [123](#c07.xhtml_Page_123)
125.  [124](#c07.xhtml_Page_124)
126.  [125](#c07.xhtml_Page_125)
127.  [126](#c07.xhtml_Page_126)
128.  [127](#c07.xhtml_Page_127)
129.  [128](#c07.xhtml_Page_128)
130.  [129](#c07.xhtml_Page_129)
131.  [130](#c07.xhtml_Page_130)
132.  [131](#c07.xhtml_Page_131)
133.  [132](#c07.xhtml_Page_132)
134.  [133](#c07.xhtml_Page_133)
135.  [134](#c07.xhtml_Page_134)
136.  [135](#c07.xhtml_Page_135)
137.  [136](#c07.xhtml_Page_136)
138.  [137](#c07.xhtml_Page_137)
139.  [138](#c07.xhtml_Page_138)
140.  [139](#c08.xhtml_Page_139)
141.  [140](#c08.xhtml_Page_140)
142.  [141](#c08.xhtml_Page_141)
143.  [142](#c08.xhtml_Page_142)
144.  [143](#c08.xhtml_Page_143)
145.  [144](#c08.xhtml_Page_144)
146.  [145](#c08.xhtml_Page_145)
147.  [146](#c08.xhtml_Page_146)
148.  [147](#c08.xhtml_Page_147)
149.  [148](#c08.xhtml_Page_148)
150.  [149](#c08.xhtml_Page_149)
151.  [150](#c08.xhtml_Page_150)
152.  [151](#c08.xhtml_Page_151)
153.  [152](#c08.xhtml_Page_152)
154.  [153](#c08.xhtml_Page_153)
155.  [154](#c08.xhtml_Page_154)
156.  [155](#c08.xhtml_Page_155)
157.  [156](#c08.xhtml_Page_156)
158.  [157](#c09.xhtml_Page_157)
159.  [158](#c09.xhtml_Page_158)
160.  [159](#c09.xhtml_Page_159)
161.  [160](#c09.xhtml_Page_160)
162.  [161](#c09.xhtml_Page_161)
163.  [162](#c09.xhtml_Page_162)
164.  [163](#c09.xhtml_Page_163)
165.  [164](#c09.xhtml_Page_164)
166.  [165](#c09.xhtml_Page_165)
167.  [166](#c09.xhtml_Page_166)
168.  [167](#c09.xhtml_Page_167)
169.  [168](#c09.xhtml_Page_168)
170.  [169](#c09.xhtml_Page_169)
171.  [170](#c09.xhtml_Page_170)
172.  [171](#c09.xhtml_Page_171)
173.  [172](#c09.xhtml_Page_172)
174.  [173](#c09.xhtml_Page_173)
175.  [174](#c09.xhtml_Page_174)
176.  [175](#c10.xhtml_Page_175)
177.  [176](#c10.xhtml_Page_176)
178.  [177](#c10.xhtml_Page_177)
179.  [178](#c10.xhtml_Page_178)
180.  [179](#c10.xhtml_Page_179)
181.  [180](#c10.xhtml_Page_180)
182.  [181](#c10.xhtml_Page_181)
183.  [182](#c10.xhtml_Page_182)
184.  [183](#c10.xhtml_Page_183)
185.  [184](#c10.xhtml_Page_184)
186.  [185](#c10.xhtml_Page_185)
187.  [186](#c10.xhtml_Page_186)
188.  [187](#c10.xhtml_Page_187)
189.  [188](#c10.xhtml_Page_188)
190.  [189](#c10.xhtml_Page_189)
191.  [190](#c10.xhtml_Page_190)
192.  [191](#c10.xhtml_Page_191)
193.  [192](#c10.xhtml_Page_192)
194.  [193](#p03.xhtml_Page_193)
195.  [195](#c11.xhtml_Page_195)
196.  [196](#c11.xhtml_Page_196)
197.  [197](#c11.xhtml_Page_197)
198.  [198](#c11.xhtml_Page_198)
199.  [199](#c11.xhtml_Page_199)
200.  [200](#c11.xhtml_Page_200)
201.  [201](#c11.xhtml_Page_201)
202.  [202](#c11.xhtml_Page_202)
203.  [203](#c11.xhtml_Page_203)
204.  [204](#c11.xhtml_Page_204)
205.  [205](#c11.xhtml_Page_205)
206.  [207](#c12.xhtml_Page_207)
207.  [208](#c12.xhtml_Page_208)
208.  [209](#c12.xhtml_Page_209)
209.  [210](#c12.xhtml_Page_210)
210.  [211](#c12.xhtml_Page_211)
211.  [212](#c12.xhtml_Page_212)
212.  [213](#c12.xhtml_Page_213)
213.  [214](#c12.xhtml_Page_214)
214.  [215](#c12.xhtml_Page_215)
215.  [216](#c12.xhtml_Page_216)
216.  [217](#c12.xhtml_Page_217)
217.  [219](#a01.xhtml_Page_219)
218.  [220](#a01.xhtml_Page_220)
219.  [221](#a01.xhtml_Page_221)
220.  [222](#a01.xhtml_Page_222)
221.  [223](#a01.xhtml_Page_223)
222.  [224](#a01.xhtml_Page_224)
223.  [225](#a01.xhtml_Page_225)
224.  [226](#a01.xhtml_Page_226)
225.  [227](#a01.xhtml_Page_227)
226.  [228](#a01.xhtml_Page_228)
227.  [229](#a01.xhtml_Page_229)
228.  [230](#a01.xhtml_Page_230)
229.  [231](#a01.xhtml_Page_231)
230.  [232](#a01.xhtml_Page_232)
231.  [233](#a01.xhtml_Page_233)
232.  [234](#a01.xhtml_Page_234)
233.  [235](#a01.xhtml_Page_235)
234.  [236](#a01.xhtml_Page_236)
235.  [237](#a01.xhtml_Page_237)
236.  [238](#a01.xhtml_Page_238)
237.  [239](#a01.xhtml_Page_239)
238.  [240](#a01.xhtml_Page_240)
239.  [241](#a01.xhtml_Page_241)
240.  [242](#a01.xhtml_Page_242)
241.  [243](#a01.xhtml_Page_243)
242.  [244](#a01.xhtml_Page_244)
243.  [245](#a01.xhtml_Page_245)
244.  [246](#a01.xhtml_Page_246)
245.  [247](#a01.xhtml_Page_247)
246.  [248](#a01.xhtml_Page_248)
247.  [249](#a01.xhtml_Page_249)
248.  [250](#a01.xhtml_Page_250)
249.  [251](#a01.xhtml_Page_251)
250.  [252](#a01.xhtml_Page_252)
251.  [253](#a01.xhtml_Page_253)
252.  [254](#a01.xhtml_Page_254)
253.  [255](#a01.xhtml_Page_255)
254.  [256](#a01.xhtml_Page_256)
255.  [257](#a01.xhtml_Page_257)
256.  [258](#a01.xhtml_Page_258)
257.  [259](#a01.xhtml_Page_259)
258.  [260](#a01.xhtml_Page_260)
259.  [261](#a01.xhtml_Page_261)
260.  [262](#a01.xhtml_Page_262)
261.  [263](#a01.xhtml_Page_263)
262.  [264](#a01.xhtml_Page_264)
263.  [265](#a01.xhtml_Page_265)
264.  [266](#a01.xhtml_Page_266)
265.  [267](#a01.xhtml_Page_267)
266.  [268](#a01.xhtml_Page_268)
267.  [269](#a01.xhtml_Page_269)
268.  [270](#a01.xhtml_Page_270)
269.  [271](#a01.xhtml_Page_271)
270.  [272](#a01.xhtml_Page_272)
271.  [273](#a01.xhtml_Page_273)
272.  [274](#a01.xhtml_Page_274)
273.  [275](#a01.xhtml_Page_275)
274.  [276](#a01.xhtml_Page_276)
275.  [277](#a01.xhtml_Page_277)
276.  [278](#a01.xhtml_Page_278)
277.  [279](#a01.xhtml_Page_279)
278.  [280](#a01.xhtml_Page_280)
279.  [281](#a01.xhtml_Page_281)
280.  [282](#a01.xhtml_Page_282)
281.  [283](#a01.xhtml_Page_283)
282.  [284](#a01.xhtml_Page_284)
283.  [285](#a01.xhtml_Page_285)
284.  [286](#a01.xhtml_Page_286)
285.  [287](#a01.xhtml_Page_287)
286.  [288](#a01.xhtml_Page_288)
287.  [289](#a01.xhtml_Page_289)
288.  [290](#a01.xhtml_Page_290)
289.  [291](#a01.xhtml_Page_291)
290.  [292](#a01.xhtml_Page_292)
291.  [293](#b01.xhtml_Page_293)
292.  [294](#b01.xhtml_Page_294)
293.  [295](#b01.xhtml_Page_295)
294.  [296](#b01.xhtml_Page_296)
295.  [297](#b01.xhtml_Page_297)
296.  [298](#b01.xhtml_Page_298)
297.  [299](#b01.xhtml_Page_299)
298.  [300](#b01.xhtml_Page_300)
299.  [301](#b01.xhtml_Page_301)
300.  [302](#b01.xhtml_Page_302)
301.  [303](#b01.xhtml_Page_303)
302.  [304](#b01.xhtml_Page_304)
303.  [305](#b01.xhtml_Page_305)
304.  [306](#b01.xhtml_Page_306)
305.  [307](#b01.xhtml_Page_307)
306.  [308](#b01.xhtml_Page_308)
307.  [309](#b01.xhtml_Page_309)
308.  [310](#b02.xhtml_Page_310)
309.  [311](#eula.xhtml_Page_311)

# Introduction

This book provides practice questions for the Linux Professional Institute LPIC-1 certification. Specifically, the book has been updated to reflect the objectives for exams 101-500 and 102-500\. The book includes numerous multiple-choice questions related to the exam objectives found on the LPI website.

## What Does This Book Cover?

Each chapter of the book connects directly to one of the objectives, and each objective is covered throughout the book. In addition, two practice exams are included in the book that you should find helpful in preparing for the exams.

The book does not require that you start at the beginning and read through in a linear, page-by-page manner. Rather, you may skip to objective areas that might be less familiar, and you can do so without losing any fidelity or missing something from a previous chapter.

## Who Should Read This Book

It is assumed that you would have a companion text for this book in order to obtain deeper information on the given subjects for the exam. However, it is possible to use this book as a stand-alone means for preparation.

Here are some basic assumptions about the audience for this book:

*   You have used Linux or are using the book to learn Linux.
*   You have used a computer for basic operations.
*   You will use the book as a means for practicing for the certification exams.

## How to Use This Book

This book is best used as a tool for testing your knowledge in the objective domains specified for the exam. The book provides explanations for each question, including, where applicable, explanations as to why the other options were incorrect. Ideally, the book is used in conjunction with the companion text in order to fully explain the concepts.

## Certification Exam Policies

The Linux Professional Institute outlines various policies related to certification and other similar matters. In addition, other policies applicable may be through the testing facility or organization. More information on some of the LPI policies can be found at [www.lpi.org/policies](http://www.lpi.org/policies).

## Exam Objectives

The following lists contain the topics and weights for Exams 101 and 102\. This list follows the sequence in which they are covered in the book. You can find more information about what is covered in each topic, including key knowledge areas and files, terms, and utilities, at the start of the applicable chapter.

### Exam 101-500

**Topic 101: System Architecture**

*   101.1 Determine and configure hardware settings (weight 2).
*   101.2 Boot the system (weight 3).
*   101.3 Change runlevels/boot targets and shutdown or reboot system (weight 3).

**Topic 102: Linux Installation and Package Management**

*   102.1 Design hard disk layout (weight 2).
*   102.2 Install a boot manager (weight 2).
*   102.3 Manage shared libraries (weight 1).
*   102.4 Use Debian package management (weight 3).
*   102.5 Use RPM and YUM package management (weight 3).
*   102.6 Linux as a virtualization guest (weight 1)

**Topic 103: GNU and UNIX Commands**

*   103.1 Work on the command line (weight 4).
*   103.2 Process text streams using filters (weight 2).
*   103.3 Perform basic file management (weight 4).
*   103.4 Use streams, pipes, and redirects (weight 4).
*   103.5 Create, monitor, and kill processes (weight 4).
*   103.6 Modify process execution priorities (weight 2).
*   103.7 Search text files using regular expressions (weight 3).
*   103.8 Basic file editing 3

**Topic 104: Devices, Linux Filesystems, Filesystem Hierarchy Standard**

*   104.1 Create partitions and filesystems (weight 2).
*   104.2 Maintain the integrity of filesystems (weight 2).
*   104.3 Control mounting and unmounting of filesystems (weight 3).
*   *104.4 Removed*
*   104.5 Manage file permissions and ownership (weight 3).
*   104.6 Create and change hard and symbolic links (weight 2).
*   104.7 Find system files and place files in the correct location (weight 2).

### Exam 102-500

**Topic 105: Shells and Shell Scripting**

*   105.1 Customize and use the shell environment (weight 4).
*   105.2 Customize or write simple scripts (weight 4).

**Topic 106: User Interfaces and Desktops**

*   106.1 Install and configure X11 (weight 2).
*   106.2 Graphical desktops (weight 1)
*   106.3 Accessibility (weight 1)

**Topic 107: Administrative Tasks**

*   107.1 Manage user and group accounts and related system files (weight 5).
*   107.2 Automate system administration tasks by scheduling jobs (weight 4).
*   107.3 Localization and internationalization (weight 3)

**Topic 108: Essential System Services**

*   108.1 Maintain system time (weight 3).
*   108.2 System logging (weight 4)
*   108.3 Mail Transfer Agent (MTA) Basics (weight 3)
*   108.4 Manage printers and printing (weight 2).

**Topic 109: Networking Fundamentals**

*   109.1 Fundamentals of Internet protocols (weight 4)
*   109.2 Persistent network configuration (weight 4)
*   109.3 Basic network troubleshooting (weight 4)
*   109.4 Configure client-side DNS (weight 2).

**Topic 110: Security**

*   110.1 Perform security administration tasks (weight 3).
*   110.2 Set up host security (weight 3).
*   110.3 Securing data with encryption (weight 4)

# PART I
Exam 101-500

# Chapter 1
Topic 101: System Architecture

**THE FOLLOWING EXAM OBJECTIVES ARE COVERED IN THIS CHAPTER:**

*   **![images](images/correction.png)  101.1 Determine and configure hardware settings.**
    *   Key knowledge areas:
        *   Enable and disable integrated peripherals.
        *   Differentiate between the various types of mass storage devices.
        *   Determine hardware resources for devices.
        *   Tools and utilities to list various hardware information (e.g. lsusb, lspci, etc.)
        *   Tools and utilities to manipulate USB devices
        *   Conceptual understanding of sysfs, udev, and dbus
    *   The following is a partial list of the used files, terms, and utilities:
        *   /sys/
        *   /proc/
        *   /dev/
        *   modprobe
        *   lsmod
        *   lspci
        *   lsusb
*   **![images](images/correction.png)  101.2 Boot the system.**
    *   Key knowledge areas:
        *   Provide common commands to the boot loader and options to the kernel at boot time.
        *   Demonstrate knowledge of the boot sequence from BIOS/UEFI to boot completion.
        *   Understand SysV init and systemd.
        *   Awareness of Upstart
        *   Check book events in the log files.
    *   The following is a partial list of the used files, terms, and utilities:
        *   dmesg
        *   journalctl
        *   BIOS
        *   UEFI
        *   bootloader
        *   kernel
        *   initramfs
        *   init
        *   SysV init
        *   systemd
*   **![images](images/correction.png)  101.3 Change runlevels/boot targets and shut down or reboot system.**
    *   Key knowledge areas:
        *   Set the default runlevel or boot target.
        *   Change between runlevels/boot targets including single-user mode.
        *   Shut down and reboot from the command line.
        *   Alert users before switching runlevels/boot targets or other major system events.
        *   Properly terminate processes.
        *   Awareness of acpid
    *   The following is a partial list of the used files, terms, and utilities:
        *   /etc/inittab
        *   shutdown
        *   init
        *   /etc/init.d/
        *   telinit
        *   systemd
        *   systemctl
        *   /etc/systemd/
        *   /usr/lib/systemd/
        *   wall

1.  Which of the following commands is used to view kernel-related udev events in real time?

    1.  udevls all
    2.  lsudev -f
    3.  udevmon -a
    4.  udevadm monitor

2.  Which command enables you to view the current interrupt request (IRQ) assignments?

    1.  view /proc/irq
    2.  cat /proc/interrupts
    3.  cat /dev/irq
    4.  less /dev/irq

3.  Configuration of udev devices is done by working with files in which directory?

    1.  /udev/devices
    2.  /devices/
    3.  /udev/config
    4.  /etc/udev

4.  Which command is used to automatically load a module and its dependencies?

    1.  modprobe
    2.  lsmod
    3.  insmod
    4.  rmmod

5.  Which command is used to obtain a list of USB devices?

    1.  usb-list
    2.  lsusb
    3.  ls-usb
    4.  ls --usb

6.  When working with hotplug devices, you need to gather more information about them through udevadm. Which udevadm command enables you to query the udev database for information on a device?

    1.  query
    2.  info
    3.  getinfo
    4.  devinfo

7.  Which command can be used to view the kernel ring buffer in order to troubleshoot the boot process?

    1.  lsboot
    2.  boot-log
    3.  krblog
    4.  dmesg

8.  During the initialization process for a Linux system using SysV init, which runlevel corresponds to single-user mode?

    1.  Runlevel 5
    2.  Runlevel SU
    3.  Runlevel 1
    4.  Runlevel 6

9.  On a system using SysV init, in which directory are the startup and shutdown scripts for services stored?

    1.  /etc/init-d
    2.  /etc/init
    3.  /etc/sysV
    4.  /etc/init.d

10.  Which command can be used to reboot a system?

    1.  init 6
    2.  shutdown -h -t now
    3.  init 1
    4.  refresh-system

11.  When using an SysV init-based system, which command would you use if you make changes to the /etc/inittab file and want those changes to be reloaded without a reboot?

    1.  init-refresh
    2.  init 6
    3.  telinit
    4.  reload-inittab

12.  Which command displays the current runlevel for a system?

    1.  show-level
    2.  init --level
    3.  sudo init
    4.  runlevel

13.  Within which folder are systemd unit configuration files stored?

    1.  /etc/system.conf.d
    2.  /lib/system.conf.d
    3.  /lib/systemd/system
    4.  /etc/sysconfd

14.  Which command is used with systemd in order to list the available service units?

    1.  systemd list-units
    2.  systemctl list-units
    3.  systemd unit-list
    4.  systemctl show-units

15.  Which option to lspci is used to display both numeric codes and device names?

    1.  -numdev
    2.  -n
    3.  -nn
    4.  -devnum

16.  Which command can be used to obtain a list of currently loaded kernel modules?

    1.  insmod
    2.  modlist
    3.  ls --modules
    4.  lsmod

17.  Which option to the modprobe command shows the dependencies for a given module?

    1.  --show-options
    2.  --list-deps
    3.  --show-depends
    4.  --list-all

18.  Which command can you use to send a message to all users who are currently logged into a system?

    1.  cat
    2.  wall
    3.  tee
    4.  ssh

19.  Which of the following is a good first troubleshooting step when a hard disk is not detected by the Linux kernel?

    1.  Unplug the disk.
    2.  Check the system BIOS.
    3.  Restart the web server service.
    4.  Run the disk-detect command.

20.  Within which directory is information about USB devices stored?

    1.  /etc/usbdevices
    2.  /var/usb
    3.  /lib/sys/usb
    4.  /sys/bus/usb/devices

21.  If the kernel ring buffer has been overwritten, within which file can you look to find boot messages?

    1.  /var/log/bootmessages
    2.  /var/log/mail.info
    3.  /var/adm/log/boot.info
    4.  /var/log/dmesg

22.  Which command and option can be used to determine whether a given service is currently loaded?

    1.  systemctl --ls
    2.  telinit
    3.  systemctl status
    4.  sysctl -a

23.  Which command on a systemd-controlled system would place the system into single-user mode?

    1.  systemctl one
    2.  systemctl isolate rescue.target
    3.  systemctl single-user
    4.  systemctl runlevel one

24.  Which command on a system controlled by Upstart will reload the configuration files?

    1.  initctl reload
    2.  systemd reload
    3.  upstart --reload
    4.  ups -reload

25.  When working with a SysV system, which option to chkconfig will display all services and their runlevels?

    1.  --reload
    2.  --list
    3.  --all
    4.  --ls

26.  A drive connected to USB is considered which type of device?

    1.  Medium
    2.  Coldplug
    3.  Hotplug
    4.  Sideplug

27.  The system is using a temporary flash USB disk for data mounted at /dev/sda1. You need to remove the disk. Which of the following commands will enable the disk to be safely removed from the system?

    1.  usbstop /dev/sda
    2.  umount /dev/sda1
    3.  unmount /dev/sda1
    4.  dev-eject /dev/sda1

28.  You have connected a USB disk to the system and need to find out its connection point within the system. Which of the following is the best method for accomplishing this task?

    1.  Rebooting the system
    2.  Viewing the contents of /var/log/usb.log
    3.  Connecting the drive to a USB port that you know the number of
    4.  Running dmesg and looking for the disk

29.  Which of the following commands will initiate an immediate shutdown of the system?

    1.  shutdown -c
    2.  halt
    3.  systemd stop
    4.  stop-system

30.  Which option within a systemd service file indicates the program to execute?

    1.  StartProgram
    2.  ShortCut
    3.  ExecStart
    4.  Startup

31.  Which command will display the default target on a computer running systemd?

    1.  systemctl defaults
    2.  update-rc.d defaults
    3.  systemctl runlevel
    4.  systemctl get-default

32.  Which option to the systemctl command will change a service so that it runs on the next boot of the system?

    1.  enable
    2.  startonboot
    3.  loadonboot
    4.  start

33.  Which of the following best describes the /proc filesystem?

    1.  /proc contains information about files to be processed.
    2.  /proc contains configuration files for processes.
    3.  /proc contains information on currently running processes, including the kernel.
    4.  /proc contains variable data such as mail and web files.

34.  Which command will retrieve information about the USB connections on a computer in a tree-like format?

    1.  lsusb -tree
    2.  lsusb --tree
    3.  lsusb -t
    4.  usblist --tree

35.  What is one reason why a device driver does not appear in the output of lsmod, even though the device is loaded and working properly?

    1.  The use of systemd means that drivers are not required for most devices.
    2.  The use of initramfs means that support is enabled by default.
    3.  The system does not need a driver for the device.
    4.  Support for the device has been compiled directly into the kernel.

36.  Which option to rmmod will cause the module to wait until it’s no longer in use to unload the module?

    1.  -test
    2.  -f
    3.  -w
    4.  -unload

37.  You are using a storage area network (SAN) that keeps causing errors on your Linux system due to an improper kernel module created by the SAN vendor. When the SAN sends updates, it causes the filesystem to be mounted as read-only. Which command and option can you use to change the behavior of the filesystem to account for the SAN bug?

    1.  mount --continue
    2.  tune2fs -e continue
    3.  mkfs --no-remount
    4.  mount -o remount

38.  Within which directory are rules related to udev stored?

    1.  /etc/udev.conf
    2.  /etc/udev.conf.d
    3.  /etc/udev/rules.d
    4.  /etc/udev.d

39.  Which option to lspci displays the kernel driver in use for the given Peripheral Component Interconnect (PCI) device?

    1.  -t
    2.  -k
    3.  -n
    4.  -a

40.  Within which of the following directories will you find blacklist information for modules loaded with modprobe?

    1.  /etc/blacklist
    2.  /etc/modprobe.d
    3.  /etc/blacklist.mod
    4.  /etc/modprobe

41.  When working with a CentOS 6 system, which command is used to create the initial RAM disk?

    1.  mkinit
    2.  dracut
    3.  mkraminit
    4.  mkinitfs

42.  Within which file will you find a list of the currently available kernel symbols?

    1.  /proc/kernelsyms
    2.  /etc/kernel.conf
    3.  /etc/lsyms
    4.  /proc/kallsyms

43.  Which of the following commands can be used to show the various information related to a currently loaded module, including core size and settings for options?

    1.  systool -v -m <module>
    2.  modinfo -r <module>
    3.  lsmod <module>
    4.  infmod <module>

44.  Which directory contains various elements and configuration information about the kernel such as the release number, domain name, location of modprobe, and other settings?

    1.  /proc/sys/kmod
    2.  /proc/sys/kernel
    3.  /proc/kernel
    4.  /proc/kernel/sys

45.  Within which directory should systemd unit files that you create be stored?

    1.  /etc/system
    2.  /etc/systemd/system
    3.  /usr/share/systemd
    4.  /usr/share/system

46.  Which of the following commands should you execute after making changes to systemd service configurations in order for those changes to take effect?

    1.  systemd reload
    2.  reboot
    3.  systemctl daemon-reload
    4.  systemctl reboot

47.  Which of the following files contains the runlevels for the system along with a reference to the corresponding rc file?

    1.  /etc/runlevels
    2.  /etc/inittab
    3.  /etc/rc
    4.  /etc/runlevel

48.  Which boot loader can be used for File Allocation Table (FAT) filesystems and might be used for a rescue disk?

    1.  SYSBOOT
    2.  SYSLINUX
    3.  TIELINUX
    4.  FATLINUX

49.  Which of the following is used to provide an early filesystem-based loading process for key drivers needed to continue the boot process?

    1.  bootrd
    2.  driverload
    3.  initrd
    4.  initdrv

50.  When booting a system you receive an error similar to "No init found" and are then placed at an initramfs prompt. You need to check the hard drive for errors. Which of the following commands performs an error check on a hard drive partition in Linux?

    1.  defrag
    2.  fsck
    3.  checkfs
    4.  chkfs

51.  Which of the following commands places the system in single-user mode?

    1.  tellinit 1
    2.  chginit 1
    3.  telinet 1
    4.  telinit 1

52.  Which of the following commands changes the boot order for the next boot?

    1.  efibootmgr -c
    2.  efibootmgr -b -B
    3.  efibootmgr -o
    4.  efibootmgr -n

53.  Which boot loader can be used with ISO9660 CD-ROMS?

    1.  ISOLINUX
    2.  EFIBOOT
    3.  ISOFS
    4.  BOOTISO

54.  Within which directory are systemd user unit files placed by installed packages?

    1.  /usr/lib/systemd/user
    2.  /usr/lib/systemd/system
    3.  /usr/systemd
    4.  /usr/system

55.  When using Unified Extensible Firmware Interface (UEFI), which of the following files can be used as a boot loader?

    1.  shim.uefi
    2.  shim.efi
    3.  shim.fx
    4.  efi.shim

56.  Which directory on a SysV init-based system contains scripts that are used for starting and stopping services?

    1.  /etc/rc.int
    2.  /etc/boot
    3.  /etc/bootscripts
    4.  /etc/init.d

57.  Which of the following commands is used to find overriding configuration files on a systemd-based system?

    1.  diff
    2.  systemctl -diff
    3.  systemd-delta
    4.  systemctl configoverride

58.  Which of the following commands on a Red Hat system lists all of the SysV services set to be executed on boot along with their setting for each runlevel?

    1.  rlevel
    2.  chkconfig --list
    3.  bootldr --list
    4.  init --bootlist

59.  Which of the following commands, executed from within the UEFI shell, controls the boot configuration?

    1.  bootcfg
    2.  bcfg
    3.  grub-install
    4.  grcfg

60.  Which file must exist within /tftpboot on the Trivial File Transfer Protocol (TFTP) server for a system that will use PXELINUX for its boot loader?

    1.  pxelinux.tftp
    2.  pxelinux.boot
    3.  pxelinux.conf
    4.  pxelinux.0

61.  Which utility can you use on a Debian or Ubuntu system to manage SysV init scripts, such as setting them to run on boot?

    1.  bootorder
    2.  bootloader
    3.  configchk
    4.  update-rc.d

62.  Which key, pressed during the operating system selection menu, is used to enable editing of the parameters related to boot with GRUB?

    1.  v
    2.  e
    3.  r
    4.  y

63.  Which systemctl subcommand is used to switch runlevels?

    1.  switch
    2.  move
    3.  runlevel
    4.  isolate

64.  When examining the /etc/inittab file, which option signifies the default runlevel to which the system will boot?

    1.  default
    2.  defaultboot
    3.  initdefault
    4.  defaultlvl

65.  Which of the following is used instead of initrd to provide an early filesystem for essential drivers?

    1.  initnext
    2.  initramfs
    3.  initialize
    4.  initfs

66.  Which of the following commands sets the default systemd target to multi-user?

    1.  systemctl set-default multi-user.target
    2.  systemd set-default multi-user.target
    3.  systemctl set-def muser.target
    4.  systemd set-def muser.target

67.  When using a shim for booting a UEFI-based system, which of the following files is loaded after shim.efi?

    1.  grubx64.cfg
    2.  grub.conf
    3.  grubx64.efi
    4.  efi.boot

68.  Within which hierarchy are files from /etc/init.d linked so that the files are executed during the various runlevels of a SysV system?

    1.  /etc/rc.S
    2.  /etc/rc
    3.  /etc/boot/rc
    4.  /etc/rc.d

69.  What is the name of the unit to which a systemd system is booted in order to start other levels?

    1.  default.target
    2.  init.target
    3.  initial.target
    4.  load.target

70.  When viewing information in /dev/disk/by-path using the command ls -l, which of the following filenames represents a logical unit number (LUN) from Fibre Channel?

    1.  /dev/fc0
    2.  pci-0000:1a:00.0-fc-0x500601653ee0025f:0x0000000000000000
    3.  pci-0000:1a:00.0-scsi-0x500601653ee0025f:0x0000000000000000
    4.  /dev/fibre0

71.  You have purchased new solid-state drive (SSD) hardware that uses the NVMe (Non-Volatile Memory Express) protocol but cannot find the disks in the normal /dev/sd* location in which you have traditionally found such storage. In which location should you look for these drives?

    1.  /dev/nd*
    2.  /dev/nvme*
    3.  /dev/nv*
    4.  /dev/nvme/*

72.  Which file contains information about the current md Redundant Array of Inexpensive Disks (RAID) configuration such as the personalities?

    1.  /proc/raidinfo
    2.  /proc/rhyinfo
    3.  /proc/mdraid
    4.  /proc/mdstat

73.  Which of the following directory hierarchies contains information such as the World Wide Name (WWN) for Fibre Channel?

    1.  /sys/class/wwn
    2.  /sys/class/fc_host
    3.  /sys/class/fclist
    4.  /sys/class/fc/wwn

74.  Information about logical volumes can be found in which of the following directories?

    1.  /dev/lvinfo
    2.  /dev/map
    3.  /dev/mapper
    4.  /dev/lvmap

75.  Which of the following commands will examine the PCI subsystem for NVMe-based devices?

    1.  psnvme
    2.  lsnvme
    3.  lspci | grep scsi
    4.  lspci | grep -i nvme

76.  Which of the following devices is the location of the first Small Computer System Interface (SCSI) tape device detected at boot?

    1.  /dev/st1
    2.  /dev/sd0
    3.  /dev/sd1
    4.  /dev/st0

77.  Which of the following files should be used to display a message to users prior to logging in locally?

    1.  /etc/loginmesg
    2.  /etc/logmessage.txt
    3.  /etc/issue
    4.  /etc/banner

78.  Which file contains a message that is displayed after a successful login?

    1.  /etc/loginbanner
    2.  /etc/issue
    3.  /etc/motd
    4.  /etc/message

79.  Which of the following files can be used to provide a message to users logging in remotely with a protocol such as telnet?

    1.  /etc/telnet.msg
    2.  /etc/issue.net
    3.  /etc/login.msg
    4.  /etc/telnet.login

80.  Which of the following commands turns off the computer, including removing power, if possible?

    1.  systemctl halt
    2.  systemctl reboot
    3.  systemctl stop
    4.  systemctl poweroff

81.  Which of the following shutdown commands reboots the system in 15 minutes?

    1.  shutdown -r +15
    2.  shutdown +15
    3.  shutdown -15
    4.  shutdown -r 00:15

82.  When terminating a process on a SysV init-based system, which command can be used to stop the process?

    1.  service
    2.  sysv
    3.  syscl
    4.  servc

83.  Which of the following commands show the boot messages captured by systemd?

    1.  journalctl -b
    2.  systemctl -b
    3.  journalctl -bm
    4.  journalctl -l

84.  Which option to the shutdown command halts or stops the system?

    1.  -h
    2.  -s
    3.  -f
    4.  -t

85.  Which signal number is used as SIGKILL when used with the kill command?

    1.  1
    2.  4
    3.  9
    4.  11

86.  Which directory contains rc-related startup scripts on a legacy Debian system?

    1.  /etc/init
    2.  /etc/inittab
    3.  /etc/init.d
    4.  /etc/rc.init

87.  When attempting to enable an integrated peripheral on a basic input/output system (BIOS) system, what should be done to determine whether the peripheral has been enabled within the BIOS?

    1.  Examine boot messages to determine if the kernel has detected the peripheral.
    2.  Examine /var/log/auth.log for detection of the peripheral.
    3.  Reboot the system to determine if the device works.
    4.  Enable the peripheral by removing it from the blacklisted modules.

88.  Which option to the wall command suppresses the "Broadcast message" banner that normally displays?

    1.  -b
    2.  -a
    3.  -n
    4.  -d

# Chapter 2
Topic 102: Linux Installation and Package Management

**THE FOLLOWING EXAM OBJECTIVES ARE COVERED IN THIS CHAPTER:**

*   **![images](images/correction.png)  102.1 Design hard disk layout.**
    *   Key knowledge areas:
        *   Allocate filesystems and swap space to separate partitions or disks.
        *   Tailor the design to the intended use of the system.
        *   Ensure the /boot partition conforms to the hardware architecture requirements for booting.
        *   Knowledge of basic features of LVM
    *   The following is a partial list of the used files, terms, and utilities:
        *   /(root) filesystem
        *   /var filesystem
        *   /home filesystem
        *   /boot filesystem
        *   EFI System Partition (ESP)
        *   swap space
        *   mount points
        *   partitions
*   **![images](images/correction.png)  102.2 Install a boot manager.**
    *   Key knowledge areas:
        *   Provide alternative boot locations and backup boot options.
        *   Install and configure a boot loader such as GRUB Legacy.
        *   Perform basic configuration changes for GRUB2.
        *   Interact with the boot loader.
    *   The following is a partial list of the used files, terms, and utilities:
        *   menu.lst, grub.cfg, and grub.conf
        *   grub-install
        *   grub-mkconfig
        *   MBR
*   **![images](images/correction.png)  102.3 Manage shared libraries.**
    *   Key knowledge areas:
        *   Identify shared libraries.
        *   Identify the typical locations of system libraries.
        *   Load shared libraries.
    *   The following is a partial list of the used files, terms, and utilities:
        *   ldd
        *   ldconfig
        *   /etc/ld.so.conf
        *   LD_LIBRARY_PATH
*   **![images](images/correction.png)  102.4 Use Debian package management.**
    *   Key knowledge areas:
        *   Install, upgrade, and uninstall Debian binary packages.
        *   Find packages containing specific files or libraries which may or may not be installed.
        *   Obtain package information like version, content, dependencies, package integrity, and installation status (whether or not the package is installed).
        *   Awareness of apt
    *   The following is a partial list of the used files, terms, and utilities:
        *   /etc/apt/sources.list
        *   dpkg
        *   dpkg-reconfigure
        *   apt-get
        *   apt-cache
*   **![images](images/correction.png)  102.5 Use RPM and yum package management.**
    *   Key knowledge areas:
        *   Install, re-install, upgrade, and remove packages using RPM, yum, and zypper.
        *   Obtain information on RPM packages such as version, status, dependencies, integrity, and signatures.
        *   Determine what files a package provides, as well as find which package a specific file comes from.
        *   Awareness of dnf
    *   The following is a partial list of the used files, terms, and utilities:
        *   rpm
        *   rpm2cpio
        *   /etc/yum.conf
        *   /etc/yum.repos.d/
        *   yum
        *   zypper
*   **![images](images/correction.png)  102.6 Linux as a virtualization guest**
    *   Key knowledge areas:
        *   Understand the general concept of virtual machines and containers.
        *   Understand common elements of virtual machines in an IaaS cloud, such as computing instances, block storage, and networking.
        *   Understand unique properties of a Linux system that have to change when a system is cloned or used as a template.
        *   Understand how system images are used to deploy virtual machines, cloud instances, and containers.
        *   Understand Linux extensions that integrate Linux with a virtualization product.
        *   Awareness of cloud-init
    *   The following is a partial list of the used files, terms, and utilities:
        *   Virtual machine
        *   Linux container
        *   Application container
        *   Guest drivers
        *   SSH host keys
        *   D-Bus machine id

1.  A Serial Advanced Technology Attachment (SATA) disk will use which of the following identifiers?

    1.  /dev/hdX
    2.  /dev/sataX
    3.  /dev/sdX
    4.  /disk/sataX

2.  Which option given at boot time within the GRUB configuration will boot the system into single-user mode?

    1.  single-user
    2.  su
    3.  single
    4.  root

3.  During boot of a system with GRUB, which key can be pressed to display the GRUB menu?

    1.  Shift
    2.  E
    3.  V
    4.  H

4.  When booting, which option can be added to a GRUB configuration line to set or change the root partition at boot time to /dev/sda2?

    1.  rootpartition={hd0,2}
    2.  root=/dev/sda2
    3.  root={hd0,3}
    4.  rootpartition=/dev/sda2

5.  Which key combination will enable you to edit the kernel options and then boot when using GRUB Legacy?

    1.  ESC for editing and then Return to boot
    2.  v for editing and then Return to boot
    3.  e for editing and then b to boot
    4.  v for editing and then b to boot

6.  During the boot process for a virtual machine, what is the next step in the boot process after the kernel has taken over the initialization process and initializes devices?

    1.  The system BIOS initializes devices.
    2.  The system is placed in multi-user mode.
    3.  The boot loader initializes the kernel.
    4.  The root partition is mounted.

7.  Where in the filesystem will the EFI system partition (ESP) typically be mounted?

    1.  /etc/efi
    2.  /efi
    3.  /sys/efi
    4.  /boot/efi

8.  When partitioning a disk for a mail server running postfix, which partition/mounted directory should be the largest in order to allow for mail storage?

    1.  /etc
    2.  /usr/bin
    3.  /mail
    4.  /var

9.  Which option within GRUB Legacy is used to indicate that a root partition contains a non-Linux kernel?

    1.  initrd
    2.  non-linux
    3.  rootnoverify
    4.  root-win

10.  Which command will output a new GRUB2 configuration file and send the output to the correct location for booting?

    1.  update-grub > /boot/grub/grub.cfg
    2.  update-grub boot > /boot/grub.cfg
    3.  grub-rc.d
    4.  grub-boot

11.  What is the maximum number of primary partitions available on an MBR partitioning system?

    1.  2
    2.  4
    3.  1
    4.  5

12.  Which command is used to update the links and cache for shared libraries on the system?

    1.  ldcache
    2.  cache-update
    3.  link-update
    4.  ldconfig

13.  Which command and option is used to update a Debian system to the latest software?

    1.  apt-update
    2.  apt-get upgrade
    3.  dpkg -U
    4.  apt-cache clean

14.  Which option given to a yum command will install a given package?

    1.  update
    2.  configure
    3.  install
    4.  get

15.  What is the location of the home directory for the root user?

    1.  /home/root
    2.  /home/su
    3.  /root
    4.  /

16.  When using rpm2cpio, by default the output is sent to which location?

    1.  STDOUT
    2.  The cpio.out file
    3.  The a.out file
    4.  The /tmp/cpi.out file

17.  Which partition or directory structure typically holds most of the programs for a Linux system?

    1.  /etc
    2.  /usr
    3.  /home
    4.  /var

18.  Your GRUB Legacy configuration includes a dual-boot option with Linux listed first and another operating system listed second. Which of the following options will boot to the Linux partition by default?

    1.  default=linux
    2.  default=0
    3.  default=1
    4.  default=other

19.  Which file should you edit when using GRUB2 in order to set things like the timeout?

    1.  /etc/default/grub
    2.  /etc/grub/boot
    3.  /etc/boot/grub.d
    4.  /grub.d/boot

20.  Which yum option displays the dependencies for the package specified?

    1.  list
    2.  deplist
    3.  dependencies
    4.  listdeps

21.  Which options for an rpm command will display verbose output for an installation along with progress of the installation?

    1.  -ivh
    2.  -wvh
    3.  --avh
    4.  --ins-verbose

22.  Which of the following commands adds /usr/local/lib to the LD_LIBRARY_PATH when using BASH shell?

    1.  set PATH=/usr/local/lib
    2.  export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib
    3.  LD_LIBRARY_PATH=/usr/local/lib
    4.  connectpath LD_LIBRARY_PATH=/usr/local/lib

23.  Which command can be used to download an RPM package without installing it?

    1.  yumdl
    2.  yumdownloadonly
    3.  yumdown
    4.  yumdownloader

24.  Which command will search for a package named zsh on a Debian system?

    1.  apt-cache search zsh
    2.  apt-get search zsh
    3.  apt-cache locate zsh
    4.  apt search zsh

25.  Which option within /etc/default/grub is used to configure the default operating system for boot?

    1.  GRUB_OS
    2.  GRUB_ON
    3.  GRUB_DEFAULT
    4.  DEFAULT_OS

26.  When found in a GRUB configuration file, what does the ro option indicate?

    1.  Initially mount the root partition as read-only.
    2.  Mount the kernel as read-only.
    3.  Start the init program as read-once.
    4.  Mount the root partition in Raised Object mode.

27.  Within which directory will you find the repositories used by yum?

    1.  /etc/yum.conf
    2.  /etc/repos
    3.  /etc/yum.conf.d
    4.  /etc/yum.repos.d

28.  Which rpm option can be used to verify that no files have been altered since installation?

    1.  -V
    2.  -v
    3.  --verbose
    4.  --filesum

29.  Which option for the grub-mkconfig command sends output to a file instead of STDOUT?

    1.  -stdout
    2.  --fileout
    3.  -o
    4.  -f

30.  The presence of menu.lst within the filesystem typically indicates which condition?

    1.  GRUB Legacy is in use on the system.
    2.  GRUB2 is in use on the system.
    3.  An error has occurred creating the output to menu.lst.
    4.  The options for rescue boot have been changed.

31.  Which command is used to determine the libraries on which a given command depends?

    1.  ldconfig
    2.  librarylist
    3.  listdeps
    4.  ldd

32.  Which of the following is true of Linux swap space?

    1.  Swap is used to hold temporary database tables.
    2.  Swap is used as additional memory when there is insufficient RAM.
    3.  Swap is used by the mail server for security.
    4.  Swap is used to scrub data from the network temporarily.

33.  Which of the following is not typically used to store libraries?

    1.  /lib
    2.  /etc/lib
    3.  /usr/lib
    4.  /usr/local/lib

34.  Which of the following commands updates the package cache for a Debian system?

    1.  apt-get cache-update
    2.  apt-cache update
    3.  apt-get update
    4.  apt-get upgrade

35.  Within which file are details of the current package repositories stored on a Debian system?

    1.  /etc/apt.list
    2.  /etc/sources.list
    3.  /etc/apt/sources.list
    4.  /etc/apt.d/sources.list

36.  Of the following choices, which size would be most appropriate for the /boot partition of a Linux system?

    1.  Between 100MB and 500MB
    2.  Between 1GB and 10GB
    3.  /boot should not be partitioned separately.
    4.  Less than 5MB

37.  Which of the following commands initializes a physical disk partition for use with Logical Volume Manager (LVM)?

    1.  lvmcreate
    2.  pvcreate
    3.  fvcreate
    4.  lvinit

38.  Which of the following commands installs GRUB into the MBR of the second SATA disk?

    1.  grub-install /dev/hdb2
    2.  grub-install /dev/sda2
    3.  grub-config /dev/sda
    4.  grub-install /dev/sdb

39.  Which command should be used to make changes to the choices made when a Debian package was installed?

    1.  dpkg-reconfigure
    2.  dpkg -r
    3.  dpkg --reconf
    4.  apt-get reinstall

40.  Which command is used to create a logical volume with LVM?

    1.  pvcreate
    2.  lvmcreate
    3.  lvcreate
    4.  volcreate

41.  What is the logical order for creation of an LVM logical volume?

    1.  Physical volume creation, volume group creation, logical volume creation
    2.  Physical volume creation, logical volume creation, volume group creation
    3.  Logical volume creation, physical volume creation, volume group creation
    4.  LVM creation, format, partition

42.  Which of the Debian package management tools provides a terminal-based interface for management?

    1.  apt-get
    2.  dpkg
    3.  apt-cache
    4.  aptitude

43.  Which option for yum performs a search of the package cache?

    1.  seek
    2.  query
    3.  --search
    4.  search

44.  Which command option for rpm can be used to show the version of the kernel?

    1.  rpm kernel
    2.  rpm -qa kernel
    3.  rpm search kernel
    4.  rpm --list kern

45.  Assuming a menu entry of Debian in your GRUB configuration, which option in /etc/default/grub would set that as the default operating system to boot?

    1.  GRUB_OS
    2.  GRUB_OS_DEF
    3.  GRUB_DEFAULT
    4.  GRUB_CONF

46.  Which option in /etc/yum.conf is used to ensure that the kernel is not updated when the system is updated?

    1.  exclude=kernel*
    2.  exclude-kernel
    3.  updatekernel=false
    4.  include-except=kernel

47.  Which command should be run after making a change to the /etc/default/grub file?

    1.  grub
    2.  grub-mkconfig
    3.  grub-inst
    4.  reboot

48.  Which command searches for and provides information on a given package on a Debian system, including whether or not the package is currently installed?

    1.  dpkg -i
    2.  dpkg -s
    3.  apt-cache
    4.  apt-info

49.  Which command is used to search for physical volumes for use with LVM?

    1.  lvmcreate
    2.  pvcreate
    3.  lvmdiskscan
    4.  lvmscan

50.  Which option added to yumdownloader will also download dependencies?

    1.  --deps
    2.  --resolve
    3.  --resdeps
    4.  -d

51.  Which of the following installs a previously downloaded Debian package?

    1.  dpkg -i <package name>
    2.  apt-install <package name>
    3.  apt-slash <package name>
    4.  dpkg -U <package name>

52.  A hard drive is reported as hd(0,0) by the GRUB Legacy configuration file. To which of the following disks and partitions does this correspond?

    1.  /dev/hdb2
    2.  /dev/hda0
    3.  /dev/disk1
    4.  /dev/sda1

53.  Which filesystem format type is used for the EFI System Partition (ESP)?

    1.  FAT
    2.  EXT4
    3.  NTFS
    4.  EXT3

54.  Which of the following commands installs extlinux into the /boot partition?

    1.  extlinux --install /boot
    2.  extlinux --inst /boot
    3.  extlinux -boot
    4.  extlinux /boot install

55.  Which of the following commands mounts /dev/sda1 in the /boot partition?

    1.  mount /dev/sda /boot
    2.  mount /boot /dev/sda1
    3.  mount /dev/sda1 /boot
    4.  mount -dev sda1 /boot

56.  Which of the following can be identified as an initial sector on a disk that stores information about the disk partitioning and operating system location?

    1.  Minimal boot record (MBR)
    2.  Master boot record (MBR)
    3.  Init sector
    4.  Master partition table (MPT)

57.  Which option to grub-install will place the GRUB images into an alternate directory?

    1.  --boot-dir
    2.  -b
    3.  -boot
    4.  --boot-directory

58.  Within which file is a list of the currently mounted filesystems stored?

    1.  /etc/fstab
    2.  /etc/curmount
    3.  /var/spool/files
    4.  /etc/mtab

59.  Which command is used to activate swap space on a system?

    1.  mkswap
    2.  swapon
    3.  swapact
    4.  actswap

60.  Which of the following commands displays information about a given physical volume in an LVM setup?

    1.  pvdisp
    2.  pvlist
    3.  pvdisplay
    4.  pvl

61.  Which of the following commands creates a logical volume with LVM?

    1.  lvc
    2.  lvcreate
    3.  lvlist
    4.  lvmake

62.  Which of the following commands looks for LVM physical volumes and volume groups involved in an LVM configuration?

    1.  vgscan
    2.  lvmscan
    3.  lvlist
    4.  pvlist

63.  Which of the following commands is used to display a list of physical volumes involved in LVM?

    1.  pvdisp
    2.  pvlist
    3.  pvscan
    4.  pvmm

64.  Which option to lvchange sets whether the logical volume is available?

    1.  -a
    2.  -b
    3.  -c
    4.  -d

65.  When working with a script to create directories, the script is checking to see if srv/vhosts exists. When doing an ls of the root directory, /, you see that it does exist. However, the script does not. What might be the issue?

    1.  The script is not executable.
    2.  The script does not have the setuid bit set.
    3.  The script is using a relative path.
    4.  The script is owned by root.

66.  You are architecting an application and need to choose between application containerization and virtualization. Which of the following describes a difference between application containers and a virtual machine?

    1.  An application container can contain only one application whereas a virtual machine can contain many.
    2.  An application container shares the host kernel whereas a virtual machine can have its own kernel.
    3.  An application container is used for small applications whereas a virtual machine is used for large applications.
    4.  The use of application containers is for testing only whereas a virtual machine is used for production.

67.  In addition to including /lib and /usr/lib, where does ldconfig look to find additional directories to incorporate into the library path?

    1.  /etc/lib.conf
    2.  /etc/ldconf
    3.  /etc/lib.cfg
    4.  /etc/ld.so.conf

68.  You are working with a cloud instance virtual machine deployed with an Infrastructure-as-a-Service (IaaS) provider. The virtual machine is running slowly. Which type of resource might you add to the cloud instance in order to improve performance?

    1.  Compute
    2.  Block storage
    3.  Networking
    4.  Disk

69.  When working with a system to determine if it is using GRUB or GRUB2, the presence of which file indicates that it is GRUB2?

    1.  grub.cfg
    2.  grub.conf
    3.  menu.lst
    4.  grub2.conf

70.  You are working to create a system image or template from which other virtual machines will be deployed. Which of the following represents a unique item that will change with each deployed virtual host or image?

    1.  System directories
    2.  MAC address
    3.  Guest drivers
    4.  Pilot homing

71.  Which program can be used to deploy an Ubuntu image to a remote cloud provider?

    1.  dep-image
    2.  cloud-init
    3.  init-cloud
    4.  image-dep

72.  Which file is used as the primary configuration file for the yum package manager?

    1.  /etc/yum.cfg
    2.  /etc/yum.d
    3.  /etc/yum.conf
    4.  /etc/yum.config

73.  Which of the following commands and options lists all of the files included with a package on a Debian system?

    1.  apt -L
    2.  dpkg -L
    3.  dpkg -f
    4.  apt-get show

74.  When working with SSH (Secure Shell) keys for a virtual machine cloud deployment, which key is deployed to the virtual machine so that you can connect from the host?

    1.  The public key
    2.  The signature file
    3.  The private key
    4.  Both the public and private keys

75.  When using a GPT disk, which partition needs to be created for a Linux system to boot?

    1.  /boot/efi
    2.  /boot/gpt
    3.  /gpt
    4.  /vmgpt

76.  Which option to zypper installs a package?

    1.  install
    2.  retr
    3.  get
    4.  ref

77.  You are working with a Fedora 22 system and need to install a package. Which of the following is the default package manager on this system?

    1.  yum
    2.  apt
    3.  dpkg
    4.  dnf

78.  You need to list the files available on a package on CentOS. Which of the following commands accomplishes this task?

    1.  repoquery -l
    2.  pkgquery -l
    3.  dpkg -L
    4.  pkglist

79.  You need to create a backup of user home directories including root. Which directory or directories need to be included in the backup?

    1.  /home
    2.  /home and /home/root
    3.  /home and /root
    4.  /home and /root/home

80.  In which file can you find the unique D-Bus machine ID for a given system?

    1.  /etc/machine-id
    2.  /etc/machineID
    3.  /etc/mch.conf
    4.  /etc/machine.id.conf

81.  Which option to ldconfig can be used to process only those directories given on the command line rather than the directories found in /etc/ld.so.conf?

    1.  -n
    2.  -i
    3.  -v
    4.  -r

82.  When working with package caches on Debian, you need to determine if the package list is being updated. Which option to apt-cache shows the number of available packages on the system?

    1.  packagenum
    2.  status
    3.  stats
    4.  liststatus

83.  Which option to grub-install specifies the directory in which the EFI partition is located?

    1.  --boot-dir
    2.  --efi
    3.  --efi-boot
    4.  --efi-directory

84.  Within which file are mount points for the system stored?

    1.  /etc/fstab
    2.  /etc/mtab
    3.  /etc/partitions.list
    4.  /etc/disk.conf

85.  Which of the following option sets for rpm lists the files within the package?

    1.  lf
    2.  qlp
    3.  qf
    4.  eps

86.  When working with a CentOS system, you need to determine the release of a certain package. Which command and option will accomplish this task?

    1.  dpkg -i
    2.  yum info
    3.  yum search
    4.  apt search

87.  You are using a host machine and are unsure if it supports the extensions to enable virtualization. Which of the following should you look for in /proc/cpuinfo to indicate that the system is ready for virtualization?

    1.  vmx
    2.  virt
    3.  envirt
    4.  vtcapable

88.  Within which file can you configure a filter for devices when using vgscan?

    1.  lvm.conf
    2.  vg.conf
    3.  vgscan.conf
    4.  lv.cfg

89.  Which of the following swapon options displays information on the size of swap space along with its used space?

    1.  --list
    2.  -a
    3.  --show
    4.  -h

# Chapter 3
Topic 103: GNU and UNIX Commands

**THE FOLLOWING EXAM OBJECTIVES ARE COVERED IN THIS CHAPTER:**

*   **![images](images/correction.png)  103.1 Work on the command line.**
    *   Key knowledge areas:
        *   Use single shell commands and one-line command sequences to perform basic tasks on the command line.
        *   Use and modify the shell environment including defining, referencing, and exporting environment variables.
        *   Use and edit command history.
        *   Invoke commands inside and outside the defined path.
    *   The following is a partial list of the used files, terms, and utilities:
        *   bash
        *   echo
        *   env
        *   export
        *   pwd
        *   set
        *   unset
        *   type
        *   which
        *   man
        *   uname
        *   history
        *   .bash_history
        *   Quoting
*   **![images](images/correction.png)  103.2 Process text streams using filters.**
    *   Key knowledge areas:
        *   Send text files and output streams through text utility filters to modify the output using standard UNIX commands found in the GNU textutils package.
    *   The following is a partial list of the used files, terms, and utilities:
        *   bzcat
        *   cat
        *   cut
        *   head
        *   less
        *   md5sum
        *   nl
        *   od
        *   paste
        *   sed
        *   sha256sum
        *   sha512sum
        *   sort
        *   split
        *   tail
        *   tr
        *   uniq
        *   wc
        *   xzcat
        *   zcat
*   **![images](images/correction.png)  103.3 Perform basic file management.**
    *   Key knowledge areas:
        *   Copy, move, and remove files and directories individually.
        *   Copy multiple files and directories recursively.
        *   Remove files and directories recursively.
        *   Use simple and advanced wildcard specifications in commands.
        *   Use find to locate and act on files based on type, size, or time.
        *   Use tar, cpio, and dd.
    *   The following is a partial list of the used files, terms, and utilities:
        *   cp
        *   find
        *   mkdir
        *   mv
        *   ls
        *   rm
        *   rmdir
        *   touch
        *   tar
        *   cpio
        *   dd
        *   file
        *   gzip
        *   gunzip
        *   bzip2
        *   bunzip2
        *   xz
        *   unxz
        *   file globbing
*   **![images](images/correction.png)  103.4 Use streams, pipes, and redirects.**
    *   Key knowledge areas:
        *   Redirect standard input, standard output, and standard error.
        *   Pipe the output of one command to the input of another command.
        *   Use the output of one command as arguments to another command.
        *   Send output to both stdout and a file.
    *   The following is a partial list of the used files, terms, and utilities:
        *   tee
        *   xargs
*   **![images](images/correction.png)  103.5 Create, monitor, and kill processes.**
    *   Key knowledge areas:
        *   Run jobs in the foreground and background.
        *   Signal a program to continue running after logout.
        *   Monitor active processes.
        *   Select and sort processes for display.
        *   Send signals to processes.
    *   The following is a partial list of the used files, terms, and utilities:
        *   &
        *   bg
        *   fg
        *   jobs
        *   kill
        *   nohup
        *   ps
        *   top
        *   free
        *   uptime
        *   pgrep
        *   pkill
        *   killall
        *   watch
        *   screen
        *   tmux
*   **![images](images/correction.png)  103.6 Modify process execution priorities.**
    *   Key knowledge areas:
        *   Know the default priority of a job that is created.
        *   Run a program with higher or lower priority than the default.
        *   Change the priority of a running process.
    *   The following is a partial list of the used files, terms, and utilities:
        *   nice
        *   ps
        *   renice
        *   top
*   **![images](images/correction.png)  103.7 Search text files using regular expressions.**
    *   Key knowledge areas:
        *   Create simple regular expressions containing several notational elements.
        *   Understand the differences between basic and extended regular expressions.
        *   Understand the concepts of special characters, character classes, quantifiers, and anchors.
        *   Use regular expression tools to perform searches through a filesystem or file content.
        *   Use regular expressions to delete, change, and substitute text.
    *   The following is a partial list of the used files, terms, and utilities:
        *   grep
        *   egrep
        *   fgrep
        *   sed
        *   regex(7)
*   **![images](images/correction.png)  103.8 Basic file editing**
    *   Key knowledge areas:
        *   Navigate a document using vi.
        *   Understand and use Vi modes.
        *   Insert, edit, delete, copy, and find text in Vi.
        *   Be aware of Emacs, nano, and vim.
        *   Configure the standard editor.
    *   The following is a partial list of the used files, terms, and utilities:
        *   vi
        *   /, ?
        *   h,j,k,l
        *   i, o, a
        *   d, p, y, dd, yy
        *   ZZ, :w!, :q!
        *   EDITOR

1.  Assume that you’re using the Bash shell and want to prevent output redirects from accidentally overwriting existing files. Which command and option can be used to invoke this behavior?

    1.  setoutput -f
    2.  overwrite=no
    3.  overwrite -n
    4.  set -C

2.  What command can be used to view the current settings for your environment when using Bash?

    1.  environment
    2.  env
    3.  listenv
    4.  echoenv

3.  Which command is used to access documentation on the Linux computer for a given command?

    1.  doc
    2.  heredoc
    3.  man
    4.  manual

4.  Which of the following commands will print various information about the kernel and architecture, along with other details?

    1.  info --sys
    2.  man sys
    3.  sysinfo
    4.  uname -a

5.  When using sed for a substitution operation, which option must be included so that the substitution applies to the entire line rather than just the first instance?

    1.  g
    2.  a
    3.  r
    4.  y

6.  Which option for the wc command prints the number of lines given as input?

    1.  -f
    2.  -a
    3.  -l
    4.  -o

7.  What is the default number of lines printed by the head and tail commands, respectively?

    1.  10 for head, 5 for tail
    2.  5 for head, 10 for tail
    3.  10 for both head and tail
    4.  3 for both head and tail

8.  You are attempting to use rmdir to remove a directory, but there are still multiple files and other directories contained within it. Assuming that you’re sure you want to remove the directory and all of its contents, what is the command and arguments to remove the directory and all of its contents?

    1.  rm -f
    2.  rm -rf
    3.  rmdir -a
    4.  rmdir -m

9.  Which command will find directories with names beginning with 2014 located beneath the current directory?

    1.  find ./ -name "2014"
    2.  find ./ -type d -name "2014"
    3.  find / -type d "2014"
    4.  find ./ -type d -name "2014*"

10.  Which of the following commands will provide the usernames in a sorted list gathered from the /etc/passwd file?

    1.  cat /etc/passwd | awk -F : '{print $1}' | sort
    2.  sort /etc/passwd | cut
    3.  echo /etc/passwd
    4.  cat /etc/passwd | awk '{print $1}' | sort

11.  Which options to ls will produce output, including hidden (dot) files, in a list that is ordered such that the newest files are at the end of the output?

    1.  -la
    2.  -lat
    3.  -latr
    4.  -ltr

12.  What will be the result if the touch command is executed on a file that already exists?

    1.  The access time stamp of the file will change to the current time when the touch command was executed.
    2.  The file will be overwritten.
    3.  There will be no change.
    4.  The file will be appended to.

13.  Which option to both mv and cp will cause the command to prompt before overwriting files that already exist?

    1.  -f
    2.  -Z
    3.  -r
    4.  -i

14.  Which of the following commands will send the contents of /etc/passwd to both STDOUT and to a file called passwordfile?

    1.  cat /etc/passwd > passwordfile
    2.  var /etc/passwd | passwordfile
    3.  cat /etc/passwd | tee passwordfile
    4.  echo /etc/passwd | stdout > passwordfile

15.  The current hierarchy on the server contains a directory called /usr/local. You need to create additional directories below that are called /usr/local/test/october. Which command will accomplish this task?

    1.  mkdir -p /usr/local/test/october
    2.  mkdir /usr/local/test/october
    3.  mkdir -r /usr/local/test/october
    4.  mkdir -f /usr/local/test/october

16.  Which option to the cp command will copy directories in a recursive manner?

    1.  -v
    2.  -R
    3.  -Z
    4.  -i

17.  You have received a file that does not have a file extension. Which command can you run to help determine what type of file it might be?

    1.  grep
    2.  telnet
    3.  file
    4.  export

18.  Which command will create an image of the /dev/sda1 disk partition and place that image into a file called output.img?

    1.  dd if=sda of=/dev/sda1
    2.  dd if=output.img of=/dev/sda1
    3.  dd if=/dev/sda1 of=output.img
    4.  echo /dev/sda1 > output.img

19.  What is the default delimiter used by the cut command?

    1.  Colon
    2.  Tab
    3.  Space
    4.  Comma

20.  Which of the following will unzip and extract the contents of a file that has been tarred and gzipped?

    1.  tar -zxf <file.tgz>
    2.  tar -xf <file.tgz>
    3.  tar -vz <file.tgz>
    4.  tar -fd <file.tgz>

21.  What command is used to bring a command to foreground processing after it has been backgrounded with an &?

    1.  bg
    2.  fore
    3.  4g
    4.  fg

22.  You need to write a script that gathers all of the process IDs for all instances of Apache running on the system. Which of the following commands will accomplish this task?

    1.  ps auwx | grep apache
    2.  pgrep apache
    3.  processlist apache
    4.  ls -p apache

23.  Which of the following command lines would monitor a single process called nagios in a continuous manner?

    1.  top -n 1
    2.  top -p 23
    3.  ps -nagios
    4.  top -p`pidof nagios`

24.  Users are reporting that various programs are crashing on the server. By examining logs, you see that certain processes are reporting out-of-memory conditions. Which command can you use to see the overall memory usage, including available swap space?

    1.  tree
    2.  pgrep
    3.  uptime
    4.  free

25.  You are using the Vi editor for changing a file and need to exit. You receive a notice indicating "No write since last change". Assuming you want to save your work, which of the following commands will save your work and exit Vi?

    1.  :wq
    2.  :q!
    3.  dd
    4.  x

26.  What option is used to change the number of lines of output for the head and tail commands?

    1.  -l
    2.  -f
    3.  -g
    4.  -n

27.  Which command can be used to determine the current load average along with information on the amount of time since the last boot of the system?

    1.  uptime
    2.  sysinfo
    3.  bash
    4.  ls -u

28.  You need to start a long-running process that requires a terminal and foreground processing. However, you cannot leave your terminal window open due to security restrictions. Which command will enable you to start the process and return at a later time to continue the session?

    1.  fg
    2.  bg
    3.  kill
    4.  screen

29.  You have attempted to stop a process using its service command and also using the kill command. Which signal can be sent to the process using the kill command in order to force the process to end?

    1.  -15
    2.  -f
    3.  -9
    4.  -stop

30.  When working in the Bash shell, you need to redirect both STDOUT and STDERR. Which of the following commands will redirect both STDOUT and STDERR?

    1.  1>2
    2.  >2
    3.  2>&1
    4.  >>

31.  Which command can be run to determine the default priority for processes spawned by the current user?

    1.  prio
    2.  nice
    3.  renice
    4.  defpriority

32.  Which of the following egrep commands will examine /etc/passwd to find users who are using either /bin/bash or /usr/bin/zsh for their shell environment?

    1.  grep sh /etc/passwd
    2.  egrep '/*/.sh$' /etc/passwd
    3.  grep '/*/.=sh$' /etc/passwd
    4.  egrep '/*/..?sh$' /etc/passwd

33.  Which option to the man command accesses a different level of documentation, for example, system call documentation?

    1.  man 2 <argument>
    2.  progman <argument>
    3.  man --sys <argument>
    4.  man --list sys

34.  When editing with Vi, which command changes to insert mode and opens a new line below the current cursor location?

    1.  f
    2.  a
    3.  o
    4.  i

35.  Which kill signal can be sent in order to restart a process?

    1.  -HUP
    2.  -RESTART
    3.  -9
    4.  -SIG

36.  Which of the following commands will display the last 50 lines of your command history when using Bash, including commands from the current session?

    1.  bashhist 50
    2.  history 50
    3.  cat .bash_history
    4.  tail -f .bash_history

37.  You have backgrounded several tasks using &. Which command can be used to view the current list of running tasks that have been backgrounded?

    1.  procs
    2.  plist
    3.  jobs
    4.  free

38.  Which of the following commands searches each user’s .bash_history file to determine whether the user has invoked the sudo command?

    1.  find /home -name "bash_history" | grep sudo
    2.  find /home -name ".bash_history" | xargs grep sudo
    3.  find /home/.bash_history | xargs grep sudo
    4.  find /home -type history | xargs grep sudo

39.  Which command will watch the Apache log at /var/log/httpd/access.log and continually scroll as new log entries are created?

    1.  watch /var/log/httpd/access.log
    2.  tail /var/log/httpd/access.log
    3.  tail -f /var/log/httpd/access.log
    4.  mon /var/log/httpd/access.log

40.  You are debugging a configuration file and the daemon indicates there is a problem on line 932\. Which of the following commands will prepend line numbers onto the file?

    1.  lines
    2.  wc -l
    3.  newline
    4.  nl

41.  You receive a file with an .lzma extension. Which command can you use to decompress this file?

    1.  xz
    2.  lz
    3.  gz
    4.  bzip

42.  Which find command will locate files within the current directory that have been modified within the last 24 hours?

    1.  find ./ -type f -mtime 0
    2.  find ./ -type f -mtime 24
    3.  find ./ -type f -mtime +1
    4.  find ./ type -f time 24

43.  Which command will move all files with a .txt extension to the /tmp directory?

    1.  mv txt* tmp
    2.  move *txt /temp
    3.  mv *.txt /tmp
    4.  mv *.txt tmp

44.  Which command prints your current directory?

    1.  cwd
    2.  curdur
    3.  cd
    4.  pwd

45.  Assume that you have a file called zips.txt that contains several postal ZIP codes and you need to determine how many unique ZIP codes there are in the file. Which of the following commands can be used for that purpose?

    1.  sort zips.txt | uniq -c
    2.  uniq zips.txt
    3.  count zips.txt
    4.  cat zips.txt | uniq -c

46.  When using Bash, how would you execute the last command starting with a certain string, even if that command was not the last one that you typed?

    1.  Precede the command with ! and then the string to search for.
    2.  Search for the command in history.
    3.  Precede the command with a ? and then the string to search for.
    4.  This is not possible with Bash.

47.  Which command can be used to kill all processes by using their name?

    1.  killproc
    2.  killname
    3.  killall
    4.  kill -f

48.  You’re working with a large file in Vi and need to search for instances of a string earlier in the file. Which key will search backward in the file?

    1.  /
    2.  h
    3.  ?
    4.  x

49.  You need to declare a local environment variable that will then be available to child processes. Which of the following commands accomplishes this task?

    1.  ex
    2.  echo
    3.  dec
    4.  export

50.  You are creating a Bash shell script and need to output the current script name to the current terminal. Which of the following commands accomplishes this task?

    1.  cat <CMD>
    2.  echo $0
    3.  echo $SCRIPT
    4.  echo $PS1

51.  You have downloaded a file with a .gz extension. What is the most likely command that you will use to decompress this file?

    1.  unz
    2.  gunzip
    3.  hunzip
    4.  gzunzip

52.  You need to remove a single file from a directory if it exists but would like to be prompted for confirmation before doing so. Which option to the rm command causes the command to prompt for confirmation?

    1.  -a
    2.  -e
    3.  -i
    4.  -o

53.  You need to determine files that are sized above 1GB. Which of the following commands accomplishes this task?

    1.  find / -size +1G
    2.  find / -size 10000M
    3.  find / +1M
    4.  find / -size +1B

54.  Which option to cpio lists the files as it is operating on them?

    1.  -l
    2.  -v
    3.  -k
    4.  -s

55.  Which command is used to send contents of a bzip2 archive to STDOUT?

    1.  bzout
    2.  bzcat
    3.  bz2cat
    4.  bz2echo

56.  You are attempting to find more information about the jobs command; however, an Internet search was not particularly helpful because there are so many Linux-related jobs available. Additionally, you attempted to view the man page for the jobs command but it was not available. Which man page should you use to view more information on jobs?

    1.  jbs
    2.  procctl
    3.  bash
    4.  ps

57.  You need to start a process that cannot be sent or will not accept a SIGHUP signal. Which command should be used to start the process?

    1.  nosig
    2.  nohup
    3.  nokill
    4.  noproc

58.  You need to run a command periodically and examine its output in real time. Which of the following commands enables this scenario?

    1.  mon
    2.  procmon
    3.  pgrep
    4.  watch

59.  You would like to tail a log file to watch entries as they are being added to the log file. In addition, you would also like to work within the same terminal window or SSH (Secure Shell) session to add entries to another file at the same time. Which command can be used to create two sessions within the same terminal window?

    1.  screen
    2.  tmux
    3.  sess
    4.  termse

60.  You need to kill several processes at once. Rather than writing a complex ps-based command to do so, you can use which other command?

    1.  pkill
    2.  psk
    3.  pskill
    4.  prock

61.  You are using pgrep to find the process IDs for a given command. However, several other commands seem to also appear. Which option to pgrep enables matching against the full path of the process?

    1.  -f
    2.  -d
    3.  -o
    4.  -i

62.  You need to determine the exact command that will be run based on your current environment settings. Which command is used for this purpose?

    1.  what
    2.  which
    3.  find
    4.  ls

63.  An environment variable has been set on login, but you need to remove that variable temporarily for the current session. Which shell built-in command can be used for this purpose?

    1.  reset
    2.  unset
    3.  undo
    4.  clear

64.  You cannot find the man page of a command but you know the command exists. For example, the alias command exists but there is no man page for it. Which of the following commands could you execute to determine what type of command alias is?

    1.  type
    2.  cmd
    3.  uses
    4.  listr

65.  Which type of quotes are used so that variables are interpolated within a Bash shell script?

    1.  Escaped quotes
    2.  Single quotes
    3.  Double quotes
    4.  Side quotes

66.  Which of the following pagers includes the ability to search backward and forward as well as move backward and forward, line-by-line, and page-by-page?

    1.  more
    2.  mplus
    3.  less
    4.  catch

67.  You have a specialized need for outputting a file in octal format. Which command or series of commands can be used for this purpose?

    1.  oct
    2.  cat <file> | octalf
    3.  od
    4.  octf

68.  Which option to sha256sum causes the file to be read in binary mode?

    1.  -i
    2.  -b
    3.  -c
    4.  -p

69.  When operating in command mode, which keys enable you to move the cursor in the Vi editor?

    1.  a, s, d, f
    2.  h, j, k, l
    3.  q, w, e, r
    4.  z, x, c, v

70.  Which options to xz are functionally equivalent to the xzcat program?

    1.  decompress and output
    2.  output and format
    3.  decompress and stdout
    4.  stdout and format

71.  Which environment variable is used to control the default text editor used on a Linux system?

    1.  EDITOR
    2.  EDIT
    3.  TEXTEDITOR
    4.  DEFAULT_EDITOR

72.  You need to examine the seventh section of the manual page for regular expressions, or regex, on a Linux system. Which command displays the seventh section of the manual?

    1.  man regex -7
    2.  man regex 7
    3.  man --page 7 regex
    4.  man 7 regex

73.  Which of the following commands reprioritizes an already running process?

    1.  nice
    2.  renice
    3.  chnice
    4.  altnice

74.  The fgrep command is equivalent to running the grep command with which option?

    1.  -f
    2.  -F
    3.  -a
    4.  -E

75.  Which of the following regular expressions would find the pattern Steve or steve in a file when used with grep?

    1.  '[sS]teve'
    2.  '[S]*teve'
    3.  '^[Ss]teve'
    4.  '[$Steve]'

76.  Which of the following commands shows the currently running processes and their resource usage in real time, updated every few seconds?

    1.  nice
    2.  ps
    3.  top
    4.  procs

77.  You have been asked to create a compressed file that will be readable by those with other operating systems. Which tool can you use for this purpose?

    1.  gzip
    2.  bzip2
    3.  xz
    4.  tar

78.  You need to match files that begin with 201, as in 2017, 2018, 2019\. Which of the following wildcard specifications can be used?

    1.  201?
    2.  201$
    3.  201@
    4.  201]

79.  You need to break a large file into smaller pieces. Which command can be used for this purpose?

    1.  cut
    2.  split
    3.  dice
    4.  rem

80.  When examining the output from top, you see that a process has a value in the PR column of 20\. To what does the PR column refer?

    1.  The process ID
    2.  The process utilization
    3.  The process priority
    4.  The processor core on which the process is executing

81.  You need to cut or remove eight lines from a file while editing with Vi. Which combination should be used for this purpose?

    1.  d7
    2.  d8
    3.  r8
    4.  x7

82.  Which command is used in order to decompress a file that has been compressed with xz?

    1.  unxz
    2.  dexz
    3.  xzu
    4.  u2xz

83.  Which of the following commands uses 128-bit message digests?

    1.  sha256sum
    2.  sha512sum
    3.  sh128sum
    4.  md5sum

84.  You have several files that need to be combined, with a line from each file being appended onto a single line. Which command can be used for this purpose?

    1.  paste
    2.  comb
    3.  appfile
    4.  combo

85.  You need to run a command that is not inside your current path. Which of the following represents the typical method for doing so?

    1.  Use a fully qualified path for the command.
    2.  Set the PATH environment variable to include the correct path.
    3.  Restart the shell environment.
    4.  Restart the computer for settings to take effect.

86.  Which signal is used by default by the pkill command?

    1.  SIGKILL
    2.  SIGTERM
    3.  SIGHUP
    4.  SIGKS

87.  You are working with the jobs built-in command to display jobs. You would like to see only running jobs. Which option to the jobs built-in command will display only running jobs?

    1.  -s
    2.  -a
    3.  -l
    4.  -r

88.  Which option to the bunzip2 command sends output to STDOUT, much like the bzcat command?

    1.  -s
    2.  -o
    3.  -c
    4.  -d

# Chapter 4
Topic 104: Devices, Linux Filesystems, Filesystem Hierarchy Standard

**THE FOLLOWING EXAM OBJECTIVES ARE COVERED IN THIS CHAPTER:**

*   **![images](images/correction.png)  104.1 Create partitions and filesystems.**
    *   Key knowledge areas:
        *   Manage MBR and GPT partition tables.
        *   Use various mkfs commands to create various filesystems such as:
            *   ext2/ext3/ext4
            *   XFS
            *   VFAT
            *   exFAT
        *   Basic feature knowledge of Btrfs, including multi-device filesystems, compression, and subvolumes
    *   The following is a partial list of the used files, terms, and utilities:
        *   fdisk
        *   gdisk
        *   parted
        *   mkfs
        *   mkswap
*   **![images](images/correction.png)  104.2 Maintain the integrity of filesystems.**
    *   Key knowledge areas:
        *   Verify the integrity of filesystems.
        *   Monitor free space and inodes.
        *   Repair simply filesystem problems.
    *   The following is a partial list of the used files, terms, and utilities:
        *   du
        *   df
        *   fsck
        *   e2fsck
        *   mke2fs
        *   tune2fs
        *   xfs_repair
        *   xfs_fsr
        *   xfs_db
*   **![images](images/correction.png)  104.3 Control mounting and unmounting of filesystems.**
    *   Key knowledge areas:
        *   Manually mount and unmount filesystems.
        *   Configure filesystems mounting on bootup.
        *   Configure user mountable removable filesystems.
        *   Use labels and UUIDs for identifying and mounting filesystems.
        *   Awareness of systemd mount units
    *   The following is a partial list of the used files, terms, and utilities:
        *   /etc/fstab
        *   /media/
        *   mount
        *   umount
        *   blkid
        *   lsblk
*   **![images](images/correction.png)  104.4 Manage file permissions and ownership.**
    *   Key knowledge areas:
        *   Manage access permissions on regular and special files as well as directories.
        *   Use access modes such as suid, sgid, and the sticky bit to maintain security.
        *   Know how to change the file creation mask.
        *   Use the group field to grant file access to group members.
    *   The following is a partial list of the used files, terms, and utilities:
        *   chmod
        *   umask
        *   chown
        *   chgrp
*   **![images](images/correction.png)  104.5 Create and change hard and symbolic links.**
    *   Key knowledge areas:
        *   Create links.
        *   Identify hard and/or soft links.
        *   Copying versus linking files
        *   Use links to support system administration tasks.
    *   The following is a partial list of the used files, terms, and utilities:
        *   ln
        *   ls
*   **![images](images/correction.png)  104.6 Find system files and place files in the correct location.**
    *   Key knowledge areas:
        *   Understand the correct locations of files under the FHS.
        *   Find files and commands on a Linux system.
        *   Know the location and purpose of important file and directories as defined in the FHS.
    *   The following is a partial list of the used files, terms, and utilities:
        *   find
        *   locate
        *   updatedb
        *   whereis
        *   which
        *   type
        *   /etc/updatedb.conf

1.  Which option best describes the following output from the ls -la command:

    lrwxrwxrwx. 1 root root 35 Jul 8 2014 .fetchmailrc -> .configs/fetchmail/.fetchmailrc?

    1.  It is a file called .fetchmailrc that is linked using a symbolic link.
    2.  It is a file called .configs/fetchmail/.fetchmailrc that is owned by lrwxrwxrwx.
    3.  It is a directory called .fetchmailrc that is owned by user Jul.
    4.  It is a local directory called .configs/fetchmail/.fetchmailrc.

2.  Assuming that a USB disk contains a single partition and is made available on /dev/sdb, which command mounts the disk in /media/usb?

    1.  mount /dev/sdb1 /media/usb
    2.  usbconnect /dev/sdb0 /media/usb
    3.  mount /dev/sdb0 /media/usb
    4.  usbmount /dev/sdb1 /media/usb

3.  Which option within a partition-mounting command will cause the partition to be mounted in such a way as to prevent execution of programs?

    1.  execless
    2.  stoprun
    3.  noexec
    4.  norun

4.  When working with partitions on disk, you see the type 0x82\. Which type of partition is this?

    1.  Linux
    2.  Linux swap
    3.  NTFS
    4.  FAT

5.  Which partition type should be created for a Linux system, non-swap partition?

    1.  82
    2.  83
    3.  84
    4.  L

6.  Which command can be used to determine the location of a given executable that would be run if typed from your current environment and location?

    1.  which
    2.  what
    3.  whatis
    4.  when

7.  Which of the following commands will correctly change the group ownership of the file called a.out to users?

    1.  chgrp users a.out
    2.  chgrp a.out users
    3.  groupchg a.out users
    4.  grpchg users a.out

8.  Another administrator made a change to one of the local scripts used for administrative purposes. The change was also immediately reflected in your copy of the script. However, when examining the file with ls, you see that it appears to be a normal file. What is the likely cause of such a scenario?

    1.  The file was executed after edit.
    2.  The administrator copied the file to yours.
    3.  Your file is a hard link to the original.
    4.  The file has been restored from backup.

9.  Which of the following commands shows the usage of inodes across all filesystems?

    1.  df -i
    2.  ls -i
    3.  du -i
    4.  dm -i

10.  You’re running fsck on an ext3 filesystem, and the process is taking longer than expected and requiring input from the administrator to fix issues. What option could be added to fsck next time so that the command will automatically attempt to fix errors without intervention?

    1.  -o
    2.  -V
    3.  -y
    4.  -f

11.  Which of the following describes a primary difference between ext2 and ext3 filesystems?

    1.  ext3 was primarily a bug fix update to ext2.
    2.  ext3 includes journaling for the filesystem.
    3.  ext3 completely changed the tools needed for management of the disks.
    4.  ext3 filesystems have no significant differences.

12.  Which option to umask will display the permissions to be used in a Portable Operating System Interface (POSIX) format?

    1.  -P
    2.  -p
    3.  -S
    4.  -v

13.  Which option to ln creates a symlink to another file?

    1.  -sl
    2.  -s
    3.  -l
    4.  --ln

14.  Which of the following commands can be used if you need to locate various elements of a given command, such as its binaries and man pages?

    1.  whatis
    2.  find
    3.  whereis
    4.  ls

15.  Which option in /etc/updatedb.conf will remove a path from inclusion in the results?

    1.  PRUNEPATHS
    2.  EXCLUDEPATHS
    3.  INCLUDEEXCLUDE
    4.  SEPARATEPATH

16.  According to the filesystem hierarchy standard (FHS), what is the correct location for site-specific data for a server?

    1.  /etc
    2.  /var
    3.  /tmp
    4.  /srv

17.  Which of the following commands enables the sticky bit for a user on a file called homescript.sh?

    1.  chmod +sticky homescript.sh
    2.  chmod 755 homescript.sh
    3.  chmod u+s homescript.sh
    4.  chown u+sticky homescript.sh

18.  Which option to the mount command will mount all filesystems that are currently available in /etc/fstab?

    1.  -g
    2.  -a
    3.  -r
    4.  -y

19.  Which command is used to format a swap partition?

    1.  fdisk
    2.  mkswap
    3.  formatswap
    4.  format -s

20.  Which command and option is used to display the number of times that a filesystem has been mounted?

    1.  tune2fs -l
    2.  cat /etc/fstab
    3.  mount -a
    4.  less /etc/fsmnt

21.  Which option to xfs_metadump displays a progress indicator?

    1.  -g
    2.  -p
    3.  -f
    4.  -v

22.  The system is running out of disk space within the home directory partition and quotas have not been enabled. Which command can you use to determine the directories that might contain large files?

    1.  du
    2.  df
    3.  ls
    4.  locate

23.  Which file contains information about the filesystems to mount, their partitions, and the options that should be used to mount them?

    1.  /etc/filesystems
    2.  /etc/mounts
    3.  /etc/fstab
    4.  /srv/mounts

24.  According to the FHS, what is the proper mount point for removable media?

    1.  /etc
    2.  /srv
    3.  /tmp
    4.  /media

25.  Which file contains information on currently mounted filesystems, including their mount options?

    1.  /etc/mtab
    2.  /etc/fstab
    3.  /tmp/files
    4.  /etc/filesystems

26.  Which option to umount will cause the command to attempt to remount the filesystem in read-only mode if the unmounting process fails?

    1.  -o
    2.  -r
    3.  -f
    4.  -v

27.  The umask reports as 022\. What is the permission that will be in effect for a newly nonexecutable created file?

    1.  u+rw, g+r, w+r
    2.  755
    3.  022
    4.  a+r

28.  The locate command is reporting out-of-date information. Which command should be run in order to have the locate command update its database?

    1.  locatedb -u
    2.  locate -u
    3.  updatedb
    4.  updatelocate

29.  Which shell built-in command can be used to determine what command will be run?

    1.  type
    2.  when
    3.  find
    4.  help

30.  Which option to chown recursively changes the ownership?

    1.  -f
    2.  -R
    3.  -a
    4.  -m

31.  Which of the following represents the correct format for the /etc/fstab file?

    1.  <directory> <device> <type> <options>
    2.  <device> <type> <options>
    3.  <device> <type> <options> <directory> <dump> <fsck>
    4.  <filesystem> <mount point> <type> <options> <dump> <pass>

32.  Which of the following commands is used to identify the UUID for partitions?

    1.  blkid
    2.  ls
    3.  find
    4.  cat

33.  Which of the following describes the priority order for configuration files with systemd?

    1.  Files in /etc/, files in /run, and then files in /lib
    2.  Files in /run, files in /etc/, and then files in /lib
    3.  Files in /lib, files in /run, and then files in /etc
    4.  Files in /lib, files in /etc, and then files in /run

34.  Which options to the fsck command will find and automatically assume that it should repair errors that it finds?

    1.  -y
    2.  -vy
    3.  -my
    4.  -xy

35.  Which option to mke2fs sets the type of filesystem to be created?

    1.  -F
    2.  -a
    3.  -t
    4.  -e

36.  Which of the following files is the default configuration file for the autofs automounter?

    1.  /etc/autofs
    2.  /etc/auto.master
    3.  /etc/autofs.conf
    4.  /etc/automounter.conf

37.  Which of the following commands is used to create an ISO filesystem?

    1.  mkiso
    2.  mkfsiso
    3.  mkisofs
    4.  isofs-mk

38.  Which option to the tune2fs command sets the maximum mount count before the system will automatically run fsck on the partition on boot?

    1.  -b
    2.  -c
    3.  -C
    4.  -a

39.  Which option to the mount command can be used to simulate the mount process without actually mounting the filesystem?

    1.  -q
    2.  -v
    3.  -l
    4.  -f

40.  When viewing /proc/mounts, you see a filesystem with the letters ro in the fourth column. To what do the letters ro refer?

    1.  relative option
    2.  realtime option
    3.  read-only
    4.  relative-only

41.  Which option to dumpe2fs displays the bad blocks for a given partition?

    1.  -bb
    2.  -C
    3.  -b
    4.  -f

42.  Which of the following filesystem types features copy-on-write?

    1.  ext3
    2.  ext4
    3.  FAT
    4.  Btrfs

43.  Which of the following commands displays filesystem geometry for an XFS filesystem?

    1.  xfsinfo
    2.  xfs_info
    3.  xfs -info
    4.  xfs --info

44.  Which of the following commands can be used to display information such as the UUID for partitions on a system?

    1.  blkid
    2.  blockdev
    3.  devinfo
    4.  uuidinfo

45.  Which option to the umount command will cause it to unmount only filesystems of the specified type?

    1.  -v
    2.  -f
    3.  -t
    4.  -a

46.  Which command causes unwritten data to be written to disk immediately?

    1.  write
    2.  wrnow
    3.  connwrite
    4.  sync

47.  Which option to xfs_check is used to verify a filesystem that is stored in a file?

    1.  -v
    2.  -a
    3.  -f
    4.  -d

48.  Which option to debugfs causes the filesystem to be opened in read-write mode rather than the default read-only?

    1.  -rw
    2.  -w
    3.  -r
    4.  -n

49.  Which daemon is responsible for monitoring Self-Monitoring, Analysis, and Reporting Technology (SMART)-compatible hard drives?

    1.  smartmon
    2.  smarty
    3.  sartd
    4.  smartd

50.  When checking an ext3 filesystem, which option to the fsck.ext3 command causes it to run the check even if the filesystem is apparently marked as clean?

    1.  –f
    2.  -m
    3.  -a
    4.  -c

51.  You are performing an xfsrestore. The xfsdump was executed with a block size of 4MB. Which option do you need to invoke on xfsrestore in order for it to successfully use this dump?

    1.  -b 4M
    2.  -g 1M
    3.  -i 1M
    4.  -k 1028K

52.  You see the word *defaults* within /etc/fstab. Which options are encompassed within the defaults?

    1.  ro, exec, auto
    2.  rw, suid, dev, exec, auto, nouser, async
    3.  rw, exec, auto, nouser, async
    4.  rw, exec, nouser, async, noauto, suid

53.  Which of the following commands creates a btrfs subvolume?

    1.  btrfs create subvolume
    2.  btrfs subvolume create
    3.  btrfs sv create
    4.  btrfs svcreate

54.  Which of the following options to xfsdump sets the maximum size for files to be included in the dump?

    1.  -p
    2.  -s
    3.  -z
    4.  -b

55.  Which option to the tune2fs command sets the behavior when a filesystem error occurs?

    1.  -f
    2.  -d
    3.  -e
    4.  -k

56.  The /etc filesystem has been mounted as a read-only for a recovery process. You need to mount another partition. Which option to the mount command causes it to not write to /etc/mtab?

    1.  -a
    2.  -m
    3.  -b
    4.  -n

57.  Which of the following commands deactivates swap space?

    1.  swapoff
    2.  swap -off
    3.  unmountswap
    4.  uswap

58.  Within the [mount] section of a systemd mount unit, which directive specifies the location for mounting the chosen filesystem?

    1.  Where=
    2.  Location=
    3.  List=
    4.  Dest=

59.  Which of the following commands can be used to format a FAT filesystem?

    1.  mkfs.fat
    2.  mkfs -f
    3.  mkfs --fat
    4.  mkfat

60.  Which of the following commands adds a journal to an existing ext2 filesystem?

    1.  tune2fs -jrn
    2.  e2fs -x
    3.  tune3fs
    4.  tune2fs -j

61.  Which of the following commands creates a snapshot of a btrfs subvolume?

    1.  btrfs subvolume snapshot
    2.  btrfs snapshot --create
    3.  btrfs create snapshot
    4.  btrfs --create

62.  Which option to xfs_repair will force log zeroing even if there may be metadata within the log?

    1.  -L
    2.  -v
    3.  -d
    4.  -V

63.  Which of the following commands mounts a filesystem in read-only mode?

    1.  mount read-only
    2.  mount --read
    3.  mount -o ro
    4.  mount -or

64.  When you are using tune2fs to set an extended option such as stripe_width, which command-line option is needed to signify that an extended option follows?

    1.  -extend
    2.  -E
    3.  -e
    4.  -f

65.  Which utility is used for formatting GPT disks?

    1.  gdisk
    2.  gptdisk
    3.  gpdisk
    4.  pgdisk

66.  What is the maximum size of a partition on an MBR-formatted disk?

    1.  2TB
    2.  4TB
    3.  2MB
    4.  512TB

67.  Which option to mkfs.ext4 can be used to prevent reservation of blocks for system or superuser use?

    1.  -r 0
    2.  -r 0b
    3.  -m 0
    4.  -m 0b

68.  What is the default time in seconds that xfs_fsr will use to reorganize a filesystem?

    1.  3600
    2.  7200
    3.  86400
    4.  5150

69.  A user who is a member of the custom admins group is attempting to read the contents of a file but is not the owner of the file. Rather than granting sudo access to this file, what is another way to grant read access, assuming that the file is currently marked with 640 permissions? Note that you should choose the most appropriate answer to fulfill the need while minimizing additional privileges.

    1.  Grant root access to the user.
    2.  Run chmod 777 on the file.
    3.  Use chgrp to change group ownership to admins.
    4.  Use chown to change the ownership of the file to the individual user.

70.  Which option to lsblk shows empty devices?

    1.  -g
    2.  -a
    3.  -r
    4.  -y

71.  The /media/ mount point is used frequently for which types of devices?

    1.  Hard drives
    2.  SAN
    3.  NAS
    4.  USB devices

72.  Which of the following commands is used to format an exFAT filesystem?

    1.  mkexfat
    2.  mkfat.ex
    3.  mkfs.exfat
    4.  mkfs2.exf

73.  Which of the following commands is used for debugging an XFS-formatted filesystem?

    1.  debug_xfs
    2.  xfs_debug
    3.  xfs_db
    4.  debugxfs

74.  You’re working with an ext2 filesystem and you suspect the superblock is corrupted. Which option to e2fsck enables you to specify the location of an alternate superblock?

    1.  -B
    2.  -s
    3.  -b
    4.  -o

75.  Which option to df shows the numerical output in larger size increments, like MB, GB, TB, and so on rather than in bytes?

    1.  -h
    2.  -m
    3.  -n
    4.  -s

76.  Assuming the use of Bash for the shell, in which file can the umask be set such that the file creation mask is set automatically on login?

    1.  /etc/umask.def
    2.  /etc/profile
    3.  /etc/bash.d/umask
    4.  /etc/bash.umask

77.  You need to enable two users to edit the same file but keep their own individual changes. Another administrator suggested making a symbolic link for the file. Is a symbolic link the appropriate solution for this scenario and, if not, what is?

    1.  A symbolic link is not appropriate because the users cannot keep their own changes. A copy would be a better option.
    2.  A symbolic link is appropriate here because each user can access the file, assuming write permissions.
    3.  A symbolic link is not appropriate given that the users will not have permissions on symbolic links. Linux cannot meet the scenario described.
    4.  A symbolic link is appropriate because symbolic links have the ability to do version control, thus enabling the scenario.

78.  You have deleted a user from the system and want to determine if this user still has files on the system. Which command will fulfill this scenario?

    1.  locate <user>
    2.  find -uid <uid>
    3.  find -user <user>
    4.  fileloc -user <user>

79.  You need to update the locate database. Which of the following commands is used for this purpose?

    1.  updatedb
    2.  locatedb
    3.  updlocdb
    4.  locdbupd

80.  Which option to lsblk shows the UUID of each filesystem?

    1.  –u
    2.  -f
    3.  -o
    4.  -a

81.  Which option to mkswap checks the device for bad blocks before formatting?

    1.  -b
    2.  -B
    3.  -c
    4.  -d

82.  You are examining output from ls -la and one file contains the permissions -rwSrw-r--. To what does the *S* refer?

    1.  Specific execute
    2.  Source formatting
    3.  Selective execution
    4.  Sticky bit

83.  You need to change file permissions to be setgid for a file called sync.sh. The file is normally permission 755. Which of the following commands accomplishes this task?

    1.  chmod 2775 sync.sh
    2.  chmod u+s sync.sh
    3.  chmod 2755 sync.sh
    4.  chmod 4755 sync.sh

84.  Which of the following commands finds files with a .sql extension across the entire filesystem?

    1.  find . -name "*.sql"
    2.  find /root -ext sql
    3.  find / -name "*.sql"
    4.  find / -exten ".sql"

85.  When working with /etc/fstab to mount by UUID, which syntax is correct as the first column in /etc/fstab, assuming a UUID denoted by <UUID>?

    1.  <UUID>
    2.  UUID=<UUID>
    3.  ID=<UUID>
    4.  GPT=<UUID>

86.  Which option to du displays information on inode usage?

    1.  -i
    2.  -h
    3.  --inodes
    4.  -d

87.  Which of the following find commands will look for files that are over 1GB in size?

    1.  find -size +1G
    2.  find -size 1GB
    3.  find -fssize +1GB
    4.  find -filesize +1G

88.  You have a set of libraries that were installed into /usr/local/lib and would like to ensure that the libraries are also available in /usr/lib. What is the preferred way to make the libraries available in this location?

    1.  Copy the libraries.
    2.  Create a symbolic link.
    3.  Move the libraries.
    4.  Create a script to synchronize the libraries between the two locations with rsync.

# PART II
Exam 102-500

# Chapter 5
Topic 105: Shells and Shell Scripting

**THE FOLLOWING EXAM OBJECTIVES ARE COVERED IN THIS CHAPTER:**

*   **![images](images/correction.png)  105.1 Customize and use the shell environment.**
    *   Key knowledge areas:
        *   Set environment variables (e.g. PATH) at login or when spawning a new shell.
        *   Write bash functions for frequently used sequences of commands.
        *   Maintain skeleton directories for new user accounts.
        *   Set command search path with the proper directory.
    *   The following is a partial list of the used files, terms, and utilities:
        *   .
        *   source
        *   /etc/bash.bashrc
        *   /etc/profile
        *   env
        *   export
        *   set
        *   unset
        *   ∼/.bash_profile
        *   ∼/.bash_login
        *   ∼/.profile
        *   ∼/.bashrc
        *   ∼/.bash_logout
        *   function
        *   alias
*   **![images](images/correction.png)  105.2 Customize or write simple scripts.**
    *   Key knowledge areas:
        *   Use standard sh syntax (loops, tests).
        *   Use command substitution.
        *   Test return values for success or failure or other information provided by a command.
        *   Execute chained commands.
        *   Perform conditional mailing to the superuser.
        *   Correctly select the script interpreter through the shebang (#!) line.
        *   Manage the location, ownership, execution, and suid-rights of scripts.
    *   The following is a partial list of the used files, terms, and utilities:
        *   for
        *   while
        *   test
        *   if
        *   read
        *   seq
        *   exec
        *   ||
        *   &&

1.  Which of the following best describes the PS1 environment variable?

    1.  PS1 is used to set the location of the PostScript command.
    2.  PS1 is used to define the default shell prompt for bash.
    3.  PS1 is used as a per-system variable.
    4.  PS1 is user-defined and does not have a default value or setting.

2.  Which command is used to read and execute commands from a file in the Bash shell?

    1.  run
    2.  execute
    3.  source
    4.  func

3.  You need a command to be executed on logout for all users. Within which file should this be placed (assuming all users are using Bash)?

    1.  ∼/.bash_logout
    2.  /etc/bash.bash_logout
    3.  /home/.bash_logout
    4.  /etc/bash_logout

4.  Which of the following commands removes an environment variable that has been set?

    1.  profile --unset
    2.  env -u
    3.  set -u
    4.  import

5.  Which option to the unset command explicitly informs the command that the name given refers to a shell variable and not a function?

    1.  -a
    2.  -s
    3.  -v
    4.  -e

6.  Which of the following commands ensures that the -la options are used when the ls command is executed without other options?

    1.  alias ls="ls -la"
    2.  ln -s ls ls -la
    3.  alias "ls -la" = ls
    4.  set ls

7.  What is the order in which user configuration files are located on login to a Bash shell?

    1.  .bash_login, .profile, /etc/profile
    2.  .bash_profile, .bash_login, .profile
    3.  .profile, .bash_login, .bash_profile
    4.  .bash_login, .bash_profile, .profile

8.  Which variable within a Bash script is used to access the first command-line parameter?

    1.  $ARG
    2.  $CMD
    3.  $1
    4.  $ARG0

9.  Which of the following provides the end for an if conditional in a Bash script?

    1.  ex
    2.  }
    3.  ]
    4.  fi

10.  Which of the following commands will print a list of 6 numbers beginning at 0 within a Bash script?

    1.  list 0-5
    2.  seq 0 1 5
    3.  echo 0-5
    4.  seq 0 1 6

11.  When creating a shell script, which of the following commands is used to display the contents of variables?

    1.  var_dump
    2.  echo
    3.  ls
    4.  env

12.  A command has the following listing obtained with ls -la:

    *   -rwsr-xr-x 1 suehring suehring 21 Nov 2 13:53 script.sh
    *   What does the s denote within the user permissions in the listing?

    1.  The suid bit has been set for this program.
    2.  This is a symlink.
    3.  The file will not be executable.
    4.  The file is a special system file.

13.  Which of the following commands will execute a script and then exit the shell?

    1.  run
    2.  source
    3.  ./
    4.  exec

14.  Which sequence of characters will execute two commands but only if the first command exits successfully?

    1.  --
    2.  &*
    3.  &&
    4.  &

15.  Which command within a shell script awaits user input and places that input into a variable?

    1.  exec
    2.  get
    3.  read
    4.  prompt

16.  What characters are used to mark a sequence of commands as a function in a Bash script?

    1.  Parentheses to declare the function (optional) and curly braces to contain the commands
    2.  Curly braces to declare the function and parentheses to contain the commands
    3.  Square brackets to declare the function and curly braces to contain the commands
    4.  Runquotes to denote the function

17.  Which character sequences denote an alternate command to execute if the preceding command does not exit successfully?

    1.  &&
    2.  --
    3.  ||
    4.  EL

18.  Which keyword(s) is/are used to begin an alternate condition within a Bash script?

    1.  if
    2.  else if
    3.  elif
    4.  elsif

19.  Which of the following commands removes a currently defined aliased command?

    1.  remove
    2.  rm
    3.  unalias
    4.  delete

20.  When sourcing a file in Bash, which chmod command would be necessary to provide the minimum privileges in order for the file to be sourced correctly, assuming that your current user owns the file?

    1.  chmod 600
    2.  chmod 755
    3.  chmod 777
    4.  chmod 400

21.  Assuming that a space-separated list of values has been defined as LIST="one two three four", which of the following for loop constructs will iterate through the elements in the list?

    1.  for LIST
    2.  for VAR in LIST
    3.  for VAR in $LIST
    4.  for $LIST -> $VAR

22.  Which test within a shell script while loop will examine one value to see if it is less than another?

    1.  -less
    2.  -lessThan
    3.  -lt
    4.  -lthan

23.  Which of the following tests will determine if a file exists in the context of a shell script?

    1.  -a
    2.  -e
    3.  -m
    4.  -i

24.  Within which directory should you place files to have them automatically copied to a user’s home directory when the user is created?

    1.  /etc/userhome
    2.  /etc/templateuser
    3.  /etc/skel
    4.  /home/skel

25.  Which option to bash will cause the shell to be executed without reading the initialization files?

    1.  --no-rc
    2.  --no-init
    3.  --norc
    4.  --rc-none

26.  Which of the following creates an array in a Bash script?

    1.  ARRAY=(val1 val2)
    2.  ARRAY = "val1 val2"
    3.  ARRAY_PUSH($ARRAY,"val1","val2");
    4.  ARRAY{0} = "val1"

27.  Which option of declare displays output in a way that could then be used as input to another command?

    1.  -o
    2.  -n
    3.  -p
    4.  -m

28.  You need to create a function that will be available each time that you log in to the system. Within which file should this function be placed?

    1.  .bash_profile
    2.  .rc
    3.  /etc/profile
    4.  .bash_run

29.  Which shell built-in command is used to display a list of read-only variables?

    1.  ro
    2.  readonly
    3.  env-ro
    4.  ro-env

30.  Which characters are used to denote the beginning and end of the test portion of a while loop in a shell script?

    1.  Parentheses ( )
    2.  Curly braces { }
    3.  Square brackets [ ]
    4.  Double-quotes " "

31.  When using the test built-in with one argument, what will be returned if its argument is not null?

    1.  false
    2.  true
    3.  unknown
    4.  -1

32.  Which environment variable is used when changing directory with the tilde character, such as cd ∼ ?

    1.  HOMEDIR
    2.  HOMEPATH
    3.  HOME
    4.  MAILPATH

33.  Which environment variable can be set if you want to automatically log users out of their shell after a certain period of inactivity?

    1.  TIMEOUT
    2.  TMOUT
    3.  TO
    4.  IDLETIME

34.  When using a case statement within a shell script, which sequence denotes the ending of the case/switch statement?

    1.  caseend
    2.  esac
    3.  endcase
    4.  }

35.  Which of the following commands will obtain the date in seconds since the epoch and place it into a variable called DATE within a shell script?

    1.  DATE="$(date +%s)"
    2.  DATE="date"
    3.  DATE="$(date)";
    4.  DATE="$date %s"

36.  Assume that you have a variable called $FILEPATH within a Bash shell script. Which characters can be used to ensure that the variable will be interpolated correctly regardless of where the variable appears within the script?

    1.  Dollar sign: $FILEPATH
    2.  Curly braces: ${FILEPATH}
    3.  Parentheses: $(FILEPATH)
    4.  Square brackets: $[FILEPATH]

37.  Which sequence is used to mark the beginning and end of the commands to execute within a for loop in a shell script?

    1.  Curly braces: { }
    2.  The keywords do and done
    3.  Semicolons: ;
    4.  Tabs

38.  Which of the following tests will determine if a file exists and can be read by the user executing the test?

    1.  -e
    2.  -m
    3.  -a
    4.  -r

39.  Which option of the declare command will create a variable that is read-only?

    1.  -r
    2.  -ro
    3.  -p
    4.  -x

40.  Which character sequence is used to provide a default case when used within a case statement in a shell script?

    1.  default:
    2.  =)
    3.  -->
    4.  *)

41.  Which character sequence can be used for command substitution in Bash?

    1.  Backquotes: ` `
    2.  Single quotes: ‘ '
    3.  Double quotes: ""
    4.  Backslashes: \\

42.  When using a while loop in Bash, which character sequence marks the end of the loop?

    1.  elihw
    2.  done
    3.  end
    4.  od

43.  Which operator is used to test if a value is greater than or equal to something in a Bash script?

    1.  !=
    2.  >=
    3.  =>
    4.  >>

44.  You are working with a shell script called listusers and the script does not execute with the error "permission denied". What could be the possible cause of this issue?

    1.  The script should have an .sh extension.
    2.  The script contains a syntax error.
    3.  The script does not have its execute permission set correctly.
    4.  The script is named with lowercase letters.

45.  Which option to the export built-in command makes names available as functions to child processes?

    1.  -m
    2.  -e
    3.  -w
    4.  -f

46.  If a variable has been created using the set command, which command can be used to remove the variable?

    1.  remove
    2.  del
    3.  delete
    4.  unset

47.  Which of the following files is a systemwide initialization script for Bash?

    1.  /etc/bash.bashrc
    2.  /etc/bash.init
    3.  /etc/bash.cfg
    4.  /etc/bash/bash.init

48.  Which option to the set command enables debugging output?

    1.  -d
    2.  +d
    3.  -x
    4.  +x

49.  Which of the following files is executed with every interactive Bash shell invocation?

    1.  /etc/bash.d
    2.  /etc/bash.interactive
    3.  ∼/.bash_inter
    4.  ∼/.bashrc

50.  Which keyword declares a block of code to be a function in a Bash script?

    1.  function
    2.  repeat
    3.  func
    4.  block

51.  Which of the following statements adds the /srv/bin path to the path for a Bash shell?

    1.  PATH=/srv/bin
    2.  PATH=$PATH:/srv/bin
    3.  PATH = /srv/bin
    4.  PATH=/srv/bin;$PATH

52.  Which variable is available to a Bash script and contains the name of the script itself?

    1.  $SCR
    2.  $SCRIPT
    3.  $CMD
    4.  $0

53.  Which option to the seq command sets a delimiter of a space between the numbers 1 through 5?

    1.  seq -s ' ' 1 5
    2.  seq -d ' ' 1 5
    3.  seq 1 5
    4.  seq -m 1 5

54.  Which file test is used to determine if you are the owner of the file being tested?

    1.  -m
    2.  -k
    3.  -w
    4.  -O

55.  When testing a return value in a Bash script, which exit code indicates success?

    1.  0
    2.  1
    3.  2
    4.  C

56.  You have created a README file and placed it into /etc/skel so that users get the file in their home directories. The file is missing from some home directories on the system. Which of the following best explains this scenario?

    1.  The file is not copied automatically for existing users.
    2.  The file is too big for a user’s home directory.
    3.  The file already exists.
    4.  The file needs a file extension.

57.  You have a Bash script that uses the following find command:

    *   find . -name ".git" -type d
    *   When another administrator uses the script, it does not find all of the indicated directories. Which of the following is the best explanation for this scenario?

    1.  The find command is tied to specific users.
    2.  The find command cannot find directories beginning with a dot.
    3.  The find command begins the search in the current directory.
    4.  The find command cannot find directories.

58.  You have specialized software that needs to be installed with an empty environment. Which option to the env command can be used to meet this requirement?

    1.  -e
    2.  –i
    3.  -f
    4.  -c

59.  Which option enables debugging when used on the interpreter (#!) line within a Bash script?

    1.  -x
    2.  -d
    3.  -a
    4.  -f

60.  Which of the following will output the number 5 as part of a Bash script?

    1.  echo 2+3
    2.  echo 2 + 3
    3.  echo $[2+3]
    4.  echo ${2+3}

61.  You need to prompt the user to enter two values in a Bash script and capture them in variables VAL1 and VAL2. Which of the following commands can be used for this purpose?

    1.  read VAL1 VAL2
    2.  prompt VAL1 VAL2
    3.  VAL1=$0 VAL2=$1
    4.  (VAL1 VAL2) = prompt

62.  Which option to the export built-in command removes a variable from being exported?

    1.  -m
    2.  -o
    3.  -r
    4.  -n

63.  Which of the following tests the return value from the previous command to see if the command was successful?

    1.  if [ $? -eq 0 ];
    2.  if [ $? = 0 ];
    3.  if ($PREV == 0) {
    4.  if [ $RETV === 0 ];

64.  You have a file containing bash functions. Which command can be used to add these functions to the current environment?

    1.  function
    2.  include
    3.  require
    4.  source

65.  Which chmod command grants the user execute permission on a script?

    1.  chmod user += exec
    2.  chmod u+x
    3.  chmod 644
    4.  chmod u+all

66.  Which find command will locate all files named with an .sh extension?

    1.  find / -name "*.sh"
    2.  find / -name "*.sh" -type f
    3.  find / -name "*.sh" -type d
    4.  find ./ -name "*.sh"

67.  Which unset option can be used to remove a function from being defined?

    1.  -r
    2.  -a
    3.  -f
    4.  -g

68.  When setting the shebang line of a shell script, which of the following commands will help to determine the location of the interpreter automatically?

    1.  #!/usr/bin/env bash
    2.  #!/bin/bash
    3.  #!env
    4.  /bin/int bash

69.  Which mathematical operator is used for division within a Bash script?

    1.  \
    2.  /
    3.  *
    4.  //

70.  You need to send an email to the superuser if a command is successful. Which of the following commands will send mail from a Bash script?

    1.  smtpsend
    2.  mailx
    3.  sendm
    4.  mailsend

71.  Which file test operator is used to determine if the file is not zero size?

    1.  -d
    2.  -e
    3.  -f
    4.  -s

72.  You have created an alias but it is gone the next time you log in. Which of the following best explains this scenario?

    1.  The alias was not placed into an initialization script.
    2.  The alias was invalid.
    3.  The command is not valid for which the alias was created.
    4.  The alias created an invalid symlink.

73.  Which of the following is valid syntax to create a variable named FILENAME in a Bash script and set it equal to the second command-line argument?

    1.  $FILENAME = $2
    2.  FILENAME=1
    3.  FILENAME = $(2)
    4.  FILENAME=$2

74.  You are working with a user who is reporting that their environment does not have certain variables defined, but other users do have those same variables available within their environment on login. The issue was not corrected by having the user log out and then log in again, and you can see their successful login. What is the most likely explanation for this issue?

    1.  The user has logged in from the console.
    2.  The user is using a different shell.
    3.  The user has removed the environment variables manually.
    4.  The user is logging in to a different system.

75.  Which environment variable contains the username of the currently logged-in user?

    1.  LOGNAME
    2.  LOGIN
    3.  LOGGEDIN
    4.  LOGINUSER

76.  Which file test operator is used to determine if the file is a symbolic link?

    1.  -h
    2.  -p
    3.  -S
    4.  -t

77.  Which option to the readonly command marks a function as being read-only?

    1.  -a
    2.  -r
    3.  -f
    4.  -p

78.  Which find command will locate all files where the users have the execute bit set?

    1.  find ./ -type f -perm 700
    2.  find / -type f -perm -u+x
    3.  find / -type f -perm 777
    4.  find / -type f -perm -execuser

79.  According to the FHS, which of the following directories is used for local binaries?

    1.  /usr/local/bin
    2.  /usr/bin
    3.  /usr/sbin
    4.  /home/scripts

80.  Which key sequence can be used to terminate a Bash script?

    1.  Ctrl+d
    2.  Ctrl+l
    3.  Ctrl+a
    4.  Ctrl+c

81.  You need to view the current environment variables in a single line rather than with newlines separating each variable. Which option to the env command can be used for this purpose?

    1.  -n
    2.  -0
    3.  -c
    4.  -e

82.  You are attempting to copy several files, but the cp command keeps asking for confirmation before overwriting. Which of the following best describes the most likely cause?

    1.  The cp command has been compiled to ask for confirmation.
    2.  The cp command always prompts for confirmation.
    3.  The cp command cannot be used for the purpose described.
    4.  The cp command has been aliased to include the -i option.

83.  You receive an exit code of 1 when working with the grep command in a Bash script. What does exit code 1 mean with grep?

    1.  Error
    2.  Success
    3.  Search pattern not found
    4.  Search pattern found

84.  Which of the file test operators is used to determine if a file is a directory?

    1.  -e
    2.  -d
    3.  -w
    4.  -a

85.  Which of the following statements prepends the /usr/local/bin path to the path for a Bash shell?

    1.  $PATH=/usr/local/bin:$PATH
    2.  PATH=/usr/local/bin:$PATH
    3.  PATH=$PATH:/usr/local/bin
    4.  PATH=$PATH;/usr/local/bin

86.  Which looping construct is executed at least once in a Bash script?

    1.  while
    2.  for
    3.  until
    4.  case

87.  Which character or character sequence is equivalent to the source built-in in Bash?

    1.  <>
    2.  .
    3.  ->
    4.  %

88.  Which option to the export built-in command displays the list of exported variables?

    1.  -p
    2.  -a
    3.  -t
    4.  -d

89.  Which character or character sequence denotes the beginning of a while loop in a Bash script?

    1.  start
    2.  {
    3.  >>
    4.  do

# Chapter 6
Topic 106: User Interfaces and Desktops

**THE FOLLOWING EXAM OBJECTIVES ARE COVERED IN THIS CHAPTER:**

*   **![images](images/correction.png)  106.1 Install and configure X11.**
    *   Key knowledge areas:
        *   Understanding of the X11 architecture
        *   Basic understanding and knowledge of the X Window configuration file
        *   Overwrite specific aspects of Xorg configuration, such as keyboard layout.
        *   Understand the components of desktop environments, such as display managers and window managers.
        *   Manage access to the X server and display applications on remote X servers.
        *   Awareness of Wayland
    *   The following is a partial list of the used files, terms, and utilities:
        *   /etc/X11/xorg.conf
        *   /etc/X11/xorg.conf.d/
        *   ~/.xsession-errors
        *   xhost
        *   xauth
        *   DISPLAY
        *   X
*   **![images](images/correction.png)  106.2 Graphical desktops**
    *   Key knowledge areas:
        *   Awareness of major desktop environments
        *   Awareness of protocols to access remote desktop sessions
    *   The following is a partial list of the used files, terms, and utilities:
        *   KDE
        *   Gnome
        *   Xfce
        *   X11
        *   XDMCP
        *   VNC
        *   Spice
        *   RDP
*   **![images](images/correction.png)  106.3 Accessibility**
    *   Key knowledge areas:
        *   Basic knowledge of visual settings and themes
        *   Basic knowledge of assistive technology
    *   The following is a partial list of the used files, terms, and utilities:
        *   High contrast/large print desktop themes
        *   Screen reader
        *   Braille display
        *   Screen magnifier
        *   On-screen keyboard
        *   Sticky/repeat keys
        *   Slow/bounce/toggle keys
        *   Mouse keys
        *   Gestures
        *   Voice recognition

1.  Within which configuration file is the greeter configured for LightDM?

    1.  /etc/lightdm/lightdm.conf
    2.  /etc/lightdm/greeter.conf
    3.  /etc/lightdm.conf
    4.  /var/lib/lightdm/lightdm.conf

2.  Which section in /etc/X11/xorg.conf is used to describe configurations for a given graphics card and monitor pair?

    1.  Server
    2.  Screen
    3.  VidMode
    4.  Video

3.  When you’re setting the frequency options for a given monitor, which of the following is not an available frequency unit?

    1.  uHz
    2.  MHz
    3.  kHz
    4.  M

4.  Which command on a systemd-based system is used to disable booting into a GUI?

    1.  systemctl gui-boot disable
    2.  systemctl set-default boot-gui false
    3.  systemctl set-default multi-user.target
    4.  systemctl set-default-multi false

5.  Assuming X forwarding has been enabled on the SSH server, which environment variable is used to set the location for newly spawned windows from within an SSH session?

    1.  DISPLAY
    2.  XTERMINAL
    3.  XTERM
    4.  XDISP

6.  Within the greeter section of a display manager such as GNOME Display Manager (GDM), which option sets the welcome message for users logging in locally?

    1.  LoginMessage
    2.  Login
    3.  WinGreet
    4.  Welcome

7.  Within GNOME, enabling sticky keys can be done by pressing which key five times in a row?

    1.  Ctrl
    2.  Enter
    3.  Shift
    4.  Tab

8.  Which option in the Module section of the xorg.conf configuration file causes a default module to be unloaded or not loaded by default?

    1.  Disable
    2.  Unload
    3.  LoadDisable
    4.  DisableLoad

9.  Which program is used in a GNOME environment as a screen reader?

    1.  Orca
    2.  Screed
    3.  Screen
    4.  Reader

10.  Assuming a monitor that is currently set at 1024×768, which command will change the screen resolution so that icons and other elements appear larger?

    1.  xterm -r 0
    2.  xset res 1024x768
    3.  xrandr -s 800x600
    4.  xVGA

11.  LightDM typically allows guest login by default. Which configuration option within SeatDefaults changes this to disallow guests?

    1.  guest-login=false
    2.  guest=false
    3.  allowg=false
    4.  allow-guest=false

12.  When using XFree86 as the X server, which command will cause the X server to query for hardware and create a new configuration file?

    1.  XFree86 --newconfig
    2.  XFree86 --query
    3.  XFree96 -configure
    4.  xf -config

13.  Which configuration option for X is used to configure the keyboard model?

    1.  XkbLayout
    2.  XkbModel
    3.  XkbType
    4.  XkbInput

14.  Which configuration line with a Monitor section of an X server configuration file will set the vertical refresh rate between 55 and 75 hertz?

    1.  Vert 55-75
    2.  VertRefresh 55.0 - 75.0
    3.  VertSync 55.0 - 75.0
    4.  RefreshMode 55.0 - 75.0

15.  Within which file can a user place commands for executing X clients?

    1.  ∼/.xclients
    2.  ∼/.xsess.rc
    3.  ∼/.xsessrc
    4.  ∼/.xsession

16.  Which AccelerationProfile for an input device such as a mouse enables linear acceleration (more speed and more acceleration)?

    1.  0
    2.  –1
    3.  6
    4.  7

17.  Which of the following directories is used by an Xorg-based server for storage of fonts?

    1.  /usr/share/fonts
    2.  /usr/X11/fonts
    3.  /etc/fonts
    4.  /var/font/xorg

18.  Native support for a Braille display requires a minimum of which kernel version?

    1.  2.2.0
    2.  2.4.22
    3.  2.6.26
    4.  3.2.1

19.  Which configuration option in an xorg.conf file can be set to prevent a user from changing video modes using the Ctrl+Alt+Keypad-Plus and Ctrl+Alt+Keypad-Minus?

    1.  DontZoom
    2.  Modes=No
    3.  NoModeSwitch
    4.  DontZap

20.  In which location does the xauth utility look for the X authority file?

    1.  ∼/.Xauth
    2.  ∼/.xauth.cfg
    3.  ∼/.Xauthority
    4.  ∼/.xau

21.  Access to hosts controlled with XDMCP is configured in which file?

    1.  xdmcp.access.conf
    2.  XDMCPAccess.cfg
    3.  Xaccess
    4.  XDaccess.conf

22.  When using KDE, which program provides magnification functionality?

    1.  xmag
    2.  mag
    3.  pmag
    4.  kmag

23.  Which signal is used by an X server to cause a clean exit?

    1.  SIGTERM
    2.  SIGKILL
    3.  SIGCLEAN
    4.  SIGEX

24.  Within GNOME, which section of GNOME Control Center is used to choose a high-contrast theme?

    1.  Display
    2.  Appearance
    3.  Locale
    4.  Contrast

25.  Which of the following best describes the concept of a mouse gesture?

    1.  A mouse gesture enables special clicks, such as a right-click context menu.
    2.  A mouse gesture facilitates the use of programs by moving the mouse in a certain way.
    3.  A mouse gesture is used for login purposes.
    4.  A mouse gesture is used to capture screenshots.

26.  In GNOME 3.9 or later, which keyboard shortcut activates the screen reader?

    1.  Super+R
    2.  Super+S
    3.  Ctrl+Super+S
    4.  Alt+Super+S

27.  Assume that the display manager has been disabled on boot. Which command can be used after login to start the X server?

    1.  xs
    2.  xstart
    3.  X -start
    4.  startx

28.  Which option in an xorg.conf file configures the amount of time before the screen goes into blank mode but does not go into standby and is available on non-Display Power Management Signaling (DPMS)-capable monitors?

    1.  StandbyTime
    2.  BlankTime
    3.  SuspendTime
    4.  OffTime

29.  Which of the following commands helps you to determine information about a given window within an X session, including information on the window size and its position?

    1.  xkbinfo
    2.  xdspy
    3.  xwininfo
    4.  xver

30.  Which option/button on the GNOME On-Screen Keyboard (GOK) is used show the keys that would be used in place of a mouse?

    1.  Mouse
    2.  MouseKeys
    3.  Movement
    4.  Compose

31.  Which of the following commands allows a host named cwa to connect to the X server?

    1.  xconnect cwa
    2.  xterm +cwa
    3.  xhost +cwa
    4.  xf cwa

32.  Which of the following options in the client SSH configuration file needs to be enabled so that X sessions can be sent over an SSH connection?

    1.  X11Connect yes
    2.  ForwardX11 yes
    3.  ForwardX yes
    4.  XForward yes

33.  Which configuration option in a Files section of an xorg.conf configuration file can be used to add a path in which the server will search for fonts?

    1.  FontSection
    2.  Fonts
    3.  FontLoc
    4.  FontPath

34.  Which assistive technology is used to provide an input method for users who cannot type but can use a pointer, such as a mouse?

    1.  Keyboard
    2.  Sticky keys
    3.  Mouse keys
    4.  On-screen keyboard

35.  Which environment variable can be used to specify the location of a user’s xauth authority file?

    1.  XAUTH
    2.  USERXAUTH
    3.  XAUTHORITY
    4.  xauthloc

36.  When using LightDM, which key combination is used to revert back to a terminal?

    1.  Alt+Ctrl+F2
    2.  Alt+Ctrl+F1
    3.  Ctrl+F1
    4.  Ctrl+Esc

37.  Which option in the LightDM configuration enables automatic login for a specific user?

    1.  auto-login
    2.  autologin-user
    3.  autologin
    4.  auto-login-user

38.  Which of the following is a legacy utility that can be used to set accessibility options on older systems?

    1.  Xaccessibility
    2.  Xas
    3.  AccessX
    4.  setX

39.  Which command, when executed on a remote host, will send the display of X programs to the local client? (Assume Bash is used as the shell.)

    1.  export DISPLAY
    2.  env DISPLAY
    3.  setx HOST
    4.  export XHOST

40.  Which option in GOK is used to display the keys that correspond to a given application’s menu?

    1.  Menus
    2.  Activate
    3.  MenuKeys
    4.  Keys

41.  Which directory is used to store individual configuration files related to LightDM?

    1.  /etc/light
    2.  /etc/lightdm/lightdm.conf.d
    3.  /usr/lightdm
    4.  /etc/lightdm.conf

42.  Which environment variable is used by Xsession to specify the width of a terminal device?

    1.  TERMCHAR
    2.  COLUMNS
    3.  CHARACTERWIDTH
    4.  TERMCOL

43.  Which option within the Device section for a video card will set the amount of RAM available on the card?

    1.  VRAM
    2.  RAM
    3.  VideoRam
    4.  vRam

44.  When configuring a Screen section in an X configuration file, the Display subsection can contain the color depth. What is the name of the option to set the color depth of the given display?

    1.  ColorDepth
    2.  Depth
    3.  CDepth
    4.  colorDep

45.  Multiple server layouts may be created within an X configuration file. Which option is used to differentiate between the different server layout options?

    1.  ID
    2.  Identifier
    3.  LayoutName
    4.  Layout

46.  Which command can be used to create a fonts.scale file definition when executed against the current directory?

    1.  mkfontsscale
    2.  mk.fonts
    3.  mkfontfile
    4.  fontmk

47.  What abbreviation used in X signifies a display that utilizes additional capabilities such as extended power-saving capabilities?

    1.  DPMS
    2.  XPMS
    3.  DISPPWR
    4.  PWRD

48.  What is the name of the accessibility function that provides an alternative to the Orca program to assist users who have visual impairments?

    1.  Viz
    2.  emacspeak
    3.  Ahleah
    4.  vAssist

49.  Which of the following is a reference implementation of the Wayland protocol?

    1.  Wlnd
    2.  Weston
    3.  Wausau
    4.  Wittenberg

50.  Within an xorg configuration file, which option sets the inactivity timeout for the suspend mode of a DPMS-capable monitor?

    1.  InactTimeout
    2.  InactivityTime
    3.  SuspendTime
    4.  InTmout

51.  When the X server is started as a normal user, configuration files from which directory are also included?

    1.  /etc/X
    2.  /etc/X11/UserConfig
    3.  /etc/X11/xorg.conf.d
    4.  /etc/X/UserConf.d/

52.  Which of the following remote desktop protocols uses no compression or transport/session encryption?

    1.  SSH
    2.  XDMCP
    3.  XR
    4.  RD

53.  Within which desktop implementation would you find the xfwm4 window manager?

    1.  XWin
    2.  KDXF
    3.  Exf
    4.  Xfce

54.  Which option to Spice startup disables simple authentication?

    1.  disable-auth
    2.  disable-ticketing
    3.  disable-authentication
    4.  disable-simpleauth

55.  Which speech recognition software is included with the KDE desktop environment?

    1.  Alvin
    2.  Simon
    3.  Theodore
    4.  Zeppo

56.  Within the GNOME 3 desktop environment, within which Settings panel are the options for slow keys found?

    1.  Access
    2.  Typing Settings
    3.  Keyboard
    4.  Universal Access

57.  When an X session is already running, which command can be used to enable pointer keys?

    1.  setxkbmap
    2.  ptrkeys
    3.  pointerkeys
    4.  keypad -ptrkeys

58.  Which of the following provides a server-side implementation of Remote Desktop (RDP) for Linux?

    1.  lrdp
    2.  xrdp
    3.  rdp-linux
    4.  lindp

59.  You are attempting to edit the sudoers file with visudo over an SSH connection on a system that has GNOME installed and you receive an error indicating that gedit cannot run. Which of the following commands can be used to solve this issue?

    1.  export VISUAL="/bin/vim"
    2.  export DISPLAY
    3.  subst DISPLAY=local
    4.  env VISUAL=ssh

60.  Which option to x11vnc sets the password to be used for clients connecting to the server?

    1.  -password
    2.  -passwd
    3.  -pass
    4.  -auth

61.  Which program is used to add entries to the X authority file?

    1.  xf
    2.  xauthen
    3.  authx
    4.  xauth

62.  Which assistive technology will ignore keys that are pressed in succession or held down?

    1.  Sticky keys
    2.  Mouse keys
    3.  Bounce keys
    4.  On-screen keyboard

63.  Which environment variable is used by Xsession if the Xsession error file cannot be opened in its default location?

    1.  XLOG
    2.  TMPDIR
    3.  SESSLOG
    4.  LOGTMP

64.  From within an X session, which of the following commands shows information about the display, including resolution and color depth?

    1.  xinfo
    2.  xterm
    3.  xwin
    4.  xdpyinfo

65.  Which of the following files is the configuration file for Weston?

    1.  ∼/.config/weston.cfg
    2.  ∼/.config/weston.ini
    3.  ∼/weston.cfg
    4.  ∼/.westoncfg

66.  Which of the following remote desktop programs offers transport layer security?

    1.  x11vnc
    2.  xrd
    3.  tls
    4.  x11rtm

67.  Which add-on to Orca enables braille display support?

    1.  brl
    2.  brltty
    3.  brldis
    4.  dispbrl

68.  Which of the following is a screen magnifier program?

    1.  xmag
    2.  xzoom
    3.  xzmag
    4.  scrmag

69.  Which GRUB variable can be used to beep when the GRUB prompt is ready to accept input?

    1.  GRUB_BEEP
    2.  BEEP_START
    3.  GRUB_START_TONE
    4.  GRUB_INIT_TUNE

70.  You need to remove a host from being able to connect to the X server. Which of the following will remove a host named cwa from being able to connect?

    1.  xrem cwa
    2.  xhost -cwa
    3.  xhost -rem:cwa
    4.  xrem -host cwa

71.  The X Display Manager, xdm, runs various scripts as part of the login process. Which of the following scripts is executed as the user logging in?

    1.  Xstart
    2.  Xsession
    3.  Xstartup
    4.  Xuser.conf

72.  Which option to the X server disables listening for TCP connections?

    1.  -nolisten tcp
    2.  -notcp
    3.  -noconn tcp
    4.  -noconnect tcp

73.  Which signal is used to close existing connections, free resources, and restore defaults for an X server?

    1.  SIGKILL
    2.  SIGHUP
    3.  SIGN4
    4.  SIGALL

74.  Which option in the SeatDefaults section of the lightdm.conf configuration file is used to disable the display of usernames for login?

    1.  greeter-disable-user
    2.  greeter-enable-login
    3.  greeter-show-manual-login
    4.  greeter-disable-auto-login

75.  Which option to the xauth program disables hostname resolution?

    1.  -r
    2.  -n
    3.  -h
    4.  -m

76.  Which command will switch the system into an init in which the X server is not typically executed?

    1.  telinit 6
    2.  telinit 1
    3.  telinit 3
    4.  telinit 5

77.  What is the default location for the error log if the X server is run with xdm?

    1.  /etc/X11.log
    2.  /var/log/Xdm.log
    3.  /usr/lib/X11/xdm/xdm-errors
    4.  /var/log/xdmerrors

78.  Which script can be used for per-user initialization of xinit?

    1.  ∼/.xinit.conf
    2.  ∼/.xinitrc
    3.  ∼/.xinit.rc
    4.  ∼/.xinit.cfg

79.  Which option prevents abstract sockets from listening with X11?

    1.  -nolisten sock
    2.  -nolisten absock
    3.  -nolisten local
    4.  -nolisten socklocal

80.  Which option to XDMCP enables sending of BroadcastQuery packets?

    1.  -bcast
    2.  -bcastQ
    3.  -broadcastQuery
    4.  -broadcast

81.  When using GDM as the display manager, which GUI program can be used to set options for the login window?

    1.  gdmlogin
    2.  gdmconfig
    3.  gdmsetup
    4.  gdm

82.  Within the XDMCP access configuration file, there is a line like the following:

    *   *.example.com
    *   Which of the following describes how access will be treated for hosts from example.com?

    1.  Only the host named *.example.com can connect.
    2.  No hosts from example.com can connect.
    3.  Any host within example.com can connect.
    4.  Hosts that begin with * within example.com can connect.

83.  When using xhost, what is the syntax to enable a host named san to connect using IPv6?

    1.  xhost +ipv6:san
    2.  xhost -enablev6 san
    3.  xhost +inet6:san
    4.  xhost +enablev6 san

84.  Within which file are errors for Xsession and X client processes placed?

    1.  ∼/.xsession-error.log
    2.  ∼/.xsession-errors
    3.  ∼/.xclient.log
    4.  ∼/.xclient.errorlog

85.  GNOME includes native on-screen keyboard functionality. Which of the following commands starts the on-screen keyboard?

    1.  gok
    2.  osk
    3.  kb
    4.  oskb

86.  Which option to the xauth program specifies the authority file to use?

    1.  -a
    2.  -f
    3.  -a
    4.  -v

87.  Which accessibility option is helpful if several keys are sometimes pressed or if there is difficulty in consistently pressing the correct key on the keyboard?

    1.  Key toggle
    2.  Slow keys
    3.  KeyAssist
    4.  UniversalKeys

88.  On which port does RDP listen by default?

    1.  389
    2.  8080
    3.  3389
    4.  3306

# Chapter 7
Topic 107: Administrative Tasks

**THE FOLLOWING EXAM OBJECTIVES ARE COVERED IN THIS CHAPTER:**

*   **![images](images/correction.png)  107.1 Manage user and group accounts and related system files.**
    *   Key knowledge areas:
        *   Add, modify, and remove users and groups.
        *   Manage user/group info in password/group databases.
        *   Create and manage special purpose and limited accounts.
    *   The following is a partial list of the used files, terms, and utilities:
        *   /etc/passwd
        *   /etc/shadow
        *   /etc/group
        *   /etc/skel/
        *   chage
        *   getent
        *   groupadd
        *   groupdel
        *   groupmod
        *   passwd
        *   useradd
        *   userdel
        *   usermod
*   **![images](images/correction.png)  107.2 Automate system administration tasks by scheduling jobs.**
    *   Key knowledge areas:
        *   Manage cron and at jobs.
        *   Configure user access to cron and at services.
        *   Understand systemd timer units.
    *   The following is a partial list of the used files, terms, and utilities:
        *   /etc/cron.{d,daily,hourly,monthly,weekly}/
        *   /etc/at.deny
        *   /etc/at.allow
        *   /etc/crontab
        *   /etc/cron.allow
        *   /etc/cron.deny
        *   /var/spool/cron
        *   crontab
        *   at
        *   atq
        *   atrm
        *   systemctl
        *   systemd-run
*   **![images](images/correction.png)  107.3 Localization and internationalization**
    *   Key knowledge areas:
        *   Configure locale settings and environment variables.
        *   Configure time zone settings and environment variables.
    *   The following is a partial list of the used files, terms, and utilities:
        *   /etc/timezone
        *   /etc/localtime
        *   /usr/share/zoneinfo/
        *   LC_*
        *   LC_ALL
        *   LANG
        *   TZ
        *   /usr/bin/locale
        *   tzselect
        *   timedatectl
        *   date
        *   iconv
        *   UTF-8
        *   ISO-8859
        *   ASCII
        *   Unicode

1.  You need to enable the web server (running as the www-data user and group) to write into a directory called /home/webfiles. Which commands will accomplish this task in the most secure manner?

    1.  chgrp www-data /home/webfiles ; chmod 775 /home/webfiles
    2.  chmod 777 /home/webfiles
    3.  chgrp www-data /home/webfiles ; chmod 711 /home/webfiles
    4.  chmod 707 /home/webfiles

2.  Which of the following will execute a job through cron at 12:15 a.m. and 12:15 p.m. every day?

    1.  0,12 15 * * *
    2.  15 0,12 * * *
    3.  15 * * * 0/12
    4.  */12 * * * 15

3.  Which file is used to indicate the local time zone on a Linux server?

    1.  /etc/timez
    2.  /etc/timezoneconfig
    3.  /etc/localtime
    4.  /etc/localtz

4.  When importing entries into the LDAP database using ldapadd -f <filename>, in which format should the file be?

    1.  LDAP
    2.  TXT
    3.  CSV
    4.  LDIF

5.  Which of the following commands removes an expiration from an account?

    1.  sudo chage -l username
    2.  sudo chage -E -1 username
    3.  sudo chage -E now username
    4.  sudo chage --noexpire username

6.  Within which directory will you find files related to the time zone for various regions?

    1.  /etc/timezoneinfo
    2.  /etc/zoneinfo
    3.  /var/zoneinfo
    4.  /usr/share/zoneinfo

7.  Which of the following commands schedules a series of commands to execute 1 hour from now?

    1.  atq +1hr
    2.  at now + 1 hour
    3.  atq
    4.  at -1

8.  You need to delete a user from the system, including their home directory. Which of the following commands accomplishes this task?

    1.  userdel
    2.  userdel -r
    3.  userdel -R
    4.  deluser

9.  Which file contains a list of usernames, UIDs, and encrypted passwords?

    1.  /etc/passwd
    2.  /etc/shadow
    3.  /etc/encpass
    4.  /etc/grouppass

10.  Which job scheduler should you use if the computer on which you need to schedule the job is powered down at various times?

    1.  cron.d
    2.  cron.hourly
    3.  anacron
    4.  at

11.  Which of the following commands provides the current date and time in a format of seconds since the epoch?

    1.  date +%seconds
    2.  date +%s
    3.  date --seconds
    4.  date --now

12.  Which option to the iconv command shows the available character sets on a given system?

    1.  --showchar
    2.  --show
    3.  --list
    4.  --all

13.  Which environment variable controls the format of dates and times, such as a 12-hour or 24-hour formatted clock?

    1.  LOCALE_DATE
    2.  DATE_FORMAT
    3.  LC_TIME
    4.  LC_DATE

14.  Which command is recommended for configuration of slapd for OpenLDAP versions 2.3 and later?

    1.  slapd-conf
    2.  config-slapd
    3.  openldap-config
    4.  slapd-config

15.  Which shortcut within cron enables running of a task every day at midnight?

    1.  @daily
    2.  @daybegin
    3.  @topday
    4.  @beginday

16.  Which of the following encoding provides a multibyte representation of characters?

    1.  ISO-8859
    2.  UTF-8
    3.  ISO-L
    4.  UFTMulti

17.  Which of the following commands changes a group called DomainAdmins to DomainUsers?

    1.  groupmod -n DomainAdmins DomainUsers
    2.  groupchg DomainAdmins DomainUsers
    3.  chgroup DomainAdmins DomainUsers
    4.  group -N DomainAdmins DomainUsers

18.  Which file stores group information on a Linux server?

    1.  /etc/groupinfo
    2.  /etc/groups
    3.  /etc/roles
    4.  /etc/group

19.  Which command can be used to create an LDIF file from the current LDAP database?

    1.  slapdump
    2.  ldapdump
    3.  slapcat
    4.  catldap

20.  You are looking for a scheduled job that is not found in /etc/crontab, through systemd timers, or within /var/spool/cron. What is another location in which the scheduled job might be stored?

    1.  /etc/crontabs
    2.  /etc/cron.conf
    3.  /etc/cron.d/
    4.  /etc/sked

21.  You need to determine if LDAP integration is working correctly. In order to do so, you would like to obtain a list of users, as read by /etc/nsswitch.conf. Which command can be used for this purpose?

    1.  getuser
    2.  getent
    3.  usermod
    4.  userlist

22.  What is the name of the configuration file that contains information about group and user addition, such as the maximum and minimum user and group IDs, to be used when adding users and groups?

    1.  /etc/groupinfo
    2.  /etc/login.defs
    3.  /etc/login.info
    4.  /etc/loginlist

23.  Which environment variable is used for localization related to measurement units such as metric?

    1.  LC_METRIC
    2.  LC_MEASURE
    3.  LC_MEASUREMENT
    4.  LC_MEASUREUNITS

24.  Which of the following lines added to .profile in a user’s home directory will set their time zone to Central time?

    1.  TZ=/Central ; export TZ
    2.  TIMEZONE='America/Chicago' ; export TIMEZONE
    3.  set TZ=/Central
    4.  TZ='America/Chicago'; export TZ

25.  Within which directory will you find scripts that are scheduled to run through cron every 24 hours?

    1.  /etc/cron.daily
    2.  /etc/cron.weekly
    3.  /etc/cron.hourly24
    4.  /etc/crontab

26.  Which of the following values for the LANG variable will configure the system to bypass locale translations where possible?

    1.  LANG=COMPAT
    2.  LANG=NONE
    3.  LANG=C
    4.  LANG=END

27.  When running useradd, which option needs to be specified in order for the user’s home directory to be created?

    1.  -h
    2.  -m
    3.  -x
    4.  -a

28.  Which of the following commands locks out password-based login for a user but does not prevent other forms of login?

    1.  usermod -L
    2.  userdel -r
    3.  useradd -h
    4.  userlock

29.  If you need to temporarily reconfigure all locale variables and settings for a given session, which environment variable can be used?

    1.  LC_LIST
    2.  LC_GLOBAL
    3.  LC_ALL
    4.  ALL_LOCALE

30.  Which of the following will run a command called /usr/local/bin/changehome.sh as the www-data user when placed in /etc/crontab?

    1.  1 1 * * * www-data /usr/local/bin/changehome.sh
    2.  www-data changehome.sh
    3.  */1 www-data changehome.sh
    4.  * * */www-data /usr/local/bin/changehome.sh

31.  Which of the following commands produces a report listing the last password change date for all users on the system?

    1.  passwd -a
    2.  passwd -S
    3.  passwd -a -S
    4.  passwd --all

32.  Assume that passwords must be changed every 60 days. Which command will change the date of the user’s last password change without the user actually changing the account password?

    1.  chage -f
    2.  chage -W
    3.  chage -l
    4.  chage -d

33.  Which of the following files is used by anacron for reading configuration information related to jobs?

    1.  /etc/anacron.d
    2.  /etc/anacrontab
    3.  /etc/anacron.config
    4.  /etc/anacron.conf

34.  Which of the following commands is used to add entries to the OpenLDAP database?

    1.  ldapd
    2.  adduser
    3.  addldap
    4.  ldapadd

35.  Which file contains a list of users who are not allowed to create cron scheduled tasks?

    1.  /etc/cron.users
    2.  /etc/cron.deny
    3.  /etc/cron.denyusers
    4.  /etc/cron.userlist

36.  You are viewing the /etc/passwd file and see a * where the password should be. What does the presence of a * indicate within the password file?

    1.  The system uses forward password aging.
    2.  The system uses shadow passwords.
    3.  The system has been compromised.
    4.  Users have a * for their passwords.

37.  Which of the following best describes the relationship between UIDs and GIDs on a Linux system?

    1.  The UID and GID are the same across the system for a given user.
    2.  Each user has a UID and GID that are the same and are created when the user is created.
    3.  The UID represents the user whereas the GID is a globally unique user ID.
    4.  There is no direct relationship between UID and GID.

38.  Which of the following commands is used to re-create indexes based on existing slapd databases?

    1.  ldapind
    2.  ldapindex
    3.  slapindex
    4.  indexldap

39.  Which command is used to change a user’s home directory to /srv/data/username and move the contents at the same time?

    1.  usermod -md /srv/data/username <username>
    2.  homedir -m /srv/data/username <username>
    3.  userex -m /srv/data/username <username>
    4.  userchg /m /srv/data/username -d <username>

40.  Which option to useradd will add groups for a user?

    1.  -g
    2.  -x
    3.  -l
    4.  -G

41.  Which command will list the cron entries for a given user as denoted by <username>?

    1.  crontab -l -u <username>
    2.  crontab -u <username>
    3.  cron -u <username>
    4.  cronent -u <username>

42.  Which option to useradd creates a system user rather than a normal user?

    1.  -r
    2.  -s
    3.  -a
    4.  -S

43.  Which file contains encrypted password information for groups?

    1.  /etc/group
    2.  /etc/gshadow
    3.  /etc/gsecure
    4.  /etc/group.conf

44.  Which of the following commands can be used to help with recovery of a corrupted OpenLDAP database?

    1.  openldap-recover
    2.  oreco
    3.  slapd-recover
    4.  slapd_db_recover

45.  Which of the following best describes the use of the groupdel command?

    1.  You may force group deletion with the -f option.
    2.  If a user’s primary group is to be deleted, that user must be deleted first or have their primary group changed.
    3.  groupdel can be run at any time, regardless of group membership.
    4.  The -r option for groupdel will recursively change user’s GIDs after group deletion.

46.  Which of the following commands displays the UID, primary group, and supplemental groups for a given user?

    1.  id
    2.  getid
    3.  passwd
    4.  chage

47.  Which option to the usermod command is used to change a given user’s real name?

    1.  -R
    2.  -n
    3.  -d
    4.  -c

48.  Assume that you have deleted a user account with UID 1501, including the -r option. Which command should you also run to look for other files that might have been owned by the user?

    1.  find -id 1501
    2.  grep 1501 *
    3.  grep -u 1501 *
    4.  find / -uid 1501

49.  On which port does the slapd LDAP daemon listen for connections?

    1.  389
    2.  3389
    3.  3306
    4.  110

50.  Which of the following commands will set the systemwide time zone to America/Los_Angeles?

    1.  ln -sf /usr/share/zoneinfo/America/Los_Angeles /etc/localtime
    2.  ln -sf America/Los_Angeles ; /etc/localtime
    3.  ln -sd /etc/localtime /usr/share/timezone/America/Los_Angeles
    4.  ln -sf /etc/localtime /usr/share/zoneinfo/America/Los_Angeles

51.  Which locale-related variable is used for currency-related localization?

    1.  LC_MONE
    2.  LC_CURRENCY
    3.  LC_MONETARY
    4.  LC_CURR

52.  Which option to systemd-run adds a timed event?

    1.  --timed
    2.  --add-timer
    3.  --on-calendar
    4.  --on-time

53.  Which file is used to provide a list of users who can add and delete cron jobs?

    1.  /etc/cron.job
    2.  /etc/cron.allow
    3.  /etc/cron.users
    4.  /etc/crontab

54.  Which debug level for slapd is used to provide debugging of configuration file processing?

    1.  1
    2.  64
    3.  8
    4.  0

55.  Which command deletes an at job with an ID of 3?

    1.  atdt
    2.  at -l
    3.  atrm 3
    4.  rmat 3

56.  Which command on a Debian-based system can be used to change the time zone using the package-based tools?

    1.  dpkg-reconfigure time
    2.  dpkg-reconfigure tzdata
    3.  apt-select tzdata
    4.  apt-config timezone

57.  What will be logged with the loglevel set to 0x10 in a slapd.conf configuration file?

    1.  No debugging
    2.  Trace debugging
    3.  Stats logging
    4.  Packets sent and received

58.  Within which directory should you place files in order for the files to be copied to a user’s home directory when the user is created?

    1.  /etc/skel
    2.  /etc/homedir
    3.  /home/usertemplate
    4.  /etc/template

59.  Which command displays a list of jobs currently scheduled with at?

    1.  atlist
    2.  atq
    3.  atl
    4.  at --jobs

60.  On which port does LDAP over SSL listen for connections?

    1.  389
    2.  443
    3.  636
    4.  3128

61.  Which scheduler can be used to schedule a command to run once at a certain time?

    1.  at
    2.  cron
    3.  job
    4.  jobctl

62.  Which file provides a list of users who are allowed to create at jobs?

    1.  /etc/at.users
    2.  /etc/at.scheduler
    3.  /etc/at.conf
    4.  /etc/at.allow

63.  Which file extension is used for systemd timer units?

    1.  .conf
    2.  .timer
    3.  .timerd
    4.  .timeevent

64.  Within which directory would you find a list of files corresponding to the users who have current cron jobs on the system?

    1.  /var/spool/cron/crontabs
    2.  /var/spool/jobs
    3.  /etc/cron
    4.  /etc/cron.users

65.  When using slapadd for a large import, an error occurs at roughly 90 percent completion. Which option to slapadd enables specification of a line number from which the import will be restarted?

    1.  -l
    2.  -f
    3.  -q
    4.  -j

66.  Which argument to the locale command displays currently available locales for a given system?

    1.  -c
    2.  -a
    3.  -p
    4.  -s

67.  Which option to timedatectl sets the system clock?

    1.  --adjust-system-clock
    2.  -s
    3.  -c
    4.  -a

68.  Which option to the file command displays information on the MIME type of the file being interrogated?

    1.  -i
    2.  -m
    3.  -l
    4.  -a

69.  Which environment variable is used to set the paper size?

    1.  LC_PAPERSIZE
    2.  LC_PAPER
    3.  LC_PRINTERQ
    4.  LC_PRINTSIZE

70.  Which of the following is used as a systemwide cron file?

    1.  /etc/cron.d
    2.  /etc/cron.sys
    3.  /etc/crontab
    4.  /etc/cron.tab

71.  Which command can be used to view the available timezones on a system and obtain output that can be used in scripts for setting the time zone?

    1.  tzd
    2.  /etc/locale
    3.  tzdata
    4.  tzselect

72.  Which option within a systemd timer unit will start a timer 90 minutes after boot?

    1.  OnBootSec=90min
    2.  OnBoot=90min
    3.  OnBootHour=1.5
    4.  StartOnBoot=90min

73.  Which abbreviation is another name for information like the user’s full name, telephone number, and other contact information found in /etc/passwd?

    1.  USERINFO
    2.  GECOS
    3.  HOMEINFO
    4.  CDATA

74.  Which option to the groupadd command specifies the GID for the group?

    1.  -g
    2.  -a
    3.  -h
    4.  -k

75.  When working with systemd timer units, which option to systemctl displays the active timers?

    1.  list-timerunits
    2.  show-timers
    3.  list-timers
    4.  list-activetimers

76.  Which shortcut to the OnCalendar systemd timer function indicates that the timer unit should run once a week?

    1.  OnceAWeek
    2.  weekly
    3.  everyweek
    4.  oneperweek

77.  Which option to the crontab command removes the current crontab?

    1.  -r
    2.  -l
    3.  -g
    4.  -f

78.  Which variable in /etc/default/useradd controls the location of the skeleton home directory?

    1.  SKELETON
    2.  SKEL
    3.  SKELDIR
    4.  SKELLOC

79.  Which option to getent enumerates the password database for a given system?

    1.  password
    2.  listpass
    3.  passwd
    4.  showpassdb

80.  Which directory contains the jobs scheduled with at?

    1.  /var/spool/cron/atjobs
    2.  /var/spool/at
    3.  /var/spool/cron/at
    4.  /var/spool/atjobs

81.  Which variable in /etc/login.defs controls the minimum group ID to use on the system?

    1.  GIDMIN
    2.  GROUPID_MIN
    3.  GID_MIN
    4.  MIN_GID

82.  Which variable in /etc/login.defs contains the location of a user’s email directory for use by programs such as userdel?

    1.  EMAILDIR
    2.  DIR_EMAIL
    3.  MAILDIR
    4.  MAIL_DIR

83.  Which file contains user information such as username and real name and is readable by all users of the system?

    1.  /etc/pass
    2.  /etc/shadow
    3.  /etc/passwd
    4.  /etc/userinfo

84.  Which shortcut can be used to indicate that a cron job should be executed on restart?

    1.  @restart
    2.  @startup
    3.  @reboot
    4.  @onboot

85.  Which option to groupadd specifies that the group will be a system group?

    1.  -r
    2.  -m
    3.  -j
    4.  -b

86.  Within which directory are databases stored for OpenLDAP?

    1.  /var/lib/ldap
    2.  /var/cache/openldap
    3.  /var/share/ldap
    4.  /usr/share/openldap

87.  When listing systemd timer units, which option to list-timers shows both active and inactive units?

    1.  --all
    2.  --active-and-inactive
    3.  --inactive
    4.  All are shown by default.

88.  Which file provides a list of users who are not allowed to create at jobs?

    1.  /etc/at.allow
    2.  /etc/at.deny
    3.  /etc/at.denyusers
    4.  /etc/at.conf.deny

# Chapter 8
Topic 108: Essential System Services

**THE FOLLOWING EXAM OBJECTIVES ARE COVERED IN THIS CHAPTER:**

*   **![images](images/correction.png)  108.1 Maintain system time.**
    *   Key knowledge areas:
        *   Set the system date and time.
        *   Set the hardware clock to the correct time in UTC.
        *   Configure the correct timezone.
        *   Basic NTP configuration using ntpd and chrony
        *   Knowledge of using the pool.ntp.org service
        *   Awareness of the ntpq command
    *   The following is a partial list of the used files, terms, and utilities:
        *   /usr/share/zoneinfo/
        *   /etc/timezone
        *   /etc/localtime
        *   /etc/ntp.conf
        *   /etc/chrony.conf
        *   date
        *   hwclock
        *   timedatectl
        *   ntpd
        *   ntpdate
        *   chronyc
        *   pool.ntp.org
*   **![images](images/correction.png)  108.2 System logging**
    *   Key knowledge areas:
        *   Basic configuration of rsyslog
        *   Understanding of standard facilities, priorities, and actions
        *   Query the systemd journal.
        *   Filter systemd journal data by criteria such as date, service, or priority.
        *   Configure persistent systemd journal storage and journal size.
        *   Delete old systemd journal data.
        *   Retrieve systemd journal data from a rescue system or filesystem copy.
        *   Understand interaction of rsyslog with systemd-journald.
        *   Configuration of logrotate
        *   Awareness of syslog and syslog-ng
    *   The following is a partial list of the used files, terms, and utilities:
        *   /etc/rsyslog.conf
        *   /var/log/
        *   logger
        *   logrotate
        *   /etc/logrotate.conf
        *   /etc/logrotate.d/
        *   journalctl
        *   systemd-cat
        *   /etc/systemd/journald.conf
        *   /var/log/journal/
*   **![images](images/correction.png)  108.3 Mail Transfer Agent (MTA) basics**
    *   Key knowledge areas:
        *   Create email aliases.
        *   Configure email forwarding.
        *   Knowledge of commonly available MTA programs (Postfix, sendmail, Exim) (no configuration)
    *   The following is a partial list of the used files, terms, and utilities:
        *   ~/.forward
        *   sendmail emulation layer commands
        *   newaliases
        *   mail
        *   mailq
        *   Postfix
        *   sendmail
        *   Exim
*   **![images](images/correction.png)  108.4 Manage printers and printing.**
    *   Key knowledge areas:
        *   Basic CUPS configuration (for local and remote printers)
        *   Manage user print queues.
        *   Troubleshoot general printing problems.
        *   Add and remove jobs from configured printer queues.
    *   The following is a partial list of the used files, terms, and utilities:
        *   CUPS configuration files, tools, and utilities
        *   /etc/cups/
        *   lpd legacy interface (lpr, lprm, lpq)

1.  Which of the following commands is used to examine the systemd journal or log file?

    1.  journallist
    2.  ctlj
    3.  journalctl
    4.  jctl

2.  Which system logging facility is used for messages from the kernel?

    1.  syslog
    2.  kernel
    3.  kern
    4.  system

3.  To what server address can you set a Network Time Protocol (NTP) client in order to receive time from a regionally local server?

    1.  127.0.0.1
    2.  192.168.1.100
    3.  ntp.example.com
    4.  pool.ntp.org

4.  What is the name of the systemd service that provides logging facilities?

    1.  systemd-journald
    2.  systemd-loggingd
    3.  systemd-syslog
    4.  journalctl

5.  Which option within a logrotate configuration stanza informs logrotate to create a new log file owned by the user and group www-data and with permission 600?

    1.  new www-data.www-data mode 600
    2.  create 600 www-data www-data
    3.  new 600 www-data
    4.  createlog mode 600 user www-data group www-data

6.  Within which directory hierarchy will you find configuration files related to printing with the Common UNIX Printing System (CUPS) printing system?

    1.  /etc/cupsd
    2.  /etc/cups.d
    3.  /etc/CUPS
    4.  /etc/cups

7.  Which access control directive in a CUPS configuration file configures the system to accept connections from the local network with addresses from 192.168.1.1 through 192.168.1.127?

    1.  Allow 192.168.1.0/25
    2.  Allow 192.168.1.0/24
    3.  Allow 127.0.0.0/8
    4.  AllowHosts 192.168.1.0

8.  Which of the following commands will set the date immediately and can be used from the command line in a script?

    1.  ntpd
    2.  ntpdate pool.ntp.org
    3.  settime
    4.  time

9.  When executing the ntpq command, you receive a message like read: Connection refused. What would this typically indicate?

    1.  The network is down.
    2.  The NTP daemon is not running.
    3.  The use of NTP is administratively prohibited.
    4.  The current user does not have permission to execute ntpq.

10.  Which command is used to query and work with the hardware clock on the system?

    1.  hwc
    2.  ntpdate
    3.  systime
    4.  hwclock

11.  Which directory contains a listing of available time zones on a Linux system?

    1.  /etc/timezones
    2.  /etc/tzdata
    3.  /usr/share/zoneinfo
    4.  /usr/share/timezones

12.  Which syslog level is used to provide informational messages?

    1.  kern
    2.  emerg
    3.  debug
    4.  info

13.  Within /etc/ntp.conf, which of the following configuration lines sets the location of the drift file?

    1.  drift /var/lib/ntp/drift
    2.  driftfile /var/lib/ntp/drift
    3.  drift-file /var/lib/ntp/drift
    4.  driftconfig /var/lib/ntp/drift

14.  Which configuration option in /etc/logrotate.conf will cause the log to be emailed to [admin@example.com](mailto:admin@example.com) when the logrotation process runs for the selected log?

    1.  mail[admin@example.com](mailto:admin@example.com)
    2.  sendmail[admin@example.com](mailto:admin@example.com)
    3.  maillog[admin@example.com](mailto:admin@example.com)
    4.  logmail[admin@example.com](mailto:admin@example.com)

15.  Which of the following commands is used to determine the amount of disk space used by systemd journal logfiles?

    1.  journalctl --disk
    2.  journalctl -du
    3.  journalctl --disk-usage
    4.  journalctl -ls

16.  Which of the following commands displays the current mail queue on a Postfix server?

    1.  qmail
    2.  mailqueue
    3.  mail -q
    4.  mailq

17.  When you’re running the NTP daemon, which command can you execute to work with the NTP server in an interactive mode?

    1.  ntpd
    2.  ntpdate
    3.  ntpq
    4.  ntp-interactive

18.  Assume that you want all email for the root user to be sent to [admin@example.com](mailto:admin@example.com). Which of the following lines in /etc/aliases will accomplish this task?

    1.  [admin@example.com](mailto:admin@example.com)-> root
    2.  root ->[admin@example.com](mailto:admin@example.com)
    3.  root,[admin@example.com](mailto:admin@example.com)
    4.  root:[admin@example.com](mailto:admin@example.com)

19.  When you’re working with klogd, which option can be used to control the file to which messages are logged?

    1.  -d
    2.  -f
    3.  -v
    4.  -l

20.  Which set of programs or packages can be used for setting the system time on a device that is offline frequently?

    1.  chrony
    2.  htpoffline
    3.  ntpd-off
    4.  chrondate

21.  Which of the following commands places a file into the print queue?

    1.  lpr
    2.  lpd
    3.  lpq
    4.  lpx

22.  Which of the following options to the sendmail command will print information about the mail queue?

    1.  -bi
    2.  -queue
    3.  -bp
    4.  -f

23.  Which function of the hwclock command will set the hardware clock to the current system time?

    1.  -w
    2.  -s
    3.  -a
    4.  -m

24.  What is the default port for the CUPS administrative web interface?

    1.  tcp/53
    2.  tcp/8080
    3.  udp/456
    4.  tcp/631

25.  Which of the following commands causes sendmail to attempt to deliver the messages in its queue?

    1.  sendmail -q
    2.  sendmail -b
    3.  sendmail -f
    4.  sendmail -v

26.  You need to create an email address to accept email for [abuse@example.com](mailto:abuse@example.com). However, you would like abuse reports sent to multiple email addresses within your organization. Which of the following will send email destined for the abuse account to [admin@example.com](mailto:admin@example.com) and [security@example.com?](mailto:security@example.com?)

    1.  Create a .forward in the home directory for the abuse user and forward email accordingly.
    2.  Within /etc/aliases, add this: abuse:[admin@example.com](mailto:admin@example.com),[security@example .com](mailto:security@example.com).
    3.  Create a .forward file for root and forward email accordingly.
    4.  Within /etc/aliases, add this: abuse:[admin@example.com](mailto:admin@example.com)\[tsecurity@example .com](mailto:tsecurity@example.com).

27.  Which of the following commands sets the hardware clock to Coordinated Universal Time (UTC) based on the current system time?

    1.  hwclock --systohc --utc
    2.  hwclock --systohc --localtime
    3.  hwclock --systohc
    4.  hwclock --systoutc

28.  You need to delete all messages from the queue on a Postfix server. Which of the following commands will perform this action?

    1.  postqueue -remove
    2.  rm -rf
    3.  postfix -f
    4.  postsuper -d ALL

29.  Which of the following URLs can be used to view a list of completed print jobs in CUPS?

    1.  [http://localhost:631/jobs?which_jobs=completed](http://localhost:631/jobs?which_jobs=completed)
    2.  [http://localhost:631?completed](http://localhost:631?completed)
    3.  [http://localhost:631/?completed](http://localhost:631/?completed)
    4.  [http://cups/jobs=completed](http://cups/jobs=completed)

30.  Which option to the journalctl command will continuously update the display as new log entries are created?

    1.  -tail
    2.  -t
    3.  -f
    4.  -l

31.  Assuming that the $ModLoad imudp configuration option has been set in the configuration for rsyslogd, which of the following additional options is necessary to configure the port on which the server will listen?

    1.  $Port 514
    2.  $UDPServerRun 514
    3.  $Listen 514
    4.  $UDPListen 514

32.  Which of the following commands causes the mail queue to be processed on a Postfix server?

    1.  postqueue -f
    2.  postqueue -D
    3.  postfix -q
    4.  postsuper -q

33.  When running ntpd, the server will not adjust or synchronize if the time is skewed from the NTP server by a significant amount of time. Which option to ntpd disables this and causes the synchronization process to continue even if there is a large skew?

    1.  ntpd -noskew
    2.  ntpd -skewcheck=off
    3.  ntpd -g 0
    4.  ntpd -s 0

34.  Which option in journald.conf controls the maximum file size for individual journal logs?

    1.  SystemMaxFileSize
    2.  MaxFile
    3.  LogFileSize
    4.  LogSize

35.  Which command can be executed to view completed print jobs?

    1.  lpstat -q
    2.  lpq
    3.  lpstat -W completed
    4.  lpqueue -c

36.  When configuring a log file for rotation, you need to execute a command to run a script after log file rotation. Which option within the logrotate.conf configuration file can be used to facilitate this behavior?

    1.  after-rotate
    2.  run-script
    3.  rotatecomplete
    4.  postrotate

37.  You are deploying an Exim server and need to work with the firewall to ensure the proper incoming ports are open. Which protocol and port should you allow inbound for normal Simple Mail Transfer Protocol (SMTP) traffic?

    1.  TCP/23
    2.  TCP/25
    3.  TCP/110
    4.  TCP/143

38.  Which command should be executed after making a change to the sendmail access database /etc/access?

    1.  makemap
    2.  makedb
    3.  newaccess
    4.  rebuilddb

39.  When working with syslog-ng, which of the following is the correct path and filename for the primary configuration file?

    1.  /etc/syslog-ng/syslog-ng.conf
    2.  /etc/syslog/syslog-ng.conf
    3.  /etc/syslog-ng/ng.conf
    4.  /etc/syslog-ng/ngd.conf

40.  A developer has created an application and wants to take advantage of syslog for logging to a custom log file. Which facility should be used for an application such as this?

    1.  syslog
    2.  kern
    3.  local#
    4.  user

41.  A user needs to work with printer-related items. Which of the following commands adds the user (called username in the options) to the appropriate group for this purpose?

    1.  usermod -aG printerusers username
    2.  usermod -aG lpadmin username
    3.  usermod -gA lpadm username
    4.  usermod -a lpadm username

42.  Which option within a logrotate configuration file disables compression of the log file?

    1.  compressoff
    2.  limitcompress
    3.  nocompression
    4.  nocompress

43.  Which command should be used to enable printer sharing through CUPS?

    1.  cupsctl --enable-sharing
    2.  cupsc --share
    3.  cupsctl --share-printers
    4.  cupsc --printer-sharing

44.  Which command can be used to gather and display statistics about mail processed on a server running sendmail?

    1.  mailq
    2.  mailstats
    3.  statmail
    4.  sendmailstats

45.  You need to determine the size of the systemd journals on the system. Which option to journalctl is used for this purpose?

    1.  --disk-use
    2.  --disk-usage
    3.  --disk-space
    4.  --disk-used

46.  You are troubleshooting a problem with printing and believe the CUPS service needs to be restarted. Which of the following commands can be used to restart CUPS on a server running systemd?

    1.  systemctl restart cups.service
    2.  systemctl restart cups-service
    3.  systemctl reboot cups.target
    4.  systemctl restart cups.target

47.  You are working with journalctl and need to see only messages that are at a debug priority. Which of the following options enables this scenario?

    1.  -pri debug
    2.  -prior debug
    3.  -d debug
    4.  -p debug

48.  Which option in a CUPS configuration file causes the daemon to listen on all interfaces on port 631?

    1.  Port 631
    2.  Listen All:631
    3.  Listen 127.0.0.1:631
    4.  Port All:631

49.  Which command is used to remove an email from the mail queue with Postfix?

    1.  postsuper -d
    2.  postmaster
    3.  postfix -d
    4.  postdel

50.  Which option to journalctl will clear logs older than five days?

    1.  --clear=5d
    2.  --vacuum-time=5d
    3.  --delete-older=5d
    4.  --clear-time=5d

51.  When configuring email forwarding with Procmail, which of the following files is used as a user-based configuration file for Procmail?

    1.  /home/procmail.conf
    2.  ~/.procmailrc
    3.  /etc/procmail.conf
    4.  ~/procmail.conf

52.  Which of the following definitions in /etc/aliases will deliver mail destined to root to two email addresses, [admin@example.com](mailto:admin@example.com) and [webmaster@example.com?](mailto:webmaster@example.com?)

    1.  [root] =[admin@example.com](mailto:admin@example.com), [webmaster@example.com](mailto:webmaster@example.com)
    2.  root: admin webmaster
    3.  root: admin, webmaster
    4.  root:[admin@example.com](mailto:admin@example.com), [webmaster@example.com](mailto:webmaster@example.com)

53.  Which of the following commands views the contents of a message that exists in the Postfix queue?

    1.  postshow
    2.  postless
    3.  postmore
    4.  postcat

54.  Within which file will you find errors related to delivery of mail on a Postfix server?

    1.  /var/log/mail
    2.  /var/log/postfix.log
    3.  /var/log/mail.err
    4.  /var/log/postfix.err

55.  When testing SMTP communications between a client and a server, you need to begin the conversation. Which of the following lines shows the beginning of an SMTP conversation using Extended Hello syntax from mail.example.com?

    1.  BEGIN mail.example.com
    2.  SMTP mail.example.com
    3.  HELO mail.example.com
    4.  EHLO mail.example.com

56.  Which option to timedatectl shows the available time zones?

    1.  list-timezones
    2.  show-tz
    3.  --tzinfo
    4.  --timezones

57.  You are viewing a directory listing of the /etc/localtime file and it looks like the following:

    *   lrwxrwxrwx 1 root root 35 Oct 30 2018 /etc/localtime -> /usr/share/zoneinfo/America/Chicago
    *   From that directory listing, what can you tell about the file?

    1.  The file is a symlink to a timezone in /usr/share/zoneinfo.
    2.  The /usr/share/zoneinfo file is a symlink to /etc/localtime.
    3.  The /etc/localtime file is a hard link to /usr/share/zoneinfo.
    4.  The time zone cannot be set because the file must exist as its own separate file.

58.  You need to set the correct time zone on a server. How can you tell what the current time zone is set to?

    1.  Run the date command.
    2.  Run the tzdata command.
    3.  Examine /proc/timezone.
    4.  Examine /etc/tzdata.

59.  Which of the following is the configuration file used by the Chrony package?

    1.  /etc/chrony.cfg
    2.  /etc/chrony/default.cfg
    3.  /etc/chrony.conf
    4.  /etc/chrony.d/chrony.cf

60.  Which option to journalctl queries for only kernel messages?

    1.  -ok
    2.  -okern
    3.  -k
    4.  -limitk

61.  Which command must you run after making a change to email aliases on a server running Postfix?

    1.  service postfix restart
    2.  newaliases
    3.  alias -n
    4.  postfix -e

62.  You need to log output to the systemd journal from a script. Which of the following commands facilitates this scenario?

    1.  systemd-log
    2.  systemd-logger
    3.  systemd-logm
    4.  systemd-cat

63.  Which command can be used to remove print jobs from the queue?

    1.  lprm
    2.  lpdel
    3.  lpqman
    4.  lprmj

64.  When running from a shell script, which command enables logging to syslog?

    1.  logd
    2.  login
    3.  logit
    4.  logger

65.  You need to find the mail queue path on a Postfix server. You’re using postconf -d to view all parameters. Which parameter contains the mail queue path on a Postfix server?

    1.  mqueue
    2.  queue_dir
    3.  mailq_path
    4.  mqueue_path

66.  Which of the following options can be given to journalctl in order to filter based on a service name?

    1.  _SYSTEMD-SERVICE
    2.  _SERVICENAME
    3.  _SYSTEMD_SERVICE
    4.  _SYSTEMD_UNIT

67.  Which command can be used to add a job to a print queue?

    1.  lpadd
    2.  lkp
    3.  lp
    4.  lpprint

68.  Which of the following files enables per-user email forwarding?

    1.  ~/.mailforward
    2.  ~/.forward
    3.  ~/.formail
    4.  ~/.forwardmail

69.  Which argument to the mail command sets the subject for the email to be sent?

    1.  -E
    2.  -s
    3.  -c
    4.  -f

70.  Which option to the date command can be used to set the date and time?

    1.  date -f
    2.  date -t
    3.  date --change
    4.  date -s

71.  Which option to journalctl will trim the journal data size so that it consumes the amount specified?

    1.  --clear-size
    2.  --vacuum-size
    3.  --delete-size
    4.  --consume-max

72.  Which option to journalctl filters based on time?

    1.  --since
    2.  --time
    3.  --time-t
    4.  --filter-time

73.  When viewing the syslog configuration, you notice a minus sign (−) preceding several log files. What is the significance of the − sign in the configuration?

    1.  The use of − indicates that the log may be rotated any time.
    2.  The use of − indicates that the system can utilize other logging facilities when appropriate.
    3.  The use of − omits the disk sync process for every entry into the log.
    4.  The use of − comments out the line.

74.  Which option to lpr sends a print job to a given destination?

    1.  -P
    2.  -a
    3.  -p
    4.  -h

75.  Which Postfix-related command is used to provide an overview of the number of messages in the incoming and active queues arranged by age?

    1.  queuelist
    2.  postq
    3.  qshape
    4.  queueshow

76.  Within the journald configuration file, which option is used to configure the maximum space used by journal files?

    1.  SystemFileSizeLimit
    2.  SystemMaxFile
    3.  SystemMaxSize
    4.  SystemMaxUse

77.  Within which directory hierarchy are queue-related messages stored for Postfix?

    1.  /var/mqueue
    2.  /var/spool/mailq
    3.  /var/spool/postfix
    4.  /var/postfix

78.  Which option to journalctl can be used to specify an alternate location for journal data, such as might be the case when retrieving journal data from a rescue system or a filesystem copy?

    1.  --alt
    2.  --journal-location
    3.  --journal-dir
    4.  --directory

79.  Within which directory are system logs normally kept on a Linux system?

    1.  /etc/logs/
    2.  /var/logs/
    3.  /var/log/
    4.  /tmp/log/

80.  Which shortcut can be used as the destination in an Exim alias to prevent Exim from delivering mail to a certain address, such as when you want to essentially delete the mail rather than deliver it?

    1.  :del:
    2.  :block:
    3.  :blackhole:
    4.  :deletemail:

81.  Which stanza within a CUPS printers.conf configuration file is used to configure a default local printer with CUPS?

    1.  <LOCAL printerName>
    2.  <Printer printerName>
    3.  <DefaultPrinter printerName>
    4.  <PrintDefault printerName>

82.  Which of the following commands can be used to remove all jobs queued for printing?

    1.  lprm --all
    2.  lprm --del A
    3.  lprm -
    4.  lprm --remove ALL

83.  When using the mail command, which option enables setting the From header?

    1.  -f
    2.  -r
    3.  -o
    4.  -m

84.  Which character sequence is used to precede the host or IP in order to specify that TCP should be used for remote system logging in /etc/rsyslog.conf?

    1.  @TCP
    2.  @@
    3.  @
    4.  :tcp@

85.  Within the /etc/systemd/journald.conf file, which key/value pair will enable the journal to be persistent?

    1.  Keep=All
    2.  Store=Persistence
    3.  Storage=Persistent
    4.  Keep=Persist

86.  Which command can be used to monitor the status of chronyd?

    1.  chronyc
    2.  chronystat
    3.  chrony-stats
    4.  chronyd-stat

87.  Within which directory will you find configuration files for various logs that are to be rotated with logrotate?

    1.  /etc/logrotate
    2.  /etc/logs
    3.  /etc/logrotate.d
    4.  /var/spool/logrotate

88.  Which of the following commands is used to view the pending messages queue on a Postfix server?

    1.  postqueue -p
    2.  postconf -pending
    3.  postqueue -f
    4.  postsuper pending

# Chapter 9
Topic 109: Networking Fundamentals

**THE FOLLOWING EXAM OBJECTIVES ARE COVERED IN THIS CHAPTER:**

*   **![images](images/correction.png)  109.1 Fundamentals of Internet protocols**
    *   Key knowledge areas:
        *   Demonstrate an understanding of network masks and CIDR notation.
        *   Knowledge of differences between private and public “dotted quad” IP addresses
        *   Knowledge about common TCP and UDP ports and services (20, 21, 22, 23, 25, 53, 80, 110, 123, 139, 143, 161, 162, 389, 443, 465, 514, 636, 993, 995)
        *   Knowledge about the differences and major features of UDP, TCP, and ICMP
        *   Knowledge of the major differences between IPv4 and IPv6
        *   Knowledge of the basic features of IPv6
    *   The following is a partial list of the used files, terms, and utilities:
        *   /etc/services
        *   IPv4, IPv6
        *   Subnetting
        *   TCP, UDP, ICMP
*   **![images](images/correction.png)  109.2 Persistent network configuration**
    *   Key knowledge areas:
        *   Understand basic TCP/IP host configuration.
        *   Configure ethernet and Wi-Fi network configuration using NetworkManager.
        *   Awareness of systemd-networkd
    *   The following is a partial list of the used files, terms, and utilities:
        *   /etc/hostname
        *   /etc/hosts
        *   /etc/nsswitch.conf
        *   /etc/resolv.conf
        *   nmcli
        *   hostnamectl
        *   ifup
        *   ifdown
*   **![images](images/correction.png)  109.3 Basic network troubleshooting**
    *   Key knowledge areas:
        *   Manually configure network interfaces, including viewing and changing the configuration of network interfaces using iproute2.
        *   Manually configure routing, including viewing and changing routing tables and setting the default route using iproute2.
        *   Debug problems associated with the network configuration.
        *   Awareness of legacy net-tools commands
    *   The following is a partial list of the used files, terms, and utilities:
        *   ip
        *   hostname
        *   ss
        *   ping
        *   ping6
        *   traceroute
        *   traceroute6
        *   tracepath
        *   tracepath6
        *   netcat
        *   ifconfig
        *   netstat
        *   route
*   **![images](images/correction.png)  109.4 Configure client-side DNS.**
    *   Key knowledge areas:
        *   Query remote DNS servers.
        *   Configure local name resolution and use remote DNS servers.
        *   Modify the order in which name resolution is done.
        *   Debug errors related to name resolution.
        *   Awareness of systemd-resolved.
    *   The following is a partial list of the used files, terms, and utilities:
        *   /etc/hosts
        *   /etc/resolv.conf
        *   /etc/nsswitch.conf
        *   host
        *   dig
        *   getent

1.  Which of the following commands shows the current default route without performing Domain Name System (DNS) lookups on the IP address(es) involved?

    1.  netstat -rn
    2.  netstat -n
    3.  netstat -r
    4.  netstat -f

2.  You are having difficulty with an interface on the server and it is currently down. Assuming that there is no hardware failure on the device itself, which command and option can you use to display information about the interface?

    1.  ifconfig -a
    2.  ifup
    3.  netstat -n
    4.  ifconfig

3.  Which of the following is not used as a private address for internal, non-Internet, use?

    1.  172.16.4.2
    2.  192.168.40.3
    3.  10.74.5.244
    4.  143.236.32.231

4.  Which of the following commands adds a default gateway of 192.168.1.1 for interface eth0?

    1.  route add default gateway 192.168.1.1 eth0
    2.  eth0 --dg 192.168.1.1
    3.  route add default gw 192.168.1.1 eth0
    4.  route define eth0 192.168.1.1

5.  Which option for the host command will query for the authoritative name servers for a given domain?

    1.  -t ns
    2.  -t all
    3.  -ns
    4.  -named

6.  Which port(s) and protocol(s) should be opened in a firewall in order for the primary and secondary name servers to communicate for a given domain?

    1.  udp/53
    2.  Both tcp/53 and udp/53
    3.  tcp/53
    4.  udp/53 and tcp/503

7.  Which option for the ping command enables you to choose the interface from which the Internet Control Message Protocol (ICMP) packets will be generated?

    1.  -i
    2.  -I
    3.  -t
    4.  -a

8.  You need to split a subnet to enable four subnets with up to 30 hosts each. Which subnet mask, in Classless Inter-Domain Routing (CIDR) notation, facilitates this scenario?

    1.  /25
    2.  /24
    3.  /32
    4.  /27

9.  Which of the following commands queries for the mail servers for the domain example.com?

    1.  dig example.com mx
    2.  dig example.com
    3.  host -t smtp example.com
    4.  dig example.com smtp

10.  Which of the following addresses represents the localhost in IPv6?

    1.  0:1
    2.  ::1
    3.  127:0:1
    4.  :127:0:0:1

11.  Which option to the traceroute command will use TCP SYN packets for the path trace?

    1.  -T
    2.  -t
    3.  -s
    4.  -i

12.  Which of the following commands will attempt to bring online all interfaces marked as auto within the networking configuration?

    1.  ifconfig -a
    2.  ifup auto
    3.  ifup -a
    4.  ifstat

13.  In a scripting scenario, which command will return the domain name configured for the server?

    1.  dnsname
    2.  fqdn
    3.  hostname
    4.  hostname -d

14.  Which command can be used to listen for netlink messages on a network?

    1.  ip monitor
    2.  netlink -a
    3.  ip netlink
    4.  route

15.  If the traceroute6 command is not available, which option to the traceroute command can be used for an IPv6 traceroute?

    1.  -ipv6
    2.  -net6
    3.  -v6
    4.  -6

16.  Which of the following configuration lines in /etc/nsswitch.conf causes a lookup for group information to first use local files and then use LDAP?

    1.  group: files ldap
    2.  lookup: group [local ldap]
    3.  group: [local ldap]
    4.  group: localfiles ldap

17.  Which of the following dig commands sends the query for example.com directly to the server at 192.168.2.5 rather than to a locally configured resolver?

    1.  dig example.com @192.168.2.5
    2.  dig -t 192.168.2.5 example.com
    3.  dig -s 192.168.2.5 example.com
    4.  dig server=192.168.2.5 example.com

18.  Which ports need to be allowed through the firewall for Simple Network Management Protocol (SNMP) traffic?

    1.  Ports 23 and 25
    2.  Ports 110 and 143
    3.  Ports 80 and 443
    4.  Ports 161 and 162

19.  Which of the following commands will enumerate the hosts database?

    1.  getent hosts
    2.  gethosts
    3.  nslookup
    4.  host

20.  Which of the following netmasks is used for a subnet described with a /25 in CIDR notation?

    1.  255.255.255.0
    2.  255.255.0.0
    3.  255.255.255.192
    4.  255.255.255.128

21.  Which of the following configuration lines will set the DNS server to 192.168.1.4 using /etc/resolv.conf?

    1.  dns 192.168.1.4
    2.  dns-server 192.168.1.4
    3.  nameserver 192.168.1.4
    4.  name-server 192.168.1.4

22.  When examining open ports on the server, you see that TCP port 3000 is listed with no corresponding protocol name, such as SMTP, IMAP over SSL (IMAPS), and so on. In which file would you find a list of port-to-protocol translations that could be customized to add this new port?

    1.  /etc/ports
    2.  /etc/p2p
    3.  /etc/ppp
    4.  /etc/services

23.  Which of the following commands adds a route to the server for the network 192.168.51.0/24 through its gateway of 192.168.51.1?

    1.  route add -net 192.168.51.0 netmask 255.255.255.0 gw 192.168.51.1
    2.  route add -net 192.168.51/24 gw 192.168.1.51
    3.  route -net 192.168.51.0/24 192.168.51.1
    4.  route add 192.168.51.1 -n 192.168.51.0//255.255.255.0

24.  Which of the following netstat options displays the send and receive queues for each socket?

    1.  -r
    2.  -M
    3.  -a
    4.  -v

25.  Which of the following represents a correct configuration line for /etc/hosts?

    1.  192.168.1.4 cwa.braingia.org cwa
    2.  cwa.braingia.org cwa 192.168.1.4
    3.  cwa.braingia.org 192.168.1.8 alias cwa
    4.  alias cwa.braingia.org cwa 192.168.1.4

26.  Which of the following commands configures the eth0 device with an IP address of 192.168.1.1 in a /24 network?

    1.  ifconfig eth0 192.168.1.1/24
    2.  ifconfig eth0 192.168.1.1/255.255.255.0
    3.  ifconfig eth0 192.168.1.1 netmask 255.255.255.0
    4.  ifconfig 192.168.1.1 netmask 255.255.255.0 eth0

27.  Which of the following describes a primary difference between IPv4 and IPv6?

    1.  IPv4 is for internal networks only, whereas IPv6 is for public networks.
    2.  IPv4 is for public networks, whereas IPv6 is for internal networks.
    3.  IPv4 uses a 32-bit address, whereas IPv6 uses a 128-bit address.
    4.  With IPv6, no subnetting is necessary.

28.  On which port does ICMP operate?

    1.  TCP/43
    2.  UDP/111
    3.  UDP/69
    4.  ICMP does not use ports.

29.  Which of the following commands will change the default gateway to 192.168.1.1 using eth0?

    1.  ip route default gw 192.168.1.1
    2.  ip route change default via 192.168.1.1 dev eth0
    3.  ip route default gw update 192.168.1.1
    4.  ip route update default 192.168.1.1 eth0

30.  Which of the following ports is used for Secure Shell communication?

    1.  TCP/23
    2.  TCP/25
    3.  TCP/22
    4.  TCP/2200

31.  Which options for netcat will create a server listening on port 8080?

    1.  netcat -p 8080
    2.  nc -l -p 8080
    3.  nc -p 8080
    4.  nc -s 8080

32.  Which of the following commands displays the Start of Authority information for the domain example.com?

    1.  dig example.com soa
    2.  dig example.com authority
    3.  dig example.com -auth
    4.  dig -t auth example.com

33.  Assume that you want to enable local client services to go to hosts on the network without needing to fully qualify the name by adding the domain for either example.com or example.org. Which option in /etc/resolv.conf will provide this functionality?

    1.  search
    2.  domain
    3.  local-domain
    4.  local-order

34.  Which of the following commands sends an IPv6 ping to a unique local address?

    1.  ping -6 127.0.0.1
    2.  ping6 fddi/128
    3.  ping6 fdd6:551:b09f::
    4.  ping -6 fdd6:551:b09f::

35.  Which of the following commands prevents traffic from reaching the host 192.168.1.3?

    1.  route add -host 192.168.1.3 reject
    2.  route -nullroute 192.168.1.3
    3.  route add -null 192.168.1.3
    4.  route add -block 192.168.1.3

36.  Which of the following describes a primary difference between traceroute and tracepath?

    1.  The traceroute command requires root privileges.
    2.  The tracepath command provides the MTU for each hop, whereas traceroute does not.
    3.  The tracepath command cannot be used for tracing a path on an external network.
    4.  The traceroute command is not compatible with IPv6.

37.  Which of the following commands will emulate the ping command in Microsoft Windows, where the ping is sent for four packets and then the command exits?

    1.  ping -n 4
    2.  ping -t 4
    3.  ping -p 4
    4.  ping -c 4

38.  Which command provides an interface into NetworkManager that works from a terminal window?

    1.  nmcli
    2.  nmui
    3.  nm
    4.  nman

39.  Which of the following commands configures eth1 with an additional IPv6 address of fdd6:551:b09e::?

    1.  ifconfig eth1 inet6 add fdd6:551:b09e::/128
    2.  ifconfig add fdd6:551:b09e::
    3.  ifconfig fdd6:551:b09e:: eth1
    4.  ifconfig eth1 fdd6:551:b09e

40.  On which port does LDAP over SSL operate?

    1.  Port 53
    2.  Port 389
    3.  Port 636
    4.  Port 443

41.  You need to prevent local clients from going to a certain host, [www.example.com](http://www.example.com), and instead redirect them to localhost. Which of the following is a method to override DNS lookups for the specified host?

    1.  Add a firewall entry for the IP address of [www.example.com](http://www.example.com) to prevent traffic from passing through it.
    2.  Delete [www.example.com](http://www.example.com) from the route table using the route command.
    3.  Add a null route to prevent access to the IP address for [www.example.com](http://www.example.com).
    4.  Add an entry for [www.example.com](http://www.example.com) in /etc/hosts to point to 127.0.0.1.

42.  Which of the following commands should be executed after running ip route change?

    1.  ip route flush cache
    2.  ip route reload
    3.  ip route cache reload
    4.  ip route restart

43.  Which option should be used to send a DNS query for a Sender Policy Framework (SPF) record with dig?

    1.  -t txt
    2.  -t spf
    3.  -t mx
    4.  -t mailspf

44.  Which of the following protocols uses a three-way handshake?

    1.  ICMP
    2.  TCP
    3.  UDP
    4.  IP

45.  How many IP addresses are available in the 172.16.0.0 private range in IPv4?

    1.  /32
    2.  16,777,216
    3.  65,536
    4.  1,048,576

46.  When troubleshooting a connectivity issue, you have found that you can reach a server via the web but cannot ping it. Which of the following best describes a possible cause for this scenario?

    1.  TCP traffic has been blocked at the firewall.
    2.  The DNS lookup is failing.
    3.  ICMP traffic has been blocked.
    4.  There is a reject route in place.

47.  When viewing the available routes using the route command, one route contains UG flags and the others contain U flags. What do the letters UG signify in the route table?

    1.  The G signifies that the route is good.
    2.  The G signifies that the route is unavailable.
    3.  The G signifies that this is a gateway.
    4.  The G signifies that the route is an aggregate.

48.  Which of the following commands requests a zone transfer of example.org from the server at 192.168.1.4?

    1.  dig example.org @192.168.1.4 axfr
    2.  dig example.org @192.168.1.4
    3.  dig example.org @192.168.1.4 xfer
    4.  dig example.org #192.168.1.4 xfer

49.  Which of the following commands displays the number of packets forwarded by the kernel?

    1.  ls
    2.  ipstat
    3.  ifconfig -a
    4.  netstat -s

50.  When using the ip command, which protocol family is used as the default if not otherwise specified?

    1.  tcpip
    2.  ip
    3.  inet
    4.  arp

51.  Which of the following commands changes the Media Access Control (MAC) address of eth0?

    1.  ifmac eth0
    2.  ifconfig eth0 hw ether
    3.  ifconfig eth0 mac
    4.  ifconfig eth0 hw mac

52.  You are using the route command to view routes. However, name resolution is taking a long time and causing delay in the response from the route command. Which option to route can be added to cause it to not perform name resolution?

    1.  -d
    2.  -e
    3.  -f
    4.  -n

53.  You have replaced a device on the network but used the IP from another active device. Which command can be run to remove the MAC address entry from your computer so that it performs the address resolution again?

    1.  arp -d
    2.  netstat -rn
    3.  hostname
    4.  dig

54.  Which of the following commands displays information such as link status about the wireless device wlan0?

    1.  iw dev wlan0 link
    2.  wlan0 list
    3.  iw wlan0 -l
    4.  iw dev link

55.  Which command is used for setting parameters such as the essid, channel, and other related options for a wireless device?

    1.  ifconfig
    2.  iwconfig
    3.  wlancfg
    4.  iconf

56.  Which of the following commands can be used to scan for available wireless networks?

    1.  iwlist get
    2.  iwconfig scan
    3.  iwlist scan
    4.  iw-scan

57.  You need to offer internally facing NTP services. On which protocol and port does NTP listen?

    1.  TCP/20 and TCP/21
    2.  UDP/123
    3.  TCP/139
    4.  UDP/5150

58.  You need to set the MTU to a specific value for a network interface. Which option to ifconfig facilitates this?

    1.  -mtu
    2.  mtu
    3.  metric
    4.  addrmtu

59.  Which option to the arp command creates a new entry for a given IP address-to-MAC address pair?

    1.  -s
    2.  -c
    3.  -d
    4.  --add

60.  Which of the following commands shows network sockets and their allocated memory?

    1.  ss -m
    2.  mpas
    3.  mem
    4.  free

61.  When troubleshooting a potential hardware problem, you need to determine which physical interface is being used for a certain address. One way to accomplish this is with the ping command in order to monitor the activity lights on the device. Which of the following options to ping will flood the interface with ECHO_REQUEST packets?

    1.  -e
    2.  -a
    3.  -c
    4.  -f

62.  Which of the following commands can be used to test network connectivity at the TCP level instead of telnet?

    1.  netstat
    2.  nc
    3.  nettest
    4.  ping

63.  Which option to tcpdump displays a list of available interfaces on which tcpdump can operate?

    1.  -a
    2.  -d
    3.  -D
    4.  -i

64.  Which command provides a method for sending ICMP requests for IPv6?

    1.  ping6
    2.  pingv6
    3.  tracert
    4.  6ping

65.  Which of the following commands displays information about addresses, specifically only IPv6 addresses, currently in use on the computer?

    1.  ip addr
    2.  ip -6 addr
    3.  ip6add
    4.  ipv6addr

66.  Which of the following commands will disable ARP on the interface eth0?

    1.  ifconfig eth0 -arp
    2.  ip eth0 noarp
    3.  ifconfig eth0 noarp
    4.  if eth0 disable arp

67.  Which option to the route command forces the kernel to use the specified device for the route rather than attempting to determine the correct device?

    1.  inet
    2.  addr
    3.  dev
    4.  device

68.  Which option to the ss command shows the process IDs associated with the socket?

    1.  -l
    2.  -a
    3.  -p
    4.  -f

69.  Which option to traceroute causes the command to use ICMP for requests?

    1.  -T
    2.  -A
    3.  -I
    4.  -i

70.  Which programmatic function is used by the hostname command internally?

    1.  getaddr
    2.  gethost
    3.  gethostname
    4.  getname

71.  Which of the following commands will examine the system log for information regarding DHCP activity?

    1.  grep -i dhcp /var/log/syslog
    2.  grep -v dhcp /var/log/syslog
    3.  grep -vi dhcp /var/log/kern.log
    4.  dmesg | grep dhcp

72.  Which of the following characters are valid for hostnames in /etc/hosts?

    1.  Alphanumerics, minus, underscore, and dot
    2.  Alphanumerics, minus, and dot
    3.  Alphanumerics and dot
    4.  Alphanumerics

73.  Which of the following configuration lines in /etc/resolv.conf enables debugging?

    1.  debug
    2.  options debug
    3.  option debug
    4.  enable-debug

74.  Which of the following commands views systemd journal entries for the NetworkManager unit?

    1.  systemd NetworkManager
    2.  systemd NetworkCtl
    3.  systemctl NetworkManager
    4.  journalctl -u NetworkManager

75.  Which file is read at boot to set the local computer’s hostname?

    1.  /etc/hostname
    2.  /etc/hosts
    3.  /etc/localhost
    4.  /etc/networkhost

76.  Which traceroute command is used exclusively for IPv6 route traces?

    1.  trace6
    2.  traceroute6
    3.  tracert6
    4.  6trace

77.  Which type can be used with the dig command to test a zone transfer?

    1.  xfr
    2.  transfer
    3.  zxfr
    4.  axfr

78.  Which option to the host command sets the query type to ANY?

    1.  -a
    2.  -b
    3.  -c
    4.  -d

79.  Within which file can per-user default settings be created for the dig command?

    1.  /etc/dig.cfg
    2.  /etc/dig.conf
    3.  ~/.digrc
    4.  ~/.dig.conf

80.  Which type of DNS record is used for specifying a POP3 server?

    1.  POP
    2.  PO
    3.  MX
    4.  There is no specific type for POP3 servers.

81.  Which of the following iproute2 commands changes the address of device eth0 to 192.168.1.1 with netmask 255.255.255.0?

    1.  ip addr add 192.168.1.1/24 dev eth0
    2.  ip addr eth0 192.168.1.1 255.255.255.0
    3.  ip addr dev eth0 192.168.1.1 255.255.255.0
    4.  ip addr 192.168.1.1/255.255.255.0 eth0

82.  Which command is used to show the settings for DNS resolution with systemd-resolved?

    1.  systemctl resolvers
    2.  resolvectl status
    3.  systemctl --resolvers
    4.  resolvectl --view-status

83.  Which of the following commands enables NetworkManager so that it can be used to configure Ethernet and Wi-Fi network devices?

    1.  nmcli networking on
    2.  netman enable
    3.  NetworkManager --enable
    4.  nmti --enable networking

84.  You are troubleshooting a DNS problem using the dig command and receive a status: NXDOMAIN message. Which of the following best describes what NXDOMAIN means?

    1.  NXDOMAIN means that you have received a nonauthoritative answer for the query.
    2.  NXDOMAIN means that the domain or host is not found.
    3.  NXDOMAIN indicates a successful query.
    4.  NXDOMAIN signifies a new domain record has been added.

85.  Which systemd daemon can be used to manage network interfaces through systemd?

    1.  networker
    2.  networked
    3.  networkd
    4.  netwrkd

86.  Which command for hostnamectl can be used to set the hostname?

    1.  set-host
    2.  set-hostname
    3.  set-name
    4.  hostname

87.  On which port does IMAP over SSL (IMAPS) listen?

    1.  993
    2.  995
    3.  465
    4.  514

88.  When you’re looking to parse the output of the ip command, which option can you set to remove newlines so that the output can be piped to the grep command?

    1.  -n
    2.  -o
    3.  -l
    4.  -f

# Chapter 10
Topic 110: Security

**THE FOLLOWING EXAM OBJECTIVES ARE COVERED IN THIS CHAPTER:**

*   **![images](images/correction.png)  110.1 Perform security administration tasks.**
    *   Key knowledge areas:
        *   Audit a system to find files with suid sgid bit set.
        *   Set or change user passwords and password aging information.
        *   Be able to use nmap and netstat to discover open ports on a system.
        *   Set up limits on user logins, processes, and memory usage.
        *   Determine which users have logged in to the system or are currently logged in.
        *   Basic sudo configuration and usage
    *   The following is a partial list of the used files, terms, and utilities:
        *   find
        *   passwd
        *   fuser
        *   lsof
        *   nmap
        *   chage
        *   netstat
        *   sudo
        *   /etc/sudoers
        *   su
        *   usermod
        *   ulimit
        *   who, w, last
*   **![images](images/correction.png)  110.2 Setup host security.**
    *   Key knowledge areas:
        *   Awareness of shadow passwords and how they work
        *   Turn off network services not in use.
        *   Understand the role of TCP wrappers.
    *   The following is a partial list of the used files, terms, and utilities:
        *   /etc/nologin
        *   /etc/passwd
        *   /etc/shadow
        *   /etc/xinetd.d/
        *   /etc/xinetd.conf
        *   systemd.socket
        *   /etc/inittab
        *   /etc/init.d/
        *   /etc/hosts.allow
        *   /etc/hosts.deny
*   **![images](images/correction.png)  110.3 Securing data with encryption**
    *   Key knowledge areas:
        *   Perform basic OpenSSH 2 client configuration and usage.
        *   Understand the role of OpenSSH 2 server host keys.
        *   Perform basic GnuPG configuration, usage, and revocation.
        *   Use GPG to encrypt, decrypt, sign, and verify files.
        *   Understand SSH port tunnels (including X11 tunnels).
    *   The following is a partial list of the used files, terms, and utilities:
        *   ssh
        *   ssh-keygen
        *   ssh-agent
        *   ssh-add
        *   ~/.ssh/id_rsa and id_rsa.pub
        *   ~/.ssh/id_dsa and id_dsa.pub
        *   ~/.ssh/id_ecdsa and id_ecdsa.pub
        *   ~/.ssh/id_ed25519 and id_ed25519.pub
        *   /etc/ssh/ssh_host_rsa_key and ssh_host_rsa_key.pub
        *   /etc/ssh/ssh_host_dsa_key and ssh_host_dsa_key.pub
        *   /etc/ssh/ssh_host_ecdsa_key and ssh_host_ecdsa_key.pub
        *   /etc/ssh/ssh_host_ed25519_key and ssh_host_ed25519_key.pub
        *   ~/.ssh/authorized_keys
        *   ssh_known_hosts
        *   gpg
        *   gpg-agent
        *   ~/.gnupg/

1.  You need to temporarily prevent users from logging in to the system using ssh or another means. Which of the following describes one method for accomplishing this task?

    1.  touch /etc/nologin
    2.  Disable sshd.
    3.  Remove /etc/login.
    4.  Add a shadow file.

2.  Which of the following commands searches the entire filesystem for files with the setuid bit set?

    1.  find ./ -perm suid
    2.  find / -perm 4000
    3.  find / -type suid
    4.  find / -type f -perm setuid

3.  Which of the following commands displays the currently open ports and the process that is using the port?

    1.  netstat -a
    2.  lsof -i
    3.  ps auwx
    4.  netlist

4.  You are attempting to unmount a filesystem using the umount command. However, when you do so you receive a message indicating that the filesystem is in use. Which of the following commands can be used determine which process is keeping a filesystem open?

    1.  fuser
    2.  ls
    3.  find
    4.  ps

5.  Which of the following commands displays account information such as expiration date, last password change, and other related details?

    1.  usermod -l
    2.  userinfo -a
    3.  chageuser -l
    4.  chage -l

6.  Which of the following commands scans the IP address 192.168.1.154 for open ports?

    1.  nmap 192.168.1.154
    2.  lsof 192.168.1.154
    3.  netstat 192.168.1.154
    4.  netmap 192.168.1.154

7.  Which command is used to create a public/private key pair for use with ssh?

    1.  ssh -k
    2.  ssh-keygen
    3.  ssh-genkey
    4.  ssh -key

8.  Which of the following configuration options sets a hard limit of 25 processes for a user called suehring in /etc/security/limits.conf?

    1.  suehring hard proc 25
    2.  suehring hard nproc 25
    3.  suehring proc 25 hard-limit
    4.  proc 25 suehring hard

9.  Within which file should you place public keys for servers from which you will accept key-based ssh authentication?

    1.  ~/.ssh/authorized_keys
    2.  ~/.ssh/keys
    3.  ~/.ssh/keyauth
    4.  ~/.sshd/authkeys

10.  The system on which you are working does not have the lsof command installed, and you are not allowed to install software without going through four levels of approval and scheduling the installation weeks in advance. However, the netstat command is available. Which option to netstat will show the process ID to which a given network port is connected?

    1.  -a
    2.  -n
    3.  -p
    4.  -l

11.  You need to look at information on logins beyond that which is captured by the current log file for the last command. Which option to the last command can be used to load information from an alternate file?

    1.  -a
    2.  -t
    3.  -e
    4.  -f

12.  You need to examine who is currently logged in to the system. Which of the following commands will display this information?

    1.  listuser
    2.  fuser
    3.  ls -u
    4.  w

13.  You need to execute a command as a specific user. Which of the following commands enables this to occur?

    1.  sudo -u
    2.  sudo -U
    3.  sudo -s
    4.  sudo -H

14.  Which option in /etc/sudoers will cause the specified command to not prompt for a password?

    1.  PASSWORD=NO
    2.  NOPASSWD
    3.  NOPASSWORD
    4.  NOPROMPT

15.  Which of the following commands will display the CPU time, memory, and other limits for the currently logged-in user?

    1.  reslimit
    2.  limitres -a
    3.  ulimit -a
    4.  proclimit -n

16.  Which line in the /etc/hosts.deny file will prevent any host within the 192.168.1.0/24 network from accessing services that operate from xinetd?

    1.  BLOCK: 192.168.1.0/24
    2.  REJECT: 192.168.1.0
    3.  ALL: 192.168.1.0/255.255.255.0
    4.  NONE: 192.168.1/255.255.255.0

17.  When expiring a user account with usermod -e, which of the following represents the correct date format?

    1.  YYYY-MM-DD
    2.  MM/DD/YYYY
    3.  DD/MM/YY
    4.  MM/DD/YY HH:MM:SS

18.  Which of the following directives in a configuration file found within /etc/xinetd.d will prevent the service from starting?

    1.  enable no
    2.  start no
    3.  disable yes
    4.  boot no

19.  You are using an RSA-based key pair for SSH. By default, what is the name of the private key file in ~/.ssh?

    1.  id_rsa
    2.  id_rsa.priv
    3.  id_rsa.key
    4.  rsa_key.priv

20.  Which option to the su command will execute a single command with a noninteractive session?

    1.  -s
    2.  -u
    3.  -c
    4.  -e

21.  Which file is used to enable the setting of limits for things like logins, processes, memory, and the like for users?

    1.  /etc/security/limits.conf
    2.  /etc/userlimits.conf
    3.  /etc/security/userlimits.conf
    4.  /etc/security/procmem.conf

22.  Which of the following best describes the method to use with ssh in order to execute a single command on a remote server?

    1.  Use the -e option followed by the command.
    2.  Send the command after the other options as part of the command line.
    3.  Use the --execute option followed by the command.
    4.  Use the -s option followed by the command.

23.  When you’re using ssh-agent, which command and option lists the currently loaded keys?

    1.  ssh-agent -l
    2.  ssh -l
    3.  ssh-list-keys
    4.  ssh-add -l

24.  Which of the following commands should be used to edit the /etc/sudoers file?

    1.  Any text editor such as vi or emacs
    2.  editsudo
    3.  visudo
    4.  visudoers

25.  Which of the following commands can be used to stop a given service, such as httpd.service, from starting on boot with a systemd-based system?

    1.  systemctl disable httpdservice
    2.  systemctl stop httpd.service
    3.  systemd disable httpd.service
    4.  systemd enable httpd.service boot=no

26.  Which of the following commands will set an account to expire based on the number of days elapsed since January 1, 1970?

    1.  passwd -e
    2.  chage -E
    3.  usermod -l
    4.  chguser

27.  You need to specify a list of known hosts for SSH for certain hosts within your organization rather than each user needing to accept those keys individually. Which option within a server-wide SSH client configuration file enables this scenario?

    1.  KnownHosts
    2.  PerMachineKnownHosts
    3.  GlobalKnownHostsFile
    4.  ServerKnownHostsFile

28.  Which option within /etc/security/limits.conf is used to control the number of times that a given account can log in simultaneously?

    1.  nlogins
    2.  loginmax
    3.  maxlogins
    4.  loginlimit

29.  Which file can be used to store a server-wide cache of hosts whose keys are known for ssh?

    1.  /etc/sshd_known_hosts
    2.  /etc/ssh_known_hosts
    3.  ~/.ssh/known_hosts
    4.  /root/ssh_known_hosts

30.  Within the following entry in /etc/shadow, to what does the number 15853 refer?

    *   mail:*:15853:0:99999:7:::

    1.  The UID of the mail user
    2.  The number of files owned by mail
    3.  The date of the last password change (since 1/1/1970)
    4.  The number of days until the account expires

31.  Which of the following commands sets up a local port-forwarding session on local port 5150 to remote port 80 of [www.example.com?](http://www.example.com?)

    1.  ssh -L 5150:[www.example.com:80](http://www.example.com:80)
    2.  ssh 5150:[www.example.com](http://www.example.com)
    3.  ssh -p 5150 [www.example.com](http://www.example.com)
    4.  ssh -e 5150 [www.example.com:80](http://www.example.com:80)

32.  Which option must be enabled in /etc/sshd_config on the destination server in order for X11 forwarding to work?

    1.  XForward yes
    2.  Xenable yes
    3.  X11Forwarding yes
    4.  Xconnection yes

33.  Which of the following commands generates a GnuPG key pair?

    1.  gpg --gen-key
    2.  gpg --key
    3.  gpg --send-key
    4.  gpg --create-key

34.  Signatures with gpg can be generated by using which option on the gpg command line?

    1.  --sign
    2.  --signature
    3.  --si
    4.  --dsign

35.  Which option to ssh is used to set the port for the remote host?

    1.  -p
    2.  -P
    3.  -l
    4.  @

36.  Which option to nmap sets the scan to use TCP SYN packets for finding open ports?

    1.  -sS
    2.  -sT
    3.  -sY
    4.  -type SYN

37.  Which of the following logs is used by the last command for detailing recent logins?

    1.  /var/log/last
    2.  /var/log/all.log
    3.  /var/log/wtmp
    4.  /var/log/logins

38.  Which option to ssh enables the use of a key for authentication?

    1.  -i
    2.  -k
    3.  -f
    4.  --key

39.  In a scripting scenario, you need to prevent sudo from prompting for credentials or for any other reason. Which option to sudo is used to indicate this?

    1.  -n
    2.  --noprompt
    3.  -i
    4.  -q

40.  Which of the following commands generates an RSA key for use with ssh?

    1.  ssh -key rsa
    2.  ssh --gen-key rsa
    3.  ssh-keygen -t rsa
    4.  ssh-keygen rsa

41.  You need to disable a service found in /etc/inetd.conf. Which of the following is used as a comment character in that file?

    1.  -
    2.  #
    3.  /
    4.  %

42.  Which of the following commands can be used to lock an account?

    1.  usermod -L
    2.  usermod -l
    3.  passwdlock
    4.  lockacct

43.  Which file is used as the default storage for public keyrings for gpg?

    1.  publickeys.gpg
    2.  pubring.gpg
    3.  public.gpg
    4.  pubkeys.gpg

44.  Which file in ~/.gnupg/, if present, indicates that files have been migrated to gpg version 2.1 or later?

    1.  .gpg-v21
    2.  .gpg-updated
    3.  .gpg-v21-migrated
    4.  .gpg-files-v21

45.  Which of the following commands searches a server for files with the setgid bit enabled?

    1.  find / -perm 4000
    2.  find ./ -perm setgid
    3.  grep setgid *
    4.  find / -perm 2000

46.  Which of the following commands creates links within /etc/rc.d/* for starting and stopping services on a Debian system?

    1.  createsym
    2.  startstop-service
    3.  update-rc.d
    4.  createconfig

47.  Which runlevel is typically used for single-user mode, as indicated in /etc/inittab?

    1.  1
    2.  2
    3.  5
    4.  6

48.  Which option to the su command is used to obtain the normal login environment?

    1.  -u
    2.  -U
    3.  -
    4.  -login

49.  Which of the following commands shows network services or sockets that are currently listening along with sockets that are not listening?

    1.  netstat -a
    2.  netlink -a
    3.  sockets -f
    4.  opensock -l

50.  Which of the following commands lists open files belonging to all processes except those owned by the user bind?

    1.  lsof -i
    2.  lsof -u bind
    3.  lsof -u ^bind
    4.  lsof | grep bind

51.  Which option to nmap will cause it to always perform name resolution?

    1.  -n
    2.  -R
    3.  -b
    4.  -a

52.  Which wildcard can be used in /etc/hosts.allow to specify a match for a host whose name does not match its IP address?

    1.  *
    2.  ALL
    3.  PARANOID
    4.  NAMEMATCH

53.  Which of the following options within an OpenSSH server configuration is used to determine whether the root user can log in directly with an SSH client?

    1.  PermitRootLogin
    2.  AllowRoot
    3.  RootLogin
    4.  PermitDirectRootLogin

54.  Which of the following commands executes a port scan using TCP connect to the host 192.168.2.3?

    1.  portscan 192.168.2.3
    2.  nmap -sT 192.168.2.3
    3.  maphost 192.168.2.3
    4.  tcpscan -C 192.168.2.3

55.  Which option to the ssh command is used for X11 application forwarding?

    1.  -X11
    2.  -A
    3.  -X
    4.  -F

56.  Which option to gpg should be used in order to specify the destination for the encrypted file?

    1.  --dest
    2.  --output
    3.  --destination
    4.  --out

57.  Which command is used to add keys to the SSH agent?

    1.  ssh-keyadd
    2.  ssh-add
    3.  ssh-ed
    4.  ssh-cat

58.  Which option to the passwd command sets the maximum password age until the password needs to be changed?

    1.  -a
    2.  -x
    3.  -l
    4.  -r

59.  Which option to the ulimit command enables setting of a limit on memory that can be locked?

    1.  -l
    2.  -x
    3.  -b
    4.  -t

60.  Which of the following commands prints a list of existing users from the password file?

    1.  passwd --list
    2.  cat /etc/passwd | cut -d':' -f1
    3.  grep "USERS" /etc/passwd
    4.  lookup --user

61.  You are defining a service in /etc/xinetd.conf. Which option is used to configure the times that access to the service is allowed?

    1.  time_allowed
    2.  access_times
    3.  timed_access
    4.  access_when

62.  What file extension is used for interprocess communication service units that are controlled by systemd?

    1.  .socket
    2.  .ipc
    3.  .comm
    4.  .intercom

63.  You are generating a host key for the SSH server with ssh-keygen and want to ensure that the key does not require a password when the SSH server starts. Which command-line option accomplishes this task?

    1.  -p
    2.  -P
    3.  -N
    4.  -d

64.  When working with the /etc/shadow password file, you see passwords beginning with $1$. What algorithm does $1$ indicate has been used for password storage?

    1.  MD5
    2.  Blowfish
    3.  RIN
    4.  PIK

65.  Which option to gpg creates a detached signature?

    1.  --sig
    2.  --detach-sig
    3.  --det-sig
    4.  --sgn-det

66.  Which of the following best describes the role of server host keys for SSH?

    1.  The server host key is used to connect to remote servers.
    2.  The server host key is used for encrypting SSL communications.
    3.  The server host key is used for client connections and provides a means by which the client can verify that the server has not changed.
    4.  The server host key provides secure DNS resolution.

67.  When using a custom client configuration for SSH, which option specifies the key that will be used to connect to the host?

    1.  KeyFile
    2.  IdentityFile
    3.  Key
    4.  HostKey

68.  Which of the following commands is used as a daemon process to manage private keys for GnuPG?

    1.  gpgpkd
    2.  gpg_pkd
    3.  gpg-agent
    4.  gpg-pkagent

69.  You need to enable editing of certain files with root privileges but do not want to grant sudo access to an editor such as vim due to the possibility of a shell escaping. Which command can be used in place of vim to provide privileged editing of files?

    1.  suvim
    2.  nano
    3.  sudon
    4.  sudoedit

70.  Which option to the ssh command enables changing the login name for a given host?

    1.  -l
    2.  -u
    3.  -a
    4.  -m

71.  Which option to the usermod command changes a username?

    1.  -l
    2.  -u
    3.  -a
    4.  -m

72.  After specifying the key server, which option to gpg is used to specify the key to send to the key server?

    1.  key-name
    2.  keyname
    3.  send-keys
    4.  sendkey

73.  Which of the following represents a group called admins within /etc/sudoers?

    1.  @admins
    2.  admins
    3.  -admins
    4.  %admins

74.  Which limits-related option is used to control the maximum file size that a user can create?

    1.  filesize
    2.  maxfile
    3.  fsmax
    4.  fsize

75.  You are using an SSH server over a poor network connection but would like to maintain the connection in the event of keepalive messages being lost. Which client option can be set to set the number of keepalive messages that can be lost before the client will terminate the connection?

    1.  ServerTerminateCount
    2.  ServerAliveCountMax
    3.  ServerKeepAliveCount
    4.  ServerClientKeepAliveCount

76.  If the /etc/nologin file exists and is in use preventing users from logging in, which file can be used to provide a message to those users who are refused a login?

    1.  /etc/login.mesg
    2.  /etc/login.disabled
    3.  /etc/nologin
    4.  /etc/nologin.message

77.  Which option to ssh-add specifies the lifetime that a key is held in the agent?

    1.  -t
    2.  -a
    3.  -l
    4.  -c

78.  Which option for an SSH connection sets up a remote forwarding scenario?

    1.  -R
    2.  -r
    3.  -e
    4.  -d

79.  Which option to chage sets the number of days that a user will be warned before they need to change their password?

    1.  -w
    2.  -W
    3.  -t
    4.  -a

80.  Another administrator made a change on the system that resulted in the /etc/shadow file becoming corrupted. Which of the following can be used to recover quickly?

    1.  The /etc/shadow.bak file
    2.  The /etc/shadow- file
    3.  The latest backup in /var/backups/
    4.  Single-user mode

81.  When examining the documentation for a service, you notice that it can use libwrap. What functionality does libwrap enable?

    1.  Start/stop from remote
    2.  TCP wrappers
    3.  DNS resolution
    4.  Shadow passwords

82.  Which option within /etc/sudoers enables the use of an alias for a group of users?

    1.  User_Alias
    2.  User_Group
    3.  User_List
    4.  User_Spec

83.  You are using nmap to scan a host for open ports. However, the server is blocking ICMP echo requests. Which option to nmap can you set in order to continue the scan?

    1.  -P0
    2.  -no-ping
    3.  -s0
    4.  -ping-0

84.  Which option within a server-wide SSH client configuration specifies the name and location of the known hosts file to use?

    1.  KnownHosts
    2.  UserKnownHosts
    3.  UserKnownHostsFile
    4.  UserKnownHostsFilePath

85.  You need to generate a host key for SSH using ssh-keygen that has been generated with DSA rather than RSA. Which option and argument to that option will create a DSA key?

    1.  -k dsa
    2.  -a DSA
    3.  -t dsa
    4.  -h dsa

86.  The total number of users logged in can be found with which argument to the who command?

    1.  -t
    2.  -e
    3.  -q
    4.  -l

87.  Which option to the passwd command unlocks an account?

    1.  -t
    2.  -u
    3.  -r
    4.  -l

88.  Which option for user limits sets the maximum number of logins that a user can have on the system?

    1.  maxsyslogins
    2.  maxuserlogins
    3.  maxlogins
    4.  kennyloggins

# PART III
Practice Exams

# Chapter 11
Practice Exam 1

1.  Which filesystem is used to store information about current running processes?

    1.  /environment
    2.  /proc
    3.  /etc
    4.  /dev

2.  What is the default directory for configuration information related to the modprobe command?

    1.  /etc/modprobe.conf
    2.  /etc/modprobe
    3.  /etc/modprobe.d
    4.  /var/modprobe

3.  Which of the following wall commands send the message "Please Log Off" to users in the operator group?

    1.  wall -g operator "Please Log Off"
    2.  wall "Please Log Off"
    3.  wall -operator "Please Log Off"
    4.  echo "Please Log Off" | group operator

4.  Which option to dmesg displays the time in local time?

    1.  -rel
    2.  -e
    3.  -f
    4.  -t

5.  Which process ID is typically associated with the init process?

    1.  0
    2.  1
    3.  5
    4.  100

6.  You have been troubleshooting a system issue that may be related to the driver in use for a PCI device in the system. Which command and option will display the PCI devices and the drivers being used for those devices?

    1.  lsusb -v
    2.  ls -pci
    3.  lspci -k
    4.  showpci

7.  Which option to the telinit command will cause the operation to not send any notice to logged-on users?

    1.  -q
    2.  -v
    3.  --no-wall
    4.  -l

8.  Which file in the sysfs filesystem could you view in order to see the MAC address of eth0?

    1.  /sys/class/net/eth0/address
    2.  /sys/devices/eth0
    3.  /sysfs/devices/eth0
    4.  /sys/net/eth0

9.  When using systemctl to kill a process, what is the default signal sent to a process?

    1.  SIGKILL
    2.  SIGTERM
    3.  SIGINT
    4.  SIGCALL

10.  A newly added Serial ATA (SATA) disk is not showing up during the boot process. Where can you check to begin troubleshooting this issue?

    1.  Using system logging
    2.  Using debugfs
    3.  Within the fdisk utility
    4.  Within the computer BIOS

11.  Which command can be used to monitor communication taking place with dbus?

    1.  dbus-mon
    2.  dbus -m
    3.  dbus-monitor
    4.  dbus-debug

12.  Within a systemd environment, which service manages udev?

    1.  systemd-udevd.service
    2.  systemd-udev.service
    3.  udevd-service
    4.  systemd.udevd-service

13.  What is the correct syntax to indicate that the system should shut down at 8 p.m.?

    1.  shutdown 20:00
    2.  shutdown 8pm
    3.  shutdown +20:00
    4.  halt 20

14.  Which option to the systemctl kill command will change the signal sent to the process to be killed?

    1.  -k
    2.  -f
    3.  -s
    4.  -d

15.  Which systemd command and option is equivalent to the chkconfig --list command in a SysVinit environment?

    1.  systemctl list-unit-files
    2.  systemctl list-service
    3.  systemctl --list
    4.  systemctl list-unit-files --type=service

16.  Which option to ldconfig is used to change the location of the cache to be updated?

    1.  -C
    2.  -c
    3.  --f
    4.  -v

17.  Which of the following commands will remove all files for a package in Debian, including configuration files?

    1.  apt-get remove
    2.  apt-cache clean
    3.  dpkg -P
    4.  apt-get conf-remove

18.  What is the prefix used to denote a Debian source repository in /etc/apt/sources.list?

    1.  deb
    2.  source
    3.  deb-src
    4.  debsrc

19.  Which options to rpm will upgrade a package while displaying progress and other additional information about the operation?

    1.  -Iv
    2.  -Uvh
    3.  -U
    4.  -vh

20.  Which option to a yum install command will cause yum to assume yes and therefore not prompt for verification when performing actions deemed critical?

    1.  -y
    2.  -f
    3.  -p
    4.  -m

21.  When working with a yum-based system, you need to create a configuration to ensure that certain packages are not upgraded or installed. Which option can you set in /etc/yum .conf to facilitate this behavior?

    1.  exclude
    2.  noupdate
    3.  assumeupdate
    4.  clearupdate

22.  You are having difficulty with shared libraries on the system. Which of the following commands will print the current directories and libraries in the cache?

    1.  ldconfig -C
    2.  ldd -f
    3.  ldconfig -p
    4.  ldd -b

23.  Which option within a .repo file in /etc/yum.repos.d/ is used to set the URL for the repository?

    1.  url
    2.  repourl
    3.  httpurl
    4.  baseurl

24.  Which command and option is used to display basic information about each available package and its dependencies on a Debian system?

    1.  apt-get list
    2.  apt-cache dump
    3.  apt-get list-all
    4.  apt-cache list

25.  When running the lsblk command, there is no separate partition listed for /boot. From which partition is the system likely booted?

    1.  There is a /boot directory under the / partition.
    2.  The /boot partition is hidden.
    3.  The system has not yet built the /boot partition.
    4.  The /boot partition does not show up with lsblk.

26.  Within which hierarchy is cached data stored for both yum- and apt-style systems?

    1.  /etc
    2.  /var/cache
    3.  /usr/lib
    4.  /tmp

27.  On a BIOS-based system, within which region of the disk is the boot loader typically installed?

    1.  MBR
    2.  /boot
    3.  Sector 8192
    4.  Front

28.  Which of the following best describes the contents of the / filesystem within Linux?

    1.  The / filesystem is the root filesystem and contains temporary files.
    2.  The / filesystem is root’s home directory.
    3.  The / filesystem is used for storage of device and swap information.
    4.  The / filesystem is the root filesystem and is the logical root of the hierarchy within Linux.

29.  Which of the following commands will send the output of the grub-mkconfig command to the correct location for booting?

    1.  grub-mkconfig --output=/boot/grub2/grub.cfg
    2.  grub-mkconfig --file=/boot/grub2.menu
    3.  grub-mkconfig --file=/boot/grub.lst
    4.  grub-mkconfig --output=/boot/menu.lst

30.  Which of the following commands writes an image called from the current directory called raspbian.img to the SD card mounted at /dev/sdc?

    1.  dd if=raspbian.img of=/dev/sdc bs=1M
    2.  imgwrite raspbian.img > /dev/sdc
    3.  imgw raspbian.img | cat /dev/sdc
    4.  dd raspbian.img > /dev/sdc

31.  When troubleshooting a problem, you look through .bash_history to determine commands that you’ve recently executed. However, the file does not contain information from your current session. Which command can you use to view the commands that have been executed during the current session?

    1.  cmdhist
    2.  cmds
    3.  pwd
    4.  history

32.  Which option should be sent to grub-install if you want to install the boot images within a directory other than /boot?

    1.  --boot
    2.  --image
    3.  --boot-directory
    4.  --b

33.  Which command should be run in order to make changes take effect for a GRUB2 configuration change?

    1.  update-grub
    2.  grub-update
    3.  grub-config
    4.  grub-ins

34.  Which of the following commands will set the environment variable JAVA_PATH equal to /home/user/java2 when using the Bash shell?

    1.  invoke JAVA_PATH=/home/user/java2
    2.  export JAVA_PATH=/home/user/java2
    3.  envvar JAVA_PATH=/home/user/java2
    4.  echo JAVA_PATH=/home/user/java2

35.  Which option in the .bashrc sets the number of commands to keep in the .bash_history file?

    1.  HISTLIMIT
    2.  HISTORYFILE
    3.  HISTFILESIZE
    4.  HISTNUM

36.  Which of the following commands will cause nl to number all lines, including blank lines, for a file called code.php?

    1.  nl code.php
    2.  nl -a code.php
    3.  nl -n code.php
    4.  nl -b a code.php

37.  Which command can be used to create an octal representation of a given plaintext file?

    1.  oct
    2.  cat
    3.  list
    4.  od

38.  Which command and option can be used to format text with pagination in a double-space format, including page numbers?

    1.  pr -d
    2.  pag -db
    3.  cat -pd
    4.  print -d

39.  Of the following options for the tail command, which option outputs the last lines beginning at the 30th line from the start of the file rather than the end of the file?

    1.  -n +30
    2.  -n 30
    3.  -30
    4.  +30

40.  Which option to the uniq command causes the matching to be done in a case-insensitive manner?

    1.  -c
    2.  -f
    3.  -i
    4.  -n

41.  Which of the following commands prints the username and real name of all users in /etc/passwd in a tab-separated format?

    1.  cut -d: -f 1,6 /etc/passwd
    2.  sed 's/://' /etc/passwd
    3.  awk -F: '{print $1,$5}' OFS="\t" /etc/passwd
    4.  cat -o "\t" /etc/passwd

42.  Which option to cp will preserve symlinks in a recursive copy?

    1.  -f
    2.  -d
    3.  -a
    4.  -b

43.  Which of the following key combinations is a technique for moving to the 23rd line of a file in Vi?

    1.  23G
    2.  /23
    3.  i23
    4.  ZZ

44.  Which option to the top command changes the update interval?

    1.  -d
    2.  -t
    3.  -n
    4.  -f

45.  Which of the following commands will display the process ID, the real user ID, the filesystem access user ID, and command for processes on the system?

    1.  listproc -uf
    2.  ps -eo pid,euser,fuser,comm
    3.  ps -e pid,user,comm
    4.  ps -fa

46.  Which command can be used to search the contents of all files below your current location for files that contain the characters DB?

    1.  grep -r "DB" *
    2.  grep -ri "DB" *
    3.  cat * | less
    4.  cat *.txt | grep DB

47.  Which of the following commands will locate all files that begin with the name DB, starting from the current directory?

    1.  locate "DB*"
    2.  find ./ -name "DB*"
    3.  whereis "DB*"
    4.  find "DB*"

48.  Which of the following files is the location used to gather information about load average for use in the uptime command?

    1.  /proc/uptime
    2.  /proc/loadavg
    3.  /proc/load
    4.  /proc/utime

49.  When running fsck on an EXT3 filesystem, which option to fsck causes the operation to prompt when attempting a repair action?

    1.  -y
    2.  -f
    3.  -a
    4.  No option required

50.  Which of the following files is updated dynamically with information about currently mounted filesystems?

    1.  /etc/fstab
    2.  /etc/files
    3.  /boot/fstab
    4.  /etc/mtab

51.  When running the df command, you need to change the scale so that the report shows terabytes instead of bytes. Which option will accomplish this task?

    1.  -ST
    2.  -BT
    3.  -j
    4.  -T

52.  What command can be used to create an image of important metadata for an ext3 filesystem?

    1.  e2image
    2.  e3image
    3.  dumpe2fs
    4.  dumpe3fs

53.  Which option to mke2fs is used to check for bad blocks during filesystem creation?

    1.  -a
    2.  -b
    3.  -c
    4.  -d

54.  Which of the following commands changes the ownership of the file called Class.java to the user steve and the group developers?

    1.  chgrp steve:developers Class.java
    2.  chown steve.developers Class.java
    3.  chown developers.steve Class.java
    4.  chown Class.java steve.developers

55.  When bootstrapping a virtual machine, which command can be used to add the fingerprint of a server to the known_hosts file?

    1.  ssh-keyscan
    2.  ssh-keyadd
    3.  ssh-keylist
    4.  ssh-getkey

56.  Which configuration option can be set within /etc/default/grub to affect the behavior of the system after a failed boot?

    1.  GRUB_RECOVER
    2.  GRUB_NOFAIL
    3.  GRUB_RECORDFAIL_TIMEOUT
    4.  GRUB_RECOVER_TIMEOUT

57.  Which options to du will print a summary of information in a human-readable format?

    1.  -sh
    2.  -h
    3.  -s
    4.  -su

58.  Which option to the find command causes it to follow symbolic links?

    1.  -S
    2.  -H
    3.  -P
    4.  -L

59.  Which option to the tee command enables appending to the destination files rather than overwriting?

    1.  -a
    2.  -m
    3.  -g
    4.  -d

60.  When creating a backup for a system, which directory should be included so that most configuration files will be backed up?

    1.  /var
    2.  /opt
    3.  /etc
    4.  /bin

# Chapter 12
Practice Exam 2

1.  To which file should you add an entry in order for a host to be blocked using TCP wrappers?

    1.  /etc/hosts.deny
    2.  /etc/tcp.wrappers
    3.  /etc/wrap.config
    4.  /etc/tcpwrap.conf

2.  Which of the following commands creates an alias for the ps command such that the options auwx are included when the user types psa?

    1.  alias "ps auwx" = "psa"
    2.  alias psa=ps uawx
    3.  alias psa="ps auwx"
    4.  psa="ps auwx"

3.  Which of the following conditionals in a Bash script will test if the variable DAY is equal to SUNDAY?

    1.  if ($DAY == "SUNDAY")
    2.  if ($DAY -eq "SUNDAY")
    3.  if [[ $DAY == "SUNDAY" ]]
    4.  if [ DAY = "SUNDAY" ]

4.  Which of the following commands is necessary for making a variable defined in your current shell available to child processes?

    1.  export
    2.  source
    3.  let
    4.  def

5.  You are watching another administrator perform some work on a server. As part of that work, the admin uses the following command:

    . variables.sh

    Which of the following is the equivalent of . variables.sh?

    1.  let variables.sh
    2.  set variables.sh
    3.  source variables.sh
    4.  var variables.sh

6.  Which of the following commands adds ~/code/bin to the path?

    1.  PATH=~/code/bin:$PATH
    2.  PATH=/code/bin:$PATH
    3.  PATH=/home/code/bin:$PATH
    4.  PATH=PATH:~/code/bin

7.  Which of the following shows a valid Bash function called sayHello?

    1.  function sayHello () { echo "hello"; }
    2.  function sayHello{}
    3.  function sayHello() { echo Hello }
    4.  function sayHello() { echo Hello } ;

8.  Which of the following commands sends an email to root with the subject of Update and the content of the /etc/hostname file?

    1.  mail root > /etc/hostname
    2.  mail -s Update root > /etc/hostname
    3.  mail -s Update root < /etc/hostname
    4.  mail root -s Update /etc/hostname

9.  Files that should be copied to a user’s home directory when their account is created should be placed in which of the following directories?

    1.  /etc/usertemplate
    2.  /etc/template
    3.  /etc/skel
    4.  /etc/userskel

10.  Which of the following areas within an Ubuntu system contains information and settings for accessibility?

    1.  Accessibility
    2.  Access and Help
    3.  Universal Use
    4.  Universal Access

11.  Which command can be used to set the delay and repeat rate for a keyboard?

    1.  keyboard
    2.  kbdrate
    3.  kbd
    4.  keyrate

12.  Which variable is used to indicate the screen on which GUI applications will be shown?

    1.  DISPLAY
    2.  SCREEN
    3.  LIST
    4.  XWIN

13.  Users can be added or removed for access to the X server. Which command facilitates this?

    1.  xauthorization
    2.  xhost
    3.  xwin
    4.  xconnect

14.  Which option to useradd sets the number of days between password expiration and when the account is disabled?

    1.  -n
    2.  -f
    3.  -e
    4.  -g

15.  Which of the following commands displays the current mail aliases known on the server?

    1.  getent aliases
    2.  getalias
    3.  listalias
    4.  mail aliases

16.  Which of the following configuration lines in /etc/hosts.deny creates a deny-by-default policy where clients will need to be specifically allowed in /etc/hosts.allow?

    1.  *.*
    2.  All: *
    3.  ALL: ALL
    4.  LOC: ALL

17.  Which of the following describes the result of running the atq command as root?

    1.  The current cron and at jobs for root will be listed.
    2.  The current at jobs for all users will be listed.
    3.  The current cron and at jobs for all users will be listed.
    4.  The last 10 entries in the at log will be shown.

18.  Which command option can be used to remove all cron jobs for a given user using the crontab command?

    1.  -d
    2.  -e
    3.  -r
    4.  -l

19.  Which option to the crontab command enables you to work with a different user’s cron jobs?

    1.  -u
    2.  -m
    3.  -d
    4.  -e

20.  When deleting a user from the server, you need to maintain their home directory rather than deleting it. Which option of the following commands deletes the user <username> but preserves their home directory?

    1.  userdel <username>
    2.  userdel -r <username>
    3.  userdel -h <username>
    4.  userdel -p <username>

21.  After deleting a group, you need to search the filesystem for files owned by the group using its group ID. Which option to the find command will search using the group ID?

    1.  -name
    2.  -group
    3.  -groupid
    4.  -gid

22.  Which of the following commands changes the group name from admins to serveradmins?

    1.  groupmod -g admins serveradmins
    2.  groupmod -n serveradmins admins
    3.  groupchg -n serveradmins admins
    4.  groupchg admins -n serveradmins

23.  Which command is used to parse log file entries on a systemd-based system?

    1.  logger
    2.  journalentry
    3.  jrnctl
    4.  journalctl

24.  Which option to the ntpdate command configures the version to use such that an older Network Time Protocol (NTP) server could be queried?

    1.  -o
    2.  -v
    3.  -e
    4.  -r

25.  Within which directory are systemd journals stored by default?

    1.  /var/log/systemd
    2.  /var/systemd/journal
    3.  /var/log/journald
    4.  /var/log/journal

26.  Which option to the logrotate command specifies the mailer to use?

    1.  -o
    2.  -s
    3.  -m
    4.  -v

27.  Which option to date changes the output to Coordinated Universal Time (UTC) regardless of the current time zone?

    1.  -u
    2.  -t
    3.  -s
    4.  -v

28.  Which of the following commands can be used to delete a print job on a system that uses the lp print system?

    1.  lpdel
    2.  rmprint
    3.  rm -print
    4.  lprm

29.  Which of the following subnet masks represents a /23?

    1.  255.255.255.0
    2.  255.255.0.0
    3.  255.255.255.255
    4.  255.255.254.0

30.  An entry in /etc/nsswitch.conf indicates hosts: files dns. In which order will /etc/hosts be queried for a hostname lookup?

    1.  The /etc/hosts file will be examined first.
    2.  The /etc/hosts file is not related to hostname lookup.
    3.  The /etc/hosts file will be queried second.
    4.  The /etc/hosts file will be queried last.

31.  Which port needs to be allowed through the firewall for standard Lightweight Directory Access Protocol (LDAP) traffic to be received by the server?

    1.  TCP port 25
    2.  TCP port 443
    3.  TCP port 143
    4.  TCP port 389

32.  Which option to ssh changes the username to use for logging in to the server?

    1.  -v
    2.  -i
    3.  -l
    4.  -u

33.  Which option to ping disables name resolution?

    1.  -d
    2.  -D
    3.  -f
    4.  -n

34.  Which of the following commands shows various statistics for a network interface such as packets and bytes received and transmitted along with errors and other such conditions?

    1.  ifconfig
    2.  ifstat
    3.  if -s
    4.  ifcond

35.  When using the host command, which option displays the Start of Authority (SOA) record from each of the authoritative DNS name servers for the given domain?

    1.  -N
    2.  -n
    3.  -C
    4.  -a

36.  You need to specify an additional localhost address and hostname for a server in order to support a specialized network configuration. Which line in /etc/hosts sets the hostname with a unique IP address in the correct range for localhost?

    1.  127.0.1.1 host.example.com host
    2.  192.168.0.1 host.example.com host
    3.  host.example.com 127.0.0.1
    4.  host.example.com 172.16.31.32

37.  Which of the following options to ifup tells the command to ignore errors and continue?

    1.  --continue
    2.  --C
    3.  --ignore-errors
    4.  -h

38.  Which option to passwd can be used to unlock an account that was locked with the passwd command?

    1.  -S
    2.  -l
    3.  -u
    4.  -w

39.  Which of the following is the correct syntax to connect using ssh to host.example.com on port 2200?

    1.  ssh -l 2200 host.example.com
    2.  ssh host;example.com
    3.  ssh host.example.com:2200
    4.  ssh host:2200 -d example.com

40.  Which option in /etc/sudoers sets the destination address for administrative and security emails related to sudo?

    1.  mail
    2.  mailto
    3.  secmail
    4.  adminmail

41.  Which of the following commands displays a listing of who is logged in to the server along with the date and time that they logged in?

    1.  whois
    2.  who
    3.  loggedin
    4.  curusers

42.  Which port should be allowed through a firewall for NTP communication?

    1.  Port 139
    2.  Port 161
    3.  Port 123
    4.  Port 194

43.  Which option to nmap causes it to scan using UDP?

    1.  -sT
    2.  -sS
    3.  -sP
    4.  -sU

44.  Which of the following options to lsof searches an entire directory tree for open instances of files or directories?

    1.  -d
    2.  +D
    3.  -f
    4.  -i

45.  Which option to the ip command displays DNS names rather than merely IP addresses?

    1.  -n
    2.  -f
    3.  -r
    4.  -a

46.  Which of the following commands and options enables you to examine timing related to listening sockets?

    1.  ss -o
    2.  netstat -rn
    3.  ping -f
    4.  ls -l

47.  Which of the following IP address and subnet mask pairs represents a private network in a /24 size?

    1.  192.168.3.0/255.255.255.128
    2.  172.16.19.128/255.255.0.0
    3.  192.168.2.0/255.255.255.0
    4.  10.168.1.0/0.0.0.255

48.  When viewing the results of a traceroute, you see !H. To what does !H refer?

    1.  Network unreachable
    2.  Host available
    3.  Host unreachable
    4.  High length

49.  On which port does the ping command operate for Internet Control Message Protocol (ICMP) echo requests?

    1.  53
    2.  1337
    3.  33433
    4.  No port is used for ICMP.

50.  When using netstat -a, which file is consulted for the port number to name translation?

    1.  /etc/portnum
    2.  /etc/services
    3.  /etc/portnames
    4.  /proc/sys/net/ipv4/ports

51.  Which of the following commands launches Orca with speech capabilities?

    1.  orca --no-setup --disable main-window
    2.  orca --screen
    3.  orca --screen-reader
    4.  orca --no-setup -s

52.  Which of the following locations stores the configuration for LightDM?

    1.  /etc/lightdm/
    2.  /etc/lightdm.conf
    3.  /etc/lightdm-conf
    4.  /etc/lightdm.d

53.  Which of the following commands displays statistics and information about windows in X windows?

    1.  xinfo
    2.  xstats
    3.  xwin
    4.  xwininfo

54.  Which of the following commands can be used to set the time zone on a Debian system?

    1.  tzconfig
    2.  /etc/timeconfig
    3.  timeconfig
    4.  timecfg

55.  Which of the following commands displays the available character maps?

    1.  charmap
    2.  charmap -l
    3.  locale -m
    4.  mapinfo

56.  Within which directory hierarchy will you find information regarding the available time zones on the server?

    1.  /usr/zoneinfo
    2.  /usr/share/zoneinfo
    3.  /etc/zoneinfo
    4.  /etc/tz.conf.d

57.  The driftfile, as specified in /etc/ntp.conf on a Red Hat system, is stored in which location by default?

    1.  /var/lib/ntp/drift
    2.  /var/ntp/drift
    3.  /usr/share/ntpdrift
    4.  /usr/share/lib/ntpdrift

58.  Which character combination sets the body of the message to STDIN when using the mail command?

    1.  <
    2.  >
    3.  <<<
    4.  |

59.  Which of the following commands deletes a group from a CentOS Linux system?

    1.  groupdm
    2.  grouprm
    3.  groupdel
    4.  delgroup

60.  Which of the following syslog facilities captures messages from the lp printing facility?

    1.  auth
    2.  messages
    3.  lpr
    4.  root

# Appendix
Answers to Review Questions

## Chapter 1: Topic 101: System Architecture

1.  D. The udevadm command is used to work with the udev interface of the kernel, and the monitor subcommand displays kernel uevents and other udev events in real time.

2.  B. Current IRQ assignments are contained in the file /proc/interrupts. Therefore, viewing the contents of the file with a command such as cat will work. There is no “view” command, making option A incorrect. Likewise, there is no /dev/irq file, making options C and D incorrect.

3.  D. Configuration files for udev are found in /etc/udev, which makes option D correct. The other options do not exist.

4.  A. The modprobe command loads the module and its dependencies, if applicable. The lsmod command is used to list currently loaded modules, making option B incorrect. The insmod command will load a given module but not its dependencies. Option D, rmmod, is used to remove a module from memory.

5.  B. The lsusb command is used to obtain a basic list of USB devices on a system. The other commands are not valid. In the case of option D, the ls command is valid, but there is no --usb option.

6.  B. The info command for udevadm enables querying for additional information about a hotplug device managed with udev.

7.  D. The dmesg command displays the contents of the kernel ring buffer. On many Linux distributions, this log is also saved to /var/log/dmesg. The other options shown for this question are not valid commands.

8.  C. Runlevel 1, sometimes displayed as runlevel s or S, is single-user mode in which many services are not started. Runlevels 5 and 6 are used for other purposes, and runlevel SU is not a valid option.

9.  D. Scripts are stored in /etc/init.d on a system using SysV init. You may sometimes find these linked from /etc/rc.d/init.d as well. The other options are not valid for this question.

10.  A. The init command can be used to access different runlevels. Runlevel 6 is used for rebooting the system. Option B will shut down the system entirely, not reboot it. Option C will place the system into single-user mode. Option D is not a valid option.

11.  C. The telinit command can be used to refresh the system after changes have been made to /etc/inittab. Notably, option B will reboot the system but that was not an option in the question. Options A and D are not valid commands.

12.  D. The runlevel command displays the current runlevel for a system. Option B is not a valid option to the init command, and adding sudo in front of the init command makes no difference. Option A is not a valid command.

13.  C. Unit configuration files are stored in /lib/systemd/system. The other directory options for this question are not relevant or do not exist by default.

14.  B. The systemctl command is used to work with services and targets. The list-units command is used to list targets. The other commands are not used for this purpose or do not exist with the required option.

15.  C. The -nn option displays both numbers and device names, making option C correct. The -n option (option B) displays only numbers. The other two options do not exist.

16.  D. The lsmod command is used to list currently loaded kernel modules, making option D correct for this question. The insmod command (option A) is used to load modules. Option C is a valid command but not a valid option for that command, and option B does not exist.

17.  C. The --show-depends option shows the modules that depend on the specified module. The other options do not exist.

18.  B. The wall command is used to send a message to all users, thereby making option B correct. The cat command is used as a means to concatenate or view files, and tee is used to send output to standard output and a file. Finally, ssh is the secure shell client command and is not used for the purpose specified.

19.  B. Checking to ensure that the disk is detected in the basic input/output system (BIOS) is a good first step in troubleshooting. Option A, unplugging the disk, won’t help it to be detected. Restarting the web server won’t help detect the disk, and the disk-detect command does not exist.

20.  D. The /sys/bus/usb/devices directory contains information about USB devices. The other directories are not valid for this purpose.

21.  D. The file /var/log/dmesg will typically contain historical messages from the current booting of the system. On some distributions of Linux, this information is also in /var/log/boot.log.

22.  C. Out of the options given, the systemctl status command and option is the most appropriate. The telinit and sysctl commands are not used for this purpose. Likewise, the --ls option is not valid for systemctl.

23.  B. The isolate option is used to move the system into the target specified, making option B the correct one. The other options do not exist.

24.  A. The initctl reload command causes Upstart to reread its configuration files.

25.  B. The --list option will show all services on a system along with their status for each runlevel.

26.  C. USB devices are generally considered to be hotplug devices. Hotplug devices describe those devices that can be inserted and removed while the system is “hot,” or powered on, whereas coldplug devices are those that must be inserted and removed when the system is powered off.

27.  B. The umount command is used to unmount drives within a running system. The other commands do not exist.

28.  D. Of the options presented, running dmesg is a common way to determine the location to which the kernel has assigned the drive. Rebooting the system is not a good option, though it would work. There is no such thing as /var/log/usb.log, and the location of the drive may change regardless of port, depending on how the drive may be detected in the system.

29.  B. From these options, only B will shut down the system immediately. Option A will cancel a shutdown.

30.  C. The ExecStart option indicates the command to be executed on startup of a systemd service.

31.  D. The systemctl get-default command will show the default target. The other commands and options are not valid.

32.  A. The enable option configures the service to start on boot. The start option, D, is used to start a service immediately. The other options are not valid for this command.

33.  C. The /proc filesystem contains information about currently running processes and additional information about the kernel and current boot of the system.

34.  C. The -t option to lsusb will print output in a tree-like format so that you can see which devices are connected to which bus. The other arguments to lsusb are not valid, and the usblist command is not real.

35.  D. If a working device does not appear in lsmod, it typically means that the kernel has a driver already loaded by virtue of being compiled into the kernel itself rather than loaded through a module. The use of systemd (option A) or initramfs (option B) has no effect.

36.  C. The -w option causes the module to wait until it’s no longer needed prior to unloading. The -f option forces immediate removal and should be used with caution. The other options are not valid for rmmod.

37.  B. The tune2fs command can be used for this purpose but should be used with care because it can result in data corruption.

38.  C. Rules related to udev are stored in /etc/udev/rules.d. The /etc/udev hierarchy contains the udev.conf configuration file along with other components related to the configuration of udev.

39.  B. The -k option shows the kernel driver associated with a given PCI device and can be helpful when planning a new kernel compile. The -t option displays information in a tree-like structure, and -n uses numbers instead of device names. There is no -a option.

40.  B. The /etc/modprobe.d directory is used for storing configuration information related to modules such as that used for blacklisting purposes but also for other configuration information, such as udev and module options.

41.  B. The dracut command is used to create the initial RAM disk for newer systems and has replaced the legacy mkinitrd command used for the same purpose.

42.  D. The file /proc/kallsyms provides a way to view the currently loaded kernel symbols. This can be helpful for resolving module dependencies. Note that on legacy systems, this file might be called /proc/ksyms.

43.  A. The systool utility can be used to show currently loaded options for a given module. The modinfo -r command is not valid, and though modinfo shows information about a module, it does not include core size and other settings. The lsmod command cannot be used for this purpose, and there is no infmod command.

44.  B. The /proc/sys/kernel hierarchy contains vital configuration information about a kernel. These settings can be changed on a running system.

45.  B. The /etc/systemd/system directory is where it is recommended to store unit files for systemd. The other locations are not valid.

46.  C. The systemctl command will be used for this purpose with the daemon-reload subcommand. The reboot option would work to reload the systemd configuration but is not correct because it requires the entire server to reboot, which is not what was asked in this question.

47.  B. The /etc/inittab file contains the various runlevels and what to run at the given runlevel. For example, runlevel 1 is single-user, runlevel 6 is reboot, and so on. The other files listed do not exist.

48.  B. The SYSLINUX boot loader is used for FAT filesystems to create rescue disks and to assist with installation of Linux in general. SYSLINUX also describes an overall project containing other specialty boot loaders. The other options listed for this question are not valid boot loaders, though.

49.  C. initrd is used for an initial root filesystem for early drivers. initrd is configured to load within the GRUB configuration file for a given operating system.

50.  B. The fsck command is used to diagnose and repair hard drive problems in Linux. The defrag command is not available in Linux.

51.  D. The telinit command can be used for this purpose, and passing 1 as the argument will switch the system into single-user mode. The other commands shown are not valid.

52.  D. The -n option changes the boot order for the next boot only and boots from the specified partition. The -b along with -B modifies and then deletes the option. The -o option sets the boot order. The -c option creates a boot number.

53.  A. ISOLINUX provides a means by which CD-ROMS formatted as ISO 9660 can be booted. It’s very common to have live CDs or rescue/recovery CDs that use ISOLINUX for boot. The other boot loaders are not valid for this purpose or don’t exist.

54.  A. The /usr/lib/systemd hierarchy contains files related to systemd configuration. The user directory within the hierarchy is used for user unit files, and the system files are stored in /usr/lib/systemd/system.

55.  B. Due to the decidedly insecure decisions made with the design of Microsoft’s UEFI, a shim is often needed to enable Linux to boot on a system with UEFI. The shim.efi file can be used as an initial boot loader for this purpose.

56.  D. Scripts for starting and stopping services are located in /etc/init.d on a SysV init-based system. The other directories listed within this question are not valid.

57.  C. The systemd-delta command is used to determine overridden configuration files. Of the other commands, diff is valid but not for this purpose. The systemctl command is also valid, but again, not for the purpose described.

58.  B. The chkconfig --list command displays all services that will be executed on boot along with the setting for each service for each runlevel. Of the other commands, the init command is valid but does not have a --bootlist option. The other commands are invalid.

59.  B. The bcfg command within the UEFI shell is used to configure boot loaders on a UEFI-based system. The command can accept various parameters to configure how the boot loader and kernel will load on boot. Of the other commands shown, grub-install is valid but not within the UEFI shell.

60.  D. The pxelinux.0 file must exist within /tftpboot on the TFTP server in order for a system to use PXELINUX for booting. The other files are not valid or necessary for PXELINUX.

61.  D. The update-rc.d utility can be used to manage SysV init scripts on Debian or Ubuntu and other distributions. When using update-rc.d, you supply the script name and the utility will take care of creating symlinks to the appropriate runlevels.

62.  B. The e key, when pressed at the right time during boot, will send you into the GRUB shell, where you can change parameters related to boot, such as the kernel options and other related parameters.

63.  D. The isolate subcommand followed by the desired target is used to switch between runlevels with a systemd-based system. The other subcommands shown are not valid for systemctl.

64.  C. The runlevel defined as initdefault is the default runlevel for the system. The other options shown do not exist.

65.  B. The initramfs system is used instead of initrd to create the filesystem-based loading process for key drivers that are needed for boot.

66.  A. The systemctl command will be used for this purpose, and the set-default subcommand is necessary to affect the desired behavior. The target file is simply called multi-user.target.

67.  C. The shim.efi boot loader loads another boot loader, which is grubx64.efi by default. The other options are not valid filenames for the purpose described.

68.  D. The /etc/rc.d hierarchy contains symbolic links to files found within /etc/init.d. These symlinks are then used for executing the scripts at the appropriate runlevel. For example, on boot the system will execute the scripts found in the runlevel directory for each runlevel executed at boot time.

69.  A. The default.target is the default target unit that is activated by systemd on boot. The default target then starts other services based on the dependencies.

70.  B. LUNs that contain the characters fc are found through Fibre Channel. Therein lies the difference between options B and C, where option C contains the letters scsi, which would usually represent a local disk. The other options are not valid.

71.  B. NVMe-capable drives are named /dev/nvme*. No special drivers are needed other than those found in the native kernel on a modern system. The other options do not exist as paths by default.

72.  D. The /proc/mdstat file contains information on RAID arrays, including RAID personalities found on the system, the devices that comprise the array, and other pertinent information. The other files shown are not valid.

73.  B. The /sys/class/fc_host directory contains other directories based on the Fibre Channel connections available. Within those host directories will be found the WWN in a file called port_name. The other directory hierarchies are not valid.

74.  C. The /dev/mapper directory contains information about multipath devices such as logical volumes. The other directories are not valid.

75.  C. The lspci command will be used for this purpose. NVMe devices are listed with the name nVME or NVMe; therefore, adding -i to grep will make the search case insensitive. You’d use this in order to ensure that the devices are detected. The other commands are not valid, with the exception of the lspci command, but you cannot grep for scsi in this scenario.

76.  D. Tape devices are found within /dev/st*, making st0 the first device.

77.  C. The /etc/issue file is used to provide a message to users, such as a login banner, prior to local login. The other files shown are not valid for the purpose described.

78.  C. The contents of the file motd, an abbreviation for Message of the Day, are displayed when a user logs in successfully. Among the other options, the contents of /etc/issue are displayed prior to local login. The other filenames are not valid for this purpose.

79.  B. The /etc/issue.net file is used to provide a message for remote logins such as telnet. The other files listed are not valid for the purpose described.

80.  D. The poweroff target of systemd, accessed using the systemctl command, is used for halting the system and then attempting to remove power on compatible systems. The halt target stops the system but does not attempt to remove power, whereas reboot simply restarts the system. There is no stop target.

81.  A. The -r option is needed to specify reboot, and the format for counting time from now is prefaced with a plus sign (+), making option A correct. Of the other commands, specifying +15 without the -r option simply shuts down the computer in 15 minutes, and specifying the time as 00:15, as in option D, will shut down the computer at 12:15 a.m.

82.  A. The service command is used to work with services, such as starting and stopping them. On newer systems, the systemctl command has replaced the service command.

83.  A. The journalctl command with the -b option displays boot messages.

84.  A. The -h option halts the system, including shutting down acpid-related hardware.

85.  C. The number 9 corresponds to SIGKILL and can be passed to the kill command to issue that signal. The number 1 is SIGHUP. Others can be found within the manual for the kill command.

86.  C. The /etc/init.d directory contains the startup and shutdown scripts for services on a Debian system that is not running systemd.

87.  A. Among the options, examining the boot messages would be a first logical step and would prevent having to reboot the system. Rebooting may be a next step in order to examine the status of the peripheral within the BIOS.

88.  C. The -n option prevents the banner from displaying when using wall. The other options shown are not used with the wall command.

## Chapter 2: Topic 102: Linux Installation and Package Management

1.  C. SATA disks are addressed as /dev/sdX, just like a Small Computer System Interface (SCSI ) disk. /dev/hdX is a traditional ATA disk. The other options do not exist.

2.  C. The keyword single, given on the Linux kernel command line, will boot the system into single-user mode. The other options are not valid.

3.  A. The Shift key, if pressed when control has first been handed to GRUB, will cause the GRUB menu to be displayed.

4.  B. The root=/dev/sda2 option will cause the given kernel to load /dev/sda2 for its root partition. The rootpartition option is not valid, and the format of the root={hd0,3} is not valid in this context.

5.  C. You begin an editing session with an e when the boot option is highlighted. You can then make changes and, when done, press b to boot the system.

6.  D. The root partition is mounted after device initialization. System services, including multi-user mode, start after the root partition is mounted. The other two options, A and C, take place prior to the kernel-initializing device drivers. This process is essentially the same for virtual machines as it is for physical machines.

7.  D. The ESP is typically mounted at /boot/efi.

8.  D. The partition containing /var should be the largest for a mail server because mail spools are stored within this hierarchy. The /etc/ hierarchy is usually small, as is /usr/bin. The /mail directory does not exist by default.

9.  C. The rootnoverify option is used to specify a non-Linux kernel, one that GRUB should not attempt to load. The initrd option is used for specifying the initial RAM disk, making option A incorrect. The remaining options, B and D, are not valid options for GRUB.

10.  A. The update-grub command sends its output to STDOUT. Therefore, you must redirect using > and send that output to the correct file. The other options are not valid for this purpose. Options C and D are not valid commands, and option B contains invalid options as well as an invalid location for the destination file.

11.  B. MBR-based disks can be partitioned with up to four primary partitions, one of which can be further partitioned or extended into logical partitions.

12.  D. The ldconfig command updates the current shared library cache and list. ldconfig reads /etc/ld.so.conf and incorporates any changes found within it. The other commands listed as options for this question do not exist.

13.  B. The upgrade option for apt-get will upgrade the system to the latest version of software for packages already installed. The apt-update command does not exist, nor does the -U option to dpkg. The apt-cache command is used to work with the package cache.

14.  C. The yum install command will install a given package. The update option will update a package. The other options listed do not exist.

15.  C. Root’s home directory is /root on a Linux system. While the /home directory does exist, there is no root or su user within that hierarchy by default. The / directory is the root of the filesystem but not the root’s home directory.

16.  A. rpm2cpio sends its output to STDOUT by default, and therefore that output needs to be redirected to a file in most cases.

17.  B. The /usr hierarchy contains many of the programs that run on a Linux system. Other notable directories for programs are /bin and /sbin.

18.  B. GRUB begins its count at 0 and in this scenario there are two operating systems. Therefore, because Linux is first in the configuration file its number would be 0, which is then sent to the default= option.

19.  A. The /etc/default/grub file can be used for this purpose. You may also edit /boot/grub/grub.cfg, but this was not an option given for this question.

20.  B. The deplist option displays the dependencies for the given package. The list option displays information about a specific package while the other two options are not valid.

21.  A. The -ivh options will install a file using rpm, displaying both verbose output and hash marks for progress. The other options presented do not exist or do not accomplish the specified task.

22.  B. The export command is used to set environment variables in BASH. The other commands are not valid for this purpose.

23.  D. The yumdownloader utility will download an RPM package but not install it. The yumdownloader utility is part of the yum-utils package. The other options listed for this question do not exist.

24.  A. The apt-cache command is used to work with the package cache and the search option is used to search the cache for the supplied argument, in this case zsh. The apt-get command is used to work with packages themselves, and the apt search command does not exist.

25.  C. The GRUB_DEFAULT option, when in the /etc/default/grub file, is used to configure the operating system that will boot by default. The other options do not exist in this context.

26.  A. The ro option, which is the default for GRUB, will initially mount the root partition as read-only and then remount as read-write.

27.  D. Configuration files related to the repositories for yum are located in /etc/yum.repos.d. Of the other options, /etc/yum.conf is a file and not a directory, and the other directories do not exist.

28.  A. The -V or --verify option will check the files in a given package against versions (or checksums) in the package database. If no files have been altered, then no output is produced. Note that output may be produced for files that are changed during installation or for other reasons. Note also the use of an uppercase V for this option as opposed to the lowercase v for verbose.

29.  C. The -o option can be used to specify a destination file to which output will be sent instead of STDOUT. The other options listed in this question do not exist.

30.  A. The menu.lst and grub.conf files are used in GRUB Legacy, that is, prior to GRUB 2\. This therefore makes option B incorrect.

31.  D. The ldd command will list the libraries on which the command’s argument depends.

32.  B. Swap space is used when there is insufficient RAM memory on a system.

33.  B. The /etc/lib directory is not typically associated with library files and does not usually exist on a Linux system unless manually created. The other options either contain system libraries or can be used for that purpose.

34.  C. The apt-get update command will cause the package cache to be updated by retrieving the latest package list from the package sources. There is no cache-update or update option to apt-cache. The upgrade option is used to update the system’s packages and not the cache.

35.  C. The sources.list file located in /etc/apt contains the list of repositories for Debian packages. The other file locations do not exist by default.

36.  A. The /boot partition will typically be much less than 500MB but should not be undersized. The used space within /boot will increase as more kernels are added, such as during an upgrade process. Therefore, even though the recommended size is up to 500MB, experience proves that a larger partition is helpful, possibly 1GB to 2GB.

37.  B. The pvcreate command initializes a physical partition for future use as a logical volume with LVM.

38.  D. The grub-install command is used to install GRUB onto a disk and the second SATA disk would be /dev/sdb, making option D correct.

39.  A. The dpkg-reconfigure program will cause an already installed package to be reconfigured or changed. The -r option for dpkg removes a package, making option B incorrect. There is no reconf option for dpkg or reinstall option for apt-get.

40.  C. The lvcreate command is used to create logical volumes with LVM. The pvcreate command initializes physical volumes prior to creating logical volumes. The commands in the other two options for this question do not exist.

41.  A. Physical volumes are initialized first, followed by volume group creation, and then logical volume creation.

42.  D. aptitude provides the terminal-based interface rather than the standard command-line interface of the other tools listed in this question.

43.  D. The search option performs a search of various fields such as the package name and description.

44.  B. The rpm -qa kernel command will show the kernel version. You can also use uname -r for the same purpose.

45.  C. The GRUB_DEFAULT option in /etc/default/grub will set the operating system to boot by default.

46.  A. The exclude option can be used to exclude certain packages. The argument accepts wildcards, and therefore excluding all kernel* updates will create the desired behavior.

47.  B. The grub-mkconfig command should be run after making a change to the /etc/default/grub file so that a new configuration file can be created with the changed option(s).

48.  B. The -s option to dpkg searches for the given package and provides information about its current status on the system. The apt-cache command is not used for this purpose, and the -i option for dpkg installs a package. The apt-info command does not exist.

49.  C. The lvmdiskscan command looks for physical volumes that have been initialized for use with LVM.

50.  B. The --resolve option will download the dependencies of the package being downloaded. The other options shown within this question are not valid for the yumdownloader command.

51.  A. The -i option to dpkg will install a previously downloaded package. The other commands don’t exist, and the -U option for dpkg does not exist.

52.  D. GRUB Legacy begins counting at 0 and separates disk letter and partition with a comma, making 0,0 the first partition on the first disk. Options A and C are not the first disk on the system, and option B contains a nonexistent partition.

53.  A. ESP uses the legacy FAT filesystem type for its underlying format. There is a specification for how the ESP partition must be created on top of the FAT format for boot loaders and kernel images. Note that the partition is typically FAT32 but can be FAT16 if only Linux systems will reside on the drive.

54.  A. The --install option is used followed by the partition to which extlinux will be installed for boot.

55.  C. The format for the mount command is [partition] [target], making option C correct. The other options are not valid because the arguments are in the wrong order.

56.  B. The master boot record (MBR) is the first sector on a disk and contains information about the structure of the disk. If the MBR becomes corrupt, all data on the disk may be lost. The other options shown for this question are not valid.

57.  D. The --boot-directory option enables you to specify an alternative location for GRUB images rather than the default /boot. The other options shown for this question are not valid.

58.  D. The /etc/mtab file lists the currently mounted filesystems. The /etc/fstab file lists overall filesystems for the computer but does not distinguish between mounted or unmounted filesystems. The other options listed for this question do not exist.

59.  B. The swapon command enables swap space, making it available for use as virtual memory. The mkswap command formats the space. The other two commands are not valid.

60.  C. The pvdisplay command shows information about a given physical volume. You can use pvdisplay to view the device on which the PV is built along with the extent size of the PV. The other commands shown are not valid.

61.  B. The lvcreate command is used to create a logical volume from previously created physical devices and volume groups. Using lvcreate is the final of three steps in the process for using LVM prior to actually using the logical volume.

62.  A. The vgscan command looks for both physical volumes and volume groups related to an LVM configuration. The vgscan command is run at system startup but can also be run manually. The other commands are not valid.

63.  C. The pvscan command displays a list of physical volumes on a given server. The PVs displayed are those that have been initialized with pvcreate for use with LVM.

64.  A. The -a or --activate option sets whether or not the logical volume can be used. There is no -b or -c option, and the -d option is used for debugging.

65.  C. The script is using a relative path to look for srv/vhosts rather than /srv/vhosts with an absolute path back to the root directory of the system.

66.  B. Application containers share kernel and other resources with the underlying OS and use a container daemon to communicate between the host OS and the application container. Virtual machines have their own kernel and are self-contained machines running on top of a host OS or host kernel. Linux containers also provide a containerized virtual machine–like experience but are distinct from application containers.

67.  D. The /etc/ld.so.conf directory is used in addition to /lib and /usr/lib to configure library locations. The other paths and files shown do not exist.

68.  A. Among these options, compute resources, such as adding more CPUs, would be the most likely option. Adding RAM might also be warranted, but that was not one of the available options for this question. There is no indication in the question that the network is slow, and there is no indication that adding disk space or block storage (which are essentially the same thing in this context) will help.

69.  A. GRUB 2 uses grub.cfg whereas GRUB uses menu.lst and grub.conf, making option A the correct choice.

70.  B. The MAC address will be unique for each virtual machine deployed using the image. Guest drivers would usually not be unique to an individual virtual machine but might be unique on a per-template or per-image basis. System directories are not unique per virtual machine, and there is no such thing as pilot homing in this context.

71.  B. The cloud-init program is available on Ubuntu and other distributions and can be used to deploy images to popular cloud providers.

72.  C. The yum package manager configuration file is /etc/yum.conf. The other files listed do not exist.

73.  B. The -L option to dpkg lists the files included with a given package. The -f option to dpkg shows a field from a package entry, and the other options do not exist.

74.  A. The public key is deployed to the authorized_keys file on each image, and the private key is used from the host to connect to each virtual machine. There is no reason to deploy the private key to the virtual machine in order to make a connection to it.

75.  A. The /boot/efi partition needs to exist for the EFI partition and is typically sized 100MB to 250MB, though that size can vary.

76.  A. The install option, or simply in, will install a package on a system that uses zypper for package management. Among the other options listed, the ref option refreshes the repository. The other options are not valid with zypper.

77.  D. A system running Fedora 22 will use the dnf package manager by default. The yum package manager is used on CentOS and Red Hat, and apt and dpkg are used on Debian.

78.  A. The repoquery command with the -l option is used for this purpose. The dpkg -L command is appropriate for this purpose on Debian systems. The other commands do not exist.

79.  C. Home directories for normal users are in /home and the home directory for root is at /root, making option C correct.

80.  A. The /etc/machine-id file contains the unique identifier for a given machine.

81.  A. The -n option tells ldconfig to process only the directories given on the command line. The -i option ignores the auxiliary cache file. The -v option is verbose, and -r changes the root directory from which to begin processing.

82.  C. The stats option shows total package names along with other information about the package cache. The other options are not valid for use with apt-cache.

83.  D. The --efi-directory option is used to specify the location of the EFI partition, typically /boot/efi.

84.  A. The /etc/fstab file contains a list of partitions for the system. The /etc/mtab file contains currently mounted partitions. The other files do not exist.

85.  B. The options qlp list the files in an rpm package. The other options are not valid for the purpose described in the question.

86.  B. Among the commands and options shown, the info option to yum is used for this purpose. The dpkg and apt package managers are used on Debian systems and thus would not be appropriate for a CentOS system.

87.  A. The presence of the string vmx in the flags section indicates that an Intel processor is capable of virtualization. This extension is called svm on an AMD architecture.

88.  A. The lvm.conf file is a primary configuration file for LVM. Within lvm.conf, typically found in /etc/ or /etc/lvm/, you can set things like filters for devices to include or exclude from the vgscan process. The other files shown are not valid.

89.  C. The --show option displays information about the swap spaces on the computer, including how much swap is currently being used. The -a option activates all swap spaces. There is no --list option, and -h displays help.

## Chapter 3: Topic 103: GNU and UNIX Commands

1.  D. The set command can be used for a variety of purposes to change how the shell environment works. One such option is –C, which prevents output redirection such as that done with > from overwriting a file if the file already exists.

2.  B. The env command will print the current environment variables from Bash. The printenv command will perform the same operation. The other commands listed in this question do not exist.

3.  C. The man command displays documentation for the command given as the argument. The other options listed for this question do not exist.

4.  D. The uname command is used to print system information, and the -a option prints all information available to uname.

5.  A. The g option, also known as global or greedy, will apply the matched operation to the entire line rather than just the first instance of the match. The other options apply as they would for a Perl-Compatible Regular Expression. Note also the tr command that provides some of the same functionality as sed.

6.  C. The -l option provides the number of lines given as input. For example, wc -l /etc/passwd would print the number of lines in the /etc/passwd file. The other options given in this question are not valid for the wc command.

7.  C. Both head and tail print 10 lines of output by default.

8.  B. The -rf options to rm will recursively remove the contents of a directory, including other directories. The -f option alone will not work in this case because of the additional directories. The other options given for rmdir do not exist.

9.  D. The -type option causes find to limit its search to directories only, whereas the -name option limits the names of returned elements. Note the use of the wildcard due to the phrasing of the question. Also note the use of ./ to denote beginning the search in the current directory.

10.  A. The cat command will display the contents of file /etc/passwd and then pipe that output to the awk command. The awk command then parses its input, splitting along the specified separator for /etc/passwd, which is a colon (:). The output is then printed and piped to the sort command. The sort command in option B will not work because the cut command requires an argument. Likewise, the echo command in option C will only echo /etc/passwd to STDOUT.

11.  C. The -l option for ls produces long or listed output and -t sorts by time stamp. The -r option reverses the order, and -a is needed to include hidden (dot) files, making option C correct.

12.  A. The time stamp of the file will change when touch is run on a file that already exists.

13.  D. The -i option will cause both cp and mv to be interactive, that is, prompt before overwriting. The -f option will force the command to run, whereas -r is recursive.

14.  C. The tee command will send output both to STDOUT and to the specified file, making option C correct. Option A will redirect output to the correct file but not to STDOUT simultaneously. The other options will not work for this question.

15.  A. The -p option will cause mkdir to create additional levels of directories without error. Running mkdir without options will not work in this case. The -r and -f options to mkdir do not exist.

16.  B. The -R option will copy directories recursively. Note that if the -i option is not enabled, the recursive copy will overwrite files in the destination. The -v option adds verbosity but does not cause any recursion, and the -Z option does not exist.

17.  C. The file command can be used to determine which type of file is being used. This can be particularly helpful for files without extensions where you are unsure if you should view the contents of the file. Option A, grep, is used to look within files but would not be helpful in this case. The telnet and export commands are not used for this purpose.

18.  C. The dd command is used to create disk images, among other things. In this case, the input file is /dev/sda1 and the output file is output.img. It’s also common to add the blocksize option by using the bs argument, such as bs=1M.

19.  B. The cut command uses Tab as its default delimiter. This can be changed with the -d option.

20.  A. The -z option will unzip the file, -x will extract from the tar archive, and -f is used to indicate the file on which to perform the aforementioned operations. It’s typical to add -v for verbose output as well.

21.  D. The fg command will bring a command to the foreground if it has been backgrounded with either & or with the bg command.

22.  B. While the ps auwx command combined with grep will provide information on the running Apache instances, it will provide much more information than is required or useful for this problem. The pgrep command provides only the process IDs and therefore meets the criteria presented in the question.

23.  D. The top command is used to continuously monitor things like CPU and memory usage, and the -p option monitors a single process. By using the runquotes with the pidof command, the process ID is provided as input to the -p option.

24.  D. The free command displays overall memory usage for both RAM and swap and can be used to determine when additional memory might be needed.

25.  A. You need to write the changes to the file; therefore you’ll need :w. The addition of q will also quit. Note that you could use ZZ to write and quit as well. The dd command deletes a line, and x deletes a single character.

26.  D. The -n option changes the number of lines of output for both head and tail to the number specified. The other options listed in this question are not valid for head, and the -f option follows a file with tail as the file grows.

27.  A. The uptime command shows basic information such as that described along with the number of users logged into the system and the current time. The bash command is a shell environment, and the ls command will not display the required information.

28.  D. The screen command starts a new terminal that can be disconnected and reconnected as needed. Processes running from within the screen session do not know that they are running in a screen session and therefore meet the criteria needed to satisfy this question. The fg and bg commands will not meet the criteria, and the kill command will stop a process.

29.  C. The -9 option invokes SIGKILL, which will force the process to end. The 15 signal is the default, and the -f and -stop options do not exist.

30.  C. Within Bash, the number 1 represents STDOUT and 2 represents STDERR. Redirecting both means combining them in the manner shown in option C.

31.  B. The nice command, when run without arguments, will output the priority for the currently logged-in user, which is normally 0\. The renice command can be used to change the priority of running processes. The other two commands shown as options for this question do not exist.

32.  D. Within a regular expression, * represents 0 or more characters. In this case, it doesn’t matter whether a person is using /bin/bash or /usr/bin/zsh. Likewise, a . matches a single character, but in the case of bash and zsh, we need to look at the first and then optionally a second character. The ? character makes the second . optional. Finally, the $ anchors the pattern at the end of the string and is also the key for this regular expression.

33.  A. The different levels of the manual are accessed by preceding the argument with the desired level. The other options, such as --list, do not exist in this context.

34.  C. The o command opens a new line below the current cursor location. The a command begins an insert mode session at the character after the cursor, not the line. The i command begins an insert mode session at the current cursor location.

35.  A. Sending -HUP as part of the kill command will restart a process. Of the other options, a -9 will kill the process completely. The other two options do not exist as valid means to kill a process.

36.  B. The history command will display your command history, including commands from the current session. You can specify how many lines of history to display, as shown in the answer for this question. Note that .bash_history will not show the current session’s history.

37.  C. The jobs built-in command shows the list of jobs running in the background. Its output includes a job number and the status of the job.

38.  B. The find command, beginning with the path and then the -name argument, will locate all of the files called .bash_history. The output from the find command should be piped to xargs, which can then build further commands from standard input. Note that this question and solution assumes that all users use the Bash shell and are keeping history.

39.  C. The tail command provides the end portion of the file given as an argument. Adding the -f option will cause the output to update as new lines are added to the file being tailed.

40.  D. The nl command will prepend line numbers onto the file given as its argument. The output is then sent to STDOUT. Of the other options, wc -l will print the number of lines in the file but not prepend those numbers onto each line, as was asked for in this question.

41.  A. The xz command can compress and decompress files in a variety of formats, one of which is lzma.

42.  A. The find command will be used for this purpose. Adding -type f will limit the search to only files and the -mtime option will limit to modification time in day format.

43.  C. The mv command is used to move files, and *.txt will look for all files with a .txt extension. Note the fully qualified destination with a / preceding the name tmp.

44.  D. The pwd command prints the current working directory. The cd command changes directory.

45.  A. The file needs to first be sorted to group common ZIP codes together. After that, piping the output to uniq will display the unique ZIP codes, and the -c option provides a count.

46.  A. Preceding the command with a ! will search history and execute the specified command. For example, !vi will start your last Vi session.

47.  C. The killall command is used to terminate processes using their name.

48.  C. The ? key will search backward in a file within Vi. The / is used for searching forward. The h key moves the cursor to the left one character, and the x key will delete a character.

49.  D. The export command makes an environment variable available to subsequent child processes. The other commands shown are not valid.

50.  B. The echo command sends output and $0 is the parameter that contains the current script name. Of the other options, $PS1 is the shell prompt and the other two options do not exist by default.

51.  B. The gunzip command is typically used for decompressing files with a .gz extension. The other options are not valid commands.

52.  C. The -i option causes rm to use interactive mode, where the command will prompt for confirmation prior to taking action. See the (1) rm man page for additional information on the other options.

53.  A. The find command can be used for this purpose. When used with the size option, various size-related options can be used. The option +1G searches for files greater than or equal to 1GB.

54.  B. The -v or verbose option lists files as cpio is working with them. Of the other options, -s is swap bytes and –l is used to link files. The -k option is included for compatibility purposes.

55.  B. The bzcat command sends output to STDOUT from a bzip2 archive.

56.  C. The jobs command is actually a shell built-in command, meaning that more information is available by using the man page for bash itself. The other options either are not valid or will not show information about the jobs command/built-in.

57.  B. The nohup command can preface another command when starting so that the process or command will not accept a SIGHUP.

58.  D. The watch command runs a command repeatedly and displays the output and errors from the command. The pgrep command does not fulfill the needs of this scenario. The mon and procmon commands are not real.

59.  B. The tmux command creates two (or more) sessions within the same physical terminal window and thus enables this scenario. The screen command can be used to create an additional session, but the screen command does not meet the criteria specified in this scenario, because the scrollback buffer does not capture enough lines by default. The other commands shown are not valid.

60.  A. The pkill command can be used for the scenario described. The other options are not valid commands.

61.  A. The -f option matches against the full path. The -d option is used to set the delimiter, the -o option matches the oldest process, and the -i option sets the search to be case insensitive.

62.  B. The which command is used to determine the command that will be run based on the current environment settings such as the path. The find and ls commands will not work for this purpose.

63.  B. The unset shell built-in is used for the purpose described. Both the reset and clear commands do not accomplish the task described, and there is no undo command.

64.  A. The type shell built-in displays information about a given executable. For example, the command type alias shows that alias is a shell built-in as well.

65.  C. Double quotes help to ensure that variables are interpolated within a shell script. Runquotes are not used for this purpose, and the other options are not valid types of quotes.

66.  C. The less pager fits the scenario described. The more pager does not have as much flexibility as less. The other options shown are not valid.

67.  C. The od command converts a file to octal format. The other options shown all have invalid commands.

68.  B. The -b option for sha256sum and sha512sum reads the file in binary mode as opposed to text mode, which is the default.

69.  B. The h, j, k, and l keys enable movement of the cursor in command mode Vi.

70.  C. The decompress and stdout options to xz are functionally equivalent to the xzcat program. There is also a related program called zcat for outputting files compressed with gzip to STDOUT.

71.  A. The EDITOR environment variable controls the editor that is used. Typical choices include nano, Emacs, Vi or enhanced Vi, known as Vim.

72.  D. The seventh manual section for regex is found by specifying the level after the command and prior to the manual page to examine.

73.  B. The renice command changes the priority of a running process. The nice command is not capable of altering running processes, and the other commands shown are not valid.

74.  B. The fgrep command is equivalent to running the grep command with an -F option. The -f option specifies a file, and the -E option utilizes an extended regular expression and is equivalent to the egrep command. The -a option is important in its own right and causes grep to process a binary file as if it were a text file.

75.  A. All of the options shown use regular expressions. In the correct answer, the strings Steve and steve will match due to the use of a character class. Option B would match only Steve but, due to the quantifier *, would also match strings like Siwejfiwjfheteve. Option C uses anchoring and thus would only match Steve or steve at the beginning of a line. Option D also uses an anchor to indicate end of line and thus does not make sense in this context.

76.  C. The top command shows running processes, typically sorted by CPU usage and updates every few seconds. The ps command shows processes but does not auto-update. The nice command sets priority, and there is no procs command.

77.  A. Files compressed with the gzip utility can typically be read by other operating systems, though it may require additional software for certain operating systems. Compression utilities like bzip2 and xz almost certainly require additional software. The tar command in option D is not a compression utility.

78.  A. The question mark can be used as a wildcard for such a scenario. An asterisk would also work for file globbing.

79.  B. The split command can break up a file into multiple pieces. The cut command would split an individual line but does not meet the criteria in this scenario. There is no dice or rem command.

80.  C. The scheduling priority of the process is shown in the PR column. The process ID is displayed in the PID column. The top command shows CPU utilization in the %CPU column and does not display information about the processor cores.

81.  A. The d key will be used for this and the number 7 used in order to cut or remove eight lines. Other keys to work with text for cut, copy, and paste in Vi include p, y, dd, and yy. The other options shown for this question are not valid.

82.  A. The unxz command decompress a file that has been compressed with xz.

83.  D. The md5sum command creates a 128-bit MD5 message digest. The sha256sum command produces 256-bit values, whereas sha512sum produces 512-bit values.

84.  A. The paste command fits the scenario described and separates the lines from each file by a tab. The other commands are not valid.

85.  A. Using a fully qualified path meets the scenario in the most typical manner. You could add the command path to the PATH environment variable, but that is unnecessary given the scenario. Restarting the shell or computer would not have any effect.

86.  B. The SIGTERM signal is used by default by the pkill command. This can be changed using the --signal option.

87.  D. Running jobs are listed with the -r option. The -s option displays only stopped jobs, whereas -l shows process IDs. There is no -a option to the jobs built-in command.

88.  C. The -c option outputs to STDOUT. See the bzip2(1) man page for additional details.

## Chapter 4: Topic 104: Devices, Linux Filesystems, Filesystem Hierarchy Standard

1.  A. The listing shows a symbolic linked file located in the current directory, linked to .configs/fetchmail/.fetchmailrc. The file is owned by the root user and root group and was created on July 8, 2014.

2.  A. The mount command is used to mount drives in Linux. The source and destination mount points are expected as arguments. Drive partitions begin at the number 1, making the first partition number 1.

3.  C. The noexec option will prevent programs from being executed that reside on the partition. The noexec option is used frequently for mounting the /tmp partition.

4.  B. 0x82 is Linux swap, and 0x83 is Linux. NTFS is 0x07, and FAT is 0.0c.

5.  B. The partition type 0x83 should be created for a normal Linux partition. Type 82 is used for swap; 84 is an OS/2 partition. There is no L type.

6.  A. The which command returns the full path to the given command and is useful for determining both whether a given command is available and the location from which the command will run.

7.  A. The chgrp command can be used to change group ownership of a file. The order is chgrp <groupname> <target>.

8.  C. The file is almost certainly a hard link to the original script. Although ls won’t show this information, the stat command will show that it is a link and also show the inode to which the file is linked.

9.  A. The -i option to df produces information on inodes across all filesystems. The ls -i option will produce inode listings, but only for the current directory. The -i option is invalid for du, and dm does not exist as a command.

10.  C. The -y option will attempt to repair automatically, essentially answering y or yes instead of prompting. Of the other options, only -V is valid and will produce verbose output.

11.  B. The addition of journaling in ext3 increased filesystem reliability and performance.

12.  C. The -S option displays output in a format such as u=rwx,g=rx,o=rx. The other options listed do not perform the desired operation.

13.  B. The -s option to ln creates a symbolic link, or symlink.

14.  C. The whereis command displays pertinent information about the command given as its argument. For example, entering whereis apache2 on a Debian system will show the binary location, configuration file location, and other relevant details.

15.  A. The PRUNEPATHS option accepts a space-separated list of paths to remove from the results. The other options listed do not exist.

16.  D. The /srv hierarchy is used for data for server programs. The /etc hierarchy is configuration information; /var is also data files but variable, such as mail files. The /tmp directory is for temporary files.

17.  C. The chmod command is used for this purpose, and the u+s option sets the sticky bit for the user on the specified target.

18.  B. The -a option mounts all filesystems in /etc/fstab that are currently available. This option is typically used if the mount points are not mounted at boot time or another mount point is added to the system after it has been booted.

19.  B. The mkswap command formats a swap partition. The fdisk command is used to create the partition itself but not format it. The other two options do not exist.

20.  A. The tune2fs command displays a lot of information about filesystems, and when used with the -l option, the output includes the number of times that the filesystem has been mounted.

21.  A. The -g option displays progress of the dump. The other options listed do not exist.

22.  A. The du command will report on disk usage in a recursive manner, unlike the other commands shown here.

23.  C. The /etc/fstab file is used to store information about the filesystems to mount within the system.

24.  D. The /media mount point is used for removable media. See [https://wiki .linuxfoundation.org/lsb/fhs-30](https://wiki.linuxfoundation.org/lsb/fhs-30) for more information on the FHS.

25.  A. The /etc/mtab file contains currently mounted filesystems. Note that /etc/fstab contains filesystem information but doesn’t report which filesystems are currently mounted.

26.  B. The -r option causes umount to attempt to remount in read-only mode. The -v option is verbose mode, and the -f option forces the operation. The -o option does not exist.

27.  A. The 022 umask will translate into 644 permissions on a new nonexecutable file.

28.  C. The updatedb command will update the database used by the locate command.

29.  A. The type built-in returns the location that the shell will use in order to run the given command. The find command cannot be used for this purpose, and the other commands do not exist.

30.  B. The -R option will perform the change ownership in a recursive manner.

31.  D. The proper order is the device (UUID or partition) or filesystem to mount, followed by the mount point or directory to mount that device, followed by its type and options, and then the dump and pass settings.

32.  A. The blkid command will show partition UUIDs. You can also get this information with the lsblk -no UUID <partition> command. The other commands shown in this question do not accomplish the required task.

33.  A. Priority order for systemd configuration files are those within the /etc/ hierarchy, followed by files in the /run/ hierarchy, followed by files in the /lib/ hierarchy.

34.  A. The -y option causes fsck to assume yes instead of prompting when repairing a filesystem. The -v option is verbosity. There is no -m or -x option for fsck.

35.  C. The -t option sets the filesystem type as ext2, ext3, or ext4\. The mke2fs command is typically symlinked from /sbin/mkfs.ext2, /sbin/mkfs.ext3, and /sbin/mkfs.ext4. The -F option forces mke2fs to create a filesystem, and the -a and -e options do not exist.

36.  B. The file /etc/auto.master contains the configuration for autofs. The other files listed as options are not valid for this scenario.

37.  C. The mkisofs command creates an ISO filesystem, which can then be written to a CD or DVD. The other commands listed are not valid.

38.  B. The -c option sets the maximum mount count. The -C option sets the current number of mounts. The -b and -a options do not exist.

39.  D. The -f option, also known as fake, is helpful for situations where you need to debug the mount process or when you need to add an entry to /etc/mtab for a previously mounted filesystem. The -l option shows labels, and -v is verbose. There is no -q option.

40.  C. The letters ro indicate that the filesystem has been mounted read-only, meaning that it is not possible to perform a write to the filesystem. The other possible option is rw, indicating that the filesystem has been mounted read-write.

41.  C. Bad blocks are shown with the -b option. The -f option forces dumpe2fs to perform the requested operation, and the other command options do not exist.

42.  D. Btrfs is based on the copy-on-write principle and is generally considered more advanced than ext4 and its predecessors. FAT is a legacy filesystem primarily used for DOS and its follow-ons like Windows.

43.  B. The xfs_info command, which is functionally equivalent to xfs_grow -n, displays information about an XFS-formatted filesystem.

44.  A. The blkid command shows information about partitions including their type, their UUID, and other basic information. The other commands shown do not exist.

45.  C. The -t option, which can accept a comma-separated list of types, specifies that only filesystems of the listed type are to be unmounted. This is useful in conjunction with the -a option, which unmounts all filesystems except /proc. The -v option is verbose, and -f forces the operation to continue.

46.  D. The sync command writes unwritten data to the disk immediately and is useful to run just prior to attempting an unmount operation.

47.  C. The -f option specifies that xfs_check should check the contents of the named file for consistency. The -v option sets verbosity, and there is no -d or -a option.

48.  B. The -w option causes debugfs to open the filesystem in read-write mode. There is also a -c option to open in catastrophic mode for filesystems with significant damage. The -rw, -r, and -n options are not valid.

49.  D. The smartd daemon monitors SMART-compatible disks for notable events and can be configured to send alerts when events occur. The other commands listed are not valid for this scenario.

50.  A. The -f option forces fsck to run on an otherwise clean filesystem for ext3 filesystems. This can be helpful for times when you suspect there is an error on the filesystem and need to verify the integrity of the filesystem as part of the troubleshooting process. This can also be helpful to prepare the filesystem for conversion, such as might be the case with a tool like btrfs-convert.

51.  A. The block size for import or restore must match the block size used on export or dump. Block size is specified with the -b option, making option A correct. The other options are not valid for xfsrestore.

52.  B. A filesystem with the word defaults for its mount options will be mounted read-write (rw), suid, with the ability to have executables (exec). The filesystem will be auto-mounted (auto), but users will not be able to mount it (nouser). Character and block special devices will be interpreted (dev), and operations on the disk will be performed in an asynchronous manner (async).

53.  B. The btrfs subvolume create command creates a btrfs subvolume. The other commands are not valid.

54.  C. The -z option sets the maximum size for files to be included in the dump. The -b option sets the block size but is not related to what is being asked for in this scenario. The –s option sets the path for inclusion in the dump, and -p sets the interval for progress indicators.

55.  C. The -e option sets the behavior, such as continue, remount read-only, or panic, when an error occurs at the filesystem level. The -f option forces whatever operation you’re requesting to continue even if there are errors. The -d and -k options are not valid.

56.  D. The -n option causes mount to not write to /etc/mtab and is particularly useful for the scenario described. The -a option mounts all filesystems in /etc/fstab. There is no -b or -a option.

57.  A. The swapoff command deactivates swap space, thereby making it unavailable as virtual memory on the system. The other commands shown as options are not valid.

58.  A. The Where= directive specifies the location for the final mounted filesystem.

59.  A. The mkfs.fat or mkfs.vfat commands are valid for creation of FAT filesystems. There is no -f option to mkfs, and there is no mkfat command.

60.  D. The tune2fs command is used for working with ext2, ext3, and ext4 filesystems. The -j option adds a journal. The other commands are not valid.

61.  A. The snapshot subcommand of btrfs subvolume creates a snapshot. The other commands shown are not valid.

62.  A. The -L option forces the log to be cleared or zeroed out, which may cause a loss of data. The -v option sets verbose output; -V prints the version. The -d option performs a dangerous repair, which can be used on a read-only filesystem.

63.  C. The -o option enables the setting of one or more options for the mount command, and ro is read-only. Note that the -r option will also mount as read-only. The other options shown are not valid.

64.  B. The -E option signals that an extended option follows, such as stripe_width. The -f option forces an operation but should not be necessary for this solution, and the -e option sets the behavior on error. There is no -extend option.

65.  A. The gdisk utility is the equivalent of fdisk for working with GPT partitions. Later versions of fdisk can also be used to manage GPT partitions.

66.  A. The maximum size for a partition on an MBR disk is 2 terabytes. GPT has largely replaced MBR on newer Linux systems.

67.  C. The -m option with 0 will format the partition with no reserved blocks for superuser or system use. The -r option sets the filesystem revision.

68.  B. The default time for filesystem reorganization is two hours, or 7200 seconds.

69.  C. The file permissions are 640, meaning that the group owner can read the file. Therefore, changing group ownership should have the fewest side effects. Granting root access is not preferred, especially noting that the problem statement indicated that granting sudo wasn’t preferred. While using chown on the file to change the owner would also work, it’s likely to have additional side effects that could prevent the owner of the file from reading and writing, and there isn’t enough information in the problem for that. Finally, running chmod 777 is almost never the correct solution to any problem on Linux.

70.  B. The -a option shows all devices, even those that are empty. The -r option is for raw devices, and the other options do not exist.

71.  D. USB devices and others removable media can typically be found within the /media/ mount point.

72.  C. The mkfs-related commands are typically used for formatting filesystems on Linux. In this case, mkfs.exfat is the correct option for formatting exFAT filesystems.

73.  C. The xfs_db command is used for debugging XFS-formatted filesystems.

74.  C. The -b option is used to specify an alternate superblock and helps in the scenario described, where the superblock has been damaged. The -B option specifies the block size. There is no –s or -o option for e2fsck.

75.  A. The -h option is the flag for human-readable formatting and shows numerical output in larger size increments rather than bytes. The other options are not valid for df.

76.  B. The /etc/profile file is one of a few locations in which default options can be set for users of Bash. The other file locations shown do not exist.

77.  A. A symbolic link will not work. The users would be editing the same file and, without saving as a different filename, would not be able to keep their own edits.

78.  B. The find command will be used for this purpose, and the -uid option will need to be used because the user has already been deleted. If the user had not been deleted, then the -user option would still work.

79.  A. The updatedb command is used to update the locate database. The other commands are not valid.

80.  B. The -f option shows the UUIDs of the filesystems mounted on the system. The -a option shows all devices, the -o option enables specification of output columns, and the -u option does not exist.

81.  C. The -c option checks for bad blocks before formatting. The other options are not valid with mkswap.

82.  D. The sticky bit has been set on the file as denoted by an uppercase S.

83.  C. Using octal form, 4 is user, 2 is group, and 1 is sticky bit. Therefore, 2755 would have setgid for the file.

84.  C. The -name option is used for this purpose, and / indicates the root of the system. A * wildcard is used to indicate all filenames ending in .sql, as described in the scenario.

85.  B. The UUID=<UUID> syntax is correct for the /etc/fstab file.

86.  C. The --inodes option shows inode usage with du. The -h option is human-readable, and -d sets the maximum depth. There is no -i option for du.

87.  A. The -size option is used with find for this purpose, and the +1G argument will look for files greater than 1 gigabyte. Note that if the + is omitted, only files of the exact size are found.

88.  B. A symbolic link is the preferred method because it does not require additional maintenance that a script would or that copying would in order to keep the libraries current. Moving the libraries may have unintended consequences if another program is dependent on the libraries in that location.

## Chapter 5: Topic 105: Shells and Shell Scripting

1.  B. The PS1 variable usually has its default set in /etc/profile and is used as the shell prompt. Users can customize the prompt to include hostname, working directory, and other elements.

2.  C. The source command is used to execute commands from a file. A typical use case is to create functions or variables that are then available for use within the current session. The other commands listed do not exist.

3.  B. While it’s true that every user has a .bash_logout in their home directory, that file can still be edited by the user. Therefore, to ensure that the required command is executed at logout, the /etc/bash.bash_logout file must be used.

4.  B. The env -u command will unset an environment variable for the current session. The unset command can also be used for this purpose.

5.  C. The -v option, which is the default, tells unset that the name given is a shell variable rather than a function. The other options shown do not exist.

6.  A. The alias command is used for this purpose and its format is name=value, making option A correct. The ln command cannot be used for this purpose because it will not accept command-line arguments for the target in such a format, as shown in the options.

7.  B. User-based configuration files are located in the order .bash_profile, .bash_login, and .profile. Only the first file found is executed and the others are ignored.

8.  C. The $1 variable is automatically available within Bash scripts and represents the first command-line argument. The other variables listed in this question do not exist by default.

9.  D. The fi construct is used to indicate the end of an if conditional within a Bash script. In many languages, if conditionals are scoped by braces such as { }, but in shell scripting, fi is used to denote the end of the condition.

10.  B. The seq command is used to print a sequence of numbers in a variety of formats. The answer for this question provides a starting point (0), and increment (1), and the final number (5), resulting in six numbers being displayed as output.

11.  B. The echo command is used to display its argument, regardless of whether the command is used inside a shell script or from the command line itself. The env command is used to display environment variables and therefore does not meet the need specified in the question. The var_dump command is used within PHP, and ls is used to display contents of directories.

12.  A. The suid bit enables the program to run as the user who owns the file regardless of who executes the program. Using SUID is typically not recommended for security reasons.

13.  D. The exec command executes the command given as its argument and will then exit the shell. The source command does not exit the shell.

14.  C. The double-ampersand sequence executes commands only if the previous command exited cleanly.

15.  C. The read command awaits user input and places that input into the specified variable. The exec command is used to execute commands, and the other options are not valid for the purpose described.

16.  A. Parentheses are used to denote a function, such as myFunction(). The parentheses are optional but are then followed by curly braces containing the commands to be executed when the function is called.

17.  C. The || sequence indicates an alternate command to run if the initial preceding command does not exit cleanly. The && sequence executes only when the preceding command exits cleanly, so it’s just the opposite of what the question was asking.

18.  C. The elif keyword is used to create an alternative execution path within a shell script. The other constructs, such as else if and elsif, are used in other languages.

19.  C. The unalias command is used to remove a previously defined alias. The rm command will remove regular files but not aliases. The other commands do not exist.

20.  D. At a minimum, you need to be able to read the file being sourced; therefore, chmod 400 will correctly set the permissions. Any chmod that gives additional permissions is not necessary.

21.  C. The for loop construct in this case will require the variable name LIST to be preceded with a dollar sign ($),making option C correct. The other options will not work for the purpose described.

22.  C. The -lt operator is used to test for “less than” conditions within a script. The other operators are not valid for use in a shell script.

23.  B. The -e test checks to ensure that a file exists and is typically used in the context of a conditional within a shell script. The other options may work within shell scripts but are not tests for file existence.

24.  C. The /etc/skel directory contains files to be copied to the user’s home directory. The other directories listed for this question do not exist by default.

25.  C. The --norc option causes bash to execute without reading the /etc/bash.bashrc file or the local ~/.bashrc file. The other options listed do not exist as options for bash.

26.  A. Array creation in a shell script involves parentheses when used in this manner. You can also use square brackets to define individual elements, as in ARRAY[0] = "val1".

27.  C. The -p option to declare displays fully qualified shell statements such that the statements could then be used as input for another command, either through piping or redirection to a script.

28.  A. The .bash_profile file, if it exists in your home directory, will be executed on login. Note that placing the function in /etc/profile would technically work but then the function would be available to all users, which is not what the question asked for.

29.  B. The readonly command displays the list of read-only variables that have been declared in the current session. The other commands listed for this question do not exist.

30.  C. Square brackets are used to denote the beginning and end of the test portion of a while loop in a shell script. Other languages generally use parentheses for this purpose.

31.  B. The test built-in will return true and can be used to test for the value existence of a variable not being null. Note that the behavior of the test built-in differs depending on the number of arguments.

32.  C. The HOME environment variable, set automatically to the user’s home directory, is consulted when the command cd ~ is entered. The other paths beginning with HOME do not exist by default, and the MAILPATH environment variable shown contains a list of locations where mail is checked when using the shell interactively.

33.  B. The TMOUT variable can be set in a given user’s shell and that user will be logged out after the value given (in seconds) of inactivity. The other environment variables listed here do not exist.

34.  B. Just as with an if statement where the statement is ended with fi, so too is a case statement ended with the word *case* spelled backward. The curly brace shown as option D is used to close case statements in many languages, but not for shell scripts.

35.  A. The provided answer performs command substitution and places the value from the resulting command into a variable. Note the use of +%s formatting on the date, which then formats the output as seconds since the epoch, as specified in the question. Option C will provide the date within the DATE variable but will not format it as specified.

36.  B. Wrapping a variable in curly braces, such as ${FILEPATH}, will ensure that the variable is interpolated or expanded correctly even when used in a place where it might not normally be expanded, such as within a quoted string.

37.  B. In shell scripts, the commands to execute begin at the do keyword and end at the done keyword. Other languages generally use either curly braces or tabs.

38.  D. The -r test determines whether a given file exists and can be read by the current user. The -e test only checks to see if the file exists.

39.  A. The -r option to declare will create or mark the variable as read-only. The -p option prints output in a format that can be reused. The -x option declares the variable for export.

40.  D. The *) sequence is used to denote a default set of statements that will be executed if no other case matches within the set.

41.  A. Backquotes can be used for command substitution within a Bash script. The other options shown are not valid for command substitution.

42.  B. The character sequence done denotes the end of a while loop in Bash.

43.  B. Greater than or equal to is tested with >=. Of the other operators shown, != tests for inequality.

44.  C. The execute bit is not set on the script, resulting in the permission denied error, making option C correct. The file extension does not matter, so option A is incorrect. Likewise, option B is not correct because the script isn’t even executing. Lowercase or uppercase letters do not matter, making option D incorrect.

45.  D. The -f option exports names as functions to child processes. The other options shown do not exist with the export command.

46.  D. The unset command removes a variable from being set. The other options shown do not exist.

47.  A. The /etc/bash.bashrc file is a systemwide configuration file for the Bash environment. Another systemwide file used for similar purposes is /etc/profile.

48.  D. The +x option enables debugging output and is frequently used when debugging shell scripts. The -x option is used to disable debugging. The -d and +d options do not exist.

49.  D. The .bashrc file in a given user’s home directory is executed for interactive logins. The other files shown do not exist.

50.  A. The function keyword declares a block of code to be a function in Bash. It’s worth noting that the function keyword can be omitted in most cases. The other options are not valid.

51.  B. The syntax shown in option B is the correct syntax to add a path to the current environment. Option A does not include the existing path (and will, in fact, overwrite the existing path). Option C contains spaces, and option D uses a semicolon as a delimiter.

52.  D. The $0 variable is automatically defined and contains the name of the script itself. The other options shown do not exist by default.

53.  A. The -s argument enables setting of a delimiter. When used, the numbers will be printed in a sequence rather than one per line. The -m and -d options do not exist.

54.  D. The -O option is used to determine if the user currently running the test is the owner of the file being tested. The -k option checks to see if the sticky bit has been set. There is no -m file test.

55.  A. A successful return from a command executed within a Bash script is 0. A 1 or higher typically indicates an error condition. There is no C condition.

56.  A. The file is not copied to directories for existing users, making option A correct. There is nothing in the question to indicate that the file is too big or that it already exists. File extensions don’t matter in Linux, so option D cannot be correct.

57.  C. The find command begins the search in the current directory, which is problematic in a scripted scenario like the one presented. The find command can find directories, and those directories can begin with a dot character.

58.  B. The -i option ignores the environment. The other options are not valid for use with env.

59.  A. The -x option enables debugging when passed on the interpreter line of a Bash script. The other options are not valid for this purpose.

60.  C. Doing math in Bash requires a special syntax. The bc command can also be used for such operations and is frequently used for math within Bash scripts.

61.  A. The read command will be used, and option A shows the correct syntax. Option C is incorrect because it does not prompt the user. There is no prompt command, making options B and D incorrect.

62.  D. The -n option removes a variable from being exported. The other options do not exist.

63.  A. The exit code from the previous command is captured automatically in the $? variable, thus ruling out any option that did not have this value. A test for the value is done with -eq in a Bash script, thus making option A correct.

64.  D. The source command is frequently used for the purpose described. The function command can be used to create functions but would not be used for the purpose described. The include and require commands are not valid.

65.  B. Adding the execute bit for the user can be done in a non-octal format, as shown in option B. The only other valid chmod option is 644, which does not grant execute permission.

66.  B. The problem statement specified files, making option B the best answer. Option A will also find directories.

67.  C. The -f option removes a function. The other options do not exist for the unset command.

68.  A. The env command, when used as #!/usr/bin/env bash, will determine the location of the Bash interpreter automatically. This makes the resulting script more portable for systems where Bash may not be located in /bin/.

69.  B. The front slash, or forward slash, is used for division. Of the other options, an asterisk is used for multiplication and the other options are not valid.

70.  B. The mailx command can be used to send mail from the command line. The other options shown are not valid commands.

71.  D. The -s operator tests if a file is not zero size. The -d operator looks for directories, whereas -e merely checks if the file exists.

72.  A. An alias exists only for the length of the current session, making option A correct. If the alias or command was invalid, you would have seen it immediately when you created or used the alias.

73.  D. The correct syntax is shown in option D for the scenario described.

74.  B. The user is most likely not using Bash but is rather using another shell like Tcsh. The user could be logging into a different system, but hopefully by having them log out and log in again that would have been noticed, as would their manual removal of the environment variables.

75.  A. The LOGNAME environment variable contains the currently logged-in user. The other variables do not exist by default.

76.  A. The -h test determines if the file is a symbolic link. The -p option tests if the file is a pipe, and -S returns true if the file is a socket. The -t test determines if the file is a terminal.

77.  C. The -f option marks a function as read-only. The -p option prints a list of read-only identifiers. The -a option assumes that the name is an array, and there is no -r option to the readonly command.

78.  B. Option B is the best answer because it will find files where the user permission includes the execute bit. It’s worth noting that options A and C will find the execute bit but only with the exact permissions specified.

79.  A. The /usr/local/bin directory is the location specified for local binaries according to the FHS. It’s also a typical place for scripts as well. The /usr/bin and /usr/sbin directories are for system binaries, and /home/scripts does not exist by default.

80.  D. Ctrl+c is used to terminate a script and is usually used for terminating programs as well.

81.  B. The -0 option follows each environment variable with a null byte rather than a newline. The other options shown are not valid for use with env.

82.  D. In all likelihood, the cp command has been aliased with the -i option. Running unalias cp will correct the issue. It is possible that the cp command has been recompiled to always ask for confirmation, but this is not the most likely cause.

83.  C. An exit code of 1 usually means error, but in the case of grep it means that the search pattern was not found.

84.  B. The -d test checks if a file is a directory. The -e option checks for existence, and the -a option is no longer used. The -w test checks to see if a file is writable by the current user.

85.  B. The command shown prepends /usr/local/bin on to the existing path. Option A uses $PATH, which is the incorrect identifier for the left side of the assignment. Option C appends /usr/local/bin rather than prepends, and option D uses a semicolon as a delimiter.

86.  C. The until loop construct will execute at least once before the condition is evaluated. The while and for loops both evaluate the condition first. The case statement is not a loop construct.

87.  B. The single dot, ., can be used as a means to source environment variables. The other characters and character sequences do not work for the purpose described.

88.  A. The -p option displays all exported variables. The other options shown do not exist.

89.  D. The word do indicates the beginning of a while loop in a Bash script. The other options shown are not valid for the purpose described.

## Chapter 6: Topic 106: User Interfaces and Desktops

1.  A. The greeter is configured through /etc/lightdm/lightdm.conf using the greeter-session option. The other options provided here are not valid.

2.  B. The Screen section of xorg.conf is used to logically bind a given graphics card and monitor, each of which would be defined in its own respective section in the configuration file. The other options shown for this question do not exist.

3.  A. Frequency options are Hz, k, kHz, M, or MHz, making uHz an unavailable option.

4.  C. The systemctl set-default command will be used for this purpose, and the target of multi-user is used to boot to the command line. You will also need to remove the word splash from /etc/default/grub and run update-grub as well.

5.  A. The DISPLAY variable can be used to remotely send the windows of an X session to another computer when using protocols like SSH. There is no XTERMINAL or XDISP environment variable, and XTERM is typically a terminal window and not an environment variable.

6.  D. The Welcome option sets the message to be displayed to users within the display manager when they log in. For remote users, the RemoteWelcome message can be used for the same purpose.

7.  C. The Shift key can be used to enable and disable sticky keys within GNOME and other operating systems for accessibility purposes.

8.  A. The Disable keyword is used to ensure that a given module is not loaded. Note that a Load statement for the same module takes precedence over the Disable statement, but Disable can be used to unload modules that are loaded by default.

9.  A. The Orca project provides assistive screen reading capabilities within GNOME. Of the other options given, the screen program is valid but is not used for this purpose.

10.  C. The xrandr command can be used to change resolution, and changing the resolution to something like 800×600 would make icons and other items appear larger.

11.  D. The allow-guest option changes the behavior of guest login for LightDM, and disallowing guest login would generally make the computer somewhat more secure. However, if someone has physical access to the device, they might be able to get access in other ways.

12.  C. The XFree86 -configure command tells the XFree86 server to query for hardware and create a configuration for the recognized hardware. Note that you may still need to edit the resulting configuration file because of unrecognized hardware or to account for specific configuration items.

13.  B. The XkbModel configuration option is used to set the type of keyboard being used, such as pc105 for a 105-key keyboard. The XkbLayout option defines the layout of the keyboard such as US for United States–style keyboards.

14.  B. The VertRefresh option is used for this purpose and accepts a range of values in the manner shown. The other options given for this question are not valid for the purpose described.

15.  D. The file ~/.xsession can be used for commands that run X clients. The other files are not valid for the purpose described.

16.  C. The linear acceleration profile is enabled by setting AccelerationProfile to 6 within xorg.conf. The 0 setting is known as classic, whereas -1 provides constant acceleration (no profile) and 7 is known as limited, which performs the same as linear but with a maximum amount of speed and acceleration.

17.  A. The /usr/share/fonts hierarchy is used for storage of fonts. Another path that might contain font information is /usr/share/X11/fonts, but that was not among the choices given for this question.

18.  C. Kernel versions beginning with 2.6.26 include native support for Braille displays in Linux.

19.  A. The DontZoom option prevents the specified key combinations from changing the video mode. Of the other options, the DontZap option changes the behavior of the Ctrl+Alt+Backspace key combination. The other options don’t have any effect and are not valid in xorg.conf.

20.  C. The xauth program looks for the configuration file in the user’s home directory in the file .Xauthority. The other files do not exist by default.

21.  C. The Xaccess file is used to control access when using XDMCP. The other files are not valid for this purpose.

22.  D. The kmag program magnifies items on a desktop and is used as an assistive technology. In general, kmag can be used with other window managers as well.

23.  A. The SIGTERM signal causes the X server to exit cleanly. SIGKILL would not be a clean exit. The other signals shown as options are not valid signals.

24.  B. The Appearance section of GNOME Control Center is used to set many aspects of how the desktop appears and behaves, including the choice of a high-contrast theme.

25.  B. Mouse gestures are commonly associated with assistive technologies and help to facilitate uses of programs by moving the mouse in a certain way. Mouse gestures could be used for login and to capture screenshots, but those are not adequately or generally descriptive of their use.

26.  D. The Alt+Super+S keyboard shortcut activates the screen reader in GNOME 3.9 or later. The Super+S shortcut enters Overview, and the other shortcuts provided do not have a special meaning by default. Note that the Super key is also called the Windows key or the Command key.

27.  D. The startx command kicks off the display manager after login to a local terminal. The other commands shown do not exist or will not work for the purpose described.

28.  B. The BlankTime option, which is set to 10 minutes by default, causes the monitor to go blank but not actually go into standby or other power-saving modes.

29.  C. The xwininfo command displays information about a given window within an X session. The other commands listed for this question are not valid.

30.  A. The Mouse button displays keys to move the mouse. The Compose button shows a compose keyboard, and the other options are not valid.

31.  C. The xhost command is used to control access to the X server. A host is added with the + sign.

32.  B. The ForwardX11 option must be enabled on the client in order for X connections or windows generated from the X server to be sent over an SSH connection.

33.  D. The FontPath directive provides another location in which the server can find fonts. The other options do not exist within the context of an xorg.conf configuration file.

34.  D. With an on-screen keyboard, users can utilize a pointer such as a mouse to select keys on the keyboard.

35.  C. The XAUTHORITY environment variable can be used to specify the location of the xauth authority file.

36.  B. The Alt+Ctrl+F1 key combination is used to get to a terminal prompt and is helpful in situations where the X server won’t start properly.

37.  B. The autologin-user option is used to define a user who will be automatically logged in to the system. The other options given in this question do not exist.

38.  C. The AccessX utility is used on legacy or older systems to set many of the accessibility options. The functionality provided by AccessX can typically be found in one of the utilities provided by the native X window manager, dependent on the window manager in use.

39.  A. The export shell command sets an environment variable. In this case, the DISPLAY environment variable needs to be set. The env command shown will not set the variable.

40.  A. The Menus option displays the menu options for a given application so that those options can be manipulated with the keyboard. The Activate option helps to work with the desktop and other applications. The other options shown for this question are not valid.

41.  B. The /etc/lightdm/lightdm.conf.d directory contains individual *.conf configuration files for various settings and is typically parsed along with the /etc/lightdm/lightdm.conf file.

42.  B. The COLUMNS environment variable specifies the width in characters of a terminal device. The other environment variables are not valid.

43.  C. The VideoRam option, which can be expressed in bytes, configures the amount of RAM available to the video card.

44.  B. The Depth option sets the color depth for a given monitor display. A typical value might be 24 for this option.

45.  B. The Identifier option provides a unique description of each of the server layouts in an X configuration. The other options shown for this question do not exist.

46.  A. The mkfontscale command will create a fonts.scale file, which describes the outline fonts on the system and is used for configuration of fonts that are manually added to the system.

47.  A. Display Power Management Signaling (DPMS) enables additional power-saving modes, such as a full sleep mode, that enable further energy efficiency for the display.

48.  B. The emacspeak program provides another visual assistive technology as an alternative to Orca. The other technologies listed here are not related to visualization or assistive technologies.

49.  B. Weston is a reference implementation of the Wayland protocol.

50.  C. The SuspendTime sets the time, in minutes, for the monitor to go into standby mode. The other options shown are not valid.

51.  C. The files in /etc/X11/xorg.conf.d/ are included when X is starting.

52.  B. XDMCP, which is typically disabled by default, uses no compression or transport security. XDMCP is therefore not usually preferred for remote access. Of the other options, SSH offers encryption of the session, and XR and RD are not valid protocols.

53.  D. The Xfce desktop environment uses xfwm4 as its window manager. The other options are not desktop environments.

54.  B. The disable-ticketing option turns off simple authentication for clients with Spice.

55.  B. Simon is the speech recognition software that is part of the KDE project.

56.  D. The only valid panel listed in the options for this question is called Universal Access, making option D correct.

57.  A. The setxkbmap command can be used to enable Xkboptions when X is already running. The other commands shown do not exist.

58.  B. The xrdp program is an open source implementation of an RDP server. The other programs shown are not valid.

59.  A. Changing the VISUAL environment variable to an editor that can run over an SSH session will fix the issue. In this case, /bin/vim was used.

60.  B. The -passwd option is used to set the password on the server for x11vnc.

61.  D. The xauth utility is used for working with the X authority file. The other options shown are not valid.

62.  C. Bounce keys cause the interface to not react when keys are accidentally pressed in succession or held down.

63.  B. The TMPDIR environment variable is used if the normal home directory location, ~/.xsession-errors, cannot be opened. The other environment variables are not valid.

64.  D. The xdpyinfo command displays various elements about the current display(s) along with information about X itself.

65.  B. The Weston configuration file is called weston.ini and is located in ~/.config. The other files are not valid.

66.  A. The x11vnc program, an implementation of VNC, offers built-in SSL/TLS capabilities. The other programs shown are not valid.

67.  B. The brltty program enables a text-mode braille display. The other programs are not valid.

68.  B. The xzoom program is used for screen magnification. The other programs shown are not valid.

69.  D. The GRUB_INIT_TUNE variable can be used within the GRUB configuration in order to beep when GRUB is ready for input.

70.  B. The xhost command will be used for this purpose, and the minus sign removes a host from being able to connect.

71.  B. The Xsession script is executed as the user logging in, making option B correct. The Xstartup script is executed as root prior to the execution of Xsession. The other files are not valid as part of the xdm login process.

72.  A. The -nolisten tcp option disables listening for TCP connections for an X server. The other options are not valid.

73.  B. SIGHUP is used for the purpose described, typically when a user logs out. SIGKILL does not restart the server or prepare for a new connection. The other signal names given as options are not valid signals.

74.  C. The greeter-show-manual-login option, when set to true, will require the user to enter a username for login rather than select the username from a list.

75.  B. The -n option disables hostname lookups. The other options shown are not valid.

76.  C. In runlevel 3, accessed through the telinit command, the X server is not typically executed. Runlevel 6 will shut down the system. Runlevel 1 switches to single-user mode, and runlevel 5 is a multi-user mode in which X is usually running.

77.  C. According to the X server documentation at [https://www.x.org/releases/X11R7.7/doc/man/man1/Xserver.1.xhtml](https://www.x.org/releases/X11R7.7/doc/man/man1/Xserver.1.xhtml), the default location is within the /usr/lib path, but it’s worth noting that Linux distributions may change this location to be within the /var/log/ hierarchy.

78.  B. The ~/.xinitrc file can be used for per-user initialization. The other files are not used by default for this purpose.

79.  C. The -nolisten local option can be added to prevent the X server from listening on abstract sockets.

80.  D. The -broadcast option for XDMCP enables sending of BroadcastQuery packets. The other options shown are not valid options with XDMCP.

81.  C. The gdmsetup program is used to configure various options for the login window and environment, including those for local and remote users. The other options are not used for this purpose or do not exist.

82.  C. Any host within the example.com domain can connect.

83.  C. The family inet6 enables the specified host to connect with IPv6. The other methods shown will not work.

84.  B. The ~/.xsession-errors file is the default log file for Xsession and X clients. The other files are not valid for this purpose.

85.  A. The gok command, short for GNOME On-screen Keyboard, is the program to start the on-screen keyboard. The Caribou program will be the successor to GOK.

86.  B. The -f option enables file specification for the X authority file. The -v option enables verbose output. The other options are not valid.

87.  B. Slow keys is the name used to describe this assistive technology.

88.  C. RDP listens on port 3389 by default. Port 389 is LDAP, and 3306 is usually MySQL.

## Chapter 7: Topic 107: Administrative Tasks

1.  A. The best option among these choices is to change the group to www-data and change the permissions such that the group can write into the directory. Option B should never be used because it enables world-writing to the directory. The other options will not allow the web server group to write into the directory.

2.  B. The format for cron is [minute hour day-of-month month-of-year day-of-week], thereby making option B the correct option for this question.

3.  C. The /etc/localtime file, which can be an actual file or a symbolic link, is used to indicate the local time zone. The other files listed as options do not exist.

4.  D. The LDAP Data Interchange Format (LDIF) is an open format, defined in Request for Comments (RFC) 2849, that enables import and export of LDAP entries. The file formats TXT and CSV are valid but not for the purpose described; there is no specific file format known as LDAP.

5.  B. The chage command will be used for this purpose, specifically with the -E option. When provided with a date, chage will expire the account on that date. When provided with -1, the expiration will be removed.

6.  D. Within the /usr/share/zoneinfo hierarchy, you will find information on the various regions and time zones available. The files within this hierarchy can be symlinked to /etc/localtime. The file /etc/timezone is also sometimes used by Linux systems and, notably, by Java in certain situations.

7.  B. The at command is used to run a series of commands that you enter. Unlike with cron, you can schedule commands from the command line to be executed in the same order entered rather than having to create a specific script for the commands. The syntax shown in option B sets the time to be one hour from now.

8.  B. The userdel command is used for this purpose, and the -r option (lowercase) deletes both the home directory and mail spool files. The -R (uppercase) option tells the userdel command to use a chroot directory.

9.  B. The /etc/shadow file contains usernames, UIDs, and encrypted passwords and is not readable by any non-root user on the system due to the sensitive nature of the encrypted passwords. The /etc/passwd file contains usernames and UIDs but not encrypted passwords. The other two files listed for this question do not exist.

10.  C. Use anacron when you need to schedule a job on a computer that might be off when the job is scheduled. anacron will take care of running the job at its next available time.

11.  B. The +%s option will format the date as seconds since January 1, 1970\. This option is used frequently in scripting and elsewhere for obtaining a unique time stamp that can be parsed easily as an integer. The other options will not work.

12.  C. The --list option shows the available character sets on the system. The other options given for this question do not exist.

13.  C. The LC_TIME environment variable is used to control the display and behavior of the date and time and can be changed to a different locale in order to achieve the desired display and behavior of date and time formatting. The other options shown for this question do not exist.

14.  D. Beginning with OpenLDAP version 2.3, slapd-config is used for configuration of OpenLDAP, as documented at [http://www.openldap.org/doc/admin24/slapdconf2 .html](http://www.openldap.org/doc/admin24/slapdconf2.html). The other commands are not valid.

15.  A. The @daily shortcut schedules a job to run at midnight every day. The other options shown do not exist.

16.  B. UTF-8 provides multibyte character encoding and is generally accepted as the standard for encoding moving forward. ISO-8859 is single byte encoded. The other options are not valid.

17.  A. The groupmod command will be used for this purpose, and the -n option is used to change the group name. The other commands listed do not exist.

18.  D. The /etc/group file contains information on groups on a Linux system. The other files are not valid for the purpose described.

19.  C. The slapcat command dumps the slapd database in LDIF format to STDOUT. The output can then be redirected into a file. The other commands are not valid.

20.  C. The /etc/cron.d/ directory can contain scripts that have scheduling information within them along with jobs to run. The other locations given as options are not valid.

21.  B. The getent command is used to display entries based on the /etc/nsswitch.conf file. One use case for getent is when integrating with Microsoft Active Directory or another LDAP service to check if the connection can be made to the LDAP server. The usermod command is valid but is not used for this purpose, and the other commands shown for this question are not valid.

22.  B. The /etc/login.defs file contains various configuration items such as the minimum and maximum user and group IDs to be used on the system.

23.  C. The LC_MEASUREMENT environment variable is used to indicate the measurement units that should be used.

24.  D. The TZ environment variable is used for this purpose and the general format is as shown, making option D the correct answer.

25.  A. The /etc/cron.daily directory contains files such as scripts that are executed daily. There are corresponding cron.hourly, cron.weekly, and cron.monthly directories that run on their respective schedules, as indicated by the name of the directory.

26.  C. Setting LANG=C is an alias for Portable Operating System Interface (POSIX) compatibility and will cause programs to bypass locale translations. The other options shown for LANG are not valid.

27.  B. The -m option causes the user’s home directory to be created. By default, if this option isn’t specified and CREATE_HOME has not been set, the home directory won’t be created. The –h option displays help text, and the other options shown are not valid.

28.  A. The usermod -L command locks an account by placing a ! in the encrypted password. If the user has another means to log in, such as with an SSH key, using usermod -L will not prevent their login.

29.  C. The LC_ALL variable can be used to set environment variables to the current locale and will override others. This can be used when there is a need for a temporary change. The other variables listed here are not used for this purpose and are not created by default.

30.  A. The format when adding a username places the username between the schedule and the command to run, making option A correct. The other options shown for this question are invalid. In the case of option B, there is no schedule. In the case of options C and D, the schedule is incorrectly formatted.

31.  C. The passwd command will be used for this purpose. The -a option displays all users but requires the use of -S to indicate status. The -S option alone will not produce a report for all users, and the --all option is an alias for -a.

32.  D. The chage command is used for this purpose. The -d option sets the days since the last password change and is measured in days since January 1, 1970\. The -W option is the days of warning for changing a password, and the -l option displays a list of the various settings related to the account.

33.  B. The /etc/anacrontab file contains information about the jobs such as the job name and delay, among other information. The other files listed do not contain anacron-related information about jobs.

34.  D. The ldapadd command is used to add entries to the OpenLDAP database.

35.  B. The /etc/cron.deny file contains a list of users who cannot create cron scheduled tasks. The other files do not exist by default.

36.  B. The system uses shadow passwords if an asterisk shows up in the password field of the /etc/passwd entries. There is no indication that the system has been compromised, making option C incorrect, and there is no password scheme called “forward password aging,” making option A incorrect as well.

37.  D. There is no direct relationship between the UIDs and GIDs on a system. UIDs represent users, whereas GIDs represent group IDs. On some systems, the UID and GID number will match for regular users, but this is not a requirement and is more of a coincidence.

38.  C. The slapindex command generates indexes based on slapd databases. The other commands are not valid.

39.  A. The usermod command is used for this purpose. The -d option changes the home directory, whereas -m moves the contents. The other commands shown for this question are not valid.

40.  D. The -G option is a list of supplemental groups to which the user will be added. A lowercase -g option provides the primary GID. The -l option causes the user to not be added to the lastlog and faillog databases. There is no -x option.

41.  A. The crontab command can be used for this purpose, and the -l option is used to list the crontab entries. The -u option is needed to specify a user other than the current user.

42.  A. The -r option creates a system user that will typically entail no expiration, no home directory, and a UID below 1000\. The -s option defines the shell and is not typically used for this purpose. The -a and -S options do not exist.

43.  B. The /etc/gshadow file contains secure information such as an encrypted password for groups, where applicable. The /etc/group file contains general information on groups. The other two files listed as options do not exist.

44.  D. The slapd_db_recover command can be used to help recover an OpenLDAP database that has become corrupted or otherwise invalid. The remaining options for this question are not valid commands.

45.  B. The groupdel command cannot delete groups unless there are no users who have the given group as their primary GID. There is no -f or -r option.

46.  A. The id command shows the username, UID, primary group, and GID, along with supplemental groups. The passwd and chage commands are not used for this purpose. There is no getid command.

47.  D. The -c option changes the comment field in /etc/passwd. The comment field is typically associated with the real name of the account. The -R option indicates a chroot directory, whereas -d indicates a change of home directory. There is no -n option.

48.  D. The find command will be used for this purpose. The correct syntax is shown in option D. The group command will merely look in the specified files for the number 1501, and the -u option to grep includes byte offsets, which is not applicable for this question.

49.  A. The standard port for unencrypted LDAP is 389, and that is the port on which slapd listens for connections. Port 3389 is RDP, whereas 3306 is MySQL. Finally, 110 is POP3.

50.  A. The ln command is used for this purpose, and the -s option creates a symbolic link, and -f forces or overwrites the destination. The other options or order of commands are not valid.

51.  C. The LC_MONETARY variable is used by certain programs to determine the localization for currency.

52.  C. The --on-calendar option adds a timed event with systemd-run. The other options shown are not valid for use with systemd-run.

53.  B. The /etc/cron.allow file is a list of users who have permission to create and remove their own cron jobs. The /etc/crontab file is used to store cron jobs, and the other files do not exist.

54.  B. Debug level 64 provides configuration processing debug information. Debug level 1 traces function calls, whereas level 8 shows connection management. Debug level 0 is no debug.

55.  C. The atrm command removes jobs given their IDs. The ID can be obtained with the atq command. The at -l command shown will list jobs but not delete them. The rmat command is not valid.

56.  B. The dpkg-reconfigure command is used to cause the configuration questions to be asked again. The tzdata package is the name of the package on Debian-based systems. The two apt- commands shown are not valid.

57.  D. There are multiple ways to specify loglevels and debugging for slapd, including by keyword, by integer, or as shown in the question, by hex. All of the values shown are valid for loglevel. No debugging is 0, trace is 1, stats logging is 256 or 512 depending on type, and packets sent and received is integer 16, or hex 0x10.

58.  A. The /etc/skel directory contains files that are automatically copied to a user’s home directory when that user is created. The other directories listed for this question do not exist by default.

59.  B. The atq command shows a list of jobs that have been scheduled with the at command. The other commands don’t exist with the exception of option D, which shows the at command but with an invalid option, --jobs.

60.  C. The port for LDAPS or LDAP over SSL is 636\. Port 389 is standard, non-SSL, LDAP. Port 443 is used for HTTPS, and 3128 is used for Squid proxies.

61.  A. The at command runs a command at a specified time. While cron can be used to run a command, it will run the command repeatedly according to the schedule set for the command. The other commands are not valid.

62.  D. The /etc/at.allow file is used to specify users who can create at jobs. The other files are not valid.

63.  B. Systemd timer files have the extension .timer and are used for scheduling service unit files or events. The other file extensions are not used for systemd timer units.

64.  A. The /var/spool/cron/crontabs directory contains a file for each user who currently has one or more cron jobs or entries. Note that the other files listed here are not valid for this purpose.

65.  D. The -j option enables specification of a line from which the import will be started. It is useful in the scenario described where the import needs to be restarted due to error. The -f option specifies an alternate location for the slapd configuration file. The -q option is quick mode, with less checking, and -l specifies the input file.

66.  B. The -a option shows all locales currently available on a system. The other options do not produce the output specified in this scenario.

67.  A. The --adjust-system-clock option sets the system clock when used with set-local-rtc. The other options are not valid.

68.  A. The -i option displays information that can help determine the character set such as ISO-8859, ASCII, or Unicode for the given file. The -m option specifies a list of magic files, -l shows a list of patterns, and -a is not a valid option with the file command.

69.  B. The LC_PAPER variable is used to set the paper size for printing. The other variables are not available by default.

70.  C. The /etc/crontab file is a plain-text file that is treated as a systemwide cron file. As such, the file is generally not associated with any single user and it’s not necessary to run a special command after editing this file.

71.  D. The tzselect command will, by default, display a step-by-step menu to select a time zone. The eventual output will include a region/time zone line, such as America/Chicago, as output.

72.  A. The OnBootSec option is used for this scenario and option A has the correct syntax. The other options shown do not exist.

73.  B. GECOS is the legacy name for information stored in /etc/passwd such as full name and other contact information.

74.  A. The -g option sets the group ID for the newly created group. The -h option is help, and neither -k nor -a exists as an option for groupadd.

75.  C. The list-timers option shows the currently active timers with systemd. The other options are not valid.

76.  B. The weekly shortcut means that systemd will execute the event once a week. The other shortcuts given as options are not valid.

77.  A. The -r option removes the current crontab. The -i option can be added so that the user is prompted prior to removal.

78.  B. The SKEL variable controls the location of the skeleton home directory, which is normally /etc/skel/ by default. The other options shown are not used for the purpose described.

79.  C. The passwd option is used to list the password database on a system. The other options do not exist.

80.  A. The directory /var/spool/cron/atjobs contains the jobs. The other directories shown do not exist.

81.  C. The GID_MIN variable contains the minimum GID to use on the system. The other variables are not used for the purpose described.

82.  D. The MAIL_DIR variable contains the directory where a user’s mail spool is located. The other options shown are not valid variables for this purpose.

83.  C. The /etc/passwd file contains various information about users on a system such as username and real name, along with user ID (UID) and login shell. The file is world-readable.

84.  C. The @reboot shortcut indicates that the cron job will be executed when the system starts up.

85.  A. The -r option specifies that the group being added will be a system group.

86.  A. The directory /var/lib/ldap stores database files related to the OpenLDAP deployment on a given server. The other directories shown are not valid for this purpose.

87.  A. Only active units are shown by default, so the --all option displays all units.

88.  B. The /etc/at.deny file contains a list of users who cannot create at jobs.

## Chapter 8: Topic 108: Essential System Services

1.  C. The journalctl command is used to work with the systemd journal. On systemd-based systems, journalctl is a central command for debugging and troubleshooting.

2.  C. The kern facility receives messages from the kernel for logging purposes. Of the other options, syslog is used for logging messages about syslog itself. The other two options shown are not valid syslog facilities.

3.  D. ntp.org provides a free service for time synchronization. When you use pool.ntp.org as the target, you will typically receive an NTP server that is geographically close to your location, or at least as close as possible. Setting your address to 127.0.0.1 or 192.168.1.100 will use a local server but only if that server has an NTP service.

4.  A. The service used for logging on a computer managed by systemd is called systemd-journald. You use the journalctl command to view logged entries rather than the standard Linux toolset.

5.  B. The create option is used for this purpose and accepts arguments such as those shown to set the permissions and ownership. The other options shown are not valid within a logrotate configuration.

6.  D. Configuration files for CUPS are found in /etc/cups. However, it is also common to manage CUPS through its web interface. The other directories listed are not valid.

7.  A. The Allow directive is used for this purpose and the addresses 192.168.1.1 through .127 signify a /25 in Classless Inter-Domain Routing (CIDR) notation, making option A correct. Note that option B, with a /24 netmask, would allow the addresses too but would also allow 192.168.1.128 through .255, which is larger than should be allowed.

8.  B. The ntpdate command provides a command-line interface that immediately changes or sets the time according to the NTP server given as its argument. The ntpd option provided in option A will run the NTP daemon and would not be appropriate for a script. The other two commands are not valid. It is worth noting that ntpdate has been deprecated in favor of ntpd, but you will likely find ntpdate available on many systems.

9.  B. Typically, the Connection refused message from an NTP-related command means that the daemon is not running. There is no indication that the ntpq command is querying a different server; therefore, whether the network is up or down is irrelevant. The permission-based options are not valid based on the error message indicated.

10.  D. The hwclock command is used to both query and set the hardware clock, such as the one maintained by the system firmware or basic input/output system (BIOS). The ntpdate command is used to set the local system time but is not related to the hardware clock. The other commands are not valid.

11.  C. The /usr/share/zoneinfo directory and its child directories contain information on time zones on a Linux system. The other files and directories do not exist by default.

12.  D. The info severity level provides information messages for a given facility. Of the options given, emerg is used for emergency messages and not normally used by applications, whereas debug is the highest or most verbose level of logging available through syslog.

13.  B. The driftfile configuration option sets the location of the driftfile for ntpd. The drift file helps to maintain time accuracy. The location shown is the default for Red Hat Enterprise Linux.

14.  A. The mail option is used to send the log to the specified email address on completion of the logrotate process. The others shown do not exist as options in /etc/logrotate .conf.

15.  C. The journalctl command is used for this purpose, and the --disk-usage option displays the disk space used by journal log files, which are typically stored in /var/log/journal.

16.  D. The mailq command is used on Postfix servers in order to view a summary of the current mail queue. Details of the queue include the ID of the mail being sent along with one or more of the email addresses involved in the transaction. The mailq command may also work with newer versions of sendmail.

17.  C. The ntpq command provides an interactive, menu-like interface into the NTP server. You can use ntpq to check statistics on peers, for example. The ntpdate command shown as option B is used as a command-line means to set the time. The ntpd command shown as option A would execute the NTP daemon itself.

18.  D. The format is *user*: *destination for the aliases file*, making option D correct. The other options are not valid syntax for the aliases file.

19.  B. The -f option indicates the file to which messages will be logged. The -d option is used for debugging, whereas -v prints the version of klogd. There is no -l option for klogd.

20.  A. The chrony package is used for the scenario described and helps with systems that are frequently offline or disconnected from the network. The other packages listed as options are not valid for the purpose described.

21.  A. The lpr command places a file (or standard input) into the print queue for lpd to work with. The lpq command prints the current queue. There is no lpx command.

22.  C. The -bp option to the sendmail command prints information about the current queue. There is no -queue or -f option that is relevant for this question. The -bi option is used to work with the aliases database.

23.  A. The -w option sets the hardware clock to the current system time. The -s option does the opposite, setting the system time to the hardware clock. There is no -a or -m function for hwclock.

24.  D. TCP port 631 is used as the administrative interface into CUPS. Visiting an active CUPS server on that port will show the administration website for working with print queues and other configuration items related to CUPS.

25.  A. The -q option causes sendmail to attempt to deliver messages from the queue. Add the -v option to display verbose output.

26.  B. The requirements of multiple email addresses prevent the use of .forward; therefore, it will need to be accomplished in /etc/aliases. The format for multiple email addresses is to separate them with a comma, making option B correct.

27.  A. The --systohc command will set the hardware clock according to the current system time. The use of --utc is required in order to ensure that the time is set to UTC. If --utc is omitted, the time will default to whatever was used last time the command was run, which could be UTC but might also be localtime instead. Therefore, the best option is A.

28.  D. The postsuper -d command deletes messages from the queue. The ALL keyword causes all messages to be deleted from the queue. Care should be taken when performing this action because it is irreversible. There is no -remove option to postqueue, and the -f option for Postfix is not relevant. The rm -rf command shown is not specific enough, and it is generally not recommended to manually remove files from a mail queue.

29.  A. The URL shown will display the jobs area of the local CUPS server with a query string name of which_jobs and a value of completed. The other URLs shown are not valid.

30.  C. Just as the tail -f command will continuously update the display as new content is added, so too does the -f option display new entries for journalctl. The -t option shows messages for the given syslog identifier. There is no -tail or -l option.

31.  B. The $UDPServerRun option is used for the purpose described. The port on which the server should listen is then provided as the value for this option. The other options shown are not valid configuration items for rsyslogd.

32.  A. The postqueue -f command is used to flush the queue. The command will process all of the emails that are awaiting delivery. The other commands are not valid for this purpose.

33.  C. The -g option specifies the maximum offset or skew that can be adjusted for when synchronizing time. When set to 0, there is no offset check.

34.  A. The SystemMaxFileSize option controls the size of the journal log file to ensure that a log does not cause problems related to disk usage. The SystemMaxUse option controls overall size of journal files, and the default for SystemMaxFileSize is one-eighth of the SystemMaxUse setting to allow for rotation of files.

35.  C. The lpstat command is used for this purpose. The lpstat command displays information about printers, print jobs, and related information. The -W option specifies which jobs to display, complete, or not complete. The lpq command shown as an option is used to view the queue, and the other options are not valid.

36.  D. The postrotate option within a configuration for log rotation can be used for this purpose. After postrotate, a line typically follows with the script or commands to execute. The other options shown for this question are not valid.

37.  B. SMTP operates on TCP port 25, and if other servers are contacting your SMTP server, then you’ll need to listen on this port and allow traffic to it as well. Port 23 is used for telnet, port 110 is POP3, and port 143 is Internet Message Access Protocol (IMAP), none of which are necessary for SMTP traffic.

38.  A. The makemap command is used to create the hashed database in the correct format for sendmail to use. The other commands are not valid for sendmail.

39.  A. The configuration file for syslog-ng is stored in /etc/syslog-ng and is named syslog-ng.conf. There is not typically an /etc/syslog directory, even on systems without syslog-ng.

40.  C. The application could theoretically use any of the logging facilities, depending on the type of application being developed. However, the requirement to log to a custom log file means that the logs will have a different name and possibly location than the standard logs. Therefore, logging to any of the standard or system-level facilities is not appropriate for this scenario, making one of the local (local0 through local7) facilities appropriate.

41.  B. The usermod command with the -aG option is used to append a group onto the user’s list of groups. In this case, the user needs to be a member of the lpadmin group.

42.  D. The nocompress option is used to prevent the log file from being compressed or zipped as part of the rotation process. This might be needed on systems where compression negatively affects performance or where additional processing is necessary.

43.  C. The cupsctl command should be used with the --share-printers option to enable printing for remote clients within the same subnet. You would then also flag each printer for sharing with the lpadmin command, setting the printer-is-shared option to true.

44.  B. The mailstats command is used for the purpose described. Of the other options, the mailq command will display the current mail queue but not statistics on mail that has been processed. The other two options are not valid commands.

45.  B. The --disk-usage option shows the amount of space consumed by active and archived journals. The other options shown are not valid.

46.  A. The systemctl command is used for controlling services. In this case, restart should be sent to the CUPS service as denoted by the name cups.service.

47.  D. The -p option is used to filter based on priority and the loglevel given in the scenario is debug, making option D correct. The other options are not valid for the purpose described.

48.  A. The Port configuration option is used for this purpose and is used as an alternative to the Listen directive. With the Listen directive, you will specify address:port. However, option C, while valid syntactically, will listen only on the localhost IP of 127.0.0.1 and not all interfaces.

49.  A. The postsuper command is used for management of various items with Postfix, including deletion of individual messages from the mail queue. The other commands will not work for the purpose described.

50.  B. The --vacuum-time option will be used for this scenario. Time can be specified in seconds, minutes, hours, days, months, weeks, and years.

51.  B. The file .procmailrc, found in a user’s home directory, is used by Procmail for processing messages on a per-user basis. The other files are not used by Procmail in a default configuration.

52.  D. The format is *local-address*: *destination-address*. Each destination address is separated by a comma. The difference between options C and D is that the question specifically asked for addresses @example.com and since the question didn’t specify whether this server was the server for @example.com, the destination addresses needed to be fully qualified.

53.  D. The postcat command shows the contents of a message from the Postfix queue. The other commands shown are not valid.

54.  C. The /var/log/mail.err file contains errors related to mail delivery. However, on some systems, mail-related errors may go to a different log, such as /var/log/mail.log or /var/log/mail.info or similar.

55.  D. The EHLO command indicates Extended Hello syntax and is followed by the host from which communication has been initiated. Of the other options, the HELO option is valid but is not the Extended Hello syntax specified in the question.

56.  A. The list-timezones option to timedatectl shows the names of time zones and is useful for obtaining the correct time zone name. The other options are not valid with timedatectl.

57.  A. The /etc/localtime file is a symlink to /usr/share/zoneinfo/America/Chicago, making option A correct. Some systems also link /etc/timezone for the same purpose.

58.  A. The date command shows the current time zone. The other options shown will not work.

59.  C. The /etc/chrony.conf file is the configuration file used by the Chrony package. The other files do not exist by default.

60.  C. The -k option shows kernel messages only when used with journalctl. The other options shown do not query the journal.

61.  B. The newaliases command re-creates the aliases database on servers running Postfix, sendmail, and qmail. There is no need to restart the mail server after running newaliases. The alias command shown in option C will create an alias for the command shell but is not related to Postfix.

62.  D. The systemd-cat command logs to the systemd journal. When given a parameter such as a command, both STDOUT and STDERR are logged. The other commands shown as options are not valid.

63.  A. The lprm command is used to help manage printer queues by removing jobs. The other commands shown are not valid.

64.  D. The logger command is used to send messages to syslog and can be executed in a shell script context in order to take advantage of the robustness of syslog without having to write separate log management into the script.

65.  C. The mailq_path parameter contains the path to the mail queue for Postfix. You can use this to diagnose problems with the queue directories. The other parameters shown are not valid in Postfix.

66.  D. The _SYSTEMD_UNIT filter can be used to show messages related to a single service. Multiple _SYSTEMD_UNIT arguments can be given to show messages for multiple services. The other options shown for this question are not valid.

67.  C. The lp command, usually used with the -d option to specify the queue name, is used to add a job to the specified print queue. The other commands shown as options are not valid.

68.  B. When the .forward file is found within a user’s home directory, forwarding of email will typically occur when mail is destined for that user.

69.  B. The -s option sets the subject for the email to be sent. The -E option informs mail to not send messages that have an empty body. The -c option enables setting of carbon-copy (CC) addresses. The -f option specifies an alternate mailbox and would not be used for this scenario.

70.  D. The -s option sets the date and time as specified within the command. If there is another means to automatically set the date, it may override the change. For example, if ntpd is running, that process may alter the date even after it has been set with date -s.

71.  B. The --vacuum-size option to journalctl will trim the journal data files so that they consume the specified size. It is worth noting that the size may not be exactly that specified because journalctl deletes only archived files.

72.  A. The --since option filters journal messages based on the time elapsed since that specified. There is also a corresponding --until option that enables further time filtering.

73.  C. The use of - indicates that syslog does not need to sync to disk for every log entry. This can greatly improve performance for busy systems but may cause log entries to be lost if the sync process has not been run prior to a system crash or other issue.

74.  A. The -P option sends a print job to the specified destination. Of the other options shown, -h disables banner printing, and the remaining options do not exist for lpr.

75.  C. The qshape command displays information regarding the number and age of the messages in the Postfix incoming and active queues. Other queues can also be viewed using the command as well. The other commands shown as options for this question are not valid.

76.  D. The SystemMaxUse configuration option configures how much space journal files can take on the system. The other options shown are not valid, but it is worth noting that there are several options for controlling journal sizes and these options should be examined as part of preparation.

77.  C. The /var/spool/postfix directory contains directories and files related to the mail queue for Postfix. The other directories listed are not valid for this scenario.

78.  D. The --directory or -D option can be used to specify an alternate location for the journal data and would support the scenario described. The other options are not valid with journalctl for the scenario described.

79.  C. The /var/log/ directory is the normal location for system logs, and daemons will typically use this hierarchy for logs as well. For example, some Linux distributions use /var/log/journal/ for systemd journals. The other directories shown as options do not exist by default.

80.  C. The :blackhole: option can be used as a destination to prevent Exim from delivering the mail for that particular user or email account. The other options shown for this question are not valid.

81.  C. The <DefaultPrinter printerName> stanza, where printerName is the name of the printer, configures a printer for CUPS.

82.  C. The lprm command can be used for this purpose and, when given a single dash, will delete all jobs from the queue if run as root. The other options given for lprm are not valid.

83.  B. The -r option enables setting the From header of the email to be sent rather than the currently logged-in user. The -f option specifies a different mailbox and is not useful for this scenario. The -o and -m options do not exist.

84.  B. The @@ symbol specifies that TCP should be used rather than the default @ that normally precedes a host using UDP for remote logging.

85.  C. The Storage=Persistent key/value pair within the [Journal] stanza of the configuration file enables persistent storage for the journal. The other key/value pairs are not valid.

86.  A. The chronyc command can be used for monitoring the status of time updates. The other options shown are not valid commands.

87.  C. Individual configuration files for various log file rotation policies are found in /etc/logrotate.d. This directory is included in the primary configuration file /etc/logrotate.conf.

88.  A. The postqueue -p command and option view the pending queue. The postqueue -f command causes the queue to be flushed. The other commands shown are valid, but their options are not.

## Chapter 9: Topic 109: Persistent Network Configuration

1.  A. The netstat command can be used for this purpose, and the -r option displays the current routes. The addition of -n prevents DNS lookups, which can help with performance.

2.  A. The ifconfig command will be used for this purpose and requires the addition of the -a option because the adapter is currently down. The ifup command can be used to bring up an interface but does not display information by default. The netstat command displays information about the network but not with the -n option.

3.  D. Private IP addresses are found within the 10.0.0.0/8, 172.16.0.0/12, and 192.168.0.0/16 ranges, making an address in the 143 range a public IP.

4.  C. The route command is used for this purpose, and adding a route is done with the add option. The default gateway is added using the default gw keywords followed by the IP of the gateway and the adapter.

5.  A. The host command enables changing of the query type with the -t option. Using ns as the type will query for the name servers for a given domain. There is no all type, and the other options are also invalid.

6.  B. Traditionally, udp/53 is used for DNS queries, but with a primary and secondary server it is assumed that zone transfers may occur. DNS zone transfers typically take place over tcp/53.

7.  B. The -I option enables the choice of interface. A lowercase -i option sets the interval, whereas -a indicates an audible ping. Finally, -t enables a time-to-live (TTL)-based ping only.

8.  D. A /27, with a netmask of 255.255.255.224, splits a subnet into four segments of 32 addresses, thus enabling 30 usable addresses.

9.  A. The host or dig commands can be used for this purpose by setting the type to mx. The mx type will query for the mail exchanger for the given domain. There is no smtp type.

10.  B. The localhost address for IPv6 can be written as ::1\. Addresses shown like 127 represent the IPv4 localhost range but are not written properly for IPv4 or IPv6.

11.  A. The -T option causes traceroute to use TCP packets. This option, which requires root privileges, can be helpful for situations where a firewall may be blocking traceroute traffic. The -i option chooses the interface, whereas -s chooses the source address. A lowercase -t option sets the Type of Service (ToS) flag.

12.  C. The ifup command is used to bring up network interfaces, and the -a option brings up those interfaces marked as auto. Likewise, ifdown can be used to turn off network interfaces. The ifconfig -a command displays information on all interfaces, and there is no ifstat command.

13.  D. The hostname command is used to return the hostname and domain. When given the -d option, just the domain name is returned to STDOUT, thereby making it appropriate for use in a script.

14.  A. The ip command with the monitor option/subcommand will display netlink messages as they arrive. There is no netlink subcommand for ip, and the route command will not work for this purpose.

15.  D. The -6 option, as in traceroute -6, executes an IPv6 traceroute. The other options shown for this question are not valid. It would be rare for the traceroute6 command to not be available and still have the traceroute -6 command available.

16.  A. The syntax is database: databasename with additional database names separated by spaces, as shown in the correct option for this question.

17.  A. The @ symbol is used to indicate a server to which the query will be sent directly. This can be quite useful for troubleshooting resolution problems by sending the query directly to an authoritative name server for the domain. Of the other options, -t sets the type and the others are not valid.

18.  D. SNMP traffic takes place on ports 161 and 162\. Though the traffic is usually on UDP, the TCP ports are also reserved for SNMP. Ports 110 and 143 are used for POP3 and IMAP, respectively, whereas 23 and 25 are telnet and SMTP. Finally, ports 80 and 443 are HTTP and HTTPS.

19.  A. The getent command is used for working with NSS databases, and getent hosts will display the available hosts using the databases configured in /etc/nsswitch.conf.

20.  D. A /25 in CIDR notation represents half of a /24 in address space, therefore making 255.255.255.128 the masked bits. The 255.255.255.0 option is /24, whereas 255.255.255.192 is a /26\. Finally, 255.255.0.0 is a /16.

21.  C. The configuration option is called nameserver, and the value for the option is the IP address of the desired name server. There are several options that affect how name resolution is performed, such as the number of attempts and timeout. Also, the order in which name servers appear affects in which order the name servers are queried. See resolv.conf(5)for more information.

22.  D. The /etc/services file contains standard port-to-protocol information based on the well-known and assigned ports from the Internet Assigned Numbers Authority (IANA). If you’d like to provide a custom name for the service, you can do so by editing this file. There is no /etc/ports or /etc/p2p file by default, and /etc/ppp is usually a directory for the Point-to-Point protocol daemon and related services.

23.  A. The route command can be used for this purpose, and the syntax includes the network range, denoted with the -net option, followed by the word netmask and the masked bits, followed by the lettersgw and the IP of the gateway. The other options shown are invalid for a variety of reasons, including missing keywords and options and order.

24.  C. The -a option displays statistics for each socket, both listening and non-listening. Included in this information is the send and receive queues. This information can be used to gauge performance and potential bottlenecks.

25.  A. The correct format is the IP address followed by canonical hostname followed by any aliases for the host. You can use entries in /etc/hosts to override DNS lookups, which can be useful to prevent those names from resolving or to provide a different resolution.

26.  C. The ifconfig command for configuring interfaces begins with the device followed by the IP address, which is then followed by the netmask keyword and the netmask you want to add. Because this is a /24, the netmask is 255.255.255.0.

27.  C. IPv4 addresses are 32 bits in length and IPv6 addresses are 128-bits. Both IPv4 and IPv6 can be used on internal and external networks alike, and subnetting is indeed necessary with IPv6.

28.  D. ICMP is a layer 3 protocol, meaning that it does not use ports for communication. TCP/43 is used for whois whereas port 111 is used for sunrpc. UDP/69 is used for the TFTP protocol.

29.  B. The ip route command can be used for this purpose, and its syntax uses a change command and the via keyword. The same operation could be completed with the route command but would require deleting the existing gateway first and then re-adding a new default gateway.

30.  C. Secure Shell (SSH) operates on TCP port 22 by default. TCP/23 is used for telnet, TCP/25 is used for SMTP, and TCP/2200 is not associated with a well-known service.

31.  B. The nc command is used to start netcat and the -l option causes it to listen. The -p option is used to specify the port on which netcat will listen. The -s option specifies the local source address and is not used for this scenario.

32.  A. The soa type is used to query for Start of Authority records for a domain. Note that in many cases, dig will attempt to look up the domain within a given command and may not appear to have had an error. For example, when running option D (dig -t auth example.com) you will receive information about example.com and there will be a line in the output that dig has ignored the invalid type of auth.

33.  A. The search option is used for this purpose and can be provided with multiple domain names, each separated by a space or tab. The domain option is valid within /etc/resolv.conf but does not allow for multiple domain names. On newer systems, systemd-resolved has taken over for the /etc/resolv.conf file.

34.  C. The ping6 command is used to ping IPv6 addresses. Unique local addresses are the IPv6 equivalent of RFC 1918 private addresses in IPv4\. In IPv6, fc00::/7 is the unique local address space. Note that there is no -6 option to the normal ping command.

35.  A. The route command can be used for this purpose, and in the scenario described, a reject destination is used for the route. The other options shown are incorrect because they use invalid options to the route command.

36.  B. The tracepath command provides the maximum transmission unit (MTU) of the hops where possible. Both traceroute and tracepath can be used internally or externally, and both provide IPv6 capabilities, though traceroute6 and tracepath6 provide IPv6 capabilities as well. Certain options with the traceroute command can require root privileges, but not enough information was given in the question for that to have been the correct option.

37.  D. The -c option provides the count of the number of pings to send. The -n option specifies numeric output only, whereas -p specifies the pattern to use for the packet content. Finally, the -t option sets the TTL.

38.  A. The nmcli command provides a command-line interface suitable for working with NetworkManager through a terminal or SSH connection. The nmtui command provides a curses-based interface that also works through a terminal or SSH connection.

39.  A. The syntax for ifconfig uses the device—in this case followed by the protocol inet6—and then the keyword add to indicate that an additional IP address is being added, followed finally by the address itself.

40.  C. LDAP over SSL, or LDAPS, operates on port 636\. Port 53 is used for DNS, port 389 is used for normal, non-SSL LDAP, and port 443 is used for HTTP over SSL.

41.  D. The best option for this question is to add an entry for the host in /etc/hosts. Doing so will always cause DNS queries to resolve to 127.0.0.1\. The other options are not as robust because they rely on [www.example.com](http://www.example.com) always having the same IP address, or the solutions require additional maintenance to constantly add new IP addresses if [www.example.com’s](http://www.example.com) IP address changes.

42.  A. The ip route flush cache command should be executed after changing the routes. The other commands shown for this question are not valid.

43.  A. SPF records are stored in the txt record type in DNS, making -t txt the correct option for this. Of the other options, only -t mx is valid and returns the mail exchangers for the given domain.

44.  B. TCP is a connection-oriented protocol that uses a three-way handshake to establish a connection. ICMP does not use ports for communication, and UDP is connectionless. IP is the core Internet Protocol and does not use a handshake.

45.  D. There are 1,048,576 IP addresses in the 172.16.0.0 private range. There are 16,777,216 in the 10.0.0.0 range and 65,536 in the 192.168.0.0 range.

46.  C. The only viable possibility of those listed is that ICMP traffic is blocked. TCP traffic is obviously passing because of the ability to get there using HTTP, and DNS must also be working.

47.  C. The G signifies a gateway within the route table.

48.  A. The axfr type is a zone transfer, and the @ symbol signifies the server to which the query will be sent. There is no xfer type, and option B is just a normal query for the domain sent to the specified server.

49.  D. The netstat -s command displays aggregate statistical information for networking, including the total packets received and the number of packets forwarded. The ifconfig command does not show packets forwarded. The ls command is not used for networking, and the ipstat command does not exist.

50.  C. The ip command defaults to the inet family if not otherwise specified with the -f option. The command will attempt to guess the correct family and fall back to inet. The other families listed as options for this command are not valid for use with the ip command.

51.  B. The ifconfig command will be used for this purpose, followed by the interface. The hw keyword is used for the hardware address, which is then followed by the hardware class, in this case ether. That is followed by the new MAC address (not depicted in the options). The other commands are not valid.

52.  D. The -n option causes route to use numeric values only, performing no name resolution. This option is useful for the scenario described. The -e option causes the output to be in netstat format. There is no -d or -f option for the route command.

53.  A. Because we’re working with MAC addresses, the arp command will be used. The -d option removes or deletes an Address Resolution Protocol (ARP) entry, which would be appropriate here so that the MAC address resolution occurs again. The netstat command will not be used for this purpose. The hostname and dig commands work with name resolution but not for MAC addresses or the ARP table.

54.  A. The iw command will be used for this purpose. When using iw with a specific device, the dev keyword appears next, followed by the device name and then the command you want to execute on that device. In this case, the link command is used.

55.  B. The iwconfig command, which is similar to the ifconfig command, works with an individual wireless interface to set and display parameters. Of the other commands, the ifconfig command is valid but not used for wireless. The other commands are not valid.

56.  C. The iwlist command will be used for this purpose, and the scan subcommand is used to look for local access points and wireless networks. Superuser privileges are required for a full scan. The iwconfig command does not have a scan subcommand. Likewise, there is no subcommand called get for the iwlist command, and there is no iw-scan command.

57.  B. NTP listens on UDP port 123 by default. Ports 20 and 21 are used for FTP services, port 139 is used by NetBIOS, and port 5150 is not usually used.

58.  B. The mtu can be used to set the value for the maximum transmission unit (MTU) for a given interface. The metric option sets the interface metric. The other options are not valid.

59.  A. The -s option creates an ARP table entry. The -d option removes an entry. The -c and --add options do not exist.

60.  A. The ss command provides many of the same functions as netstat but can show some extended information, such as memory allocation for a given socket. The free command shows memory usage but not by socket, and the other two commands do not exist.

61.  D. The -f option is a flood ping. This will effectively cause the interface to send and receive large amounts of traffic, usually making it easier to find on a switch. The -a option is an audible ping, emitting a sound on ping. The -c option sends a certain count of pings, and there is no -e option.

62.  B. The netcat command provides a method for opening and communicating on both sides, server and client, for a TCP connection. The netcat command avoids some of the issues with telnet capturing characters specific to the Telnet protocol. The netstat command does not test connectivity, and ping does not do so at the TCP level. There is no nettest command.

63.  C. The -D option lists the interfaces on a given computer. The -d option dumps compiled matching code, and -i selects an interface. There is no -a option.

64.  A. The ping6 command performs the same as the IPv4 ping command but does so for IPv6\. The other commands are not valid on Linux.

65.  B. The ip command can be used for this purpose. When using it with the addr object and the -6 option, only information about IPv6 addresses will be shown. The first option, simply ip addr, will show all addresses, including IPv4\. The other commands are not valid.

66.  A. The ifconfig command will be used for this purpose, and ARP can be disabled by preceding the word arp with a minus sign, as shown. If no minus sign is present, then ARP will be enabled. The other commands will not work for this scenario.

67.  C. The dev option specifies the device to use for the route being specified. This is a typical use case for many routes to reduce the chance of the kernel guessing incorrectly. The other options shown for this question are not valid.

68.  C. The -p option shows the process IDs associated with a given socket within the ss output. The -a option is all sockets, whereas -l is listening sockets. The -f option is used to specify the protocol family.

69.  C. The -I option tells traceroute to use ICMP for requests. The -T option is TCP SYN. The -A option performs AS path lookups, and the -i option configures traceroute to use the specified interface.

70.  C. Internally, the hostname command uses gethostname. This can be useful to know when troubleshooting address resolution issues such as conflicting results for host naming. The other functions are not valid.

71.  A. The grep command used with the -i option makes the grep case insensitive. When used with the -v option, grep will exclude the argument, thus doing the opposite of what’s needed here. The kernel ring buffer will probably not contain information about DHCP, making dmesg an incorrect option.

72.  B. Only alphanumerics, minus/dash, and dot are valid for hosts in /etc/hosts.

73.  B. Options within /etc/resolv.conf are preceded with the options keyword followed by one or more options, such as debug.

74.  D. The journalctl command will be used for this purpose. Adding the -u option specifies the unit for which journal entries are desired.

75.  A. The /etc/hostname file typically contains only the hostname of the local computer rather than the hostname and domain name. This is then read at boot time to set the hostname for the computer. The /etc/hosts file contains information on various hosts for name resolution purposes. The other files do not exist.

76.  B. The traceroute6 command is used for tracing IPv6 routes. The other commands do not exist.

77.  D. The axfr type can be used with dig to request a zone transfer. The client from which you request the zone transfer will need to be authorized to initiate a transfer.

78.  A. Setting -a as an option to the host command sets the query type to ANY. The -c option sets the class, and -d turns on debugging. There is no -b option.

79.  C. The .digrc file, when created in a user’s home directory, can be used to set defaults for use of the dig command. There is no dig configuration file found in /etc.

80.  D. POP3 servers do not have a specific type in DNS. MX type indicates mail exchanger, or SMTP server.

81.  A. The ip addr add command is used to add IP addresses to interfaces using the syntax shown in option A. The other options do not have the correct syntax.

82.  B. The resolvectl command is used for assistance with resolution issues for systemd-resolved and, when given the status command, will return the DNS settings. The other options shown do not exist. The resolvectl command is somewhat new, and if it’s not yet available on a given systemd-based distribution, then systemd-resolve --status can be used.

83.  A. The nmcli command is the only valid NetworkManager command shown as an option, and when given the networking on command, NetworkManager will control the network interfaces. It is worth noting that if you disable NetworkManager control with networking off then all of the previously managed interfaces are disabled.

84.  B. NXDOMAIN is the status for a nonexistent domain or host, basically that the host for which the query was sent does not exist. A normal status when there has not been an error is NOERROR.

85.  C. The systemd-networkd daemon can be used to manage networking through systemd. The other options shown are not valid.

86.  B. The set-hostname command within hostnamectl sets the hostname of the device. The other commands shown are not valid for use with hostnamectl.

87.  A. IMAPS uses port 993 by default, as defined by IANA. Port 995 is POP3S, port 465 is SMTPS, and port 514 is used by syslog.

88.  B. The -o option removes newlines from the output, making the output more suitable for the grep command. The -l option specifies the number of loops for the ip addr flush command, the -f option specifies the protocol family, and there is no -n option.

## Chapter 10: Topic 110: Security

1.  A. If /etc/nologin exists, users will be prevented from logging in to the system. The root user can still log in, assuming that root logins are enabled within the ssh configuration.

2.  B. The find command will be used for this purpose, and the permission can be described as 4000 to indicate the presence of the setuid bit. The -type option can be used to change the type of object to be returned but is not relevant for the scenario described.

3.  B. The lsof command can be used for this purpose and, with the -i option, will display the network ports along with their process. The netstat command, when run with the -a option, will display network ports but not the process. The ps command is used for processes but not network ports. Finally, there is no netlist command.

4.  A. The fuser command can be used to determine which process is using a given file. The ls command will show files and find can be used to find files but not specifically for this purpose. The ps command does show processes but not necessarily ones tied to a particular file.

5.  D. The chage command is used for working with account aging information such as expiration date, password change, days between password changes, and so on. The -l command lists information for the given account. The usermod command is used to make changes to an account, and the other two commands are not valid.

6.  A. The nmap command is used to scan for open ports. By default, the nmap command will scan for open TCP ports to the address or addresses specified. The other commands shown do not scan for open ports to external (off-host) IP addresses.

7.  B. The ssh-keygen command is used to create a key pair for use with ssh instead of a password. Of the other options, the ssh command does exist but the -k option is used to disable Generic Security Service Application Program Interface (GSSAPI) credential forwarding and not for the purpose described.

8.  B. The format is username (or other specifier) followed by hard or soft, depending on the limit type, then the keyword followed by the value for that given keyword.

9.  A. The authorized_keys file, stored in the .ssh directory in your home directory, contains public keys that are authorized to log in to the server using their corresponding private key.

10.  C. The -p option shows the process ID to which a given port is connected and is useful for displaying information about which process is listening on a given port. The -a option shows listening and nonlistening sockets whereas -n disables name lookups. The -l option shows listening sockets only.

11.  D. Loading alternate files is accomplished using the -f option. Doing so facilitates exactly the scenario described, being able to examine logins from old log files. The -a option controls the location of the display for the host, whereas -t controls the display to output the logins as of the specified date and time. There is no -e option.

12.  D. The w command shows currently logged-in users along with information such as uptime and load average. The fuser command is used to show open files, and the -u option to ls controls the display for file listings. There is no listuser command.

13.  A. The -u option is correct for this purpose. An uppercase -U option sets the user context for listing privileges. The -s option sets the shell, and the -H option sets the home directory.

14.  B. The NOPASSWD option causes sudo to not prompt for a password for a given sudo command. This is useful for scripted scenarios where a password prompt would cause problems.

15.  C. The ulimit command shows such limits, and the -a option shows all limits for the currently logged-in user. The other commands are not valid.

16.  C. The syntax to block access to every service uses the ALL keyword followed by the address or network to which the policy will apply.

17.  A. The correct format is YYYY-MM-DD for the usermod command.

18.  C. The disable option is used for the purpose described, and can be set to yes or no. The other options are not valid for this scenario.

19.  A. The file is named id_rsa by default, and the public key is named id_rsa.pub. For DSA keys, the names are id_dsa and id_dsa.pub. Other key names such as id_ecdsa, id_ecdsa.pub, id_ed25519, and id_ed25519.pub are also used depending on the algorithm. For client keys, these are typically stored in ~/.ssh/ by default.

20.  C. The -c option executes a single command but does so without an interactive session. The -s option specifies the shell to be used. There is no -u or -e option for the su command.

21.  A. The /etc/security/limits.conf file (on some Linux distributions this file could be /etc/limits.conf) enables the setting of limits for user logins, processes, memory usage, and other resources. The other files shown do not exist by default.

22.  B. There is no special option necessary in order to execute a single command on a remote host with ssh, although you might sometimes place the command in quotes if spaces are included. The -s option requests a subsystem and is not related to this scenario. The -e option specifies an escape character.

23.  D. The ssh-add command is used to list currently loaded keys and is used in conjunction with ssh-agent. There is no -l option to ssh-agent, and the -l option to ssh specifies the login name to use. There is no ssh-list-keys command.

24.  C. While any text editor can be used, it is highly recommended that you use the visudo command to edit /etc/sudoers. Using visudo enables syntax checking, which will help to prevent issues with an invalid configuration, causing problems for those who rely on sudo.

25.  A. The systemctl command will be used for this purpose, and the subcommand is disable. There is a stop subcommand, but it will only stop the given service rather than prevent it from starting on boot. The other options are invalid for various reasons, including that they use systemd as the command name rather than systemctl.

26.  B. The chage command can be used for this purpose, and the -E option accepts days since 1/1/1970\. There is no -e option to passwd, and -l for usermod will not perform the action described. There is no chguser command.

27.  C. The GlobalKnownHostsFile configuration option enables the specification of a server-wide known hosts file, thus preventing users from needing to accept host keys for the hosts specified therein.

28.  C. The maxlogins parameter is used to control the number of simultaneous logins for a given account.

29.  B. The ssh_known_hosts file, typically kept in /etc/, is used for the purpose described. Note that on some systems, this file and other SSH-related configurations may be found in /etc/ssh/. The options that indicated ~ or within /root are incorrect because the question specified a server-wide list.

30.  C. The date of the last password change, as measured in days since January 1, 1970, is contained in the third field of a shadow entry. The expiration date would be the 8th field, as separated by colons.

31.  A. The format for local forwarding uses the -L option followed by the local port and then the remote host:port combination. This is typically followed by the user@host credential and destination information for the SSH connection itself.

32.  C. The option is called X11Forwarding and it must be set to yes in order for the destination server to forward X-based windows to the local client computer. The other options shown are not valid.

33.  A. The --gen-key subcommand is used for the purpose described. The other options shown do not exist.

34.  A. The --sign option is used to sign files and documents with gpg. The other options shown are not valid for signatures.

35.  A. The -p option sets the port for login and is useful for scenarios where you cannot use the host:port syntax. There is no -P or @ option with ssh, and the -l option specifies the login name.

36.  A. The -s option sets the type of scan and, when followed by an uppercase S, sets the option to SYN. The T option is a Connect() scan. There is no Y or -type option for nmap.

37.  C. The wtmp file, stored in /var/log, is used to store recent login information and must be read with the last command due to its format. The other logs listed for this question are not default logs found on a Linux system.

38.  A. The -i option for ssh is followed by the private key to use for authentication. Doing so implies that the public key is in the authorized_keys file on the remote host. The -k option disables sending of GSSAPI credentials, whereas -f is used to request backgrounding of ssh. There is no --key option.

39.  A. The -n option facilitates the scenario described and will exit non-zero rather than prompting. The -i option sets the login name and is not valid for this scenario. The -q and the --noprompt options do not exist.

40.  C. The ssh-keygen command will be used for this purpose, and the -t option specifies the type of key to generate. There are no key-related generation options for the ssh command.

41.  B. Lines can be commented out of /etc/inetd.conf with a pound sign or hash mark (#). After making changes to /etc/inetd.conf, the service should be restarted.

42.  A. The -L option to usermod can be used to lock an account. The lowercase version, -l, is used to change a username. The other commands do not exist.

43.  B. The pubring.gpg file, found in ~/.gnupg/, contains the public keyring.

44.  C. The .gpg-v21-migrated file, when present, indicates that gpg version 2.1 or later is in use and that the files have been migrated for that version or a later one.

45.  D. The find command will be used for this purpose, and the -perm option is needed, specifically as the 2000 permission to indicate setgid. Note the use of / to indicate that the entire server will be searched. The grep command shown cannot be used for this purpose because it looks for the presence of the string 'setgid' within files located in the current directory only.

46.  C. The update-rc.d command creates symbolic links from a service file in /etc/init.d/ to the appropriate locations in /etc/rc.d/* for each runlevel. The other commands shown are not valid.

47.  A. Single-user mode is typically runlevel 1\. In runlevel 1, no network services are started. Runlevel 2 has networking but typically not services. Runlevel 5 is full multiuser with networking, and runlevel 6 is reboot.

48.  C. The - option is the typical option passed to su for login. There is no -u or -U option, and the -login option does not exist. There is a --login option with two dashes, but that is not what’s shown.

49.  A. The netstat command is used for this purpose, and the -a option displays all sockets, listening and nonlistening. Note that it’s frequently helpful to add the -n option, or combine them as in netstat –an, in order to prevent name lookup. Doing so can significantly improve the performance of the command.

50.  C. This solution will require a way to filter out the bind user; therefore, options that grep for bind or specify bind as the user are incorrect. However, the lsof command allows for negation with the caret (^) character. Therefore, listing all files except bind requires the syntax shown.

51.  B. The -R option requires an attempt at name resolution be performed. The -n option does the opposite; it disables name resolution. There is no -b or -a option.

52.  C. The PARANOID wildcard specifies that the hostname and IP must match. The ALL keyword is also a valid wildcard in TCPWrappers for use in both /etc/hosts.allow and /etc/hosts.deny.

53.  A. The PermitRootLogin directive, set to yes or no, determines whether the root user can log in directly. The other options shown are not valid.

54.  B. The nmap command will be used for this purpose, and the -sT option performs a TCP connect to the specified host or network. The other commands are not valid.

55.  C. The -X option enables X11 application forwarding through an SSH connection. The -A option is used for authentication agent forwarding, and -F indicates a per-user configuration file. There is no -X11 option.

56.  B. The --output option is used with --encrypt to send the output to a specified file. The other options shown are not valid for gpg.

57.  B. The ssh-add command adds keys to ssh-agent. The other commands shown are not valid.

58.  B. The -x option sets the maximum password age until the password needs to be changed again. The -l option locks the account, and the other options do not exist.

59.  A. The -l option sets the maximum amount of memory that can be locked. The -t option sets the maximum CPU time, and the -x and -b options do not exist.

60.  B. The command shown to display the password file and pipe the output into cut will display the usernames from the password file, /etc/passwd. The /etc/shadow file would also produce the same output.

61.  B. The access_times configuration item sets the times in which access is allowed. The other configuration options shown are not valid.

62.  A. The .socket file extension is used for interprocess communication, network sockets, and first-in, first-out (FIFO) queues controlled by systemd. For more information, see systemd.socket.

63.  C. The -N option provides the “new” passphrase, and when generating a key, it can be used to generate an empty password. The -p and -P options both work with passwords but would do so on an existing key. The -d option does not exist for ssh-keygen.

64.  A. The MD5 algorithm has been used if the password in /etc/shadow begins with $1$. Of the other options, shadowed passwords beginning with $2a$ or $2y$ would indicate the Blowfish algorithm. There is no RIN or PIK algorithm for shadow passwords.

65.  B. The --detach-sig option creates a detached signature file so that the original file remains unchanged. Both the original file and detached signature file are needed in order to verify the signature. The other options do not exist.

66.  C. The server host key provides a means by which clients can verify that the server host key has not changed.

67.  B. The IdentityFile option specifies the key that will be used to connect to the host. The other options do not exist for client configurations in SSH.

68.  C. The gpg-agent command is a daemon process to manage private keys. The gpg program and other GnuPG-related utilities use gpg-agent. The other options shown for this question are not valid.

69.  D. The sudoedit editor, part of the sudo package, can be used for the purpose described. Of the other commands, only nano is a real command, but it would also present the same possibility of shell escapes as vim would in this scenario. While there may be ways to prevent a shell escaping with both vim and nano, sudoedit is typically the preferred option.

70.  A. The -l option changes the login name for a connection with ssh. Among the other options, only -a and -m exist and are not used for the purpose described.

71.  A. The -l option for usermod changes the username. It is worth noting that the user’s home directory and mail spool file do not change and would need to manually be changed following the usermod command. The other options are not used for the purpose described.

72.  C. The send-keys option followed by the name of the key sends the key to the key server specified by the key server option. This is a typical scenario for sending a locally generated public key to a public server for others to use. The other options do not exist.

73.  D. The % is used to denote a group within /etc/sudoers and provides an excellent way to facilitate an administrative privileged group.

74.  D. The fsize option is used within the limits.conf file to control the maximum size of a file that can be created by a user for whom the limit applies.

75.  B. The ServerAliveCountMax option is used to set the number of keepalive messages that can be sent by the client but not responded to before the client will terminate the connection.

76.  C. The /etc/nologin file prevents login when present and can also contain a message that is displayed to users when attempting to login.

77.  A. The -t option specifies the lifetime for the key and is usually given in seconds but can also be given in minutes, hours, days, and weeks with qualifiers. The other options shown do not fulfill the scenario described.

78.  A. The -R option sets up a remote forward so that remote users can also connect to the tunnel being set up. The other options are not valid for the remote forwarding scenario.

79.  B. The -W option sets the number of days to warn a user before their password expires. The other options do not exist for chage.

80.  B. The /etc/shadow- file contains the state of the shadow file before the last change and would likely be the first place to begin recovery. The next would likely be a backup, though /var/backups/ does not hold backups unless manually created.

81.  B. Integration with the libwrap library is an indicator that a given service or daemon will be able to utilize TCP wrappers for access control.

82.  A. The User_Alias option enables specification of a group of users for use elsewhere within the sudoers file.

83.  A. Setting -P0 will allow no ping requests to precede the scan and is useful for the scenario described. There is an -s option, but it is not used for this purpose. The other options are not valid.

84.  C. The UserKnownHostsFile configuration option enables specification of the location and filename for the known hosts file for users.

85.  C. The -t argument sets the type of key to generate, and dsa creates a key with the dsa algorithm. Other types includes rsa and ecdsa. The files are normally placed in /etc/ssh and assigned names such as ssh_host_[algorithm]_key and ssh_host_[algorithm]_key.pub, where [algorithm] is one of rsa, dsa, ecdsa, or ed25519.

86.  C. The -q option prints the users who are logged in along with a count of those users. The -l option prints the login processes, the -t option prints the last system time change, and the -e option does not exist.

87.  B. The -u option unlocks an account while setting the password. The -l option locks the account, and the -t and -r options do not exist for the passwd command.

88.  C. The maxlogins option is used to control the number of times that a user can log in. The only other limit-related option shown is maxsyslogins, which sets the maximum number of logins for the entire system.

## Chapter 11: Practice Exam 1

1.  B. The /proc filesystem stores information about running processes on the system. The /etc filesystem is used for configuration information, and /dev is used for device information. The /environment filesystem does not exist on a default Linux system.

2.  C. The /etc/modprobe.d directory contains information related to the modprobe configuration. This can be overridden with the -C option on the command line.

3.  A. The -g option to wall sends the input to the specified group. Answer B will send the output to all users, whereas answers C and D will not work.

4.  B. The -e option to dmesg displays the time in a localtime and the delta in a format that is typically easier to work with. The -rel option does not exist. The -f option specifies the logging facility, and -t does not display time at all.

5.  B. The init process is typically associated with the initial process ID of 1 to indicate that it is the process from which others are spawned. Killing PID 1 will typically and immediately halt the system.

6.  C. The lspci command shows the PCI devices in the system, and the -k option shows the kernel driver being used by the given device. The lsusb command will not accomplish the task requested and the ls command with -pci will not display the correct information. There is no showpci command.

7.  C. The --no-wall option will cause telinit to not send a wall command to logged-in users about the state change. The other options listed in this question do not exist.

8.  A. The class/net hierarchy within /sys contains information on the network configuration for the computer. It is a symlink to the devices hierarchy, where the device will be listed by its address rather than the logical eth0 name.

9.  B. The SIGTERM signal is the default signal sent with the systemctl kill command.

10.  D. A logical location to begin troubleshooting is within the system BIOS to ensure that the drive is being detected by the computer.

11.  C. The dbus-monitor program, which requires an X display, can be used to monitor dbus. The other programs and options listed for this question do not exist.

12.  A. The udevd service is called systemd-udevd.service within a systemd environment.

13.  A. The system can be scheduled to shut down at a certain time, and that time should be entered in 24-hour format, as shown in the answer.

14.  C. The -s option changes the signal to be sent from its default of SIGTERM. The new signal must be one of the main signal types, such as SIGINT or SIGSTOP.

15.  D. The list-unit-files command will show the files available, whereas --type=service will limit those files to the services, in the same way that chkconfig --list returns a list of services.

16.  A. The -C option sets the location of the cache to be updated instead of the default /etc/ld.so.cache. The lowercase option, -c, changes the format of the cache, whereas -v sets verbose mode. The --f option does not exist.

17.  C. The -P option to dpkg will purge a package from the system, including the configuration files associated with the package. The apt-cache clean command cleans the package cache but not an individual package, and the apt-get remove command removes a package but not the associated configuration files.

18.  C. The deb-src prefix is used to indicate that a given repository contains source packages. The deb prefix in option A would indicate normal packages. The other options are not valid.

19.  B. The -U option is used to upgrade a package. Adding -v for verbose and -h for hash marks will print additional information and progress, as requested by the problem.

20.  A. The -y or --assumeyes option will do what it says: Assume that you will answer “yes” and therefore not prompt. The other options do not exist.

21.  A. The exclude option within /etc/yum.conf is a space-separated list of packages that accepts wildcards and is a list of packages that cannot be installed or upgraded. The other options listed in this question do not exist.

22.  C. The ldconfig command is used to work with the library cache, and the -p option prints the directories and libraries in the cache. The -C option tells ldconfig to use a different cache. The ldd command prints the library dependencies for a given command, but the options given don’t exist for ldd.

23.  D. The baseurl option is used to set the URL and must be fully qualified, meaning that it must include the protocol, such as http:// or file://.

24.  B. The apt-cache dump command will display a listing of the available packages and their respective dependencies. The other commands and options listed in this question do not exist.

25.  A. The /boot directory almost certainly exists but has not been partitioned into its own space. The /boot partition would not be hidden from lsblk if it was indeed a separate partition.

26.  B. The /var/cache hierarchy contains cached data for both package management tools—in the case of yum, in /var/cache/yum, and in the case of a Debian-based system, in /var/cache/apt.

27.  A. The master boot record (MBR) is the typical location for the boot loader to be stored on a BIOS-based system.

28.  D. The / filesystem is the root filesystem. If separate partitions have not been created, the / filesystem will be the beginning of the hierarchy and will contain all other directories in the same partition.

29.  A. The --output option configures the location for output of the command instead of STDOUT.

30.  A. The dd command is used for this purpose, and for this case it takes an input file with the if option and an output destination with the of option. The bs option signals that the block size for writing should be 1 megabyte.

31.  D. The history command displays history from the current session and can be used for the purpose described. The .bash_history file is written on session close, by default.

32.  C. The --boot-directory option will install the boot images into the directory specified. This might be helpful for nonstandard installs or at times when you need to mount the boot partition separately. The other options listed in this question do not exist.

33.  A. The update-grub command should be executed in order to make changes take effect in the menu and when changes have been made to the GRUB configuration. The other commands listed in this question do not exist.

34.  B. The export command is used for this purpose and accepts a name=value pair, as shown in the answer. The other commands are not valid with the exception of the echo command, which will simply echo the argument to the console.

35.  C. The HISTFILESIZE option configures the number of commands to keep in the history file. The other variables are not valid within Bash.

36.  D. The -b option configures the body numbering format for nl, which by default will not number blank lines. The a format option will number all lines, including blanks. The -a option is not valid for the nl command, and the -n option configures the numbering format and would require an additional argument in order to be valid.

37.  D. The od command is used to create octal output. The cat command will show the file as it exists on disk. The other two commands are not valid.

38.  A. The pr command formats text for printing, including the date and page numbers at the top of each page. Adding the -d option causes the output to be double-spaced. The cat command will display output but not paginated in such a way. The other two commands are not valid.

39.  A. The -n option is used to change the number of lines. Adding the +N after the -n option begins the tail process at the *N*th line within the file.

40.  C. The -i option causes the unique test to be done while ignoring the case of the element to be matched.

41.  C. The awk command shown can be used for this purpose. The -F option sets the field separator, and the OFS option sets the output field separator.

42.  C. The -a option is equivalent to the -d and -R options, which preserve links and copy recursively, respectively. The -b option creates a backup, and -f forces the copy.

43.  A. When in command mode, typing a number followed by an uppercase G will immediately move the cursor to that line number. The /23 option will search for the number 23 in the file. The i23 option will insert the number 23, and finally ZZ will exit Vi.

44.  A. The -d option changes the update interval and can be helpful on a busy system where top may be affecting performance. The -n option sets the number of iterations to run. There is no -t or -f option for top.

45.  B. The ps -e command is used to display all processes, and the -o option configures the columns to display.

46.  A. The grep command will be used for this purpose. Note the difference between grep -r and grep -ri. The question did not ask for case insensitivity, and therefore the use of -i in option B makes it incorrect.

47.  B. The find command will be used for this purpose. Setting the directory from which to begin the find is required, along with the expression, which in this case, are files beginning with DB.

48.  B. Load average information is gathered from /proc/loadavg, whereas uptime information is stored on /proc/uptime.

49.  D. Interactive repair is the default, so no option is required. The -f option forces the operation, and -y and -a are both variations of noninteractive repair.

50.  D. The /etc/mtab file is updated dynamically as filesystems are mounted and unmounted. The /etc/fstab file is not dynamically updated.

51.  B. The -B option changes the format, and T sets the scale to terabytes. The -T option alone prints the filesystem type. The other options do not exist.

52.  A. The e2image program can be used to create an image of metadata that can help with drive recovery. The resulting image file can be used with programs like dumpe2fs and debugfs.

53.  C. The -c option checks for bad blocks. The -b option sets the block size. There is no -a or -d option.

54.  B. The chown command is used for this purpose and can be used to set both the user and group for ownership.

55.  A. The ssh-keyscan command can be used for the purpose described and can help with virtual machine deployment by obtaining the SSH host key and adding it to the known_hosts file.

56.  C. The GRUB_RECORDFAIL_TIMEOUT option is used to configure the behavior of the system in the event of a failed boot. Setting the value to -1 will display the GRUB menu and not continue booting. Setting the value to 0 will cause the menu to not display. Setting to a value greater than or equal to 1 will cause the menu to display for that many seconds.

57.  A. The -s option displays a summary, and -h displays it in a human-readable format.

58.  D. The -L option tells find to follow symlinks. The -H and -P options are both variations to tell find not to follow symlinks, and the -S option does not exist.

59.  A. The -a option appends to the file rather than overwriting when using tee. The other options do not fulfill the needs of the problem statement.

60.  C. The /etc directory and its subdirectories typically contain configuration files that would be necessary in order to re-create the system in a restoration scenario. The /var directory usually contains variable information, whereas /opt may be used for several other purposes. The /bin directory contains binaries that can usually be reinstalled.

## Chapter 12: Practice Exam 2

1.  A. The /etc/hosts.deny file is part of TCP wrappers along with /etc/hosts.allow. Both provide a basic mechanism for configuration of access from remote hosts to network services.

2.  C. The alias command uses the alias name followed by an equal sign followed by the command to be aliased. In this case, because the command to be aliased contains spaces, it needs to be contained in quotation marks.

3.  C. Shell scripting syntax uses the format shown, with square brackets around the condition to the tested and double-equal signs for a string test. Variables are preceded by a dollar sign as shown.

4.  A. The export command is necessary so that any variables that are manually defined in your current session become available to child processes. The source command executes the file and can be used for the purpose described but requires an additional argument. The let and def commands are not valid.

5.  C. The source command is the functional equivalent of a single dot (.). The set command exists but is not used for this purpose. The other commands are not valid.

6.  A. The syntax for setting the PATH separates the new path with a colon, as shown in the correct option. A primary difference between the correct and incorrect options for this question was in how the actual specified path was shown.

7.  A. The correct syntax is as shown. Note that a semicolon is required when the commands are included on one line, as displayed in the answer.

8.  C. The mail command with -s for the subject is necessary, followed by the email address for the mail. Then, input is redirected to the mail command using /etc/hostname.

9.  C. The /etc/skel directory contains files that are a skeleton of a user’s home directory when their account is created. The other directories listed do not exist by default.

10.  D. The Universal Access section, which can be found by typing **Universal Access** from within an Ubuntu GUI interface, enables configuration of accessibility options.

11.  B. The kbdrate command is used for the purpose described and can help with accessibility. The other commands shown are not valid.

12.  A. The DISPLAY variable controls the destination and screen for displaying GUI applications. Setting this variable facilitates forwarding of X applications over ssh.

13.  B. The xhost command is used to control who can make connections for both users and hosts to a given X server. The other commands are not valid.

14.  B. The -f option sets the days between expiration and disabled for an account. The -g option is used to set the group ID, whereas -e is used to set the overall expiration date.

15.  A. The getent command can be used for the purpose described and will display the aliases on the server by examining the aliases database. The other commands are not valid and, in the case of the mail command shown, will simply attempt to send mail to an address known as aliases.

16.  C. The ALL: ALL syntax will cause all hosts to be denied. This means that you must explicitly authorize hosts and networks using /etc/hosts.allow.

17.  B. The current at jobs for all users are shown when atq is executed as superuser.

18.  C. The -r option to the crontab command removes all cron entries for a given user. The -l option lists cron jobs, whereas the -e option edits the crontab. There is no -d option.

19.  A. The -u option specifies the user. The -l option lists the cron jobs and -e edits them. There is no -d or -m option.

20.  A. The userdel command, given no other options, does not delete the home directory. When given the -r option, the command will delete the home directory and mail spool file. There is no -h or -p option for the userdel command.

21.  D. The -gid option is used to specify group ownership for the find command. The -group option does exist, but since the question specified that the group had already been deleted, the gid must be used instead. There is a -name option, but it searches by name and not group ID.

22.  B. The groupmod command will be used for this purpose, and the -n option followed by the new group name is used to change the name. There is no groupchg command.

23.  D. The journalctl command is used to view and parse log file entries on systemd-based systems that maintain logs in a special format. The logger command can be used to create log entries, and the other commands shown do not exist.

24.  A. The -o option followed by either 1 or 2 enables ntpdate compatibility with older NTP servers. The default, when no -o option is specified, is version 3\. The -v option tells ntpdate to be verbose, whereas the -e option sets the authentication timeout.

25.  D. The /var/log/journal directory is used to store journal log files for systemd-based systems. The other directories do not exist by default.

26.  C. The -m option sets the mail program to use when mailing logs. It is set to /usr/bin/mail -s by default. There is no -o option, and -v is verbose. The -s option to the logrotate command sets the state file to use.

27.  A. The -u option configures the output to UTC regardless of the time zone. The -s option sets the time, and there is no -v or -t option.

28.  D. The lprm command is used to remove print jobs on a system that uses the lp system for printing. There is no lpdel or rmprint command. There is an rm command, but it’s not used for working with print queues.

29.  D. The 255.255.254.0 subnet mask is equivalent to /23. The 255.255.255.0 subnet mask is /24. The subnet mask 255.255.255.255 is /32, and 255.255.0.0 is /16.

30.  A. The /etc/hosts file will be examined first, and then a Domain Name System (DNS) query will be sent based on the configuration shown.

31.  D. Standard LDAP traffic is TCP port 389 on the server. TCP port 25 is SMTP, 443 is HTTPS, and 143 is IMAP.

32.  C. The -l option to ssh changes the username sent for authentication. This can be useful for scripting scenarios where the @ notation cannot be used. The -v option is verbose mode, and -i is the identity file to use. There is no -u option.

33.  D. The -n option disables name resolution for addresses involved in the ping request/reply. The -D option returns a time stamp, whereas -d sets the SO_DEBUG option. Finally, -f is a flood ping.

34.  A. The ifconfig command shows various statistics about the interfaces on a Linux system, including whether the interface is up or down, its packets and bytes, queue length, and other information. The other commands listed do not exist.

35.  C. The -C option shows the SOA for each of the DNS name servers listed as authoritative for the domain. The -a option sends an ANY query, whereas -N sets the number of dots for the domain to be considered absolute. There is no -n option.

36.  A. The entire 127.0.0.0/8 range is available for local host addresses. Therefore, an answer would need to be in this range. The proper format for /etc/hosts is IP address followed by name, followed by optional aliases, which makes option A correct.

37.  C. The --ignore-errors option tells ifup to continue even if there are otherwise fatal errors. The -h option outputs help. There is no -C or --continue option.

38.  C. The -u option unlocks an account that was locked using the -l option. The -w option sets the warn days, and -S prints the status.

39.  C. When connecting to an alternate port, you can use the -p option to set the port or use a colon to separate the host from the port.

40.  B. The mailto configuration option sets the destination for emails related to sudo. The other options listed are not valid for sudo.

41.  B. The who command displays who is currently logged in and the date and time they logged in. The whois command displays information about domains. The other commands are not valid.

42.  C. Port 123 is used for NTP communication by default. Port 161 is SNMP, 139 is NetBIOS, and 194 is IRC.

43.  D. A UDP scan can be initiated with -sU. A scan of -sT is a normal TCP scan, and -sS is a SYN scan. There is no -sP option.

44.  B. The +D option is used to search an entire directory tree for files that are open by processes. The -d option does essentially the same thing but does not go into subdirectories. The -f option is typically used in combination with other options to control path name interpretation. The -i option lists files or processes with open ports.

45.  C. The -r option causes the ip command to attempt to resolve IP addresses. The -f option specifies the protocol family. There is no -n or -a option to the ip command.

46.  A. The ss command will be used, and when given the -o option, timer information is displayed. The netstat -rn command shows route information but not sockets or timing, and ping -f is a flood ping and not related. The ls -l command displays files in a long listing format.

47.  C. All of the addresses shown are in private ranges. The only one with the correct netmask is 255.255.255.0, which is equivalent to 24 masked bits.

48.  C. The !H sequence indicates host unreachable. Network unreachable is !N.

49.  D. There is no port for ICMP. The protocol itself does not use ports.

50.  B. The /etc/services file contains the port number to name translation for a given server. The file contains well-known ports and can be customized on a per-server basis.

51.  A. The command shown launches speech output for Orca. The other commands contain options that are invalid and thus will not work.

52.  A. The configuration files can be found in the /etc/lightdm hierarchy or in /usr/share/lightdm. The other directory locations do not exist by default.

53.  D. The xwininfo command is used to gather information about windows. The other commands shown are not valid.

54.  A. The tzconfig command can be used on a Debian system to set the time zone. The other commands listed do not exist.

55.  C. The locale command will be used for this purpose, and the -m option displays the available character maps. There is no charmap or mapinfo command.

56.  B. Time zone information is found within the /usr/share/zoneinfo hierarchy. The other directories listed do not typically exist by default.

57.  A. The default location on a Red Hat system is /var/lib/ntp/drift. The other locations shown do not exist by default. Within /etc/ntpd.conf, the location of the drift file can be changed with the driftfile option.

58.  C. The <<< character combination reads input from STDIN or standard input and uses it as the body of the message for the mail command.

59.  C. The groupdel command is used to remove a group from a system. No members of the group can remain or the command will fail.

60.  C. The lpr syslog facility sends messages from the lp subsystem to syslog. The auth facility is used for security-related messages. The other listed options are not syslog facilities.

# Index

## Numbers and Symbols

*   / filesystem, [200](#c11.xhtml_Page_200)
*   128-bit message digests, [60](#c03.xhtml_Page_60)

## A

*   acceleration, linear, input devices, [107](#c06.xhtml_Page_107)
*   AccelerationProfile, input devices, [107](#c06.xhtml_Page_107)
*   accessibility
    *   GRUB beep for input, [116](#c06.xhtml_Page_116)
    *   key presses, [119](#c06.xhtml_Page_119)
    *   legacy utilities, [111](#c06.xhtml_Page_111)
    *   Orca, [112](#c06.xhtml_Page_112)
    *   screen magnifier, [116](#c06.xhtml_Page_116)
    *   speech recognition, KDE, [114](#c06.xhtml_Page_114)
    *   Ubuntu, [209](#c12.xhtml_Page_209)
*   account information, [178](#c10.xhtml_Page_178)
*   accounts
    *   disabled, [210](#c12.xhtml_Page_210)
    *   expiring, [182](#c10.xhtml_Page_182)
    *   locking, [185](#c10.xhtml_Page_185)
    *   unlocking, [191](#c10.xhtml_Page_191), [214](#c12.xhtml_Page_214)
*   addresses
    *   IPv6, [161](#c09.xhtml_Page_161), [170](#c09.xhtml_Page_170)
    *   local, IPv6 pings, [165](#c09.xhtml_Page_165)
    *   private, internal use, [160](#c09.xhtml_Page_160)
*   administrative tasks, [124](#c07.xhtml_Page_124)–138, [257](#a01.xhtml_Page_257)–263
*   aliased commands, [90](#c05.xhtml_Page_90)
*   aliases, missing, [98](#c05.xhtml_Page_98)
*   anacron, [129](#c07.xhtml_Page_129)
*   Apache, /var/log/httpd/access.log, [53](#c03.xhtml_Page_53)
*   appending files, [61](#c03.xhtml_Page_61)
    *   tee, [205](#c11.xhtml_Page_205)
*   applications, containerization *versus* virtualization, [35](#c02.xhtml_Page_35)
*   apt-cache, Debian, package lists, [38](#c02.xhtml_Page_38)
*   architecture, system, [3](#c01.xhtml_Page_3)–20, [220](#a01.xhtml_Page_220)–226
*   ARP, disabling, [170](#c09.xhtml_Page_170)
*   arp, IP address-to-Mac address pair, [168](#c09.xhtml_Page_168)
*   arrays, Bash script, [91](#c05.xhtml_Page_91)
*   assistive technology, [110](#c06.xhtml_Page_110), [115](#c06.xhtml_Page_115)–116
*   at
    *   job creation, [133](#c07.xhtml_Page_133), [138](#c07.xhtml_Page_138)
    *   job deletion, [132](#c07.xhtml_Page_132)
*   atq, as root, [210](#c12.xhtml_Page_210)
*   authentication
    *   disabling, [113](#c06.xhtml_Page_113)
    *   Spice, disable, [113](#c06.xhtml_Page_113)
    *   ssh, [179](#c10.xhtml_Page_179), [184](#c10.xhtml_Page_184)
*   autofs, configuration files, default, [72](#c04.xhtml_Page_72)

## B

*   backups, [205](#c11.xhtml_Page_205)
*   Bash, [54](#c03.xhtml_Page_54)
    *   bash function, [97](#c05.xhtml_Page_97)
    *   command history, [53](#c03.xhtml_Page_53)
    *   command substitution, [93](#c05.xhtml_Page_93)
    *   configuration files, locating on login, [88](#c05.xhtml_Page_88)
    *   environment settings, [47](#c03.xhtml_Page_47)
    *   executing commands, [87](#c05.xhtml_Page_87)
    *   file overwrite, preventing, [47](#c03.xhtml_Page_47)
    *   if conditionals, [88](#c05.xhtml_Page_88)
    *   initialization files, no reading, [91](#c05.xhtml_Page_91)
    *   logout, command execution, [87](#c05.xhtml_Page_87)
    *   output, redirect, [47](#c03.xhtml_Page_47)
    *   printing, list of numbers, [88](#c05.xhtml_Page_88)
    *   quotes, [57](#c03.xhtml_Page_57)
    *   reading commands, [87](#c05.xhtml_Page_87)
    *   sayHello function, [209](#c12.xhtml_Page_209)
    *   scripts, command-line parameters, [88](#c05.xhtml_Page_88)
    *   shell script, outputting name, [55](#c03.xhtml_Page_55)
    *   source built-in, [100](#c05.xhtml_Page_100)
    *   STDERR, redirecting, [52](#c03.xhtml_Page_52)
    *   STDOUT, redirecting, [52](#c03.xhtml_Page_52)
    *   umask setting, [79](#c04.xhtml_Page_79)
*   Bash scripts
    *   arrays, creating, [91](#c05.xhtml_Page_91)
    *   debugging, #! line, [96](#c05.xhtml_Page_96)
    *   division operator, [98](#c05.xhtml_Page_98)
    *   email, sending, [98](#c05.xhtml_Page_98)
    *   exit code, [95](#c05.xhtml_Page_95)
    *   find command, [96](#c05.xhtml_Page_96)
    *   functions, command sequence as, [89](#c05.xhtml_Page_89)
    *   greater than or equal to, [94](#c05.xhtml_Page_94)
    *   initialization, system wide, [94](#c05.xhtml_Page_94)
    *   keywords, [89](#c05.xhtml_Page_89), [95](#c05.xhtml_Page_95)
    *   loops, [100](#c05.xhtml_Page_100)
    *   output, [96](#c05.xhtml_Page_96)
    *   return values, testing, [95](#c05.xhtml_Page_95)
    *   terminating, [99](#c05.xhtml_Page_99)
    *   values, user entry, [96](#c05.xhtml_Page_96)
    *   variables, [95](#c05.xhtml_Page_95), [98](#c05.xhtml_Page_98), [208](#c12.xhtml_Page_208)
*   Bash shell
    *   invocation, file execution, [95](#c05.xhtml_Page_95)
    *   path, /srv/bin, [95](#c05.xhtml_Page_95)
    *   /user/local/lib, [28](#c02.xhtml_Page_28)
    *   /usr/local/bin, [100](#c05.xhtml_Page_100)
*   .bash_history, [201](#c11.xhtml_Page_201)
*   .bashrc, [201](#c11.xhtml_Page_201)
*   BIOS (basic input/output system)
    *   boot loader, disk location, [200](#c11.xhtml_Page_200)
    *   integrated peripherals, [20](#c01.xhtml_Page_20)
*   blocks, reserving, [77](#c04.xhtml_Page_77)
*   boot loaders, ISO9660 CD-ROMS, [14](#c01.xhtml_Page_14)
*   boot order, [14](#c01.xhtml_Page_14)
*   /boot partition
    *   /dev/sdal, [33](#c02.xhtml_Page_33)
    *   extlinux, [33](#c02.xhtml_Page_33)
*   booting
    *   configuration, /etc/default/grub, [29](#c02.xhtml_Page_29)
    *   GUI, disabling, [105](#c06.xhtml_Page_105)
    *   initramfs, [14](#c01.xhtml_Page_14)
    *   No init found, [14](#c01.xhtml_Page_14)
    *   reboot, [7](#c01.xhtml_Page_7)
    *   troubleshooting, kernel ring buffer and, [7](#c01.xhtml_Page_7)
*   bootstrapping, [205](#c11.xhtml_Page_205)
*   Braille display, [107](#c06.xhtml_Page_107)
    *   Orca, [116](#c06.xhtml_Page_116)
*   btrfs subvolume, [75](#c04.xhtml_Page_75)–76
*   built-in commands, listing read-only variables, [91](#c05.xhtml_Page_91)
*   bunzip2, [61](#c03.xhtml_Page_61)
*   bzip2, archive, sending to STDOUT, [56](#c03.xhtml_Page_56)

## C

*   case statement, [92](#c05.xhtml_Page_92)–93
*   CentOS
    *   groups, deleting, [217](#c12.xhtml_Page_217)
    *   packages, [37](#c02.xhtml_Page_37), [39](#c02.xhtml_Page_39)
*   CentOS 6, RAM disk creation, [12](#c01.xhtml_Page_12)
*   change, password changes, [191](#c10.xhtml_Page_191)
*   character maps, [217](#c12.xhtml_Page_217)
*   character sets, [125](#c07.xhtml_Page_125)
*   characters
    *   commands as function, Bash script, [89](#c05.xhtml_Page_89)
    *   multibyte representation, [126](#c07.xhtml_Page_126)
    *   sequence, alternate command, [89](#c05.xhtml_Page_89)
*   child processes, variables, [208](#c12.xhtml_Page_208)
*   chmod
    *   execute permission, [97](#c05.xhtml_Page_97)
    *   minimum privileges, [90](#c05.xhtml_Page_90)
*   chown, recursive change, [71](#c04.xhtml_Page_71)
*   Chrony package, [152](#c08.xhtml_Page_152)
*   chronyd, status, [156](#c08.xhtml_Page_156)
*   CIDR (Classless Inter-Domain Routing), subnets
    *   netmasks, [163](#c09.xhtml_Page_163)
    *   splitting, [161](#c09.xhtml_Page_161)
*   clock, hardware, [143](#c08.xhtml_Page_143)
*   command-line
    *   date, [143](#c08.xhtml_Page_143)
    *   parameters, Bash script, [88](#c05.xhtml_Page_88)
*   commands. *See also* specific commands
    *   aliased, removing, [90](#c05.xhtml_Page_90)
    *   executing two, [89](#c05.xhtml_Page_89)
    *   foreground processing, [50](#c03.xhtml_Page_50)
    *   history, [53](#c03.xhtml_Page_53)
    *   libraries, [29](#c02.xhtml_Page_29)
    *   locating elements, [69](#c04.xhtml_Page_69)
    *   paths, [61](#c03.xhtml_Page_61)
    *   return value test, [97](#c05.xhtml_Page_97)
    *   scheduling execution, [125](#c07.xhtml_Page_125)
    *   types, [57](#c03.xhtml_Page_57)
*   compression, [59](#c03.xhtml_Page_59)
    *   decompressing files, [53](#c03.xhtml_Page_53)
    *   log files, disabling, [149](#c08.xhtml_Page_149)
*   configuration
    *   booting, [29](#c02.xhtml_Page_29)
    *   CUPS, [142](#c08.xhtml_Page_142)
    *   devices, udev, [6](#c01.xhtml_Page_6)
    *   /etc/hosts, [164](#c09.xhtml_Page_164)
    *   Ethernet devices, [173](#c09.xhtml_Page_173)
    *   files
        *   autofs, [72](#c04.xhtml_Page_72)
        *   Bash, [86](#c05.xhtml_Page_86)
        *   Chrony, [152](#c08.xhtml_Page_152)
        *   locating on login, Bash, [88](#c05.xhtml_Page_88)
        *   logrotate, [156](#c08.xhtml_Page_156)
        *   modprobe, [196](#c11.xhtml_Page_196)
        *   priority order, [72](#c04.xhtml_Page_72)
        *   systemd, [8](#c01.xhtml_Page_8), [72](#c04.xhtml_Page_72)
        *   Upstart, [9](#c01.xhtml_Page_9)
        *   X clients, [107](#c06.xhtml_Page_107)
        *   XDMCP, [118](#c06.xhtml_Page_118)
        *   yum, [36](#c02.xhtml_Page_36)
    *   GRUB 2, [26](#c02.xhtml_Page_26), [201](#c11.xhtml_Page_201)
    *   IPv6, [166](#c09.xhtml_Page_166)
    *   kernel, [13](#c01.xhtml_Page_13)
    *   LightDM, [105](#c06.xhtml_Page_105), [111](#c06.xhtml_Page_111), [216](#c12.xhtml_Page_216)
    *   modprobe, [196](#c11.xhtml_Page_196)
    *   persistent, [157](#c09.xhtml_Page_157)–174, [270](#a01.xhtml_Page_270)–277
    *   SSH custom client, [189](#c10.xhtml_Page_189)
    *   systemd, [13](#c01.xhtml_Page_13), [15](#c01.xhtml_Page_15)
    *   udev, [6](#c01.xhtml_Page_6)
    *   UEFI (Unified Extensible Firmware Interface), [15](#c01.xhtml_Page_15)
    *   Weston, [115](#c06.xhtml_Page_115)
    *   Wi-Fi devices, [173](#c09.xhtml_Page_173)
    *   X, [107](#c06.xhtml_Page_107), [112](#c06.xhtml_Page_112), [113](#c06.xhtml_Page_113)
*   connectivity
    *   testing, TCP level, [170](#c09.xhtml_Page_170)
    *   troubleshooting, [167](#c09.xhtml_Page_167)
*   copying
    *   directories, recursive, [49](#c03.xhtml_Page_49)
    *   files, at user creation, [90](#c05.xhtml_Page_90)
*   copy-on-write, [73](#c04.xhtml_Page_73)
*   cp, [202](#c11.xhtml_Page_202)
    *   confirmation, [100](#c05.xhtml_Page_100)
    *   directories, copying recursively, [49](#c03.xhtml_Page_49)
    *   file overwrite, [49](#c03.xhtml_Page_49)
*   cpio, [56](#c03.xhtml_Page_56)
*   CPU time, displaying, [180](#c10.xhtml_Page_180)
*   cron, [124](#c07.xhtml_Page_124)
    *   jobs, [132](#c07.xhtml_Page_132), [210](#c12.xhtml_Page_210)
    *   restart, [137](#c07.xhtml_Page_137)
    *   scheduled jobs, [126](#c07.xhtml_Page_126)
    *   user listing, [134](#c07.xhtml_Page_134)
*   crontab, [210](#c12.xhtml_Page_210)
    *   other users, [211](#c12.xhtml_Page_211)
    *   removing, [136](#c07.xhtml_Page_136)
*   CUPS (Common UNIX Printing System)
    *   configuration files, [142](#c08.xhtml_Page_142)
    *   daemon, listening on port 631, [150](#c08.xhtml_Page_150)
    *   default local printer configuration, [155](#c08.xhtml_Page_155)
    *   default port, [145](#c08.xhtml_Page_145)
    *   print jobs, completed, viewing, [146](#c08.xhtml_Page_146)
    *   print sharing, [149](#c08.xhtml_Page_149)
    *   restarting, [149](#c08.xhtml_Page_149)
*   currency-related localization, [132](#c07.xhtml_Page_132)
*   cut, delimiters, default, [50](#c03.xhtml_Page_50)

## D

*   data, writing to disk, [74](#c04.xhtml_Page_74)
*   databases
    *   hosts, enumerating, [163](#c09.xhtml_Page_163)
    *   updates, [71](#c04.xhtml_Page_71)
*   date
    *   command line, [143](#c08.xhtml_Page_143)
    *   current, [125](#c07.xhtml_Page_125)
    *   environment variables, [126](#c07.xhtml_Page_126)
    *   setting, [153](#c08.xhtml_Page_153)
*   date, date/time set, [153](#c08.xhtml_Page_153)
*   DATE variable, shell script, [92](#c05.xhtml_Page_92)
*   dbus, communication, monitoring, [197](#c11.xhtml_Page_197)
*   D-Bus, machine ID, [38](#c02.xhtml_Page_38)
*   Debian
    *   packages, [30](#c02.xhtml_Page_30)–32, [33](#c02.xhtml_Page_33), [36](#c02.xhtml_Page_36), [38](#c02.xhtml_Page_38), [198](#c11.xhtml_Page_198)–199
    *   reconfiguration, [31](#c02.xhtml_Page_31)
    *   services, starting/stopping, [185](#c10.xhtml_Page_185)
    *   source repository, [198](#c11.xhtml_Page_198)
    *   startup scripts, [20](#c01.xhtml_Page_20)
    *   time zones, [133](#c07.xhtml_Page_133), [216](#c12.xhtml_Page_216)
    *   updates, [27](#c02.xhtml_Page_27)
    *   zsh package, [28](#c02.xhtml_Page_28)
*   debugfs, [74](#c04.xhtml_Page_74)
*   debugging
    *   /etc/resolv.conf and, [172](#c09.xhtml_Page_172)
    *   messages, journalctl, [149](#c08.xhtml_Page_149)
    *   slapd, [132](#c07.xhtml_Page_132)
    *   XFS filesystem, [78](#c04.xhtml_Page_78)
*   declare, [91](#c05.xhtml_Page_91), [93](#c05.xhtml_Page_93)
*   decompressing files, [53](#c03.xhtml_Page_53), [60](#c03.xhtml_Page_60)
*   default gateway, changing, [164](#c09.xhtml_Page_164)
*   desktop, [113](#c06.xhtml_Page_113), [251](#a01.xhtml_Page_251)–257
*   devices, [63](#c04.xhtml_Page_63)–81
    *   answers to review questions, [239](#a01.xhtml_Page_239)–245
    *   drivers, lsmod output, [11](#c01.xhtml_Page_11)
    *   empty, [78](#c04.xhtml_Page_78)
    *   filters, vgscan, [39](#c02.xhtml_Page_39)
    *   hotplug, udevadm commands, [6](#c01.xhtml_Page_6)
    *   input, acceleration, [107](#c06.xhtml_Page_107)
    *   NVMe-based, [18](#c01.xhtml_Page_18)
    *   USB, listing, [6](#c01.xhtml_Page_6)
    *   wireless, parameters, [168](#c09.xhtml_Page_168)
*   /dev/sdal, /boot partition, [33](#c02.xhtml_Page_33)
*   df, [79](#c04.xhtml_Page_79), [204](#c11.xhtml_Page_204)
*   DHCP, activity, [171](#c09.xhtml_Page_171)
*   dig, [162](#c09.xhtml_Page_162), [172](#c09.xhtml_Page_172), [173](#c09.xhtml_Page_173)
*   directories
    *   backups, user home, [37](#c02.xhtml_Page_37)
    *   changes, tilde character and environment variable, [92](#c05.xhtml_Page_92)
    *   copying recursively, [49](#c03.xhtml_Page_49)
    *   FHS, local binaries, [99](#c05.xhtml_Page_99)
    *   files, coping, [209](#c12.xhtml_Page_209)
    *   finding, [48](#c03.xhtml_Page_48)
    *   ldconfig, command-line, [38](#c02.xhtml_Page_38)
    *   printing, [54](#c03.xhtml_Page_54), [199](#c11.xhtml_Page_199)
    *   removing, [48](#c03.xhtml_Page_48)
    *   root user, home directory, [27](#c02.xhtml_Page_27)
    *   skeleton home directory, [136](#c07.xhtml_Page_136)
    *   system log, [155](#c08.xhtml_Page_155)
    *   time zones, [217](#c12.xhtml_Page_217)
    *   useradd, [128](#c07.xhtml_Page_128)
    *   users, changing, [130](#c07.xhtml_Page_130)
*   display
    *   accessibility, Orca, [112](#c06.xhtml_Page_112)
    *   assistive technology, [110](#c06.xhtml_Page_110)
    *   Braille, [107](#c06.xhtml_Page_107), [116](#c06.xhtml_Page_116)
    *   fonts, [107](#c06.xhtml_Page_107), [110](#c06.xhtml_Page_110)
    *   fonts.scale, [112](#c06.xhtml_Page_112)
    *   GDM (GNOME Display Manager), welcome message, [105](#c06.xhtml_Page_105)
    *   GNOME, [106](#c06.xhtml_Page_106), [108](#c06.xhtml_Page_108), [109](#c06.xhtml_Page_109), [114](#c06.xhtml_Page_114)
    *   GUI, boot disable, [105](#c06.xhtml_Page_105)
    *   inactivity timeout, [113](#c06.xhtml_Page_113)
    *   input devices, linear acceleration, [107](#c06.xhtml_Page_107)
    *   KDE, magnification, [108](#c06.xhtml_Page_108)
    *   LightDM, [105](#c06.xhtml_Page_105), [106](#c06.xhtml_Page_106), [110](#c06.xhtml_Page_110)
    *   monitor, [105](#c06.xhtml_Page_105), [106](#c06.xhtml_Page_106)
    *   mouse gestures, [108](#c06.xhtml_Page_108)
    *   RDP (Remote Desktop), server-side implementation, [114](#c06.xhtml_Page_114)
    *   screen magnifier, [116](#c06.xhtml_Page_116)
    *   video cards, RAM, [112](#c06.xhtml_Page_112)
    *   X
        *   authority files, [108](#c06.xhtml_Page_108)
        *   local client, [111](#c06.xhtml_Page_111)
        *   monitor vertical refresh, [107](#c06.xhtml_Page_107)
        *   window information, [109](#c06.xhtml_Page_109)
    *   X Display Manager, login, [116](#c06.xhtml_Page_116)
    *   X session
        *   information, [115](#c06.xhtml_Page_115)
        *   pointer keys, [114](#c06.xhtml_Page_114)
        *   terminal device width, [111](#c06.xhtml_Page_111)
    *   xauth authority file, [110](#c06.xhtml_Page_110)
    *   XFree86, hardware query, [106](#c06.xhtml_Page_106)
    *   xfwm4 window manager, [113](#c06.xhtml_Page_113)
    *   xorg.conf
        *   blank mode, [109](#c06.xhtml_Page_109)
        *   video mode changes, [108](#c06.xhtml_Page_108)
*   division operator, Bash script, [98](#c05.xhtml_Page_98)
*   dmesg, time, [196](#c11.xhtml_Page_196)
*   DNS (Domain Name System)
    *   default route, [160](#c09.xhtml_Page_160)
    *   lookups, overriding, [166](#c09.xhtml_Page_166)
    *   POP3 server specification, [173](#c09.xhtml_Page_173)
    *   setting, [163](#c09.xhtml_Page_163)
    *   SPF query, [167](#c09.xhtml_Page_167)
    *   systemd-resolved, [173](#c09.xhtml_Page_173)
*   documentation, access, [47](#c03.xhtml_Page_47)
*   domain names, [162](#c09.xhtml_Page_162)
*   DPMS (Display Power Management Signaling), [109](#c06.xhtml_Page_109), [113](#c06.xhtml_Page_113)
*   drift file, location, [144](#c08.xhtml_Page_144)
*   driftfile, [217](#c12.xhtml_Page_217)
*   du, printing, [205](#c11.xhtml_Page_205)
*   dumpe2fs, partition bad blocks, [73](#c04.xhtml_Page_73)

## E

*   e2fsck, superblocks, location, [79](#c04.xhtml_Page_79)
*   egrep, [52](#c03.xhtml_Page_52)
*   email. *See also* messages
    *   abuse account, [146](#c08.xhtml_Page_146)
    *   aliases, [210](#c12.xhtml_Page_210)
    *   forwarding, Procmail, [150](#c08.xhtml_Page_150)
    *   per-user forwarding, [153](#c08.xhtml_Page_153)
    *   processing statistics, [149](#c08.xhtml_Page_149)
    *   removing, [150](#c08.xhtml_Page_150)
    *   root user, [144](#c08.xhtml_Page_144), [209](#c12.xhtml_Page_209)
*   emulation, ping, [166](#c09.xhtml_Page_166)
*   encrypted files, gpg, [187](#c10.xhtml_Page_187)
*   encryption
    *   passwords, [131](#c07.xhtml_Page_131)
    *   remote desktop, [113](#c06.xhtml_Page_113)
*   env, [96](#c05.xhtml_Page_96)
*   environment, Bash, [47](#c03.xhtml_Page_47)
*   environment variables
    *   date format, [126](#c07.xhtml_Page_126)
    *   declaring, [55](#c03.xhtml_Page_55)
    *   directory change, tilde character and, [92](#c05.xhtml_Page_92)
    *   localization, [127](#c07.xhtml_Page_127)
    *   paper size, [135](#c07.xhtml_Page_135)
    *   PS1, [87](#c05.xhtml_Page_87)
    *   removing, [87](#c05.xhtml_Page_87)
    *   removing temporarily, [57](#c03.xhtml_Page_57)
    *   single-line viewing, [99](#c05.xhtml_Page_99)
    *   terminal device, X session, [111](#c06.xhtml_Page_111)
    *   text editors, [58](#c03.xhtml_Page_58)
    *   time format, [126](#c07.xhtml_Page_126)
    *   usernames, [99](#c05.xhtml_Page_99)
*   ESP (EFI system partition)
    *   filesystem mount, [26](#c02.xhtml_Page_26)
    *   format type, [33](#c02.xhtml_Page_33)
    *   grub-install, [38](#c02.xhtml_Page_38)
*   /etc/aliases, email messages, [150](#c08.xhtml_Page_150)
*   /etc/default/grub, [29](#c02.xhtml_Page_29), [32](#c02.xhtml_Page_32)
*   /etc/fstab, [72](#c04.xhtml_Page_72), [75](#c04.xhtml_Page_75), [81](#c04.xhtml_Page_81)
*   /etc/hosts, [164](#c09.xhtml_Page_164), [171](#c09.xhtml_Page_171)
*   /etc/hosts.allow, wildcards, [186](#c10.xhtml_Page_186)
*   /etc/inetd.conf, services, disabling, [184](#c10.xhtml_Page_184)
*   /etc/inittab, runlevel, single-user mode, [185](#c10.xhtml_Page_185)
*   /etc/localtime, directory listings, [151](#c08.xhtml_Page_151)
*   /etc/logrotate.conf, emailing log, [144](#c08.xhtml_Page_144)
*   /etc/ntp.conf, drift file, location, [144](#c08.xhtml_Page_144)
*   /etc/passwd, [49](#c03.xhtml_Page_49)
*   /etc/resolv.conf, debugging and, [172](#c09.xhtml_Page_172)
*   /etc/security/limits.conf, [182](#c10.xhtml_Page_182)
*   /etc/shadow, [183](#c10.xhtml_Page_183), [188](#c10.xhtml_Page_188)
*   /etc/sudoers, [214](#c12.xhtml_Page_214)
    *   admins group, [190](#c10.xhtml_Page_190)
    *   editing, [182](#c10.xhtml_Page_182)
    *   password prompt, [180](#c10.xhtml_Page_180)
*   /etc/X11/xorg.conf, [105](#c06.xhtml_Page_105)
*   /etc/yum.conf, kernel update, [32](#c02.xhtml_Page_32)
*   Ethernet, device configuration, [173](#c09.xhtml_Page_173)
*   event viewing, [6](#c01.xhtml_Page_6)
*   Exam 1, practice exam, [284](#a01.xhtml_Page_284)–288
*   Exam 101-500, practice exam, [288](#a01.xhtml_Page_288)–292
*   executable files, location, [67](#c04.xhtml_Page_67)
*   exFAT filesystem, formatting, [78](#c04.xhtml_Page_78)
*   Exim server
    *   mail delivery, [155](#c08.xhtml_Page_155)
    *   SMTP traffic and, [148](#c08.xhtml_Page_148)
*   expiration, removing, [124](#c07.xhtml_Page_124)
*   export
    *   names as functions, [94](#c05.xhtml_Page_94)
    *   variables, [101](#c05.xhtml_Page_101)
        *   removing, [97](#c05.xhtml_Page_97)
*   expressions, regular expressions, [59](#c03.xhtml_Page_59)
*   ext2 filesystem, [68](#c04.xhtml_Page_68)
    *   journal, adding, [76](#c04.xhtml_Page_76)
    *   superblock, corrupt, [79](#c04.xhtml_Page_79)
*   ext3 filesystem, [68](#c04.xhtml_Page_68)
    *   checking clean, [75](#c04.xhtml_Page_75)
    *   metadata image, [204](#c11.xhtml_Page_204)
    *   repairs, [204](#c11.xhtml_Page_204)
*   extlinux, installation, /boot partition, [33](#c02.xhtml_Page_33)

## F

*   FAT (File Allocation Table)
    *   formatting, [76](#c04.xhtml_Page_76)
    *   rescue disks, boot loader, [13](#c01.xhtml_Page_13)
*   Fedora 22, packages, installation, [37](#c02.xhtml_Page_37)
*   fgrep, [59](#c03.xhtml_Page_59)
*   FHS (filesystem hierarchy standard), [69](#c04.xhtml_Page_69)–70, [99](#c05.xhtml_Page_99)
*   Fibre Channel, [17](#c01.xhtml_Page_17)
*   file compression, [53](#c03.xhtml_Page_53), [59](#c03.xhtml_Page_59), [60](#c03.xhtml_Page_60)
*   file dumps, maximum file size, [75](#c04.xhtml_Page_75)
*   file tests, [95](#c05.xhtml_Page_95)
    *   operator, [98](#c05.xhtml_Page_98)–100
*   $FILEPATH variable, [92](#c05.xhtml_Page_92)
*   files
    *   appending, [61](#c03.xhtml_Page_61)
    *   binary mode, [58](#c03.xhtml_Page_58)
    *   content search, [203](#c11.xhtml_Page_203)
    *   copying, [90](#c05.xhtml_Page_90), [209](#c12.xhtml_Page_209)
    *   decompressing, [53](#c03.xhtml_Page_53)
    *   existence, testing, [93](#c05.xhtml_Page_93)
    *   extracting, [50](#c03.xhtml_Page_50)
    *   group information, [126](#c07.xhtml_Page_126)
    *   gzip, [50](#c03.xhtml_Page_50)
    *   initialization, no reading, [91](#c05.xhtml_Page_91)
    *   line numbers, prepending, [53](#c03.xhtml_Page_53)
    *   listing, [56](#c03.xhtml_Page_56)
    *   moving, [54](#c03.xhtml_Page_54)
    *   open, listing, [186](#c10.xhtml_Page_186)
    *   overwriting, confirmation, [100](#c05.xhtml_Page_100)
    *   ownership, [68](#c04.xhtml_Page_68), [204](#c11.xhtml_Page_204)
    *   passwords, [125](#c07.xhtml_Page_125)
    *   removing, [55](#c03.xhtml_Page_55)
    *   removing lines, [60](#c03.xhtml_Page_60)
    *   searches, backward, [55](#c03.xhtml_Page_55)
    *   size, [55](#c03.xhtml_Page_55), [190](#c10.xhtml_Page_190)
    *   splitting, [60](#c03.xhtml_Page_60)
    *   tar, [50](#c03.xhtml_Page_50)
    *   UID, [125](#c07.xhtml_Page_125)
    *   usernames, [125](#c07.xhtml_Page_125)
    *   users, deleted, [79](#c04.xhtml_Page_79)
*   filesystems
    *   copy-on-write, [73](#c04.xhtml_Page_73)
    *   creating, bad blocks, [204](#c11.xhtml_Page_204)
    *   disk space, [70](#c04.xhtml_Page_70)
    *   ext2, [68](#c04.xhtml_Page_68)
    *   ext3, [68](#c04.xhtml_Page_68)
    *   extensions, missing, [49](#c03.xhtml_Page_49)
    *   hierarchy, [63](#c04.xhtml_Page_63)–81, [239](#a01.xhtml_Page_239)–245
    *   information, [70](#c04.xhtml_Page_70)
    *   inodes, [68](#c04.xhtml_Page_68)
    *   ISO, creating, [72](#c04.xhtml_Page_72)
    *   Linux, [63](#c04.xhtml_Page_63)–81
    *   listing currently mounted, [34](#c02.xhtml_Page_34)
    *   mounted, [204](#c11.xhtml_Page_204)
    *   mounting, [69](#c04.xhtml_Page_69), [70](#c04.xhtml_Page_70), [71](#c04.xhtml_Page_71), [77](#c04.xhtml_Page_77)
    *   overwriting, [49](#c03.xhtml_Page_49)
    *   processes, running, [196](#c11.xhtml_Page_196)
    *   read-write mode, [74](#c04.xhtml_Page_74)
    *   ro, [73](#c04.xhtml_Page_73)
    *   sticky bits, [69](#c04.xhtml_Page_69)
    *   type, mke2fs, [72](#c04.xhtml_Page_72)
    *   unmounting, [74](#c04.xhtml_Page_74), [178](#c10.xhtml_Page_178)
    *   verifying, [74](#c04.xhtml_Page_74)
    *   xfs_check, [74](#c04.xhtml_Page_74)
*   find, [54](#c03.xhtml_Page_54), [81](#c04.xhtml_Page_81), [97](#c05.xhtml_Page_97), [99](#c05.xhtml_Page_99), [205](#c11.xhtml_Page_205)
*   firewalls
    *   ports, [160](#c09.xhtml_Page_160), [214](#c12.xhtml_Page_214)
    *   protocols, [160](#c09.xhtml_Page_160)
*   fonts, X.org, [107](#c06.xhtml_Page_107)
*   fonts.scale, [112](#c06.xhtml_Page_112)
*   for loops, [90](#c05.xhtml_Page_90), [93](#c05.xhtml_Page_93)
*   foreground processing, [50](#c03.xhtml_Page_50), [51](#c03.xhtml_Page_51)
*   fsck, [68](#c04.xhtml_Page_68), [72](#c04.xhtml_Page_72), [204](#c11.xhtml_Page_204)

## G

*   gateways, default, [160](#c09.xhtml_Page_160), [164](#c09.xhtml_Page_164)
*   GDM (GNOME Display Manager)
    *   greeter, welcome message, [105](#c06.xhtml_Page_105)
    *   login window options, [118](#c06.xhtml_Page_118)
    *   welcome message, [105](#c06.xhtml_Page_105)
*   getent, password database, [136](#c07.xhtml_Page_136)
*   GIDs, UIDs and, [130](#c07.xhtml_Page_130)
*   GNOME
    *   GOK (GNOME On-Screen Keyboard), [109](#c06.xhtml_Page_109)
    *   high-contrast theme, [108](#c06.xhtml_Page_108)
    *   on-screen keyboard, [119](#c06.xhtml_Page_119)
    *   screen reader, [106](#c06.xhtml_Page_106), [109](#c06.xhtml_Page_109)
    *   slow keys, [114](#c06.xhtml_Page_114)
    *   sticky keys, [106](#c06.xhtml_Page_106)
*   GNU, commands, [41](#c03.xhtml_Page_41)–61
    *   answers to review questions, [233](#a01.xhtml_Page_233)–239
*   GnuPG
    *   key pair generation, [183](#c10.xhtml_Page_183)
    *   private keys, daemon process, [189](#c10.xhtml_Page_189)
*   GOK (GNOME On-Screen Keyboard), [109](#c06.xhtml_Page_109), [111](#c06.xhtml_Page_111)
*   gpg
    *   detached signatures, [188](#c10.xhtml_Page_188)
    *   encrypted files, [187](#c10.xhtml_Page_187)
    *   keys, sending to key server, [190](#c10.xhtml_Page_190)
    *   public keys, [185](#c10.xhtml_Page_185)
    *   signatures, generating, [183](#c10.xhtml_Page_183)
*   GPT disks
    *   formatting, [77](#c04.xhtml_Page_77)
    *   partitions, Linux, [37](#c02.xhtml_Page_37)
*   greater than or equal to operator, [94](#c05.xhtml_Page_94)
*   grep, [100](#c05.xhtml_Page_100), [174](#c09.xhtml_Page_174)
*   group ID, minimum group ID, [137](#c07.xhtml_Page_137)
*   group information, [126](#c07.xhtml_Page_126), [127](#c07.xhtml_Page_127)
*   group ownership of files, [68](#c04.xhtml_Page_68)
*   groupadd, [135](#c07.xhtml_Page_135), [137](#c07.xhtml_Page_137)
*   groupdel, [131](#c07.xhtml_Page_131)
*   groups
    *   changes, [126](#c07.xhtml_Page_126)
    *   names, [211](#c12.xhtml_Page_211)
*   GRUB
    *   beep for input, [116](#c06.xhtml_Page_116)
    *   *versus* GRUB 2, [36](#c02.xhtml_Page_36)
    *   images, alternate directory, [34](#c02.xhtml_Page_34)
    *   MBR, SATA disk, [30](#c02.xhtml_Page_30)
    *   menu display, [25](#c02.xhtml_Page_25)
    *   operating system, default boot, [32](#c02.xhtml_Page_32)
    *   parameters, editing, [16](#c01.xhtml_Page_16)
    *   partitions, [25](#c02.xhtml_Page_25)
    *   ro option, [29](#c02.xhtml_Page_29)
    *   single-user mode, [25](#c02.xhtml_Page_25)
    *   timeout, setting, [28](#c02.xhtml_Page_28)
*   GRUB Legacy
    *   dual-boot option, [27](#c02.xhtml_Page_27)
    *   hd(0,0), [33](#c02.xhtml_Page_33)
    *   kernel options, [25](#c02.xhtml_Page_25)
    *   non-Linux kernel, [26](#c02.xhtml_Page_26)
*   GRUB2
    *   configuration changes, [201](#c11.xhtml_Page_201)
    *   configuration file, [26](#c02.xhtml_Page_26)
    *   *versus* GRUB, [36](#c02.xhtml_Page_36)
*   grub-install, [34](#c02.xhtml_Page_34)
    *   boot images, [201](#c11.xhtml_Page_201)
*   grub-mkconfig, [200](#c11.xhtml_Page_200)
    *   file output, [29](#c02.xhtml_Page_29)
*   GUI (graphical user interface)
    *   applications, screen, [209](#c12.xhtml_Page_209)
    *   boot disable, [105](#c06.xhtml_Page_105)
*   .gz extension, [55](#c03.xhtml_Page_55)
*   gzip files, [50](#c03.xhtml_Page_50)

## H

*   handshakes, three-way, [167](#c09.xhtml_Page_167)
*   hardware, clock
    *   system time, [145](#c08.xhtml_Page_145)
    *   UTC, [146](#c08.xhtml_Page_146)
    *   working with, [143](#c08.xhtml_Page_143)
*   head, [48](#c03.xhtml_Page_48), [51](#c03.xhtml_Page_51)
*   /home/webfiles, [124](#c07.xhtml_Page_124)
*   host, [160](#c09.xhtml_Page_160), [172](#c09.xhtml_Page_172)
*   hostname
    *   boot and, [172](#c09.xhtml_Page_172)
    *   setting, [174](#c09.xhtml_Page_174)
*   hostname, programmatic functions, [171](#c09.xhtml_Page_171)
*   hosts
    *   blocking, TCP wrappers and, [208](#c12.xhtml_Page_208)
    *   storing, ssh keys, [182](#c10.xhtml_Page_182)
*   hosts database, enumerating, [163](#c09.xhtml_Page_163)
*   hotplug devices, udevadm commands, [6](#c01.xhtml_Page_6)
*   hwclock, system time, [145](#c08.xhtml_Page_145)

## I

*   IaaS (Infrastructure as a Service), performance, [36](#c02.xhtml_Page_36)
*   ICMP (Internet Control Message Protocol)
    *   echo requests, [216](#c12.xhtml_Page_216)
    *   packets, generating, interface, [161](#c09.xhtml_Page_161)
    *   ports, [164](#c09.xhtml_Page_164)
    *   requests for IPv6, [170](#c09.xhtml_Page_170)
*   iconv, [125](#c07.xhtml_Page_125)
*   if conditionals, Bash script, [88](#c05.xhtml_Page_88)
*   ifconfig, MTU, network interfaces and, [168](#c09.xhtml_Page_168)
*   ifup, [214](#c12.xhtml_Page_214)
*   IMAPS (IMAP over SSL), listening port, [174](#c09.xhtml_Page_174)
*   indexes, recreating, [130](#c07.xhtml_Page_130)
*   init, process IDs, [196](#c11.xhtml_Page_196)
*   initialization
    *   files, no reading, [91](#c05.xhtml_Page_91)
    *   xinit, [117](#c06.xhtml_Page_117)
*   initrd, filesystem, [16](#c01.xhtml_Page_16)
*   inodes, [68](#c04.xhtml_Page_68)
    *   usage information, [81](#c04.xhtml_Page_81)
*   input. *See also* assistive technology
    *   devices, acceleration, [107](#c06.xhtml_Page_107)
*   installation
    *   Fedora 22 system, [37](#c02.xhtml_Page_37)
    *   Linux, [21](#c02.xhtml_Page_21)–39, [226](#a01.xhtml_Page_226)–232
    *   rpm, [28](#c02.xhtml_Page_28)
    *   yum package, [27](#c02.xhtml_Page_27)
    *   zypper, [37](#c02.xhtml_Page_37)
*   interfaces, [105](#c06.xhtml_Page_105)–119
    *   answers to review questions, [251](#a01.xhtml_Page_251)–257
    *   auto, online, [161](#c09.xhtml_Page_161)
    *   displaying information, [160](#c09.xhtml_Page_160)
    *   selecting, [161](#c09.xhtml_Page_161)
*   interprocess communication service units, systemd, [188](#c10.xhtml_Page_188)
*   ip, [168](#c09.xhtml_Page_168), [174](#c09.xhtml_Page_174), [215](#c12.xhtml_Page_215)
*   IP addresses, availability, [167](#c09.xhtml_Page_167)
*   ip route change, [166](#c09.xhtml_Page_166)
*   iproute2, address changes, [173](#c09.xhtml_Page_173)
*   IPv4/ IPv6 comparison, [164](#c09.xhtml_Page_164)
*   IPv6
    *   addresses, [161](#c09.xhtml_Page_161), [170](#c09.xhtml_Page_170)
    *   configuration, [166](#c09.xhtml_Page_166)
    *   IPv4comparison, [164](#c09.xhtml_Page_164)
    *   pings, unique local address, [165](#c09.xhtml_Page_165)
    *   route traces, [172](#c09.xhtml_Page_172)
    *   traceroute, [162](#c09.xhtml_Page_162)
*   IRQ (interrupt request), assignments, viewing, [6](#c01.xhtml_Page_6)
*   ISO filesystem, creating, [72](#c04.xhtml_Page_72)
*   ISO9660 CD-ROMS, boot loader, [14](#c01.xhtml_Page_14)

## J

*   JAVA_PATH, [201](#c11.xhtml_Page_201)
*   job schedulers, [125](#c07.xhtml_Page_125), [126](#c07.xhtml_Page_126), [127](#c07.xhtml_Page_127), [128](#c07.xhtml_Page_128), [133](#c07.xhtml_Page_133), [136](#c07.xhtml_Page_136)
*   jobs, [56](#c03.xhtml_Page_56), [61](#c03.xhtml_Page_61)
*   journal logs, files, maximum size, [147](#c08.xhtml_Page_147)
*   journalctl, [149](#c08.xhtml_Page_149)
    *   filters, time-based, [154](#c08.xhtml_Page_154)
    *   journal data location, [155](#c08.xhtml_Page_155)
    *   journal data size, [153](#c08.xhtml_Page_153)
    *   kernel message queries, [152](#c08.xhtml_Page_152)
    *   logs, clearing, [150](#c08.xhtml_Page_150)
    *   maximum space, [154](#c08.xhtml_Page_154)
    *   new log entries, [147](#c08.xhtml_Page_147)
    *   service names, [153](#c08.xhtml_Page_153)
*   journald.conf, file size, [147](#c08.xhtml_Page_147)

## K

*   KDE
    *   magnification, [108](#c06.xhtml_Page_108)
    *   speech recognition, [114](#c06.xhtml_Page_114)
*   keepalive messages, [190](#c10.xhtml_Page_190)
*   kernel
    *   configuration information, [13](#c01.xhtml_Page_13)
    *   messages, [142](#c08.xhtml_Page_142), [152](#c08.xhtml_Page_152)
    *   modules, listing, [8](#c01.xhtml_Page_8)
    *   printing information, [47](#c03.xhtml_Page_47)
    *   ring buffer, [7](#c01.xhtml_Page_7), [9](#c01.xhtml_Page_9)
    *   symbols, files, [12](#c01.xhtml_Page_12)
    *   udev events, [6](#c01.xhtml_Page_6)
    *   updating, [32](#c02.xhtml_Page_32)
*   key pairs, [179](#c10.xhtml_Page_179), [183](#c10.xhtml_Page_183)
*   keyboard, [209](#c12.xhtml_Page_209)
*   keys, listing current, [181](#c10.xhtml_Page_181)
*   keywords, Bash scripts, [89](#c05.xhtml_Page_89), [95](#c05.xhtml_Page_95)
*   kill, [20](#c01.xhtml_Page_20), [51](#c03.xhtml_Page_51), [52](#c03.xhtml_Page_52), [57](#c03.xhtml_Page_57)
*   killing processes, [54](#c03.xhtml_Page_54)
*   klogd, logging messages, [145](#c08.xhtml_Page_145)

## L

*   LANG variable, [128](#c07.xhtml_Page_128)
*   last, recent login details, [184](#c10.xhtml_Page_184)
*   LDAP (Lightweight Directory Access Protocol), [213](#c12.xhtml_Page_213)
    *   entries, importing, [124](#c07.xhtml_Page_124)
    *   LDIF file, creating, [127](#c07.xhtml_Page_127)
    *   local files, lookups, [162](#c09.xhtml_Page_162)
    *   over SSL, listening, [133](#c07.xhtml_Page_133)
    *   user list, [127](#c07.xhtml_Page_127)
*   LDAP over SSL, port, [166](#c09.xhtml_Page_166)
*   ldconfig
    *   cache location, [198](#c11.xhtml_Page_198)
    *   directories, [35](#c02.xhtml_Page_35), [38](#c02.xhtml_Page_38)
    *   library path, directories, [35](#c02.xhtml_Page_35)
*   LDIF files, creating, [127](#c07.xhtml_Page_127)
*   libraries
    *   availability, [81](#c04.xhtml_Page_81)
    *   commands, [29](#c02.xhtml_Page_29)
    *   printing, [199](#c11.xhtml_Page_199)
    *   shared, [26](#c02.xhtml_Page_26)
    *   storage, [30](#c02.xhtml_Page_30)
*   libwrap, [191](#c10.xhtml_Page_191)
*   LightDM
    *   configuration, [105](#c06.xhtml_Page_105), [111](#c06.xhtml_Page_111), [216](#c12.xhtml_Page_216)
    *   guest login, [106](#c06.xhtml_Page_106)
    *   login, [111](#c06.xhtml_Page_111), [117](#c06.xhtml_Page_117)
    *   revert to terminal, [110](#c06.xhtml_Page_110)
    *   usernames, display, [117](#c06.xhtml_Page_117)
*   lightdm.conf, SeatDefaults section, [117](#c06.xhtml_Page_117)
*   line numbering, [201](#c11.xhtml_Page_201)
*   linear acceleration, input devices, [107](#c06.xhtml_Page_107)
*   link status, displaying, [168](#c09.xhtml_Page_168)
*   links, symbolic, [79](#c04.xhtml_Page_79)
*   Linux
    *   / filesystem, [200](#c11.xhtml_Page_200)
    *   /boot partition, size, [30](#c02.xhtml_Page_30)
    *   directory structure, [27](#c02.xhtml_Page_27)
    *   documentation, access, [47](#c03.xhtml_Page_47)
    *   filesystems, [63](#c04.xhtml_Page_63)–81, [239](#a01.xhtml_Page_239)–245
    *   GIDs, *versus* UIDs, [130](#c07.xhtml_Page_130)
    *   initialization, single-user mode, [7](#c01.xhtml_Page_7)
    *   installation, [21](#c02.xhtml_Page_21)–39, [226](#a01.xhtml_Page_226)–232
    *   package management, [21](#c02.xhtml_Page_21)–39, [226](#a01.xhtml_Page_226)–232
    *   partition, non-swap, [67](#c04.xhtml_Page_67)
    *   partition structure, [27](#c02.xhtml_Page_27)
    *   swap, [30](#c02.xhtml_Page_30)
    *   swap space, deactivating, [76](#c04.xhtml_Page_76)
    *   system logs, [155](#c08.xhtml_Page_155)
    *   time zones, [124](#c07.xhtml_Page_124), [143](#c08.xhtml_Page_143)
    *   UIDs, *versus* GIDs, [130](#c07.xhtml_Page_130)
*   ln, symlinks, [69](#c04.xhtml_Page_69)
*   load average
    *   determining, [51](#c03.xhtml_Page_51)
    *   uptime, [203](#c11.xhtml_Page_203)
*   loading, modules, [6](#c01.xhtml_Page_6)
*   locale
    *   currency-related, [132](#c07.xhtml_Page_132)
    *   LANG variable, [128](#c07.xhtml_Page_128)
    *   reconfiguring variables, [128](#c07.xhtml_Page_128)
*   locale, [134](#c07.xhtml_Page_134)
*   localhost, redirecting to, [166](#c09.xhtml_Page_166)
*   locate, [71](#c04.xhtml_Page_71), [80](#c04.xhtml_Page_80)
*   log files
    *   compression, disabling, [149](#c08.xhtml_Page_149)
    *   entries, parsing, [211](#c12.xhtml_Page_211)
    *   journal logs, maximum size, [147](#c08.xhtml_Page_147)
    *   journalctl, [150](#c08.xhtml_Page_150)
    *   rotation, configuring, [148](#c08.xhtml_Page_148)
    *   systemd, disk space used, [144](#c08.xhtml_Page_144)
*   log in
    *   automatic, LightDM, [111](#c06.xhtml_Page_111)
    *   message display, [18](#c01.xhtml_Page_18), [19](#c01.xhtml_Page_19)
    *   number logged, [191](#c10.xhtml_Page_191)
    *   number of, [182](#c10.xhtml_Page_182)
    *   password-based, [128](#c07.xhtml_Page_128)
    *   preventing temporarily, [178](#c10.xhtml_Page_178)
    *   users logged in, [180](#c10.xhtml_Page_180)
    *   X Display Manager, [116](#c06.xhtml_Page_116)
*   log zeroing, [77](#c04.xhtml_Page_77)
*   logging
    *   kernel messages, [142](#c08.xhtml_Page_142)
    *   messages, klogd, [145](#c08.xhtml_Page_145)
*   logical volumes, [18](#c01.xhtml_Page_18)
*   login name, changing, [189](#c10.xhtml_Page_189)
*   logout, command execution, Bash shell, [87](#c05.xhtml_Page_87)
*   logrotate, [142](#c08.xhtml_Page_142), [149](#c08.xhtml_Page_149), [156](#c08.xhtml_Page_156), [212](#c12.xhtml_Page_212)
*   logs, emailing, /etc/logrotate.conf, [144](#c08.xhtml_Page_144)
*   lookups, [162](#c09.xhtml_Page_162)
*   loops, [90](#c05.xhtml_Page_90), [100](#c05.xhtml_Page_100), [101](#c05.xhtml_Page_101)
*   ls, [48](#c03.xhtml_Page_48), [87](#c05.xhtml_Page_87)
*   ls -la, output, [67](#c04.xhtml_Page_67)
*   lsblk
    *   empty devices, [78](#c04.xhtml_Page_78)
    *   filesysem UUID, [80](#c04.xhtml_Page_80)
    *   partitions, [200](#c11.xhtml_Page_200)
*   lsof, instances, open, [215](#c12.xhtml_Page_215)
*   lspci, [8](#c01.xhtml_Page_8), [12](#c01.xhtml_Page_12)
*   LUN (logical unit number), [17](#c01.xhtml_Page_17)
*   lvchange, logical volume availability, [35](#c02.xhtml_Page_35)
*   LVM (Logical Volume Manager), [30](#c02.xhtml_Page_30), [31](#c02.xhtml_Page_31), [32](#c02.xhtml_Page_32), [34](#c02.xhtml_Page_34), [35](#c02.xhtml_Page_35)
*   .lzma extension, [53](#c03.xhtml_Page_53)

## M

*   MAC (Media Access Control), [168](#c09.xhtml_Page_168)
*   mail, [153](#c08.xhtml_Page_153), [155](#c08.xhtml_Page_155)
*   mail servers, querying for, [161](#c09.xhtml_Page_161)
*   man, [52](#c03.xhtml_Page_52)
*   man pages, [56](#c03.xhtml_Page_56), [59](#c03.xhtml_Page_59)
*   MBR partitioning system, [26](#c02.xhtml_Page_26), [30](#c02.xhtml_Page_30)
*   MBR-formatted disks, partition size, [77](#c04.xhtml_Page_77)
*   measurement, environment variables, [127](#c07.xhtml_Page_127)
*   /media/ mount point, [78](#c04.xhtml_Page_78)
*   memory
    *   displaying, [180](#c10.xhtml_Page_180)
    *   limits, [187](#c10.xhtml_Page_187)
    *   sockets, [168](#c09.xhtml_Page_168)
    *   usage, [50](#c03.xhtml_Page_50)
*   menu.lst, [29](#c02.xhtml_Page_29)
*   messages. *See also* email
    *   all users, [8](#c01.xhtml_Page_8)
    *   debugging, journalctl, [149](#c08.xhtml_Page_149)
    *   keepalive, [190](#c10.xhtml_Page_190)
    *   log, klogd, [145](#c08.xhtml_Page_145)
    *   Postfix server, [146](#c08.xhtml_Page_146), [150](#c08.xhtml_Page_150)
    *   subject, [153](#c08.xhtml_Page_153)
*   MIME types, [134](#c07.xhtml_Page_134)
*   minimum group ID, [137](#c07.xhtml_Page_137)
*   mke2fs, [72](#c04.xhtml_Page_72), [204](#c11.xhtml_Page_204)
*   mkfs.ext4, block reservation, [77](#c04.xhtml_Page_77)
*   mkswap, back block check, [80](#c04.xhtml_Page_80)
*   modprobe
    *   configuration information, [196](#c11.xhtml_Page_196)
    *   module dependencies, [8](#c01.xhtml_Page_8)
    *   modules, blacklist information, [12](#c01.xhtml_Page_12)
*   monitors, [105](#c06.xhtml_Page_105), [106](#c06.xhtml_Page_106)
*   mount, [69](#c04.xhtml_Page_69), [73](#c04.xhtml_Page_73)
*   mount points, [38](#c02.xhtml_Page_38)
    *   FHS, removable media, [70](#c04.xhtml_Page_70)
    *   maximum, [73](#c04.xhtml_Page_73)
    *   /media/, [78](#c04.xhtml_Page_78)
*   mounting
    *   filesystems, [69](#c04.xhtml_Page_69), [70](#c04.xhtml_Page_70), [71](#c04.xhtml_Page_71), [77](#c04.xhtml_Page_77)
    *   partitions and, [67](#c04.xhtml_Page_67), [76](#c04.xhtml_Page_76)
    *   simulating mount process, [73](#c04.xhtml_Page_73)
    *   unmounting, [74](#c04.xhtml_Page_74), [178](#c10.xhtml_Page_178)
    *   USB disk, [67](#c04.xhtml_Page_67)
*   mouse gestures, [108](#c06.xhtml_Page_108)
*   moving, files, [54](#c03.xhtml_Page_54)
*   MTU, network interfaces, [168](#c09.xhtml_Page_168)
*   mv, file overwrite, [49](#c03.xhtml_Page_49)

## N

*   nagios, monitoring, [50](#c03.xhtml_Page_50)
*   name resolution, [168](#c09.xhtml_Page_168), [186](#c10.xhtml_Page_186), [213](#c12.xhtml_Page_213)
*   netcat, servers, listening ports, [165](#c09.xhtml_Page_165)
*   netlink, messages, listening for, [162](#c09.xhtml_Page_162)
*   netmasks, subnets, CIDR notation, [163](#c09.xhtml_Page_163)
*   netstat
    *   -a, [216](#c12.xhtml_Page_216)
    *   process ID, [179](#c10.xhtml_Page_179)
    *   sockets, send and receive queues, [163](#c09.xhtml_Page_163)
*   Network Manager, [166](#c09.xhtml_Page_166), [172](#c09.xhtml_Page_172), [173](#c09.xhtml_Page_173)
*   networks, persistent configuration, [157](#c09.xhtml_Page_157)–174, [270](#a01.xhtml_Page_270)–277
*   nl, [201](#c11.xhtml_Page_201)
*   nmap
    *   name resolution, [186](#c10.xhtml_Page_186)
    *   open ports, finding, [184](#c10.xhtml_Page_184)
    *   UDP and, [215](#c12.xhtml_Page_215)
*   nptd, synchronization, time and, [147](#c08.xhtml_Page_147)
*   NTP (Network Time Protocol)
    *   interactive mode, [144](#c08.xhtml_Page_144)
    *   internally facing, [168](#c09.xhtml_Page_168)
    *   ntpdate, [211](#c12.xhtml_Page_211)
    *   time, [142](#c08.xhtml_Page_142)
*   ntpdate, [211](#c12.xhtml_Page_211)
*   ntpq, messages, [143](#c08.xhtml_Page_143)
*   numbering lines, [201](#c11.xhtml_Page_201)
*   NVMe-based devices, [18](#c01.xhtml_Page_18)
*   NXDOMAIN, [173](#c09.xhtml_Page_173)

## O

*   OnCalendar systemd, [136](#c07.xhtml_Page_136)
*   OpenLDAP
    *   corrupted, recovery, [131](#c07.xhtml_Page_131)
    *   database storage, [137](#c07.xhtml_Page_137)
    *   entries, adding, [129](#c07.xhtml_Page_129)
    *   slapd, [126](#c07.xhtml_Page_126)
*   operators, [94](#c05.xhtml_Page_94), [98](#c05.xhtml_Page_98), [99](#c05.xhtml_Page_99), [100](#c05.xhtml_Page_100)
*   Orca, [112](#c06.xhtml_Page_112), [116](#c06.xhtml_Page_116), [216](#c12.xhtml_Page_216)
*   out-of-memory conditions, [50](#c03.xhtml_Page_50)
*   output, realtime viewing, [56](#c03.xhtml_Page_56)
*   overwriting files, [49](#c03.xhtml_Page_49), [100](#c05.xhtml_Page_100)
*   ownership of files, group ownership, [68](#c04.xhtml_Page_68)

## P

*   packages
    *   cache update, Debian systems, [30](#c02.xhtml_Page_30)
    *   CentOS, [37](#c02.xhtml_Page_37), [39](#c02.xhtml_Page_39)
    *   Debian, [28](#c02.xhtml_Page_28), [31](#c02.xhtml_Page_31), [32](#c02.xhtml_Page_32), [33](#c02.xhtml_Page_33), [36](#c02.xhtml_Page_36)
    *   information, Debian, [199](#c11.xhtml_Page_199)
    *   installation, Fedora 22 system, [37](#c02.xhtml_Page_37)
    *   Linux, [21](#c02.xhtml_Page_21)–39
    *   RPM, downloading, [28](#c02.xhtml_Page_28)
    *   upgrades, yum, [199](#c11.xhtml_Page_199)
    *   upgrading, rpm, [199](#c11.xhtml_Page_199)
    *   yum, [27](#c02.xhtml_Page_27), [28](#c02.xhtml_Page_28), [31](#c02.xhtml_Page_31)
    *   zypper, installation, [37](#c02.xhtml_Page_37)
*   packet forwarding, number of packets, [168](#c09.xhtml_Page_168)
*   packets, statistics, [213](#c12.xhtml_Page_213)
*   pagers, backward/forward search, [58](#c03.xhtml_Page_58)
*   parameters, wireless devices, [168](#c09.xhtml_Page_168)
*   partitions
    *   bad blocks, [73](#c04.xhtml_Page_73)
    *   GRUB, [26](#c02.xhtml_Page_26)
    *   images, [49](#c03.xhtml_Page_49)
    *   initial sector, [33](#c02.xhtml_Page_33)
    *   Linux systems, [27](#c02.xhtml_Page_27), [67](#c04.xhtml_Page_67)
    *   lsblk, [200](#c11.xhtml_Page_200)
    *   LVM (Logical Volume Manager), initializing, [30](#c02.xhtml_Page_30)
    *   mail servers, [26](#c02.xhtml_Page_26)
    *   MBR system, [26](#c02.xhtml_Page_26), [77](#c04.xhtml_Page_77)
    *   mounting and, [67](#c04.xhtml_Page_67)
    *   swap partitions, formatting, [70](#c04.xhtml_Page_70)
    *   type 0x82, [67](#c04.xhtml_Page_67)
    *   UUID, [74](#c04.xhtml_Page_74)
*   passwd, [187](#c10.xhtml_Page_187), [214](#c12.xhtml_Page_214)
*   passwordfile, /etc/passwd, [49](#c03.xhtml_Page_49)
*   passwords
    *   age, [187](#c10.xhtml_Page_187)
    *   change, [191](#c10.xhtml_Page_191)
    *   change date, [129](#c07.xhtml_Page_129)
    *   changing, [129](#c07.xhtml_Page_129)
    *   encrypted, [131](#c07.xhtml_Page_131)
    *   expiration, [210](#c12.xhtml_Page_210)
    *   files, [125](#c07.xhtml_Page_125), [188](#c10.xhtml_Page_188)
    *   getent, [136](#c07.xhtml_Page_136)
    *   password-based login, [128](#c07.xhtml_Page_128)
    *   unlocking accounts, [214](#c12.xhtml_Page_214)
    *   x11vnc, [114](#c06.xhtml_Page_114)
*   paths, [61](#c03.xhtml_Page_61)
    *   ~/code/bin, [208](#c12.xhtml_Page_208)
    *   removing from results, [69](#c04.xhtml_Page_69)
*   PCI devices, [196](#c11.xhtml_Page_196)
*   permissions
    *   chmod, [90](#c05.xhtml_Page_90)
    *   editing, simultaneous, [79](#c04.xhtml_Page_79)
    *   execute, [97](#c05.xhtml_Page_97)
    *   granting, [78](#c04.xhtml_Page_78)
    *   ls command, [88](#c05.xhtml_Page_88)
    *   root privileges, [189](#c10.xhtml_Page_189)
    *   setgid, [80](#c04.xhtml_Page_80)
*   persistent configuration, [157](#c09.xhtml_Page_157)–174, [270](#a01.xhtml_Page_270)–277
*   pgrep, [57](#c03.xhtml_Page_57)
*   ping, [161](#c09.xhtml_Page_161), [166](#c09.xhtml_Page_166), [213](#c12.xhtml_Page_213)
*   pkill, [61](#c03.xhtml_Page_61)
*   plaintext files, octal representation, [202](#c11.xhtml_Page_202)
*   pointer keys, X session, [114](#c06.xhtml_Page_114)
*   POP3, DNS and, [173](#c09.xhtml_Page_173)
*   port scans, TCP connect, [187](#c10.xhtml_Page_187)
*   port-forwarding, local session, [183](#c10.xhtml_Page_183)
*   ports
    *   firewalls, [160](#c09.xhtml_Page_160), [214](#c12.xhtml_Page_214)
    *   open, [178](#c10.xhtml_Page_178)
    *   scanning for open, [178](#c10.xhtml_Page_178)
    *   Secure Shell, [164](#c09.xhtml_Page_164)
    *   SNMP, [162](#c09.xhtml_Page_162)
*   port-to-protocol translation, [163](#c09.xhtml_Page_163)
*   POSIX (Portable Operating System Interface), umask and, [68](#c04.xhtml_Page_68)
*   Postfix server
    *   email aliases, [152](#c08.xhtml_Page_152)
    *   mail delivery, errors, [151](#c08.xhtml_Page_151)
    *   mail queue, [144](#c08.xhtml_Page_144), [147](#c08.xhtml_Page_147), [150](#c08.xhtml_Page_150), [152](#c08.xhtml_Page_152), [154](#c08.xhtml_Page_154)
    *   messages, [146](#c08.xhtml_Page_146), [150](#c08.xhtml_Page_150), [156](#c08.xhtml_Page_156)
*   power, shutdown, [19](#c01.xhtml_Page_19)
*   practice exams
    *   Exam 1, [284](#a01.xhtml_Page_284)–288
    *   Exam 101-500, [288](#a01.xhtml_Page_288)–292
*   prepending line numbers, [53](#c03.xhtml_Page_53)
*   printing
    *   adding jobs to queue, [153](#c08.xhtml_Page_153)
    *   deleting jobs, [212](#c12.xhtml_Page_212)
    *   directories, [54](#c03.xhtml_Page_54), [199](#c11.xhtml_Page_199)
    *   head, default number printed, [48](#c03.xhtml_Page_48)
    *   human-readable format, [205](#c11.xhtml_Page_205)
    *   libraries, [199](#c11.xhtml_Page_199)
    *   lpr option, [154](#c08.xhtml_Page_154)
    *   queue, placing file, [145](#c08.xhtml_Page_145)
    *   removing jobs, [152](#c08.xhtml_Page_152), [155](#c08.xhtml_Page_155)
    *   tail, default number printed, [48](#c03.xhtml_Page_48)
    *   users, groups, [148](#c08.xhtml_Page_148)
    *   viewing jobs, [147](#c08.xhtml_Page_147)
    *   wc, number of lines, [47](#c03.xhtml_Page_47)
*   private addresses, internal use, [160](#c09.xhtml_Page_160)
*   /proc filesystem, [11](#c01.xhtml_Page_11)
*   process IDs, [50](#c03.xhtml_Page_50), [196](#c11.xhtml_Page_196), [203](#c11.xhtml_Page_203)
*   processes
    *   child, variables, [208](#c12.xhtml_Page_208)
    *   killing, [54](#c03.xhtml_Page_54)
    *   priorities, [52](#c03.xhtml_Page_52)
    *   reprioritizing running, [59](#c03.xhtml_Page_59)
    *   running, [196](#c11.xhtml_Page_196)
*   Procmail, email forwarding, [150](#c08.xhtml_Page_150)
*   programs, crashing, [50](#c03.xhtml_Page_50)
*   protocols
    *   firewalls, [160](#c09.xhtml_Page_160)
    *   ip, [168](#c09.xhtml_Page_168)
*   ps, aliases, [208](#c12.xhtml_Page_208)
*   PS1 environment variable, [87](#c05.xhtml_Page_87)
*   ps-based commands, [57](#c03.xhtml_Page_57)
*   public/private key pair, ssh, [179](#c10.xhtml_Page_179)

## R

*   RAID (Redundant Array of Inexpensive Disks), [17](#c01.xhtml_Page_17)
*   RAM, video cards, [112](#c06.xhtml_Page_112)
*   rc files, runlevels, [13](#c01.xhtml_Page_13)
*   RDP (Remote Desktop), [114](#c06.xhtml_Page_114), [119](#c06.xhtml_Page_119)
*   read access, granting, [78](#c04.xhtml_Page_78)
*   README file, missing, [96](#c05.xhtml_Page_96)
*   readonly, [99](#c05.xhtml_Page_99)
*   read-only mode, filesystem mounting, [77](#c04.xhtml_Page_77)
*   read-only variables, [91](#c05.xhtml_Page_91), [93](#c05.xhtml_Page_93)
*   read-write mode, [74](#c04.xhtml_Page_74)
*   reboot, commands, [7](#c01.xhtml_Page_7)
*   recursive copy, symlinks, [202](#c11.xhtml_Page_202)
*   Red Hat, [15](#c01.xhtml_Page_15), [217](#c12.xhtml_Page_217)
*   regular expressions, [59](#c03.xhtml_Page_59)
*   remote desktop, [113](#c06.xhtml_Page_113), [115](#c06.xhtml_Page_115)
*   remote forwarding, SSH, [191](#c10.xhtml_Page_191)
*   remote hosts, port setting, [183](#c10.xhtml_Page_183)
*   remote servers, command execution, [181](#c10.xhtml_Page_181)
*   remote system logging, [156](#c08.xhtml_Page_156)
*   removable media, mount points, FHS, [70](#c04.xhtml_Page_70)
*   repositories, yum, [29](#c02.xhtml_Page_29)
*   rm, [55](#c03.xhtml_Page_55)
*   rmdir, [48](#c03.xhtml_Page_48)
*   rmmod, module, unloading, [11](#c01.xhtml_Page_11)
*   ro, GRUB file, [29](#c02.xhtml_Page_29)
*   root user, home directory, [27](#c02.xhtml_Page_27)
*   route, [167](#c09.xhtml_Page_167), [168](#c09.xhtml_Page_168), [171](#c09.xhtml_Page_171)
*   rpm, [28](#c02.xhtml_Page_28), [29](#c02.xhtml_Page_29), [31](#c02.xhtml_Page_31), [38](#c02.xhtml_Page_38), [199](#c11.xhtml_Page_199)
*   RPM, packages, downloading, [28](#c02.xhtml_Page_28)
*   rpm2cpio, output location, [27](#c02.xhtml_Page_27)
*   RSA-based key pairs, [181](#c10.xhtml_Page_181), [184](#c10.xhtml_Page_184)
*   rsyslogd, server listening, [147](#c08.xhtml_Page_147)
*   runlevel
    *   default, [16](#c01.xhtml_Page_16)
    *   display, [7](#c01.xhtml_Page_7)
*   runlevels, systemctl, [16](#c01.xhtml_Page_16)
*   running tasks, backgrounded, [53](#c03.xhtml_Page_53)

## S

*   SAN (storage area network), [11](#c01.xhtml_Page_11)
*   SATA (Serial Advanced Technology Attachment)
    *   disks, [197](#c11.xhtml_Page_197)
    *   identifiers, [25](#c02.xhtml_Page_25)
*   sayHello function, [209](#c12.xhtml_Page_209)
*   scheduling
    *   certain time, [133](#c07.xhtml_Page_133)
    *   command execution, [125](#c07.xhtml_Page_125)
    *   cron, [126](#c07.xhtml_Page_126)
    *   directories, [136](#c07.xhtml_Page_136)
    *   listing jobs, [133](#c07.xhtml_Page_133)
    *   power down and, [125](#c07.xhtml_Page_125)
    *   scheduled jobs, finding, [127](#c07.xhtml_Page_127)
    *   script directory, [128](#c07.xhtml_Page_128)
*   screen magnifier, [116](#c06.xhtml_Page_116)
*   screen resolution, [106](#c06.xhtml_Page_106)
*   scripts. *See also* Bash scripts
    *   answers to review questions, [245](#a01.xhtml_Page_245)–251
    *   changes, [68](#c04.xhtml_Page_68)
    *   command line, date, [143](#c08.xhtml_Page_143)
    *   domain names, server, [162](#c09.xhtml_Page_162)
    *   execute then leave, [89](#c05.xhtml_Page_89)
*   SCSI (Small Computer System Interface), [18](#c01.xhtml_Page_18)
*   searches, [55](#c03.xhtml_Page_55), [58](#c03.xhtml_Page_58), [60](#c03.xhtml_Page_60)
*   Secure Shell, ports, [164](#c09.xhtml_Page_164)
*   security, [175](#c10.xhtml_Page_175)–192, [277](#a01.xhtml_Page_277)–284
*   sed, [47](#c03.xhtml_Page_47)
*   sendmail, [145](#c08.xhtml_Page_145), [146](#c08.xhtml_Page_146), [148](#c08.xhtml_Page_148), [149](#c08.xhtml_Page_149)
*   seq, delimiters, [95](#c05.xhtml_Page_95)
*   server host keys, SSH, [189](#c10.xhtml_Page_189)
*   servers
    *   routes, adding, [163](#c09.xhtml_Page_163)
    *   setgid bit, [185](#c10.xhtml_Page_185)
*   set, [94](#c05.xhtml_Page_94)
*   setgid, file permissions, [80](#c04.xhtml_Page_80)
*   setuid bit set, [178](#c10.xhtml_Page_178)
*   shared libraries, [26](#c02.xhtml_Page_26)
*   shebang line, [97](#c05.xhtml_Page_97)
*   shell scripts, [85](#c05.xhtml_Page_85)–101
    *   answers to review questions, [245](#a01.xhtml_Page_245)–251
    *   DATE variable, [92](#c05.xhtml_Page_92)
    *   files, existence, [90](#c05.xhtml_Page_90)
    *   permission denied, [94](#c05.xhtml_Page_94)
    *   shebang line, [97](#c05.xhtml_Page_97)
    *   syslog, logging to, [152](#c08.xhtml_Page_152)
    *   variable contents, displaying, [88](#c05.xhtml_Page_88)
    *   variables, user input, [89](#c05.xhtml_Page_89)
*   shells, [85](#c05.xhtml_Page_85)–101
    *   answers to review questions, [245](#a01.xhtml_Page_245)–251
    *   built-in commands, [71](#c04.xhtml_Page_71), [91](#c05.xhtml_Page_91)
    *   script, execute then leave, [89](#c05.xhtml_Page_89)
*   shutdown, [10](#c01.xhtml_Page_10), [19](#c01.xhtml_Page_19), [198](#c11.xhtml_Page_198)
*   shutdown command, [19](#c01.xhtml_Page_19)
*   SIGHUP signals, [56](#c03.xhtml_Page_56)
*   SIGKILL, [20](#c01.xhtml_Page_20)
*   single-user mode, [14](#c01.xhtml_Page_14)
*   skeleton home directory, [136](#c07.xhtml_Page_136)
*   slapadd, line number specification, [134](#c07.xhtml_Page_134)
*   slapd, [126](#c07.xhtml_Page_126), [130](#c07.xhtml_Page_130), [132](#c07.xhtml_Page_132)
*   SMART (Self-Monitoring, Analysis, and Reporting Technology), compatible hard drives, [74](#c04.xhtml_Page_74)
*   SMTP (Simple Mail Transfer Protocol), [148](#c08.xhtml_Page_148), [151](#c08.xhtml_Page_151)
*   snapshots, btrfs subvolumes, [76](#c04.xhtml_Page_76)
*   SNMP (Simple Network Management Protocol), ports, [162](#c09.xhtml_Page_162)
*   SOA (Start of Authority), [213](#c12.xhtml_Page_213)
*   source built-in, [100](#c05.xhtml_Page_100)
*   speech capabilities, Orca, [216](#c12.xhtml_Page_216)
*   speech recognition, KDE, [114](#c06.xhtml_Page_114)
*   SPF (Sender Policy Framework), [167](#c09.xhtml_Page_167)
*   Spice, authentication disable, [113](#c06.xhtml_Page_113)
*   .sql extension, searching for, [80](#c04.xhtml_Page_80)
*   srv/vhosts, [35](#c02.xhtml_Page_35)
*   ss, process IDs, [171](#c09.xhtml_Page_171)
*   SSD (solid-state drive), hardware, NVMe (Non-Volatile Memory Express), [17](#c01.xhtml_Page_17)
*   ssh
    *   authentication key, enabling, [184](#c10.xhtml_Page_184)
    *   key-based authentication, [179](#c10.xhtml_Page_179), [184](#c10.xhtml_Page_184)
    *   public/private key pair, [179](#c10.xhtml_Page_179)
    *   remote host port, [183](#c10.xhtml_Page_183)
    *   username change, [213](#c12.xhtml_Page_213)
    *   X11 application forwarding, [187](#c10.xhtml_Page_187)
*   SSH (Secure Shell)
    *   custom client configuration, [189](#c10.xhtml_Page_189)
    *   hosts, [182](#c10.xhtml_Page_182)
    *   keys, adding, [187](#c10.xhtml_Page_187)
    *   keys, virtual machine cloud deployment, [37](#c02.xhtml_Page_37)
    *   new windows, X forwarding and, [105](#c06.xhtml_Page_105)
    *   remote forwarding, [191](#c10.xhtml_Page_191)
    *   server host keys, [189](#c10.xhtml_Page_189)
    *   server-wide client, [191](#c10.xhtml_Page_191)
    *   sudoers, [114](#c06.xhtml_Page_114)
    *   visudo, [114](#c06.xhtml_Page_114)
    *   X sessions, [110](#c06.xhtml_Page_110)
*   ssh-agent, keys, listing current, [181](#c10.xhtml_Page_181)
*   ssh-keygen, [188](#c10.xhtml_Page_188), [191](#c10.xhtml_Page_191)
*   Start of Authority, information display, [165](#c09.xhtml_Page_165)
*   STDERR, redirect, [52](#c03.xhtml_Page_52)
*   STDIN, mail, [217](#c12.xhtml_Page_217)
*   STDOUT, redirect, [52](#c03.xhtml_Page_52)
*   sticky bits, [69](#c04.xhtml_Page_69)
*   sticky keys, GNOME, [106](#c06.xhtml_Page_106)
*   storage, libraries, [30](#c02.xhtml_Page_30)
*   su, [181](#c10.xhtml_Page_181), [186](#c10.xhtml_Page_186)
*   subnets, [215](#c12.xhtml_Page_215)
    *   masks, [212](#c12.xhtml_Page_212)
    *   netmasks, [163](#c09.xhtml_Page_163)
    *   splitting, [161](#c09.xhtml_Page_161)
*   sudo, [53](#c03.xhtml_Page_53), [78](#c04.xhtml_Page_78), [184](#c10.xhtml_Page_184), [214](#c12.xhtml_Page_214)
*   sudoers, SSH connection, [114](#c06.xhtml_Page_114)
*   suehring, [179](#c10.xhtml_Page_179)
*   swap partitions, formatting, [70](#c04.xhtml_Page_70)
*   swap space (Linux), [30](#c02.xhtml_Page_30)
    *   activating, [34](#c02.xhtml_Page_34)
    *   deactivating, [76](#c04.xhtml_Page_76)
    *   determining, [50](#c03.xhtml_Page_50)
    *   swapon, [39](#c02.xhtml_Page_39)
*   swapon, [39](#c02.xhtml_Page_39)
*   switch statement, [92](#c05.xhtml_Page_92)
*   symbolic links, [79](#c04.xhtml_Page_79)
    *   file test operators, [99](#c05.xhtml_Page_99)
    *   find, [205](#c11.xhtml_Page_205)
*   symlinks
    *   ln, [69](#c04.xhtml_Page_69)
    *   recursive copy, [202](#c11.xhtml_Page_202)
*   sysfs filesystem, MAC addresses, [197](#c11.xhtml_Page_197)
*   syslog
    *   - sign in configuration, [154](#c08.xhtml_Page_154)
    *   custom log files, [148](#c08.xhtml_Page_148)
    *   informational messages, [143](#c08.xhtml_Page_143)
    *   logging to, [152](#c08.xhtml_Page_152)
    *   lp printing, [217](#c12.xhtml_Page_217)
*   syslog-ng, configuration files, primary, [148](#c08.xhtml_Page_148)
*   system architecture, [3](#c01.xhtml_Page_3)–20, [220](#a01.xhtml_Page_220)–226
*   system clock, [134](#c07.xhtml_Page_134)
*   system logs, Linux directories, [155](#c08.xhtml_Page_155)
*   system services, [139](#c08.xhtml_Page_139)–156
    *   access allowed, [188](#c10.xhtml_Page_188)
    *   answers to review questions, [263](#a01.xhtml_Page_263)–270
    *   libwrap, [191](#c10.xhtml_Page_191)
    *   listening, [186](#c10.xhtml_Page_186)
    *   loaded, [9](#c01.xhtml_Page_9)
    *   preventing startup, [181](#c10.xhtml_Page_181), [182](#c10.xhtml_Page_182)
*   system time, [145](#c08.xhtml_Page_145), [146](#c08.xhtml_Page_146)
*   systemctl, [11](#c01.xhtml_Page_11)
    *   processes, killing, [197](#c11.xhtml_Page_197)
    *   runlevels, [16](#c01.xhtml_Page_16)
*   systemctl kill, [198](#c11.xhtml_Page_198)
*   systemd, [198](#c11.xhtml_Page_198)
    *   active timer display, [136](#c07.xhtml_Page_136)
    *   boot messages, [19](#c01.xhtml_Page_19)
    *   booting, [17](#c01.xhtml_Page_17)
    *   configuration files, [8](#c01.xhtml_Page_8), [72](#c04.xhtml_Page_72)
    *   configurations, [13](#c01.xhtml_Page_13)
    *   default target, [10](#c01.xhtml_Page_10)
    *   GUI, boot disable, [105](#c06.xhtml_Page_105)
    *   interprocess communication service units, [188](#c10.xhtml_Page_188)
    *   journal, [142](#c08.xhtml_Page_142), [149](#c08.xhtml_Page_149), [172](#c09.xhtml_Page_172), [212](#c12.xhtml_Page_212)
    *   location specification, [76](#c04.xhtml_Page_76)
    *   log file, [142](#c08.xhtml_Page_142), [144](#c08.xhtml_Page_144)
    *   logging, [142](#c08.xhtml_Page_142)
    *   multi-users, [16](#c01.xhtml_Page_16)
    *   network interface management, [174](#c09.xhtml_Page_174)
    *   output logging, [152](#c08.xhtml_Page_152)
    *   overriding configuration files, [15](#c01.xhtml_Page_15)
    *   program executing, [10](#c01.xhtml_Page_10)
    *   service units, listing, [8](#c01.xhtml_Page_8)
    *   single-user mode command, [9](#c01.xhtml_Page_9)
    *   storage, [13](#c01.xhtml_Page_13)
    *   timer units, [134](#c07.xhtml_Page_134), [135](#c07.xhtml_Page_135)
    *   udev, [197](#c11.xhtml_Page_197)
    *   user init files, [14](#c01.xhtml_Page_14)
*   systemd-resolved, DNS resolution, [173](#c09.xhtml_Page_173)
*   systemd-run, timed events, [132](#c07.xhtml_Page_132)
*   systemed, timer units, [138](#c07.xhtml_Page_138)
*   SysV system
    *   chkconfig, services, [9](#c01.xhtml_Page_9)
    *   init, [7](#c01.xhtml_Page_7), [15](#c01.xhtml_Page_15)
    *   process termination, [19](#c01.xhtml_Page_19)
    *   scripts, starting/stopping, [15](#c01.xhtml_Page_15)
*   SysVinitu environment, [198](#c11.xhtml_Page_198)

## T

*   tail, [48](#c03.xhtml_Page_48), [51](#c03.xhtml_Page_51), [202](#c11.xhtml_Page_202)
*   tar files, [50](#c03.xhtml_Page_50)
*   tasks
    *   administrative, [124](#c07.xhtml_Page_124)–138
    *   running, backgrounded, [53](#c03.xhtml_Page_53)
*   TCP (Transmission Control Protocol)
    *   remote system logging, [156](#c08.xhtml_Page_156)
    *   wrappers, blocking hosts, [208](#c12.xhtml_Page_208)
*   tcpdump, available interfaces, [170](#c09.xhtml_Page_170)
*   tee, appending, [205](#c11.xhtml_Page_205)
*   telinit, [197](#c11.xhtml_Page_197)
*   terminal processing, [51](#c03.xhtml_Page_51), [56](#c03.xhtml_Page_56)
*   terminal-based interface, package management, Debian, [31](#c02.xhtml_Page_31)
*   test built-in command, arguments, not null, [92](#c05.xhtml_Page_92)
*   text, formatting, [202](#c11.xhtml_Page_202)
*   TFTP (Trivial File Transfer Protocol), PXELINUX, [15](#c01.xhtml_Page_15)
*   three-way handshake, [167](#c09.xhtml_Page_167)
*   time
    *   current, [125](#c07.xhtml_Page_125)
    *   dmesg, [196](#c11.xhtml_Page_196)
    *   environment variables, [126](#c07.xhtml_Page_126)
    *   hardware clock, [143](#c08.xhtml_Page_143)
    *   NTP (Network Time Protocol), [142](#c08.xhtml_Page_142)
    *   setting, [153](#c08.xhtml_Page_153)
    *   system clock, [134](#c07.xhtml_Page_134), [145](#c08.xhtml_Page_145), [146](#c08.xhtml_Page_146)
    *   system time, offline devices, [145](#c08.xhtml_Page_145)
*   timedatectl, [134](#c07.xhtml_Page_134), [151](#c08.xhtml_Page_151)
*   timezones
    *   available, [135](#c07.xhtml_Page_135), [143](#c08.xhtml_Page_143)
    *   current, [151](#c08.xhtml_Page_151)
    *   Debian, [133](#c07.xhtml_Page_133), [216](#c12.xhtml_Page_216)
    *   directories, [124](#c07.xhtml_Page_124), [217](#c12.xhtml_Page_217)
    *   Linux server, [124](#c07.xhtml_Page_124)
    *   systemwide, [132](#c07.xhtml_Page_132)
    *   timedatectl, [151](#c08.xhtml_Page_151)
    *   user home directory, [127](#c07.xhtml_Page_127)
*   top, [60](#c03.xhtml_Page_60), [203](#c11.xhtml_Page_203)
*   touch, [48](#c03.xhtml_Page_48)
*   tracepath, [165](#c09.xhtml_Page_165)
*   traceroute, [165](#c09.xhtml_Page_165)
    *   ICMP, request and, [171](#c09.xhtml_Page_171)
    *   IPv6 route traces, [172](#c09.xhtml_Page_172)
    *   TCP SYN packets, [161](#c09.xhtml_Page_161)
*   traceroute, !H, [215](#c12.xhtml_Page_215)
*   traceroute6, IPv6 traceroute, [162](#c09.xhtml_Page_162)
*   traffic, route limiting, [165](#c09.xhtml_Page_165)
*   transport layer security, remote desktop, [115](#c06.xhtml_Page_115)
*   tune2fs, [73](#c04.xhtml_Page_73), [75](#c04.xhtml_Page_75), [77](#c04.xhtml_Page_77)
*   type 0x82 partition, [67](#c04.xhtml_Page_67)

## U

*   Ubuntu
    *   accessibility, [209](#c12.xhtml_Page_209)
    *   images, deploying to remote provider, [36](#c02.xhtml_Page_36)
*   udev, [6](#c01.xhtml_Page_6), [12](#c01.xhtml_Page_12)
*   udevadm commands, hotplug devices, [6](#c01.xhtml_Page_6)
*   UDP, nmap, [215](#c12.xhtml_Page_215)
*   UEFI (Unified Extensible Firmware Interface)
    *   boot configuration, [15](#c01.xhtml_Page_15)
    *   boot loaders, [14](#c01.xhtml_Page_14)
    *   booting, shim, [16](#c01.xhtml_Page_16)
*   UG flags, [167](#c09.xhtml_Page_167)
*   UIDs
    *   files, [125](#c07.xhtml_Page_125)
    *   GIDs and, [130](#c07.xhtml_Page_130)
*   ulimit, memory limits, [187](#c10.xhtml_Page_187)
*   umask, POSIX format and, [68](#c04.xhtml_Page_68)
*   umount, [71](#c04.xhtml_Page_71), [178](#c10.xhtml_Page_178)
*   uniq, [202](#c11.xhtml_Page_202)
*   UNIX, commands, [41](#c03.xhtml_Page_41)–61, [233](#a01.xhtml_Page_233)–239
*   unset, [87](#c05.xhtml_Page_87)
*   unset option, [97](#c05.xhtml_Page_97)
*   updates, kernels, [32](#c02.xhtml_Page_32)
*   Upstart, configuration files, [9](#c01.xhtml_Page_9)
*   uptime, load average information, [203](#c11.xhtml_Page_203)
*   USB (Universal Serial Bus)
    *   connections, information, [11](#c01.xhtml_Page_11)
    *   devices, [6](#c01.xhtml_Page_6), [9](#c01.xhtml_Page_9), [10](#c01.xhtml_Page_10)
    *   disks, mounting, [67](#c04.xhtml_Page_67)
    *   drives, [10](#c01.xhtml_Page_10)
    *   temporary disk, removing, [10](#c01.xhtml_Page_10)
*   user information, [137](#c07.xhtml_Page_137)
*   useradd
    *   account disabled, [210](#c12.xhtml_Page_210)
    *   adding groups, [130](#c07.xhtml_Page_130)
    *   home directory, [128](#c07.xhtml_Page_128)
    *   password expiration, [210](#c12.xhtml_Page_210)
*   usermod, [131](#c07.xhtml_Page_131), [189](#c10.xhtml_Page_189)
*   usernames
    *   changing, [189](#c10.xhtml_Page_189), [213](#c12.xhtml_Page_213)
    *   environment variables, [99](#c05.xhtml_Page_99)
    *   files, [125](#c07.xhtml_Page_125)
    *   printing, [202](#c11.xhtml_Page_202)
    *   sorted list, [48](#c03.xhtml_Page_48)
*   users
    *   account expiring, [182](#c10.xhtml_Page_182)
    *   deleting, [79](#c04.xhtml_Page_79), [125](#c07.xhtml_Page_125), [211](#c12.xhtml_Page_211)
    *   directories, [130](#c07.xhtml_Page_130), [133](#c07.xhtml_Page_133)
    *   executing commands on, [180](#c10.xhtml_Page_180)
    *   expiring account, [180](#c10.xhtml_Page_180)
    *   file copying, [90](#c05.xhtml_Page_90)
    *   interfaces, [105](#c06.xhtml_Page_105)–119, [251](#a01.xhtml_Page_251)–257
    *   limits, [180](#c10.xhtml_Page_180), [181](#c10.xhtml_Page_181), [191](#c10.xhtml_Page_191)
    *   logged in currently, [180](#c10.xhtml_Page_180)
    *   login, preventing temporarily, [178](#c10.xhtml_Page_178)
    *   messaging all, [8](#c01.xhtml_Page_8)
    *   names, printing, [202](#c11.xhtml_Page_202)
    *   printing, from password file, [188](#c10.xhtml_Page_188)
    *   time zones, [127](#c07.xhtml_Page_127)
    *   useradd, [128](#c07.xhtml_Page_128)
*   /usr/local, directories, creating, [49](#c03.xhtml_Page_49)
*   UTC (Coordinated Universal Time)
    *   hardware clock, current system time, [146](#c08.xhtml_Page_146)
    *   output to, [212](#c12.xhtml_Page_212)
*   UUID
    *   lsblk and, [80](#c04.xhtml_Page_80)
    *   partition identification, [72](#c04.xhtml_Page_72), [74](#c04.xhtml_Page_74)

## V

*   variables
    *   Bash script, [98](#c05.xhtml_Page_98), [208](#c12.xhtml_Page_208)
    *   child processes, [208](#c12.xhtml_Page_208)
    *   DATE, [92](#c05.xhtml_Page_92)
    *   environment
        *   declaring, [55](#c03.xhtml_Page_55)
        *   localization, [127](#c07.xhtml_Page_127)
        *   paper size, [135](#c07.xhtml_Page_135)
        *   PS1, [87](#c05.xhtml_Page_87)
        *   removing, [87](#c05.xhtml_Page_87)
        *   single-line viewing, [99](#c05.xhtml_Page_99)
        *   terminal device, X session, [111](#c06.xhtml_Page_111)
        *   usernames, [99](#c05.xhtml_Page_99)
    *   export, [101](#c05.xhtml_Page_101)
    *   exported, [101](#c05.xhtml_Page_101)
    *   $FILEPATH, [92](#c05.xhtml_Page_92)
    *   read-only, declare, [93](#c05.xhtml_Page_93)
*   .variables.sh, [208](#c12.xhtml_Page_208)
*   vgscan, devices, filters, [39](#c02.xhtml_Page_39)
*   Vi editor
    *   cursor, moving, [58](#c03.xhtml_Page_58)
    *   files, removing lines, [60](#c03.xhtml_Page_60)
    *   insert mode, [52](#c03.xhtml_Page_52)
    *   moving to line, [203](#c11.xhtml_Page_203)
    *   save and exit, [51](#c03.xhtml_Page_51)
    *   searches, backward, [55](#c03.xhtml_Page_55)
*   video cards, RAM, [112](#c06.xhtml_Page_112)
*   virtual machine
    *   boot process, [25](#c02.xhtml_Page_25)
    *   bootstrapping, [205](#c11.xhtml_Page_205)
    *   deployment, [36](#c02.xhtml_Page_36)
*   virtualization, [35](#c02.xhtml_Page_35), [39](#c02.xhtml_Page_39)
*   visudo, SSH connection, [114](#c06.xhtml_Page_114)
*   volumes, logical volumes, [18](#c01.xhtml_Page_18)

## W

*   wall, user log off, [196](#c11.xhtml_Page_196)
*   Wayland protocol, [113](#c06.xhtml_Page_113)
*   wc, printing, number of lines, [47](#c03.xhtml_Page_47)
*   web server, /home/webfiles, [124](#c07.xhtml_Page_124)
*   Weston, configuration, [115](#c06.xhtml_Page_115)
*   while loops, [90](#c05.xhtml_Page_90), [91](#c05.xhtml_Page_91), [93](#c05.xhtml_Page_93), [101](#c05.xhtml_Page_101)
*   Wi-Fi, device configuration, [173](#c09.xhtml_Page_173)
*   wildcards, [60](#c03.xhtml_Page_60)
    *   /etc/hosts.allow, [186](#c10.xhtml_Page_186)
*   wireless devices, parameters, [168](#c09.xhtml_Page_168)
*   wireless networks, scanning for, [168](#c09.xhtml_Page_168)
*   WWN (World Wide Name), directory hierarchies, [18](#c01.xhtml_Page_18)

## X

*   X
    *   abbreviations, [112](#c06.xhtml_Page_112)
    *   authority files, [108](#c06.xhtml_Page_108), [115](#c06.xhtml_Page_115)
    *   clients, executing, configuration file, [107](#c06.xhtml_Page_107)
    *   configuration
        *   keyboard model, [107](#c06.xhtml_Page_107)
        *   Screen section, [112](#c06.xhtml_Page_112)
        *   server layouts, [112](#c06.xhtml_Page_112)
    *   local client, display, [111](#c06.xhtml_Page_111)
    *   SSH (Secure Shell), [110](#c06.xhtml_Page_110)
    *   window information, [109](#c06.xhtml_Page_109)
*   X Display Manager, login, [116](#c06.xhtml_Page_116)
*   X forwarding, SSH server, new windows, [105](#c06.xhtml_Page_105)
*   X server
    *   clean exit, [108](#c06.xhtml_Page_108)
    *   configuration, [107](#c06.xhtml_Page_107), [113](#c06.xhtml_Page_113)
    *   connections, closing, [117](#c06.xhtml_Page_117)
    *   defaults, restoring, [117](#c06.xhtml_Page_117)
    *   error log, [117](#c06.xhtml_Page_117)
    *   hosts, [110](#c06.xhtml_Page_110), [116](#c06.xhtml_Page_116)
    *   init, [117](#c06.xhtml_Page_117)
    *   resources, freeing, [117](#c06.xhtml_Page_117)
    *   TCP, listening disable, [116](#c06.xhtml_Page_116)
    *   user access, [210](#c12.xhtml_Page_210)
*   X session, pointer keys, [114](#c06.xhtml_Page_114)
*   X windows, [216](#c12.xhtml_Page_216)
*   X11, [118](#c06.xhtml_Page_118), [187](#c10.xhtml_Page_187)
*   x11vnc, passwords, [114](#c06.xhtml_Page_114)
*   xauth, [117](#c06.xhtml_Page_117), [119](#c06.xhtml_Page_119)
*   xauth authority file, [110](#c06.xhtml_Page_110)
*   xauth utility, X authority files, [108](#c06.xhtml_Page_108)
*   XDMCP
    *   BroadcastQuery packets, [118](#c06.xhtml_Page_118)
    *   configuration file, [118](#c06.xhtml_Page_118)
    *   host access, [108](#c06.xhtml_Page_108)
*   XFree86, hardware query, [106](#c06.xhtml_Page_106)
*   XFS filesystem, [73](#c04.xhtml_Page_73), [78](#c04.xhtml_Page_78)
*   xfs_check, [74](#c04.xhtml_Page_74)
*   xfs_fsr, filesystem reorganization time, [78](#c04.xhtml_Page_78)
*   xfs_metadump, progress indicator, [70](#c04.xhtml_Page_70)
*   xfs_repair, log zeroing, [77](#c04.xhtml_Page_77)
*   xfsrestore, options, [75](#c04.xhtml_Page_75)
*   xfwm4 window manager, [113](#c06.xhtml_Page_113)
*   xhost, hosts, enabling, [118](#c06.xhtml_Page_118)
*   xinit, per-user initialization, [117](#c06.xhtml_Page_117)
*   X.org, font storage, [107](#c06.xhtml_Page_107)
*   xorg.conf
    *   blank mode, [109](#c06.xhtml_Page_109)
    *   Files section, fonts, [110](#c06.xhtml_Page_110)
    *   inactivity timeout, [113](#c06.xhtml_Page_113)
    *   Module section, [106](#c06.xhtml_Page_106)
    *   video mode changes, [108](#c06.xhtml_Page_108)
*   Xsession, [111](#c06.xhtml_Page_111), [115](#c06.xhtml_Page_115), [118](#c06.xhtml_Page_118)
*   xzcat program, [58](#c03.xhtml_Page_58)

## Y

*   yum
    *   configuration file, primary, [36](#c02.xhtml_Page_36)
    *   package cache search, [31](#c02.xhtml_Page_31)
    *   package installation, [27](#c02.xhtml_Page_27)
    *   packages, [28](#c02.xhtml_Page_28), [199](#c11.xhtml_Page_199)
    *   repositories, [29](#c02.xhtml_Page_29)
    *   verification prompt, [199](#c11.xhtml_Page_199)
*   yumdownloader, dependencies, downloading, [32](#c02.xhtml_Page_32)

## Z

*   zone transfer, [167](#c09.xhtml_Page_167)
*   zsh, searching for, [28](#c02.xhtml_Page_28)
*   zypper, packages, installation, [37](#c02.xhtml_Page_37)

# Comprehensive Online Learning Environment

Register to gain one year of FREE access to the online interactive learning environment and test bank to help you study for your LPIC-1 certification exams—included with your purchase of this book!

The online test bank includes the following:

*   **Practice Test Questions** to reinforce what you’ve learned
*   **Bonus Practice Exams** to test your knowledge of the material

Go to [http://www.wiley.com/go/sybextestprep](http://www.wiley.com/go/sybextestprep) to register and gain access to this comprehensive study tool package.

### Register and Access the Online Test Bank

To register your book and get access to the online test bank, follow these steps:

1.  Go to [bit.ly/SybexTest](http://bit.ly/SybexTest).
2.  Select your book from the list.
3.  Complete the required registration information, including answering the security verification to prove book ownership. You will be emailed a PIN code.
4.  Follow the directions in the email or go to [https://www.wiley.com/go/sybextestprep](https://www.wiley.com/go/sybextestprep).
5.  Enter the pin code you received and click the “Activate PIN” button.
6.  On the Create an Account or Login page, enter your username and password, and click Login. A “Thank you for activating your PIN!” message will appear. If you don’t have an account already, create a new account.
7.  Click the “Go to My Account” button to add your new book to the My Products page.

![inline](images/advert.jpg)

# **WILEY END USER LICENSE AGREEMENT**

Go to [www.wiley.com/go/eula](http://www.wiley.com/go/eula) to access Wiley’s ebook EULA.