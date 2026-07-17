![](cover.jpeg)

COMPUTER PROGRAMMING             

4 books in 1:

SQL for Beginners, C# for Beginners, C# for intermediate, Hacking with Kali Linux, Everything you Need for Mastering Programming & Cyber Security

Andrew Sutherland

 Copyright 2019 by Andrew Sutherland - All rights reserved.

This Book is provided with the sole purpose of providing relevant information on a specific topic for which every reasonable effort has been made to ensure that it is both accurate and reasonable. Nevertheless, by purchasing this Book, you consent to the fact that the author, as well as the publisher, are in no way experts on the topics contained herein, regardless of any claims as such that may be made within. As such, any suggestions or recommendations that are made within are done so purely for entertainment value. It is recommended that you always consult a professional prior to undertaking any of the advice or techniques discussed within.

This is a legally binding declaration that is considered both valid and fair by both the Committee of Publishers Association and the American Bar Association and should be considered as legally binding within the United States.

The reproduction, transmission, and duplication of any of the content found herein, including any specific or extended information will be done as an illegal act regardless of the end form the information ultimately takes. This includes copied versions of the work both physical, digital, and audio unless the expressed consent of the Publisher is provided beforehand. Any additional rights reserved.

Furthermore, the information that can be found within the pages described forthwith shall be considered both accurate and truthful when it comes to the recounting of facts. As such, any use, correct or incorrect, of the provided information will render the Publisher free of responsibility as to the actions taken outside of their direct purview. Regardless, there are zero scenarios where the original author or the Publisher can be deemed liable in any fashion for any damages or hardships that may result from any of the information discussed herein.

Additionally, the information in the following pages is intended only for informational purposes and should thus be thought of as universal. As befitting its nature, it is presented without assurance regarding its prolonged validity or interim quality. Trademarks that are mentioned are done without written consent and can in no way be considered an endorsement from the trademark holder.

Table of Contents

SQL for Beginners

[INTRODUCTION](#part0000_split_008.html__Toc24454313)

[CHAPTER 1: AN INTRODUCTION TO GETTING STARTED WITH SQL](#part0000_split_009.html__Toc24454314)

[Structured Query Language (SQL)](#part0000_split_010.html__Toc24454315)

[Benefits of Working with Databases](#part0000_split_011.html__Toc24454316)

[Types of Structured Query Language Commands](#part0000_split_012.html__Toc24454317)

[CHAPTER 2: BASIC SQL COMMANDS](#part0000_split_013.html__Toc24454318)

[SELECT](#part0000_split_014.html__Toc24454319)

[UPDATE](#part0000_split_015.html__Toc24454320)

[DELETE](#part0000_split_016.html__Toc24454321)

[INSERT](#part0000_split_017.html__Toc24454322)

[CREATE TABLE](#part0000_split_018.html__Toc24454323)

[ALTER TABLE](#part0000_split_019.html__Toc24454324)

[DROP TABLE](#part0000_split_020.html__Toc24454325)

[CREATE INDEX and DROP INDEX](#part0000_split_021.html__Toc24454326)

[CREATE VIEW](#part0000_split_022.html__Toc24454327)

[GROUP BY](#part0000_split_023.html__Toc24454328)

[JOIN](#part0000_split_024.html__Toc24454329)

[CREATE DATABASE and ALTER DATABASE](#part0000_split_025.html__Toc24454330)

[Other Basic SQL Commands](#part0000_split_026.html__Toc24454331)

[CHAPTER 3: CREATING YOUR FIRST DATABASE AND TABLE](#part0000_split_027.html__Toc24454332)

[Steps](#part0000_split_028.html__Toc24454333)

[Creating Your First Database and Table Using Command Line](#part0000_split_029.html__Toc24454334)

[CHAPTER 4: INSERTING, UPDATING AND DELETING DATA IN SQL PROGRAMMING](#part0000_split_030.html__Toc24454335)

[Inserting, Updating, and Deleting Data](#part0000_split_031.html__Toc24454336)

[SQL UPDATE Multiple Columns](#part0000_split_034.html__Toc24454337)

[Deleting Data from SQL Table](#part0000_split_035.html__Toc24454338)

[CHAPTER 5: MODIFYING AND CONTROLLING TABLES IN SQL PROGRAMMING](#part0000_split_036.html__Toc24454339)

[Changing Tables](#part0000_split_036.html__Toc24454340)

[Modifying and Removing Constraints](#part0000_split_037.html__Toc24454341)

[CHAPTER 6: WORKING WITH SUBQUERIES](#part0000_split_038.html__Toc24454342)

[The SQL Server Subquery](#part0000_split_039.html__Toc24454343)

[Creating New Databases in SQL Programming](#part0000_split_040.html__Toc24454344)

[Industries That Use SQL Programming](#part0000_split_041.html__Toc24454345)

[Common SQL Database Systems](#part0000_split_042.html__Toc24454346)

[The Relevance of the Database System to Social Networks](#part0000_split_043.html__Toc24454347)

[CHAPTER 7: COMBINING QUERIES IN SQL](#part0000_split_044.html__Toc24454348)

[How to Create Union Query by Creating and Uniting the Select Queries](#part0000_split_045.html__Toc24454349)

[An Example You Can Recreate the Northwind Sample Database](#part0000_split_046.html__Toc24454350)

[CHAPTER 8: BASIC SQL MATHEMATICS AND STATISTICS](#part0000_split_047.html__Toc24454351)

[Mathematics and Statistics for Data Science](#part0000_split_048.html__Toc24454352)

[CHAPTER 9: SAVING TIME WITH VIEWS, FUNCTIONS, AND TRIGGERS](#part0000_split_049.html__Toc24454353)

[Best Practices and Approach for One to Achieve a Goal](#part0000_split_050.html__Toc24454354)

[Database Objects](#part0000_split_051.html__Toc24454355)

[CHAPTER 10: SQL EMBEDDED JAVA PROGRAM](#part0000_split_052.html__Toc24454356)

[Overview and A Brief History of SQL](#part0000_split_053.html__Toc24454357)

[Benefits of Java Programming](#part0000_split_054.html__Toc24454358)

[Benefits of SQL](#part0000_split_055.html__Toc24454359)

[Disadvantages of SQLJ Programming](#part0000_split_056.html__Toc24454360)

[Requirements for LQLJ](#part0000_split_057.html__Toc24454361)

[Development Goals of SQLJ](#part0000_split_058.html__Toc24454362)

[CHAPTER 11: COMMON ROOKIE MISTAKES](#part0000_split_059.html__Toc24454363)

[CHAPTER 12: BUILT-IN FUNCTIONS & CALCULATIONS](#part0000_split_060.html__Toc24454364)

[Types of SQL Functions](#part0000_split_061.html__Toc24454365)

[Categories of Functions](#part0000_split_062.html__Toc24454366)

[SQL Calculations](#part0000_split_063.html__Toc24454367)

[The Importance of SQL Built-In Functions and Mathematical Applications](#part0000_split_064.html__Toc24454368)

[Downsides of In-Built Functions](#part0000_split_065.html__Toc24454369)

[CHAPTER 13: AN INTRODUCTION TO JOINS](#part0000_split_066.html__Toc24454370)

[How to Setup the Database Environment in SQL](#part0000_split_067.html__Toc24454371)

[Basics of SQL Joins](#part0000_split_068.html__Toc24454372)

[Types of SQL Joins](#part0000_split_069.html__Toc24454373)

[CHAPTER 14: TEN TIPS FOR EASY RETRIEVAL](#part0000_split_070.html__Toc24454374)

[CHAPTER 15: VARIABLES AND STORED ROUTINES](#part0000_split_072.html__Toc24454375)

[Declaring the Variables](#part0000_split_073.html__Toc24454376)

[CHAPTER 16: PROJECTS AND EXERCISES IN SQL PROGRAMMING](#part0000_split_074.html__Toc24454377)

[Examples of Exercises in SQL](#part0000_split_075.html__Toc24454378)

[Projects in SQL Programming](#part0000_split_076.html__Toc24454379)

[Application of SQL](#part0000_split_077.html__Toc24454380)

[Applications of SQL](#part0000_split_078.html__Toc24454381)

[CONCLUSION](#part0000_split_079.html__Toc24454382)

# Table of Contents

C# for Beginners

[Introduction](#part0000_split_082.html__Toc27818607)

[Chapter 1: An Introduction to C#](#part0000_split_083.html__Toc27818608)

[What is the C# Language?](#part0000_split_084.html__Toc27818609)

[The .Net Framework](#part0000_split_085.html__Toc27818610)

[The C# IDE](#part0000_split_086.html__Toc27818611)

[How to Work with C# On Linux and Mac Computers](#part0000_split_087.html__Toc27818612)

[Chapter 2: Get Ready for C#](#part0000_split_088.html__Toc27818613)

[How to Install Visual Studio Community](#part0000_split_089.html__Toc27818614)

[Writing Your First Program in C#](#part0000_split_090.html__Toc27818615)

[The Basics of Your Code](#part0000_split_091.html__Toc27818616)

[Chapter 3: C# Keywords](#part0000_split_092.html__Toc27818617)

[Chapter 4: File Input and Output](#part0000_split_093.html__Toc27818618)

[Implementing the File Input and Output Operators](#part0000_split_094.html__Toc27818619)

[The FileStream Class](#part0000_split_095.html__Toc27818620)

[The FileMode Enumerator](#part0000_split_096.html__Toc27818621)

[How to Implement Reading and Writing Into Our Files](#part0000_split_097.html__Toc27818622)

[Chapter 5: Making Choices and Decisions](#part0000_split_098.html__Toc27818623)

[A Look at the If Statement](#part0000_split_099.html__Toc27818624)

[A Look at the If Else Statement](#part0000_split_100.html__Toc27818625)

[What the Nested Conditional Statement is All About](#part0000_split_101.html__Toc27818626)

[Chapter 6: Basic Math](#part0000_split_102.html__Toc27818627)

[What is the Arithmetic Operators?](#part0000_split_103.html__Toc27818628)

[What are the Assignment Operators?](#part0000_split_104.html__Toc27818629)

[What are the Relational Operators?](#part0000_split_105.html__Toc27818630)

[What are the Logical Operators?](#part0000_split_106.html__Toc27818631)

[What are the Bitwise Operators?](#part0000_split_107.html__Toc27818632)

[Chapter 7: A Look at Polymorphism](#part0000_split_108.html__Toc27818633)

[Chapter 8: Enumerations](#part0000_split_109.html__Toc27818634)

[How We Can Turn Enumeration Types Into Bit Flags](#part0000_split_110.html__Toc27818635)

[System.Enum Type](#part0000_split_111.html__Toc27818636)

[Handling Some Conversions](#part0000_split_112.html__Toc27818637)

[Chapter 9: Multithreading](#part0000_split_113.html__Toc27818638)

[The Lifecycle of a Thread](#part0000_split_114.html__Toc27818639)

[A Look At the Main Thread](#part0000_split_115.html__Toc27818640)

[Properties of the Thread Class](#part0000_split_116.html__Toc27818641)

[Creating Threads](#part0000_split_117.html__Toc27818642)

[Chapter 10: The Variables](#part0000_split_118.html__Toc27818643)

[How to Define the Variable](#part0000_split_119.html__Toc27818644)

[Initializing the Variables](#part0000_split_120.html__Toc27818645)

[Lvalue and Rvalue Expressions](#part0000_split_121.html__Toc27818646)

[Chapter 11: Encapsulation](#part0000_split_122.html__Toc27818647)

[Public Access](#part0000_split_123.html__Toc27818648)

[Private Access](#part0000_split_124.html__Toc27818649)

[Protected Access](#part0000_split_125.html__Toc27818650)

[Internal Access](#part0000_split_126.html__Toc27818651)

[Chapter 12: Simple Projects to Get Some Practice](#part0000_split_127.html__Toc27818652)

[Creating Hangman in C#](#part0000_split_128.html__Toc27818653)

[Conclusion](#part0000_split_129.html__Toc27818654)

 Table of Contents

C# for Intermediate

[Introduction](#part0000_split_132.html__Toc25717409)

[Why C#](#part0000_split_133.html__Toc25717410)

[.NET Framework](#part0000_split_134.html__Toc25717411)

[What Is Meant By The.NET Framework?](#part0000_split_135.html__Toc25717412)

[Chapter 1 - Create Types](#part0000_split_136.html__Toc25717413)

[Common Language Runtime - CLR](#part0000_split_136.html__Toc25717414)

[Intermediate Language](#part0000_split_137.html__Toc25717415)

[The Execution](#part0000_split_138.html__Toc25717416)

[A Class Of Its Own](#part0000_split_139.html__Toc25717417)

[The Boolean Type](#part0000_split_140.html__Toc25717418)

[Is This The Right Type?](#part0000_split_141.html__Toc25717419)

[Implicit Conversions](#part0000_split_142.html__Toc25717420)

[Type Conversion](#part0000_split_143.html__Toc25717421)

[Error During Explicit Conversion](#part0000_split_144.html__Toc25717422)

[Avoiding Conversion Errors](#part0000_split_145.html__Toc25717423)

[Chapter 2 - Linq](#part0000_split_146.html__Toc25717424)

[Create You The Library Project](#part0000_split_147.html__Toc25717425)

[Derivation In An Application](#part0000_split_148.html__Toc25717426)

[Chapter 3 - Methods](#part0000_split_149.html__Toc25717427)

[Constants](#part0000_split_150.html__Toc25717428)

[Literals Constants](#part0000_split_151.html__Toc25717429)

[Escape Sequences](#part0000_split_152.html__Toc25717430)

[Instructions](#part0000_split_153.html__Toc25717431)

[Whitespaces](#part0000_split_154.html__Toc25717432)

[Empty Instructions](#part0000_split_155.html__Toc25717433)

[Composite Statement And Blocks](#part0000_split_156.html__Toc25717434)

[Expressions](#part0000_split_157.html__Toc25717435)

[Operators](#part0000_split_158.html__Toc25717436)

[Assignment Operator](#part0000_split_159.html__Toc25717437)

[Mathematical Operators](#part0000_split_160.html__Toc25717438)

[Remainder Operator](#part0000_split_161.html__Toc25717439)

[Increment and Decrement Operators](#part0000_split_162.html__Toc25717440)

[Ranking And Parentheses](#part0000_split_163.html__Toc25717441)

[Comparison Operators](#part0000_split_164.html__Toc25717442)

[Chapter 4 - C# Style Conventions And Nesting](#part0000_split_165.html__Toc25717443)

[Condition Operator](#part0000_split_166.html__Toc25717444)

[Chapter 5 - Input / output and strings](#part0000_split_167.html__Toc25717445)

[Strings And I / O](#part0000_split_168.html__Toc25717446)

[Formatting With Escape Sequences](#part0000_split_169.html__Toc25717447)

[Format Numbers](#part0000_split_170.html__Toc25717448)

[Standard Formatting Of Numbers](#part0000_split_171.html__Toc25717449)

[Formatting Floating Point Numbers](#part0000_split_172.html__Toc25717450)

[Currency Format](#part0000_split_173.html__Toc25717451)

[Special Formatting](#part0000_split_174.html__Toc25717452)

[Custom Formatting](#part0000_split_175.html__Toc25717453)

[0 Formatting](#part0000_split_176.html__Toc25717454)

[Cross-Formatting](#part0000_split_177.html__Toc25717455)

[Formatting Groups](#part0000_split_178.html__Toc25717456)

[Percent Formatting](#part0000_split_179.html__Toc25717457)

[Literals Formatting](#part0000_split_180.html__Toc25717458)

[Case Formatting](#part0000_split_181.html__Toc25717459)

[Format Date And Time Values](#part0000_split_182.html__Toc25717460)

[Output of Enumerations](#part0000_split_183.html__Toc25717461)

[Compare Strings](#part0000_split_184.html__Toc25717462)

[Insert, Delete and Replace](#part0000_split_185.html__Toc25717463)

[Preparing Strings](#part0000_split_186.html__Toc25717464)

[Chapter 6 - Flow Control](#part0000_split_187.html__Toc25717465)

[Branches](#part0000_split_188.html__Toc25717466)

[Switch Statement](#part0000_split_189.html__Toc25717467)

[Grinding](#part0000_split_190.html__Toc25717468)

[The Forefather Of The Loops - Goto Instruction](#part0000_split_191.html__Toc25717469)

[Continue Statement](#part0000_split_192.html__Toc25717470)

[Chapter 7 - Methods, Parameters And Validity Of Variables](#part0000_split_193.html__Toc25717471)

[Definition and Call](#part0000_split_194.html__Toc25717472)

[Parameters Of A Method](#part0000_split_195.html__Toc25717473)

[Defining Parameters](#part0000_split_196.html__Toc25717474)

[Types Of Parameters](#part0000_split_197.html__Toc25717475)

[Chapter 8 - Arrays](#part0000_split_198.html__Toc25717476)

[Data Management with Arrays](#part0000_split_199.html__Toc25717477)

[Sort Arrays](#part0000_split_200.html__Toc25717478)

[Search In Sorted Arrays](#part0000_split_201.html__Toc25717479)

[Arrays As Parameters](#part0000_split_202.html__Toc25717480)

[Composite Arrays](#part0000_split_203.html__Toc25717481)

[Multidimensional Arrays](#part0000_split_203.html__Toc25717482)

[There Is No Multidimensionality](#part0000_split_204.html__Toc25717483)

[Arrays Of Arrays](#part0000_split_205.html__Toc25717484)

[Chapter 9 - Fields](#part0000_split_206.html__Toc25717485)

[Initialization](#part0000_split_207.html__Toc25717486)

[Object Variables As Fields](#part0000_split_208.html__Toc25717487)

[Constant Fields](#part0000_split_209.html__Toc25717488)

[Chapter 10 - Heredity](#part0000_split_210.html__Toc25717489)

[The Principle Of Inheritance](#part0000_split_211.html__Toc25717490)

[The Basic Mechanism](#part0000_split_212.html__Toc25717491)

[The Meaning Of Inheritance](#part0000_split_213.html__Toc25717492)

[Some Important Facts](#part0000_split_214.html__Toc25717493)

[Inherited Elements Form Sub-Objects](#part0000_split_215.html__Toc25717494)

[Why Do The Inherited Elements Form Sub-Objects?](#part0000_split_216.html__Toc25717495)

[Three Access Levels](#part0000_split_217.html__Toc25717496)

[Three access levels](#part0000_split_218.html__Toc25717497)

[Access To Hidden Elements](#part0000_split_219.html__Toc25717498)

[Inheritance vs. Embedding](#part0000_split_220.html__Toc25717499)

[Nested Classes](#part0000_split_221.html__Toc25717500)

[Chapter 11 - Projects](#part0000_split_222.html__Toc25717501)

[Making Code Decisions](#part0000_split_222.html__Toc25717502)

[Optional Exercises](#part0000_split_223.html__Toc25717503)

[Repeating A Code Block](#part0000_split_224.html__Toc25717504)

[To Know More Of While](#part0000_split_225.html__Toc25717505)

[EXERCISES](#part0000_split_226.html__Toc25717506)

[CLASSES AND OBJECTS](#part0000_split_227.html__Toc25717507)

[Organizing The Object Code](#part0000_split_228.html__Toc25717508)

[Extracting Behavior Through Methods](#part0000_split_229.html__Toc25717509)

[Returning Values Inside The Method](#part0000_split_230.html__Toc25717510)

[Standard Value Of Class Attributes](#part0000_split_231.html__Toc25717511)

[Names Convention](#part0000_split_232.html__Toc25717512)

[Exercises](#part0000_split_233.html__Toc25717513)

[Class Composition](#part0000_split_234.html__Toc25717514)

[ENCAPSULATION AND ACCESS MODIFIERS](#part0000_split_235.html__Toc25717515)

[Simplifying Property Statement With Self-Implemented Properties](#part0000_split_236.html__Toc25717516)

[Name Convention For Property](#part0000_split_237.html__Toc25717517)

[Exercises](#part0000_split_238.html__Toc25717518)

[Conclusion](#part0000_split_239.html__Toc25717519)

# [Table of Contents](XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX)

Hacking with Kali Linux

[Introduction](#part0000_split_242.html__Toc22993521)

[Chapter 1: An Introduction to Kali Linux](#part0000_split_243.html__Toc22993522)

[An Overview of Kali Linux](#part0000_split_244.html__Toc22993523)

[Introduction to Penetration Testing](#part0000_split_245.html__Toc22993524)

[Chapter 2: Vulnerability Assessment](#part0000_split_246.html__Toc22993525)

[Introduction to Vulnerability Assessment](#part0000_split_247.html__Toc22993526)

[Chapter 3: Wireless Network Hacking](#part0000_split_249.html__Toc22993527)

[Introduction to Wireless Network Hacking](#part0000_split_250.html__Toc22993528)

[Basic Wireless Commands](#part0000_split_251.html__Toc22993529)

[Wi-Fi Recon with Aircrack-ng](#part0000_split_252.html__Toc22993530)

[Detecting and Connecting to Bluetooth](#part0000_split_253.html__Toc22993531)

[The Implementation of Wireless Testing Methodology](#part0000_split_254.html__Toc22993532)

[Chapter 4: Analyzing and Managing Networks](#part0000_split_256.html__Toc22993533)

[Introduction to Analyzing and Managing Networks](#part0000_split_257.html__Toc22993534)

[Chapter 5: Penetration Testing and Web Security](#part0000_split_258.html__Toc22993535)

[Penetration Testing](#part0000_split_259.html__Toc22993536)

[Chapter 6: Text Manipulation and Bash Scripting](#part0000_split_260.html__Toc22993537)

[Text Manipulation](#part0000_split_261.html__Toc22993538)

[Bash Scripting](#part0000_split_262.html__Toc22993539)

[Chapter 7: Cracking Encryptions & Attacking with Frame Networks](#part0000_split_263.html__Toc22993540)

[Cracking Encryptions](#part0000_split_264.html__Toc22993541)

[Chapter 8: File Systems and Storage Device Management](#part0000_split_265.html__Toc22993542)

[File Systems](#part0000_split_265.html__Toc22993543)

[Storage Device Management](#part0000_split_266.html__Toc22993544)

[Chapter 9: Becoming Secure and Anonymous](#part0000_split_267.html__Toc22993545)

[Introduction to Becoming Secure and Anonymous](#part0000_split_268.html__Toc22993546)

[How Tor Works](#part0000_split_269.html__Toc22993547)

[Chapter 10: Advanced Social Engineering and Physical Security](#part0000_split_270.html__Toc22993548)

[Introduction to Advanced Social Engineering and Physical Security](#part0000_split_271.html__Toc22993549)

[Chapter 11: Python Scripting Basics for Hackers](#part0000_split_273.html__Toc22993550)

[What is Python?](#part0000_split_273.html__Toc22993551)

[Python Basics](#part0000_split_274.html__Toc22993552)

[The Python Standard Library](#part0000_split_276.html__Toc22993553)

[Conclusion](#part0000_split_277.html__Toc22993554)

SQL

Learn SQL Programming and Learn Coding Fast with This Comprehensive, Step-by-Step Guide for Beginners

Andrew Sutherland

 Copyright 2019 by Andrew Sutherland - All rights reserved.

This Book is provided with the sole purpose of providing relevant information on a specific topic for which every reasonable effort has been made to ensure that it is both accurate and reasonable. Nevertheless, by purchasing this Book, you consent to the fact that the author, as well as the publisher, are in no way experts on the topics contained herein, regardless of any claims as such that may be made within. As such, any suggestions or recommendations that are made within are done so purely for entertainment value. It is recommended that you always consult a professional prior to undertaking any of the advice or techniques discussed within.

This is a legally binding declaration that is considered both valid and fair by both the Committee of Publishers Association and the American Bar Association and should be considered as legally binding within the United States.

The reproduction, transmission, and duplication of any of the content found herein, including any specific or extended information will be done as an illegal act regardless of the end form the information ultimately takes. This includes copied versions of the work both physical, digital, and audio unless the expressed consent of the Publisher is provided beforehand. Any additional rights reserved.

Furthermore, the information that can be found within the pages described forthwith shall be considered both accurate and truthful when it comes to the recounting of facts. As such, any use, correct or incorrect, of the provided information will render the Publisher free of responsibility as to the actions taken outside of their direct purview. Regardless, there are zero scenarios where the original author or the Publisher can be deemed liable in any fashion for any damages or hardships that may result from any of the information discussed herein.

Additionally, the information in the following pages is intended only for informational purposes and should thus be thought of as universal. As befitting its nature, it is presented without assurance regarding its prolonged validity or interim quality. Trademarks that are mentioned are done without written consent and can in no way be considered an endorsement from the trademark holder.

# INTRODUCTION

Congratulations on purchasing Learn SQL Programming, and thank you for doing so. Computer languages have become more popular today since the introduction of instructions fed into machines. As almost everything now become more reliant on computers, hence is the need to learn a few things, including understanding computer SQL programming language.

The following chapters will discuss SQL programming, which is among one of the many programming languages out there. As learning the basics is critical in every course, the book highlights the fundamental essential components of SQL programming. As such, you will learn about the introduction of how to get started, including the primary definition and reasons why it is crucial. SQL programming also entails various benefits and types which will learn. Besides, the chapters provide a quick overview of server and client technology, which is also essential while learning SQL programming.

That said, learning about the introduction part puts you at the forefront of meeting your goals when taking a lesson in SQL programming. Therefore, the chapters will also discuss the basic commands commonly used. Like other programming languages, SQL programming encompasses different commands, but in this case, this book will solely focus on the basic ones to bring out the general idea. After having the necessary preparations, you will also learn about how to create your initial database as well as tables. It is also essential to learn how to put the lesson learned into practice to ascertain its applicability in the computer industry.

# CHAPTER 1: AN INTRODUCTION TO GETTING STARTED WITH SQL

Structured Query Language or SQL primarily deals with databases crucial for developers, analysts, and administrators essential for providing skills on how to create room to store data in an organized manner. Learning SQL can sometimes become challenging, especially when you fail to commit adequate time as well as taking inappropriate approaches. However, learning SQL programming will significantly promote careers in SQL, as it is one of the most demanded skills globally today. You should understand that learning about SQL programming without practical is usually a failing course.

SQL was first introduced by Ted Code but later enhanced by Donald D. Chamberlin and Raymond F. Boyce in the early 1970s. The initial language name was referred to as SEQUEL, Structured English Query Language, and incorporated to help in information retrieval. The name was later changed to SQL and first used commercially in 1979 and the subsequent years. Over the years, its development continued leading to the introduction of more advanced SQL commands. By 1990, there existed new versions with standard Database Language SQL with the recent version released in 2016\. However, various developments and advanced have witnessed over time, making SQL programming flexible and more reliable, especially in storage and quick retrieval of information when the need arises.

## Structured Query Language (SQL)

Structured Query Language or SQL is a standard programming tool commonly preferred by developers, analysts and administrators to design, create, and supervise rational databases. These databases comprise different sets of tables which entail rows or columns filled with data. On each column, the database or table is filled with information of a given set of identical data such as name, address, cost, or other values. On the other hand, rows usually contain data values that intersect the information of each column. Generally, databases are mostly full of tables containing data sets crucial for a given organization, including the storage of data for quick retrieval. Since it is among computer programming languages, SQL is a universal coding programming tool commonly considered a doorway to learn other programming languages such as Python. It was first introduced in the 1970s, and learners do not necessarily require prior knowledge in programming to venture into learning SQL programming. When you are ready to learn about SQL, it is always advisable to understand the basics by beginning with simple queries before jumping into complex processes. Read and learn from different sources, including tutorials, while making progress each day. Besides, engage in creating and designing different databases to advance in trickier programming practices.

## Benefits of Working with Databases

### Ease of Access

A database typically accommodates massive amounts of data, which may include millions of specific data. For instance, when you use other forms of data storage units, retrieving such information may become a bit complicated due to the load in the system. However, SQL, like most databases, provides straightforward access to specific information. That is, you can readily search the needed data from millions of files and gain access to it in seconds. Besides, if employees of a given organization need to access the data from different regions or areas, all they need is a reliable internet connection and access to this information at any time. Therefore, employees can continue working with the data when traveling or at home.

### Restrictions of Access

Databases are an essential tool for the storage of data, especially when you need to create a platform to secure a company or other sensitive information. This is because the databases have become more secure today, making it difficult for unauthorized personnel from accessing the data. However, this is offered in two ways; a user may access the data but only read rather than make changes while others may be able to read and make necessary changes. This is crucial, especially for employees and the management when sharing data vital for the running of the organization.

### Self-Describing Capabilities

Database systems usually are fitted with adequate room to create and design tables with a complete description of each data stored. When, for instance, feeding a piece of given information into the system, the database will provide a summary of each set. Each dataset will have a description providing a separation of data which fit specific areas. This way, database systems are considered self-describing as they contain metadata descriptions essential for the identification of data and relations in different tables within a particular system.

### Provision of Data Redundancy Controls

Databases commonly store each dataset in one place as an approach to promote data storage, especially when there is a need to create effective database systems. However, some instances of data redundancy may occur as a way to enhance the performance of the system. Databases primarily offer controls to data redundancy but controlled solely by the application. The general idea is to introduce as reduced redundancy as possible when creating and designing databases.

### Allowance of Data Independency

Database management systems also accompany the benefit of data independence, which makes metadata and other data descriptions to become separate from the program. This process is made possible because data structures are handled separately by the system but not included in the program. More so, the database allows for transaction processing of data, which involves concurrency control subsystems. This, therefore, ensures that the data remains valid and similar when undergoing transaction processing.

## Types of Structured Query Language Commands

### Data Definition Language (DDL)

This is a command type that allow users to develop and restructure physical database structure, and when executed, it makes changes immediately. The most commonly used commands in this type include CREATE, ALTER and DROP TABLE, CREATE INDEX and CREATE VIEW, among others. These commands usually focus on the definition of the table more so during designing abs making other changes to the database system in general.

### Data Manipulation Language (DML)

This is the command where manipulation of values, objects, and figures within the table undergo changes, mainly when focusing on mistakes on the datasets. DML is often done when the table has been created, and a database designed by DDL commands. The commands used include INSERT, UPDATE, and DELETE. Besides, these commands are among the most beneficial, especially when making changes in the database management systems. 

### Data Control Language (DCL)

A data control command is an SQL command which allows users to access the information stored within the database system quickly. ALTER PASSWORD, GRANT, REVOKE, and CREATE SYNONYM are the commonly used commands essential for the management of data. Besides, DCL is also critical handling matters related to data control, including controlling the user to gain access to the database system accordingly.

### Data Query Language (DQL)

This is an SQL query that comprises only one command but widely used today as it combines with other SQL functions to retrieve and collect data from specific tables under given parameters. The command SELECT works well with additional options and clauses of SQL and handles all queries, either simple or complex. Also, the Data Query Language command is applicable for vague and specific datasets.

### Transactional Control Commands

As the name suggests, this command allows for the management of problems and queries involving transactions of data in any database system. Transaction Control Language is often used for making changes where the need is and uses both 'undo' and 'apply' options for making changes. The commands used include COMMIT, ROLLBACK, SAVEPOINT, and SET TRANSACTION. As such, making changes as well as modifications can be made without any significant complications when using commands in SQL programming.

### Server and Client Technology

Server and client technology are an ability to separate specific functions of programs or applications into two or more parts, providing a relationship between computers. In other words, it is the ability of one program, the client, to make a request to two or more processors, the server, and they comply with the application. In this case, the client can access, present, and make modifications to this data from the main desktop computer. On the other hand, the server acts as a storage unit to supply protected data to the client. Therefore, server and client technology create a network structure where data can be retrieved with minimal stress, especially when there is a need to supply the needed information.

However, the interconnection arises where clients significantly rely on servers for supply or relevant components such as files and devices as well as processing capabilities. Servers, therefore, are compelling computer systems suitable for handling file servers in the form of disk drives, print, and network servers. Clients often workstations or PCs where applications are run. The model is usually through a computer network with an active and partitioned workload system on separated hardware. Despite so, clients do not share resources but communicates with the server for content or other service functions.

# CHAPTER 2: BASIC SQL COMMANDS

As mentioned earlier, SQL used specific commands which control the tables within database systems, especially when handling multiple tables with big data. Each table is often defined by a given name, such as customers or orders. It should be known that all functions or commands are done with SQL statements. More so, SQL statements, as well as keywords, are not case sensitive, and some databases may require semicolons on statements as a standard format. Therefore, SQL statements include SELECT, UPDATE, DELETE, INSERT INTO, and more. 

## SELECT

Like most computer commands, SELECT is primarily utilized for querying the database as well as in the retrieval of intended data that matches the parameters specified. For example, SELECT column1 [, column2, …], FROM (table name), WHERE (condition). When writing the SELECT command, you may use conditional clauses such as equal (=), greater than (>), less than (<), greater than or equal (>=), less than or equal (<), not equal to (<>) and LIKE. When you write SELECT * FROM (table_name), it readily returns the entire data from the table and may, at times, include quotes around the text. However, do not use quotes to enclose mathematical objects. When using LIKE, ensure it matches a pattern, especially when involving the use of (%), which denotes 0 in SQL programming. For example, 'A%' resembles all strings which use A as the first letter while '%a' matches data, which ends with a. Similarly, '%a%' matches strings or data which have an 'a' between values or information in a given table or database.

## UPDATE

When there are preexisting values in a table and there in need to change them, then the UPDATE command is used. The command uses the functions UPDATE (table_name), SET colX=valX [, colY=valY,…], WHERE (condition). This type of SQL command is applicable when there is a need to change, alter, or edit rows in a given table, therefore, creating a more significant process of the management of database systems. At some point, specific rows can be modified without causing any impact to data in a similar column.

## DELETE

As the name suggests, this is a term used in computing for the removal of unwanted, repeated, or unused data from the system. Similarly, SQL also utilizes a similar function as a command to remove unwanted records from a given table within the system. In this case, it uses the feature DELETE FROM (table_name), WHERE (conditions), and the file will be deleted successfully. You can also clear the entire information without getting rid of the table using the function DELETE * FROM (table_name). Therefore, when removing the record, the specified range or conditions set determines the extent of what you are getting rid of. However, some conditions may compromise the data if you delete vital data due to wrongly and unspecified parameters.

## INSERT

When the table has been created, that is, the columns and rows are specified as required, data is then fed into the system. However, it is usually challenging to feed information one at a time in each column and row more so when the data is bulky. This may result in errors that may go unnoticed, therefore compromising the future. Therefore, SQL uses the INSERT VALUE, also referred to as the INSERT INTO command, to feed data into the table and at required columns and rows. The programming language uses the function INSERT INTO (table_name), (col1,…….., coln), VALUES (val1,….,valn) to insert values. The 'n' denotes the number of the last column in your table where the previous value will be added. In this case, inserting the values into the table becomes straightforward, quicker and prevents cases emerging from sparse data entry formats.

## CREATE TABLE

The CREATE TABLE clause is another basic command of SQL essential for developing a table to insert the information needed. The function used is CREATE TABLE (table_name), (column1 data type, column2 data type, column3 data type,…). When creating a table, there are also other considerations, which include char for which the fixed-length character string, varchar also size, number with a maximum column value and data value. As database systems comprise of several tables, you can add more tables in a certain database and insert your values.

## ALTER TABLE

In some cases, you may have created a table with either more or fewer columns hence the need to delete or add. Therefore, SQL provides a query that enables you to quickly remove or columns to an existing table by first specifying a data type and the number of columns to add or delete. The format used in this case is ALTER TABLE (table_name), DROP COLUMN colname. That is, specify the table name in which you are to add or delete columns and then set the parameters for which data type and on which column you wish to modify.

## DROP TABLE

Another necessary command used in SQL is for getting rid of the entire table from the database when it is unwanted of there is a need to create a new one. That is, SQL allows you to use the command DELETE * FROM (table_name) and drop a given table. As a basic command in SQL, DROP TABLE is crucial, especially when you want to have another table with fresh details, which differs significantly when compared to the previous one.

## CREATE INDEX and DROP INDEX

Another typical command in SQL is for creating indexes also essential in databases. When you want to create an index, it involves developing a search key that facilitates the process of searching and retrieving data quickly. Like the DROP TABLE command, DROP INDEX means deleting of an existing index from the database and the development of a new one.

## CREATE VIEW

As a result of an SQL SELECT, CREATE VIEW is another command or query that entails a virtual table but with fields from more than one table in a database system. As it has similar values like that of the original table, view tables are meant to provide a preview of the information stored in one or more tables within a database. Therefore, a view or virtual table can be considered a real table. The function used is CREATE TABLE view_name AS, SELECT col_name(s), FROM table_name, WHERE (condition). View table can be utilized within a command, saved procedures, and from other similar commands. As such, this facilitates the process of adding more functions and linking them, therefore, presenting the necessary data to the user.

## GROUP BY

The GROUP BY is a much newer command added to facilitate the process of grouping aggregate results searched by column values. In other words, GROUP BY entails enabling the database to group data with respect to the similarities highlighted by the user into a given column. The format used included; SELECT col_name, function (col_name) FROM table_name GROUP BY col_name. However, the 'WHERE’ keyword was replaced in this command with 'HAVING,' which brings out the condition. Therefore, the function used is SELECT col_name, function (col_name) FROM table_name, GROUP BY col_name, HAVING function (col_name) conditions data. In this case, the user is, therefore, capable of grouping columns according to their requirements.

## JOIN

Data may be spread among different tables within a single database; hence, you wish to collate these data into one table. Tables under a single database typically have a connection through the keys, therefore, making it easy to associate the data between different tables. As such, the tables can be linked together through the process of join in SQL programming. For example, if you have three tables with a connection such as customers, orders, and product supply, then you can join them using the JOIN command. As such, use the command SELECT customer_name, product name, FROM customer_name, order, product supply, WHERE customer = orders = product supply. Besides, the command also allows for INNER JOIN for the selection of two tables and LEFT JOIN to return all the rows to the initial table.

## CREATE DATABASE and ALTER DATABASE

When using the SQL programming tool, you may choose to create more than one database using the necessary command of CREATE DATABASE. The command quickly incorporates a fresh database where an individual can develop and design several tables within. Most often, you may create a database and then go ahead to make changes and modify the tables as well. As to modify the SQL database, you may use the statement ALTER DATABASE which readily modifies the system.

## Other Basic SQL Commands

ORDER BY is another clause that orders column names according to user needs using the command ORDER BY col_name ASC for ascending and DESC for descending. There is also IN, AND/OR, BETWEEN and AND. All these functions are essential for operating values in the table. For instance, IN is crucial for returning for a known value using the format SELECT * FROM table_name WHERE col_name IN (val1, val2,…). BETWEEN  and  AND are vital for providing a range between two values and use the function SELECT * FROM table_name WHERE col_name BETWEEN val1 AND val2\. AND/OR may be used to join two or more values or conditions and uses either WHERE, AND, and OR formats to determine its viability.

# CHAPTER 3: CREATING YOUR FIRST DATABASE AND TABLE

Before having a successful database with practical tables in SQL programming, both the creation of a database and then a table is required. However, there are several SQL data application software out there, but all have almost a similar step of creating a new database and tables. When you create your first database system, you will then have to design a table where you will feed your data and store it more securely and effectively. SQL offers a free graphical user interface, and it is easy to create. The following is a step by step guide on how to create your first SQL database and tables before thinking of feeding your data.

## Steps

### Step 1: SQL Server Management Studio Software Installation

The firsts step in creating your first database and table is by acquiring the SQL software available for free online from Microsoft. This software comes fully packed, allowing you to interact and manage the SQL server with limited command-line instructions. Besides, it is crucial when it comes to using databases when in remote regions. Mac users can, however, utilize open-source programs, for instance, SQuirrel SQL, to maneuver through the Database system.

### Step 2: Launch the SQL Studio

When you launch the SQL studio, the software occasionally requests for a server at first that you will prefer using all along or the one you are using presently. If you have an already existing one, you may choose to input the permissions, authenticate, and connect. Some may prefer local database systems by setting a new name authenticate using a preferred name or address. Launching the SQL server management studio begins the process of interacting with the software and a path to creating your first database and table.

### Step 3: Identify Database Folder

Immediately after the connection is made on either the local or remote, a Window will open on the left of the screen. On top, there will be a server where it will connect to. If not, you may click on the icon '+,' which will display multiple elements, including the option to create a new database. In some versions, you may see the icon for creating a new database immediately on the left drop-down Window. You can then click on 'Create New Database.'

### Step 4: Create a New Database

As mentioned in step 3, the drop-down menu will fully display multiple options, including the one to create a new database. First, you will configure the database according to your parameters as well as providing the name for ease of identification. Most users prefer leaving the settings in their default, but you can change them if you are familiar with how they impact your process of data storage in the system. Note that when you create the database name, two files will generate the data automatically and log files. Data files are responsible for the storage of data while log files track all the changes, modifications, and other alterations made in the database.

### Step 5: Create Your Tables

Databases often do not store data unless structures in forms of rows and tables are created for that data to remain organized. Tables are the primary storage units where data is held, but initially, you have to create the table before you insert the information. Similar to creating a new database, tables are also straightforward when creating. In the Databases folder, expand the Window then right-click on Tables and choose 'Nee Table.' Windows will open, displaying a table that can be easily manipulated towards the number rows and columns, titles, and how you want to organize your work. In this step, you will succeed in creating both the database and table, therefore, moving forward in organizing your task.

### Step 6: Developing the Primary Key

The primary key plays a significant role in databases as it acts as a record number or ID for easy identification and remembrance when you view the page later. As such, it highly recommended creating these keys in the first column. There are many ways to do this and include entering the ID in the column field by typing int and deselecting the 'Allow Nulls.' Select the key icon found in the toolbar and marks it as the Primary key.

### Step 7: Structure the Tables

Tables typically have multiple columns, also referred to as fields, and each column represents one element of data entries. When creating your table, you initially structured it to fit the number of data entries, therefore essential for each dataset as other primary keys. Thus, the structuring process will entail identifying each column with a given set of data. For example, FirstName column, Last name, and address column, among others. 

### Step 8: Creating Other Columns

Immediately you create the columns for primary keys; you will notice that there appear more columns below it. These are not for primary keys but essential for the insertion of other information. As such, ensure you input the correct data for each column to avoid filling the table with the wrong information. In the column, you will enter the 'nchar,' which is a data type for text, 'int' used for whole numbers, and 'decimal' for storage of decimal numbers.

### Step 9: Saving the Table

After you finish creating the content in each field, you will notice that your table will consist of rows and columns. However, you will need to first save the table before entering the information. This can be done by selecting the Save icon also in the toolbar and name your table. When naming your table, ensure that you create a name that you can easily relate to the content or recognize. Besides, databases with different tables should have different names so that they can be identified easily.

### Step 10: Add Data

Once the table is saved, you can now add the data into the system feeding each field with relevant information. However, you can confirm if the table is saved by expanding the Tables Folder and try to see if our table name is listed. If not, use the Table Folder to refresh the tables, and you will see your table. Back in the table, Right-click on the table where a drop dialog box will appear and select 'Edit Top 200 Rows'. The Window will then display fields for you to add data but ignore the primary keys as they will fill automatically. Continue with the same process until when you enter the last data in the table.

### Step 11: Running the Table

After you have finished working on the table, you are to save the content so that you do not lose your work. As the table is already saved, click on 'Execute SQL' on the toolbar when you have finished entering data, and it will execute the process of feeding each data you entered into the columns. The parsing process may take a few seconds, depending on a load of data. If there are any errors in the feeding process, the system will show you where you input data incorrectly. More so, you can execute the program parsing of all the data by using the combination of 'ctrl' and 'R.'

### Step 12: Data Querying

At this step, you have created your first database and table and successfully saved the information through SQL language programming. The database is now fully functional, and you henceforth create more tables within a single database. However, there is a limit on how many tables per database, but many users do not worry about this rule. You can, therefore, create new database systems you want and create more tables. At this end, you can query your data for reports or any relevant purposes, such as organizational or administrative purposes. Often, having a general idea of SQL programming, especially for putting it into practice in creating databases and tables, allows you to advance your learning skills.

## Creating Your First Database and Table Using Command Line

As already discussed in the last chapter, you can as well use SQL commands and statements to create databases and tables. The same applies to SQL Server Management Studio like the above guide, but commands and statements are used to give instructions to the system to perform a given function. As to build your first database, you use the command' SELECT DATABASE (database_name)’ and hitting the execute button to create the program. The message on the screen should, therefore, be 'Command(s) completed successfully," showing that your database has been created.

As to use the database, run the command 'USE (database_name),' which tells the query window to run the new database program. On the other hand, creating a new table entails running the command 'CREATE TABLE (table_name).' Entering data follows the command 'INSERT DATA INTO (table_name), VALUES (table_name),' and repeating the same process for all the datasets you have. The same also allows for viewing the data you saved and includes the command format 'SELECT * FROM (table_name). All the above commands are the critical ones when it comes to maneuvering through different SQL databases. As such, it is always essential to learn about each SQL basic commands to execute programs readily.

# CHAPTER 4: INSERTING, UPDATING AND DELETING DATA IN SQL PROGRAMMING

There is too much buzz available in the technological world about data. However, raw data is not so useful when on its own. SQL is pronounced as “sequel”. It stands for Structured Query Language. It is typically a language that allows for communication through databases. This happens so that it can easily manage all the data contained within the databases. 

In modern days, most businesses, both small and large corporations, make use of data in running their operations. All the data being used is managed through the use of databases. For this reason, there has been a very high demand for experts in database administration. Being skilled in database development, basically, SQL development proves to be essential. 

Data continues to be the central part of numerous mobile applications and web applications. For instance, Facebook application holds the information of a user’s profile as well as data on their posts and friends. To maintain this kind of data, a database system is applied. Therefore, Structured Query Language, is one of the programming languages that allow programmers to work with the available data. 

Typically, databases are not designed to understand other programming languages. They know the SQL programming language only. It is a must for those intending to work on app development and web development to learn the SQL programming language. Like all programming languages, SQL possesses its typical markup. Due to this, programmers should find it necessary to be conversant with SQL markup before they can effectively use it in their applications. 

Additionally, SQL programming has another unique feature due to its concept of tables. Each database can be presented as a certain number of tables. Every table usually has several rows and columns and acts as a representation of sets of data. The tables allow programmers to store all the information they need. 

Several SQL commands are frequently used. Programmers must be familiar with the commands for database work. Some of the commands that a programmer is required to write include: 

CREATE DATABASE- This enables the creation of a database

CREATE TABLE- It allows for the creation of tables

SELECT- This is when a programmer if finding and extracting data from a database

UPDATE- Helps in making adjustments and editing data

DELETE- It is written when deleting data

Other than the above that are most commonly used, other complicated commands depend on the complexity of the database. It means that the more the complexity of the database, the number of commands the programmer is supposed to use also increase. The commands are used anytime queries are being written. They are referred to as the inquiries that allow programmers to operate the data present in the databases. 

In simpler words, when the commands are entered within a database system, they are interpreted and processed by the system. The outcomes are, for instance, new records in the database or new databases are created. In most cases, the initial query is responsible for coming up with a new database. 

SQL programming language is categorized into several language elements; they include:

Clauses- They are the constituent elements of queries and statements. There are instances where provisions are optional.

Expressions- They come up with scalar values or tables that consist of rows and columns holding data.

Predicates- They act as the specifications for conditions that have been evaluated to SQL 3VL (three-valued logic). It can also be in the form of Boolean truth values. They are used in limiting the effects brought about by queries and statements. They are also used in changing the flow of programs. 

Queries- They are used when retrieving data based on specified criteria. Queries are essential elements to SQL. 

Statements- They have consistent effects on data and schemata. They also control program flow, diagnostics, transactions, sessions and connections. All statements in SQL programming include a semicolon that is a symbol of statement termination. The semicolon is, however, not necessary on each platform. It is one of the standard parts of the SQL language. 

Insignificant Whitespace- In most cases it is ignored in SQL queries and statements. This makes it simpler for the formatting of SQL and enhancing the readability of the language.

## Inserting, Updating, and Deleting Data

In this section, the topic will be on how to add new records into a database, how to update the existing files, and how to delete the data you no longer need or use. Inserting data is one of the simplest tasks. It is because it starts with simple problems of inserting single rows. In many cases, it is, however, efficient to use set-based approaches when creating new rows. In such a case as a programmer, you will find numerous techniques that can help you insert multiple rows simultaneously. 

Similar to inserting, updating and deleting start as simple tasks. A programmer can update a single record, and delete a single record. One can as well update multiple files simultaneously using some more sophisticated methods. Similarly, there are numerous ways through which data can be deleted in SQL programming. For instance, one can delete entire rows in a table considering they are existing or not in another table. 

SQL also has new additional ways through which programmers can insert, update, and delete data simultaneously. It is one of the best features that SQL programming language can offer. 

### Inserting New Data

The problem: In this, a programmer wants to add a new record into a given table. In such cases, the programmer uses the INSERT statement when inserting data to tables. The INSERT statement is also referred to as the INSERT INTO statement. It is used when inserting one or multiple rows into tables. 

The SQL INSERT statement is used when inserting a single row into a table. Below is an illustration of the INSERT statement used in inserting one row into a table that already exists. 

      INSERT INTO table (column1, column2…)

      VALUES (value1, value1,…)

When inserting a row into a table, a programmer is required to give three specifications. One is the table in which they want to insert the new row, in the INSERT, INTO clause. Second is a list of columns separated by a comma in the table and surrounded by parentheses. The third is a list of values separated by a command surrounded by parentheses inside the values code. The list used for columns should have a similar number of elements as those in the values list. In cases where they fail to match, the SQL database engine will typically issue an error. 

An example is using an INSERT statement when inserting new rows into a shipper’s table. 

   INSERT INTO shippers (company name, phone.)

   VALUES (Alliance Shippers’, 1-680-199-6)

The two constants Alliance Shippers and 1-680-199-6 are identified in the VALUE clause. The SQL engine respectively inserts them into the company name and phone columns. After the execution of the statement, the server in the database brings back a message. That message helps in indicating the number of rows that have been affected. In such a case, the programmer gets a message that “1 row affected”. This message informs the programmer that there is one new row that has been successfully inserted. 

The shipper’s ID column is not specified in the column list. This is because the column used for the shipper’s ID is an AUTOINCREMENT column. The next sequence is automatically generated by the database engine anytime a new row is inserted into the existing table. 

SQL programming provides programmers with a shorter form of using the INSERT Statement to write lesser code. 

    INSERT INTO table

    VALUES (value1, value2,…)

When this form is applied, the list used for values is supposed to have a similar order as the list of columns present in the table. When a programmer uses the INSERT INTO statement, they are required to supply all columns with values apart from the AUTOINCREMENT column. The best thing about practising the use of column names in INSERT statements is that it helps to make code maintainable. 

SQL INSERT statement can also allow programmers to insert multiple rows into an existing table. One can add the rows using one statement. 

    INSERT INTO table- name (column 1, column2,...)

    VALUES (value1, value2 …)

In such a form, a programmer is required to provide numerous values’ lists with each list separated from the other using a comma. Below is an example of an INSERT statement used in inserting two rows into a shippers table.

    INSERT INTO shippers (company name, phone number)

    VALUES (ALL, 1-400-670-7569’)

            (DHL’, 1-400-522-5435’)

SQL INSERT statement also can be used to copy data table. Other than coming up with specifications of values’ lists, a programmer can make use of the SELECT statement in selecting values form other tables and supplying them to the INSERT statement. In such a case, the programmer can easily copy data from one particular table to another. 

It is also possible for programmers to block users or delinquent software applications from inserting new values into particular columns in a table. In this case, a programmer comes up with a view on the specific table that exposes only the columns that they wish to unearth. All inserts are then forced to pass through the view. Access is allowed to only users and software that are eligible. 

Updating Data in SQL Programming

The SQL UPDATE statement is used in updating the existing data in SQL tables. It is used in changing existing data in a single or multiple rows present in a table. Below is an illustration of the UPDATE statement. 

      UPDATE table

      SET

           Column1= new_value1,

           Column2= new_value2,

      WHERE

     Condition;

When updating data in a table, a programmer is required first to give a specification of the name of the table that they want to change data in the UPDATE clause. Secondly, assign new values for the column that wants to be updated. When a programmer wants to update the data present in multiple columns, every column= value pair and a comma is used when separating the two. Thirdly the programmer should consider specifying the rows that want to be updated in the WHERE clause. The use of WHERE clause is optional and when omitted all the existing rows in a table are updated. 

The SQL engines issue messages that specify the number of rows that are affected after the statement is executed. Below are some examples of the SQL UPDATE statements. We can use an example of an employee, Juliet having an id 3, and gets married. The employer is required to change her last name in the table. The existing record name of Juliet may be as follows:

     SELECT

          Employed, Lastname, first name

     FROM

          Alliance-ph. Employees

     WHERE

            EMPLOYEE ID

 Employee id last name first name

   3 Jolie Juliet

The UPDATE statement will help in changing Juliet’s last name from Jolie to Francis

    UPDATE employees

    SET

         Lastname- Francis

    WHERE

          EmployeeID=3

THE select statement is executed to help in verifying the change the will occur as:

 Employee id last name first name

 3 Francis Juliet

## SQL UPDATE Multiple Columns

There are cases where programmers will be required to update data existing in various columns. For instance, in the case of Juliet above, she moves to a new home after getting married. It will mean that the address filled in the original record will change. The UPDATE statement is used in the following way:

    UPDATE employees

    SET

        Address= ‘1200 Carter St’

        City= New York

        Postalcode= 4093

         Region= CA

    WHERE

         EmployeeID= 3

## Deleting Data from SQL Table

The SQL DELETE statement is used when a programmer wants to delete existing data in a table. To successfully use the SQL DELETE statement, one needs to first come up with the table where the data should be removed in the DELETE FROM clause. Then one should put up conditions within the WHERE clause to help in specifying rows that are to be removed. When the WHERE clause is omitted, every row existing in the table is removed. It is also possible for programmers to delete all rows existing in a table without necessarily deleting the table.  

# CHAPTER 5: MODIFYING AND CONTROLLING TABLES IN SQL PROGRAMMING

## Changing Tables

In many cases, SQL database tables that are newly created need to be tweaked a little. For instance, when a programmer is working for someone else, a client may come to them after the database table has already been created and request to keep track of other data items. It means that the programmer will have to return to the drawing board. When one is building databases for their use, some deficiencies in their structures may be quite apparent after the structure is created. For instance, one can get some proposals from different countries and will be required to add county columns. It is the time that a programmer needs to make some modifications to their table. 

### Simple Modifications to SQL Table Structures

SQL databases are used in storing relationships and data within tables. Changes within the tables are likely to occur from time to time. The changes cater to new or missed out requirements. All SQL tables are structured in ways that they can be modified. Modification of the SQL table structures depends on their complexity; this means that some may be easier than others. Below is a precise analysis of the change of SQL table structures.

All the SQL databases make use of the containers referred to as tables as storage of data and the relationships between these data. There are several rows existing in each table. They are also referred to as tuples where all related data is stored. Each row in an SQL database table usually comprises of columns. These columns are also referred to as fields. Each column stores original data contents. Over time the structure of the table is likely to change. In the case of a business, a supplier ID may need to be increased due to business expansion. Therefore, the number of suppliers may need to improve, and this calls for some changes on the SQL database table structure. 

Some of the standard generic modifications that are made to tables include the following.

*   Changes to the columns in the table- this can involve changing, adding or removing column types or sizes. 
*   Changes to constraints and the rules applying to the tables or the relationships among the charts.
*   Changing the values of data that are stored in the tables. This can involve, for instance, adding new records, deleting new files or changing the values of documents that are already existing. However, this does not include the modification of the SQL database table structure. 

Numerous SQL implementations provide two options that can be used in making modifications within the SQL table. One of the alternatives requires one to use SQL statements. The second option requires one to use GUI tools that are provided by SQL implementation. 

Below are some of the steps that one can follow to add new rows and enhance change accommodation successfully. A programmer should open their initial table and follow each step appropriately. 

In the window showing table-creation, one should right-click within a small, colored square on the left of the City field. It will help in selecting rows. Then choose Insert Rows from a menu that will pop up. A blank row will appear above the cursor position and will push down every row that exists. 

Second, one is required to enter the fields that they want to be added to the existing table. For instance, one can add an Address3 area above the Country and County fields. 

The final step is making sure after the modifications are done, the table is saved. This is a crucial step before closing the table. It helps in ensuring that all the changes that have been made are protected as it was required. 

The SQL ALTER TABLE statement is used when adding, deleting or modifying existing tables in SQL programming. It is also used in dropping and adding some constraints to SQL existing tables. 

The ALTER TABLE- ADD Column is used when adding columns to existing tables. The following syntax is used in the process: it is one of the most straightforward modifications that can be done on current tables. The operation is considered to be free from potential risks. This is because it is not dependent on other elements in the existing database. 

       ALTER TABLE table_ name

       ADD column_name datatype;

 When adding an Email column to a “customers” table, the following SQL is used. 

       ALTER TABLE Customers

       ADD Email varchar (255)

ALTER TABLE- DROP COLUMN is used when deleting columns present in a table. There are some databases that do not allow for columns to be removed. For those that would enable, the following syntax is used;

        ALTER TABLE table_name

        DROP COLUMN column_name;

 When deleting an Email column from an existing “customers” table, the following SQL is used.

    ALTER TABLE Customers

     DROP COLUMN Email;

ALTER TABLE- ALTER/ MODIFY COLUMN is used when changing the data type existing in a column. The SQL Server/ MS Access is the syntax used in such cases. They are applied in the following manner.

    ALTER TABLE table_name

     ALTER COLUMN column_ name datatype

Creating some changes in the field structure requires adequate preparation. This is because in cases where the specific field needs some shrinking, essential precautions must be followed. These precautions help in ensuring that data that is already existing in the field is not tampered with as a result of the changes. When numeric field formats are changed, it is possible that inaccuracy or loss of precision can be experienced. In most cases, the SQL systems send some warning if any tampering occurs and the change may not occur if it is affecting the type of data.  

## Modifying and Removing Constraints

In some databases, there are constraints or rules that are mainly defined for the tables. Therefore, this means that to make successful modifications, one needs to be adequately prepared and make some considerable plans and efforts. This is because in most cases, the adjustments being made are likely to affect the other tables as well. 

Dropping columns from existing tables can have some adverse effects on the integrity of the database. This mainly happens when the field being cut is a foreign or primary key of reference by the other tables. The process of dropping the area may be quite challenging. Overcoming it needs a programmer to be adequately prepared and follow all the necessary steps. One should also consider being well conversant with the SQL programming language to ensure they are capable of tackling every task required. 

# CHAPTER 6: WORKING WITH SUBQUERIES

In SQL programming, a subquery is also referred to as a nested query or an inner query. Subqueries are defined as queries within other SQL queries. They are customarily embedded inside the WHERE clause. 

The purpose of subqueries is returning data that will be used in the significant queries as conditions for further restricting of data being retrieved. Subqueries can be used in coordination with SELECT, INSERT, UPDATE, and DELETE statements. They can also be used along with operators such as, IN, =, <=,>=, and BETWEEN. 

There are rules that are set to be followed by subqueries. They include; 

All subqueries should be enclosed inside parentheses

Each subquery can only contain one column within the SELECT clause. This is possible unless there are many columns existing in the significant query for the subqueries to compare their selected columns. 

Subqueries that are returning multiple rows can only be used together with the numerous value operators. Such operators include the IN operator. 

The SELECT list must not include any references evaluating to a CLOB, ARRAY, NCLOB, or BLOB. 

It is not possible for subqueries to be enclosed in a set of functions.

It is not applicable for the BETWEEN operator to be used with a subquery. It is, however, possible for the BETWEEN operator to be used in a subquery. 

In most frequent cases, subqueries are used together with the SELECT statement. There are also instances when the subqueries are used along with the INSERT Statements. The INSERT statements make use of the data returned from the subqueries. This data is used when inserting into other tables. Data that is selected in the subqueries is modified using different characters, date, and number functions. 

Subqueries are also used in coordination with the UPDATE statements. One or many columns existing in a table are updated by the use of a subquery together with the UPDATE statement. Subqueries are also applicable together with the DELETE statements. In such a case, they are used in deleting records from existing tables that are no longer valuable. When the two are used together, they bring about some changes to the existing table’s columns and rows. 

There is no specified syntax for use in subqueries. However, in most cases, subqueries are used with the SELECT statements as indicated below. 

   SELECT column_name

   FROM table_name

    WHERE column_name

       Expression operator

             (SELECT COLUMN_ NAME from TABLE NAME WHERE…)

## The SQL Server Subquery

It is essential for programmers to understand SQL Server subqueries and how subqueries are used for querying data. SQL servers help in executing whole queries. In the case of customers’ tables, it first comes up with lists of customers’ IDs. It then comes up with substitution of the identification numbers that are returned by subqueries within the IN operator. It then engages in executing outer queries to help in getting the final outcomes set.

 Using subqueries can help programmers join two or more steps together. This is because they allow for the elimination of the need to select the identification numbers of customers and plug them within the outer queries. Additionally, the questions themselves adjust automatically anytime there are changes in the customer’s data. 

Subqueries can also be nested in other subqueries. SQL programming servers support over 30 levels of nesting. The SQL server subqueries are used in place of expressions. When the subqueries return single values, they are used anywhere expressions are used. SQL server subqueries are used together with the IN operator. Subqueries used with this operator usually return zero or more value sets. The outer queries make use of the values that have been answered by the central subqueries. 

SQL server subqueries are also used with the ANY operator. Subqueries that are introduced using the ANY operators usually have the following syntax:

    Scalar_expression   

    Comparison_operator ANY

     (subquery)

When the subqueries return lists of values such as v1, v2, v3, the ANY operator statement usually return TRUE if there is a comparison of one pair and FALSE when it does not. The ALL operator, on the other hand, returns TRUE in case all the comparisons made pair, and when they do not, it returns FALSE. THE EXIST operators return TRUE when subqueries return results, but when they do not, they return FALSE. 

## Creating New Databases in SQL Programming

When creating a database in SQL programming, the initial queries are responsible for the creation of new databases. One of the best examples is the Facebook application. The application contains some databases for all the following components.

 Users- This is a database on Facebook that is used as a storage for every information on the user’s profile. It stores all the details as the person uploads them on their accounts. 

Interests- The database on Facebook helps in holding various interests of the user. These interests are applied when tracking down the hobbies and talents of the users. 

Geographic Locations- This is a database that holds every city around the universe where any user live. 

The second query when creating a database is responsible for coming up with new tables within specific databases. 

## Industries That Use SQL Programming

SQL programming databases are commonly applied in technological fields whereby large amounts of data are used. Some of the most common sectors are the finance, music applications, and social media platforms industries. 

In the finance industries, SQL is mainly used in payments processors, and banking applications. They include Stripe, whereby they operate and store data involving significant financial transactions as well as users. All these processes are supported by complex databases. Banking database systems usually require maximum security. This is, therefore, one of the reasons why the SQL code applied has the highest levels and capabilities of risk compliance. 

Some of the music applications such as Pandora and Spotify also require the use of intensive databases. These databases play significant roles because they help the applications to store large libraries consisting of music albums and files. The music stored in there is from different artists. Therefore, these databases are used when finding what users are trying to look for, storing the data about particular users as well as their preferences, and interests. 

Social media platforms are other industries that commonly use SQL programming. This is because they require multiple data processing. Some of the social media apps such as Snapchat, Facebook, and Instagram are using SQL to enhance the storage of the profile information of their users. Such information includes biography, location, and interests. SQL is also applied in these applications to improve efficient updating of the application’s database anytime a user comes up with some new posts, or share some photos. It also allows for the recording of messages that are generally sent from one user to the other. By this, it helps the users to retrieve the messages posted and reread them in the future. 

## Common SQL Database Systems

The SQL database systems are typically ranked depending on the DB-Engines popularity score. Below are some of the variables that are taken into consideration during the rankings.

The number of time the system has been mentioned on websites. This is measured in terms of the outcomes in queries on the search engines. 

The general interest within the system. This considers how frequently it has been searched in Google Trends. 

The frequency of technical discussions on the particular database system. 

The number of job offers through which the database system has been mentioned. 

The number of profiles existing in professional networks whereby the system has been mentioned. 

## The Relevance of the Database System to Social Networks

1\. Oracle Database

This is the most common SQL database system used all over the world today. Numerous industries are using it in their operations. It is, however, commonly used in the processing of online transactions and data warehousing. 

2\. MYSQL Database

It is one of the open-source database systems in SQL. It is freely available to businesses and individuals. Sit is popularly used by small scale businesses and startups. They commonly use it because it does not have a license fee. It is also used in multiple applications and software programs that are open-source in nature. 

3\. Microsoft SQL Server

The SQL Server is Microsoft’s modified database management system. It is used in the running on all main versions of the Windows operating systems. It is also used in the consumer software and web servers running on Windows. This means that the Microsoft SQL server has an extensive user base. 

4\. POSTGRESQL 

It is also a free open source database system. It is commonly used in multiple industries due to free license models. 

# CHAPTER 7: COMBINING QUERIES IN SQL

SQL designed to manage relational databases; equally, SQL is used to create queries from the clients’ program to the database. You may want to query from more than one table to develop one set of records. You can achieve this through a union query.

However, for one to comprehend union queries, there is a need to understand the basics of designing queries, perhaps in Access or other databases. In the Microsoft office, there is a database that is shipped with Ms. Office suite. You may look for the Northwind Access template to help you understand the basics of designing queries.

After you open the Northwind database, you will be prompted to log in, dismiss the dialog, and expand the navigation pane. For you to be able to organize the database as per their types, proceed by selecting the Object type. Next, you will have to expand the Queries group, where you will note a query named Product Transaction.

For you to identify the union query, check for a special icon of two intertwined circles. The symbol represents a union of two sets. However, Access graphic queries cannot be united since the tables are not associated with a union query. This is evident when you open union queries from the navigation pane as Ms Access opens it in a datasheet view. In a normal Ms. Access interface, on the home tab, there are two major functions; design view and datasheet view. However, when working with union queries, the datasheet view is not available. Therefore, you can only switch between SQL view and Datasheet view.

For further learning about basic designing of queries, and eventually, how to work with union queries, click the Home function in the Ms. Access interface, then views, and lastly, SQL view to see the SQL syntax that defines that particular union query. Below is an example of SQL syntax of union query as it is in the Northwind database:

SELECT [Product ID], [Order Date], [Company Name], [Transaction], [Quantity]

FROM [Product Orders]

UNION

SELECT [Product ID], [Creation Date], [Company Name], [Transaction], [Quantity]

FROM [Product Purchases]

ORDER BY [Order Date] DESC;

The first and second statements are literally two distinct queries. These queries retrieve distinct sets of records, one fro, product purchase table, while the other from the product order table. The word UNION between the two statements shows that the two queries will be combined to make them a union query. In the last part of the syntax, the term ORDER BY determines the ordering of the united records. For instance, in this syntax, the abbreviation DESC means all records will be ordered by the Order Field in descending order.

## How to Create Union Query by Creating and Uniting the Select Queries

It is possible to create union queries by coding the syntax of the union syntax in SQL view. However, it is much easier to develop it in parts with select queries. After developing the independent select queries, you can later copy and paste the SQL parts into the joined union query. Below are the steps of creating a union query by uniting the select queries.

1.  In the file menu bar, select create> quires group> query design.
2.  Double click the table that has field want to include in the show table. The selected fields will be added to the windows query design window.
3.  Now close the Show Table dialog box.
4.  While in the query design window, double click individual fields to be included in the query. However, ensure to add an equivalent number of fields to each of the select queries, in a similar order. Secondly, ensure the data types in the corresponding fields are compatible with the data you are dealing with and to those of the select queries to be combined with.
5.  Although this is an optional step, you may add criteria to the fields by entering the suitable expression in the Criteria row of the particular field.
6.  After making sure to have checked all the attributes of the field by checking the data type and, perhaps, adding the field criteria click Design> Results> Run. This will help you to preview the output. Switch the query to the Design view.
7.  If the previewed results are as per your wish, save the PostgreSQLselect query.
8.  Without closing the windows for the previous select query, repeat the above steps to each of the select queries you wish to combine.

When you are through with creating the select queries, now you will have to combine them to make the union queries. Below are the steps of combining your select queries to form a union query.

1.  In the file menu bar, select create> quires group> query design.
2.  Close the Show Table dialog box.
3.  Click Design> query group> union. This will hide the query design window and display the SQL view object option. However, you should note that, at this point, the view object tab will be empty.
4.  Select the tab of the first constituent query of the supposed union query.
5.  Click home> view> SQL view.
6.  Copy the SQL syntax of the select query and paste it in the tab for union query opened in step 3.
7.  Each of the select queries has semicolons at the end of the individual syntax, which you should delete.
8.  Punch the Enter button on your keyboard to start a new line and type the word UNION.
9.  Repeat steps 4 to 8 until you have included all the select queries that you wish to combine. However, DO NOT delete the semicolon of the last select query’s syntax.
10.  Click Design> Results> Run. This will give you the output of the union query in a datasheet view.

## An Example You Can Recreate the Northwind Sample Database

In this example, the union query will collect a combination of names of people from the Client table and names of people from the Distributors table. Below are the steps to accomplish this task.

1.  Start by creating two select queries, Query 1 and Query 2, and name them client and distributor as data sources. Use the First name and Surname field to display the values.
2.  Secondly, create another query, Query3, with no data source.
3.  Click Design> Union and make the latter query, Query three, into Union query.
4.  Finally, copy and paste statements of the selects queries, Qyery1 and Query2, into Query 3\. Recall to have the semicolon only at the end of the syntax and to add the word UNION between the sentences. You may, at this point, check the preview in the datasheet view.
5.  Add to one of the queries in an ordering clause and then paste the ORDER BY statement into the SQL view of the union query. Note that in Query3, when the order is to be appended, the union query first removes the semicolons, then the name of the table from the field names.
6.  Your final findings of the combined query should be as follows:

SELECT Clients.company, Clients.[Last Name], Clients.[First Name]

FROM Clients

UNION

SELECT Suppliers.The company, Distributors.[Last Name], Distributors.[First Name]

FROM Distributors

ORDER BY [Last Name], [First Name];

If you are very comfortable writing SQL syntax, you can write your own SQL statement directly to the SQL view for the union query. Nonetheless, using the method of copying and pasting SQL from other database objects, you may find it useful and easier. That request can be much more complex than the simple examples used here for choosing queries. Creating and testing each query carefully before combining them in the union query can be to your advantage. If the union query is not working, you can change each query individually until it is efficient and restore your union query with the corrected syntax.

# CHAPTER 8: BASIC SQL MATHEMATICS AND STATISTICS

The basic entities for data science and machine learning are mathematics and statistics. Most of the known and productive data scientists come from one of these areas— informatics, applied mathematics, and statistics, or economics. If you want to excel in data science, you need to have a clear understanding of basic mathematics and statistics.

Nevertheless, studying mathematics can be daunting for people with no interest in mathematics. Next, you need to decide what to study and what not to test. Linear algebra, calculus, probability, statistics, discrete math, regression, optimization, and many more topics can be included in the list.

If you have never been in this field, worry not for this literature will take you through each bit on the same. Here is a list of famous open courses on Coursera, edX, Udemy, and Udacity's data science mathematics. The list was carefully curated to provide you with a standardized path to teach you the necessary mathematics concepts used in data science.

It takes a lot of brainpower and understanding to turn raw and quantitative data into structured and insightful knowledge. It's true that not everyone can be like Aryabhatta, the earliest mathematician; however, you should be strong, concentrated, and committed. With concentration, commitment, and passion in mathematics and statistics, now you just require dedication and hard work to start learning.

Mathematics and statistics are essential disciplines in learning Data Science. Most of the analogies and concepts in Data Science are drawn from the two disciplines. Below is a brief discussion on the different concepts in this field that create data science and its practical uses.

## Mathematics and Statistics for Data Science

In today's world, data science has become a phenomenon in engineering. You need to strengthen your knowledge of mathematics and statistics to learn data science.

### Mathematics for Data Science

In most of the learning subjects, Mathematics has had much of the domination. The extent to which mathematics is used varies depending on the disciplines. Basically, mathematics can be grouped into two components, namely Linear Algebra and Calculus; these components are part and parcel in Data Science. Below is a brief review of these two fields. In this section you will learn how mathematics contributes to the study of data science.

1\. Linear Algebra

Linear algebra is the leading topic in data science. Linear algebra is widely used for recognition of images, text analysis, and also reduction of dimensionality. For instance, can you differentiate a dog from a cat? Yes, you should, of course! The reason being our minds have been conditioned to distinguish dogs from cats since birth. We use our intuition to gain insights into the information as a result.

But what if you need to design an algorithm that can be used to classify cats and dogs? This task is called classification and is the most popular machine learning application. As a matter of fact, through linear algebra, the machine can identify the images of cats and dogs.

The use of matrixes is the primary way of storing images. Therefore, linear algebra, which is the most important component of matrices, is highly regarded. Linear Algebra is intended to solve linear equation problems. These equations may contain variables of higher dimensions. It is not possible to imagine or manipulate these higher dimension variables. Therefore, we apply matrix power to help us in manipulating n-dimensional data. Three forms of matrices exist –

*   Vectors – single-dimensional matrixes.
*   2-Dimensional Matrix – two-dimensional matrixes; n-rows and n-columns.
*   Scalars – their order is much greater than two.

Techniques that use Linear Algebra in Data Science

It is essential to note that there are other types of matrices, whose importance cannot be despised, such types include inverse matrix and those of operations such as matrix transposition. Below are the essential techniques used in creating solutions using linear algebra in data science.

Single Value Decomposition – Decomposition of Singular Value helps you to manipulate matrices by separating them into three separate matrices. Scaling, rotating, and shearing of these matrices.

Eigenvalue Decomposition – Decomposition of the original value helps you to simplify the operations of the matrix. This technique is of help in generating new vectors in the same direction as the former ones. Further, the matrix is decomposed into eigenvalue and eigenvectors

Principal Component Analysis – They use the Principal Component Analysis to reduce higher dimensions. It is most commonly used to reduce dimensionality, which, literally means, reducing the number of variables or measurements without elimination of correlated tags.

2\. Calculus

Calculus is a very important element in data science. Calculus is used primarily in techniques for optimization. It is indisputable that it is close to impossible to learn data science without a primary knowledge of algebra. Calculus enables operations such as performing artificial neural networks, mathematical modeling, and increasing their accuracy and efficiency too. The measurement can be divided into –

2.1\. The Differential Calculus

This is the study of the rate of change in the quantity. Derivatives are most widely used to determine the function maxima and minima. Derivatives are applied in techniques of optimization where we need to find the minimum value by minimizing the error function.

Another crucial derivative definition every learner should know about is the partial derivative that is used in neural networks to model back-propagation. Another important concept used to measure back-propagation is chain law. I addition to reducing functions and back-propagation errors, Generative Adversarial Neural Networks differential game theory is applied.

2.2 The Integral Calculus

This refers to the mathematical analysis of quantity accumulation and the field under the curve to be found. Therefore, integrals are classified into certain integrals and indefinite integrals. The operation of integrating is commonly used in calculating functions of probability density and random variable variance. Another important entity that makes use of the integral calculus is the Bayesian Inference.

Upon recognizing the key mathematics subjects, it is equally important to study some of the important data science statistics concepts –

### Application of Statistics in Data Science

Statistics refers to the operation of collecting, evaluating, visualizing and interpreting the information. This uses statistics to turn raw data into observations that make up the data goods. The raw data is managed and let companies make careful choices that are guided by data. Statistics provides a variety of resources and features that can help you discover a massive amount of data.

In addition, by summarizing and making inferences on data, you can develop a deep understanding of data with statistics. With regard to these two terms, the statistics are divided into two –

*   The Descriptive Statistics
*   The Inferential Statistics

1\. The Descriptive Statistics

To explain the results, descriptive statistics or summary statistics are used. This deals with numerical information analysis. The analysis is achieved by means of diagrams and graphical representations. For one to have a reasonable comprehension of descriptive statistics, it is essential to understand the following concepts:

1.1 Normal Distribution

Here, a large number of data samples are represented in a plot. Equally, there is describing large values of variables in a bell-shaped curve using the normal distribution, also known as a Gaussian Curve. The bell curve is symmetrical in nature, expressing that the values are similarly off in both the left and the right directions farther away from the mean taper. For an accurate undertaking of inferential statistics, it is necessary that the data be normally distributed.

1.2 The Central Tendency

Here you identify the central point of the data using a central tendency. Mean, median, and mode are the three primary components of central tendency. Mean is the mean arithmetic of all sample data values. On the other hand, the median is the mid-value of data (arranged in ascending order). Lastly, a mode is the sample's most frequently occurring point.

1.3 The Skewness & Kurtosis

There may be data instances where there is no symmetry in the distribution. A Gaussian curve, for instance, has zero skewness. Whenever data accumulates on the left side, the results are referred to as positive skew, while the contrast implies a negative skew.

The kurtosis tests the graph's "tailedness." From tailness, we conclude that in either of the graph's tails, kurtosis tests extreme values. Essentially, large-scale kurtosis distributions have tails larger than normal distributions; on the other hand, a negated kurtosis has smaller tails than normal distributions.

1.4 The Variability

As the name suggests, it is the measuring of the distance of the data-point from the central mean of the distribution. However, there are various measures of variability, such as range, variance, standard deviation, and inter-quartile ranges.

2\. The Inferential Statistics

It is the process of the data being inferred or concluded. By carrying out several tests and deductions from the smaller sample, we draw a conclusion about the larger population by inferential statistics. For example, one may wish to know the approximated number of people who support a certain political party in a survey. The aim is to collect the views of the people, right? However, this method is simply not suitable, because in a country with billions of people, and surveying each of the citizens is a curb some task. As a result, a smaller sample will be taken, and conclusions are made from that sample; thereafter, the findings are attributed to the larger population.

Inferential statistics, there are different methods that are useful for data science. Some of these are methods –

2.1 The Central Limit Theorem

The mean is equal despite the size of the data; a smaller sample has a mean equal to that of a larger population in a central limit theorem. The actual standard deviation is, therefore, equal to the population standard deviation. The calculation of population means is an important technique of the Central Limit Theorem. Equally, the margin error is equal to the product of the average standard error and the percentage of trust level z-score.

2.2 The Hypothesis Testing

Hypothesis testing refers to the hypothesis calculation. We assign findings from a smaller sample to a much larger group using hypothesis testing. We need to test against each other two hypotheses–the Null Hypothesis and Alternative Hypothesis. The optimal scenario is represented by a null hypothesis; contrarily, an alternative hypothesis is usually the opposite of that which we try to prove correct.

2.3 ANOVA

Checking the hypothesis with multiple groups is done using ANOVA. It is an improvement in another type of an inferential t-test technique. ANOVA conducts the test with a minimum rate of error. An f-ratio is called a metric for measuring ANOVA. F-ratio is the intergroup mean-square ratio or intergroup mean-square.

2.4 The Qualitative Data Analysis

This type of analysis is made up of two main approaches–correlation and regression. By definition, correlation is the test that involves finding correlations between random variables and bi-variant data. On the other hand, regression is another form of analyzing qualitative data. In regression, the relationship between the variables is estimated. There are straightforward regression and regression that is multi-variable. Also, we have a non-linear regression if the function is non-linear in nature.

Briefly, the above discussion is on various data science and machine learning computational and numerical criteria. Therefore, the widespread use of linear algebra in computationally complex tasks has been addressed. Equally, calculus and its use to reduce mathematical models' loss function have been addressed. Additionally, a brief study of how descriptive and inferential statistics are essential in data science was made. Ultimately, we conclude that data science mathematics and statistics are mandatory requirements in data science, for instance, in SQL programming.

# CHAPTER 9: SAVING TIME WITH VIEWS, FUNCTIONS, AND TRIGGERS

Arguably, for all business requirements, one strategy is not exclusively the best solution. Therefore, explanations will be made in the next few parts of the key issues to be put into consideration when settling on one solution over another. Often you will find that a combination of methods works best even in a single application.

## Best Practices and Approach for One to Achieve a Goal

It is necessary to figure out what you are trying to achieve before choosing one approach over another and then decide how using one approach matches your set objectives. The downside of such a concept is that it gives one a feeling that because it is always right, there is no need to doubt a method. Only follow the best practices outlined in the topic by an expert, and things are going to come into place, eventually. Instead of just focusing on best practices, I would suggest that you think about what they are trying to achieve and why one approach is better to get there than another. Therefore, in your consideration, have priorities based on the goal. In this section, we will discuss considerations at a functional level that is very elementary rather than a level of macro applications. Arguably, it is important to view each of an application's operational tasks individually rather than assuming the wholesome of the application. For instance, it may occur that one component of an application that needs to communicate to a mainframe server or run scheduled tasks; however, it does not make sense to drive the entire application structure based on the need for this one-time feature. Therefore, when making your consideration, answer the following questions:

*   Does this feature have to work in different database types?
*   Is this feature used in several system sections or applications?
*   Does this feature require multiple arguments and return one set of values as a single table or as a scalar value?
*   Does this feature allow a few arguments to be transferred to the server, but does it require a lot of database information to get results?
*   Is the information-intensive or minimal processor function? For example, is it an encryption function or the product of a complex query, or is it more SQL-intensive or more procedural-intensive?

• Are the function parameters consistently the same, or do they vary? For example, a complex search form will not always have to pass the same criteria, but a simple search form will only have one search field and always pass it.

• Is the function page requiring long SQL statements batches, or is it a single line SQL statement?

• Are the result fields always the same or need to be varied? For example, are you always joining the same set of tables that vary slightly depending on the need for different fields or data sub-sets?

## Database Objects

It is very amusing that when people talk about the logic of databases, they are very focused on stored procedures when, literally, there is almost nothing else. Whether these people have ever interacted with modern systems is still unclear. One of the oldest methods of encapsulating database logic is stored procedures, but they are not the only method available. Nowadays, most relational databases have views, restrictions, referential integrity with cascading updates, remove, stored functions, triggers, and the like. When used properly, these are extremely powerful devices.

The discussion below will cover stored procedures and the other types of database objects in the next couple of sections while describing each of the strengths and weaknesses to encapsulate logic. For each feature ‘0’, we will assign a score of 0-5, meaning that the feature is non-existent, 5 meaning that this object is one of the most suitable objects for this type of mission.

### Stored Procedures

One of the available methods for encapsulating database logic in the database is through stored procedures. These procedures are similar to regular programming language procedures, which, by arguments, do something, and sometimes return outcomes. However, at times, they even modify the values of the arguments they take when arguments are declared as output parameters. The similarity can be easily drawn considering they can return data; nevertheless, stored procedures cannot be used in queries. Because stored procedures are declared as OUTPUT by the process of taking arguments; therefore, they can return more than one output.

### Stored Functions

Except in three major ways, as discussed below, stored functions portrays similar attributes to those of stored procedures.

1\. These can be used in views, stored procedures, among other stored functions, as opposed to stored procedures.

2\. It is prohibited to change data on many servers or have DDL / DML limitations.  This is not valid for databases like PostgreSQL, as the distinction between a stored function and a stored procedure is very gray.

3\. Generally speaking, they cannot take output arguments (placeholders), which are then passed back with modified values.

### Views

Among the function that was received with ululations in the technology field are views. The key advantage of view is that in most cases, it can be used as a table; however, unlike a table, it can encapsulate very complex calculations and widely used joints. Except for stored procedures, it can also use practically any object in the database. Views are most useful when you always have to enter the same set of tables in order to get overview calculation fields, say an order with an order description.

### Triggers and Rules

Triggers are entities usually linked to a table or view that run code based on certain events, such as data initialization before data is added, updated/deleted, and before such events occur.

Triggers can be great things and, at the same time, very dangerous. Dangerous in the sense that, triggers are difficult to debug but strong because the device can easily escape no change to a table with a click.

These are useful for ensuring that certain events often happen while adding or modifying data-e.g. setting complex field default values, inserting record logging into other tables.

Triggers are particularly useful for a particular situation, which is to be applied rather than logic. As we said earlier, for example, most views that include more than one table cannot be modified.

Nevertheless, in Database Management System such as PostgreSQL, you may establish a rule on a view that happens when someone attempts to modify or insert it into the view, and instead of inserting it will occur. The rule can be quite complicated and can set out how, in such a case, the tables should be modified. With INSTEAD OF triggers, MS SQL Server, and SQLite, you are let to do something similar.

Note that the term rule in DBMS is somewhat confusing because it means quite different things.

For example, a rule in Microsoft SQL Server is an obsolete concept used to define tables’ constraints. A rule is very similar to a trigger in PostgreSQL except that it is not triggered per row event and is specified without a handling function being needed.

### Foreign Key Constraints, Primary Key Constraints, Referential Integrity, Cascade Update/Delete

No constraints, referential integrity, and cascade update/delete, there should be no true repository. Using SQL DDL statements or a relational model, you can describe them. The use of these tools is limited, but with other database objects, the purpose they serve cannot be easily replicated. Two main purposes served by these tools are:

• Provide a database declarative template, and how the data are interrelated, a resource for self-documentation.

• Make sure you are not wrong in your coding to do something dumb to break your pattern. If your design is good, a mistake in your programming logic can signal errors in your code. If you get errors in your programming logic, test the sound of your template.

# CHAPTER 10: SQL EMBEDDED JAVA PROGRAM 

Computers work by utilizing instructions that they receive from people. The different forms of instructions that computers process are called programming. Programming has two essential components: data and explanation of instructions. Computer instructions are written by programmers who apply computer language. There are different kinds of computer languages. For instance, there is Java, Ruby, and HTML. The initials SQL stand for Structured Query Language, which assists in database management. This piece evaluates the various aspects of SQL language, including its brief history, its core elements, and why SQL is embedded with Java program. Additionally, the article highlights and explains some ten common mistakes during SQL programming and how to avoid them. Finally, the article tackles on built-in functions and calculations of SQL.

## Overview and A Brief History of SQL

The primary role of SQL is to manage different relational databases and assist in performing different computations on the information. IBM created the SQL program in the 1970s which they called SEQUEL. After sometimes, Microsoft and Oracle started applying for the SEQUEL program. After using the language for sometimes, industry players changed applying the term SEQUEL and started using SQL. One of the fantastic features of the SQL program is the fact that it's an international standardized language which facilitates communication in different databases. This means that this program can permit the implementation of any language like PHP in connection with any particular database including MS Access, MySQL and others.

 SQL programming has different features. These include:

1.  High Performance- SQL programming offers unique and powerful abilities to handle massive databases which are highly used. The programming offers different methods of data analysis and interpretation.
2.  Availability- SQL programming is friendly to various databases including HANA, MS Access, Microsoft SQL and others. Because most of these databases support SQL programming, it is simple to create additional procedural functions when they apply the language. This feature makes SQL a powerful programming language.
3.  Scalability- SQL is highly flexible meaning that you can apply or drop previously formed tables in any database.
4.  Vigorous Transactional Support- SQL programming enables you to deal in massive records and large transactions.
5.  Data Security-SQL programming permits access to tables, processes and views. This means that the security of your data is enhanced.
6.  Flexible Applications-SQL enables programmers to access databases. It's used for both small and big organizations.
7.  Data Management Commands-SQL programming is applied in different data management systems. The program uses standard commands including select, create, insert, delete and others. These standardized data management commands make the program the best when handling vast amounts of data.

Java Language

Java is one of the well-liked programming languages that is used on different devices. The language is quick, safe and dependable. The java language is object-oriented. The java language is written once but operates anywhere. This means that the Java code is applied in any operating system.

Java language is object-oriented programming which enables breaking down of a complicated problem into smaller manageable ones by forming objects. Java has different features, including:

1.  Quick-Although the early versions of java were slug, the current ones are fast. In case you're looking for a fast object-oriented programme, you need to consider java.
2.  Safety-The language has a variety of features that makes it safe. These include automated memory administration, provision of safe communication by offering privacy and security of information, and the java platforms are secure in creating and operating applications.
3.  Large Standard Library-Java is a popular program because it has a substantial standard library. The programme has different methods and classes that are essential for any developer.
4.  Excellent Performance- Java is designed to perform highly. The language utilizes bytecodes which are compiled by the compiler. After undergoing the aforementioned procedure, it is passed through a java virtual machine and converted into machine-level code thereafter. All these procedures make the language great.
5.  Object-Oriented- Java language is completely object-oriented. It has various features that make it a pure object-oriented program. These include polymorphism and abstraction.
6.  Simple to Use-Java language is simple to learn and understand because of its easy syntax. This makes it the best language for any learner.

## Benefits of Java Programming

Java programming has the following advantages:

1.  Simple to Understand-Java language doesn't have any complications and is simple to learn. In case you're new to computer programming, this is the language to start with.
2.  Performance On Any Network-Java programming is applicable in any of the operating systems like Linux. The language does not change whenever it's applied in any operating system.
3.  Security-Java has a highly secure environment where viruses, worms and phishing cannot be condoned.
4.  Reliable-Reliability is an essential aspect of any computer programming. Java is a trustworthy program because it can detect any problems before its installation. This enables you to collect them on time.
5.  Performance of Multiple Jobs- Java enables you to perform many tasks at the same time. This is because it's multithreaded computer programming. You can apply it to both pictorial and network programming.
6.  Dynamic-Java classes are kept in different files and fed into the java interpreter when the occasion demands so. The programme can expand its functionality by choosing the classes it needs.
7.  Pocket friendly- Java is an open-source programme. This means that you don't need to pay for its license annually. In case you want to minimize the costs of operating business, this is the best programming language to choose.

### The SQL Embedded Java Programme

An embedded database implies that the database is mixed and cannot be separated from the computer programme. Embedding assists in the development of different devices, including mobiles phones and specific parts of vehicles. The SQLJ is a programme that enables the integration of SQL statements into the java programmes. The SQLJ is essential because it allows the confirming of the syntax of SQL statements during conversion.

In ordinary situations, when interacting with Java information, you use JDBC. JDBC is an excellent method when interacting with flexible queries. However, when interacting with static statements, SQLJ is the best approach.

## Benefits of SQL

Embedding SQL and java programming has various advantages. These include:

1.  The programme is more compact-this is because it offers a shorter syntax compared to JDBC programme.
2.  Error checking-SQLJ programming is able to detect issues at the beginning and arrest them. JDBC, on the other hand, doesn't check for any mistakes before runtime. Checking errors at the beginning is crucial because it assists the programmer to avoid them 
3.  Comprehensive- SQLJ programme is built to make it ease in accessing many types of facilities. Examples of these facilities include queries, transaction administration, and others. Ac
4.  Data independence- SQLJ programming has three ways of ensuring that there is data independence. These include SQLJ is data neutral, the computer programming makes it possible for consortium members to share a familiar translator and the SQLJ code is standard. These features make it possible for an SQLJ to access any database that applies SQLJ.
5.  Vendor-specific customization- SQLJ programming enables the application of vendor-customization specifications. The programme has profiles that are meant to explain the SQL running. These profiles can be applied in the creation of customized vendor-specific applications. There are two kinds of customizations: profile customization and customization to access specific features.
6.  Flexible deployment-SQLJ produces a java code which can be applied in any standardized java machine. This enables the natural division of SQLJ programmes in different tiers without changing the code. 
7.  SQLJ Productivity-SQLJ can be applied by any professional who is involved in programme development. The programme is used when dealing with static programming activities. Therefore, the programme is relevant to SQL tasks as they're static in nature. SQLJ enables java users to be productivity by applying SQL programming and avoiding data programming.
8.  Brevity of commands- SQLJ commands are brief when compared with JDBC.

## Disadvantages of SQLJ Programming 

1.  Requires a pre-processing step-this makes waste the time of a programming developer.
2.  Some IDEs lack SQLJ support-this can be stumbling block for programmers who want to apply for the programme.
3.  Oracle 12.2-it does not support SQLJ in its database.

## Requirements for LQLJ

Before applying SQLJ, you require the following:

1.  SQLJ Translator-this converts SQLJ files into java.
2.  Java compiler-the java compiler should be friendly with JDK.
3.  SQLJ runtime classes-the SQLJ has different packages like sqlj.runtime.

## Development Goals of SQLJ

SQLJ computer programming was developed by Oracle. The programme aims are as follows:

1.  Accessibility of static data-SQL is static data. Therefore, the developer of SQLJ wanted to build a programme that allows the accessibility of the static data.
2.  Independence of semantics and syntax locations-this is because the two features do not rely on the configuration in which the programme operates.
3.  Group of vendors-This SQLJ programming supports specific groups of vendors. The vendors are willing to embrace the program's support.

# CHAPTER 11: COMMON ROOKIE MISTAKES

Although SQL is a simple computer programming language, you may find it hard when working with massive data. It is essential to ensure that you write high-quality statements before you start working on moderate and huge tables. As you engage in writing your statements for various sites, you need to avoid the following mistakes:

1.  Primary Keys-Primary keys are essential when working with each of the SQL tables. The primary keys are used to identify rows in a table. You'll not produce impressive work without the keys. The primary role of these keys is to quicken queries. Having the primary key should be the first step when handling relational databases. It's essential to ensure that you apply a primary key in all the tables that you form.
2.  Repetition of Data-Repetition of the same set of data in different tables is referred to as data redundancy. It's essential to ensure that each table has different kinds of data set and avoid repeating it. To ensure that you don't repeat the same data in different tables, it crucial that you abide by normalization rules. If you repeat, you create confusion. For instance, you may have a table that has a client's mobile number. Since the mobile number belongs to the client, it can quickly identify them. It'll be wrong to create an order table and add the client's mobile number again. To avoid this mistake, it's essential to store your data in a single location and apply relationships existing between the primary and foreign key in handling your data.
3.  Use Join- Many programmers commit a mistake of applying statements that are poorly optimized. It's essential to desist from using statements like: NOT IN and IN. Although these statements are convenient, you can easily avoid them and apply JOIN instead. Using JOIN ensures that your data is optimized.
4.  Forgotten NULL vs Empty String Value-You have the choice of either using the NULL or apply actual values like nil. However, it's vital to ensure that you retain uniformity in the database.
5.  The asterisk character in SELECT statements-To ensure that there is standard performance and safety; you must define and identify the sections that you need to return when querying.
6.  Avoid Using Too Many Cursors- Use of too many cursors when performing your SQL is bothersome. It's essential to desist from applying too many loops when undertaking your SQL procedures. Although loops are a common feature in programming, they're ineffective in SQL. Instead of using them, you can apply effectively presented SQL statements. In case you occasionally use cursors, it's important to minimize them.
7.  Data Mismatches-Upon establishing your table columns, it's crucial to provide a data type to all of them. The data type must contain all the information that you need to keep there. The definition you give to each table column should guide you in determining the info that you need to store therein. For instance, table columns that are meant to store decimal information should not be used to store integers. In case you store a different set of data in a column instead of the one defined, you may mess up your database. At the outset, it's essential to determine what you want to store in each table column ensure that you actually keep it as defined.
8.  Using of AND and OR operations-Sometimes, you may fail to adhere to a logical order when writing your queries. The way you apply the AND and OR statements may change your information. It's essential to apply the right parenthetical structures or arrange your statements in the right pre-determined sequence.
9.  Selection of Wrong Database-Upon establishing your SQL, it is crucial to choose the right database from the window. To avoid this mistake, you must always check the database that you've.
10.  Spelling Mistakes-SQL is a machine language and may be harsh if you misspell the words. For instance, instead of typing the word SELECT you write SELCT. You need to desist from making this mistake by ensuring that you type the words correctly using capital letters. You also need to create borders that separate your main words from other words and table columns.
11.  Missing Brackets and Single Quotes-These grammatical structures are applied many times in SQL programming. They come in pairs. The errors that many people make is that they either forget using these structures or don't apply them properly. For instance, you may use an opening bracket {( } and forget the closing one {)}. SQL also requires that you enclose text figures in single quotes. In case you don't have a quote, SQL may not understand where your text starts and stops. To stop committing these mistakes, it's essential to remember that brackets and quotes come in pairs and always observe this rule when dealing in them.
12.  Commas and Semi Colons-These punctuation marks are applied in SQL for different purposes. Whereas commas are used when separating lists, semi-colons are applied to signal to end of an expression. To avoid these mistakes, ensure that you place a comma in the front. Semi-colons are optional and may or may not be used.
13.  Failure to Review Your Data Model-The data model that you build determines how the users access your information. It's essential to think of the kind of model that you require and the simplicity with which your users access it. Failing to determine the model that you need attracts complicated queries and complex codes as you progress with your work. To avoid these mistakes, it's essential to have a print out of the data model that you want. You can also invest in a data modelling tool that can help you. When you use either a printout or a modelling tool, you determine what you might not want in your database and avoid it on time.
14.  Failing to Determine the Right Logic-You've two kinds of logic when performing your SQL: cursor and set-based logic. You need to determine the best form of logic which satisfy your needs.
15.  Discarding Old Techniques-Some programmers avoid applying old techniques because they think that they're no longer helpful. In case you want to avoid any unnecessary errors, it's essential to apply the old tested and tried techniques. Avoid rushing to embrace new tactics that you lack much information concerning them.
16.  Avoiding Peer Review-Consulting a knowledgeable person to review your query plan is essential before you deploy it. The reviewer may discover some few things that may have escaped your attention. You'll also benefit from the suggestions and comments of the reviewer.
17.  Failing to Test Queries-Many developers avoid testing their queries due to a variety of reasons. For instance, they claim that testing is thorough and may not have the time to do so. However, it's essential to acknowledge that testing is a vital process in coding. You need to ensure that you have rigorously tested your code and it apes the final production environment.
18.  Not Minding Your Syntax-Syntax means the way words come together to form phrases and sentences thereafter. In case you don't arrange your words well, you'll not make a sensible statement. Likewise, in case you don't apply the right syntax your database may not understand what you're saying. This may result in poor performance.
19.  Assuming That Your Clients Understand What They Need-When clients call you, do not assume that they fully understand their database problem. It's essential to let them know that you're a professional in that area and you'll assist them in discovering the problem and fixing it.
20.  Project Scope-Some rookie SQL programmers fail to demand an adequately documented project scope from the clients. Due to this mistake, clients keep adding more tasks on top of the first ones that make the work enormous but poorly paid. Before you embark on any SQL project, it is essential to ensure that you sign a contract that captures all the tasks that you're required to offer. Any additional task that is not captured in the contract must attract an additional payment.
21.  Nontechnical Aspects of The Project- Before you commence any SQL writing project, it's vital to consider other nontechnical factors that may impact on how the project is delivered. Factors like politics and business environment may have any impact on the way the SQL project is delivered. You need to enlighten yourself on some of these factors before you start delivering it.
22.  Avoiding Feedback- Although you'll be inclined to listen more to the managers who offered you the job; it's equally important to listen to the end-users of the programme. So, apart from listening to managers, it's also important to listen to the users of the programme like the clerks.
23.  Reviews-Some rookie programmers may avoid selecting a professional reviewer to offer them essential suggestions about the programme design. Before you begin the project, you need to identify a reviewer who can provide helpful tips on how to improve it.

# CHAPTER 12: BUILT-IN FUNCTIONS & CALCULATIONS

In regard to SQL, a built-in function can be defined as a portion of programming that accepts zero or any other input and returns an answer. There are different roles of built-in functions. These include the performance of calculations, obtaining of the system value, and application in textual data manipulation. This part aims at examining the various SQL built-in functions, categories of functions, pros and cons of functions and types of built-in functions.

## Types of SQL Functions

The SQL functions are grouped into two groups: aggregate and scalar function. Working on Group by, the aggregate functions run on different records and deliver a summary. Scalar functions, on the other hand, run on different records independently.

These are as follows:

1.     Single Row Functions-They provide a one-row return for any queried table. They are found in select lists, START WIH, WHERE CLAUSE and others. Examples of single-row functions include numeric_, data_mining, Datetime_, conversion_ and XML_functions.

2.     Aggregate Function-When you apply this kind of function, you see a single row returns based on different rows. The aggregate function exists in Select lists, ORDER BY and HAVING CLAUSE. They go hand in hand with Group By Clause and SELECT statements. Many of them do not take attention to null values. Those that are usually used include AVG, EANK, MIN, SUM and others.

3.     Analytic Function-They are used to compute an aggregate value that are found on specific groups of rows. When you run this function, it delivers many rows for every group. The analytic functions are the last one to be run in a query. Examples of analytic functions include analytic-_clause and Order-by-Clause.

4.     Model Functions-These are found in SELECT statements. Examples of model functions include CV, presentv and previous.

5.     User-Defined Function-They are used in PL/SQL to offer functions that are not found in SQL. They mostly used in sections where expressions occur. For instance, you can find them in select list of Select statement.

6.     SQL COUNT Function-It is used to provide the number of rows in a table.

## Categories of Functions

Functions are classified according to the role they play on the SQL database. The following are some of the function categories available:

1\. Aggregate Functions-They do a calculation on a specific set of values and deliver a single value. The aggregate values are used in the SELECT LIST and HAVING clause. The aggregate functions are referred to as being deterministic. This means that they return the same value when running on the same input value.

2\. Analytic Function-They calculate an aggregate value according to a group of rows. They return many rows for different groups. The analytic functions can be used to perform different computations like running totals, percentages and others.

3\. Ranking Functions-They provide a ranking value for each portioned row. These kinds of functions are regarded as nondeterministic.

4\. Rowset Functions- They're used to return an object that can be applied.

5\. Scalar Functions-They work on a single value to return the same. There are various kinds of scalar values. These include configuration function, conversion function and others.

a) Configuration Functions-They offer information about the present configuration.

b) Conversion Functions-They support data changing.

c) Cursor Functions-They provide information concerning cursors.

d) Date and Time Data Type-They are concerned with operations as regards date and time.

6. Function Determinism-Functions that are found in SQL servers are either deterministic or nondeterministic. Deterministic functions provide the same answers when they are used. Nondeterministic functions, on the other hand, offer different results when they are applied.

## SQL Calculations

There are various mathematical functions build-in the SQL server. The functions can be classified into 4 main groups, including Scientific and Trig Functions, rounding functions, signs and random numbers. Although there are numerous mathematical functions within each class, not all of them are used regularly. The various classes are highlighted and explained below:

1\. Scientific and Trig Functions-Under this category, there are various subclasses found under it. These include P1, SQRT, and SQUARE. P1 function is used to compute the circumference and area in circles. How it works: SELECT 2 *10. SQRT connotes square root. This function is used most of the time. The function recognizes any number that can be changed to float datatype. Example: SELECT SQET (36) Returns 6.SQUARE means that you multiply any number by itself. The concept of Pythagoras theorem is useful here. This means that Asquared+Bsquared=Csquared. This can be performed as SELECT SQRT (SQUARE (A) + SQUARE(B)) as C.

2\. Rounding Functions- Under this class, there are various subcategories which include the CEILING and FLOOR. The ceiling function is helpful when dealing with a float or decimal number. Your interest is to find out the highest or lowest integer. Whereas the CEILING is the best highest integer, the floor represents the lowest integer. The ROUND function is applied when you want to round a number to the nearest specific decimal place. This is expressed as ROUND (value, number of decimal places).

3. Signs- There are occasions that require that you obtain an absolute figure of a number. For instance, the absolute value of -7 is 7\. The absolute number doesn't contain any sign. To assist you with this task, it's essential to utilize the ABS function.

4. COS (X)-This function recognizes an angle expressed as radian as the parameter. After an operation, you get a cosine value.

5.     SIN (X)-This function notices a radian angle. After computation, it gives back a sine value.

6.     Sign-You can use a sign function when you want a negative, positive, or zero value.

## The Importance of SQL Built-In Functions and Mathematical Applications

The build-in functions are sub-programs that help users to achieve different results when handling SQL database. These applications are used several times when you want to manipulate or process data. The SQL functions provide tools that are applied when creating, processing, and manipulating data. The benefits of SQL in-build and maths functions are as follows:

1\. Manipulation of Data-The in-built tools and maths functions play a significant role in data manipulation. Manipulating massive data may be difficult if you do it manually. This is especially when the data is massive. Therefore, these functions play a significant role in ensuring that your data is manipulated fast as per your demands.

2\. Assist in The Processing of Data-To benefit from data; you must process it. You may never have the ability to process big data manually. Therefore, the built-in SQL functions and maths applications assist you in processing your database.

3\. Simplifies Tasks-In case you're a programmer, you can attest to the fact that these functions and formulas make your work ease. You can work fast when you apply these in-build functions and formulas. Due to these tools, you'll accomplish many projects within a short time.

4\. Increase Your Productivity-Using the in-built functions enhance your productivity as a programmer. This is because the functions enable you to work quickly on different projects. In case you were to handle data manually, you may take much time before you accomplish a task which ultimately injures your productivity. However, the built-in functions and calculations allow quick execution of tasks.

5\. Time Saving-Because functions are written once and used several times, and they save much time. Besides time-saving, the functions offer support to modular programming.

6\. They Enhance Performance- When you apply functions; you enhance the performance of your database. This is because the functions are prepared and inserted prior to usage.

7\. Enhances Understanding of Complicated Logic-Handling of SQL database is a complex tax. Therefore, functions enable you to decompose data into smooth and manageable functions. In this way, you find it easy to maintain your database.

8\. Cost Effective-Because the functions are in-build in the SQL database; you can use them many times without the need to invest in new ones. In this connection, therefore, they reduce the cost of operating and maintaining your SQL database.

## Downsides of In-Built Functions

The SQL in-built functions have various limitations, including:

1\. Testability- When using the in-built functions, it's challenging to test their business philosophy. This is a big challenge, especially when you want the functions to support your business philosophy. You may never understand whether the functions are in line with your business vision and mission.

2\. Versioning-It's challenging to establish the kind of version that is used in the SQL build-functions. You need to understand whether there're any new versions that can probably provide the best service.

3\. Errors-In case there are errors within the in-build functions which you don't know, they may disrupt the program. This may prove costly and time-wasting.

4. Fear of Change-In case there is change; you may not understand how it will affect your SQL built-in functions. The world of technology keeps changes, and this change may affect the in-built functions.

The SQL in-built functions and calculations are essential as they enable a programmer to execute a task fast with minimal errors. The calculations in the in-built database makes it possible to process and manipulate data.

# CHAPTER 13: AN INTRODUCTION TO JOINS

This chapter seeks to inform you about SQL joins their fundamentals as well as a sneak preview of how you can handle them. When you are analyzing data on the SQL platform, you will sometimes need to work on several tables and merge them to achieve the set goals. The skill of joining or merging tables is essential for data scientists, even though some scientists don't take it seriously. This chapter will enlighten you about the various types of table joins and how you can be able to apply them to SQL.

We will start by discussing the basic concepts of SQL joins and later look at the various types of joins in existence today. This chapter ends with a quick look at different types of queries applied when using more than one table. To understand this topic, you should have beginners' knowledge of SQL and writing a simple question in the PostgreSQL.

## How to Setup the Database Environment in SQL

You need to create a few tables for your analysis before studying the basics of joins. The most recommended kind of table is one having at least one column. You can, however, implement the join queries on similar tables without necessarily creating a new one.

A tool is known as pgAdmin that comes up when you install PostgresSQL helps you perform almost all SQL operations. It is a tool that can be created on a database to create tables in a case where you won't have a database in existence. The following specifications can help you create tables, check them out.

name_student (the name or id) student_stream (student id)

You ought to note that the two tables share a common column. To build a table, you can apply a create statement to create those tables. The table entries ought to have a clean outline if you followed the table creation instructions. At the end of it, you should have at least two simple tables for this discussion. Having learned that, we next discuss the fundamentals of the SQL joins.

## Basics of SQL Joins

The joins will let you collate or merge more than one table with the use of primary identifiers. To understand this, let us look at the two tables we created earlier: all of them share and an id column. You might be wondering what the purpose of joining in SQL is? Well, we discuss that next.

Given the constraints associated with normalization, you might miss out on some of the vital information in one table. The process of normalization isn't only recommended but also a must to ensure consistency, bring down redundancy levels as well as preventing various insertions and updating issues. Let's go back to the two tables again, suppose you want to locate the stream in which a student named Sayak has been enrolled. To do so, you will have to merge the tables and then carry on accordingly.

For you two to join two tables, they must be an everyday thing between those two tables. How can this be achieved? Having the two tables share a column with the same name? Or what does that statement exactly mean? Well, we discuss this next!

The tables that are supposed to be joined might not share a column that has the same name, but in a real sense, the two tables should have a common name. For instance, each set of data should have a thing in common. In this case, you cannot merge two or more tables that have a column with a similar name but with a completely different set of data types.

To break this down further, we next discuss the various types of Joins in SQL.

## Types of SQL Joins

This part of the chapter discusses the different types of joins in SQL joins. We shall discuss each participates to have a clear understanding. It is recommended you first visually study the joins and later execute the set join queries as highlighted in SQL.

### The Inner Join

It is one of the most popular types of joins in SQL. For you to understand it better, take another look at the two tables we created earlier. In those tables, the column we are putting under consideration is the one with ID details. In columns where values aren't common in either of the tables, inner join ignores the rest of that column. Below is am executed example of a query where the inner join is performed in between both tables. These are the student name and the student stream. Once you have completed the question is indicated below, you will attain the exact results as presented in the table.

The self-join option lets you carry out the joining process on the same table, saving you the time you spend organizing the final table. There are, however, a few situations where this can be a good option. Imagine the chart you created earlier has the columns consisting of country and continent.

When faced with a task of listing countries located in the same continent, a clearly outlined set below should give you a glimpse of the results expected.

### The Outer Join

This type of SQL join can further be subdivided into three different types: the left join, the right join as well as the full outer join. The outer join primary role is returning all the identified rows from a single table, and once they join the target is archived, it includes the columns from another table. Outer joins are different from inner joins in the essence that an inner join cannot involve the unmatched rows in the final set of results.

When using an order entry, for instance, you may be faced with situations where it is inevitable to list every employee regardless of the location, they put customer orders. In such a case, this kind of joins is beneficial. When you opt to use this kind of join, all employees, including those that have been given marching orders, will be included in the final result.

Let us discuss the three types of outer joins we highlighted earlier. 

The Left Outer Join: This is a kind of outer join that is responsible for returning each row from the first left side of the table and those row that match from the right side of the table. In case there are no matches on the right side, left join returns a null value for each of those columns.

The Right Outer Join: It is a type of outer join that is tasked with returning each row from the right side of the table and those that merge from the other side (left) of the table. Again, if there aren't any values for those digits in the column, the join returns null values for them.

The full outer join:  it is tasked with returning rows from their initial location in the inner join, and in case there is no match found, this join returns null results for those tables.

### The Cross Join

It is a kind of join that is essentially a product of cartesian elements that is expressed in the SQL set up. Picture this; you require a whole set of combinations available between both tables or even in just one table. You will have to use the cross join to achieve that technique. To help you understand this join better, you can go back to the two tables we created at the beginning of the article. Look at both the columns and try to compare the impact each one of them has to the final result. The cross join plays an essential in ensuring accuracy during merging. You ought to note that there are apparent differences between cross joins and outer joins, even though the description makes them almost look similar. We hope to discuss that in this chapter as well.

Some scientists have questioned the need to combine data with the SQL joins. Well, this has sparked a heated debate on whether it is essential to do. We shall briefly look at why it is vital to combine your data with SQL joins. To better understand this, let's look at other forms of SQL and how they function. SQLite and various databases like the Microsoft SQL servers related in some way. These databases have made it easier for you to build data tables as well as a faculty to link the data closer together.

Given the requirements needed to achieve a set of indicated goals, the joins are aligned against basic practices to reduce data quality problems. This is done through a process known as normalization, which enables each table to attain a particular meaning and goal.  Picture this, you have a table containing various columns with each having crucial information, and you want to change just a section of it; this can be very difficult if you don't have a recommended recovery mechanism in place.

# CHAPTER 14: TEN TIPS FOR EASY RETRIEVAL

In this chapter, we will discuss some of the best tips you can retrieve SQL. To begin with, we need to understand what SQL select is: this refers to a kind of tool that helps you in digging up hidden info in a particular database. It does not matter whether you know what you want to retrieve, being able to translate that idea to SQL can be a difficult task. You need to be very careful with it because even the slightest mistakes will lead to wrong results. To help you stay on track, we have highlighted the following then tips on avoiding the errors.

1\. Verifying Database Structures

When you succeed in retrieving data from your database, and it ends up not making logical sense, you should check the design of your database. It could be because a lot of the databases are poorly designed; if this is the case, you will have to first fix that design before working on another solution. You should keep in mind that good design is essential data integrity.

Most database administrators, as well as developers, mostly assigned character data types on columns that have specifically numeric data. The digital data columns contain any data and are better with catch-all.

2\. Querying on the Test Database

This tip can be implemented by creating a test database containing a similar structure as that of the production database, but this time, only with a few elements representing it in the table. Select data so as you can foretell the kind of results the queries will portray. Additionally, you should deploy every query test on your data and establish whether the outcome matches your expectations. In case they do not match, you will be forced to restructure your queries. Again, when you reformulate your questions and still end up with the wrong outcomes, you may be forced into your entire database.

Create various sets of data sets, and just for accuracy, you should include uncommon cases like the empty tables as well as ridiculous values that fall far off the allowable costs. Picture scenarios that are unlikely to happen and check out for complete behavioral changes in case they happen. In the process of doing so, you are more like to picture out what kind of problems might occur, and well, you will be better prepared.

3\. Confirming the Queries that Contain Joins

Joins are known to be commonly counterintuitive. In case the query you are working on has one of the mentioned joins, you must ensure that it is performing according to how you instructed it before adding it where other clauses are located.  The other thing you ought to do is avoid assigning too much memory.

You ought to know that as part of the administration and installation of SQL, it allows indicating the level of memory assigned to the SQL servers. However, you should know that allocating too much mind to the SQL servers will increase the weight on general servers by preventing it from essential memory resources that can be used to perform other tasks like operating systems and apps.

This trick is also very appropriate, especially with databases that have been inactive for quite some time. Some other retrieval techniques can be useful as well, but not as accurate as this can be. Follow the steps we highlighted carefully and watch your data set get retrieved.

4.  Confirm the Queries that have Subselects

Queries that contain subselects can obtain data from a table, and based on the kind of data that has been retrieved, it might interfere with the set data in a different schedule. From this, we can tell that recovering such type of data can be so hard. You should ensure that the kind of data the inner join retrieves is the same that outer select requires to output desired results. You need to be even more careful in cases where you have more than one level of subselect.

You should also avoid using highly duplicate telexes. This is because a highly duplicated index has a limited set of unique values. To understand this better, let us look a the following example. Imagine you have highlighted an index on the set column which contains slightly less than three values, it means the index is a highly duplicated value. What most people don't know is that having a highly duplicate set of the index isn't good compared to not having it at all. This is because when indexes are highly duplicate, it will force the engine database to work harder to process it during very critical operations like updating or deleting data.

5\. Summarize Your Data with GROUP BY

Picture this; you are working on a table that consists of data about the national baseball league. It can contain information such as the name of the player, teams playing in the league as well as the number of first runs scored by each baseball player in the league. You can be able to retrieve the total points for the home team with the following query. Select team, Add (the home team from nation league group by team): This query will display a list of the total number of home teams, the goals scored as wells the players who scored them. In a majority of identified implementations, such kind of a query can result in null outcomes or errors. In the previous types of data retrieval methods, we have seen more of using data sets that are aligned in columns, than those aligned in rows. There are different ways you can apply that set by using a particular set of formulas. This segment has discussed two methods that, when used appropriately, can result in the desired outcome.

6\. Analyze GROUP BY Section Restrictions

Let us assume that you need a table that consists of the league's top goal scorers. The following query will help you come up with your target results.

SELECT Player, Team they play for, Home Country they come from >= 25 GROUP BY Players:

In a standard set up, this query will result in an error. However, this shouldn't mean that it is not a performing retrieval method. Generally, in this method, the selected columns applied in the grouping or the columns involved in a user query are more likely to appear in that particular list. In q situation where you will prefer viewing that set of data, use the following collection of functions.

SELECT Player, Team they play for, Home Country they come from >= 25 GROUP BY Players:

Because the columns you would like to display in clause appear to be named GROUP BY, it successfully delivers the results you objected to and desired. This is achieved through enlisting the name of the team, then players, and lastly, the total number of goals scored by each player.

7\. Apply the Parentheses with Clauses NOT, OR & AND

In some situations, when a scientist mixes the clauses AND & OR, SQL will mostly won't carry out the expression in the manner you expected to or how you planned. It is therefore recommended that you include these parentheses in the set of sophisticated expressions so that you can ensure you attain your desired results. Keying in an extra set of critical strokes will ensure you smaller reparation for the error you made, and in return, more accurate results.

This set of parentheses will ensure that each game of the clause is applied in the keyword or term you instructed it to. This ensures not only a more accurate set of information but also consistency.

From the previous methods of retrieval we have talked about earlier, this can be said to be among the most affordable of them all. It does not require complicated steps or technicians to do it; contrary, you only need basic knowledge to pull it through. Most scientists have recommended it for the efficiency and accuracy that comes with it. Try using it and watch out for improved, efficient, and more accurate results!

8\. Regulate the Retrieval Privileges

Most of us do not take advantage of the security apparatus that are available in the DBMS. They are not ready to be involved with them because often, they think that misusing and misunderstanding of data are things that only happen to inexperienced people.

However, this is not true; I advise you to establish a significant security device in your system and maintain it so that you can have a more secure set of information. In other words, this segment is encouraging you to ensure that you maximize the security apparatus available in your system.

Additionally, do not hesitate to summarize all the instructions your data set has identified. Even though many have not approved this retrieval method, it is one of the most efficient, and I would advise you to go for it!

A study done by a leading company in Chicago revealed that this retrieval method is safer and does not expose your data to any theft or vulnerability. As we said earlier, this method is also safe and affordable.

9\. Regularly Back up your Databases

Most people think that data is challenging to retrieve when a power outage occurs during infernos, earthquakes, or any other natural disaster that can destroy your hard drive. You should also keep in mind that sometimes, a computer can die on its own, without warning and with your essential information. It is advisable to back up your data frequently to avoid these inconveniences, store the backup media in a secure location.

What do we mean by a secure location? Well, this will depend on how crucial your data is and its importance. It can be anywhere: a fireproof section of your house, it can be a few blocks from where your computer is, or a concrete bunker dug under the mountain and modified by hardening it to without horror scenes like nuclear attacks. It is, therefore, in your hands to decide the kind of security you want to accord your data set. It doesn't matter how weak it can be; the bottom line is ensuring your data is backed up somewhere safe.

10\. Handling the Error Conditions Effectively

Whether you are developing a set of queries around your workstation or applying questions to a particular app, many times, the SQL will return error feedback or something you did not expect. In such situations, it essential to decide the next step to undertake, depending on the kind of message that was returned.

In applications, however, the situation is usually a little bit different. The application user is not generally aware of the appropriate action to take. To take care of such uncertainties, you are advised to install an extensive error handling software into your system. It will effectively tackle every error that might occur. You should, however, note that creating an error managing code needs a lot of effort. It is one of the most complicated procedures that will require you to be a little more careful. The result of it is worth it. Give it a try and watch your data get secured!

# CHAPTER 15: VARIABLES AND STORED ROUTINES

This chapter discusses the variables in a stored procedure and how you can declare them and use them as well. Additionally, we will also discuss the various scopes that the variables contain.

Let us begin by defining a variable. Well, a variable refers to a named data object that its value is not constant and can change during stored procedure fulfillment. In such occurrences, you can use the procedures that have been saved to maintain instant outcomes. These kinds of results or variables are essential to the method you have stored. You should be aware that before you use any variable, you must declare it first.

## Declaring the Variables

To declare a variable, you are recommended you use the following 'declare' statement. Declare variable_user, the data method (measure) [Default default_type]:

In that connection, you must first begin with specifying the name of each variable immediately after you announce a keyword. You must ensure that the name of your variable follows the naming regulations of MySQL column names.

Secondly, you need to ensure that you have specified the data length and type of variables you plan to use. There are different sets of data types that variables can contain, such as Datetime, INT, and VARCHAR. Some of us might be wondering what they mean. To break it down further, you ought to know that these variables refer to the basic sets of rules you use when filling up a table. To this point, we have discussed a host of regulations that are necessary to come up with when working towards achieving your desired goals.

Thirdly, you tasked with assigning a set of variables a primary value through the default option. An amount is certified null when you declare its variable without identifying a default value. The MySQL data set enables you to denote more than one set of variables that have a standard collection of data using the statement we identified earlier on. You can use the following collection of data to declare a variable that contains a similar data set.

Similarly, MySQL system has a slot that allows you to announce more than one set of variables that have a standard type of data. Again, most of the technicians have had issues with how this command relays information to related databases. In the various methods of storing variances and variables, this one has proven to be more secure than others. Consequently, it has been known to be the most popular of them all.

Variables can be applied in mathematical expressions, for example, adding values altogether or combining and holding texts. It can be applied as a section of the general information. For your information, variables are employed in storing information so as one can participate in a kind of calculations. Additionally, variables can be part of the parameters and are used in procedural assessments. It is a two in one method that not only lets you declare a variable but also setting it up with values that have a similar data type. Going back to the examples we gave earlier, we can affirm that varchar is a kind of data that lets you sustain more than one kind of character in just a single string.

At this point, you should be in a position to understand the kind of data sets and various types in existence. This knowledge will not only let you be in an excellent place to tackle errors in case they occur and prevent them from happening as well. When Hillary Bladiwn, a renown data scientist and a graduate of Oxford University, first used varchar, he recommended it for being efficient and accurate. He rated it among the best types of data set in the market today. It does not have an allocation for potential occurrences of errors. It is hard to interfere with such a highly secure kind of data type.

The self-variable option lets you carry out the joining process on the same table, saving you the time you spend organizing the final table. There are, however, a few situations where this can be a good option. Imagine the chart you created earlier has the columns consisting of country and continent.

When faced with a task of listing countries that located on the same continent, a clearly outlined set below should give you a glimpse of the results expected.

This type of SQL variable can be subdivided further into three different types: the left join, the right join as well as the full outer join. The outer join primary role is returning all the identified rows from a single table, and once the joining target is archived, it includes the columns from another table. Outer joins are different from inner joins in the essence that an inner join cannot involve the unmatched rows in the final set of results.

When using an order entry, for instance, you may be faced with situations where it is inevitable to list every employee regardless of the location, they put customer orders. In such a case, this kind of joins is beneficial. When you opt to use this kind of join, all employees, including those that have marching orders, will be included in the final result.

Let us discuss the three types of variables we highlighted earlier.

This is a kind of outer join responsible for returning each row from the initial left side of the table and those row that match from the right side of the table. In case there are no matches on the right side, left join returns a null value for each of those columns. A type of outer join is tasked with merging each row from the right side of the table to the other side (left). Again, if there aren't any values for those digits in the column, the join returns null values for them.

It has the task of returning rows from their initial location in the inner join, and in case there is no match found, this join returns null results for those tables.

It is a kind of variable that is essentially a product of cartesian elements that have been expressed in the SQL set up. Picture this; you require a whole set of combinations available between both tables or even in just one table. You will have to use the cross join to achieve that technique. To help you understand this join better, you can go back to the two tables we created at the beginning of the article. Look at both the columns and try to compare the impact each one of them has to the final result. The cross join plays an essential in ensuring accuracy during merging. You ought to note that there are apparent differences between cross joins and outer joins, even though the description makes them almost look similar. We hope to discuss that in this chapter as well.

# CHAPTER 16: PROJECTS AND EXERCISES IN SQL PROGRAMMING

SQL in full is the Structured Query Language and is a kind of ANSI computer language that has been specially designed to access, manipulate, and update database systems. SQL has different uses; the most significant of them is managing data in database systems that can store data in table forms. Additionally, SQL statements have been used regularly in updating and retrieving data from databases.

What we have thought since childhood is the best to learn a new concept is by practicing it. It is no exception; you have to do various equations related to SQL as a way of learning about them. This section seeks to provide you with a list of exercises or equations that when you solve them, you will be in a position to resolve your issues related to this topic. Check them out!

## Examples of Exercises in SQL

The following are random exercises that you can do in SQL. Assuming you are an employee of a particular research company and you have the task of finding out data about customers in a specific business establishment. Below are some of the queries you are more likely to encounter.

- You are instructed to construct a query that can display every customer that has spent over 100 dollars in a hotel. This exercise will help you acquire mathematical skills in SQL.

- Draft down queries that will indicate every customer that resides in New York City and has to spend over two hundred dollars in the business establishment.

- Draft down questions that will show every customer that either live in New York City OR has spent over two hundred dollars in the business establishment.

- Draft down queries that will indicate every customer that either resides in New York City or HAS NOT to spend over two hundred dollars in the business establishment.

- Draft down queries that will indicate every customer that DOES NOT reside in New York City and HAS NOT to spend over two hundred dollars in the business establishment.

- Draft down queries that will indicate either the orders NOT issued by the last day of the week by a salesman whose identification number is 505 and below and the rules that the amount spent on them is one thousand dollars and below.

- Write down a SQL equation or statement that displays the salesman's identification number, his name, and the city that he comes from. Also, ensure that the commission involved has a range of more than 0.20%, but below 0.15% captured.

-Draft a SQL query that shows every order that customers spend not more than two hundred dollars on, don't include those that were made passed the tenth of February, and purchased by customers that have identification numbers below 5009\.

- Pen down SQL statements to isolate the rows that fulfill the orders made before first August, and the amount spent on them is below one thousand dollars. Secondly, let it include the customer identification numbers that are more than one thousand.

- Draft a list of SQL queries that will display the order number, the amount of money spent, the number of targets achieved, and those that have not been made. Also, indicate the name of the salesman working on them and their success rates.

## Projects in SQL Programming

Below are random projects that you can encounter in SQL programming. They have been picked and randomly, and I believe if you practice them out, you will be better equipped in handling such situations. Before we list the projects, we first should get to understand the differences between exercises and projects. Well, logically, a task is more of a quick test you can do without a lot of complications: it is less complicated compared to projects. On the other hand, projects are a little more complicated and sophisticated. It requires advanced skills as well as data research to do it.

Having learned that, let's discuss the potential projects you can encounter in SQL programming.

i) Interviews

When making software for a particular company, you will need knowledge of an existing system that belongs to that company. For such purposes, you will have to carry out interviews for some individuals working in that company and collect critical information. You will have to do interviews on people that are aware of that software. Such people could be working as hostel wardens or trainers.

ii) Discussions (Groups)

They can be a kind of group discussion that has occurred between employees of the company you are working on. For a start, a good number of ideas might appear clustered together or filled by concepts that already exist. Such ideologies might be brought on board by programmers.

Additionally, it can be done through online observation. It is a procedure of obtaining more essential details about the existing software or web apps from the web. The primary purpose of this project is getting as close as possible to the system. SQL programming plays a critical role in ensuring the systems are up and running as recommended.

## Application of SQL

The self-variable option lets you carry out the joining process on the same table, saving you the time you spend organizing the final table. There are, however, a few situations where this can be a good option. Imagine the chart you created earlier has the columns consisting of country and continent.

When faced with a task of listing countries located on the same continent, a clearly outlined set below should give you a glimpse of the results expected. SQL variable can further be subdivided into three different types: the left join, the right join as well as the full outer join. The outer join primary role is returning all the identified rows from a single table, and once the joining target is archived, it includes the columns from another table. Outer joins are different from inner joins in the essence that an inner join cannot involve the unmatched rows in the final set of results.

When using an order entry, for instance, you may be faced with situations where it is inevitable to list every employee regardless of the location, they put customer orders. In such a case, this kind of joins is beneficial. When you opt to use this kind of join, all employees, including those that have been given marching orders, will be included in the final result.

This is a kind of outer join that is responsible for returning each row from the first left side of the table and those row that match from the right side of the table. In case there are no matches on the right side, left join returns a null value for each of those columns. A type of outer join has the task of returning each row from the right side of the table and merging with the other side (left) of the table. Again, if there aren't any values for those digits in the column, the join returns null values for them.

It has the task of returning rows from their initial location in the inner join, and in case there is no match found, this join returns null results for those tables.

This is a kind of variable that is essentially a product of Cartesian elements that have been expressed in the SQL set up. Picture this; you require a whole set of combinations available between both tables or even in just one meal. You will have to use the cross join to achieve that technique. To help you understand this join better, you can go back to the two tables we created at the beginning of the article. Look at both the columns and try to compare the impact each one of them has to the final result. The cross join plays an essential in ensuring accuracy during merging. You ought to note that there are apparent differences between cross joins and outer joins despite the fact that the description makes them almost look similar. We hope to discuss that in this chapter as well.

Similarly, MySQL system has a slot that allows you to announce more than one set of variables that has a common type of data. Again, most of the technicians have had issues with how this command relays information to related databases. In the various methods of storing variances and variables, this one has proven to be more secure than others. Consequently, it has been known to be the most popular of them all.

Variables can be applied in mathematical expressions, for example, adding values altogether or combining and holding texts. This can be used as a section of the general information. For your information, variables are also applied in storing information so as one can participate in a kind of calculations. Additionally, variables can be part of the parameters and are used in procedural assessments. This is two in one method that not only lets you declare a variable but also setting it up with values that have a similar data type. Going back to the examples we gave earlier, we can affirm that varchar is a kind of data that lets you sustain more than one kind of character in just a single string.

Up to this point, you should be in a position to understand the kind of SQL Exercises and Programs as well as the various types in existence. This will not only let you be in an excellent place to tackle errors in case they occur and prevent them from happening as well. When Mark Suaman, a renown data scientist and a graduate of Havard University, first used varchar, he recommended it for being efficient and accurate. He rated it among the best types of data set in the market today. It does not have an allocation for potential occurrences of errors. It is hard to interfere with such a highly secure kind of data type.

## Applications of SQL

Since its introduction in the computing world, SQL has played a significant role in revolutionizing data storage in a systematic manner as well as direct retrieval. As the digital world continues to grow steadily, the amount of data stored quickly escalates, making organizations and personal data piling up. Therefore, SQL acts as a platform where these data are stored while offering direct access without the emergence of limitations. As such, SQL is used in different sectors, including telecommunication, finance, trade, manufacturing, institutional, and transport. Its presence primarily deals with data but also accompanies other significant benefits on its application.

### Data Integration

Across the sectors mentioned above, one of its main applications of SQL is the creation of data integration scripts commonly done by administrators and developers. SQL databases comprise of several tables which may contain different data. When these data are integrated, it creates a new experience essential for the provision of meaningful information, therefore, increasing productivity. Data integration scripts are crucial in any given organization, including the government, as it offers trusted data which can be utilized to promote the achievement of the set goals.

### Analytical Queries

Data analysts regularly utilize Structured Query Language to smoothen their operations more so when establishing and executing queries. That is, as discussed earlier, SQL comprises multiple tables that consist of different datasets. When these data are combined, it brings out more comprehensive information critical for any individual or organization. The same is also applicable for data analysts as they use a similar aspect. As they use an analytical query structure, queries, and tables from SQL are fed into the structure to deliver crucial results from varying sources. In this case, data analysts can readily acquire different queries and customize them to have a more comprehensive data to depend on as solutions.

### Data Retrieval

This is another important application of SQL to retrieve data from different subsets within a database with big data. This is essential in financial sectors and analytics as to the use of numerical values typically consists of mixed statistical data. The most commonly used SQL elements are create, select, delete, and update, among others. The technique is made possible when the user quickly can search the database and acquire the needed data as SQL sieves the information to bring out the desired data. In some cases, the language may deliver similar or related data when the required data is missing. This is crucial as one can compare the results as well as make changes where the need arises.

# CONCLUSION

As mentioned above, SQL is used in different sectors globally and applied in different areas to help in data management. One of them includes index structures modifications that encompass the creation of pathways that helps in the collection of data that quickly trace information of interest. SQL can also be applied as a technique to modify and change database tables. That is, it helps in keeping the data stored up to date, therefore, eliminating instances of outdated data, which are often misleading.

C#

New step by Step Guide to Learn C #

in One Week.

Including Projects And Exercise To

Mastering C#.

Beginners User

Andrew Sutherland

 Copyright 2019 by Andrew Sutherland - All rights reserved.

This eBook is provided with the sole purpose of providing relevant information on a specific topic for which every reasonable effort has been made to ensure that it is both accurate and reasonable. Nevertheless, by purchasing this eBook you consent to the fact that the author, as well as the publisher, are in no way experts on the topics contained herein, regardless of any claims as such that may be made within. As such, any suggestions or recommendations that are made within are done so purely for entertainment value. It is recommended that you always consult a professional prior to undertaking any of the advice or techniques discussed within.

This is a legally binding declaration that is considered both valid and fair by both the Committee of Publishers Association and the American Bar Association and should be considered as legally binding within the United States.

The reproduction, transmission, and duplication of any of the content found herein, including any specific or extended information will be done as an ille.g.al act regardless of the end form the information ultimately takes. This includes copied versions of the work both physical, digital and audio unless express consent of the Publisher is provided beforehand. Any additional rights reserved.

Furthermore, the information that can be found within the pages described forthwith shall be considered both accurate and truthful when it comes to the recounting of facts. As such, any use, correct or incorrect, of the provided information will render the Publisher free of responsibility as to the actions taken outside of their direct purview. Regardless, there are zero scenarios where the original author or the Publisher can be deemed liable in any fashion for any damages or hardships that may result from any of the information discussed herein.

Additionally, the information in the following pages is intended only for informational purposes and should thus be thought of as universal. As befitting its nature, it is presented without assurance re.g.arding its prolonged validity or interim quality. Trademarks that are mentioned are done without written consent and can in no way be considered an endorsement from the trademark holder.

# 
Introduction

Congratulations on purchasing C#, and thank you for doing so.

The following chapters will discuss all of the different parts that we need to work with when it comes to learning how to code C#. There are a lot of options when it comes to learning how to work with some of the coding and the programming that you want to do. But one of the best options that we can choose from is the C#, and this guidebook is going to spend some time looking at what we are able to do with the C# language, and how we are able to make it work for all of our coding needs as well.

The beginning of this guidebook is going to take some time to look at how we are able to work with the C# language and some of the steps that we can bring in when it is time to make this program be on our computers and to ensure that it is going to work in the proper manner. While C# is a language that is found on the Windows system, it is possible to go through and add it to the Linux and the Mac systems as well, allowing us to have a bit more freedom with some of the codings that we want to do as well. We will discuss this and so much more as we go through this guidebook.

Once we have the program ready to go on our computer, it is time to move on to some of the actual coding that we want to do as well. We will look at how we are able to go through and install Visual Studio Community, how to write out some of our own programs in the C# language, and some of the basic parts of the code that we need to know in order to get started with coding in this language. We will even take a look at how to work on the keywords in this language and what they mean to provide commands to our codes as well.

From there, we are able to move on to some of the other things that we are able to work with when in this language. We can spend some time working with the File Input and Output of our codes, how to make some of our own conditional statements so that the program can make decisions based on the conditions that you set, and how to work with a lot of the operators that are found in this language as well.

That is just the beginning of what we are able to do with the C# language. When we have some of those basics down, it is time for us to go through and look at some of the more complex topics that need to show up when we are doing our work in C#. We will spend this time looking at what polymorphism is about, how to work with the enumeration data type, how to work with multithreading and why this is important, and how the variables work in more depth so we know why we would like to work with these.

To finish off this guidebook, we are going to spend some time looking at a few projects that you are able to bring in to ensure that you are going to get the best results out of this process. There are a lot of different parts that we tried to take a look at the inside of this guidebook, and the best way to get them all under control and to ensure that it is going to work in the manner that you would like is to get some practice. This final chapter is going to help us to get this down and will ensure that we are prepared to get started as well.

There are a lot of things that we are able to enjoy when it comes to working with the C# language. And while there may be some other coding languages that we are able to focus on as well, you will find that the C# language will be able to handle all of your coding needs in no time. When you are ready to get started with coding in the C# language, and you want to learn how to make this all work well for your coding and programming needs, make sure to check out this guidebook to help you out!             

There are plenty of books on this subject on the market, thanks again for choosing this one! Every effort was made to ensure it is full of as much useful information as possible, please enjoy it!

# 
Chapter 1: An Introduction to C#

Learning how to code is going to provide you with a ton of benefits along the way. It is going to make it easier to create some of the programs and applications that you would like. It is going to be able to help you further your career with a lot of options that are simple to work with and can allow us to get the best out of these new skills and more money as well. And then there are times when learning how to work with C# is going to be important because it will allow us to learn more about our computers and how they work.

There are a lot of great options when it is time to work with programming. Many languages have been developed to work on different projects, and sometimes they will work on different types of processes and applications as well. While many of these can be useful based on what you would like to accomplish with the language in the first place, we are going to take a look at how to work with the C# language and how great this one can be for our needs as well. Let’s dive into the C# language and how to make this work for our programming needs as well.

## What is the C# Language?

The first thing that we need to take a look at here is the C# language. C# is going to be an elegant and object-oriented language that is going to be helpful because it allows programmers to go through and built up a variety of robust and secure applications, all of which are going to run with the .NET Framework. It is possible to work with C# on a variety of projects, including with Windows client applications, Web services, client-server applications, XML  database applications and so much more.

When we are working with the C#, we will find that visually it is going to provide us with an advanced code editor along with some user interface designers that are more convenient to use, a debugger that is integrated, and some other tools that will ensure that it is easier to develop some of our applications based on this language.

The neat thing about the C# language is that it is not only going to be highly expressive and able to help us out with a lot of the more complicated codes that we want to handle, but it is also going to be easy to learn and simple. The curly-braces that are part of the syntax of C# is something that is going to look familiar, especially if you have worked with Java, C++, and C in the past. Developers who are good with these languages will find that it does not take that long to learn C# because of the similarities.

C# is useful because it is going to be able to simplify some of the issues that happen with the C++ language, and it is going to provide us with some powerful features including value types that can be null, delegates, enumerations, lambda expressions, and even memory access that is direct. None of these are going to be featured are available with languages like Java.

In addition to this, you will find that the C# language is going to be able to support some of the generic methods and types, which is going to help us provide increased type safety and performance, and it comes with some iterators, which enable the implementers of collection classes to help define custom iteration behaviors that will be easy to use by the client code.

Because this language is going to fit into the category of object-oriented, it is going to be able to support a lot of topics and options that fit into this category, and that we will be able to explore in more detail later on, including polymorphism inheritances, and encapsulation. All methods and variables that we use are going to be encapsulated within these definitions of classes. And it is possible for a class to inherit directly from one parent class, but it can be set up to implement any number of interfaces.

Methods in this language will be able to override accidental redefinition. When we work with C#, a struct is going to be similar to a lightweight class. This means that it is going to be a stack-allocated type that will be able to come on board and implement interfaces, but it is not going to be able to help us when supporting inheritances.

In addition to some of the basic principles that we just took a look at, you will find that C# is going to make it easier in order to develop some of the components of software through a few constructs, and these are going to include the following:

1.  It is able to go through and encapsulate some of our method signatures through the use of delegates. These are going to enable some of the type-safe event notifications that we need.
2.  Properties that are going to be there to work as the accessors for some private member variables.
3.  Attributes, which are going to help provide declarative metadata about some of the different types when the program runs.
4.  LINQ, which is going to stand for a Language Integrated Query. This is useful because it is going to provide us with some built-in query capabilities no matter which sources of data that we are going to work with.

There are a lot of benefits that we are able to see when it is time to work with the C# language and make it work for some of our needs. It is an object-oriented language that makes it easier to organize and keep things together, and when we are able to utilize the right IDE, and the .NET platform that we will talk about in a moment, we will be able to utilize it to make the powerful programs that we want, without all the complexities of the missing features that happen with other languages that are similar.

## The .Net Framework

Another thing that we need to take a look at when working with the C# language is the .NET framework. This is going to be a framework that Microsoft has developed to run well on Windows. It is going to include a very big class library, which is known as the FCL or the Framework Class Library and this is going to provide us with language interoperability, which means that each language can use code that is written out in other languages, across more than one kind of language.

Programs that are written out in this kind of framework are going to be able to execute itself in the environment for the software rather than the hardware environment, known as the CLR or Common Language Runtime. The CLR is going to be an application virtual machine that will help to provide us with some different services including security, exception handling, and memory management. Because of this, the codes that are written with this Framework is going to be known as managed code. Both the CLR and the FCL that we have talked about are going to make up the .NET framework that we are talking about.

First, the FCL is going to be important. It provides us with some of the user interface, database connectivity, data access, web application development, algorithms, network communication, and more. Programmers are able to produce some software when they combine the source code they are working on with the .NET framework and some of the other libraries that are available.

This is a framework that is designed to work well with most new applications that we want to create on the Windows platform. In addition, Microsoft is going to produce an IDE that is specifically for the .NET software that is known as Visual Studio.

The .NET Framework began just as proprietary software, although it has since been standardized to help work on other options as well. Despite some of the standardization efforts that have happened, most developers expressed how uneasy they felt with some of the terms and the prospects that came with the open-sourced and free implementations. Because of that, the Microsoft company has changed the .NET development to help closely follow a contemporary model of a community-developed software project, including issuing an update to its patent that would help to address these concerns.

There are a lot of things that we are able to work with when it comes to the .NET Framework. There are methods that have been developed to work not only on the Windows systems but also with some of the other operating systems, including Linux and Mac. And it is able to help us work with a variety of languages, especially with C#, while being portable, secure, high in performance, and good with managing the memory that we need while writing out certain codes.

## The C# IDE

Before we are able to get into details about how we can code, and what all we are able to do with the C# language, we need to get a better idea of what an IDE is about, and why this is such an important part of any coding that we want to do. To start, an IDE is going to be an integrated Development Environment, which is basically an application we can use to help with application development. In general, this is going to be a GUI or graphical user interface that is designed to make it easier for any developer to build software applications. Many times these are going to have more of the tools that you need.

Most of the common features, such as data structure browsing, version control, and even debugging, are going to be there to help the developer execute actions without needing to switch back and forth between the different applications that they are working with. This makes it easier to maximize the productivity because we are able to provide similar user interfaces for the components that are related, and it is going to reduce the amount of time that it takes to learn a new language. In addition, depending on the kind of IDE that you choose to go with, it can sometimes just support one language, and other times it will support many languages.

The concept that is behind the IDE is something that evolved from some simple command-based software, which at the time was not really as useful as the menu-driven software. Some of the modern IDE’s are going to be used more in the context of our visual programming, while the applications in these are going to be created in a quick and efficient manner by moving the code nodes or the building blocks of programming that will generate the flowchart and structured diagrams. These can then be either compiled or interpreted based on what you hope to get out of the process.

It is important that we take the time to pick out a good IDE, and there are a number of factors that we need to consider as we work through this. For example, we need to spend time looking at the language support, operating system needs, and some of the costs. Sometimes the IDE that we want to work with will be free, but sometimes these are going to have limited features. It often depends on what you would like to design with that language, and what features are important to your coding needs.

There are a number of good IDE’s out there that are available with the C# language. It is important to do some research and learn more about how these work, and which ones are going to have the features that you would like in order to get the best results. When you are able to do this, it is infinitely easier to get the codes written that you would like.

## How to Work with C# On Linux and Mac Computers

While C# is considered a Windows language, it is possible for us to go through and work with it on a Linux and Mac computer as well. We may need to go through a few extra steps, and sometimes a few of the functionalities that we are used to seeing with Windows will be gone, but there are still a lot of benefits that we will see with using this option on other operating systems.

For the Linux system, the MonoDevelop IDE, which is part of the Mono Project, should be just what you need in order to develop some C# coding on a Linux computer. The easiest way for you to install this is to work with the MonoDevelop package that was developed to work with Ubuntu. Sometimes it is recommended to work with the WinForms toolkit, but this one is not going to be as efficient and easy to work with.

We can also set this language up to work on a Mac computer. The first step is to download an IDE, and Visual Studio Code is usually the best one here because it does work well with Mac and still provides you with the functionality that you need while the simplicity of use is still there. Just visit the Visual Studio website (we will go into more details about working with Visual Studio in the next chapter), and then make sure to click on the button to download to Mac. This should download what you need in a zip file.

Once you have been able to get this setup, you can unzip the file and then drag it over to the Applications folder. You should be able to download it from there. The next step is to go through and download the C# extension. You can go into Visual Studio Code and open up the Extensions that you need to make this work.

Now, as you are going through this process, you are going to notice that there is a search bar at the top of the extensions view. This is where you are going to type in “C#”. The one that you need is going to be by Microsoft, so make sure to click on this one. Click to install and you are ready to go.

Remember though this process that the C# language is one that has been developed to work the best with a Windows system. So, if you are on a Windows system, you are more likely to find this language easy to use, and all of the features and functionalities that you are looking for in coding are more likely to be where you put them.

This does not mean that you are not able to get this to work on your Mac computer at all. It simply means that you need to take a few extra steps to get this setup, and it may not be as easy to accomplish some of the things that you would like. Taking some time to get familiar with the C# language on a Linux or Mac computer will be important to helping you get the best results in the process.

# Chapter 2: Get Ready for C#

Now that we know a bit more about the C# language and what it is all about, it is time for us to dive in and take a look at some of the main points that come with this language and how we are able to make all of this work for our needs. In this chapter, we are going to get the environment for C# all set up and ready to go, and then we will move on to some of the ways that we can write out codes in C# and the basics to help us get the most out of the whole thing. Let’s get started with the C# language and how we can use this for our needs.

## How to Install Visual Studio Community

The first thing to look at here is to make sure that we have our computer ready to go. Before we can install the Visual Studio program, there are a few steps to go through, including:

1.  Take a moment to check out the system requirements that are there. These are going to give us an idea of whether our computer is set up to support Visual Studio 2019\. We are going to focus on this version of Visual Studio, but the steps for some of the other versions are going to be similar.
2.  Apply all of the updates for Windows that are available. These are important because they will ensure that the computer is going to have all of the system components and the right security updates in order to handle Visual Studio.
3.  When the updates are done, it is time to do a reboot of the system. This will help us make sure that the pending updates or installs are not going to hinder the work that we do with installing Visual Studio.
4.  You may also need to go through and free up some space on your computer. Ake some time here to remove any of the applications and files that are not needed on your system. You can do this quickly and efficiently with the Disk Cleanup App.

When the computer is all set up, it is time to download the Visual Studio program. You can download this with the Visual Studio bootstrapper file. To do this one, though, you need to go to the Microsoft site for Visual Studio and click on the Download button. You can choose to install, then save before opening up the folder.

While we are at this part, we want to install the Visual Studio installer. Run the file that we talked about earlier in order to install all that we need with Visual Studio. This is a new and lightweight installer that is going to include all of the parts that we need for installing and then customizing the Visual Studio file that we need.

To start this, we need to go into the Downloads folder, double-click on the bootstrapper that is going to match or looks similar for one of the files below:

1.  Vs_community.exe: This is going to be the one if you downloaded Visual Studio Community.
2.  Vs_professional.exe: This is going to be the one if you are downloading Visual Studio Professionals.
3.  Vs_enterprise.exe: This is going to be the one if you are downloading Visual Studio Enterprise.

If you do this, you are going to end up with a User Account Control notice. Make sure to click on yes for this one. Then you will need to go through and acknowledge that you see the License Terms and the Privacy Statement. Read through those and then click on Continue.

Then it is time for us to look at some of the steps that we need to take to choose our workloads. After the installer is set up, you can use it to help make some customizations to your installation by going through and selecting out the feature sets, or workloads, that you would like to handle. You can go through all of these now and see what they are like and what you would like to work with as well. You can always add in more features later on if you decide that you need them by going into Visual Studio and into Tools.

There are a number of optional parts that you are able to work with next if you would like, depending on how you would like to work with this. You can change the languages that this is able to support, for example. Take some time to look through these options as you go through them and decide if they are the right ones for you to use for your needs or not.

And when this is done, it is time to take the Visual Studio program and start doing some of the developing that you would like. There are a few steps that we are able to use to make this one happen, and that includes:

1.  When the installation is done, you can choose the Launch button in order to get started with some of the codings and developing that you would like to do.
2.  While you are on the start window, you can choose to create a new project.
3.  When the search box shows up, you can enter in the type of app that you would like to create in order to see a list of templates that are available. The templates that are there will depend on which workloads you decided to go with during the installation. If you want more or different options for these templates, then you need to go through and choose different workloads.
    1.  It is also possible to go through and filter out the search that you do for a specific coding language with the drop-down list for Language. Then we are able to filter these out with the Platform list or with the Project Type list as well.
4.  When you have made these decisions, you will find that Visual Studio is going to open up the new project, and you are ready to go and get to work.

## Writing Your First Program in C#

The next thing that we need to take a look at is how you can write out your first programs in C#. It is important to get a good look at some of the ways that you can write out a program in C# or any language that you are learning for that matter, and when we are able to actually write out a few codes, it makes things that much easier to handle along the way as well.

To help us get started with this, we need to open up our text editor, such as Notepad, and Visual Studio, so that we are ready to write out some of the codes that we need. Once you have that all opened up and ready to go, make sure to type in the code below in order to see more about how this language works:

class FirstProgram

{

static void Main()

{

Console.WriteLine(“UsingC# is fun.”);

}

}

Now you can access the command prompt and type:

csc FirstProgram.cs

After you issue this command, the compiler for C# will process this file and then create a .exe file in the same location as your code. For example, if you saved the original file on the desktop, you should see a new program come up called “FirstProgram.ee.” right in the same place. If there is an error in the code that you wrote, you will see an error message come up.

Now you can run this application by entering “FirstProgram.exe.” into the command prompt. If everything was done correctly, you should see that the command prompt will display the message: “Using C# is fun.”

## The Basics of Your Code

With the information above about how to write out code, it is time to go through it a bit more and learn about how each part is important to the work that we did. This will make it easier to write out some of the codes that we are looking for along the way, and this can really ensure that we can write out some of the more complicated codes at a later on. Some of the different parts of a C# code includes:

First, we need to take a look at the top line. This is going to have our identifier along with the keyword. The keyword will be any word inside the code that also has some special functions to get the compiler to work. With this keyword, just like we did in the example above, we are working to create a new class in this program. The identifier, when it is used well in this code, is going to be in charge of listing out the class, the method, and the variable. This one, in particular, is known as “FirstProgram”.

Then we are going to move our way down to the third line in the code above. This is where we are going to spend time defining the method of Main()> This one acts as the starting point for any of the applications that we see on the computer. The program will be able to star tout by executing this method, regardless of the location where this is found inside of our code. There are two main words that will fit here, static and void, just like you see above. This will help us to determine which object we are going to see in the code.

Now we can skip down to the fifth line of the code. This is going to be the final part that we need to look at for now because it is going to include the message that we want to show up on the computer when the whole of this has been executed. This is going to rely on the WriteLine() method so that you can actually get it to show up in writing on the screen. It is possible to take this further and add in as many messages as you would like with the help of this part.

Along with the topics that we just went over, you may notice that there are a number of braces that show up in the code. These are important because they will divide the code up into blocks so that you can separate out the parts a bit easier. Keep in mind when you are writing out some of the codes that you want to use in C#, the semicolon is going to be important, too, just like what we see with Java and C.

#   Chapter 3: C# Keywords

Another topic that we need to take some time to look at is the C# keywords. These are going to be identifiers that are reserved and predefined. They are set up to have special meanings to the compiler, and will basically be the commands that the compiler is supposed to follow. You should not use these in the program as identifiers unless they will have, as a prefix, the @ symbol. For example, the @if is going to be an identifier that is valued, but it will not be since this is a keyword.

The first table that we are going to take a look at will have all of the keywords that are reserved identifiers when you work with the C# program. Then we are going to take a break from that and look at some of the contextual keywords that are available.

There is a difference between the regular keywords and the contextual keywords. For example, the contextual keywords are going to come with some special meaning but only in a limited program context, and we are able to use them ad identifiers outside of that context. This makes them a bit different than what we are able to do with some of the regular keywords as well.

In general, as we add more of these keywords to the C# in the future, we will find that they will be added into the library as the contextual keywords. The reason for doing this is to make sure that we are not breaking up or ruining some of the programs that the programmer was able to write out in earlier versions.

There are a number of keywords that we are able to utilize in order to make the C# program work in the manner that we want. Some of the most common keywords that we are able to work with will include:

| While | Volatile | Void | Virtual | Using static |
| Using | Ushort | Unsafe | Unchecked | Ulong |
| Uint | Typeof | Try | True | Throw |
| This | Switch | Struct | String | Static |
| Stackalloc | Sizeof | Short | Sealed | Sbyte |
| Return | Ref | Readonly | Public | Protected |
| Private | Params | Override | Out | Operator |
| Object | Null | New | Namespace | Long |
| Lock | Is | Internal | Interface | Int |
| In | Implicit | If | Goto | Foreach |
| For | Float | Fixed | Finally | False |
| Extern | Explicit | Event | Enum | Else |
| Double | Do | Delegate | Default | Decimal |
| Continue | Const | Class | Checked | Char |
| Catch | Case | Byte | Break | Bool |
| Base | As | abstract |  |  |

From that point, we are able to work with what is known as the contextual keywords. These are going to be a bit different than what we are going to find with some of the other options. These are still important, but it is going to depend on the part of the code that we are working with, and what we hope to be able to get out of it all.

To start, the contextual keyword is going to be used in order to provide some of the specific meaning in the code that we want, but it will not be reserved like the other keywords that we are using here. For example, a few of the contextual keywords that we see in here, including where and partial, are going to have special meanings in two or more contexts based on how we are going to work with them. Some of the different contextual keywords that you are going to find in this kind of language will include:

| Yield | Where (the query clause) | Where (generic type constraint) | When (filter condition |
| Var | Value | Unmanaged (generic type constraint) | Set |
| Select | Remove | Partial (method) | Partial (type) |
| Orderby | On | Nameof | Let |
| Join | Into | Group | Global |
| Get | From | Equals | Dynamic |
| Descending | By | Await | Async |
| Ascending | Alias | add |  |

The keywords are going to be important in some of the codings that we will do because they ensure that we are going to be able to see some of the results that we want in the process, and will make it easier for the compiler to do some of the commands that we would like as well. Make sure to learn some of these and keep them separate so that we are using them to provide the right commands, rather than getting an error in the code that we write.

#   Chapter 4: File Input and Output

Another topic that we need to spend some of our time working within the C# language is the idea of our files. These are going to be important because they will ensure that we are able to see some of the results that we want in our codes and that we will be able to pull out the different parts based on what we are hoping to accomplish as well.

These files are simple to work with, but there are different things that we need to do with each one to ensure that they are going to work the way that we want. We can set up the files to save some of the work that we want to do, and to organize the different parts of the code that we want to work with. It takes a bit of coding and a bit of work to make all of this come together and behave in the manner that you would like.

With some of this in mind, let’s take a look at how the files are going to work in this kind of language and look at how we are able to handle the file input and the file output in the C# language.

## Implementing the File Input and Output Operators

The first thing that we need to take a look at here is how to implement these operations. Programs that are able to accept some kind of input from the user are also able to process this input and then produce some kind of output. All of the languages for coding out there are going to support this in order to make it work. The file is going to help with this as a collection of data that is stored on our disks with a specific name, as well as a directory path that needs to be followed. The file that is open for us to read and write data in is known as the stream.

To take this further, the stream is going to be a sequence of bytes that come from the source all the way to a destination through the path of communication that we set up. The two basic streams, of course, are going to be the input and output. Each of these streams will have some kind of function associated back to it. The input stream is there to help with the read operation, and then the output stream is for our write operation.

The system input and output namespace will often work with a lot of classes that are meant to help out with things that we need to get done in our code. Some of these will include reading operations, file deletion, file creation, and writing the operations as well. TO give us a better idea of how to describe some of the classes that are able to fall into this kind of namespace, we are able to look at the information below:

1.  FileStream: This is going to be used to help us to read and to write from any location that we want within our file.
2.  BinaryReader: This one is going to be used to help us read some of the data types that are more primitive from the binary stream.
3.  BinaryWriter: This is going to be used when we would like to take those primitive data types from before and write them into a binary format so that they can go over to a binary stream.
4.  StreamReader: This is a good one to learn how to use because it is able to read the characters that we need from a byte stream.
5.  StreamWriter: This is going to help us to write the characters that we would like over to a stream.
6.  StringReader: This is going to be similar to the others we have talked about, but it is going to be used to help us read from a string buffer.
7.  stringWriter: And again, this one is similar, but this time we are going to write into that string buffer that we are using.
8.  DirectoryInfo: This one is going to be used in order to perform some operations on directions and more.
9.  FileInfo: This one is important because it is going to help us to perform some operations on files.

## The FileStream Class

Now that we have been able to talk about some of the different parts here, we also need to take a look at this class, in particular, a little bit. The operations for the file input and output are going to be implemented in that System IO namespace that we were talking about earlier. The user is able to work with this class in order to read, write, and close up the files.

From there, the classes that we have been able to go through and be inherited from an abstract class. This abstract class is going to be known as the Stream. A good example of the syntax that we are able to work within order to create one of the objects that will be found in this particular class of FileStream will be found below:

      FileStream <objectname> = new FileStream ( <file name>, <file Mode Enumerator>,

                                                      <File Access Enumerator> , <FileShare Enumerator> ); 

## The FileMode Enumerator

The next thing that we need to take a look at is known as the FileMode Enumerator. This one is important because it is going to help us to define methods to open up the files that we need. It is also going to be used in order to restrict the mode where the file can be opened or the method that the file can be opened by the user. The parameters to this enumerator are going to be important because they will check out whether this particular file can be overwritten, created, or opened. The members of the enumerator that you will use here will be like the following:

1.  Append: We would use this member to help us open u a file if it is already created, and then it will place the cursor at the end so that we can add some of the parts that we would like. If the file is not already there, then it is going to create a new file for us.
2.  Create: This is the member that is going to help us to create a new file.
3.  CreateNew: This is the member that we will use when we would like to specify which operating system that new file needs to be created in.
4.  Open: This one is going to help us out by opening up a file that is already around.
5.  OpenOrCreate: This member can be used because it helps to specify to the system that it should open up a file if it exists, or it should create a new file as well.
6.  Truncate: This one is important because it is going to open up a new file for us. When it is opened, the file should then go through the process of being truncated, and the size of this file is then going to be at zero bytes to start.

Then we need to take a look at a few of the FileAccess Enumerators that we are able to work with. For this one, the file will be opened so that we can do operations of reading and writing on it. The enumerator here is going to be used to help us figure out whether the user would like to read the data that is found in that file, or if they would like to write data onto the file. It is possible for the user to want to do both of these operations as well. the members of this kind of enumerator that we are able to work with include ReadWrite, Write, and Read.

Then there is the FileShare Enumerator that we need to spend some time on. The enumerator here is going to contain a few constants for controlling the access that the constructors for FileStream are going to have on that particular file. The use of this enumeration here is going to be to help us define whether two applications can, at the exact same time, will be able to read the information out of the same file. Some of the members of the enumerator of FileShare will include:

1.  Inheritable: This is going to allow one of our file handles to pass the inheritance over to the child processes.
2.  Note: This one is going to reject the sharing of the current file that we are in.
3.  Read: This one will allow the user to open up the file. The user will only be able to read the file, though, without being able to make any changes or additions or write in it at all.
4.  ReadWrite: This one is going to allow the user to do whatever they would like in the file. It helps them to open up the file and either read through it, write in it, or do a combination of both.
5.  Write: This is going to allow us to open up the file and write or make changes to that file.

## How to Implement Reading and Writing Into Our Files

The next thing that we need to take a look at is how we are able to get the files set up so that we are able to read and write the text that is found inside of them. For this, the Stream class is going to be important. For example, this class is going to be used in order to write and read any of the data that we want in the text files. The StreamWriter and the StreamReader classes will be able to help us get this done.

The first option here that we need to take a look at is going to be the StreamReader class. This is going to be a class that has been inherited from the TextReader class, one that was kind of abstract but is still important. The class is going to be helpful here because it represents that the reader is going to be able to read through the characters that are there.

There are a few methods that we are able to work with this one in order to help work on this class. Some of these include:

1.  Close: This one is going to close up the objects of the StreamReader class and stream, and then it is able to release the resources of the system that are associated with that reader.
2.  Peek: This one is going to help us by returning the next character that is available, but it is not going to consume it.
3.  Read: This one is going to read the character that is coming up next, or it could be a set of characters that are in the stream.
4.  ReadLine: This one is going to help us by reading a line of characters out of the current system and then will help us to return that all out in a data string.
5.  Seek: This one is going to allow us to be in the read and write position and will allow us to move this to any of the positions that are inside of the file.

To get a better idea of how we are able to work with this particular class and make it easy for us to read data out of any file that we would like in this language, we can work with the following code:

class  Program

{

    public  void  ReadData()

    {

        FileStream fs = new  FileStream("E:\\data.txt", FileMode.Open, FileAcess.Read);

        StreamReader sr = newStreamReader ( fs );

        sr.BaseStream.Seek( 0, SeekOrigin.Begin);

        string str = sr.ReadLine();

        while  ( str ! = null  )

        {

            Console.WriteLine("{0}", str );

            str = sr.ReadLine();

        }

            sr.Close();

            fr.Close();

    }

    static  void  Main ( string[ ] args )

    {

        Program p = new  Program();

        p.ReadData();

        Console.Read();

    }

}

Now, we are able to go through and work with this a bit more. We can see that there is a FileMode property value that we are going to use in order to open up our file, and then there is a property value of FileAccess that allows us to read the file. The file data.txt is going to be in the mode of open and will prepare the stream for the read operation. From there, we are going to see that our reader statement is there to create a new instance of this class so that the text file is able to use it.

One final thing to note here is the Seek() method. This is an important method because it is there to allow us a chance to move the read position to the beginning of our file. This is then going to allow us to read all the way through until we get to the very end of that file.

Next on the list is the StreamWriter class. This is going to be similar to the other option that we talked about, but this one is going to allow us to go further and write in the text file, rather than just reading. It is going to be an inheritance that comes from the abstract class known as TextWriter. The class is going to represent a writer, which is then able to come in and write out as many characters as they would like in that file. Some of the methods that we are going to be able to rely on when working with this class includes:

1.  Close: This is going to help us to close up the object we are currently on and the stream.
2.  Flush: This is going to help us clear all of the buffers for the current writer and will cause any of the data that has been buffered to be written over to the stream.
3.  Write: This one is going to write what we would like to the stream.
4.  WriteLine: This will help us write data specified by the overloaded parameters, followed by the end of the line.

The code below is a good one to work with because it helps us to implement this class so that it is able to accept the data from the user, and then will write all of that data into the file of our choice.

class  Program

{

    public  void  WriteData()

    {

        FileStream fs = new  FileStream(“E://data.txt”, FileMode.Append, FileAccess.Write);

        StreamWriter w = new  StreamWriter(fs);

        Console.WriteLine(“Enter the string”)l

        string str = Console.ReadLine();

        w.Write(str);

        w.Flush();

        fs.Close();

    }

    static  void  Main ( string[ ] args )

    {

        Program p = new  Program();

        p.WriteData();

        Console.Read();

    }

}

Now we are able to take a closer look at the code that we are working with here. In this code, we are going to find the FileMode property value, and this will be the Append value. Then the property value that comes with FileAccess is going to be Write in this case. We will open up the file named data.txt here and it will be in the append mode, which allows us to go through and add in more of the information that we want along with the way.

When we are in the append mode and using the code that we have above, the stream will be what we use and rely on for the write operation. When this is all said and done, we know that a new instance of the StreamWriter class is created for us to use.

Another thing that you may notice with this one is that the Flush() method is there, and it is responsible for clearing the stream buffer. At the same time, the Close() method is going to be there and can close up the stream while releasing the resources that have been associated with the stream at that time. This helps to keep it all together and working how we need it.

Being able to read and write on some of the files that you want to use in C# is going to be important. It will ensure that we are able to put together a lot of different parts, that we can view what is in one of our files, and that we are better able to even write out some new information on one of the files. Working with some of the code that we have present is going to make all of the difference when it comes to working on these files.

www.wideskills.com/csharp/file-input-and-output

#   Chapter 5: Making Choices and Decisions

While we are in the C# language, we need to take some time to work with the decision control statements or conditional statements. These are basically going to be the types of codes that are able to take the input from the user, compare it to the conditions that you set within the code, and then will make some important decisions on its own based on both of these.

There will be times when you write outcode, and you want to make sure that this program is able to handle some decisions on its own. You can choose to write it out so that there are specific conditions to find in the code ahead of time, and then the code is able to respond based on the input that the user has added into the computer.

The good news with this one is that there are a few options that you can choose from with these conditional statements. Each one is going to work in a slightly different manner based on what you are hoping to get out of the program as well, and how you would like it to respond to different inputs from the user. As we go through the different options, you will better be able to see how each one works and why it is such a great option for you to choose one of them along the way. Let’s dive in and take a look at some of the main conditional statements available in the C# language, learn how each one is going to work, and explore some of the basics of coding with them as well.

## A Look at the If Statement

The first kind of conditional statement that we want to take a look at here is known as our if statement. Out of all the conditional statements that we will look through, this one is going to be the most basic. It does miss out a bit on some of the functionality that we will see with these statements, but it does help us to learn more about conditional statements and can be useful in some situations as well, so it is important to learn.

When you handle this if statement, you will find that when it runs, the code will only provide us with a reply as long as the user gives us an input that matches with the conditions that are set in the code. When this does happen, then the code will be able to execute, and it will usually come up with some kind of message, depending on what the programmer puts into the code. Sometimes you will set it up to execute something else as well.

However, if the user comes through and puts in an input that does not match up with the conditions that we set up, then there will be nothing that shows up on the screen. This can cause some problems, which is why the if statement may not be used as much as some of the other options.

The good news out of all of this is that you will find, even as a beginner, that these if statements are easy to set up and work with. Let’s take a look at the coding below to see how we can create one of these if statements in the C# language for our own needs:

If (x > 0)

{

Console.Write(“The value is positive.”);

}

With the example that we listed above, there are certain things that need to happen. If the value that the user put sin is higher than zero, then the program is set up to print off “The value is positive”. However, if the expression turns out to be false, or the input is less than zero, then the program will ignore the whole statement that comes after Console. Write and will move on.

## A Look at the If Else Statement

As we can tell pretty quickly when we work with the if statement, there will be many situations where these statements are not going to be able to help us get things done in the manner that we want. You do not want to set up some codes that are not strong enough to handle the work that you want. It is never a good idea to set up a code where the user can put in something, and then the program just ends or freezes up. And this is where we will take a look at a new conditional statement, known as the if else statement.

The if else statement is going to be a nice one to work with because it adds in a ton of power to the code that we are doing and writing, while still allowing us to add in more than one option and handle pretty much anything that the user will add to the program. Sometimes we will only add in one or two options, but sometimes we can use the if else statement to handle a ton of options along the way as well.

To get to the point, we need to take a look at the syntax for the if else statement so we get a better understanding of how this will work in the C# language. A good example of the syntax for this one will be below:

If (the Boolean expression)

{The statement/s you want to run if the result is true;

}

Else

{The statement/s you want to run if the result is false;

}

As you can already see with this one, there is going to be a lot more power that comes with the if else statement. This is a basic option with the if else statement, but you are able to add in some more lines to make it more powerful. With these, if else statements, if the answer is false, your code will go on to the next part of the statement to see whether or not that one is true. If there are more than two options, it will keep going down the if else statement until the answer turns out true, and then it will go and display the message that comes up.

Now that we have taken some time to talk about it, it is time to look at an example of how this will work so you can use it in your own codes:

If ( x > 0)

{

Console.Write(“This value will be positive.”);

}

Else

{

Console.Write(“The value is less than or equal to zero.”)

}

You are going to find that when we work with the example above, the else clause is going to be important, or at least hidden until the Boolean expression ends up being false. It is there when the process will actually need the else statement. But if we end up getting a value that is true, then the first statement will be the one that will show up so we won’t need the else statement at all.

## What the Nested Conditional Statement is All About

Any time that we look through some of the new codes that come with C#, you should find that it is easier to work with two statements that we had above, or you can combine them to make a nested conditional statement for some of your codes as well. with a nested conditional statement, we are going to take one of the types of conditional statements above and place it inside of another one. The point of doing this is to add in some more complexity to the work that we want to see with coding, and can really give us a chain of conditions when they are needed.

The main thing that we have to focus on when it comes to handling any nested conditional statement is that if there is some mistake that happens when you write out the statement, it is going to cause an error in the whole thing, and it can take some time to fix. This makes them a bit difficult to handle and work with along the way so be careful.

The neat thing about them, though, and something that will make them pretty appealing is that they allow us to add in as many, or as few, levels as we would like. Even with this in mind, most professionals in this language will recommend that the nested statements stay around three levels or less so that they don’t become too big of a mess along the way.

If you do end up going past the third level when working on these statements, then you may end up with something that is unruly and doesn’t behave in the manner that you would like, and may not even work. As a beginner, stick with the three levels and go up to more as you get better with the coding.

Now, compared to the other two types of conditional statements, there will not be as many situations where you work with these nested statements, but they are still pretty neat to work with. If you do decide to work with a nested statement, it is important to know how they work, and some of the codings below is going to make this a possibility for you:

Double r = 60;

Double s = 70;

If (r ==s)

{

System.Console.WriteLine(“These numbers are equal.);

}

Else

{

If (r > s)

System.Console.WriteLine(“The value of the first variable is greater than that of the second one.”)’

}

Else

{

System.Console.WriteLine(The value of the second variable is greater than that of the first one.”)’

}

}

With the example that we are looking at above, you will have a few options that will work with the if else clause. This will allow you to pick out the command so that the program knows what it needs to readout. This will help you to do some more with your program and will make it easier to make the program more complicated.

There are many codes that you are able to write that will rely on these conditional statements. They really help you to make the code stronger and will ensure that we are able to handle some of the inputs that our users give to us, even if we are not able to guess ahead of time what answer the user is going to add to the program. These can base the input off any conditions that we set, and will ensure that the program is going to behave in the manner that we would prefer. This makes it so much easier for us to see results and for us to make sure the program works the way that we want.

#   Chapter 6: Basic Math

While we are on the topic, we need to spend a bit of time taking a look at how we are able to handle some of the operators that show up in our code. These operators will ensure that we are able to put together several different parts of the code, add them, subtract them, assign values, and more. In many of the coding languages that we can learn, operators are going to show up. Even though they are an important part for us to work with, we need to remember that they are simple, and it is not something to be scared about at all.

In this chapter, we are going to spend some time looking over the basics of the C# operators so we can see what kinds are there when we would need to use each type, and more.

## What is the Arithmetic Operators?

The first type of operator that we need to take a look at will be the arithmetic operators. These are pretty basic, and any of the mathematical symbols that you are used to working with, such as adding, subtracting, multiplying and so on, are going to fit into this category. It is likely that you are going to recognize most of the operators that show up in this one. So, any time that we want to work with some of these arithmetic operators remember that they are going to be in charge of helping us to tell the compiler that it is time to do some math.

With these, as long as the right mathematical symbol shows up in the code, and the numbers are put in the right position (this will depend on the answer that you want to get in the end), then the arithmetic options are going to work perfectly for your needs. With that in mind, some of the best arithmetic operators that you can work with will include:

*   “+” this is the addition operator. It is going to add two operands together. So you would get x+y=25
*   “-“ this is the subtraction operator. It is going to allow you to subtract the value of the right-handed operand from the left-hand operand. So you would get y-x=-5.
*   “*” this is the one that will tell the computer to multiply the two operands. So you could do x*y=150.
*   “/” this one is the operator that will tell the computer to divide the left-hand operand with the right-hand operand. For example, y/x.
*   “%” is often called the remainder of the modulo operator. It is going to divide the left-hand operand by the right operand and then returns the remainder.
*   “++” is the increment operator. It is going to increase the value of the operand by one. So you would have ++x=16
*   “—“ programmers will often call this the decrement operator. It is going to decrease the value of the operand by one. This means that you will have –x=14.

There are a lot of times when you will need to work with these arithmetic operators, and it often will depend on whether your program will need to add or subtract or do some other kind of math along the way. It can also be helpful if you are trying to add together two parts of the code, even if they are not numbers. As you look through some of the codes that we will do in this guidebook, you are likely to see some of these show up as well.

## What are the Assignment Operators?

There are times when you will use the arithmetic operators in some of the codes that you want to write. But these are not the only types of operators that you may want to work with either. Now that we know a bit about those and how they work, it is time to work with the second kind of operator in C# that we can work with, known as the assignment operators.

We are going to talk about variables a little bit more in some of the chapters that are coming up. But these are basically going to be a part of our code that is able to help us save a spot in the memory for a value of our choice. This is going to be really useful for some of the work that we want to do. But we need to make sure that we are able to assign a value to the variable. Without this, we are going to end up with an issue because we just reserved an empty spot in the memory of our computer.

The most common of all the assignment operators that we are able to choose from is pretty simple, as it is just the equal sign. This means that we can make up our variable in the code, and then just put an equal sign between this and the value that we want to assign over to the variable. The compiler will notice the equal sign and know exactly what you are trying to do.

While the equal sign is going to be the most common option, there are a few other operators that we are able to work with that fit under the umbrella term of the assignment operator. Some of these are going to include the following:

*   “=” this operator will allow you to perform simple assignment operations. It is going to assign the value to a variable that you are working on at that time. For example, writing int sample = 100 will tell the program that you want to assign 100 to the variable that is called “sample”. It won’t perform any extra processes on this variable or on the value involved.
*   “+=” this is the additive assignment operator. It is going to add up the values of your two operands and then will assign the sum to your left-hand operand.
*   “-=”  programmers will often refer to this as the subtractive assignment operator. It is going to subtract the value of the operand on the right side from the one on the left side and then assign the difference to the left-hand operand.
*   “*=” this operator will multiply the values of each operand and then will assign the product to the left-hand operand.
*   “/=” this is when you will divide up the two variables and then take the result and assign it to the variable on the left.

When you decide that you need to add in one of the assignment operators to your code, you have to make sure that both of your operands are going to fall into the same category of the data type. In some cases, while writing codes, the operands that you choose will not end up as compatible, and using these is going to make it hard for the program to behave in the manner that you would like. So, if you do end up with an error in this one, you can go through and change this part up, checking that the data points match up to how we want, and then working from there on it as well.

## What are the Relational Operators?

We have taken a look at the arithmetic operators so far. These are the ones that help us to do some of the math that we would like in our codes, and can add together numbers and parts of the code, while also working on other mathematical formulas along the way. We then went on to the assignment operators. The most common option for this is the equal sign that will help to give a value to one of the variables that you want to work with. Now it is time to move on to the relational operators and see what these are all about.

These relational operators are important to work within many codes because they make sure that we get an easy method to compare the values of two operands at the same time. Because we are able to make this comparison, these are usually going to be found inside of those conditional statements that we already talked about before.

With this in mind, we do need to take some time to look more closely at some of the types of relational operators that are available in the C# language, because there are a number of these that you can choose from. To help us make sure that this is going to work well, and that we can get a full understanding of how these work, assume for now that d = 100 and e = 150\. With that in mind, some of the relational operators that are found in the C# language includes:

*   “==” this is the operator that you can use to check the equality of two values. If the two values end up being equal, the operand will tell you it is true. Otherwise, the operand will tell you it is false. For example, saying the d == e would show up as false.
*   “!=” this operator allows you to test the inequality of two values. If the values end up not being equal, it will tell you this is true. For example, e != d would result in a true.
*   “>” this operator is used to check whether the operand on the left is greater than the operand on the right. If it is, then the operator will tell you it is true. For example, saying that e > d would be true.
*   “<” this is the less than an operator, it will allow you to check whether the operand on the left side is less than the operand on the right side. If it is, you will get it to show up true, such as the formula d < e.
*   “>=” this is the operand that will say it is true if the value of the operand on the left side is great then, or equal to, the operand on the right side. Otherwise, it will tell you the statement is false. For example, saying that e >=d evaluates as true.
*   “<=” with this operator, you will get a true if the operand on the left side is less than or equal to the operand that is on the right side. For example, d <= e is true.

Now, with this one, we do not want to make it more difficult than it needs to be. But we have to remember that when it comes to these, we are going to end up with the result that is always Boolean. This isn’t complicated. It simply means that any answer we get with these relational operators will either be false or true, and that will depend on the conditions that you add into the code.

Along with that idea, when we work with the relational operators, we have to check out whether we are working with the right amount of these equal signs. For example, if you are trying to work with the equality operator that we showed above, then there needs to be two, rather than one, equal sign. If you mix up these operators and end up with an assignment operator rather than a relational operator, the code will either not work the way that you want or there will be an error message that shows up.

## What are the Logical Operators?

We have had a lot of fun taking a look at some of the different operators that we are able to handle in this language, and now it is time for us to move on to some of the logical operators that are available for our work as well. These logical operators are also going to rely on Boolean expressions as well because they are going to accept a value that is Boolean and then can provide us with a new value that is Boolean when we are all done with it. This one, just like some of the other operators out there, will accept, as well as rely on, the answers being either true or false when you are adding them to your code.

Now, when it is time to work on these logical operators that can be added into codes in C#, you will find that there are going to be four main ones that we can spend our time concentrating on. We are going to look at some of the examples of how these work below. But remember here that we are going to assume that c is true, d is true, and e is false. With this in mind, we can look at the following logical operators that can show up in our codes:

*   “&&” this operator is called logical AND. It will only result in true if both operands are true. For example, d && c will evaluate to true.
*   “||” this is the logical OR. This operator is going to give you a true if at least one of your operands is true. For example, c || e will result in true.
*   “^” this operator is the Logical Exclusive OR, and it will result in a true if one of the operands is true. If both operands can be false or true, the operator will give you a false.
*   “!” with this one, you will be able to reverse the value of your Boolean variable. For example, if you type in !d, you will get a false.

## What are the Bitwise Operators?

Now that we have had some time to go through a few types of operators, especially ones that are pretty common in some of the other coding languages that you may work within other situations, it is time for us to take a look at a new kind of operator, one that may not be as common and you may not use it as often, but it is going to be important to helping you to get things done in your code. And these are going to be known as the Bitwise operators.

The Bitwise operator is going to be fairly similar to what is found with the logical operator, and in the beginning, it may seem like you are working with the exact same thing with them. The main difference between this bitwise operator and the logical operator is that the former is going to take a binary value and then will turn it into a Boolean value.

To make it simple, binary values are going to consist of 0 and 1, and will not look like the words that we are used to seeing out of the computer. Let’s take a look at some of the different types of bitwise operators that we are able to work with here.

For this, let’s assume that I = 0, h = 1, j =0 and g = 1

*   “&” this is the operator that is known as the Bitwise AND. It is going to assign 1 to the positions where both of the operands have 1\. For example, g & h will give you 1.
*   “|” this is the bitwise OR. It is going to assign 1 to the positions when there is at least one of the operands with a 1\. For instance, doing h | 1 will give you a result of 1.
*   “^” this is the exclusive OR that will work well for binary data. Just like working with the logical values, this kind of operator is only going to give you 1 in the areas that the operand has a 1\. For example, if you do g^j, you will get a result of 1.

You will find that the bitwise operator is going to take on a bit more work to accomplish compared to the other operators that we are talking about. And it is true that you will probably not spend a ton of time looking at and working on this operator in your beginner codes. But it is still an important operator to learn more about, and it is worth our time to learn how to make this work as well.

As we can see, there are a lot of different types of operators that we are able to work with, and each one will be able to help us get more things done in the long-term with some of our codes. The goal of each one is different, so it is often going to depend on what we would like to see happen in the code, and how we want it to play out for us. Make sure to take a look at some of these different types of operators and learn how you are able to use each one in some of the codes that you would like to write out.

#   Chapter 7: A Look at Polymorphism

The next thing that we need to focus on when it comes to working on the C# language is the idea of polymorphism. This is going to be seen in many cases as the third pillar when it comes to working with object-oriented programming, along with inheritances and encapsulation. This is an important topic that shows up in some of the more advanced parts that we will focus on with our coding, so it is important that we take a look at them now.

To start, polymorphism is going to be based on the Greek word for “many-shaped”. There are two main aspects that make this a distinct thing that we need to focus on, and these will include:

1.  When we get to run time, the objects that are in our derived class are going to be treated as the objects for our base classes in places, including the arrays, collections, and the method parameters. When this does happen, the objects declared type is not going to be identical to the type it was at run time.
2.  The base classes that we see are going to define and implement some of the virtual methods, and then it is possible for the derived classes to override them. This means that they are able to go through and provide their own implementations and definitions as we go through this. When we get to the run time, when the client code calls up the method that we are working with, the CLR is going to look up the type of the object at run time. This is then going to be the part that will override our virtual method. This means that in the source code, you are able to call up a method on a base class, and this is going to cause a derived class’s version of the method to be executed.

The virtual methods are there to enable us to work with some groups of objects that are related but in a uniform method. For example, maybe you are doing a kind of drawing application that will allow your user to come in and create a wide variety of shapes on that drawing surface. When you start, you will not know at compile time what shapes the user will want to create because it is always hard to guess on human behavior.

However, even with this kind of challenge, this program will need to pay attention and hold onto information about the shapes we can work with, and the ones that the user creates, and then it has to be able to update them in the proper manner in response to what the user does with the mouse. The neat idea here is that we are able to work with a polymorphism in order to solve this problem with the help of two basic steps. Those steps are going to include:

1.  The first step that we are able to do is create our own class hierarchy, where all of the shape classes are going to derive from some of the common base class.
2.  Another option that we can work with is to bring up the virtual method, which is going to make sure that the correct method  of the classes that we derive when we work with just one call back with the base class method we work with as well.

With this in mind, we need to start this out by creating a base class that we are going to call Shape, and then we need to go through and create some of the derived classes that we need, such as Circle, Triangle, and Rectangle. We can give the shape class a virtual method that is known as Draw, and then we would work to override it in all of our classes that are then derived from the original so that we can actually draw out the shape that the class is supposed to represent, and that the user is looking for.

From there, we are going to work through in creating our own List<Shape> object and then add in a Circle, Rectangle, and Triangle to this. If we would like to be able to update our drawing surface inside of this application, we will want to work with the foreach loop in order to iterate through the list and to call up the method of Draw and on each of the Shape objects that are in your list.

Even though all of the objects that are on this list have been able to declare the type of Shape that they are, it is going to be time to look at the type for the run time that will be invoked. This is going to be the overridden version of the method that is found in each class that we derived in this process if we would like.

One thing that we need to remember when we are working on this kind of process is that in this language, each type is going to be polymorphic because of all of the types, even the ones that the user is able to define on their own is going to inherit back from the object. This is a little bit different than what we are going to see with some of the other options out there, so we need to keep track over that and make sure that we are using it in the right manner because it is not found in the other languages that we want to focus on.

Another thing that we need to take a look at is the virtual members that come with this process. When we are looking at one of our derived classes and how it is going to inherit from a base class, it is going to gain all of the fields, methods, events, and properties of the base class. The one who is able to design one of the new classes will be able to choose between a few actions to take in order to make the class behave in the manner that they would like. Some of these options are going to include the following:

1.  They can override some of the virtual members that are found in the base class.
2.  They can go through and inherit some of the methods of our base classes without needing to override that base class at all.
3.  They are able to go through and define some of the new implementations that are not considered virtual, and those are the members that are going to help us hide the implementations of our base class at some point.

We must remember though this that the derived class is able to come in and override the base class member in some situations, but only if the member of the base class has been declared as either abstract or virtual. The derived member needs to work with the keyword of override to help it indicate that the particular method we are on is supposed to participate in the invocation that we spend time on here.

In addition, the fields are not things that we are not able to turn into virtual objects. Only properties, indexes, events, and methods can turn into something virtual. When a derived class is able to go through and override a member that is virtual, that member is going to be called up, even when we get into a situation with an instance that has the class accessed as the instance of the base class we are using.

Virtual methods, as well as the properties that come with them, will enable the derived classes to go through and can make it easier to extend out the base class, without having to actually do some of the implementing that is usually needed on this method. An interface is also a good method to work with when we would like to define the method we are working with or when we would like to work with a set of methods that has the implementation left to the derived classes as well.

Another thing that we may want to work with when it comes to the idea of polymorphism is how to hide some of the base class members in with some of the new members that we want to work with. If you would like to handle some of the derived members and get them to come in with the exact name that we see with the base class member, but we won’t work with some of the virtual invocations, you can work with the keyword of “new”. This is a keyword that we are going to put ahead of the class member that will be the return type that we are trying to replace with this one. The following code is going to show us how this is meant to happen:

public class BaseClass

{

    public void DoWork() { WorkField++; }

    public int WorkField;

    public int WorkProperty

    {

        get { return 0; }

    }

}

public class DerivedClass : BaseClass

{

    public new void DoWork() { WorkField++; }

    public new int WorkField;

    public new int WorkProperty

    {

        get { return 0; }

    }

}

When you have a base class member that is hidden, it is possible to still access this from the client code with the help of  us being able to cast the instances of the class that is derived over to the base class instance if we would like.

Next on the list to focus on a bit is learning how to prevent the derived classes from going through and overriding the virtual members. These virtual members are going to remain virtual for an indefinite amount of time, no matter how many classes you go through and declare what is there between our virtual members and the class that was supposed to declare it in the first place.

With this one, if we want to bring out the original class, or Class A, and we have this class be the one that will declare our virtual member, and then we will have class B come in and take that member from class A. It is possible to go down the line and have class C take from the class before it, which is class B, then it is possible to inherit that virtual member as well, and it is going to do the process of overriding, regardless of whether class B went through and did the declaration that would do the override in the first place.  They are going to have a bit of independence from one another along the way as well. A good example of how this is going to work will be below:

public class A

{

    public virtual void DoWork() { }

}

public class B : A

{

    public override void DoWork() { }

}

And finally, the last thing that we are going to take a look at is how we are able to access the whatever the base class for these members are from our derived classes. Then this derived part is going to be the one that is able to replace or override the property or the method, and it still has the power to access the property for that base class in the first place. But it has to be able to work with the keyword of the base. The code that we are able to use to make this action happen for our needs includes:

public class Base

{

    public virtual void DoWork() {/*...*/ }

}

public class Derived : Base

{

    public override void DoWork()

    {

        //Perform Derived's work here

        //...

        // Call DoWork on base class

        base.DoWork();

    }

}

One last thing that we need to focus on when it comes to this topic is that it is often recommended that we spend some time working with some of the virtual members and that we work with the base keyword to help us call up all of the implementations of our base class when it is time to have that member come in with their own implementation. Allowing the behavior of the base class show up is going to enable that derived class to concentrate on implementing some of the necessary behavior that is specific to the class that you just created. But  if the implementation of that base class doesn’t happen at all, and we never call it up, then it is going to be the sole responsibility of the class that was derived to double-check that the behavior it is using will be compatible with the behavior that we see in the base class.

# 
Chapter 8: Enumerations

In the C# language, we are also able to work with parts that are known as enumerations. This is going to be one of the main data types that we can work with if we need it, but they are a little bit more specialized than what we see with the other options. For example, the enum type, or the enumeration type, is going to be one of the types of values that have been defined by a set of named constants of our underlying integral numeric type. To make it easier for us to define the enumeration that we are working with, we simply need to bring out the keyword of enum and then specify the names that we want to provide to the members of this type. A good example of the code that we can do that fits into this, and will help us to define the enumerator will include:

enum Season

{

    Spring,

    Summer,

    Autumn,

    Winter

}

We should know here that by default, the constant values that are going to be associated with these members are going to fall into the integer type. This means that they are going to be some kind of number and will start with zero before increasing by one following the text order definition that we want to handle in this part.

In addition, we are able to explicitly go through and specify any of the other types that are integral numerals as well if it is going to work as the underlying type for this class. We are also able to go through this and specify out the constant values that are associated, such as what we are going to see with the code below:

enum ErrorCode : ushort

{

    None = 0,

    Unknown = 1,

    ConnectionLost = 100,

    OutlierReading = 200

}

You are not able to go through and define a method inside the definition of the enumeration type, so try not to fall into the trap of doing this. To add some of the functionality that you would like to this type, we would need to create what is known as an extension method. The good news is that this is actually easier to work with than it may seem.

The default value that we are going to get with the enumeration type E is going to be the value that we will get when we work on the expression of (E) 0, even if you have zero sitting there and it is not going to correspond back to the member of our enum type at all.

It is also possible for us to go through and work with an enumeration type to help represent a choice from a set of mutually exclusive values, or we can do this same thing with a combination of choices as well. to make it easier for us to go through and do the process of a combination of choices if that is what is needed, then we need to work on a slightly different approach of having the enumeration type turn into bit flags instead.

Enumeration then is going to be a data type value in this language that is used for the most part to help us assign the string values or the names to some of our integral constraints. This is done to ensure that the program we are working on is easy to read and maintain over time.

For example, the four suits that we see on a deck of cards could be the four enumerators that we want to work with, and we know they are named Club, Diamond, Heart, and Spade, but they will then belong back to the enumerated type that we are able to list out as suit.

Another example of this would be some of the more natural enumerated types, such as directions, colors, days of the week, and even the planets. The main objective with these, no matter what the point of them is all about, is to help us to go through and provide a good definition for our own types of data. Enumeration is simple to declare because we just need to use the keyword of enum and make sure that it is found right inside of the structure, class, or namespace as well.

## How We Can Turn Enumeration Types Into Bit Flags

We just took a look at how to work with some of the enumeration types and even discussed that there are times when we would want to turn this type into a bit flag. Now we need to take a look at how we are able to accomplish this kind of process too.

If you would like to work with an enumeration type in order to help us represent combination of choices, we need to define the enum members for those choices such that the individual choice that we are working with is going to turn into a bit field as well. This means that the associated values for those members need to be to the power of two. Then it is possible for us to work with the logical operators that are bitwise, such as the | or & operators so that we are able to combine the choices or intersect combinations of choices based on which one we are using.

Now, if we want to go through this and indicate that one of the enumeration types we have in our code is going to be declared as a bitfield, then we need to make sure that the right flags are applied to it. A good example of this is going to be below. And you will notice that with the example below, you are able to go through and include some typical combinations when it comes to the definition of our enumeration type as well.

[Flags]

public enum Days

{

    None      = 0b_0000_0000,  // 0

    Monday    = 0b_0000_0001,  // 1

    Tuesday   = 0b_0000_0010,  // 2

    Wednesday = 0b_0000_0100,  // 4

    Thursday  = 0b_0000_1000,  // 8

    Friday    = 0b_0001_0000,  // 16

    Saturday  = 0b_0010_0000,  // 32

    Sunday    = 0b_0100_0000,  // 64

    Weekend   = Saturday | Sunday

}

public class FlagsEnumExample

{

    public static void Main()

    {

        Days meetingDays = Days.Monday | Days.Wednesday | Days.Friday;

        Console.WriteLine(meetingDays);

        // Output:

        // Monday, Wednesday, Friday

        Days workingFromHomeDays = Days.Thursday | Days.Friday;

        Console.WriteLine($"Join a meeting by phone on {meetingDays & workingFromHomeDays}");

        // Output:

        // Join a meeting by phone on Friday

        bool isMeetingOnTuesday = (meetingDays & Days.Tuesday) == Days.Tuesday;

        Console.WriteLine($"Is there a meeting on Tuesday: {isMeetingOnTuesday}");

        // Output:

        // Is there a meeting on Tuesday: False

        var a = (Days)37;

        Console.WriteLine(a);

        // Output:

        // Monday, Wednesday, Saturday

    }

}

This is just the beginning of what we are going to see when we work with these enumerations, and it is important to explore some more about the flags and how they can work with this process as well. if you want to work on this, it is a good idea to take the ideas a bit further and see how they are going to work for your needs as well.

## System.Enum Type

Another thing that we are able to take a look at is the System. Enum type. This is an important part of the process and will ensure that we are able to add in a bit more functionality to some of the codes that we are writing out in the C# language. To start, the System.Enum type is going to be the abstract base class that is there for all of the types of enumeration that we handle. It is going to provide us with a lot of methods that we can utilize along the way in order to gain more information about the enumeration, what type it is, and what values are found inside of it.

Beginning with the 7.3 version of the C# language, you are able to start using the System.Enum in a base class constraint. This is often going to be referred back to as the enum constraint. This is going to be useful when you would like to specify that a type parameter is actually an enumeration type. It is not going to be used all of the time, but there are situations where this can be useful to learn more about as well.

## Handling Some Conversions

We can also work with these enumerators to help us to handle some of the conversions that need to be done. For any type of enumeration that we want to add to our code, there is going to be a kind of explicit conversions between the type of enumeration that we focus on and the integral type that is going to be underneath it as well.

If you decide to go through, and then we can cast the value of enum to the type that is under it, the result is going to be the associated integral value that is found with this member as well. A good example of how we are able to work with the idea of conversions with our enumerations will be below:

public enum Season

{

    Spring,

    Summer,

    Autumn,

    Winter

}

public class EnumConversionExample

{

    public static void Main()

    {

        Season a = Season.Autumn;

        Console.WriteLine($"Integral value of {a} is {(int)a}");  // output: Integral value of Autumn is 2

        var b = (Season)1;

        Console.WriteLine(b);  // output: Summer

        var c = (Season)4;

        Console.WriteLine(c);  // output: 4

    }

}

We are able to work with the Enum.IsDefined method, in order to help us figure out whether one of the enumeration types that we are focusing on is going to contain the enum member with the value that we are looking for. If it is there, this is going to help us to see what is present but will return a null answer if the associated value that we want to focus on is not present in our code.

For any of the different types of enumerators that we are working with, there are going to be several conversions. This is mainly the boxing and unboxing conversions that we can work with, and these conversions allow us to go to and from the System.Enum type, respectively.

# 
Chapter 9: Multithreading

Multithreading is a unique topic that we are going to find in a lot of the object-oriented programming languages that are out there, including in the C# language. It is a bit more complicated, but it is always going to be good for us to learn a bit more about how it works, and what we are able to do with this overall.

To start, a thread is going to basically be the execution path of our program. Each of the threads that are there will define for us a unique flow of control. If you are working on an application that is going to involve some complicated operations or some that take up a lot of time, then you may find that it is a lot more helpful to go through and make sure that there are different execution threads or paths and that all of the threads are individually able to perform the job that they would like.

Threads are going to be a process that is pretty lightweight. One example of us using one of these threads in our programming would be when we would like to implement concurrent programming in one of our modern operating systems that are in use. When we choose to undertake this process with threads, it is going to help us to save on some of the waste that happens with the CPU cycle, and it will make sure that the application that is being used is as efficient as possible.

We did not have a lot of time to talk about threading in one of the other chapters, but often when threading is brought out, it is going to be used as multithreading because this allows for a lot more processes to happen overall. This is because the threading is only going to allow us to run one application at the time, and each application, with just the simple threading, is only able to take on one job at a time.

As we can imagine, some of the simple projects that we start with may be fine with some of the simple threading that we may find in other options. But many times we will work with an application that is going to be able to handle more than one task at a time. And when this is true of your own processes as well, it is time to divide them into some smaller threads, and this is where multithreading is going to come into play.

## The Lifecycle of a Thread

The first thing that we need to take a look at here is the idea of the life cycle of a thread. This is going to be a process that is able to start when an object of the System Threading is there. This allows us to start our own threading class and will make sure that the process is able to end when the thread either has a chance to complete all of its execution or when we terminate it on our own.

There are a few different states that we are going to see when it comes to the cycle of one of the threads that we want to work with. And some of these states or stages will include:

1.  The un-started state: This is going to be the situation when the instance of the thread can be created, but we are not going to call up the Start method.
2.  The Read State: This is going to be the situation where the thread is all set up and ready to run through its actions, and it is simply waiting for the CPU cycle to be ready as well.
3.  The Not Runnable State: This is going to be a thread that we are not able to execute the thread. There are a few reasons for this one including:
    1.  The sleep method is what has been called up instead.
    2.  There is a blockage in the I/O operations
    3.  The wait method is the one that has been called up instead.
4.  The Dead State: This is going to be the situation where the thread is going to either have to go through and complete the execution the whole way, or it is going to be aborted in the process.

## A Look At the Main Thread

We can also take some time to look at what is known as the main thread. When we are working on some of the codes that we need in C#, we will find that the System.Threading.Thread class is going to be used in order to work with all of the different threads that are found in your codes. This one is going to allow us to not only create but also access the individual threads that we need when we want to work with an application that needs more than one thread. The first thread that we will have set up to execute in our process is going to be important though, and this is often known as the main thread.

When the C# program is able to start up its execution, then the main thread is going to be created in an automatic manner. The thread is going to be created with the help of our class known as Thread, and it can then be known as one of the child threads out of our main thread. You are able to access this thread with the property of CurrentThread in this class if you would like.

## Properties of the Thread Class

While we are here, we need to take some time to go through some of the properties that are the most used and the most common when we are working with the Thread class that has been so important through this chapter so far. Some of these main methods and properties will include:

1.  CurrentContext: This is going to help us to take a look at the thread that is executing at this time and will provide us with the current context as well.
2.  CurrentCulture: This is going to help us to either get or set up, the culture that we would like to find on the thread we are currently using.
3.  CurrentPrinciple: This is going to help us to either get or set up, the current principal that is found on our thread. This is important because it is going to be used often for the security of that thread.
4.  CurrentThread: This one is going to list out the thread that is currently running.
5.  CurrrentUICulture: This is going to be the one that we are able to use to either get or set up the current culture with the help of the Resource Manager. This can then help us to figure out some of the resources that are culture-specific when it is time to run the program.
6.  ExecutionContext: This is going to provide us with the object that we need in order to look through all of the information about the different contexts that are found in the thread that we are working with.
7.  IsAlive: This one is going to provide us with a value that will indicate the status of execution on our current thread.
8.  IsBackground: This one is going to help us to either get or set up a value that will help to indicate whether or not a thread is going to be one of the background threads or not.
9.  IsThreadPoolThread: This is going to provide us with a value that will help us know whether or not that specific thread we are working with is going to belong to the thread pool that is being managed.
10.  ManagedThreadid: This is going to provide us with a unique identifier for the managed thread that we are currently working with.
11.  Name: This one will help us to get or set the name of the thread when we are ready to have that setup.
12.  Priority: This is going to help us to get or even to set up the value that will help us to know what the priority is for this thread when it comes to scheduling things.
13.  ThreadState: This is the final part of the properties that we are going to look at, and it is going to provide us with some of the value that we need when it is time to look at the states of our current thread.

## Creating Threads

It is possible for us to go through in some of our codes and create any of the threads that we would like along the way. It is up to us how many we think the code is going to need as well. Threads are relatively easy for us to go through and created, we just need to make sure that we are able to go through and extend out the Thread class that we have been talking about. The extended Thread class is then going to work on the process of calling up the Start() method so that we can begin with this and then look towards the child thread execution.

There are a lot of benefits that we are able to work with when it comes to handling a lot of the different parts that we are able to work with. If you want to run things on the operating system of your choice if you would like to work with more than one application at a time. Without having to make them wait for one another along the way, the multithreading will ensure that we are able to do this all in one.

We need to make sure that we fully understand the process that comes with threading and multithreading, especially if we are working with the C# language. It may not seem like it is all that big of a deal when we get started, but it can definitely make a difference to how well our codes are going to behave and whether we are able to get more than one thing done at a time.

If we work on a system that does not allow for multithreading, then we are going to have a lot of downtime and waiting. If there is already a process up and running on the computer or the system, then all of the other processes have to stop and wait their turns before they can do anything at all. Once the first process is done, then we can work on the second, and then the third, and so on down the line until it is all done.

We can quickly see why this is going to be such a big pain to work with overall. It is never very efficient to work in this manner because it forces us to wait around to get one process done at a time, and can be slow and time-consuming. Multithreading is going to come into all of this and make it better. It helps us to actually handle more than one process at a time.

For example, you could run your anti-virus on a computer, allowing it to go through a scan, while also doing some searching online. You can download a new game or another program on your computer, and then, while the download is going on, you will be able to open up a Word document and do some work or search on social media. Without multithreading, you would just have to sit around and wait until the download is done. With multithreading, you are able to handle more than one task at a time.

One thing to remember is that the power on your computer is going to determine some of these as well. If your computer does not have a lot of power or memory with it, then this multithreading is not going to be as efficient as we would like. But with a strong computer, multithreading is going to work in a seamless manner to help us to get more done in the process as well.

There are a lot of times when we will work with multithreading, and it is definitely worth our time to learn more about it. When it comes to all of the uses that we have for the C# language, it makes sense that this multithreading is going to be used as well.

# 
Chapter 10: The Variables

The next topic that we need to take a look at when we work with the C# language is the types and the variables. There are going to be two types that we are able to see in this kind of language, and they are known as the reference types and the value types. Variables that are considered a value type will be able to contain the data in a more direct manner while the reference type is going to store references to their data. The latter of these will be known as the objects that we are used to from before.

With the reference type though, we are going to find that it is possible for two of the variables to go back and reference the same object, and in the same manner, it is possible for the operations that we see in one variable to come back and affect the other variable as well. But when we are working with the value types, we will notice that the variables are each going to hold onto their own copy of the data and that it is not going to be possible for us to have an operation in one of them come in and affect one of the others. There is an exception to this where it will not work in this manner when we use the out and ref parameter variables in our codes. 

So, we now need to go a bit more into what the variable is going to be all about. To start, the variable is just going to be the name that we are able to give out to the storage area that we find in our programs, in which the program is able to manipulate along the way as well. Each of the variables that we will find with this language will come with their own specific type, which is going to determine the layout and the size of the memory of the variable. This can also tell us a bit more about the values and the range of values that we will be able to store within that spot in the memory. It also tells us the operations that we are able to apply back to that variable as well.

The basic value types that are found in the C# language are going to be found below:

1.  The integral types: These are going to include options like char, ulong, long, unit, short, byte, and more.
2.  Floating-point types: These are going to include the double and the float types that we have seen so far.
3.  Boolean types: These are going to be based on the idea of the value or the results being true or false.
4.  Decimal types: These are going to be any of the values that are decimals.
5.  Nullable types: These are going to include any of the data types that are considered nullable at the time.

Along with this idea, the C# language is going to allow us to have a few other defining types of values. We have looked at a few of these, including the reference types and the enumerators of our variables. And this would even count as the class that we talked about as well.

These variables are easier to work with than they may sound in the beginning. They have been designed to help us get a lot of work done in the process, and they will basically take a part of the memory of our system or our computers and then reserve it. Then we are able to go through and look through some of the different data types before assigning them to the variables that we have.

We have to make sure that there is some kind of value that is assigned back to the variable that we want to work with. This is going to be a bad thing because if we just have a variable without any value assigned to it, then we are just reserving some empty space in the memory of our computer. And the code is not going to pull anything up when we try to call this variable. It is always a good idea to work on assigning this value as soon as possible so you can make the program work in the right manner.

Remember back to some of those operators that we talked about earlier. We were able to work with the assignment operator in order to take control of some of the work that we were doing with these variables. Basically, we will work with the assignment operator, specifically the equal sign, to let the compiler know which value we would like to attach to that variable.

We are also able to add more than one value to our variable if we would like. This takes a little bit more work to get it all done, but you simply need to just continue working with the assignment operator, or the equal sign, to let the compiler know that you need to assign two or more values to the same variable if you would like.

## How to Define the Variable

The next thing that we need to take a look at here is how we are able to define our variable. The syntax that we are going to see with this one will be below:

<data_type> <variable_list>;

Of course, this is going to just be a simple example of what we are going to see, but it gives us an idea of what we are able to do and how we can make this work in some of our own codes.

With the syntax that is above, we need to make sure that the type of data part is going to be one of the valid types of data that C# will support. This would include double, float, int, and char. And if you go through and define one of your own types of data, then this would fit in as well. in addition, the variable_list needs to go through and contain at least one, if not more, identifier names, and it should be separated out by commas along the way.

## Initializing the Variables

Another thing that we are able to work with is initializing the variable. These variables are going to be initialized or assigned a value when we have an equal sign, and then we will follow that by a constant expression. The general form that we are going to see with this one is the following:

Variable_name = value;

Variables are unique in that they are able to be initialized in the declaration that you use. This means that we are able to take the code that we had above and actually add in the data type that we want to work with as well. It is as simple as that.

It is always a good idea for you to work with the variables in the right manner, and for you to make sure that you are able to initialize the variables in the proper manner. If you do not perform this in the right manner, it is possible that the program is going to produce some results that you are not expecting in the first place.

Now that we have had a chance to talk about this a bit, it is time for us to go through and look at some of the examples of the coding that we are able to do, and how we can make these variables work for our needs as well.

## Lvalue and Rvalue Expressions

Other things that we need to take a look at while we are here are the known as the Rvalue and the Lvalue in C#. There are going to be several expressions that are going to show up in a lot of the codes that we are trying to do, and these are going to include:

1.  The lvalue: This is going to be a kind of expression that will appear either at the left hand or the righthand side of the assignment that you are working with as well.
2.  Rvalue: this is going to be an expression that could show up on the right of our assignment, but it is not going to take on the left side of the table at all.

The variables are able to be lvalues, and this is why they could often appear so that they are on the left side of the assignment at hand if that is where we would like to find them. On the other hand, the numeric literals are going to be seen as the rvalues in this and it is possible that they will never be assigned in this case, and they definitely are not going to show up on the left part of this at all. This is why we need to learn the differences here and where all of the parts are going to fall when we are doing some of the work that we want.

As we can see, there are a lot of things that we need to consider when it comes to working with the variables and learning what they are able to do to benefit our work as well. There are a lot of times when we are going to utilize these variables, so it is worth our time to learn about them and to practice a few codes with them, so we get the best benefits out of this as well.

# 
Chapter 11: Encapsulation

The final chapter that we are going to take a look at before we go on with some of the different codes that we are able to write out in this language is the idea of encapsulation. This is going to be the process that we are able to use in order to enclose up one, and sometimes more, items into a logical or a physical package. Encapsulation, when we take a look at it in an object-oriented programming language like C#, is going to prevent access to some of the details of implementation that are there.

Encapsulation and abstraction are going to be features that are related to these kinds of languages. Abstraction is a bit different because it is going to allow us to make some of the information that is relevantly visible to the parts that need it, and then the process of encapsulation will enable the programmer to decide how much abstraction should be present. It will allow us to make parts of the code, either visible or hidden, based on how we would like those parts to be put away.

Encapsulation is going to be implemented when we work with access specifiers. This is something special in the codes that we are going to work with because it is responsible for helping us to define the visibility and the scope of a class member. There are a number of these access specifiers that we are going to find in the C# language, and some of these are going to include protected internal, internal, protected, private, and public.

## Public Access

While we could take some time to look at all of these, we are going to take a look at the three most common types, and the ones that are going to have the most to do with a lot of the codes that you want to write out in C#. The first option that we are going to look at is known as the public access specifier.

This one, in particular, is going to help out some of the codes that we want to write because it is going to allow one of the classes that we have the ability to expose its member variables, and even some of the member functions to other parts of the code, including some of the objects and the functions that we are working with. Any public member will be easy to access from outside of the class. If this is something that you want to see happen at this part of the code, then you will want to work with the public access specifier. But if not, then we would want to work with one of the other options.

This is simple to do in some of our C# codes, but we need to take a look at some of the actual coding that we are able to do with this one to get the best results. We can see the code to work with these in C# below:

using  System;

namespace  RectangleApplication  {

 class  Rectangle  {

 //member variables

 public  double length;

 public  double width;

 public  double  GetArea()  {

 return length * width;

 }

 public  void  Display()  {

 Console.WriteLine("Length: {0}", length);

 Console.WriteLine("Width: {0}", width);

 Console.WriteLine("Area: {0}",  GetArea());

 }

 }//end class Rectangle

 class  ExecuteRectangle  {

 static  void  Main(string[] args)  {

 Rectangle r =  new  Rectangle();

         r.length =  4.5;

         r.width =  3.5;

         r.Display();

 Console.ReadLine();

 }

 }

}

Take some time to type this into your compiler and see what kinds of answers you are able to get out of the process. When we look at this, we will notice that the length and the width that come with the variables here are going to be declared as public. This means that they are accessible from the Main() function using the Rectangle class that we named as r if we would like.

The member function of GetArea() and Display() can also help us to access some of these variables in a more direct manner, and we will be able to accomplish this without having to work with any kind of instance of the class at all. Then there are the member functions that we called the Display(), and we declared these as public as well. so it is going to be something that we are able to access from this class as well.

There is a lot that is going on with this kind of code that we just wrote out. But the whole point is that we are able to work on it to make the different functions and variables that we are able to work as public. This allows the main function there to access that part and will help certain codes to work in the manner that you would like as well.

## Private Access

In addition to working with the public access that we just did, it is time for us to go through and work with the private access specifier. This is going to be the opposite of what we saw when we talked about the public option. This one is going to make it possible for the programmer to come in and hide some of the member variables and the functions as well from some of the other objects and the functions that are in the code.

Only the functions that are able to stick around in the same class would be able to have any kind of access to the private members along the way. In this specifier, you will find that even an instance of a class is not going to be able to come in and access any of the private members. A good example of this one is going to be in the code below:

using System;

namespace RectangleApplication {

   class Rectangle {

      //member variables

      private double length;

      private double width;

      public void Acceptdetails() {

         Console.WriteLine("Enter Length: ");

         length = Convert.ToDouble(Console.ReadLine());

         Console.WriteLine("Enter Width: ");

         width = Convert.ToDouble(Console.ReadLine());

      }

      public double GetArea() {

         return length * width;

      }

      public void Display() {

         Console.WriteLine("Length: {0}", length);

         Console.WriteLine("Width: {0}", width);

         Console.WriteLine("Area: {0}", GetArea());

      }

   }//end class Rectangle

   class ExecuteRectangle {

      static void Main(string[] args) {

         Rectangle r = new Rectangle();

         r.Acceptdetails();

         r.Display();

         Console.ReadLine();

      }

   }

}

You can take a bit of time here to type in the code and see what the output is going to be in all of this. In this example, we took some time to hide the different properties that are going to show up in some of your codes. In this example, the member variables of width and length are going to be seen as private. This means that the function of Main()will not be able to access these at all.

The functions that are found in the same part of the code, or the same class, are able to access the variables. But those functions, the Display() and the AcceptDetails() will be public, so the Main() function is able to call them up and use them as long as they work with the instance known as r, or the Rectangle class we are working with.

## Protected Access

Another option in the specifiers that we get to work with is the protected access options. These are going to allow the new class, or the child class, the opportunity to access the variables and functions of that original class it is associated with. This is going to help in implementing some of the inheritances that we want to handle as well. This is something that is really going to be reserved for when we want to work with the idea of inheritances, but it is still a good thing to learn more about and understand that there is part of the encapsulation process that we are talking about here.

## Internal Access

The final option that we can spend our time on is internal access specifier. This is going to allow a class to go through and expose some of the variables of a member and the functions to some of the other functions and objects, but only if they are in the current assembly. What this means that any member with this kind of specifier is accessible from any method or class that has been defined within the application in which we have defined the member.

A good example of the code that we are able to work with in order to see how this one is going to work will be the following:

using System;

namespace RectangleApplication {

   class Rectangle {

      //member variables

      internal double length;

      internal double width;

      double GetArea() {

         return length * width;

      }

      public void Display() {

         Console.WriteLine("Length: {0}", length);

         Console.WriteLine("Width: {0}", width);

         Console.WriteLine("Area: {0}", GetArea());

      }

   }//end class Rectangle

   class ExecuteRectangle {

      static void Main(string[] args) {

         Rectangle r = new Rectangle();

         r.length = 4.5;

         r.width = 3.5;

         r.Display();

         Console.ReadLine();

      }

   }

}

Take some time to type this into your compiler and see what results you are able to get. In this example, you should be able to notice that the member function that we were able to label GetArea() is not going to be declared with any of the access specifiers that we saw before. If this were true, then the part that would be considered our default for this if we do not go through and mention what we would like it to be? In all cases, it would be private.

This means that if you do not go through and actually put in which of the specifiers that you would like, then the compiler is automatically going to assume that it is private and that we should keep it in this manner as well. if you don’t mind whether or not it is private, then just keep it this way. But if you would like other parts to access it, then you need to go through and add in the specifier that you would like to work with.

And then there is one more option that fits in with this one that we need to look at as well. this is going to be the protected internal access specifier, and it is going to be the one that is going to allows the class to have a way to hide all of the functions and the variables that are going to be members here from the other classes and functions in your code, but it is still open to the child class that shows up in the same applications. This is also a method that we are going to work with when it comes to the inheritance features from before.

As we can see, there are a lot of times when we are going to work with the idea of encapsulation, and it is often helpful to make sure that we are granting the right permissions to our codes. In some cases, we want to have open and public access, and other times we would prefer to not have this and to keep different parts private and away from one another. This is exactly what the process of encapsulation will do for us.

# 
Chapter 12: Simple Projects to Get Some Practice

We have spent a lot of our time in this guidebook taking a look at a lot of the codes that we are able to write out in C# and how we can make all of these parts come together for some of our own needs as well. one of the best ways to ensure that we are going to get really good with some of the codings that we want to do in this language, and to ensure that it is going to behave in the manner that we want is to do some practice along the way.

Each of the programs that you will want to write out will be a little bit different as well, and it is important for us to go through and check out the different aspects are going to work in any and all of the codes that we want to write as we go along here.

That is why this chapter is going to help us out one more time with some practice code that will result in a game that we are able to create on our own as well. This code is going to help us to learn more about some of the different parts that we have already collected and learned about along the way and will ensure that we are able to really make all of this come together for our needs as well.

In the code, you will notice that it is going to fit a lot of parts together, will ensure that we see some of the loops and the conditional statements, and can even show a lot of the comments, keywords, operators, and more in a more practical manner, and with putting them all together in one part of the code, compared to what we did before.

With that in mind, let’s take a look at how we are able to create one of our own Hangman Games and get it to work not only with some practice in the C# language but also ensuring that we are able to get the most out of actually having a game that works with our own code:

## Creating Hangman in C#

This is going to be the program that we will spend a bit of time on in this chapter. When you first look at the source code, it is going to be really long. And you may make the assumption that it is going to be too difficult for a beginner to learn how to do. But in actuality, the program is just long and not that complicated considering all of the parts that it needs to be able to do.

Think about what all goes into a simple game of Hangman. You need to have it pick out a random word for you, and then you need to make sure that it is going to know which letters are right and which ones are wrong based on the word that is up there. And there usually has to be a certain number of chances or the user to try out before the game is done, or they win. All of this has to show up in the code that we need to create below.

In the one below, we are going to set up a code that will have some blank boxes that show up at the top of the windows so that the letters that you guess right are going to show up there. The user is going to have to guess the letters and see if they can get them right. Of course, each time that the user, or you, goes in and makes a wrong guess, then the program is going to show another part of the hanged man. If you end up with 5 mistakes here, then you are going to lose. But if you guess all of the letters, you are going to win.

Now that we have the source code in place, it is time for us to go through a better explanation of how this is going to work. The event handler is first going to come through and help disable the button that is clicked, which will ensure that the user is not able to go in and click on all of that again. From there, it is going to spend time getting the tag property from the button, will convert that over to the letter of the button, and then will take the time to determine whether or not the letter is actually found in the word that we are currently working with.

We will not go over the whole code here because it can seem like a lot that we are dealing with, but a little bit of code can be worth our time to look over. Take a look at the code that we will have below, and see if you are able to recognize some of the parts that are there and how much you can remember from the other parts of our program:

/// <summary> /// Randomizes a word reading text file /// </summary> private  void SelectWord() { string filePath = Path.Combine(Path.GetDirectoryName (System.Reflection.Assembly.GetExecutingAssembly().Location), "Words.txt"); using (TextReader tr = new StreamReader(filePath, Encoding.ASCII)) { Random r = new Random(); var allWords = tr.ReadToEnd().Split(new[] { '\n', '\r' }, StringSplitOptions.RemoveEmptyEntries); currentWord = allWords[r.Next(0, allWords.Length - 1)]; // currentWord is public variable } }

If the program determines that the letter is found in that chosen word, then the program is set up to loop through the labels of the letters. If the label is able to correspond back to the letter, then this is going to be the letter that shows up, in the right spot, on the blanks at the top of the page for the word. If there are any labels that are blank there, then the user has not been able to guess all of the letters yet, and the game will continue on.

However, if the user has been able to go through and guess all of the letters, then the program is going to display the message of “you won” and will disable all of the buttons that are on the keyboard for this part.

Now, it is also possible that the user is going to go through this and will guess a letter that is not actually found in the word. When this happens, the program is going to hide the skeleton image that is being displayed, will do the increments that are needed on the CurrentPictureIndex to show the next image of the skeleton, and then will help to display that image as well.

Through this, if the current image ends up being the last one, then this is a sign that the user has lost the game, and the program is going to display the message of “you lost” on the screen. With the code that we worked with above, this is going to disable all of the buttons of the keyboard, and it is going to make each of the labels display their letters so that we are able to look them over and see what the word was.

Of course, we can also go through and add in some more ports to this as well. if we would like, it is pretty easy to go through and invent a kind of scoring system for this game, and even go through and save some of the statistics that you need including the high scores how often you win and lose, and more in the settings for that program. The code above is definitely complicated enough, using a lot of the different components that come with the C# language, so it is fine if you want to just stick with this much and enjoy the game that you created.

Before we are done with this part, though, we have one more note to finish off with. We need to note that the dictionary we are basing this program on is going to provide us with the words that we need to make the game work, and it is going to also result in the use of words that are common in more than one dictionary. In this format, the words are sometimes going to end up being uncommon words, and that can make the game a bit more difficult to work with.

You have the option to go through and try to make this a little bit easier of a game to work with and choose the dictionary that you would like to work within the process. It could even be helpful to go through and work with a dictionary that is specific to a topic or an industry to make this work for your needs.

And that is all there is to this program. When you are able to combine together a lot of the topics that we have been able to work within this guidebook in order to create our very own game. And there are so many other parts that we are able to handle and create when we work with this kind of idea, and we bring out all of the topics that we worked on so far. The hangman game is a fun way to get some practice with those topics and to ensure that you are able to get it to work for your needs.

# 
Conclusion

Thank you for making it through to the end of C#, let’s hope it was informative and able to provide you with all of the tools you need to achieve your goals whatever they may be.

The next step is to start working with some of the different parts that are in this guidebook in order to help us to learn a bit more about the C# language and to learn how to make this one that you can use in order to handle any of the programs that you want to write in the process.

There are a lot of different options that we are able to work with when it is time to start coding, and the C# language is going to be a great one to work with in order to get the applications that you would like. It works with the Windows system and is attached automatically with this system, but we can also make it work with some of the other options that we have as well. This means that we are able to work with some of the other options like the Linux and the Mac operating systems, as well.

This guidebook has taken some time to look more at the different things that we are able to with the C# language as well. There are so many different aspects that we are able to handle when we work with this kind of language. We will take a look at how we can work with conditional statements, the loops, polymorphism, enumeration, and more. All of these can come together to help us create some of the different things that we want when it comes to creating our own codes as well.

When it comes to picking out a coding language to work with, there are always a lot of different options that we want to work with. Each of these is going to come with a lot of different options that we can enjoy, and it seems like each one is going to provide us with a lot of benefits. Some are great for helping us to work with some working on the web pages and web sites that we want to create, some are really good at helping us to handle some of the different games that we want to create, and some are good for helping us with some general-purpose coding that we would like to work with as well. it all depends on what you are hoping to get out of the process and what you hope to accomplish as well.

There are so many benefits to working with the C# language, and we spent a lot of time taking a look through this guidebook and learning how we can make this language do what we would like. When we are done, we can make some of our own codes and create the programs that we want that actually work this time around. When you are ready to start working with the C# for your needs, make sure to check out this guidebook to help you out.

Finally, if you found this book useful in any way, a review on Amazon is always appreciated! 

C#

New step by Step Guide to Learn C # in One Week.

Including Projects And Exercise To Mastering C#.

Intermediate user

Andrew Sutherland

 Copyright 2019 by Andrew Sutherland - All rights reserved.

This eBook is provided with the sole purpose of providing relevant information on a specific topic for which every reasonable effort has been made to ensure that it is both accurate and reasonable. Nevertheless, by purchasing this eBook you consent to the fact that the author, as well as the publisher, are in no way experts on the topics contained herein, re.g.ardless of any claims as such that may be made within. As such, any suggestions or recommendations that are made within are done so purely for entertainment value. It is recommended that you always consult a professional prior to undertaking any of the advice or techniques discussed within.

This is a le.g.ally binding declaration that is considered both valid and fair by both the Committee of Publishers Association and the American Bar Association and should be considered as le.g.ally binding within the United States.

The reproduction, transmission, and duplication of any of the content found herein, including any specific or extended information will be done as an ille.g.al act re.g.ardless of the end form the information ultimately takes. This includes copied versions of the work both physical, digital and audio unless express consent of the Publisher is provided beforehand. Any additional rights reserved.

Furthermore, the information that can be found within the pages described forthwith shall be considered both accurate and truthful when it comes to the recounting of facts. As such, any use, correct or incorrect, of the provided information will render the Publisher free of responsibility as to the actions taken outside of their direct purview. Re.g.ardless, there are zero scenarios where the original author or the Publisher can be deemed liable in any fashion for any damages or hardships that may result from any of the information discussed herein.

Additionally, the information in the following pages is intended only for informational purposes and should thus be thought of as universal. As befitting its nature, it is presented without assurance re.g.arding its prolonged validity or interim quality. Trademarks that are mentioned are done without written consent and can in no way be considered an endorsement from the trademark holder.

# Introduction

Congratulations on purchasing C# and thank you for doing so.

There are plenty of books on this subject on the market, thanks again for choosing this one! Every effort was made to ensure it is full of as much useful information as possible, please enjoy!

Writing a program without knowing the environment in which it is to be run is like driving in a city without a city map. You only reach your destination by detours and by stopping to ask for directions.

## Why C#             

C# is basically not a new programming language, at least as far as the syntax is concerned. C# is more or less the syntax of the C ++ language family. The concept of C# has been developed from the ground up and fits 100% into the new.NET technology.

C ++ is a very complex language and therefore difficult to learn. C# is an easy-to-understand language. Since the language was newly developed, unlike C ++, it contains no annoying relics from previous versions.

There are over 20 programming languages  for.NET technology. But why does C# take on a special role in the new technology?

C# is the primary language of.NET technology and was developed specifically for use with.NET. Many parts of the.NET framework are written in C#.

In addition, C# fully supports component-based programming. Components are building blocks that - once developed - can be used over and over again, even without knowledge of the internal working method, the components must be present. Components can be used independently of project and programming languages, which not least saves development time.

C# combines the high performance of C ++ with the simplicity of Visual Basic.

## .NET Framework             

In order to be able to program effectively with C#, one needs a little theoretical background knowledge, which concerns the so-called.NET Framework. That's why the.NET Framework is an integral part of this book. Before we get more involved with the.NET Framework, you should know that it is an integral part of.NET technology.

## What Is Meant By The.NET Framework?

Primarily, it includes a conceptual platform that makes it possible to write programs and services. On this basis, different frameworks for different platform technologies have been provided so far.

C# and all the other programming languages  that were and are developed for.NET, need the.NET Framework as a run-time environment. More specifically, the runtime environment of the.NET Framework consists of the Common Language Runtime, called CLR for short. As the name Common Language Runtime suggests, it is a cross-programming language runtime environment.

The task of a runtime environment is essentially to execute the code developed with the respective programming language. In the past, however, a separate runtime library (runtime library) usually had to be provided for each programming language - and in part also for each version - in order to be able to execute the corresponding programs. For example, C ++ the file MSVCRT.DLL and in Visual Basic 6 the file MSVBVM60.DLL. The concepts of the supplied runtime environments were and are still fundamentally different today. Cross-language support provides key benefits of the.NET Framework:

*   Only one framework is needed.

*   Different (and very different) programming languages  can be used, depending on the level of knowledge and personal preference.

*   There is exactly one runtime environment for all programming languages.

From these advantages, further derivations can be made:

*   The cross-lingual integration

*   The cross-language exception handling (Exception Handlingrefers to how a program should react when events occur that are not normally expected, such as errors.)

*   Improved security (security can be controlled up to the method level)

*   A simplified versioning (several versions can exist side by side)

Because the.NET Framework provides a cross-language runtime environment, it ensures interaction and optimal collaboration between components of different programming languages.

You now know that the.NET Framework is part of.NET technology and what it has to do. The.NET Framework again consists of three main components:

Common Language Runtime - the cross-language runtime environment

Class libraries (Learn more about classes and class libraries later)

ASP.NET - server-side applications for the World Wide Web

In this book we will deal in detail with these three components. The common language runtime and class libraries will come up again and again throughout the book, as will ASP.NET in the context of web services. The two components - Common Language Runtime and Class Libraries - of the.NET Framework are also referred to as Base Frame-work.

# 
Chapter 1 - Create Types

## Common Language Runtime - CLR

Common Language Runtime, CLR for short has the task of managing the execution of the code and additionally offers services that simplify development on and with the.NET Framework.

With the common language runtime, the developer takes a lot of work. One of the big advantages is the simplified memory management, ie the management of the main memory. As a programmer, they can concentrate more on the actual task and are less confronted with internals in terms of the organization of the main memory. In addition, the same data types exist in each programming language, which is very useful when using different programming languages, because you no longer have to think constantly about the peculiarities of the respective programming language. (A data type determines what type of data is stored, and where applicable - numeric data - its range of values  and precision.)

Most or all of the memory management and many other tasks take over the common language runtime. 

When managed code refers to code that is under the control of the runtime. He is not allowed to do certain things himself, for example, directly accessing the working memory; that is why the CLR, as an intermediary and overarching body, takes care of it. Only if you use managed code, you can benefit from certain advantages, such as: As the automatic memory management or cross-language integration.

The common language runtime has its own memory management, the so-called garbage collector (literally "garbage collection for inoperative data in memory"), GC for short.

Without the use of a garbage collector you have to take care of the memory management and release yourself, which is very time-consuming and error-prone and can even lead to system crashes. The Garbage Collector manages the memory automatically, that is, it controls all memory requirements of the system that is running your program, and removes all data from the memory that is no longer referenced, so that references no longer exist, or even easier expressed - which are no longer used.

## Intermediate Language

Imagine, the whole world speaks a language and every inhabitant on this planet would understand it. The whole thing sounds very philosophical and is difficult to imagine in human communication. Translated to the.NET Framework, however, something like this has been created: an overarching, mediating language called Intermediate Language.

One of the concepts of.NET technology is to be independent of the operating system. Another advantage is the large number of available programming languages, which can be chosen according to the level of knowledge and personal preference, without any restrictions being imposed, for As for the use of written in a particular programming language component from another language.

But how are code parts that z. That were developed in C#, with code parts written in Visual Basic.NET or another programming language? At least here you have to say goodbye to conventional programming with their different runtime environments and rethink.

We know from the preceding sections that the.NET Framework has only one runtime environment and that all programming languages  can be used and understood by the.NET Framework. The problem that arises here is the intermediate step between the program (in any

.NET programming language written) and the finished execution file. This intermediate step is solved in.NET with an intermediate code. This intermediate code is called Intermediate Language Code, or IL code for short.

This IL code is understood by the.NET Framework and can be translated into an executable file. Since the.NET Framework is between program and operating system, the operating system usually plays no role in the programming, since the.NET Framework acts as an intermediary between the operating system and the program.

For developers programming on the.NET platform, this means that initially no machine code is generated (for a particular processor), but IL code. IL code can be thought of as a code for a virtual processor, a processor that does not physically exist that is "thought", that exists only in the form of software. Such a processor-independent code is not something completely new; it is usually referred to as P-code or bytecode in other technologies. Unlike the IL code, P-code is usually only one generated programming language; You are thus platform-independent, but forced to use a particular programming language.

The concept of the IL code makes it clear why a program can be implemented in a wide range of programming languages. Regardless of which programming language is used, the readable source code (that is, C# statements, for example) is converted into the general, general IL code. The program that performs this transformation is called a compiler, the process of conversion is called compilation.

In addition to the IL code, the compilers also generate additional information files, the so-called metadata. These metadata include z. For example, information about types, members, and references from your program. The common language runtime requires metadata to B. to load the classes. Metadata, as shown in the figure below, is stored together with the IL code. The IL code is the product of various compilers and is required as the execution code for the JIT compiler.

JIT Compiler

The.NET Framework is also based on the general IL code. To generate z. For example, if the C# compiler uses IL code, this code can not be understood by the computer's physical processor. Each processor type has its own machine language. Ultimately, the computer can only use the machine the language of the physical processor. This code is called Native Code (or in German as "native code"), which roughly means "innate, original".

It follows that at some point in time the IL code still has to be translated into native code. Usually, a kind of interpreter is used for comparable purposes (P-code interpreter), but at the expense of the execution speed, since the same instructions are always recompiled, even if nothing has changed in the program. Alternatively, one could also convert the code with a compiler that generates native code. This would provide a higher speed, but the programmer would have to do the conversion manually after making any changes, and there would be other drawbacks that would compromise.NET's platform independence.

To combine the advantages of compiler and interpreter, therefore, a mixture of both approaches in the form of a so-called just-in-time compiler or jitter is used. The JIT compiler automatically converts the IL code into machine code. This happens only when needed, specifically when a program is called. This transformation goes so far that program modules that are not used are not translated by the JIT compiler. Only when the program modules are called by the user or other function calls in the program, the translation takes place. The advantage is that only very slightly speed is lost; Once the program module is over-compiled, it runs at the full execution speed of the native code.

At the same time,.NET remains platform-independent without limitation, so the IL code is not dependent on a specific environment.

## The Execution

Use the C# compiler, csc.exe, to compile the existing code into the IL code. We will look more closely at the C# compiler later.

Suppose that you have developed a program that can perform various, very complex types of calculations and have realized these as separate modules and summarized them in a calculation class.

Now, when you perform a specific calculation, the JIT compiler looks for the entry point in the IL code and translates the affected computation module into native code. The remaining calculation modules are still available as IL code. If the same module is executed a second time, the JIT compiler does not have to translate the code again, it just re-executes the already translated and existing machine code. Only when further, not yet translated, modules are called, does the JIT-Com-Piler transform these modules into machine code. In this way, the execution is considerably accelerated. This acceleration is particularly noticeable in larger programs, as the call only translates the modules that are actually needed. The JIT compiler is even able to respond to changes in the hardware of the computer and to optimize the machine code for this purpose.

## A Class Of Its Own             

Before we start with actual programming, we should deal with the basics of object-oriented programming and here especially with the classes. C# is an object-oriented programming language. What constitutes a class in a programmatic sense will be described in more detail later. But for now an abstract case study to convey the basic idea of  class and class design.

Generally speaking, a class is an abstract illustration of real problems of (programming) everyday life that provides a solution in itself and / or communicates it to its environment or fulfills tasks. For this purpose, classes have methods and properties that have to be combined with each other in order to solve the problems posed. (A method performs a concrete action - a property is more of a feature, so it returns information about what it's made of.) The meaning of methods and properties will be described in detail later.)

It is also interesting to know that you can not use a class directly in a program. Now, if you are a little confused and wondering why you encapsulate problems in classes in C#, and what makes all object-oriented programming meaningful, I can fix it. I did not feel the same way when I heard about classes and object-oriented programming for the first time.

Imagine a professor who distributes his scripts in the first lecture. Hundreds of students are waiting eagerly and eager to receive their personal script. It is clear that the professor did not write this script hundreds of times, but made copies of it. The original has only the professor, who teaches the material according to the script in his lectures and points out to the students what is important and what is not. The students work with their personal script and mark, for example, with a highlighter key text passages and write notes in their script.

This small lecture example is similar to a class. The working memory of a computer can be thought of quite remotely as the lecture hall of the professor in which the students are sitting. The moment the professor distributes his first copy of the original to a student to work with the copy, a script exists that is different from the original. This script of the student is called in the object-oriented programming instance.

You will now wonder where these differences are. In order to be able to hand over a copy of the script to the new student next year, you leave the original as it is - in contrast to the copy with which the students work and possibly mark passages and add notes.

A class is similar to the original of the script. So if you want to work with the contents of the script, you get a copy of the original; the student's seat in the lecture hall is similar to the space allocated to the copy of the class in memory.

In programming, this process is called instancing or instantiation of classes. From this process of instantiation, ie the creation of a copy of the professor's script, an object results. One can imagine an object as a "working copy", in reality an object is a concrete representation of the abstract description of the class.

Now, the idea that you are not working with classes but with objects of that class by forming an instance of the class should not be too difficult for you.

## The Boolean Type

The boolean (also known as boolean data type) data type can take one of 2 values, true or false. The data type has a lot to do with a bit that can take only two values: 0 and 1\. One might think that therefore for a variable of the type boolean only 1 bit in the working memory is occupied. Due to the special management of the main memory, however, a complete byte is actually reserved, ie as much memory as in the data type byte.

The boolean data type can be found in a program mostly for decisions in conditions. The boolean type works on the positive logic: the logical 1 means true - true and the logical 0 false.

## Is This The Right Type?

In general, it is up to the programmer what type of data he decides. When choosing the right data type, however, you should think about the future, ie, the program should still work properly even if, for For example, the amount of data that is stored increases over time. Here it would be awkward to use data types that are no longer sufficient at some point. (You are well aware of the Y2K issue, which is largely due to the fact that too little memory was reserved for the year in the programs concerned, so the subsequent adjustments were costly.)

Nowadays, we usually have enough RAM and fast hardware, so you should choose the data type with a correspondingly larger value range in case of doubt. However, under no circumstances should generous data types be used. If z. For example, if it is absolutely certain that a loop will only be traversed 10 times, it would be an exaggeration to use an int data type for the affected variable. It is worth considering whether instead of a short type or even a byte type is sufficient. Another aspect is the performance (performance and speed) of a program. Since performance is not only dependent on the processor the program is running on, but also on the amount of memory used and available in a computer, you also have to worry about which types of data you are using. The long data type is slower than the int data type, because a larger amount of information is processed at the first time. It also implies that the long data type requires more memory than the int data type.

## Implicit Conversions             

Implicit conversions can be found in many situations. Mostly they are used unconsciously by the programmer, without them thinking much about it. This can sometimes lead to less beautiful side effects. 

The implicit conversion happens automatically and can, for example, lead to a reduction in the precision of the floating point types up to the absolute representation without decimal places.

## Type Conversion             

In strict contrast to implicit conversion, explicit conversion requires specifying the data type into which the variable is to be converted. The conversion types in the C# programming language depend directly on the value ranges of the various data types. If you attempt to store the contents of a variable whose data type has a larger value range than the target variable, the compiler will issue an error message.

int iNumber = 0;

short sNumber = 0;

sNumber = iNumber;

The error message generated thereby is:

Implicit conversion of type 'int' to 'short' not possible.

Here, a type conversion of the variable iNumber must be made. The variable iZahl must go through an explicit conversion instruction method is known as cast are converted to the correct data type. The data type to be generated is written in parentheses before the variable.

The statement for the explicit conversion or for the type conversion runs z. As follows:

sNumber = (short) iNumber;

## Error During Explicit Conversion

We know that all data types use a certain amount of memory. It thus becomes clear that the type conversion of data types of larger value ranges into smaller value ranges can lead to errors.

The int data type occupies 4 bytes in memory, while the short data type occupies 2 bytes. What happens if you want to convert a value of a variable of type int into a variable of type short and drop it? The following listing demonstrates the problem involved.

## Avoiding Conversion Errors

Because conversion problems and overflows are commonplace in programming, C# gives you the ability to monitor such issues. As we have seen above, the compiler does not issue an error message if an out-of-range condition is triggered by the explicit conversion. We have to tell the compiler that a certain area needs to be overseen in our program.

Conversion errors usually only become noticeable at runtime and are not always obvious to inexperienced programmers. If you want to be on the safe side, you can put all statements that contain conversions in a checked block. Over time you will get a certain routine for conversions and use the checked block only where it is needed. The next listing shows you how to use a checked block.

# 
Chapter 2 - Linq 

It's a tradition that the first program you write when you start learning a programming language does nothing other than print the welcome text "Hello world!" To the console. It was no different for me. Much has happened in the meantime; so I allow myself that in the age of Internet and.NET this greeting a little bit change.

Just type in the code that will be printed afterwards, for example by using one of the Windows editors WordPad or Notepad (the latter is called Windows only as an editor). To do this, click the S TART button and then click A LLE P ROGRAMME. Under the Z UBEHÖR folder you should find the two editors.

If you can not find any of the editors there (which should not happen), under S TART / A LLE P ROGRAMME / Z OBEHÖR click on the entry USER and open the dialog box of the same name. Enter the command notepad in it and confirm your input with OK.

At the beginning, I do not want to confront you with the Visual C# development environment, as it makes it difficult to get to grips with the essentials. We'll talk more about the Visual C# development environment later.

For the exercises that we will be creating in this book, create a folder, best known as the top-level examples of drive C :. For each day in the book, a separate sub-folder with the number of the respective chapter is recommended. Use z. For example, use Windows Explorer to create the folders. The folder structure now looks something like this:

C: \ Examples \ Chapter01

C: \ Examples \ Chapter02

## Create You The Library Project

The next step would be testing the class now. However, this requires an application that uses the class from the library because libraries themselves can not be executed directly. However, this is not tragic, because we originally planned to use the library class in an application as a base class.

## Derivation In An Application

To switch to the classes of a dynamic library (DLL) in a program

To be able to access you must:

In the source code of the program, include the namespace of the library class (alternatively, you can access the class and its elements using fully qualified identifiers starting with the name space,

Set up a reference to the library.

When you work with the Visual C# Compiler, the development environment helps you set up and manage the references. If you follow the example with the csc compiler, just create a file called Program.cs, transfer the source code below, and compile the file with the option\ r: CKummerkasten.dll, which creates a reference to the library :

 csc / r: CKummerkasten.dll Program.cs

If the DLL is not in the same directory as the EXE file to be created, you must specify the path to the DLL.

If the location of the library is not displayed as the location of the library, you probably have previously closed the bibliography library.

Before deriving from the library class, you should check that the class is working properly.

In the Main () method, instantiate the library class CKummerBox.             

Before you can build and run the project, you still need to connect to the library that contains the class CKummerkasten code.

# 
Chapter 3 - Methods

Basically, you do not need more than a suitable C# compiler to build C# programs (for example, Microsoft's csc.exe, which you already met yesterday), and an operating system with it installed.NET Framework. However, as programs become larger and more complex over time, when they need to contain multiple source files with different compiler settings, or to be outfitted with graphical user interfaces, programming with the pure C# compiler becomes more and more tedious. In this case, it pays to use a powerful development environment that actively supports the developer in programming. One such development environment is Microsoft Visual Studio 2008, which supports several programming languages  at the same time, specifying which language is preferred during installation (eg Visual Basic, Visual C ++ or Visual C#). For individual programming languages, there are also free versions, the so-called Express Editions, which can be downloaded from the Internet. These free versions have a slightly reduced functionality compared to the full version of Visual Studio. 

However, most of the code examples were chosen to be easy to set up with a simple code editor, with the individual compiler commands, including any options, often being included. Of course, these examples can all be easily created with the support of the Visual C# Express Edition. Where there are serious differences, it is explicitly pointed to the respective versions. Otherwise, there is general talk of Visual C#. The full version was mainly used for more advanced topics that are not supported by the Express version (like this one).

Today is dedicated to readers who want to work with Visual C# right from the start. The most important components of the development environment are presented. You will learn how to re-program the programs from this book with Visual C#. You'll also learn about the many smaller and larger features that make programming with Visual C# so enjoyable and comfortable.

Readers who prefer to write their code by hand and work with the pure csc compiler can simply skip the chapter and come back to it later if they want to migrate to Visual C# (or a comparable development environment).

## Constants             

In principle, a constant behaves exactly like a variable. The only difference is that you can not change a constant after its initialization. There are two types of constants in programming: literal constants (also called real, natural constants) and symbolic constants.

## Literals Constants

This type of constant is represented by its value. Literary constants are inherently constant and thus easily recognizable as such, since the value can be found directly in the source text in typed form. Examples of literal constants are:

int i = 1 ;

double d = 3.14 ;

char c = 'a' ;

string s = "Hello.NET" ;

In the example above, you see that in addition to variables, literal and symbolic constants also belong to a specific type. 1 is a value of type int and 3.14 of type double. But they are not just numeric values  as constants but also a character or a string, which you then call string constants. So the single letter 'a' is of the type char and "Hello.NET" is of the type string.

So if a constant is managed just like a variable, how can you assign a data type to a literal constant? We already know the declaration of a variable:

long iNumber = 50;

This declaration shows which data type the variable iNumber contains, namely long. 50 lies in the value range of the data type long. For us, this means that the variable iNumber stores the value 50. The value 50 represents the type int by default, but this is not problematic due to the automatic implicit conversion, as you will see shortly.

Literal constants are assigned to standard types without the use of a specification suffix. By default, the numbers in the range of -2,147,483,648 to 2,147,483,647 are declared int, so the value 50 from the example above. Floating point values  are declared as double. 

## Escape Sequences             

Finally, a little digression to the so-called escape sequences, which are very practical in practice. Escape sequences are treated in detail in connection with the formatting of strings. Escape sequences are special characters that you use within string constants. You can use it to realize line breaks or format textual output in general. In addition, the escape sequences help with display or formatting problems in the source code. For example, suppose you want to double-quote a string constant. In the source code, this means that the string is hereby terminated, resulting in an error message:

string sName = "Hello, my name is" Strasser ""

To avoid error messages, you must use a special escape sequence. The compiler recognizes this special character and then inserts a double quotation mark:

string sName = "Hello, my name is \" Strasser \ ""

The syntax of an escape sequence looks like this: a backslash (\) followed by a

Letters describing the formatting. The below table lists some important escape early sequences on:

 ![](images/00001.jpeg)

| Escape sequence | description |
|  |  |
| n \ | New line |
| \ t | Tab |
| \ b | Backspace |
| \ " | Double Quotes (") |
| \ ' | Single quote (') |
| \\ | Backslash (\) |

The following listing shows how to use the escape sequence that wraps to a new line.

using system;

namespace Kap3

{

class CDemo

{

static void Main (string [] args)

{

Console.WriteLine ("First Row \ n Second Row");

Console.ReadLine ();

}

}

}

## Instructions             

A program is controlled by various instructions. However, statements also evaluate expressions that the program can continue to process. There are a large number of operators for this purpose - eg. B. +, - and * - available.

One statement that you see very often in a program is the assignment of the contents of two different variables into a variable, which are linked by an operator for this purpose:

a = boc;

The character o here represents the operator, which links the two variables b and c together. Insert the appropriate operator. Examples of operators are the addition sign (+) and the subtraction sign (-). The result of the combination of b and c is stored in the variable a.

## Whitespaces

In addition to statements, expressions, operators and comments, there are additional characters in the source code. These characters are called whitespaces. They are used primarily for the clean, clear design of the source text. Surely you have already made extensive use of it, without being aware of it.

Whenever you indent lines by pressing the Tab key or by breaking lines with the Enter key, whitespaces are inserted. Usually, these characters are not visible on the screen, and most editors can also be configured to display whitespaces (usually with weak dots or arrows).

The whitespaces include the space and all characters that also create spaces, especially the tab and the line break.

Since the whitespaces are used primarily for formatting the source text, they are initially ignored by the compiler. Here are some examples of how to format statements using whitespaces.

a = b + c;

a = b + c;

a = b + c;             

a = b + c;

All instructions do the same. In the first line, all characters were written next to each other, which does not produce a very readable code. In the two subsequent lines, the variables and operators were visually separated by whitespaces, resulting in a much clearer code. In the fourth example, the use of whitespaces has been exaggerated (extra line break), which undermines the readability of the statement.

You should make extensive use of whitespaces to indent and otherwise visually separate statements, blocks, and other elements in your code so that the code remains clear and legible.

However, whitespaces are not always ignored by the compiler. If you use spaces and tabs within a string (data type string) or Characters (char), these characters become part of the data stored in the string or character. For example, the string "Hello.NET" stores a space between the two words "Hello" and ".NET".

The following two statements have the same result, although in the second statement a newline was inserted in the method name Console.WriteLine (this method outputs text to the console). The line breaks only change the formatting of the source text. Only in the string "Hello.NET" is the space output:

Console.WriteLine

("Hello.NET");

Console.

WriteLine

("Hello.NET");

Incidentally, you can only use the space and the tab within a string or character:

Console.WriteLine ("Hello →.NET");             

In the example, the two words are separated by the tabulator - here represented symbolically by an arrow (→) -, whereby in comparison to the normal space a much larger horizontal distance is achieved.

However, linefeeds may not be used within a string or character:

Console.WriteLine ("Hello.NET ");

Here, within a string, the following line was broken, resulting in the following error message.

Is expected line feed in constant

As you can see, not all types of whitespaces are ignored. Over time, however, you will develop a sense of how and where you can and may use Whitespaces.

## Empty Instructions

Over time, when you see other C# programs, you'll see a lone semicolon in a line here and there. Such instructions are called blank instructions. You can see such empty statements, for example, in for loops. Such instructions do not do anything. At this point, it should suffice to mention that they exist and that they are permissible in the programming language C#. A small example of a permissible empty instruction can be seen here:

for (a = 0; a <10; Console.WriteLine (a ++));

## Composite Statement And Blocks

We have already described the need for blocks to increase the clarity in a program. Such blocks are also called compound statements and combine a set of statements in a curly bracket. A block always starts with an opening curly bracket { and ends with a closing curly bracket }. The following example shows you such a block.

{

WriteLine ("{");

WriteLine ("Hello");

Console.WriteLine (". NET");

WriteLine ("}");

}

You can see blocks in programming in different ways:

{Instruction; instruction;

}

{

instruction;

instruction;

}

All these types of blocks are permitted and used in practice. The differences lie exclusively in the formatting of the source text, that is, as far as indents and line breaks are concerned.

I do not want to put a stop to your creativity, but get used to one of the block diagrams above and do not invent your own. These illustrated block statements will be found in most programs.

If at some point you expand or modify a third-party program, continue to use formatting as introduced by the developer of the program. There is hardly anything worse in a source code than inconsistent formatting.

## Expressions

An expression can be part of an instruction. Ultimately, expressions are also to be seen as instructions. In C#, anything that returns a value and consists of one or more elements (such as numeric values  or variables) is an expression. In short, anything that returns a value is an expression, and there are virtually unlimited possibilities in C#.

Thus, symbolic or literal constants and variables return expressions.

The following statement has four expressions.

a = b + c;

Of course, the three variables are also expressions, each of which contains a value of its own - before the instruction is executed - e.g. B. can evaluate with the debugger. But where does one find the fourth expression? The statement itself is an expression, since it gives the value of the addition of b and c. Do not let it irritate you; the next example will give you clarity.

If a = b + c is an instruction and at the same time an expression, since a = b + c returns a value, then the following statement should also be valid.

z = a = b + c;

True, this statement is also valid, since a = b + c is also an expression.

If b contains the integer value 5 and c the integer value 4, then it is clear that a represents the integer value 9, provided that all variables with the data type int have been declared. The expression a = b + c also contains the integer value 9\. Thus, the variable z also represents the value 9.

A included in this example, the addition of the variables b and c. The value of a is always the sum of the two variables b and c, and thus also the value represented by the variable z.

Regarding the order in which expressions are evaluated, the rank order "point before line" plays a major role; which should be well known to you from school. One speaks of the ranking of the operators. So not all expressions are evaluated equally, but first the multiplication (operator *) and divisions (/) are evaluated and then the additions (+) and subtractions (-) are evaluated.

z = a * b + c;

The expression a * b returns a value here, which is then added to the value of the variable c, which makes the entire statement an expression again.

## Operators

Operators make it possible to link an expression, an instruction or several expressions and instructions with each other. In the previous sections, you have already encountered various operators. The expressions or statements that are linked by an operator are called operands. The following example shows you a simple link based on an addition.

a = b + c;

The plus sign (the symbol for the addition) is here the operator; the two variables b and c (elements of the link) represent the operands. In C# there are a large number of such operators:

Assignment operator

Mathematical Operators

Remainder operator

Decrement and increment operators

Composite operators

Comparison operators

Logical operators

Conditional operator

Comma operator

## Assignment Operator

We have often used the assignment operator. The symbol for the assignment operator is the equal sign =. But do not confuse the assignment operator in C# with the equal sign ==, which can be found in formula collections and equates or compares two variables. For the comparison of values  there is another operator in C#, which we will get to know later.

If you want to write one value of a variable into another variable in C#, you assign the variable to another. This looks like this:

a = b;

But b does not mean that the two variables are identical in value, but that the value of variable b is written in variable a. Only after carrying out this assignment do the two variables have the same value.

## Mathematical Operators

We all know the basic accounting types and their operators. Which includes:

Addition

Subtraction

Multiplication

Division

The general notation of mathematical links looks as follows.

a = boc;

Let's write a small application with the operators + and -. The program polls two numeric values  from the user via the console. After entering these, a calculation is carried out and the result is output.

## Remainder Operator

The remainder operator returns the remainder of a division with integers. For example, 5 modulus 4 is 1 because dividing 5 by 4 leaves the value 1. The remainder operator is represented in C# by the character %.

There are a number of applications in which the remainder operator can be used. For example, suppose that you want to output a dataset line by line and create an interline after every 10th line to achieve better optical separation. In this case you can perform a calculation of line number modulus 10. If the line number is divided by 10, this division will arrive at every 10th line without remainder - you will get 0 and can get 0. Whenever 0 is returned, make an interline. 

The remainder operator works only with integers and therefore does not accept floating-point numbers. This can be z. B. in the division of integers to take advantage by further processed in addition to the actual result of the division and the remainder of the division. The following program reads two integers and divides the first number by the second number. The remainder of the division is calculated using the remainder operator %.

## Increment and Decrement Operators

In loops or conditional iterations, a variable is usually used as a counter variable, a so-called counter. Its task is to increase or decrease its value by 1 each time. This process of increasing is called incrementing and decrementing the opposite, namely decreasing the value by one. C# contains special operators for such operations.

There are various ways to increase the value of a variable by one or decrease it by one.

a = a + 1;

b = b - 1;

a ++;

b--;

++ a;

--b;

The first way to change the value of a variable by one, we already know. If a = a + 1, the current value of variable a is incremented by one and written back to variable a. The same procedure is used at b = b - 1, except that here the value is reduced by one.

The other four examples a ++, b--, ++ a, --a principally execute, increment and decrement the same actions. This type of representation or the type of these operators is called unary operators 4. Unary operators only affect one operand.

But what is the difference between a ++ and ++ a or b-- and - b ? If they appear as a single statement in a row, no difference is noticeable at first. Only in combination with an extended instruction results in a difference, in addition more. 

## Ranking And Parentheses

If you want to perform calculations in C#, you should know about the ranking of the operators. As a rule, one can fall back on the knowledge of mathematics lessons in school.

a = 5 + 4 * 2;

What about the ranking of the operators in C#? First the term 5

       4 and then multiplied by a factor of 2 ?

a = 9 * 2;

Or is the rule that we know from school days - point by line - used?

a = 5 + 8;

As already indicated in the previous sections, in the basic arithmetic operations in C# the rule is point by line, the result is therefore 4 * 2 + 5 = 8 + 5 = 13. Thus, the operator * has a higher priority than the + operator. There are other operators in C#, so you can not get ahead with the rule "dot before line" alone. Here, a well-defined ranking of the operators is used, according to which calculations are performed. 

The multiplicative operators come second. Do not let the word confuse you multiplicatively. Every division can also be expressed as multiplication. So is

z = a / b;

equivalent to

z = a * 1 / b;

The additive operators come in the ranking at the end. The same principle applies again to the order of priority as above. You can express the pressure

z = a - b;

also as

z = a + -b;

write. Consider again the example from above.

z = a * 1 / b;

This expression contains several operators with the same priority. Here is a simple rule. If, as in this example, there are several multiplicative operators in an expression, the result is evaluated from left to right. This means that first the result of the multiplication a * 1 is calculated and then the result is divided by the value of the variable b.

The analysis of the following listing illustrates the effects of the ranking of operators.

using system;

            namespace Kap3

            {

            class CDemo

            {

            static void Main (string [] args)

            {

            int a = 10;

            int b = 5;

            int c = 2;

            int z = 0;

            z = a * 1 / b;

            z = a + -b;

            z = b / c * a;

            z = a * b% 20;

            z = a ++ * b - a;

            z = ++ a * b - a;

            Console.ReadLine ();

            }

            }

            }

Let's start with line 14\. These are just multiplicative operators that have the same priority. First the result of a * 1 is calculated and then divided by the value of the variable b. The content of the variable z is thus the value 2.

In line 15 we see an additive and a unary operator. The unary operators are prioritized over the additive operators and thus calculated first. The unary sign operator reverses the sign of the contents of variable b. If there is a negative number here, the value becomes positive and vice versa. Then the value of the variable b is added to the variable a. Thus, the content of variable z is 10 + -5 = 10 - 5 = 5.

Lines 17 and 18 follow the rules described in line 14. First of line 17: The value of the variable z in this line is 20. Should it not yield 2.5? Please note, however, that an integer data type is used so that the decimal places are ignored; therefore, the result is not 2.5, but 2 (which results in 2 * 10 = 20 for z). To line 18: The result of the variable z is the value 5 * 10% 20 = 50% 20 = 10. Here you can see very well that operators of equal priority are linked from left to right.

Lines 20 and 21 are a bit more delicate. Here exist unary, multi-plicative and additive operators. First to line 20:

z = a ++ * b - a;

Unary operators have the highest priority. a ++ increments the value in line 20, but only after the value has been read out. This is the postfix notation. The value of the variable a is in this case 10 (and not about 11) and is multiplied by the variable b (10 * 5 = 50). Only after this operation is a raised by one.

Now is the outcome of 50 the value of a withdrawn, a but now has the value 11 because a is incremented after read. This results in 50 - 11 = 39. Now to line 21:

z = ++ a * b - a;

Here, the variable a initially still has the value 11. Since the prefix notation is used now (++ a), the value is already incremented before reading out, so it has the value 12. This results in 12 * 5 - 12 = 60 – 12 = 48.

The calculation of expressions is controlled in C# by means of the ranking of operators. But what if you want to control your calculation yourself? Here is the possibility to put the preferred expression in parentheses. Parentheses override the order in which variables are linked, regardless of which operator is used. Let's try changing the priority in favor of addition in the following example.

z = a ++ * b - a;

If the content of variable a is 10 and b is 5, we already know from the previous listing that z is 39. If we now want to change the priority in favor of the addition, we have to put a brace around the expression b - a.

z = a ++ * (b - a);

What do you think about the result for the variable z ? Let's get back to our knowledge. C# usually evaluates expressions from left to right. The multiplicative linking of the variable b to the variable a ++ was canceled by the parenthesis and thus the entire expression b - a is linked multipliatively. In the variable a is the value 10, which is multiplied by the expression b - a. However, the expression b - a contains the variable a, which of course was previously incremented by one. So the expression follows:

z = 10 * (5 - 11);

Before the multiplication takes place, the parenthetical expression is evaluated.

z = 10 * -6;

The content of the variable z is thus the value -60.

## Comparison Operators

The comparison operators have the task of comparing expressions with each other and thus of answering queries. However, every query has a serious limitation, as a result it returns only yes or no. So it is not possible to ask a question such as "In which directory is the file named xyz.txt ?". But you can write a routine that can answer the following question - "Is the file named xyz.txt in this directory?".

Such expressions can be edited using comparison operators. C# works with the positive logic. Thus, a question that is answered with yes results in true (true); a question that has no result, but false.

Do not confuse the assignment operator = with the comparison operator == !

If a value is assigned to a variable, for example, to be able to perform calculations, then use the assignment operator. Here, the content of the variable is manipulated. The content of variable a has the value 5 here :

a = 5;

If, on the other hand, one compares a variable with a value or another variable in order to be able to make decisions, for example, then the comparison operator is used. In this case, the content of the variable is not manipulated.

a == 10;

The content of the variable has the value 5 and not the value 10.

Here, the entire expression returns false.

Programs that execute only one instruction after the other would hardly be needed in practice for the typical problems to be solved - they would lack a certain (artificial) intelligence. However, to be able to make decisions about a program requires special instructions, which are summarized in the so-called sequential control. 

A branch in the program flow has at least one condition and from this condition a resulting statement. The result or value of a condition can only contain two states: true or false.

The state within the sequence control results from the positive logic. If the value of the condition is true, then the statements that are in the branch block are executed. However, if the value of the condition is false or false, the statements in the branch block are ignored.

The easiest way to make a decision in a program is to use the if statement. The syntax of this branch looks like this:

if (condition)

instruction;

or

if (condition)

{

Instructions;

...;

...;

}

If there are several statements in a branch block, this is called a compound statement. If the condition is met, all instructions contained in the compounding guide will be executed.

The if statement does not terminate with a semicolon.

In general, if statements are used in conjunction with expressions that are compared with each other. The following listing shows the use of if statements.

Else clause

We now know the if statement, which helps us to make decisions in a program according to certain criteria. If a condition occurs, the instructions in the instruction block are processed.

The statements in an else clause are executed if the condition of the if statement is not met. The else clause is also referred to as an alternate branch. On the one hand, the else clause increases the readability of an if statement, on the other hand, one does not want to and can not consider all the condition cases in larger programs.

The syntax of an if - else statement looks like this:

if (condition)

statement1;

else

statement2;

or

if (condition)

{

Instructions;

...;

...;

}

else

{

Instructions;

...;

...;

}

The following listing shows how to use an if - else statement. The course of the program is such that with an order value of less than 100 euros, the port costs of 5 euros are added to the order value. From an order value of 100 euros the postage costs are taken over by the sender. In addition, a discount of 100th part of the order value is subtracted.

# 
Chapter 4 - C# Style Conventions And Nesting

In principle, it is up to every programmer how to format his source code. But if you write a source code that you still want to read and understand after a few months, or work in a development team, then you should stick to some rules. The write conventions shown in previous examples in conjunction with the if statement and if - else statement, and their nesting capabilities apply to all program blocks. This includes loops such as while, do while, for etc., as well as the construction of classes and namespaces.

The structuring of the source code is an important aspect of programming.

This type of block is space-saving and still very legible. Some programmers are annoyed by the dropped curly braces (as we have used until now, which can also be seen in the following source code); They therefore choose this spelling. But you should already have some practice for this.

using system;

namespace NsX

{

class Class1

{

static void Main (string [] args)

{

}

}

}

In this case, the blocks containing the further instructions are issued. The disadvantage of this structure is that the number of lines increases significantly. However, the affiliation of the instructions is very clearly recognizable in this type of representation.

using system;

namespace NsX

{

class Class1

{

static void Main (string [] args)

{

}

}

}

This notation deviates from the previous one only by the indentation of the blocks. The disadvantage of this is that the line length increases. If you have a large number of hierarchically separated blocks in the source code, you often have to scroll horizontally in order to capture the complete line, which affects readability.

Should you ever have the problem that important parts of the source code are too far to the right, so you have to scroll horizontally, you can also move a block out - right to the left edge. Often then a comment with the content <- is inserted in the block, which symbolizes that the following block that has been pushed out actually belongs here in the hierarchy, accordingly the end of the release is again marked by a comment <-. The following example shows such a case.

namespace NsX

{

class Class1

{

static void Main (string [] args)

{

if (condition)

{// <-

if (condition)

{

...

}

...

} // <-

}

}

}

Often an instruction block has only one instruction executed on one condition. In this particular case, you are free to choose whether the block is dropped off with curly braces.

if (condition)

{

statement1;

}

statement2;

is synonymous with:

if (condition)

statement1;

statement2;

In both cases, statement1 is executed when the condition is met. Statement2 is always executed because it does not belong to the conditional statement block.

Branches can also be nested arbitrarily.

if (condition 1)

statement1;

else

if (condition2)

statement2;

statement3;

In the example above, the else clause contains another branch that executes statement 2 if condition 2 is met. Instruction3 is always executed.

Conditions are also expressions that can be combined with single expressions. Logical operators serve to execute multiple comparisons in one condition at a time.

Imagine a login system in which you can only log in on weekdays. Here, three criteria must be met. »Is today's day a business day AND does the user exist in the system AND does the password match?« In order to evaluate such expressions, we have three logical operators at our disposal.

## Condition Operator

A simple if - else statement can also be implemented using the conditional operator. Use this only for simple expressions; otherwise the readability of the source code suffers. The condition operator ? : belongs to the group of ternary 5 operators. The question mark (?) Initiates the expression to be executed when the condition is met. The colon marks the beginning of the expression to be processed if the condition is not met. The if -else statement:

if (condition 1)

statement1;

else

statement2;

can therefore also be written as

Condition1? Expression1: expression2;

# 
Chapter 5 - Input / output and strings

In the previous chapters we have created a basis for working with the programming language C#. Next we'll look at the input and output as well as the strings.

Here you learn:

*   how to format numbers

*   how to create custom styles, how to format dates and times,

*   which classes and methods are used to manipulate strings, how to use escape sequences correctly.

## Strings And I / O             

In the C# language, all strings represent instances of the System.String class of the common language runtime. There are a variety of methods in this class that help us manipulate strings.

We already met strings. In our previous examples, it was all about string constants.

"I am a string constant"

String constants are always in double quotes. If a string constant has only alphanumeric characters, output to the console will not be a problem. The string constant will be output as it is in the source code.

Console.WriteLine ("I am a string constant");

The WriteLine () method of the Console class specifies the string

I am a string constant in the console. This output of the string constant to the console is also called "outgoing data stream".

Data streams are supported in C# bidirectionally, ie in both directions. The console can only output or receive the data type string. For the programmer, this means that he has to perform a conversion when entering (or receiving) data to his program. Would you like z. For example, to process the weight of a person in their program typed by a user in the console, the weight must first be converted to the appropriate data type. The class Convert is available for this purpose.

double dWeight = Convert.ToDouble (Console.ReadLine ());

Console.ReadLine passes the program a data stream of type string. Since the implicit conversion from the data type string to a data type double does not work, an error occurs without conversion. In principle, all data streams that are transferred from the console to the program must be converted, with the exception of the string data type itself. However, the Convert class does not protect you against incorrect entries. If you try to convert a letter to a double data type, you will receive an error message.

An unhandled exception of type System.FormatException occurred in mscorlib.dll.

This error message shows you how the data stream of the console works. For example, the letter x does not correspond to the format of a data type double. The data type thus depends on the format of the input. This does not mean, such. For example, the format mark of the decimal point / point is displayed (at 5.5 or 5.5). The decisive factor is the data type of the value to be processed. Only then can you perform arithmetic operations by entering the weight.

## Formatting With Escape [Sequences](https://translate.googleusercontent.com/translate_f#page114)             

Programs should not only work properly, they should also be easy to use. The input mask presented to the user should be largely self-explanatory and concise. It follows that we need to format the output to the console accordingly. This is where the escape sequences help.  This is to be discussed in detail. Escape sequences allow you to output certain special characters as well as characters that have a special meaning for the C# compiler. A classic problem is the double quotes "". Just write these into a string constant

Console.WriteLine ("I am a string constant");

you get an error message from the C# compiler. The double quotes for the C# compiler mean that the text between two quotes is interpreted as a string constant, in the example, "I am a". After that, the compiler expects an expression or the end of the statement. The remainder of the string constant actually belonging to the text to be output is ignored. So the C# compiler looks at the above line in the form

Console.WriteLine ("I am one"

Of course, the closing bracket and the semicolon are missing here. This is exactly one of the error messages that the C# compiler outputs.

What to do if you want to output one or more double quotes in the output. In this case you use the corresponding escape sequence.

\ "

Escape sequences always start with a backslash, followed by a wider-res character. The escape sequence \ " prints a double quotation mark ("), which solves the previous problem easily.

Console.WriteLine ("I am a \" string constant \ "");

As output in the console you get then

I am a "string constant"

## Format Numbers             

The C# programming language not only provides escape sequences for formatting the output, but also special characters for formatting numbers. These formatting characters have their own syntax in C#.

## Standard Formatting Of Numbers

When you format numbers, you will most often use the standard formatting provided by the C# programming language. Depending on how you want to represent numbers, there are various possibilities.

Would you like z. For example, to output an integer, that is, values  of type int, with a certain number of decimal places, use the formatting character d. Use this character to specify the desired number of digits. B. d5 for 5 digits.

...

int iNumber = 200;

...

Console.WriteLine ("Number: {0: d5}", iNumber);

...

The value of iNumber is given by the formatting with two leading zeros.

Number: 00200

The number of decimal places specified by the d formatter are minimum digits. Use instead the number 200000, this is not reduced to 5 digits.

In mathematical applications or scientific results one often uses the exponential representation. Again, the programming language C# offers a convenient formatting option, the character e, which you can use to set the desired number of decimal places to be output:

Console.WriteLine ("Number: {0: e3}", iNumber);

The output of the value 200 is now in the form

2,000e + 002

2,000e + 002 means 2,000 * 10 2 = 2,000 * 100 = 200.

Another example: The value 123456789 is output with the help of the formatting symbol e10 :

1,2345678900e + 008

## Formatting Floating Point Numbers

In conjunction with floating-point numbers, C# provides two formatting characters that can be used to influence the number of decimal places: f and n. To do this, write the desired number of digits behind one of the characters. The difference between the two formatting marks lies in the representation of the thousands places. First of all, an example.

...

double dNumber = 12345.54321;

...

Console.WriteLine ("number: {0: f}", dzahl);

...

If you use the format character f without a position, the default value of two decimal places is output:

Number: 12345.54

An example of formatting values  with five decimal places:

Console.WriteLine ("number: {0: f5}", dzahl);

To improve the readability of large floating-point numbers, the C# programming language provides the ability to mark thousands of digits with a separator (thousands of points). For this one uses the formatting mark n. So gives the formatting

Console.WriteLine ("number: {0: n5}", dzahl);

the number

Number: 12.345,54321

with the thousands separator and five digits after the decimal point.

If you limit floating-point numbers to a certain number of decimal places, you do not have to worry about rounding the decimal places. This is done by the formatting or the C# compiler for you; it will be rounded up or down accordingly.

## Currency Format

C# makes it easy to format a number as a currency. When specifying the currency, the country-specific setting of the computer is used. The default setting of the decimal places of the currency format is 2\. So there

...

double dBetrag = 199.99;

...

Console.WriteLine ("Amount: {0: c}", dBetrag);

...

the amount with two decimal places and the currency information.

Amount: 199.99 _

Again, the automatic rounding of the output works.

Console.WriteLine ("Amount: {0: c1}", dBetrag);

Amount: 200.0 _

## Special Formatting

The programming language C# offers two further formatting types:

Formatting in hexadecimal numbering system general formatting

With the help of hexadecimal numbers you can eg. For example, the contents of memory addresses can be rendered more elegantly and efficiently than would be possible with decimal values. Thus, the number 10 in the decimal number representation corresponds to the letter A or a in hexadecimal representation. For hex values, the format characters x and X are offered. First of all to x :

...

int iNumber = 10;

...

Console.WriteLine ("Hex: {0: x}", iNumber);

...

The following line appears in the output

Hex: a

So lowercase letters are output. However, if you prefer uppercase letters, use the X formatting character :

Console.WriteLine ("Hex: {0: X}", iNumber);

The output now looks like this:

Hex: A

The same case-sensitivity of the formatting characters also works with the exponential representation.

For the so-called general formatting the formatting marks g and G (general) are offered. This type of number representation is the least expensive and makes sense if there is only limited space available for the output, but the numerical information is to be reproduced unadulterated. Here the C# compiler decides which type of representation is used.

## Custom Formatting             

Although C# has a whole range of formatting options, not all cases are covered in practice by far. For example, no volume unit liters is offered by default. However, there is the possibility to create user-defined formats.

## 0 Formatting

If you need leading zeros for the output of a number, you can do so by custom 0 formatting. Custom 0 formatting also supports the representation of floating-point numbers.

...

int i = 54321;

double d = 12345.54321;

...

WriteLine ("{0: 00000000}", i);

For 0-formatting, write a 0 (the number) for each decimal place to be displayed. In the example, each value is output with 8 digits. The zeros in the formatting are overwritten by the number shown. The value 54321 (variable i of type int) is therefore represented with three leading zeros:

00054321

For floating-point numbers, you must explicitly specify the decimal places in the formatting. If you want to output the value of variable d with three descendants, the formatting will look like this

WriteLine ("{0: 00000000,000}", d);

With this type of formatting, the decimal places are automatically rounded as in the standard formatting. So we get at the issue

00012345.543

also three leading zeros and additionally three decimal places.

## Cross-Formatting

In the so-called cross-formatting, the # character serves as a general placeholder without special fill characters such. For example, if we use the variables of the previous section, then the statement represents

WriteLine ("{0: #}", i);

no special formatting policy, the output is without special

Characteristics:

54321

The advantage of cross-formatting is that you can insert arbitrary characters as separators at specified positions in the number, and this approach can be combined well with leading zeros and decimal places. The formatting

WriteLine ("{0: 0 ## - ###}", i);

returns a special combination of numbers with leading zeros and the hyphen (-).

054-321

Of course, the cross-formatting can also be used to represent floating-point numbers. So gives the instruction

WriteLine ("{. 0: # 00}", d);

the value 12345.54321 of variable d with two decimal places :

12345.54

## Formatting Groups

Grouping numbers is needed relatively often. We already know one kind of grouping - the thousands separator. But in practice, a variety of other groupings occur, for. For example, the ISBN number, bar code numbers, etc.

This type of representation can be easily implemented in C# in combination with the formatting characters 0 and #. The following example contains some examples of how to group numbers. But there are two exceptions that may cause errors in the general grouping, as they are reserved. 

## Percent Formatting

When outputting values  that are to be displayed in percent format, no additional, manual multiplication by 100 is necessary. With the help of the formatting character %, a value is automatically converted to a percentage value and formatted accordingly.

Here is an example: First, the variable dMwSt of type double is assigned the value 0.16 :

...

double dMwSt = 0.16;

...

The result is output using percent formatting.

Console.WriteLine ("{0: #%}", dMwSt);

We get the issue 16%.

## Literals Formatting

Let us remember that various units of measure, eg. For example, liters are not supported by C# by default. This problem can be counteracted with literal formatting, with which, for. B. the unit liter can be mapped.

Here we need in our program special formatting, which also includes the liter.

Suppose, for example, that the current capacity of a milk boiler should be expressed in one liter. For this we only need to include the word liter in our formatting.

...

int iFuel = 100000;

...

Console.WriteLine ("{0: #, # liter}", iFuel);

This gives us the output

100,000 liters

## Case Formatting

In special cases, you have to format numbers differently, depending on whether they are negative, positive or null. Case formatting makes such dependent formatting easy and convenient. The three cases (for negative, positive and zero) are written next to each other in the formatting string and separated by semicolons (;). 

## Format Date And Time Values             

Of course, before we start formatting dates and times, we need to know how to create dates and times in C#. For this the class DateTime is offered. From this class we use the properties for the further use of date and time values

Now

and

Today

The Now property returns the current date and time as the datetime type.

WriteLine (DateTime.Now);

deliver us

06.06.2002 17:22:03

The Today property returns the current date. Since the datetime type is used again, the dummy time 00:00:00 is returned next to the date.

WriteLine (DateTime.Today);

returns the following:

06.06.2002 00:00:00

The two properties Now and Today of the DateTime class can not only return a complete date and time value, but also individual components. 

## Output of Enumerations

You know that these are realized by the enum data type. When outputting enumerations, there are also formatting characters available that formulate the value less, but rather determine what is displayed - the stored value (string) itself or the numeric value to which it is assigned. 

## Compare Strings

You probably know the annoying input masks in which you have to enter the user name and password. What usually happens here is that strings entered by the user are compared to values  stored in the program or stored in a database. For such and other purposes C# offers different methods and properties. 

## Insert, Delete and Replace

The programming language C# has convenient options for inserting, copying, replacing and deleting within strings. For this we have the following methods available.

Insert (Start Pos, String2) adds the string String2 from the position Startpos in the current string.

Remove (Startpos, Number) deletes the specified number of characters from the position Startpos.

Replace (search string, new string) replaces the substring search string with the string NewString. The replacement takes place globally, ie if the substring occurs several times, all occurrences are replaced.

## Preparing Strings

Often, user input or data that has been read in other ways, such as A database, not the expected format. For example, in practice, leading blanks often need to be removed. For such tasks, C# provides the following methods:

Trim () removes all leading and trailing spaces in a string.

ToUpper () converts all characters of a string to uppercase.

ToLower () converts all characters of a string to lowercase.

PadLeft inserts so many spaces at the beginning of a string that the string is stretched to the length of new_string_length.

PadRight appends so many spaces to a string that the string is stretched to the length of new_string_length.

Substring (Pos start, number) returns a substring with the length number from the current string, starting from PosBin.

# 
Chapter 6 - Flow Control

Sequential control systems are special instructions that control the execution (control) of programs. Using only instructions, the program runs strictly sequential. The various variants of scheduling, with their variety of control structures, allow the programmer to react to certain conditions or repeat instructions until a condition occurs.

## Branches             

In the C# programming language, there are three ways to branch within a program. They are the keywords if, else and switch. The simplest way to create a branch is the if statement. If the comparison of an expression matches a condition, the instructions are executed. There is also the possibility to control a condition and to take an alternative branch in case of non-fulfillment. For this we need the if-else statement. The switch statement allows us multiple selections where the various statements can be executed in a greater number of choices. Again, there is an alternative branch.

If statement - Review

An if statement controls a statement block and executes the code it contains only when the condition is met. The syntax of an if statement - depending on its formulation - looks like this:

if (condition)

instruction;

or

if (condition)

{

instruction;

}

or

if (condition)

{

instruction;

instruction;

...

}

The behavior of an if statement depends on the expression of the condition.

If the if statement is to execute only one statement, one can use the curly ones

Omit parentheses. But it does not hurt if you have the curly

Brackets sets, quite the contrary, the code is clearer.

The following example shows that there can be undesirable results if you do not set a statement block. Suppose you need an if statement that checks two numbers for equality. For this we use the variables i and j. These variables both have the value 5. The variable i should be output and then the value of the variable j should be decremented by 1. In the following form, however, the if statement becomes

if (i == j)

WriteLine (i);

J--;

do not fulfill the intended purpose. From the if statement

if (i == j)

depends only the instruction

WriteLine (i);

from. The instruction

J--;

will be executed in any case. If several statements depend on one condition of an if statement, they must be written in curly braces. The correct source code that fulfills the task looks as follows:

if (i == j)

{

WriteLine (i);

J--;

}

In daily programming everyday tasks often arise that can not be solved with an if statement alone. 

The problems in everyday life are usually complex processes that can not be solved with a single if or if-else statement. If there is a possibility of selection, this can include further options. In this case, nested multiple if statements and if-else statements are nested. This nesting is called nested conditional statements.

## Switch Statement

If you use a condition that has more than two alternatives, you could use multiple if or if-else constructs for it, but this does not lead to a very clear code. An alternative to this is the switch statement. This allows the selection of any number of alternatives in a hierarchy and thus corresponds to several if- statements in a row. The switch statement is also known as multiple selection or case discrimination. The syntax of the switch statement looks like this:

switch (expression)

{

case constant_expression1:

[Instructions)

break, goto case N;]

case constant_expression2:

[Instructions)

break, goto case N;]

...

...

...

case constant_expression...:

[Instructions)

break, goto case N;]

[default:

[Instructions)

break, goto case N;]]

}

The expression of the switch statement contains the condition to be evaluated, which is used to decide which statement block is executed. The statement blocks are prefixed with the case keyword, with a consistent expression defining the value to check for. If the constant expression in the case branch coincides with the expression of the switch statement, the statement or statements of the relevant case branch are executed. If this does not apply to any of the constant expressions, the default branch of the switch statement is executed, if available.

If there is no match between the expression of the switch statement and the constant expressions and the default branch is missing, the entire switch statement is ignored.

In a switch statement, if any instructions exist, each case branch has an abort mechanism that either sets the switch statement with the keyword

break;

leaves, or with

goto case N;

activates another case branch within the same switch statement.

## Grinding             

Loops are used in programming to execute instructions repeatedly. In jargon, repetitions are also called iterations. The functional counterpart to an iteration is recursion. In a recursion not statements and statement blocks are repeated, but complete functions or methods. 

## The Forefather Of The Loops - Goto Instruction

In the beginnings of computer science repetitions were realized by the goto statement. A goto statement, so to speak, jumps to a line and continues to execute the statements there. The structure was previously unstructured, the readability and clarity accordingly poor. Positions in the source code that can be jumped to are called jump labels. A jump label is a fixed name followed by a colon.

The syntax of a goto statement is:

goto jump label;

...

Label: instructions

As you noted above, I give the goto statement a negative image, and rightly so. Because it allows it to jump to any point in the program, which is not conducive to a structured structure with logical and comprehensible train of thought. This may not really matter in a one or two jump program, but as soon as you jump through a program, you quickly lose track.

You will now wonder why the programming language C# has kept the goto statement. This is because, in some situations, it is either imperative to solve a problem or at least greatly simplify the solution. Thus, with deeply nested loops, it may be necessary to leave them in certain program states - with one jump. But you should use the goto statement very sparingly and if possible resort to more elegant alternatives.

## Continue Statement

The continue statement is the counterpart to the break statement. If you use the continue statement in a loop, it breaks off exactly at the position where the continue statement is located. This will continue with the next loop pass.

# 
Chapter 7 - Methods, Parameters And Validity Of Variables

The larger and more complex a program becomes, the clearer it should be designed. The size and complexity of your programs will increase with your skills. So it is important to write the programs so that they are manageable and easy to maintain by breaking the structure of the programs into logical and physical modules. The advantage of this procedure is that these modules are implemented and optimized once in the program. For further use, you do not have to worry about how they work - the module becomes a black box.

## Definition and Call             

We already know that the programming language C# maps everything into classes. The functions, because they are elements of the classes, are called element functions. Over time, the term method for the element functions has prevailed. A method is thus a function within a class and belongs to the set of classes. However, many programmers do not distinguish exactly the designation rules in everyday language usage. We just have to remember that functions within a class are element functions or methods.

There are several ways to define methods.

Public - this type of method is used to communicate with the environment. They are visible to the outside and perform tasks that the environment demands.

Private - this type of method is used to execute repetitive statements and tasks within a class that cannot be called directly by the environment.

In this chapter we will deal exclusively with the second kind.

The method body contains the declarations and statements that are executed after the method is called.

## Parameters Of A Method             

Methods always fulfill a task and may require data. You can pass the data to a method using parameters that you want to process in the method. The way in which a method is supplied with data depends on the task. In principle, a distinction is made between value and reference parameters.

## Defining Parameters

If a method is to work with parameters, these must be defined in the method header. Several parameters are separated by a comma. Each parameter requires its data type and parameter name.

private static int add (int parameter1, int parameter2)

{

Instructions;

}

If you call the method Add () as shown above, it requires two parameters of the type Integer. Note that the data types of the arguments are the same as those specified in the method definition.

From the point of view of the method, we always speak of parameters. Parameters are taken from the method definition.

In connection with the call of a method we speak of arguments. Arguments are passed to the method definition.

## Types Of Parameters

The C# programming language essentially distinguishes two types of parameters. The first type are value parameters, as the example above shows. For a value parameter, only a copy of the value is passed. The called method can process the values, but has no direct influence on the parent function.

The second type are reference parameters. If a method is a reference parameter, it is defined by the reserved word ref.

# 
Chapter 8 - Arrays

## Data Management with Arrays             

The programs you've seen so far have always had a relatively small, manageable amount of data. But what happens when you need to process more data in a program, such as a larger number of readings or hundreds of addresses that you read from a file or database? Do you need to define hundreds of individual variables?

int iMeasured1, iMeasured2, iMeasured3, iMeasured4...

No, of course there is a much more elegant solution to this problem: the arrays.

The efficient management of larger amounts of data in a program is an age-old problem that computer science has dealt with at an early stage. As a result of these efforts, we now know several basic models for storing data: lists, hashes, stacks, queues and even arrays. What sets the arrays apart from the other data structures is indexed access to the values  stored in the array.

In C#, we can use the System.Array class to create arrays. For the sake of simplicity, we refer to variables that refer to array objects as arrays as well.

## Sort Arrays

Arrays of numbers or strings can be conveniently sorted using the array.Sort () static array method. All you have to do is call the method and pass it the array instance you want to sort. The contained elements (numbers or strings) are then sorted in ascending order.

## 
Search In Sorted Arrays

Arrays can manage larger amounts of data. Storing values  or objects in an array, however, would be quite uninteresting if it were not possible to efficiently manipulate the elements in the array. These include:

The indexed access to individual elements,

Traversing the array elements in a loop and finding a particular element in the array.

A simple but inefficient way to search for a name is to loop through the array and test for each element if it contains the name you are looking for. Such a search can be very fast (if the first element contains the name you are looking for), but it can take a long time (if the last element contains the name you are looking for or the name is not stored in the array).

A much more efficient search method is Binary Search, which assumes that the array is sorted. The binary search picks the middle element out of the array and checks if it is smaller or larger than the value you are looking for. Depending on the result of the comparison, searches are then continued for the same pattern in the lower or upper half of the array. In this way, the search space is halved at each step. The binary search is quite efficient; for an array with n elements, the search ends at the latest after log 2 (n + 1) comparisons.

Fortunately, the System.Array class already has a ready-implemented static method of doing binary searches: BinarySearch (). When calling, you pass to the method the array to search and the value to find. As a result, you get back the index of the item containing the value you are looking for (or a value less than 0 if the value was not found).

## 
Arrays As Parameters

Of course, arrays can also be passed as arguments to methods. The method defines a parameter of the corresponding array type:

static void values  output (int [] param)

{

foreach (int elem in param)

WriteLine (elem);

}

When called, the array to be edited is simply passed to the parameter:

static void Main ()

{

int [] anArray = {1, 2, 3, 4, 5,

6, 7, 8, 9, 10};

Outputting values  (anArray);

}

## Composite Arrays             

Arrays do not necessarily consist of a linear sequence of elements. Arrays can be multidimensional and they can contain other arrays as elements.

### Multidimensional Arrays

One-dimensional arrays can be thought of as a linear sequence of values:

12345

Two-dimensional arrays can be thought of as values  that resemble one another

Table arranged in rows and columns:

11 12 13 14 15

21 22 23 24 25

31 32 33 34 35

Three-dimensional arrays would be like cubes (with width, height, and depth), and with four-dimensional arrays, our imagination will be so slow.

To define a multidimensional array, specify the sizes of each dimension separated by commas in the square array brackets.

int [,] pay = new int [10,20];

For example, the above definition creates a two-dimensional array of 10 by 20 numbers. If you think of the array as a table, it would consist of 10 rows (first dimension) and 20 columns (second dimension).

Just as you define the array, you access its elements:

pay [5, 2] = 12;

Here, [the third](https://translate.googleusercontent.com/translate_f#page268) element in the sixth line is accessed (remember that the indexing of each dimension starts with 0).

## There Is No Multidimensionality

In fact, there are no multidimensional arrays, because the working memory in which the elements of the array are created is, after all, only a linear, one-dimensional sequence of memory cells. So the multidimensionality of the arrays is something we just foolishly think about and that's why working with data like For example, the values  of a table - which are inherently multi-dimensionally organized - are simplified.

## Arrays Of Arrays

Multi-dimensional arrays have the special property that the elements of a dimension always have [the](https://translate.googleusercontent.com/translate_f#page272) same length. For example, a two-dimensional array consists of a certain number of rows, all of which have the same number of columns (second dimension).

In practice, however, one often has to do with data that is not quite as regularly arranged. For example, suppose that in the parquet of the previous section there are only 18 seats in the third and fourth rows.

Such a parquet can not be represented by a two-dimensional array, but rather as an array whose elements themselves are again arrays.

# 
Chapter 9 - Fields

Fields are the data members of the class. They are defined by specifying an access specifier, the data type and the field name:

class CDemo

{

int field1; // private field internal double field2;...

Its scope is the class itself, which means that all methods of the class (including the constructor, destructor, properties) can access the fields.

When creating an instance, the generated object gets its own copy of each field in the class. The lifetime of a field is therefore equal to the lifetime of the object to which it belongs.

## Initialization

The usual place to initialize fields is the constructor:

class CDemo

{

int field1;

internal CDemo ()

{

field1 = 12;

}

...

However, from a technical point of view, this is not an initialization, but merely the assignment of an initial value. The field was already initialized when it was created (as it was created in the memory area of  the object). The compiler assigns the fields their default values  (for example 0 for int or double, false for bool). If you want a field to be initialized with a different value, you must specify it in the field definition:

class CDemo

{

int field1 = 122;

internal CDemo ()

{

WriteLine (Field1); // returns 122             

}

...

True initialization is faster than assigning an initial value in the constructor, but it is also less flexible because essentially only literals can be assigned.

## Object Variables As Fields

Fields can also be of the type of a class. These fields are treated like all other fields. However, it is important to make sure that an object is assigned to the field before elements of that class are accessed through the field.

class CEclass

{

int worth;

...

}

class CDemo

{

CEclass field;

internal CDemo ()

{

field = new CEineClass (); // assignment of an object             

...

## 
Constant Fields

Constant fields are fields whose value can not be changed after the assignment of an initial value. In C# there are two ways to define a constant field:

const declaration

read-only declaration

The const declaration

class CDemo

{

public const int field = 3;

In the definition, const fields must be initialized with a constant value, ie a literal or the value of another const field.

Thereafter, the value of the field can be queried, but not changed.

# 
Chapter 10 - Heredity

Inheritance in the object-oriented sense means that a class passes on the elements defined in it to another class. Therefore, to see them as a mere means of convenient code reuse would be wrong and would not do it justice, because inheritance involves a number of other important object-oriented concepts, such as the overriding of methods, polymorphism, the abstract classes and the construction of class hierarchies. So we are dealing with a rather extensive network of interdependent and interdependent concepts based on inheritance. Nonetheless, inheritance itself is only a partial aspect of an even larger thematic complex - the question of which classes can relate to each other.

The next two days introduce you to the higher consecrations of object-oriented programming. Today begins with the basic syntax of inheritance and its implementation in simple programs. Tomorrow is dedicated to polymorphism, class hierarchies and interfaces.

Do not grieve if your head eventually becomes inaccessible given the variety of syntax forms and alternative techniques. With most of the techniques presented today and tomorrow, in practice, you will come into contact with them gradually, and it is quite natural (and so thought) that you will then go back to the relevant chapters and sub-chapters and these read again. But this should not be an excuse to skip the chapter now. Work through the chapters carefully and above all try to understand the concepts and ideas behind the techniques. Be sure to read the summaries at the end of the chapters, which will give you a concentrated overview of the concepts presented.

## The Principle Of Inheritance             

With inheritance, a new class is derived from an existing class.

The derived class inherits the elements of its base class.

Base class and derived class are normal classes. The terms "base class" and "derived class" refer only to what role the classes perform in inheritance:

The base class passes (inherits) its elements.

The derived class receives (inherits) the elements.

Looking at the inheritance from the perspective of the derived class, one also speaks of derivation.

## The Basic Mechanism

Consider the following simple class:

class CBasis

{

public int value;

public void output ()

{

Console.WriteLine ("value = {0}", value);

}

}

If you want to use this class as the base class of a new class, just append the name of the base class with a colon to the name of the new class when defining the new class.

class CAdirected: CBasis

{

public void Increases ()

{

Value + = 10;

}

}

Now, the derived class CAb, in addition to its self-defined method, Elevations (), also automatically has the elements of the base class. You Beach th that can be used as early as the methods of abge-initiated class inherited members even (in our example, the method increases increase () the field value that the class CAbgeleitet of the class CBasis inherited has).

## The Meaning Of Inheritance

Throughout your career as a programmer, you will write a variety of classes to represent a wide range of objects and to solve a wide variety of tasks. At some point, you'll find that implementing a class that you want to create can very well use the functionality of a class you once wrote a long time ago. This raises the question of how the functionality representing a class can be meaningfully reused in the implementation of new classes. Object-oriented programming offers two different, complementary concepts in response to this question: inheritance and embedding.

While inheritance passes the elements of the existing class to the new class, embedding does nothing other than defining a field of the existing class type in the new class. 

 ![](images/00002.jpeg)

Even though you may not have been fully aware, you have been diligently using the concept of embedding, because whenever you declare a field of type class string in one of your classes, you have used the concept of embedding.

## 
Some Important Facts

The issue of inheritance is quite complex, too complex to be summarized here in a few sentences. Therefore, this section is intended only to draw your attention to a few points and technical details that are quickly passed on when dealing with the far more important concepts, forgotten by the author, or taken for granted.

The base class inherits all elements defined in it except the constructors and destructors.

There is no way to influence the selection of inherited elements. (That is, you can not choose to inherit a particular constructor, nor can you exclude a field or method from inheritance.)

The base class is not changed by the inheritance. (The inherited elements are not missing later in the base class, nor do definitions in the derived class return to the base class.)

## 
Inherited Elements Form Sub-Objects

When elements are passed by inheritance from a base class to a derived class, they form an independent subset, a base class part, in the derived class. On the one hand, the inheritance then makes the elements part of the derived class, on the other hand they remain base class elements once for all.

A small analogy should clarify this. Imagine being a car designer and builder. For people with the necessary change, you design and build fancy single models. For example, a wealthy Emir recently ordered the "Blue Eagle" model from you. As the basis for this model, you use the chassis and engine of a Jaguar E, chassis and interior make yourself. You sell the finished car for 120,000 euros to the Emir, who is now the proud owner of a "Blue Eagle". The "Blue Eagle" does not indicate that it was built on the basis of a Jaguar E. The components of the Jaguar have become parts of the »Blue Eagle«. However, there are still Jaguar elements, and if there is a problem with the chassis or engine, the Emir must contact a Jaguar dealer for repair.

Similarly, the inherited elements become part of the derived class, but without abandoning their descent from the base class. This has consequences for programming with inherited elements.

In principle, you can program with the inherited elements as well as with the elements that were defined directly in the derived class (see example: inheritance.cs). In certain situations, however, the basic class origin of the inherited elements comes to the fore and must be taken into account. 

## Why Do The Inherited Elements Form Sub-Objects?

The simple answer to this question is: inheritance is just an object-oriented concept and not a self-service store, in which one packs a field and a method into the shopping cart. After all, the author of the base class thought a bit about the definition of the class: He has written methods for controlled access to the fields and declared the fields as private, so that they can only be read or changed using the relevant methods. He also dumped subproblems in helper methods that are widely used by other methods in the class. Last but not least, he has written a constructor to correctly initialize the fields of the class.

Would inheritance work so that you could pick out individual elements of the basic classes or directly access inherited private elements for which the author of the base classes provided appropriate access methods in the methods of the derived class (see introductory example), breaking the complex structure of the base class and destroying the protections set up by the author of the base class, which should ensure the correct use of the base class elements. The actual, object-oriented mechanism of inheritance, on the other hand, ensures that this complex structure of effects, including the protective measures provided, is only inherited as a whole, as a subunit. Thus, the base class is protected from misuse and the author of the derived class from unnecessary errors in the use of the inherited elements.

Another reason for the object-oriented nature of inheritance is that on inheritance, other important object-oriented concepts, namely the construction of class hierarchies and polymorphism, build.

## Three Access Levels

You now know that the inherited elements in the derived class retain their self-sufficiency and their access protection. Therefore, methods defined in the derived class can not access inherited private elements. What role the access specifiers still play in inheritance, this section will clarify. Particularly important for the understanding are the three central specifiers public, protected and private.

In the following discussion, we will exclude the access specifier internal as a (restricted) special case of public access.

Public, protected and private

As a reminder, the purpose of the access specifiers is to protect individual elements from outside access, with the goal of making the use of the objects of the class safe and protecting the integrity of the objects.

Considering only the access specifiers public and private, the use and meaning of the specifiers are easy to grasp: there are only two levels of access, inside (ie within the class definition, which ultimately means "in the code of class methods") and outside (ie in code outside the class definition, which means that access is via an object of the class). The author of a class declares elements that are to be accessible from the outside as public, while marks elements that are to be used internally only by the methods of the class as private. 

## Three access levels

When you create an object from a derived class, the inherited elements in that object form a sub-object.

From the perspective of this sub-object, the three access levels are as follows: The sub-object itself is the inner world within which there is no access restriction (the sub-object's methods can access all other elements of the sub-object directly). The outside world consists of two layers. The first layer is the derived object. Out of this layer - that is, in the methods defined in the derived class - is allowed access to the public and protected, but not private, elements of the sub-object. The second layer is any outer code that creates an object of the derived class and uses it to access the elements of the sub-object. From this layer only the public elements can be accessed.

From the perspective of the derived object, there are also three levels. The first level is the object itself with the elements defined in its class. Within this level, direct, unrestricted access applies. The second level is the inherited base class subobject. Its elements can be directly accessed by the methods defined in the derived class, but with respect to the access specifiers. The third level is the outside world, which can access only an object variable and only the public elements of the object (own as well as inherited).

From the outside world's point of view, there is only a single object (the subobject is not perceived as such) and a form of access: via an object variable and only to public or internal elements (the public interface).

## Access To Hidden Elements

Hidden elements - this applies not only to hiddenness in derived classes, but in general - continue to exist even after the occlusion, but can no longer be accessed because their name would be in the relevant area of  validity (in the case of inheritance) this, for example, the derived class) has been connected to another element.

class CBasis

{

protected double value;

}

class CAdirected: CBasis

{

new public int value;

public void value setting (int p)

{

Value = p; // access to the newly defined element             

}

}

Here the element value obscures the inherited element of the same name. The valueSetting () method therefore accesses the value element defined in the CAb-routed class.

Inherited elements that were obscured in the derived class are still present and are still accessible. The programmer must precede the element name with only the keyword base, which represents the base class. This tells the compiler explicitly that it does not mean the element defined in the current class, but the same-named element that comes from the base class.

public void value setting (int p)

{

base.value = p; // Access to the hidden base class member             

}

The base keyword is mainly needed to invoke the base class version of the same name in hidden (or over-written) methods - as in the C number box method Insert () from the example above:

class CEigenerKK: CKummerkasten

{

new public void insert (string letter)

{

DateTime today = DateTime.Now;

letter = today.ToString () + ":" + letter; base.Einwerfen (brief);

}

}

The new warning

Whenever you obscure an inherited element in a derived class, the compiler generates a warning that alerts you of the occlusion and prompts you to either avoid it or tag it as intentional using the keyword new.

Perhaps one or the other reader will now think that this keyword is actually quite unnecessary, because after all, as a programmer, you should be able to ensure that you do not inadvertently cover up any inherited elements. Well, this may be true, as long as the programmer implements base classes and derived classes himself and the code remains quite clear. However, the more extensive the classes become, the more difficult it becomes, and it becomes nearly impossible for the programmer to derive from classes whose source code he does not know.

Consider the following scenario: You have acquired a library of classes to implement a inventory system. The library also includes a class CLieferauftrag, which does not quite meet your expectations. Since only the compiled library is available to you and you can not directly adapt the definition of the CLorder order class, you decide to assign your class a class CMasselivery order and provide the corresponding functionality (some additional fields and methods). add. In doing so, you overlook the fact that one of the methods you have added has the same signature as one of the methods inherited from CLieferauftrag. Without realizing it and without wanting it, you cover up the inherited method. Only the warning of the compiler makes you aware of it.

The warning also helps with naming conflicts due to changed base class versions. Let us stay with the example of the class CMeinLieferauftrag. These have been extended by an additional Discount () method compared to the base class CLorder order. Now the author of the Inventory Library delivers the newest version, in which the class CLjob order was also revised and supplemented with a discount () method. You install the new library version and recompile your code. The compiler detects that your discount () method obscures the now-existing discount () base class method and warns you.

So, if you receive a warning from the compiler to hide an inherited method, check whether the method really should be obscured. If so, set the keyword new before redefining the method and the compiler will no longer question the occlusion.

## Inheritance vs. Embedding

The equivalent to inheritance is the embedding. Embedding means that a class defines fields that come from the data type of another class. While heredity is characterized by an "is-a" relationship, embedding corresponds to a "has-a" relationship.

For example, given three classes CMotor, CAuto and CSportwagen. What are the relationships between these classes?

There is a relationship between CAuto and CMotor, because a car has an engine. In the definition of the class CMotor this is expressed as follows:

class CMotor...

class CAuto

{

CMotor myMotor;

...

On the other hand, there is an "is a" relationship between the classes CAuto and CSportwagen. The class CSportwagen is derived from CAuto (and automatically inherits the CMotor element).

## Nested Classes

From the fact that type definitions are allowed within classes, it follows that one class can be defined in another class. In addition to inheritance and embedding, this so-called nesting is the third form of the relationship between classes.

class CAussen

{

public class Cin

{

...

}

// other elements of CAussen

}

# 
Chapter 11 - Projects

## Making Code Decisions

Taking an example of banking application, we want to allow a withdrawal only if the amount to be withdrawn is less than or equal to the account balance, ie if the account balance is greater than or equal to the withdrawal amount, we must allow the transaction, otherwise we cannot allow the withdrawal. We need to do conditional execution of code.

In C #, we can execute conditional code using the if construct:

if (condition)

{

// This code will only execute if the condition is true

}

In our example, we want to execute the withdrawal logic only if the balance is greater than or equal to the withdrawal amount:

double balance = 100.0;

double valueBag = 10.0;

if (balance> = bag value)

{

// withdraw code.

}

The withdrawal code should decrease the account balance and display a message to the user indicating that the withdrawal was successful:

double balance = 100.0;

double valueBag = 10.0;

if (balance> = bag value)

{

balance = balance - valueSac;

MessageBox.Show ( "Withdrawal Successful" );

}

Note that if the account does not have sufficient balance to withdraw, the user is not warned. So we are in the following situation: "If the account has sufficient balance, I want to withdraw, otherwise I want to show the message Insufficient Balance to the user." To do this, we can use C # else :

if (balance> = bag value)

{

// withdraw code

}

else

{

MessageBox.Show ( "Insufficient Balance" );

}

More On Conditions

Notice the expression we pass to if : balance> = valueSak . In it we use the "greater or equal" operator. In addition, there are other comparison operators that we can use: greater (>), smaller (<), less or equal (<=), equal (==), and different (! =). We can also deny an if condition using the ! in front of the condition that will be denied.

In the previous chapter, we saw that a value has an associated type in C #: 10 is an int , "message" is a string . Similarly, the expression balance> = valueSak also has an associated type: the bool type , which can assume the values true or false . We can even store such a value in a variable:

bool canSacchar = (balance> = valueSac);

We can also perform some operations with bool values . We can, for example, verify that two conditions are true at the same time by using the && (AND) operator to make one and logical:

bool reallyCanSaccount = (balance> = valueSac) && (valueSac> 0);

When we need a logical OU, we use the || operator :

// this condition is true if (balance> = bag value) is true  

// or if (bag value> 0) is true.  

bool reallyCanSacc = = (balance> = valueSac) || (bag value> 0);

Thus we can build more complex conditions for an if . For example, we use the variable realmentePodeSacar declared in if that checks if the customer can withdraw or not:

if (reallyCanSac)

{

// withdraw code

}

else

{

MessageBox.Show ( "Insufficient Balance" );

}

## Optional Exercises

1\. What is the message and value of the balance variable after the following code has been executed?

double balance = 100.0;

double valueBag = 10.0;

if (balance> = bag value)

{

balance - = bag value;

MessageBox.Show ( "Withdrawal Successful" );

}

else

{

MessageBox.Show ( "Insufficient Balance" );

}

message: Withdrawal successful; balance: 90.0

message: Insufficient Balance; balance 90.0

message: Withdrawal successful; balance: 100.0

message: Insufficient Balance; balance 100.0

message: Withdrawal successful; balance: 10.0

2\. What is the message and value of the balance variable after the following code has been executed?

double balance = 5.0;

double valueBag = 10.0;

if (balance> = bag value)

{

balance - = bag value;

MessageBox.Show ( "Withdrawal Successful" );

}

else

{

MessageBox.Show ( "Insufficient Balance" );

}

message: Withdrawal successful; balance: -5.0

message: Insufficient Balance; balance -5.0

message: Withdrawal successful; balance: 5.0

message: Insufficient Balance; balance 5.0

message: Withdrawal successful; balance: 10.0

3.In some cases we may have more than two possible decisions. The bank may, for example, decide that accounts with a balance of less than $ 1000 pay 1% of the maintenance fee, accounts with a balance of $ 1000 to $ 5000 pay 5%, and accounts with a balance of $ 5000 or more pay 10\. %.

To represent this kind of situation, we can use C # else if , which works in conjunction with the if we already know. Here's what the situation described earlier would look like:

double rate;

if (balance <1000)

{

rate = 0.01;

}

else if (balance <= 5000)

{

rate = 0.05;

}

else

{

rate = 0.1;

}

C # will process the conditions in order until it finds one that is satisfied. That is, in the second condition of the code, we just need to check that balance is less than or equal to $ 5000, because if C # arrives in this condition is because it did not enter the first if , that is, we know that the balance is greater or equal to $ 1000 at this point.

Based on this, what will be the message displayed by the following code?

double balance = 500.0;

if (balance <0.0)

{

MessageBox.Show ( "You are in the negative!" );

}

else if (balance <1000000.0)

{

MessageBox.Show ( "You are a good customer" );

}

else

{

MessageBox.Show ( "You are a millionaire!" );

}

"You are in the negative!"

"You are a good customer"

No message

"You're a millionaire!"

"You're a good customer," followed by "You're a millionaire!"

4.A person can only vote in Brazilian elections if he or she is over 16 years old and is a Brazilian citizen. Create a program with two variables, int age, Brazilian bool , and have the program tell you if the person is able to vote or not, according to the data in the variables.

5.Create a program that has a doubleFiscalDateValue variable , and according to that value, the tax must be calculated. The calculation rules are:

If the value is less than or equal to 999, the tax must be 2%.

If the value is between 1000 and 2999, the tax should be 2.5%

If the value is between 3000 and 6999, the tax should be 2.8%

If it is greater than or equal to 7000, the tax must be 3%.

Print the tax on a MessageBox.

6\. (Challenge) Given the following code:

int value = 15;

string message = "";

if (value> 10)

{

message = "Greater than ten";

}

else

{

message = "Less than ten;

}

MessageBox.Show (message);

There is a way to make this code if only one line, without using the word if and else. Research this and try it.

for ;

## Repeating A Code Block

Back to the example from the previous class, suppose now that the same bank customer wants to know how much he will earn at the end of one year if he invests a value. The investment pays 1% of the amount invested per month.

For example, if the customer invests $ 1000 at the end of 12 months, it will be around $ 1126.82: in the first month, $ 1000 + $ 1000 1% = $ 1010, 00; in the second month, $ 1010 + $ 1010 1% = $ 1020.10; and so on. That is, to calculate how much he will have at the end of a year, we can multiply the amount invested 12 times by 1%.

To solve this problem, we need to make use of a control structure that repeats a given block of code until a condition is met. This structure is called loop.

To loop in C #, we will initially use the for statement. The for is an instruction that has three parts:

The first part is the initialization, in which we can declare and initialize a variable that will be used in the second part is the condition of the loop. As long as the loop condition is true, the loop will continue to execute;

The third part is the update, where we can update the variables that are used by for.

Each of the parts of the for is separated by one ; .

for (initialization; condition; update)

{

// This code will execute as long as the condition is true

}

Take the following code, for example, where we use a for that will repeat the calculation 12 times:

double valueInvested = 1000.0;

for ( int i = 1; i <= 12; i + = 1)

{

AmountInvested = AmountInvested * 1.01;

}

MessageBox.Show ( "Amount invested now is" + AmountInvested);

See that our  for   begins by initializing variable i with 1 and repeats the code inside it.                          

do ... while

as long as the value of i is less than or equal to 12, that is, it stops only when i is greater than 12\. And note that with each iteration of this loop, the value of i increases ( i + = 1 ) . In the end, the code inside the for will be repeated 12 times as we needed it.

The same program could be written using a while instead of a for :

double valueInvested = 1000.0;

int i = 1;

while (i <= 12)

{

AmountInvested = AmountInvested * 1.01;

i + = 1;

}

MessageBox.Show ( "Amount invested now is" + AmountInvested);

## To Know More Of While

In C # when using while , the loop condition is checked before all loop turns, but what if we wanted to make sure the loop body is executed at least once? In this case, we can use another type of C # loop, while do :

of

{

// loop body

}

while (condition);

With do while the loop condition is only checked at the end of the loop, ie the loop body is                          

executed and then the condition is checked, then the body always is executed by the            

least once.

To Know More Increment And Decrement

When we want to increment the value of an integer variable by one unit, we see that we have 2 options:

int value = 1;

value = value + 1;

// or value + = 1;   

However, since incrementing the value of a variable is a common programming activity, C # gives us the ++ operator to do this work:

int value = 1;

++ value;

We also have the operator - which performs the decrement of a variable.

## EXERCISES

1\. What is the value displayed in the following code:

total int = 2;

for ( int i = 0; i <5; i + = 1)

{

total = total * 2;

}

MessageBox.Show ( "Total is:" + total);

2.Make a C # program that prints the sum of the numbers from 1 to 1000.

3.Make a C # program that prints all multiples of 3, between 1 and 100.

To find out if a number is a multiple of 3, you can do if (number% 3 == 0) .

4.(Optional) Write a C # program that sums all numbers from 1 to 100, skipping multiples of 3\. The program should print the final result in a MessageBox.

What is the result?

5.(Optional) Write a C # program that prints all numbers that are divisible by 3 or 4 between 0 and 30.

6.(Optional) Make a C # program that prints the factorials 1 through 10\. The factorial of a number n is n n-1 n-2 ... to n = 1.

The factorial of 0 is 1

The factorial of 1 is (0!) * 1 = 1

The factorial of 2 is (1!) * 2 = 2

The factorial of 3 is (2!) * 3 = 6

The factorial of 4 is (3!) * 4 = 24

Make a force that starts a variable n (number) as 1 and factorial (result) as 1 and ranges n from 1 to 10:

int factorial = 1;

for ( int n = 1; n <= 10; n ++)

{

}

7.(Optional) Make a C # program that prints the first numbers of the Fibonacci series to over 100\. The Fibonacci series is as follows: 0, 1, 1, 2, 3, 5, 8, 13, 21 etc. To calculate it, the first element is worth 0, the second is worth 1, henceforth the nth element is worth the (n-1) -th element added to the (n-2) -th element (eg 8 = 5 + 3).

8.(Optional) Make a program that prints the following table using chained for s:

1

2 4  

3 6 9  

4 81216  

nn * 2 n * 3 .... n * n

## CLASSES AND OBJECTS

At this time, we want to represent several accounts in our bank. A bank account is usually composed of a number, name of the holder and balance. We can store this information in variables:

int AccountNumber1 = 1;

string holderDaAccount1 = "Joaquim José" ;

string holderAccount2 = "Silva Xavier" ;

double AccountAccount2 = 2500.0;

Note that because account information is spread across many different variables, it is very easy for us to mix this information into code. Also, imagine that before we add the account to the app we need to validate the holder's CPF. In this case we would need to call a function that performs this validation, but how can we ensure that this validation is always performed?

These points listed are some of the problems with procedural programming style. When working with procedural programming, application data is separated from business logic implementation, and it is very difficult to guarantee application data validations.

## Organizing The Object Code

To start with object orientation, let's first think about what information describes a particular Account. Every bank account has a number, holder and balance. To represent the account with this information within the project, in C #, we need to create a class. Inside C # the class declaration is made using the word class followed by the class name we want to implement:

class Account

{

}

The code of the Account class , by convention, must be inside a file with the same name as the class, so the Account class will be placed in a file called Conta.cs .

Within this class we want to store the information that describes the accounts, we do that by declaring variables within the class, these variables are the attributes:

class Account

{

int number;

string holder;

double balance;

}

But in order for application code to read and write these attributes, we need to declare them using the word public :

Class Account

{

// number, holder and balance are attributes of the object public int number;   

public string holder; public double balance;

}

In order to use the class we create within a windows form application, we need to create a new account in the form code, we do that using the new C # statement:

// form code

private void button1_Click ( object sender, EventArgs e)

{

new Account ();

}

When we use new within the code of a class we are asking C # to create a new instance of Account in memory, that is, C # will allocate enough memory to store all Account information within the application's memory.

In addition, new has one more function, return reference, an arrow that points to the object in memory, which will be used to manipulate the Account created. We can store this reference within an Account variable :

// form code

private void button1_Click ( object sender, EventArgs e)

{

Account c = new Account ();

}

to define the attribute values that will be stored in the Account , we need to access the object that lives in memory. We do this using the operator. C #, telling us which attribute we want to access. To, for example, save the value 1 as the account number we created, we use the following code:

// form code

private void button1_Click ( object sender, EventArgs e)

{

Account c = new Account ();

c.number = 1;

}

With this code, we are navigating to the reference stored in variable c , and accessing the Number field of the Account object that lives in memory. Within this field we put the value 1\. We can do the same for the other fields of the Account :

private void button1_Click ( object sender, EventArgs e)

{

Account c = new Account ();

c.number = 1;

holder = "victor" ;

c.saldo = 100;

}

## Extracting Behavior Through Methods

Now that we have created the first application account, let's try some operations. The first operation we want to implement is the money-out operation. For this, as we saw in the previous chapter, we can use the C = - = operator :

Account c = new Account ();

c.number = 1;

holder = "victor" ;

c.saldo = 100;

// account ends with 50.0 balance c.saldo - = 50.0;   

But what would happen if we tried to get 100.0 more out of this account?

c.saldo - = 100.0;

When we perform this second operation, the account will end with a balance of -50.0 , but in this system accounts cannot have a negative balance! Therefore, before we can withdraw money from the account, we need to check if it has sufficient balance.

if (c.saldo> = 100.0)

{

c.saldo - = 100.0;

}

Note that we will have to copy and paste this check at every point of the application where we wish to make a withdrawal, but what would happen if a withdrawal fee had to be charged? We would have to modify all the points at which the code was copied. It would be more interesting to isolate this code within an Account behavior .

In addition to attributes, objects can also have methods. Methods are blocks of code that isolate business logic from the object. Then we can isolate the logic of the loot within a method

Saca of class Account .

To declare a method called Saca in the Account class , we use the following syntax:

class Account

{

// declaration of attributes

public void Bag ()

{

// Method implementation

}

}

Within this method Saca , we will place the code of the serve logic.

public void Bag ()

{

if (c.saldo> = 100.0)

{

c.saldo - = 100.0;

}

}

However, in this code we have two problems: we cannot use variable c because it was declared in the form and not within the method and the value of the withdrawal is constant.

In this method Saca , we want to check the account balance on which the method was invoked. To access the reference in which a particular method was called, we use the word this . So to access the account balance, we can use this.saldo :

public void Bag ()

{

if ( this .saldo> = 100.0)

{

this .saldo - = 100.0;

}

}

We can use Saca inside the form with the following code:

Account c = new Account ();

// initialize account information c.saldo = 100.0;   

// Now call the Saca method that was defined in class c.Saca ();   

Now let's solve the problem of the fixed value of the withdrawal. When we want to pass a value to a method, we need to pass that value within the parentheses of the method call:

Account c = new Account ();

// initialize account information c.saldo = 100.0;   

// Now call the Saca method that was defined in class c.Saca (10.0);   

To receive the value that was passed in the Saca call , we need to declare an argument in the method. The argument is a variable declared within the parentheses of the method:

public void Bag ( double value)

{

if ( this .saldo> = value)

{

this .saldo - = value;

}

}

A method can have any number of arguments. We only need to separate the declaration of variables with a comma.

## Returning Values Inside The Method

Now that we have put the Sack method into the Account class , we don't need to replicate the withdrawal validation code at all points of the code, we can simply use the method created, and if we need to modify the withdrawal logic, we can simply update the code. that method, a single point in the system.

But as implemented, the user of this method does not know whether or not the withdrawal was successful. We need to have the method return a Boolean value indicating whether or not the operation was successful. We will return true if the operation is successful and false otherwise.

When a method returns a value, the type of the returned value must be before the method name in its declaration. When a method returns no value, we use the void type .

// We are declaring that the method returns a value of type bool public bool Sack ( double value)   

{

// method implementation  

}

Within the implementation of the method, we return a value using the word return followed by the value to be returned. So the implementation of Saca is as follows:

public bool Bag ( double value)

{

if ( this .saldo> = value)

{

this .saldo - = value;

return true ;

}

else

{

return false ;

}

}

When C # performs a return , it immediately returns the value and exits the method, so we can simplify the implementation of Saca to:

public bool Bag ( double value)

{

if ( this .saldo> = value)

{

this .saldo - = value;

return true ;

}

return false ;

}

In the form we can retrieve the value returned by a method.

Account c = new Account ();

// initialize the attributes  

// If the account has sufficient balance, it will work with the value true  

// otherwise, it will contain false  

bool yielded Right = c.Saca (100.0);

if (it worked)

{

MessageBox.Show ( "Withdrawal Successful" );

}

else

{

MessageBox.Show ( "Insufficient Balance" );

}

Or we can use the method return directly within if :

Account c = new Account ();

// initialize the attributes

if (c.Saca (100.0))

{

MessageBox.Show ( "Withdrawal Successful" );

}

else

{

MessageBox.Show ( "Insufficient Balance" );

}

## Standard Value Of Class Attributes

Now that we are done implementing the account withdrawal logic, let's also implement the deposit method. This method will not return any value and will be double argumented:

public void Deposits ( double value)

{

this .saldo + = value;

}

In the main application form, we can initialize the opening balance with the Deposits method :

Account c = new Account ();

c.Deposit (100.0);

In this code we are trying to deposit 100 reais into a newly created account and the Deposit method attempts to sum the 100.0 in the initial value of the account balance attribute. But what is the initial value of an attribute?

When we declare a variable in C #, it starts with an undefined value, so we can't use it until its value is initialized, but the language handles the attributes of a class differently. When we instantiate a class, all of its attributes are initialized to default values. Numeric values are initialized to zero, bool is initialized to false, and attributes that hold references are initialized to the empty reference ( C # null value ).

So in the example, when we deposit 100 reais into the newly created account, we are adding 100 to the initial account balance, which is zero, and then saving the result back to the account balance.

We can change the default value of a given attribute by placing an initial value in its declaration. To initialize the account with an initial balance of 100 reais instead of zero, we can use the following code:

class Account

{

public double balance = 100.0;

// other attributes and methods of the class

}

Now every account created will start with a starting balance of 100.0.

One Example: Download

Now let's try to implement the money transfer operation between two accounts. Within the Account class we will create one more method called Transfer , this method will receive the amount of the transfer and the accounts that will participate in the operation:

public void Transfers ( double amount, Source Account, Destination Account)

{

// implementation of the transfer

}

But do we really need to get both accounts as the method argument

Do you transfer ? Let's see how this method will be used within the form code:

Victor Account = new Account ();

// account initialization victor.saldo = 1000;   

Account guilherme = new Account ();

// account initialization  

// Now let's transfer the money from victor's account to guilherme's victor.Transfer (10.0, victor, guilherme);   

Note that using the method we are repeating the victor variable twice , but this is not necessary. We can use this to access the source account within the method, so in fact the Transfer method only needs to receive the destination account :

public void Transfer ( double amount, Destination Account)

{

// implementation of the transfer

}

Before we can withdraw money from the source account ( this ), we need to check if it has sufficient balance, just in this case we want to withdraw money from the source account and deposit it into the destiny:

public void Transfer ( double amount, Destination Account)

{

if ( this .saldo> = value)

{

this .saldo - = value;

destination.saldo + = value;

}

}

But this behavior of checking if the account has sufficient balance before making the withdrawal is the behavior of the Saca method that was previously implemented, plus adding a value to the balance is the Account Deposits operation . Therefore, we can use existing Saca and Deposit methods to implement Transfere :

public void Transfer ( double amount, Destination Account)

{

if ( this .Bag (value))

{

destination.Deposit (value);

}

}

## Names Convention

When we create a class, it's important to remember that your code will be read by other developers on the team, so it is recommended that you follow naming standards.

When we create a class, the recommendation is to use Pascal Casing to name the class:

If the class name is composed of a single word, we capitalize the first letter (account becomes Account );

If the name consists of several words, all words joined by placing the first letter of each word capitalized (life insurance becomes SeguroDeVida ).

In the case of method names, the convention is also to use Pascal Casing (for example, Draw and Deposit).

For method arguments, the recommendation is to use Pascal Casing but with the first letter in lowercase ( Bag value , for example), a convention called Camel Casing.

You can find Microsoft recommendations at this link: http://msdn.microsoft.com/en-

us / library / ms229040 (v = vs.110) .aspx

## Exercises

1\. What does a class have?

Only the attributes of a system entity;

Only attributes or only methods of a system entity;

Only the methods of a system entity;

Attributes and methods of a system entity.

2\. Let's create the Account class within the initial project using Visual Studio.

In Visual Studio, right-click the project name and select Add >                          

Class ...

Inside the window opened by Visual Studio, we need to define what is the name of the class we want to create. Choose Account Name :

After entering the class name, click the Add button . With this, Visual Studio will create a new file within the Project, Conta.cs . All code in the Account class will be inside this file:

class Account

{

// The class code is in here!

}

Now declare the following attributes within the Account : balance (double), holder (string), and                                                                    

number (int).

3.Which of the following commands instantiates a new Account?  Account Account = Account ();

  Account Account = new Account ();

  Account Account = Account.new ();

4.Considering the code:

Account c = new Account ();

c.saldo = 1000.0;

Which of the following lines adds 200 reais to this balance?

balance + = 200;

c.saldo + = 200;

Account c.saldo + = 200;

Balance Account + = 200;

5.Now let's test the Account class we just created. Place a new button on the application form. Double-click this button to define which code will be executed at the button click.

private void button1_Click ( object sender, EventArgs e)

{

// button action here.  

}

Within the code of this button, instantiate a new Account and try some tests by filling in and showing its attributes through MessageBox.Show . For example:

private void button1_Click ( object sender, EventArgs e)

{

AccountVictor Account = new Account ();

accountVictor.titular = "victor" ;

AccountVictor.number = 1;

accountVictor.saldo = 100.0;

MessageBox.Show (accountVictor.titular);

}

Try testing with multiple accounts and see that each account instance has its own attributes.

6.Now let's implement methods in the Account class . We will start with the Deposit method , this method returns nothing and should receive a double argument that is the amount that will be deposited in the Account . Your class should look like this:

// inside Account.cs file

class Account

{

// declaration of attributes

public void Deposits ( double value)

{

// what to put here in the implementation?

}

}

After implementing the Deposit method , implement the Saca method as well . It also returns no value and receives a double which is the amount that will be withdrawn from the account.

7.Now let's test the methods we just created. In the button action that we use to test the account, we will manipulate the balance using the Deposit and Cashout methods :

private void button1_Click ( object sender, EventArgs e)

{

AccountVictor Account = new Account ();

accountVictor.titular = "victor" ;

AccountVictor.number = 1;

AccountVictor.Deposit (100);

.

MessageBox.Show ( "Balance:" + AccountVictor.saldo);

accountVictor.Saca (50.0);

MessageBox.Show ( "Balance:" + AccountVictor.saldo);

}

Try to make deposits and withdrawals in several different instances of Account , note that within the methods this variable has the reference value in which the method was invoked.

8\. What is the following code output:

Mauricio account = new Account ();

mauricio.saldo = 2000.0;

Account guilherme = new Account ();

guilherme.saldo = 5000.0;

mauricio.saldo - = 200.0;

guilherme.saldo + = 200.0;

MessageBox.Show ( "mauricio =" + mauricio.saldo);

MessageBox.Show ( "guilherme =" + guilherme.saldo);

mauricio = 2200.0 and guilherme = 4800.0

mauricio = 2200.0 and guilherme = 5200.0

mauricio = 1800.0 and guilherme = 5000.0

mauricio = 1800.0 and guilherme = 5200.0

9\. What is the following code output?

Mauricio account = new Account ();

mauricio.number = 1;

mauricio.titular = "Mauritius" ;

mauricio.saldo = 100.0;

Account mauricio2 = new Account ();

mauricio2.number = 1;

mauricio2.titular = "Mauritius" ;

mauricio2.saldo = 100.0;

if (mauricio == mauricio2)

{

MessageBox.Show ( "Accounts are the same" );

}

else

{

MessageBox.Show ( "Accounts are different" );

}

Bills are the same.

The accounts are different.

10\. What is the following code output:

Mauricio account = new Account ();

mauricio.saldo = 2000.0;

Copy account = mauricio;

copy.saldo = 3000.0;

MessageBox.show ( "mauricio =" + mauricio.saldo);

MessageBox.show ( "copy =" + copy.saldo);

mauricio = 2000.0 and copy = 3000.0

mauricio = 3000.0 and copy = 2000.0

mauricio = 2000.0 and copy = 2000.0

mauricio = 3000.0 and copy = 3000.0

11.(Optional) Implement the Transfer method that receives the transfer amount and the destination account. Have it reuse implementations of the Sack and Deposit methods .

12.(Optional) Let's add validation to   the  Account Drawout method  . Modify the Draw  method so that it does not withdraw if the current account balance is less than the amount

received as an argument.

13.(Optional) Modify the Validate Draw method to return true if the draw was successful and false otherwise. Then modify the account test button code to use the value returned by the Sack method to display a message to the user. If the withdrawal is successful, we want to show the message "Withdrawal successful", otherwise we will show "Insufficient Balance"

14.(Optional) Now change the Sack method of the Account class. Limit the withdrawal amount to $ 200 if the client is underage.

Remember that you still need to validate if the amount to be withdrawn is less than or equal to the customer's current balance and is greater than $ 0.00.

## Class Composition

When we open a bank account, we have to provide a lot of information: name, social security number, ID and address.

We have seen that when we want to store information in a class, we must create attributes. But in which class put these new attributes? Clearly this information does not belong to an Account . This data belongs to the account holder, ie this information belongs to the bank customer .

Then we must store them in a Customer class .

class Customer

{

public string name;

public string cpf;

public string rg;

public string address;

}

We also know that every account is associated with a customer, that is, the account holds a reference to the associated customer.

class Account

{

// other attributes of the public Account Holder Customer;   

// account behaviors  

}

Now, when we create an account, we can also place its holder.

Customer victor = new Customer ();

victor.name = "victor" ;

Account oneAccount = new Account ();

a AccountAccount = victor;

We also saw that the holder attribute holds a reference (arrow) to a Client instance (object in memory). Therefore, assigning an AccountAccount = victor is copying the reference from the victor variable to the holder attribute .

We may modify Customer's attributes by reference stored in the holder attribute.

the Account .

Customer victor = new Customer ();

victor.name = "victor" ;

Account oneAccount = new Account ();

a AccountAccount = victor;

aHeadAccount.rg = "12345678-9" ;

// Display the name victor MessageBox.Show (a.Account.name);   

// Display the text 12345678-9 MessageBox.Show (victor.rg);   

6.9 EXERCISES

1.Create the Client class containing the attributes name (string), rg (string), cpf (string) and address (string). Modify the Account class and make its holder attribute of type

Client instead of string .

Be careful. After this modification we will not be able to assign the customer name directly to the Account holder attribute . To define the name of the holder, we will need a code similar to the following:

Account Account = new Account ();

Client Client = new Client ();

holder.account = customer;

account.titular.name = "Victor" ;

2\. What output will be printed when executing the following code snippet?

Account oneAccount = new Account ();

Customer guilherme = new Customer ();

guilherme.name = "Guilherme Silveira" ;

oneAccount.table = guilherme;

MessageBox.Show (an account.holder.name);

Guilherme Silveira

A message box will appear without any message.

The code does not compile

3\. What output will be printed when executing the following code snippet?

Account oneAccount = new Account ();

Customer guilherme = new Customer ();

guilherme.rg = "12345678-9" ;

oneAccount.table = guilherme;

aHeadAccount.rg = "98765432-1" ;

MessageBox.Show (guilherme.rg);

98765432-1

12345678-9

rg

Nothing will print

4.(Optional) Create one more attribute in the Customer class that keeps the person's age. In our case, age is an integer.

Also create a behavior (method) with the name EhMajorDeath in the Client class that takes no arguments and returns a boolean indicating whether the client is of legal age or not. When is a person of legal age in Brazil?

## ENCAPSULATION AND ACCESS MODIFIERS

At this time, our Account class has a number , balance, and a holding customer , and behaviors that allow you to withdraw and deposit:

class Account

{

public int number;

public double balance;

public Owner;

public void Bag ( double value) {

this .saldo - = value;

}

public void Deposits ( double value) {

this .saldo + = value;

}

}

If we wish to withdraw or deposit to any Account , we will:

account.Saca (100.0);

deposit account (250.0);

But what happens if a team member does:

account.saldo = 100.0;

Nothing prevents us from accessing the attributes directly. In three distinct parts of our software we have such code:

// in a file account.saldo - = 100.0;   

// in another file account.saldo - = 250.0;   

// in another file account.saldo - = 371.0;   

Now imagine that the bank changes the withdrawal rule: now with each withdrawal the bank will charge 0.10 cents. That is, if the user withdraws 10.0 reais, it is necessary to withdraw from his account 10.10 reais. We have to change all points of our application that access this attribute! But our code base can

It is very large and it is very common to forget where and who is accessing this attribute, leaving bugs every time we forget to change somewhere. If we have this line spread 300 times in our system, we need to find all 300 lines and make the change. Very complicated and costly!

What would happen when we use the Saca () method :

// in an account file. Bag (100.0);   

// in another file account.Saca (250.0);   

// in another file account.Saca (371.0);   

How would we reflect the change in the 10-cent withdrawal rule? We only need to change the Saca () method once , instead of changing all lines that access the attribute directly!

Encapsulation

By releasing access to the attributes of the Account class , we are allowing any programmer to make their own unsafe implementation of the loot logic any way they want. If the modification of the attribute was restricted to the class that declares it, everyone who wanted to withdraw or deposit money in the account would have to do so by class methods. In this case, if the withdrawal rule changes in the future, we will only modify the Sack method.

In object orientation, hiding the implementation details of a class is a concept known as encapsulation. Because the implementation details of the class are hidden, all access must be done through its public methods. We don't let others know HOW the class does her job, showing only WHAT she does.

See the line Conta.Saca (100.0); . We know what this method does for its name. But how he does his job will only know if we get into his implementation. Therefore, the behavior is encapsulated in this method.

But we haven't solved the problem of preventing programmers from directly using the attribute yet. Anyone can still execute the code below:

account.saldo - = 371.0;

For this we need to hide the attribute. We want to keep it private so that only the Account class itself can use it. In this case we want to modify access to the attribute so that it is private, private:

class Account

{

// other attributes here

.

private double balance;

public void Bag ( double value) {

this .saldo - = value;

}

public void Deposits ( double value) {

this .saldo + = value;

}

}

Private attributes and methods are accessed only by the class itself. That is, the Saca () method , for example, can make changes to it. But other classes can't access it directly! The compiler does not allow it!

The attributes of a class are implementation details, so we will mark all account attributes with the word private:

class Account

{

private int number;

private double balance;

private Customer holder;

public void Bag ( double value) {

this .saldo - = value;

}

public void Deposits ( double value) {

this .saldo + = value;

}

}

Great. Now the programmer is forced to go through the methods to manipulate the balance . If we try, for example, to type in the Account balance from a form code, we will have a compilation error:

Account c = new Account ();

// The line below generates a compilation error c.saldo = 100.0;   

But now we have another problem. If we want to display the balance we will not be able to. The private blocks both the writing, the reading!

Controlling Access To Properties

We saw that we can prohibit external access to an attribute using C # private, but private also blocks the reading of the attribute, so to retrieve its value, we need a new method within the class that will return the current value of the attribute:

class Account

{

private double balance;

private int number;

// other account attributes and methods

public double PegaSaldo ()

{

return this .saldo;

}

}

Now to show the balance to the user, we would use the following code:

Account Account = new Account ();

// initialize the account

MessageBox.Show ( "balance:" + account. HandleSaldo ());

Also, the account needs a number, but as it has been declared private , we cannot access it directly. We'll need a new method to do this work:

class Account

{

private int number;

// other attributes and methods of the account public void PutsNumber ( int number)   

{

this .number = number;

}

}

To put the number on the account, we would have to execute this code:

Account Account = new Account ();

account.Place Number (1100);

// use account in code

Note that this allows us to control all access to the Account class , but to write or read the value of an attribute we need to use the methods. Ideally we should use a syntax similar to that of attribute access, but with the control that the method gives us. To solve this problem, C # gives us the properties.

The declaration of a property is similar to the declaration of a attribute, but we need to talk about what should be done in reading ( get ) and writing ( September ) property

class Account

{

private int number;

public int Number

{

get

{

// code to read property

}

set

{

// code to write in property

}

}

}

In reading the property, we want to return the value of the Account number attribute :

class Account

{

private int number;

public int Number

{

get

{

return this .number;

}

}

}

With this, we can read the Number property with the following code:

Account c = new Account ();

MessageBox.Show ( "number:" + c.Number);

Note that access was equal to attribute access, but when we try to read the value of a property we are actually executing a code block ( get property) of the Account class . To set the account number, we will use the code:

Account c = new Account ();

c.Number = 1;

When we try to write to a property, C # uses the set block to store its value. Within the set block , the value that has been assigned to the property is within a variable called value , so we can implement the set as follows:

class Account

{

private int number;

public int Number

{

// get statement  

set

{

this .number = value ;

}

}

}

We can also declare a property that has only get , without set . In this case, we are declaring a property that can be read but not writable. With properties we can completely control access to class attributes using the attribute access syntax.

## Simplifying Property Statement With Self-Implemented Properties

Using properties, we can control access to class information, but as we have seen, declaring a property is quite laborious. We need an attribute to store its value, and we need to declare get and set .

To make it easier to declare properties, starting with C # 3.0, we have properties that are automatically implemented by the compiler, the auto-implemented properties. To declare an auto-implemented property to expose the account number, we use the following code:

class Account

{

public int Number { get ; set ; }

}

This code causes the compiler to declare an attribute of type int (whose name is known only to the compiler) and generate the code for the Number property with a get and a set that read and write to the declared attribute. Note that by using auto-implemented properties, we can only access the value of the declared attribute through the property.

Every time we declare an auto-implemented property, we always need to declare a get and a set for the property, but we can control the visibility of both get and set .

For example, in the case of balance, we want to allow anyone to read the account balance, but only the account itself can change it. In this case, we use the following code:

class Account

{

// other properties  

// get is public and can be accessed by any class  

// set is private and therefore can only be used by the account. public double Balance { get ; private set ; }   

// rest of class code.  

}

Now let's look at code that tries to read and write in the properties we declare:

Account c = new Account ();

c.Number = 1; // it works because the number set is public

MessageBox.Show ( "number:" + c.Number); // works because Number get is public

c.Saldo = 100.0; // Balance set is private, so we have an error MessageBox.Show ( "balance" + c.Saldo); // works because Balance get is public.

Note that both by declaring properties explicitly and using auto-implemented properties, we have complete control over what information will be exposed by the class.

So we should use properties every time we want to expose some class information. We should never expose class attributes (using public ) because we never want to expose the implementation details of the class.

## Name Convention For Property

The naming convention defined for C # properties is the same naming convention used for classes, ie using Pascal Casing (all words in the name are concatenated and each word has an initial capital letter, for example: bank number => BankNumber )

## Exercises

1\. What is the behavior of the attribute below:

public int Number { get ; private set ; }

The number can be read, but cannot be changed by other classes.

The number cannot be read, but can be changed by other classes.

The number can neither be read nor changed by other classes.

The number can be read and changed by other classes.

2\. About the code below it is valid to state that ...

Account c = new Account ();

double valueDispose = 200.0;

c.Salde + = valueDispose;

The deposit operation has been implemented correctly.

The deposit operation is not encapsulated and may cause future maintenance problems.

The deposit operation is not encapsulated, making future code maintenance easier.

3.What is encapsulation?

  It's very clear to everyone how the class does its job.

  It is the use of Properties in any of its variations.

  It is manipulating and changing attributes directly, without going through a specific method.

It is hiding HOW the class / method does its task. If the rule changes, we have to change only one point of the code.

4\. What is the problem with the attribute below:

public double Balance { get ; set ; }

None. It is encapsulated, after all we use Properties.

Instead of public , we should use private .

The Balance attribute can be manipulated by other classes. This goes against the encapsulation rule. It's no use creating Properties and allowing all attributes to be modified by the other classes.

5.Turn the attributes of the Account class into properties. Allow the account balance to be read but not change outside the class, also change the code of the classes that use the account to access properties instead of attributes directly.

Conclusion

Thank you for making it through to the end of C#, let’s hope it was informative and able to provide you with all of the tools you need to achieve your goals whatever they may be.

All C# classes, be they part of the.NET Framework or redefined by you, go back to a common base class: System.Object.

Classes defined without a base class are automatically assigned System.Object as a direct base class; derived classes inherit System.Object over the last of their base classes.

But if all C# classes are directly or indirectly derived from System.Object, it means that they all inherited the methods and fields of System.Object. Reason enough to take a look at the public and protected elements of System.Object.

The derived class inherits all elements of its base class, with the exception of the constructors and the destructor. It can directly access the inherited public, internal, protected, and internal protected elements, not the private elements.

The derived class can obscure or overload inherited items. Covered elements continue to exist in the derived class and can be called using the keyword base.

In C#, all classes automatically inherit the elements of the System.Object class. This provides a basic functionality common to all C# objects (support for copying, comparing and converting to strings).

Classes can implement any number of interfaces as long as they provide the methods inherited from the interfaces with appropriate statement parts.

Finally, if you found this book useful in any way, a review on Amazon is always appreciated! 

# HACKING WITH KALI LINUX

The Ultimate Beginners Guide for Learning Kali Linux to Understand Wireless Network & Penetration Testing.

Including How to Get Started with Scripting and Security.

Andrew Sutherland

Copyright 2019 by Andrew Sutherland - All rights reserved.

This eBook is provided with the sole purpose of providing relevant information on a specific topic for which every reasonable effort has been made to ensure that it is both accurate and reasonable. Nevertheless, by purchasing this eBook you consent to the fact that the author, as well as the publisher, are in no way experts on the topics contained herein, regardless of any claims as such that may be made within. As such, any suggestions or recommendations that are made within are done so purely for entertainment value. It is recommended that you always consult a professional prior to undertaking any of the advice or techniques discussed within.

This is a legally binding declaration that is considered both valid and fair by both the Committee of Publishers Association and the American Bar Association and should be considered as legally binding within the United States.

The reproduction, transmission, and duplication of any of the content found herein, including any specific or extended information will be done as an illegal act regardless of the end form the information ultimately takes. This includes copied versions of the work both physical, digital and audio unless express consent of the Publisher is provided beforehand. Any additional rights reserved.

Furthermore, the information that can be found within the pages described forthwith shall be considered both accurate and truthful when it comes to the recounting of facts. As such, any use, correct or incorrect, of the provided information will render the Publisher free of responsibility as to the actions taken outside of their direct purview. Regardless, there are zero scenarios where the original author or the Publisher can be deemed liable in any fashion for any damages or hardships that may result from any of the information discussed herein.

Additionally, the information in the following pages is intended only for informational purposes and should thus be thought of as universal. As befitting its nature, it is presented without assurance regarding its prolonged validity or interim quality. Trademarks that are mentioned are done without written consent and can in no way be considered an endorsement from the trademark holder.

# Introduction

Congratulations on downloading Hacking with Kali Linux: The Ultimate Beginners Guide for Learning Kali Linux to Understand Wireless Network & Penetration Testing, Including How to Getting Started with Scripting and Security, and thank you for doing so. The book covers the numerous tools in Kali Linux that you can use for performing penetration tests. You will also be able to learn the operations of the various utilities in this Debian distribution. To use this book effectively, you will require a prior knowledge of basic Linux administration, computer networking, and the command utilities, albeit on a minimum. This will help you to comprehend the various subjects that have been covered in this book.

You will get to know how hackers are able to gain access to your systems and the methods they use to steal information. Furthermore, you will also learn the countermeasures required to safeguard yourself against the numerous hacking techniques. This book covers topics that include Kali Linux, carrying out vulnerability assessments, hacking wireless networks, penetration testing, web security, text manipulation, encryptions, file systems, social engineering, and some basics on Python scripting you will need to know as an aspiring hacker.

By the time you flip the last page of this book, you will have mastered concepts that are both theoretical and practical on the basic techniques that you require to become a hacker. You will have the techniques needed for penetration of computer networks, computer applications alongside computer systems. Let me say that we have numerous books that cover this topic, but you have decided to pick this one up. Many thanks for that. No efforts have been left to ensure that the content in this book is relevant and refreshing to you. Have fun reading!

# 
Chapter 1: An Introduction to Kali Linux

## An Overview of Kali Linux

Kali is a distribution of the Linux family, which is established upon the Debian architecture and was purposely designed and made for auditing of security and carrying out Penetration Testing at an advanced level. This distribution has hundreds of tools geared towards numerous security-related tasks such as forensics tasks, security research, testing by penetration of various security systems, and reverse engineering, among many others. Kali has been developed and is managed by Offensive Security, an information security company specializing in training security solutions. Kali evolved from BackTrack. BackTrack was also a software of the Linux distribution family and was also utilized in penetration testing.

### Reasons Why Linux is Preferred by Hackers

As part of our introduction, we are going to discuss five reasons why the Linux operating a preferred choice for hackers.

a) It is an open-source software

Unlike the Windows operating system software, Linux distribution is open-source. A Linux user has access to the operating systems’ source code. This means that one can manipulate and change a Linux operating system to suit their needs at will. Supposing the user wants to make a particular system operate in ways besides those it was originally intended to, the ability to manipulate and change the source code is of paramount importance.

b) The operating system is transparent

A thorough understanding of a users’ operating system is required for one to carry out hacking effectively. It is also necessary to have a knowledge of the operating system one intends to hack. Unlike Windows, we are able to see and even manipulate all the working parts of Linux. That is to say, Linux is completely transparent. It is not easy to understand the inner workings of a Windows operating system. The transparency aspect means working with Linux is more effective.

c) Linux distributions provides users with granular control

A Linux user has infinite control over the system; in other words, it is granular. This is significant when compared to a Windows operating system where a user is able to control only what Microsoft allows them to. Everything in Linux, both at the minuscule and macro level, is controlled by the terminal. Additionally, scripting is simple and effective for any scripting language in Linux.

d) Hacking resources are designed for Linux

A majority of tools used in hacking are specifically written for Linux. There are some, like nmap or Metasploit, that can be available for the Windows platform but, still, not all their capabilities can be ported to Windows. They offer limited functionalities as compared to when they are on the Linux platform.

e) The future belongs to Linux/Unix

Over the years, you may have witnessed that Windows is slowing down and even stagnating in some departments. Since the advent of the internet, Linux/Unix has and is still the choice operating system for web servers primarily because of its reliability, robustness, and stability. To date, almost two-thirds of web servers utilize Linux operating systems. Examples of uses of the Linux kernel are Citrix applications, Vmware, embedded systems in switches and routers, mobile devices, and so on. It has been said that the future of computing is with mobile devices, such as phones and tablets. Android, which is used in most phones, is Linux, while iOS is a Unix kernel. It is, therefore, difficult to see how the future is not Linux/Unix. Microsoft Windows commands a meager market share of around 7 percent. The rest of the market is either Linux or Unix. In summary, the future lies with Linux/Unix.

### Using Kali Linux

This operating system, Kali Linux, was purposely meant for testing the security of a computer infrastructure so as to unearth vulnerabilities that require addressing. The following are the main steps in carrying out penetration testing on a computer network. The tools that can be used in the respective steps have also been included.

1) Reconnaissance

First and foremost, any penetration testing begins with intelligence gathering. In this stage, preliminary information about a particular target is collected. This information is what will be used in the planning of the actual attack.

Examples of tools for reconnaissance in Kali Linux include Nmap, DNSRecon, Hping3, Recon-ng, among others.

2) Scanning

The second step is to scan for more intel about the target under consideration. A vulnerability scanner is employed at this step to help a penetration tester discover security loopholes that may be present in the target network.

Tools that can be used for this purpose include Nikto, Cisco-auditing-tool, WebSploit, jSQL Injection, Arp-scan, and Oscanner.

3) Gaining access

Gaining access to a targeted network is the third step. Here, an ethical hacker will make an attempt to infiltrate a network. The intention is to enable the hacker to extract vital data with which they can use to compromise a system or use it as a platform to launch more attacks. Tools necessary  for this include John the Ripper, Browser Exploitation Framework (BeEF), Metasploit Framework, Aircrack-ng and Wireshark.

4) Maintaining access

A tester is required to maintain access to a system he or she has gained access to. This is to enable them to cause more destruction for as long as possible.To accomplish this task, stealthy tools capable of under-the-ground operations are necessary. Some of the tools include Dns2tcp, Webshells, Powersploit, Cryptcat, and Weevely.

5) Covering tracks

Here, a penetration tester will try to erase any signs or footprints of past malicious activity that has been carried out on the target network. A good example is returning original statuses of access privileges that had been escalated or altered. Kali Linux has the following tools for covering tracks: Smbexec, Meterpreter, and Veil.

## Introduction to Penetration Testing

Still on the introduction to Kali Linux, we are going to introduce penetration testing. This will give us the required background to enable us to understand its importance with regards to security analysis. Penetration testing is a valuable tool that helps security planners get to understand and improve the security of a computer or network they are managing. Nevertheless, a hacker can use penetration testing to exploit weaknesses in the system then afterward attack them and steal valuable information. A security professional is able to use penetration testing better when he or she understands why it is needed in the first place, and also when the processes and issues surrounding it are well understood. We shall look at the terms of its use, its applications, and the various processes involved. The book is not intended to be a step by step guide on how to carry out penetration testing. This is a skill that requires a lot of practical practice to master. If it is not done correctly, it can actually damage the targeted, or the results can be deemed invalid in some cases.

### What is Penetration Testing?

We define it as an agreed set of procedures and processes that are used for bypassing laid down security controls of an intended or known system or organization purposely to test the said system’s or organization’s resistance capabilities against such attacks. Penetration testing is normally carried out to unearth weaknesses in the security of a system and also to find out the ways in which a systems’ security architecture can be breached by a potential attacker. Often, a penetration test comprises of a sequence of attacks against a select target. The outcome of the penetration test, successful or otherwise, is determined by the reaction of the targets to the attacks.

The determination of the ability of a target to resist or withstand an attack launched by a hostile intruder is the overall intention of carrying out this test.

Consequently, the pen-tester will utilize techniques and tricks that an actual attacker is likely to use. In other words, the tester will simulate a real-life attack against his target. This way, the tester can unearth the weak spots and improve its security way before a malicious attacker discovers them. Organizations are turning to penetration testing to help them ascertain the effectiveness of the measures they have in place to safeguard their security. During the testing process, problems might be discovered regarding the organization’s security. Nevertheless, the pen-tester is required to elaborate on the ‘enabling factors’ that resulted in the success of the test. It is not sufficient enough for a tester to simply state that they were able to lay their hands on an organizations’ sensitive data. The onus is on the tester to give reasons why there was a lapse that enabled them to achieve their intended tasks.

A penetration test has the following basic requirements:

1) Like any other task, a penetration test needs to have a clearly defined goal or objective, which is to be documented clearly. A more specific goal makes it easier to determine whether the test was a success or failure. For instance:

Goal 1: Gain access to ABC’s corporate network

Goal 2: Gain access to ABC’s corporate network through the internet and access the sales departments’ file server.

Goal 1 is not precise, even though it is attainable. Goal 2 is precise and specific. This is what we are talking about.

Every test being done requires its individual goal. If a pen-tester intends to carry out testing of more than one aspect of security in an organization, multiple other tests need to be performed. This makes it possible for a tester to easily distinguish attempts that are successful from those that are not.

2) The penetration test is time-bound. It should be performed within a limited time period exactly as it would happen in the real world. Any real-life attacker would give up after unsuccessfully trying to penetrate a site. Additionally, the protected information being sought has a finite useful lifetime. Any penetration test needs to acknowledge this. Therefore, the goal of the test must include the time limits within which the test will be carried out based on the type of the target under consideration, the lifetime of useful information, and the level of threat that is expected.

3) The management of an organization should approve the penetration test. Since this activity will involve accessing an organizations' network and information systems, it must be authorized by the management.

### Terms Used in Penetration Testing

Let us look at the commonly used terms associated with penetration testing.

Throughout this book, we are going to use them often. They are:

*   Tester: This is the entity carrying out the penetration test. It can either be a person or a group. It is a tester that plans and carries out the penetration test.

*   Attacker: This is an original version of a penetration tester. The differentiating factor is that while testers intend to help improve the security of a company, an attackers' intention is malicious, i.e., to steal a company's' resources or information.

*   Attack: we can say these are the attempts a hacker or a penetration tester makes to help them bypass a targets’ security controls. The sequence of an attack, in most cases, has methods that are electronic, physical, or procedural.

*   Management: This is an organizations’ leadership. The testing process can include numerous levels of management, especially those controlling specific areas. The management levels involved will have an impact with regards to the scope of the test.

*   The Test Subject: This can either be a small organizational unit within a company or the entire company upon whom the penetration test will be performed.

*   The target:  the target is the organization or system being subjected to an attack.  It can be aware of the test being done on it or not. Either way, most targets have their own safeguard mechanisms with which they can defend themselves.

### Is Penetration Testing Necessary?

First and foremost, a penetration test helps a given organization ascertain the effectiveness of the laid down security protocols. The protocols can be operational, technical, or of a physical nature. A tester's job will be to determine whether these controls are up to the task by trying to overcome them. A penetration tester will also be gauging an organization’s vulnerability to a specific threat. As a tester, the most crucial role is to find out how an organizations' countermeasures are effective and inform them about areas that need improvement. Also, an organization can identify threats against itself, and it is up to the tester to validate or invalidate the threats.

Often, companies use a penetration test to bolster their image to their target market. Here, a company can indicate that it was able to withstand attacks and as such, is secure and has a robust infrastructure. This testing can also alert an organizations' management about a potential security threat existing within its operations or systems. A penetration test that is well-executed can uncover vulnerabilities systematically. The management can be unaware of the existence of these vulnerabilities.

### Types of Penetration Testing

The first type examines the physical infrastructure of a subject. A tester can exploit the physical security of an organization. In most cases, the problems do not lie in the databases and other configurations, but the physical countermeasures in place. Questions to ask here include is there adequate access control? Does the building housing the organization have security guards? Are they well trained? Is checking of sensitive materials conducted when employees exit the building? Are electronic devices registered and verified on entry and exit of the building? To answer these questions, a tester will attempt to walk into the building at a time when people are arriving to work, say in the morning. Suppose an intruder can gain access to a company's building without being checked, they will be in a position to obtain the information they are after.

The second type of penetration testing is concerned with the operational aspects of an organization. Operational testing ascertains the effectiveness of laid down procedures of operation in the organization through circumventing those procedures. This is unlike physical testing, which only checks the physical access to networks, facilities, or company computers.

The third and final type deals with electronic testing. In this testing mechanism, a tester will attack a company's' networks, communications facilities, or computer systems. Electronic testing can be accomplished by using automated tools, or it can also be done manually. Here, the main objective is to decipher vulnerabilities to an attack by way of communications facilities and data networks that are being used by the subject under consideration.

# Chapter 2: Vulnerability Assessment

## Introduction to Vulnerability Assessment

To begin, let us ask ourselves these questions. How are your computing assets safeguarded against attacks? Are they able to withstand the attacks, and to what extent? For us to answer these questions satisfactorily, we need to determine the weak links in the organizations’ security chain so that we are then able to prepare adequate countermeasures. A vulnerability assessment helps in the description, identification, and classification of security vulnerabilities or gaps within a given communications infrastructure or network.

Kali Linux comes in handy when matters dealing with vulnerability assessment are concerned. This is through the impressive array of analysis tools that are packaged with it. Through these tools, a penetration tester is able to discover any vulnerability in a target network. This means that all the tools we may ever need for carrying out security testing will be present in Kali Linux. The only problem with this is that, with all these capabilities, this distribution may overwhelm an unfamiliar user. Through this book, entry-level and intermediate-level security engineers alongside specialists and analysts will get to learn how to utilize Kali Linux in the identification of vulnerabilities in an operating system, an organization’s web, and the infrastructure housing databases.

We perform a vulnerability mapping to help us unearth security flaws that can lead to compromising of a system. The term “vulnerability mapping” is sometimes used interchangeably with “vulnerability assessment.” This is the next step a penetration tester or a malicious hacker takes after having performed an adequate gathering and an enumeration of information. We are going to have a look at a number of tools availed to us by the Kali Linux Operating System, that can help us discover vulnerabilities in a computing environment. As we have pointed out before, the vulnerabilities may likely lead to compromising systems resulting in a real hacker or the tester to violate the integrity, availability, and confidentiality of the systems.

### Types of Vulnerabilities

We can categorize vulnerabilities into three clearly distinct classes. These classes include

1) Design vulnerabilities: This class of vulnerabilities is as a result of weaknesses arising from specifications of the software being used in a given system. They are the most difficult to resolve as they normally require the application of software patches as per the security requirements recommended by the pen-tester.

2) Implementation vulnerabilities: These vulnerabilities usually result from glitches within the running software code. Once a software glitch is unearthed, it is classified here.

3) Operational vulnerabilities: Vulnerabilities falling under this class are often as a result of the improper deployment and configuration of the various application software.

The above-mentioned vulnerabilities occur either locally or remotely in the extents of the environment of the targets. Vulnerabilities that are local in nature need that a tester has physical access to the system of a target so as to exploit. On the other hand, vulnerabilities occurring remotely do not require physical access to the target system for exploitation  to be carried out.

### Vulnerability Taxonomy

With the daily increases in technology, the number of vulnerabilities has also gone up. To keep track of all that, we need a system of categorizing them. There have been significant efforts to build a taxonomy that will help us categorize vulnerabilities that are common. It is a daunting task as you can see, International organizations agreed to the standards below. I am going to provide links to each of the vulnerability databases below:

a) Google hacking database – https://www.exploit-db.com/google-hacking-database/

b) Enumeration of common weakness -  this can be found here: http://cwe.mitre.org/data/index.html

c) Database for National vulnerability – [https://nvd.nist.gov/vuln](https://nvd.nist.gov/vuln) 

d) WASC threat classification – http://projects.webappsec.org/w/page/13246978/Threat%20Classification

e) OWASP – https://www.owasp.org/index.php/

Any hacking enthusiast should be able to access the above sites to acquire more insights on vulnerabilities.

### Using Kali Linux to Do Vulnerability Scanning

A penetration tester favorite toolkit is Kali Linux, since it comes with prepackaged tools that can be used for numerous tasks. Among these tools, we have those that can be utilized to conduct a vulnerability mapping exercise.

### Scanning Vulnerabilities on Web Applications

Every day, new applications designed for the web are cropping up. Most of these programs have been coded without any regard to the due process. Disregarding secure coding principles results in applications that are vulnerable in numerous ways. With the tools below, a pen-tester is able to expose vulnerabilities falling within the documentation listed above.

1\. Nikto2

Designed based on LibWhisker2, this is a fairly straightforward web application vulnerability scanner. It has a number of enhanced capabilities as such. It can support SSL for instance; it can also be deployed across several platforms, we can also use it to do management of authentication of hosts and manage evasion of IDS.

2\. OWASP ZAP

That is for OWASP Zed Attack Proxy. This proxy tool is an open-source web application that provides to its user crucial capabilities that include web app vulnerability scanning.

3\. Nessus

If you want a web application vulnerability scanning tool that is automated, Nessus is it. It is fairly quick and easy to use and can really come in handy when a quick vulnerability assessment is needed within a short time. 

Scanning Network Vulnerability

We also have tools for scanning network devices that are inbuilt in Kali Linux. These tools can be used to scan switches, databases, routers, and protocols like SMB. These tools are endless, but we are only going to describe those that are commonly used.

1\. CISCO Analysis

We have a number of CISCO devices that possess vulnerabilities that we can use a couple of tools to reveal. Kali Linux is bundled with the Cisco Auditing Tool that can help us do an audit of the routers. This utility helps a penetration tester or an attacker to map vulnerabilities that range from community strings in SNMP, default credentials all the way to old CISCO bugs.

2\. Analysis of  SNMP

To prepare attacks that target a particular host, pen-testers and attackers normally use a Simple Network Management Protocol (SNMP) protocol to obtain information from hosts.

### Assessment of Databases in Kali Linux

Kali Linux makes it possible for a tester or hacker to assess vulnerabilities in Microsoft’s MSSQL, MySQL, and Oracle databases. Here, the vulnerabilities that can be looked out for include SQL injection, default password checks, and password policy tests.

SQLMap

SQL injection tests against databases can be carried out using the SQLMap utility. Examples of applicable databases include MySQL, PostgreSQL, MSSQL, and Oracle. Besides the detection of flaws that have been discovered, SQLMap is able to exploit them, thereby making both tester and hackers prefer it for its comprehensiveness. Attacks like SQL injection for UNION query, Stacked query, Inferential blind SQL injection, and Time-based blind SQL injection would have been time-consuming and laborious were it not for this tool.

Summary

You will now be able to proceed onto the next phase, which would ordinarily be exploitation after using the tools above to unearthed vulnerabilities. There are some cases whereby only an enumeration of vulnerabilities is required; the utilities above will be able to carry out the task sufficiently.

# Chapter 3: Wireless Network Hacking

## Introduction to Wireless Network Hacking

Wireless networks are nowadays a common feature everywhere. They provide a way to connect to the Internet for home users, at workplaces, and also in public places so that users are able to access resources online and carry out business.

They have simplified businesses and made life much easier, generally speaking. This, however, has brought along with it some security-related risks. Hackers have been able to break into companies, government institutions and banks through their Wi-Fi networks. There has been a notable increase in the number of attacks in recent times, and this has necessitated network security managers to make wireless networks more secure, reliable, and robust. Kali Linux can be used to crack wireless networks and as such, is an important tool for testing wireless networks against attacks.

### Understanding and Inspecting Wireless Networks

The ability to scan for and connect to other network devices from your device is crucial to becoming a successful hacker. Discovering and manipulating Wi-Fi and Bluetooth connections is an essential skill. If a hacker can get access to a wireless connection, they can gain entry to a device and access to confidential information. The initial step, however, is to learn how to find these devices.

### Wi-Fi Networks

We shall begin with Wi-Fi. First of all, let us look at the basic Wi-Fi terminologies you will encounter in the book.

Extended SSID - this is almost similar to Service set identifier (SSID) but can be used for multiple APs in a wireless LAN.

Basic service set identifier (BSSID) - this is the specific tool that identifies each AP, and it is the same as the MAC address of the device.

Service set identifier (SSID) - this is simply the proper name of the network.

Power - the closer you are to the Wi-Fi Access Point, the higher the power, and the easier the connection is to crack.

Access Point (AP) - wireless users connect to an Access Point when accessing the internet.

Security - this is the security protocol used on the Wi-Fi Access Point that is being read from. There are three primary security protocols for Wi-Fi. Wired Equivalent Privacy (WEP), Wi-Fi Protected Access (WPA), and WPA2PSK.

Modes – we have three modes in which Wi-Fi can operate: managed, master, or monitor.

## Basic Wireless Commands

### ifconfig

To perform a network interface configuration in Unix-based operating systems, one needs ifconfig. It is an administration utility that is found in the system. More specifically, ifconfig is an interface tool that is used to make the system scripts of numerous operating systems available to you.

The utility possesses tools used that are used to configure, query, and control TCP/IP interface parameters. It was a part of the BSD TCP/IP suite, appearing as 4.2BSD. Ifconfig is commonly used for many reasons, including assigning the IP address and netmask of each network interface, and further, enabling and disabling an interface when appropriate. There are plenty of operating systems similar to Unix that initialize their unique network interfaces with shell scripts that require ifconfig. Overall, the ifconfig is an interactive tool that is useful to system administrators in particular because they can routinely use it to analyze network interface parameters.

Additionally, ifconfig is often used to alter the media access control (MAC) address of a network interface. For this process to occur, one must first disable the interface (set down) using the ifconfig command. Next, one must enter the following MAC command to change it:

ifconfig wlan0 down

ifconfig wlan0 hw ether 13:11:20:33:49:66

ifconfig wlan0 up

In summary, ifconfig does the following:

*   Enables viewing of all network settings.
*   It displays information for any network interface
*   View network settings of a specific network interface
*   Disabling and enabling interfaces for the networks
*   Allocating IP Addresses to the interfaces
*   Netmask assigning to a network interface
*   Broadcast allocation to network interfaces
*   MTU changing for interfaces
*   Enabling promiscuous mode and disabling it
*   Alias addition and removal
*   Network interface MAC address changing

### iwevent

This command displays Wireless Events, which have been accepted by the socket known as RTNetlink. Specific Wireless Events are shown on each line. These events explain the happenings on a specified wireless interface. It does not accept  any arguments.

### iwspy

iwspy is a basic wireless command that can monitor a specific list of nodes and assess the link quality of each individual node. iwspy provides information that is identical to the information provided by /proc/net/wireless. This command also gathers noise level and signal strength. Therefore, each individual address within the list adds overhead to the driver. It is important to keep in mind that this function only works for nodes that comprise the wireless cell you are associated with; you will be unable to monitor any access points that you are not currently associated with (you can just utilize scanning for this purpose), along with lists of nodes in any other cells. In most cases, when one is using managed mode, packets will be relayed by the access point. In this particular case, you will receive the access point’s signal strength. These reasons highlight why this functionality is almost always used in ad hoc and master mode.

### iwlist

This command can be used for scanning wireless networks available and also to display any other information about the wireless networks which iwconfig cannot present to you. This basic command is useful because it provides one with a carefully curated list of nearby wireless access points along with their MAC addresses and SSIDs.

### ifrename

This command is used for renaming wireless network interfaces depending on multiple criteria that are static to allocate names consistently to each and every interface.

Every network adapter receives whichever name is available first (eth0, eth1…). This is because network interface names are, by nature, constantly changing. The order in which network interfaces are presented, however, may vary. Recently, ifrename has updated to grant users the ability to choose what they want to name a network interface. Additionally, it also contains a tool that can select an interface name that coordinates with the network interfaces currently on the system. The interface’s MAC address is most often the selector used by ifrename. Note that ifrename needs to be run before interfaces come into play, which helps to explain why it’s primary use is with different scripts (init, hotplug) but is rarely operated by the user themselves. ifrename gives network adaptors new names using mappings available in /etc/iftab.

### iwgetid

This is used in the reporting of the NWID, ESSID, or address of the access point of the wireless network currently in use. iwgetid will automatically display the ESSID of each device. When situations arise in which the ESSID is unavailable, it will output its NWID in lieu of it. The information provided is identical to the information reported by iwconfig. By comparison, it is easier and more efficient to complete integration in various scripts.

## Wi-Fi Recon with Aircrack-ng

One thing new hackers always want to try is cracking Wi-Fi access points. As mentioned, before you attack a Wi-Fi AP, you need the MAC address of the target AP, the client, and the channel the AP is operating on. We can get all that information plus more using the tools of the aircrack-ng suite. To use these tools effectively, you need first to put your wireless network card into a monitor mode so that the card is able to can view a hundred percent of the traffic that is passing its way. A network card captures traffic intended only for its normal occasions. On wired network cards, the monitor mode resembles the promiscuous mode. Using the airmon-ng command from the aircrack-ng suite puts your wireless network card to the monitoring mode.

## Detecting and Connecting to Bluetooth

In recent times, nearly all gadgets, systems, and devices have inbuilt Bluetooth. The devices can be computers, iPods, smartphones,  speakers, game controllers, keyboards, tablets, among others. The ability to break into Bluetooth networks can result in the compromising of the information on the device, assuming a devices’ control and acquisition of a platform to transmit privileges information from and to the device, among other things. We, therefore, need to understand how Bluetooth works if we are to exploit this technology. From this book, you will be able to acquire some basic knowledge that will come in handy during the scanning and connecting to Bluetooth devices in preparation for hacking them.

### How Bluetooth Works

First, we can define Bluetooth as a wireless communication technology that enables devices to wirelessly send voice or data over a relatively short distance. This technology was meant to replace the ubiquitous cables that were being used to connect devices while still securing the communications across them. The process of connecting together two Bluetooth devices is known as pairing. Pretty much any two devices can pair if they are set to a discoverable mode. In the discoverable mode, a particular Bluetooth device will broadcast the following information about themselves:

*   Technical information
*   Name
*   List of services
*   Class

Upon pairing, two Bluetooth devices will exchange a link key. The devices will store the key to be used in the identification of the other device in future pairings. Every device has a unique identifier and usually a manufacturer-assigned name. These will be useful pieces of data when we want to identify and access a device.

### Bluetooth Scanning and Reconnaissance

Linux has an implementation of the Bluetooth protocol stack called BlueZ that we’ll use to scan for Bluetooth signals. Most Linux distributions, including Kali Linux, have it as an inbuilt feature by default. BlueZ possesses utilities that can help us scan and manage Bluetooth capable devices. Examples of the aforementioned utilities are outlined below:

*   hciconfig; this is an equivalent of ifconfig in Linux, but made for Bluetooth capable devices.
*   hcitool; this is a tool that we use to perform inquiries. The inquiries can be the device ID, name, class, or even its clock information. This helps the devices to work in sync.
*   hcidump; sniffing of Bluetooth communications is carried out by this tool; therefore, gives us a chance to capture data that is being sent over the Bluetooth signal.

The first scanning and reconnaissance step with Bluetooth is to check whether the Bluetooth adapter on the system we’re using is recognized and enabled so we can use it to scan for other devices.

## The Implementation of Wireless Testing Methodology

### Wireless Penetration Testing Approach

Let us look at some approaches to carrying out penetration tests on wireless networks. An unsecured wireless network can be cracked by using a sniffing and a password combination technique. To be able to do this easily, the set up can be made fully automated or semi-automated. Here are three points to take note of:

*   Wireless Penetration testing is used for the evaluation of the risks associated with access to a wireless network.

*   Wireless access points offer easy gateways for hackers to infiltrate a given network that is internal.

*   Remediation and reinforcement of a network against vulnerabilities are possible after a Penetration test or a Wireless .

We are going to see the important steps that characterize wireless penetration testing herein this book:

### Process of Penetration Testing

1.  Lab Setup:

First, we are going to require the following:

A Laptop/computer with Kali Linux installed: the operating system can be downloaded free of charge from [https://www.kali.org/downloads/](https://www.kali.org/downloads/)

Be sure to get a version that is compatible with your computer.

Wireless card: when it comes to wireless testing, this is the most significant aspect. The card must be supported by the operating system installed on your computer. You can use an external wireless card in the event that your card is not supported. Here, a USB Wireless card with packet sniffing and packet injection capability is required.

Password list: a password list can be defined as a key that hackers and penetration testers use in wireless network cracking. A Passphrase is what a network uses for its encryption. Sometimes, a Passphrase is known as a network security key, otherwise known as a pre-shared key. Chances of accessing a wireless network increase when we have a password repository, which is comprehensive. This is a very important point to take note of.

We have a number of options which include

*   We can utilize, from the repository, a list file of passwords.
*   Downloading password list files from Google. Here we can get an updated list.
*   We have simple or complex password lists and dictionaries that we can also use.

First, we need to understand different types of encryption protocols, wireless penetration testing tools, how to change the MAC addresses, and the processes behind WLAN discovery before analysis of the wireless encryption strength.

2.  Tools required for wireless penetration testing:

Wireless toolkit for a semi-automated attack.

Tools for discovering wireless networks: ministumbler, Wi-Fi hopper, airfart, karma, wirelessmon, wellenreiter, apradar, aerosol, kismet, netstumbler, aphopper among others

Tool for capturing packets: these include Cain, Wireshark, airtraf, Airopeek and apsniff

WPA/WEP password tools: wzcook, airsnort, wep attack, Aircrack-ng, Airbase , Aircrack-ptw, cowpatty, wep crack

Tools for Frame generation: Commview, fake AP, Airgobbler, airsnarf, airpwn

Wireless toolkit for a fully automated wireless attack

In an automated attack, we can use Fern, Wi-Fi honey, and a utility for auditing wireless networks called Wifite

3.  Wireless networks encryption protocols

Below are three protocols that are used for information protection in wireless networks. The protection is from an access point to a system.

a) WEP: this is an abbreviation for Wired Equivalent Privacy. In wireless networks, this was the protocol of encryption that was developed first. WEP was purposely meant to improve the security of WLANs. The intention here was to match a wireless network security to that of wired networks. A key concern with wireless networks is privacy. A crucial drawback with this encryption protocol was that hashing was not done for the keys. The key was also linked to the Initialization Vector. A very major shortcoming there. The bottom layers of the reference OSI model (those are the data link and the physical layer) use this type of encryption. WEP does not give users an end-to-end security. This encryption protocol has plenty of weaknesses and is technically outdated. Ciphers created by WEP are easy to break into as they are crypto logically weak.

b) WPA: This is an abbreviation for Wi-Fi protected Access. This encryption protocol is an improvement on WEP. It utilizes a TKIP which is Temporal Key Integrity Protocol in full. The TKIP keeps changing keys with every message integrity check and data packet. It is also used to protect the capturing, modification and the resending of data packets so as to ascertain if the packet has been modified or not. It employs the use of EAP (Extensible Authentication Protocol) for user authentication. This is due to the fact that the authentication in WEP is executed by using the MAC address that can be sniffed easily. WPA is known to be vulnerable against a  Timing or Dictionary Attack.

c) WPA2: It is WPA  with some enhanced capabilities. Currently, it is among the commonly used encryption security protocols. This encryption protocol employs the use of what we call an advanced encryption standard, often abbreviated as AES. This is quite secure when compared to the temporal key integrity protocol. It is capable of supporting ad-hoc networks. Its predecessor, WPA, is constrained only to infrastructure networks. Normally, people wrongly think that AES is crack-proof. That is not true. As long as the password is simple, any encryption protocol can be broken into. That is to say an encryption protocol is as good as the password in use. WPA2 can be further categorized into two:

*   WPA2-PSK: This protocol was solely designed for tiny networks. For instance, networks serving a single home.

*   WPA2-ENT: This encryption protocol was created to serve enterprise entities. Compared to WPA2-PSK, we can say that it is a significantly secure network since the passphrase that is used in the encryption is not stored locally.

4.  Client and Access Points Briefly

We need to know how a client interacts with an access point before we even think of cracking a wireless network. As you will see in this book, the first thing we are supposed to do is to turn on the device that has a wireless card. The reason is to make it possible to carry out sniffing of the communications. Wireshark is used  for this task. To do this, it should be set to promiscuous mode. This way, every packet being transmitted will be captured.

5.  Wireless Attacks

We are going to study two techniques for cracking wireless networks. These approaches are  fully automated and semi-automated. Let us begin with the latter, shall we?

### The Semi-automated Technique

1.  Starting up the interface: turning on the wireless interface is the initial step of cracking any wireless network.

2.  Changing of the MAC address: This maneuver helps a hacker or a malicious user conceal their identity in the process of crack a wireless network. A hacker can use the command known as MAC changer to modify MAC Addresses of their devices.

3.  Create monitor (mon0) interface: You must put the wireless card into monitor mode.

4.  Detect available wireless networks:  in order to search available wireless networks, a hacker can execute the command “airodump-ng” so that they are able to discover a potential victim.

5.  Choose a target network: From the available wireless networks, select a victim. Remember the specific channel where a wireless network you have selected is running. Similarly, keep a note of its MAC address.

6.  Capture packets from the target: Once a hacker has made a choice regarding which wireless network to attack, they will initiate packet capturing.

7.  De-authentication attack: This is whereby a targets’ connection to the access point is terminated until an attacker sends a de-authentication packet. This will force the target to reconnect, thereby enabling the capturing of ARP packets.

8.  Circumventing the wireless key: By using aircrack-ng, the captured password file can be run against a password file the hacker has in their possession. The “captureddata” is the name of the password file captured from the target.

9.  Accessing and compromising vital information: A hacker/malicious user is able to sniff information that is critical to an organization. This is possible upon obtaining of the passphrase. Examples of critical information that can be accessed include passwords, usernames, and session IDs. These credentials can be used to carry out further compromise attacks within the entire wireless network.

### Fully-Automated Technique

When it comes to cracking networks that are wireless, the fully automated technique is, without doubt, the best approach. This method uses the Fern Wi-Fi cracker that is able to crack various encryption protocols such as WPA2, WPA, and WEP. This wireless hacking utility makes use of the command line to break into these networks. Fern has a straight forward graphical interface through which an attacker can choose the various parameters and where the output will also be displayed. The process is automatic. Session hijacking and geo-location of computers using Mac address is an additional functionality of Fern.

Once the python script has been ran, Fern will open its graphical interface. At this point, all a hacker needs to do is choose a wireless interface and thereafter, click on the scan button to obtain the access point. After scanning and picking a network to attack, hit the attack button to initiate. The rest of the procedure will be taken care of by the software. After Fern captures the handshake, a brute force will commence. Simple and straightforward. The discovered WPA key will be displayed in red if it lies within the password list that is being used.

6.  Wireless Network Threats

Currently, we have many types of attacks on wireless networks capable of affecting the Availability, Integrity, and Confidentiality of any organizations’ IT infrastructure.

AD-HOC network: A malicious user is able to connect to your ad hoc network, thereby gaining access to sensitive files. This is, by far, the most straightforward attack a hacker can carry out.

Mirror image access point: As the name implies, a malicious user can make a fake access point that resembles a legitimate one. Through this access point, they are able to get a victim’s information upon connection to it by the victim. The fake access point will broadcast a stronger signal as compared to the real access point. Any wireless network user will definitely connect to a signal that is strong.

Wireless sniffing: We can say that sniffing attacks are one of the most dangerous that can be carried out in a wireless network. Through sniffing, a malicious user will be able to get packets during the transmission process. That will give them an avenue to view comprehensive details within the selected network. Suppose traffic being sent is not encrypted, an attacker will be able to access a packets full details.

Buffer overflow: in this attack strategy, a malicious user is able to take advantage of the vulnerabilities that are present in a particular code of software. to gain escalated privileges on a target machine.

Virus/Worm/Spyware: Malicious code that exploits system vulnerabilities to gain privileged access or to manipulate data.

Software capable of remote control: Using this type of software, a malicious user is able to take over and control target machines that are remote so as to compromise the network.

Spoofing/ARP redirection: a malicious user can be able to reroute your wireless network traffic to their system by carrying out a spoofing attack on you rsystem. Sometimes, we call this type of attack MAC spoofing.

Denial of service attack: this is a de-authentication attack. The attack normally disconnects targeted clients from an AP until when a de-authentication packet is sent. What this attack does is that it will unlink a particular wireless service with the intended effect of making the resource unavailable.

7.  Securing wireless networks

Wireless network managers can adopt the following so that they are able to defend networks from malicious attacks.

Changing the default settings: the default settings that come with your infrastructure need to be changed; they include the passwords that come by default, weak algorithms, and encryption keys.

Use a strong encryption algorithm: It is in your best interest to utilize a strong algorithm for your encryption. For example, it can be a mix of minimum of eight alphabetical characters plus at least two upper and lower case characters and a special character.

Place access point devices at secure locations: When deciding where to locate access point devices, you need to place it such that it can be accessed by the majority of your users. It should also give a strong signal strength to them. Security wise, it should not “leak” or extend far out from its intended point of use.

Authentication Verification: It is recommended to verify the legitimacy or authenticity of any users prior to giving them access. One solution that has proved to be the best is the implementation of a Remote Authentication Dial-In User Service (RADIUS) server for authenticating the user.

SSID Security: Broadcasting SSID makes everything simple for a potential wireless network attacker.

Logging: By using logging, an organization is able to easily footprint the pattern of attack.

Access Point update: To be able to mitigate existing vulnerability in a previous version of a given software, it is advisable to carry out routine updates of the access point software. This will undoubtedly lower the likelihood of attacks.

Wireless Audit: this is an evaluation meant to check the security strength of a given wireless network. Results of the auditing may include security policy gaps, presence of devices that are unauthorized on the network, and so on.

Guest access security: If possible, organizations can give their guest users a separate access point or perform authentication on them before allowing them to use their main network.

Security awareness: This is an important aspect to be considered when securing a wireless network. The responsibility of informing, educating, and sensitizing employees of an organization lies with the organization itself. The employees should understand the impact of wireless network security so that the security will begin with themselves.

Wireless IDS/IPS: This can be implemented using a configuration that is secure to enable monitoring of the traffic. In case of any suspicious behavior, an alert can be generated. This system can also be used to manage wireless devices and in case any of them goes missing, it should be able to give a report.

### The Best Wireless Hacking Resources

The following wireless hacking tools can be used for testing our own personal wireless networks for potential security threats. Let’s begin straight away.

Aircrack-ng

This is one of the most commonly used tools for WEP/WPA/WPA2 cracking. The Aircrack-ng resource is used to identify and catch handshakes and packets. It is also used to de-authenticate clients connected to the network, and get all of the necessary materials to perform brute force and dictionary attacks. The aircrack-ng suite includes, among others, the utilities listed below:

*   Airodump-ng that is used to capture packets
*   Airbase-ng which is a utility used for configuring access points which are fake
*   Aircrack-ng for wireless password cracking
*   Aireplay-ng to generate traffic and client de-authentication

Aicrack-ng suite comes as a standard in Kali Linux. To be able to use this tool,  your Wi-Fi card needs to be capable of packet injection.

PixieWPS

This is a new tool that targets known WPS vulnerabilities. This tool is programmed using C and is utilized in brute-forcing the WPS PIN offline by exploiting the extremely low or, sometimes, non-existing entropy of vulnerable access points. This is referred to as a pixie dust attack. For it to work, it requires an altered version of Wifite or Reaver to work with.

Wifite

This is a Wi-Fi attack tool that is automated and is used for attacking wireless networks which are encrypted with WEP/WPA/WPA2 and WPS.

Wireshark

This is, in my opinion, the best network protocol analyzer tool out there. With Wireshark, one is able to analyze a network comprehensively. It can be used to carry out live packet capturing, careful inspection of protocols, and browse and filter packets across platforms.

Reaver

This tool targets Wi-Fi Protected Setup registrar PINs and attacks them to gain access to the passphrases. Since many router manufacturers and ISPs turn on WPS by default, a lot of routers are vulnerable to this attack out of the box. In order to properly use Reaver, you need to ensure that you have a strong signal strength to the wireless router together with the correct configuration.

oclHashcat

oclHashcat is not included with Kali Linux and is not a dedicated Wi-Fi hacking tool; however, it has the ability to perform brute force and dictionary attacks on handshakes that have been captured very quickly when using a GPU. After you have utilized Aircrack-ng suite or any other tool to capture the WPA handshake, you can successfully crack it with oclHashcat using your GPU.

Crunch

Crunch can be utilized for dictionary-based attacks. It can also be directly linked to other tools, such as Aircrack-ng. This capability saves a great deal of time as you do not have to wait until it generates an extensive password list before you are able to use them.

Macchanger

Macchanger is an essential tool that can be used to spoof your MAC address to a random MAC address. Spoofing your MAC address for Wi-Fi hacking might be necessary to avoid MAC filters or to mask your identity on a wireless network.

Fern Wi-Fi Cracker

This is a wireless security auditing and attack tool written in Python. Fern can crack and recover WEP, WPA, and WPS keys and contains tools to successfully complete MiTM attacks. Fern Wi-Fi Cracker runs on any Linux distribution, which includes the prerequisites. Fern Wi-Fi Cracker is included with Kali Linux.

Wash

We can use this tool to check if a particular access point has enabled WPS or not. It can also check if an access point has locked up the WPS mechanism after an attempt has been made by Reaver. This is because Many APs' normally lock themselves up after experiencing a brute force attack. The utility is bundled together with the Reaver package that we have said comes as a standard tool in Kali Linux.

# Chapter 4: Analyzing and Managing Networks

## Introduction to Analyzing and Managing Networks

Understanding networking is crucial for any aspiring hacker. In many situations, you’ll be hacking something over a network, and a good hacker needs to know how to connect to and interact with that network. For example, you may need to connect to a computer with your Internet Protocol address hidden from view, or you may need to redirect a target’s Domain Name System queries to your system. These kinds of tasks are relatively simple but require a little Linux network knowhow. This chapter shows you some essential Linux tools for analyzing and managing networks during your network hacking adventures.

### Analyzing Networks with IFCONFIG

The ifconfig command is one of the most basic tools for examining and interacting with active network interfaces. You can use it to query your active network connections by simply entering ifconfig in the terminal.

### Checking Wireless Network Devices with IWCONFIG

If you have a wireless adapter, you can use the iwconfig command to gather crucial information for wireless hacking, such as the adapter’s IP address, its MAC address, what mode it’s in, and more. The information you can glean from this command is particularly important when you’re using wireless hacking tools like aircrack-ng.

### Changing Your Network Information

Being able to change your IP address and other network information is a useful skill because it will help you access other networks while appearing as a trusted device on those networks. For example, in a denial of service (DoS) attack, you can spoof your IP so that that the attack appears to come from another source, thus helping you evade IP capture during forensic analysis. This is a relatively simple task in Linux, and it’s done with the ifconfig command.

### Changing Your IP Address

To change your IP address, enter ifconfig followed by the interface you want to reassign, and the new IP address you want to be assigned to that interface. For instance, if you wanted to assign the IP address 192.168.181.115 to interface eth0, you would enter the following:

kali >ifconfig eth0 192.168.181.115

kali >

When you do this correctly, Linux will return the command prompt and say nothing. Then, when you again check your network connections with ifconfig, you should see that your IP address has changed to the new IP address you just assigned.

### Changing Your Network Mask and Broadcast Address

You can also change your network mask and broadcast address with the ifconfig command. For instance, if you want to assign an eth0 interface, say 101.172.101.14 a netmask of 14.14.0.0 plus a broadcast address of 191.152.10.189, you would enter the following:

kali >ifconfig eth0 101.172.101.14 netmask 14.14.0.0 broadcast 191.152.10.189

kali >

If you’ve done everything correctly, Linux responds with a new command prompt. Now enter ifconfig again to verify that each of the parameters has been changed accordingly.

### MAC Address Spoofing

It is possible to utilize ifconfig for changing your MAC address (or HWaddr). The MAC address is globally unique and is often used as a security measure to keep hackers out of networks —or to trace them. Changing your MAC address to spoof a different MAC address is almost trivial and neutralizes those security measures. Thus, it’s a very useful technique for bypassing network access controls.

To spoof your MAC address, simply use the ifconfig command’s down option to take down the interface (eth0 in this case). Then enter the ifconfig command followed by the interface name (hw for hardware, ether for Ethernet) and the new spoofed MAC address. Finally, bring the interface back up with the up option for the change to take place.

### Assigning New IP Addresses from the DHCP Server

Linux has a Dynamic Host Configuration Protocol server that runs a daemon— a process that runs in the background—called dhcpd, or the dhcp daemon. The DHCP server assigns IP addresses to all the systems on the subnet and keeps log files of which IP address is allocated to which machine at any one time. This makes it a great resource for forensic analysts to trace hackers after an attack. For that reason, it’s useful to understand how the DHCP server works. Usually, to connect to the internet from a LAN, you must have a DHCP assigned IP. Therefore, after setting a static IP address, you must return and get a new DHCP assigned IP address. To do this, you can always reboot your system, but I’ll show you how to retrieve a new DHCP without having to shut your system down and restart it. To request an IP address from DHCP, simply call the DHCP server with the command dhclient followed by the interface you want the address assigned to. Different Linux distributions use different DHCP clients, but Kali is built on Debian, which uses dhclient. Therefore, you can assign a new address like this:

kali >dhclient eth0

### Manipulating the Domain Name System

Hackers can find a treasure trove of information on a target in its Domain Name

System (DNS). Although the design of DNS is to translate domain names to IP addresses, a hacker can use it to garner information on the target.

### Examining DNS with Dig

DNS is the service that translates a domain name like Google.com to the Appropriate IP address. This way, your system knows how to get to it. Without DNS, we would be required to memorize multiple IP addresses of our favorite websites. One of the most useful commands for the aspiring hacker is dig, which offers a way to gather DNS information about a target domain. This information may include the targets’ nameserver IP address, email server alongside any IP addresses and subdomains.

### Changing Your DNS Server

In some cases, you may want to use another DNS server. To do so, you’ll edit a plaintext file named /etc/resolv.conf on the system. Open that file in a text editor—I’m using Leafpad. Then, on your command line, enter the precise name of your editor, followed by the location of the file and the filename.

### Mapping Your Own IP Addresses

A special file on your system called the hosts file also performs domain name–IP

address translation. The hosts file is located at /etc/hosts, and kind of as with DNS, you can use it to specify your own IP address–domain name mapping. In other words, you can determine which IP address your browser goes to when you enter www.microsoft.com (or any other domain) into the browser, rather than let the DNS server decide. As a hacker, this can be useful for hijacking a TCP connection on your local area network to direct traffic to a malicious web server with a tool such as dnsspoof. By default, the hosts file contains only a mapping for your localhost, at 127.0.0.1, and your system’s hostname (in this case, Kali, at 127.0.1.1). But you can add any IP address mapped to any domain you’d like.

# Chapter 5: Penetration Testing and Web Security

## Penetration Testing

As organizations become increasingly security conscious and the cost of security

breaches rises exponentially, many large organizations are beginning to contract out security services. One of these key security services is penetration testing. A

penetration test is essentially a legal, commissioned hack to demonstrate the

vulnerability of a firm’s network and systems. Generally, organizations conduct a vulnerability assessment first to find potential vulnerabilities in their network, operating systems, and services. I emphasize potential, as this vulnerability scan includes a significant number of false positives (things identified as vulnerabilities that really are not). It is the role of the penetration tester to

attempt to hack, or penetrate, these vulnerabilities. Only then can the organization know whether the vulnerability is real and decide to invest time and money to close the vulnerability.

### Importance of Conducting a Penetration Test

A penetration, as a proactive security measure, will enable you to do the following:

1.  Enables unearthing loopholes before malicious users do

One good method of knowing how good your security is by carrying out hacking against it. Let us put it in a way that is easy to comprehend. Hacking attempts originating from an external source gives you an ability to test your systems’ resistance in a safe manner. That is because the procedure mimics what a potential malicious fellow would do. That can be exploiting vulnerabilities resulting from incorrect settings, operational weaknesses, software bugs, mistakes in the code, and even errors in service configuration. A penetration test, unlike the real hacking experience, is carried out in a controlled and safe fashion. It is an exact simulation of a hacking attack that is actual.

Through it, the likely harm that can result from malicious hacking exercise can be brought to light. A company that intends to conduct this testing normally sets the rules of the game beforehand. More often than not, organizations perform penetration tests immediately upon deployment of applications and infrastructure or sometimes after performing alterations to critical infrastructure. Penetration testing will, therefore, aid in the identification and validation of possible security-related loopholes in their networks way before hackers can exploit them.

2.  Reducing network downtime while saving remediation costs

Recovering from a breach in security is not an easy thing to do. It is an expensive and messy process that can have astounding cost implications. The costs are as a result of regulatory fines, investments on programs to protect customers and, in extereme circumstances, a total loss of business. Therefore, it means that substantial investments and a comprehensive measure intended to restore security have to be carried out to get everything back up and running. Security procedures for restoration may take plenty of time. Consequently, it will be a proactive solution to use a penetration test to identify threats to your system and how to prevent them. This is because losses resulting from cyber attacks are not only financial but reputational. In view of this, it is prudent that you carry out a penetration test once or twice a year on the lower level. Analysts dealing with professional security will be in a position to give you sound advice regarding the frequency of performing penetration tests on your IT infrastructure and business domain. They are also able to counsel you about investments and necessary procedures required for making your IT infrastructure attack-proof.

3.  Lay Down Security Measures that are efficient

A penetration test report gives comprehensive results that you may use to carry out an assessment of your organizations’ security level. Through the report, top management will get insightful information pertaining to IT security and even get to understand their potential impact on the infrastructures’ performance and general functioning. The report comes with recommendations and remedial measures that can be used in the development of reliable and cyber-secure systems.

4.  Facilitate Compliance with Regulation policies on Security

As we have noted, penetration testing is paramount when it comes to safeguarding your valuable IT assets from potential attacks. The benefits of penetration testing are not just confined to the security aspects. Leading standards, sucha as ISO 27001 and PCI, require that there is compliance to security standards. Normally, heavy fines come with noncompliance. No organizations would want to get penalized for nonadherence.

Some of these standards require that organizations carry out penetration tests regularly. Also to be done on a routine basis is security audits. Professional security analysts can help with this. The policy regulations also stipulate that organizations dealing with transactions in large volumes need to carry out annual and regular penetration testing, especially after a reconfiguration of the system. A comprehensive penetration test report is able to prompt organizations to upgrade their security layouts, and this will ultimately be used to denote due diligence to assessors.

5.  Company Image Preservation and Customer Loyalty

A company can boast of having systems that can withstand hacking attempts after conducting a penetration test. This can be a marketing point to its target customers that their transactions with the company and all other interactions are secure from any form of compromise. This can help a company’s reputation. Such tests also help to keep expensive security breaches at bay. Reputation and customer loyalty go hand in hand.

This means that it is only penetration testing that can assess a company’s resistance to cyber-attacks. It can give managers insights on the effects of a malicious attack on their IT infrastructure. Besides helping them streamline their priorities, a penetration test also helps an organization comply with relevant standards and policy frameworks. In the event that some vulnerabilities are uncovered, a company will be able to make investments in the relevant department.

### Stages of Penetration Testing

1\. Reconnaissance and Planning

In penetration testing, we start by planning and carrying out a reconnaissance. Here, the following are done:

*   The goals and the scope of the test is defined. The systems that will be tested addressed together with the testing methods that will be employed are clearly stated.
*   Intelligence gathering is carried out so that a tester is able to better comprehend how the target under consideration works and also to discover any inherent vulnerabilities.

2\. Scanning

After intelligence gathering, the tester will want to know how a target responds to the numerous attempts intrusion. To do this, a tester can use:

*   Dynamic analysis – This is when an application’s code is inspected while it is in a running state. We can see that this is a far more practical method of performing a scan since there is a real-time inspection of the performance of the applications.

*   Static analysis – A penetration tester will do an inspection of an application’s code so as to approximate its behavior when it is running. An entirety of the code can be scanned in a single pass using these tools.

3\. Obtaining Access

After getting to know a targets’ flaws and weaknesses, it will be time to exploit them. Exploits can either include intercepting traffic, escalating privileges, or even stealing data. All this is to get to know the repercussions of the damages that can be caused.

4\. Access Maintainance

A testers’ objective is to determine whether the vulnerabilities that they found are able to help them achieve a persistent presence in the exploited system. By maintaining access to a system, an attacker is able to gain in-depth access. The idea here is to simulate advanced persistent threats. These type of threats often remains in an organizations’ system for a long time in order for them to steal sensitive data from an organization.

5\. Analyzing the results

After completion of the penetration testing exercise, a tester shall be required to make a report detailing the following aspects of the test:

*   The vulnerabilities that were specifically exploited
*   Any critical information that was able to be accessed
*   Time it took to detect the penetration tester in the system.

It is this report that will be used by top-level management to lay down security strategies for their organizations and also configure countermeasures against such types of intrusions. From this report, patches and security solutions  to mitigate the vulnerabilities will be developed.

### Methods Penetration Testing

Internal testing

Here, a penetration tester having access to applications will attempt to simulate an attack as if it were being done by a malicious user from inside the organization. This simulation may represent an attack whereby a malicious user steals legitimate credentials by way of a phishing attack.

External testing

This type of penetration test is used for targeting resources of a company over the internet; an example can be the company website, the web application itself, emails together with domain name servers. The objective, as you may now know, is to access the above-mentioned systems and carry out an extraction of valuable data.

Targeted testing

Here, the security personnel and tester work together. They also update each other on their actions and movements. This method gives the security managers valuable insights in real-time, as seen from the viewpoint of the hacker.

Blind testing

A tester, in this case, is only given the name of a target organization. This provides a chance to the managers of security a sneak peek of the actual attack that will happen.

Double-blind testing

As in the blind testing above, the personnel in charge of security in an organization will not have prior knowledge of the attack that will be simulated. This type of attack is closest to real-world attacks and in such a case, they will not be given time to beef up their safeguard mechanisms before a breach happens.

Web Security

Just like physical stores, homes, government locations, web applications alongside websites are also susceptible to their security arrangements and protocols being circumvented. What is needed to counter cyber-crimes and the compromising of web applications is robust and reliable security measures.

Web security does this exactly. A functional definition of web security for us can be that it is a set of protocols and protection measures employed in the safeguarding of your website together with your web applications against hacking and against unsanctioned access by personnel who are not authorized. Web services, websites, and web applications can be protected by the integral division of Information Security. This provides the crucial security for anything that is carried out on the internet.

Normally, there exist multiple considerations that are involved when we are dealing with web protection and/or web security. For an application on the web or a website to be said to be secure, it has to be backed up by a variety of techniques and checkpoints to guarantee its security. We have standards of security that need to be adhered to at all times. OWASP is responsible for the highlighting and implementation  of these standards. Web developers who have plenty of experienced normally adhere to OWASP standards and also keenly study the Web Hacking Incident Database to be able to know vulnerabilities that lead to websites being hacked and how they are hacked.

Common website security threats

Websites can be attacked in more than one way. Before proceeding, we need to understand some common threats to website security. These are what we shall be looking to avoid and be prepared for during the planning of security measures. Some of these include Spam, Viruses and malware, WHOIS domain registration, and DDoS attacks, among many others.

How to safeguard your website

After getting to know common security threats, let us now focus on how we can prevent them. The assumption that your website is secure is not correct. As long as you have not instituted any safeguard mechanisms, there is a high chance that it can be attacked. Here are a number of steps you are required to effect to better the security of your website.

*   Restrict file uploads

It is risky to let visitors on your website upload files. The uploads may contain a script meant to exploit vulnerabilities present on your website. All uploads need to be treated as a threat to the security of the website.

*   Use HTTPS protocol

This tells the visitors of a given website that essentially, they are dealing with a proper server. This translates to “no one can intercept the interactions they are having or the content they are viewing.”

*   Secure your personal computer

Security starts with you! It is important that you take care of the security of your devices. Hackers can use your PC as a gateway to your website. Ensure that you have an antivirus software that is updated with the latest definitions. This will protect you from many malicious attacks including from file downloads. It is also possible to inject malware to the websites through stolen FTP login credentials. It is important that you frequently scan your devices for malware and viruses regularly.

*   Change your default CMS settings

We have seen that numerous attacks are normally automated these days. Malicious users do program bots to help them locate sites still using their default settings. Make it hard for them. Upon installation of a CMS you own, modify the settings which are still on default mode:

 Settings required for comments

 Controls that users require

 Information visibility

 Permissions for files

Above are settings you are able to change right away.

*   Software updates

All the software has to stay up to date. This includes the CMS, plugins, Word Press software, among many others. The updates bring improved functionality, security patches to cover vulnerabilities, fixes for bugs and software glitches, and so on.

*   Select a web hosting plan that is safe

Web hosting plans that are shared have higher chances of getting compromised. In as much as they are appealing to users due to the potential cost savings, the levels of protection are reduced. As such, they are not a secure option. Remember, cheap is expensive!

*   Limit access to users

Errors caused by human beings account for the majority of cyber-security attacks. Reducing or limiting the humans can contribute greatly to error reduction. It is not a must for every employee to access your website. Guests, web designers and consultants likewise, do not deserve automatic access. The least privilege principle needs to be implemented to secure your website.

*   Do a password change 

Pass word changing is a significant shot in the arm for web security. So, change your password. Changing the password alone is even not enough; make it a habit to change it often.

*   Monitor your security

You can get utilities that can help you monitor your websites’ security online. Such utilities can help you with conducting security audits that can help to expose potential vulnerabilities. In so doing, you are able to launch countermeasures before an attack happens.

*   Make a backup for your website

It is said that when you have been forewarned, you should forearm yourself. It is good to always be prepared for the worse. In this case, the worst that can happen is your website getting compromised. A backup ensures you are at peace since there will be no data that is lost in the event of a compromise.

# Chapter 6: Text Manipulation and Bash Scripting

## Text Manipulation

As we have seen before, almost everything in Linux is a file, text files to be precise. A good example is that all the configuration files in Linux are text files. For one to carry out a reconfiguration of an application in Linux, all they need to do is open the configuration file, modify the text, re-save, and then restart the application, and just like that, the reconfiguration will be applied. Manipulation of text becomes of essence in managing Linux applications, given the numerous text files. Let us look at a number of commands and techniques that are used to manipulating texts in Linux. I am going to use files from Snort for demonstration purposes.

### Step 1: Cat Command

Cat is the most basic text display command. Let us cat the Snort config file that is normally found in /etc/snort.

 kali > cat /etc/snort/snort.conf

From above, you can see that snort.conf is displayed on our screen until it comes to the end of the file. Definitely, that is not a convenient method to work with the file.

### Step 2: Use the Head Command

We can use the head command supposing we just want to view the beginning of a file. By default, this command displays a files’ beginning 10 lines.

kali > head /etc/snort/snort.conf

In cases where we want to view more or fewer lines, we can use the “- switch” between the command and the file name.

kali > head -15 /etc/snort/snort.conf

Here, only the first 15 lines of snort.conf will be displayed.

### Step 3: Tail Command

Just like the head command, we can see the last lines of a file by using this command. The syntax of the command is as below:

kali > tail -20 /etc/snort/snort.conf

### Step 4: Numbering the Lines

With long files, it may be desirable to display them with line numbers. snort.conf, for instance, has  over 600 lines. Numbering makes it a lot easier for referencing changes, and also, it is easy to come back to the same place within a file. To show a file with a line number, we type:

kali > nl  /etc/snort/snort.conf

Each line will now have a number making referencing much easier.

### Step 5: Grep Command

Grep is a filtering command; that is, it gives us a chance to filter the content of a file for display. Grep is an essential and powerful command for working in Linux since it can minimize wastage of time spent in searching for every occurrence of a word or command.

### Step 6: Sed Command

This command enables us to look up for occurrences of a word or text pattern and then work on it. The name is a contraction of two words, stream and editor. Simply put, sed works in the same way as the find and replace function in Windows.

### Step 7: Less and More Commands

Like we have previously said, cat is a good utility command. However, it has a number of shortcomings where the display of large files is involved. Remember us saying cat is not very convenient?

More came first and is the utility that manual pages use. Let's open snort.conf with more command.

kali > more /etc/snort/snort.conf

You will see that more displays only the first page and displays for us in the lower-left corner how much of the file is being shown. Less is similar to more, although it possesses some additional functionality. To open snort.conf with less, type the following:

kali > less /etc/snort/snort.conf

You will see near the bottom left of the screen that less has highlighted the path to the file.

## Bash Scripting

A bash script can be described  as a file consisting of plain text having a sequence of commands. The commands include those that we can type normally into the command line on our own and those we generally wouldn't type. Take note of this: Any command that is able to be executed normally from the Kali Linux terminal may be placed in the bash script. The reverse is also true. Nothing needs changing. The commands just need to be typed normally, and they will behave as they are supposed to. Let me put it this way, suppose you are familiar with the Kali command line, you will be able to carry out bash scripting as they are almost similar. Normally, an extension of .sh is affixed to all the scripts in Bash. This is, however, not necessary as the Linux system is extensionless. A script can just work fine without this feature.

### How Do These Scripts Work?

If you have been interacting with computers generally, you appreciate that we have things we call programs and others that we call processes. We all agree that a program comprises a sequence of instructions made for the computers central processing unit combined into a package and usually stored on the computer’s hard disk.

When a program runs, what is actually running is its copy. This copy is referred to as a process. What is being done here is that the instructions alongside other relevant resources are being copied to the RAM (that is, the working memory) form the hard disk. Also, a temporary storage space in the RAM is allocated for temporary data and flags that will be used by the operating system to track and manage the process as it executes.

In normal circumstances, we have several processes that represent a single program running in the computers’ memory all at the same time. Upon their completion, the system will destroy them so that we will not have any more processes for the program. At the terminal, we will have a running Bash process to provide us with the Bash shell.

### How Does the Bash Script Run?

This is quite easy. First, running a script is also known as executing a script.

We have to set permissions to execute scripts. These permissions for safety reasons are by default, not set. Skipping this step will only display an error message, but the code can still run. Let’s look at a sample script below.

1\. #!/bin/bash

2\. # This is an example of a Bash script, by Sutherland

3.

4\. echo Welcome to Kali Linux!

We are going to expound a little bit on what is going on here below:

*   Line no. 1 – That as what we call the shebang.
*   Line no. 2 - This is a comment. Anything after # is not executed.
*   Line no. 4 – This is the command known as echo. It will print a message onto the screen. On Line no. 2, you will see that it is highlighted. Highlighting of the syntax only serves to make it easy to read. You probably do not need it in your own files.

### What is the Purpose of ./ ?

For normal commands, all we need to do is type the name and voila! It starts to execute. To run a bash script, we place ./ in front of it. Bash will attempt to find the name you have typed on the command line without ./ in directories that are located in a variable called $PATH. Separation of the directories is done using " : " This script will perform a search in those particular directories and will not look at your current directory or other subdirectories.

Bash will run the first instance of the script or program that it finds after searching the directories mentioned above. It is prudent to note that the $PATH variable varies with each individual user, and they can set it up to their preference.

Below are the reasons that this is done:

1.  This way, we can install a number of different versions of a particular program. We are also able to determine which of them gets executed depending on their location in $PATH.

2.  It offers unprecedented convenience. From the lengthy explanation above, the bin directory is found on the home directory. A user is in a position to place their own programs and installed scripts in there. A user is also able to utilize them regardless of their location within the system just by doing a simple name typing. It is also possible to make scripts with a similar name as a program in case you desire to have a behavior that is slightly different.

3.  The overall safety is increased – look at this, a malicious user may make a script intended to delete everything from the home directory. It is in your best interest not to execute that script. As long as the script is not in your $PATH no problems will arise.

You are also able to tell bash where to find a program script suppose it does not lie in any of the directories in your $PATH. This can be done by including a relative or an absolute path in front of the script name or program. Do not forget that the dot ( . ) refers to the current directory you are in. Supposing the script is situated in the home directory,  you can execute it through the use of an absolute path.

### The Shebang (#!)

From the script above, we can see that this is found in the first line.

The character sequence of hash and exclamation mark ( #! ) is what is called the Shebang. What follows the shebang is a path to the program or interpreter, which does the execution of the remainder of the text file. It is essential that we get the formatting right here. Shebang must be placed at the files’ very first line. Let me repeat, the #! Has to be inserted at line 1 of the file. One other thing to pay attention to is that there should be no spaces between the sign # , the mark ! and the interpreter path. It is unwise to also omit the shebang since the Bash shell will make an assumption that it is a Bash script. This means that it will work only by the assumption that the script is being run in a Bash shell, which is not entirely true. That is a very dangerous scenario.

### Bash Scripts Formatting

Formatting is an important area of bash scripting. It is required in many areas to enable proper functioning of the scripts. An absence or presence of a space between commands can make it either work or refuse to work. It is paramount that you familiarize yourself with this issue in your coding exercise. This type of scripting was purposely designed to act as an interface through which users are able to interact with the system. Later on, the capabilities of bash as a scripting tool continued to become advanced. The improvements were initially made based on user needs, then the scripting capabilities were worked around the various user needs. I know it can be annoying for a finely written piece of code to fail. Another formatting requirement is the indentation of code. You may already know by now that it is not required for a given code to run but, its role is to ensure readability of the code. It also makes it easier to keep the simple mistakes at bay.

# Chapter 7: Cracking Encryptions & Attacking with Frame Networks

## Cracking Encryptions

Kali Linux was solely designed to be a hacker’s or security professional’s best tool. We have seen that Kali comes packed with multiple tools and programs not always available on other operating systems. One reason Kali Linux has become so popular is its ability to break wireless encryption standards that are used in securing wireless devices. An example of a wireless device is the router. An attacker can use Kali to break into wireless systems, therefore gaining themselves full access of the network. The consequences of being hacked are much more damaging in a professional setting than in any other setting. Let us have a step-by-step look at how you can break WPA and WPA2 by utilizing  Kali Linux.

### What is Needed

Make sure you have the following items together before you begin:

*   A computer with Kali Linux installed
*   A wireless router configured to use WPA2
*   A wireless card that has the capacity to run smoothly in monitor mode
*   The aircrack-ng software

### The Attack Process

Note that it would be in your best interest to have root privileges on the Kali user account you are using to perform the attack. Otherwise, you may have to resort to using the sudo command, which is typically very tedious.

Step 1

Ensure that your network card is visible in Kali by using the ifconfig command. If you are using a wireless card via USB, make sure that it is plugged in.

Step 2

Ensure that your computer is not currently connected to a wireless network. Then you will need to run the airmon-ng command from the terminal. This command will display all of your wireless interfaces that are capable of running in monitor mode.

Step 3

Now you need to actually start using airmon-ng on your wireless interface. After you have completed this step, the output in the lower-right corner of the terminal should display the listening wireless interface that will likely be named mon0.

Step 4

Next, you will need to run the dump command with the listening wireless interface as a parameter. This will show you any information obtained from wireless networks in range of your wireless card such as the encryption type, the MAC address of the wireless device (BSSID), and other information such as the channel and model number of the wireless device.

Step 5

Find the wireless network that you want to crack and copy its BSSID. Thereafter, the information obtained from airodump-ng command will be required to be plugged into the command, which is used for starting the procedure of attack. The command we will need to use is as follows:

airodump-ng -c [wireless channel] –bssid [BSSID] -w /root/Desktop/ [monitor interface]

Remember that the monitoring interface, as we have said before, is likely to be mon0.

Step 6

At this step, your wireless interface will be gathering and storing information about the wireless network, but in order for the attack to succeed, we will need a host to connect to the wireless network. When a device successfully connects to the wireless router, our Kali software will step in and obtain data regarding a four-way handshake that is identified as the weak point in the protocol. Alternatively, you can use a de-authorization command. This command will curate a few de-authorization packets to send to the target wireless router to force the reconnection process for other devices. We will target a device to force to reconnect by using the client’s BSSID in a command. The only requirement is that you already need to be able to see a connected client’s BSSID in the previous command’s output.

Step 7

Ensure that you don’t close the terminal that you started running the airodump-ng command. Then, start a second terminal and using this command:

aireplay-ng –0 2 –a [Router-BSSID] –c [Client-BSSID] mon0

Step 8

You should now view the output that displays the indication of a successful handshake. If you don’t, however, there are a multitude of factors that could have caused it to fail. One common problem is that the wireless signal was too weak, in which case you would only need to move your computer closer towards the wireless router. In addition, the connected device may not be configured to automatically reconnect to the network. If that’s the case, then you will have to wait for them to reconnect.

Step 9

Upon a successful reconnection handshake, we are going to need to crack the protocol. Enter the following command, and plug in the parameters as they pertain to your configuration:

aircrack-ng -a2 -b [Router-BSSID] -w [Wordlist-File] /root/Desktop/*.cap

The only new parameter in this command is a wordlist we have not yet discussed. Essentially, a wordlist is recognize as a file comprised of many combinations of characters that will be used to complete the attack. You can find them online for free, just make sure you remember where you store the data on your computer and use the file’s path as a parameter in the preceding command. Once the command has been properly entered, the process of cracking the wireless encryption will be initiated by the softward

Step 10

All that is needed is to wait for the software to break the key. Note that in order to successfully break the encryption, the Wi-Fi password needs to be contained in the wordlist. This is called a dictionary-based attack, which is a little different from a brute force attack. A dictionary-based attack simply tries all of the passwords in a list or database, whereas an attack of brute force fashion will attempt to utilize all the possible character combinations. If your dictionary failed to find the correct password, you could try using an additional wordlist. Also note that it could take a long time to actually break the password, depending on the strength and complexity of the password as well as how fast your computer hardware is.

Step 11

Once the software successfully cracks the password, it will display the key near the middle of the terminal in a line that reads:

KEY FOUND! [ wireless key ]

Go ahead and try logging in with the key for fun.

Finally…

Breaking WPA and WPA2 encryption is pretty easy as far as security attacks are concerned. But please remember to use this information responsibly as the consequences could be terribly severe.

### Attacking with Frame Networks

This is the attack type that is also called a de-authentication DoS Attack. Here, the attacker saturates vast amounts of frames in the network that carries out de-authentication. Targets will get disconnected from a wireless network when they receive de-authentication frames. The network users will not be able to maintain a connection if the attack is prolonged. An attacker has the ability to launch a de-authentication DoS attack in multiple different ways. Commonly used methods include

*   The attacker can create spoofed de-authentication frames and set the source MAC address as the victim. This is done by setting the MAC address and destination MAC address as the AP’s MAC address. Therefore, the AP believes that a real user wants to exit the network, and what follows is the disconnection of the particular user.

*   The attacker can create spoofed de-authentication frames and set the source MAC address as the AP’s MAC address and destination MAC address as victim MAC address. Then, the attacker can proceed to inject these spoofed frames into the target network. These spoofed frames, upon reaching the user’s terminal, disconnect the user from the network.

*   The attacker can create a packet with source MAC address of the AP and destination as broadcast MAC address. All the users linked to a particular Access point will get disconnected. A broadcast de-authentication DoS attack has impacts that are so severe to the extent that all users connected to a target access point in the network can be de-authenticated.

An attacker has at his disposal, utilities such as scapy, the aircrack-ng suite, file2air, among others that they can use for launching the denial of service de-authentication attack. An attacker just needs a networks’ SSID, BSSID of the access point, the targets’ MAC address, and is good to go. TCPdump, airodump-ng, Wireshark, and kismet are some of the tools an attacker can use to obtain this information. A wireless network attacker may opt to insert periods of silence between the transmission of de-authentication frames to evade detection and make the attack more stealthy.

# Chapter 8: File Systems and Storage Device Management

## File Systems

### What are File Systems?

We describe a filesystem as a mechanism or a data structure a particular operating system utilizes for purposes of keeping track of the files stored on a partition or disk. i.e., the manner in which the organization of files on the disk has been done. It is also used to denote a partition for storing files or type of the filesystem. The difference between a disk or partition and the filesystem it contains is essential. A few programs operate directly on the raw sectors of a disk or partition; if there is an existing file system there, it will be destroyed or severely corrupted. Most programs operate on a filesystem, and therefore won't work on a partition that doesn't contain one or is of the wrong type. Before a partition or disk can be used as a filesystem, it needs to be initialized, and the data structures required for bookkeeping have to be written to the disk. This process is called making a filesystem.

Most UNIX filesystem types have a similar general structure. The structure has a superblock, an inode, a data block, a directory block, and an indirection block. The directory stores the name, alongside the inode number. An entry in the directory is made up of an inode number that is used to represent the file together with the filename. The inode possesses numbers of the several blocks of data, all of which are utilized in the storage of data/information within a particular file. Only a small space is available to store numbers of the data blocks in the inode. The allocation of space in cases where more of it is needed is carried out dynamically. The blocks that have been allocated dynamically are called indirect blocks. This means that if you want to get the data block, you will be required first to locate its number that is located within the indirect block.

It is possible for a user to make a hole in a file in a UNIX filesystem. This is a place in the file that has zero bytes. That place has no real disk sectors allocated to it. That is commonly done for some databases, small binaries, and the Linux-shared libraries, among other cases which are exceptional. Linux supports several types of filesystems. The most important file systems include:

Minix – This is the oldest and without doubt, the most reliable. It is, however, quite limited in its features and has restricted capabilities; for instance, it only allows 64 MB at most per filesystem.

ext2 – this file system was designed purposely for upward compatibility.

Ext - ext is not upward compatible and is an older variant of ext2\. It is hardly being utilized in current installations.

ReiserFS – this filesystem is robust. It utilizes journaling, thereby making data loss highly unlikely. The journaling we have mentioned a number of times is generally a mechanism for record-keeping. By storing these records, a filesystem is able to reconstruct itself easily and quickly after the occurrence of some damage. Say, a damage brought about by the improper shutdown of the system.

Xia – this is just a minix filesystem that has been improved. It no longer has limits on sizes of the filenames and filesystem. That is the only difference it has from minix. No new features have been added. It is not popular even though it works quite fine.

ext3 – just like ext2, this filesystem possesses all the aspects in ext2 with an added functionality. This is the addition of journaling. The recovery time and performance have, therefore, been greatly improved.

jfs – is a filesystem that is journaled and was created by IBM to deliver in environments where high-performance is required.

NFS – this one is a networked filesystem that enables sharing a filesystem among multiple computers to grant access to the files within them.

smbfs - A network filesystem compatible with the Windows file sharing protocols that allow an MS Windows computer to share a filesystem.

umsdos – simply put, umsdos allows for the utilization of a normal msdos filesystem as if it was a Linux one. This eliminates the requirement of a separate partition for Linux.

xfs –Silicon Graphics designed this filesystem to function like a 64-bit journaled filesystem. Similarly, it was to be capable of high performance in cases where large files and filesystems were concerned.

MS-DOS – this was designed to provide compatibility with MS-DOS and FAT filesystems.

vfat – This is an extension of the FAT filesystem known as FAT32\. It is primarily useful because it supports larger disk sizes than FAT does. Most MS Windows disks are vfat.

iso9660 – this is a standard CD-ROM filesystem.

hpfs – This is a filesystem for OS/2.

sysv – this is a file system used in SystemV/386, Coherent and Xenix.

NTFS – This is the most advanced Microsoft journaled filesystem providing faster file access and stability over previous Microsoft filesystems.

### Deciding Which Filesystem to Use

As of today, the journaled Ext3 filesystem is the most popular. Selecting this type of filesystem is undoubtedly a wise choice. Similar to ext3, is Reiserfs. Remember we said that it is also a filesystem that is journaled. The selection of which file system to use can be arrived at on a case-by-case basis based on the users’ requirements. They can either be compatibility, speed, reliability, or overheads for structures required for bookkeeping. There are many other factors, but these are the common ones. We use the term “journaled filesystem” to denote a filesystem utilizing journaling in its file storage mechanisms. The journals’ main function is to keep logs of what is going on within the filesystem, that is, journals. In the unfortunate scenario whereby we have a system crash, a journaled filesystem will use the logs for the recreation of data that is unsaved or lost. It is not prudent, however, to be intrigued by this. Nothing is perfect; errors are bound to arise at some point. Backing up of vital information is the only sure bet whenever an emergency arises.

### Creation of a Filesystem

Filesystems are created using the mkfs command; that is, they are initialized. Each and every filesystem type has its own separate program. mkfs can be said to be a front end used for executing appropriate programs based on the preferred filesystem type. The type of filesystem can be selected using “-t fstype,” which is one of the options this command gives. Most programs that are called using the mkfs command possess a dissimilar interface of the line of the commands,that is the command line, albeit slightly. Below are the commonly used;

*   -t fstype: this selects the filesystem type.

*   -c: this searches for blocks that are bad. It also initializes the list of bad blocks accordingly.

*   -l filename: this enables the reading of the initial list of bad blocks from the name file.

### File System Block Size

It is a block size that is used for specifying a filesystems’ size that it shall utilize in the reading and writing of data. Subsequently, it means that a block size that is large can aid in the improvement of the performance of the disk input/output in places or systems that use files that aare large. A database is an example of this. This is due to the fact that the data reading or writing operation may take more time to need to search for the next block. However, a lot of disk space can get wasted in circumstances where we have a filesystem with a lot of smaller files.

Take an example of the /etc. The maximum file size that can be supported on some filesystems is determined by the block size. Modern filesystems are, in most cases, limited by the number of blocks and not by file size or block size.

### Mounting and Unmounting

One has to carry out the mounting of a filesystem before using it. To ensure that everything will work as expected, the operating system will then do a number of bookkeeping tasks. In UNIX, a single directory treehouses all the files. The operation for mounting the file system normally results in new filesystem contents being similar to those located in an existing subdirectory which is in a file system that has been mounted already. Only two arguments can be accepted by the mount command. The first argument that can be accepted is the device file that corresponds to the partition or the disk that contains the filesystem. The directory below, which will be mounted, is the second argument. Like we have mentioned earlier, upon execution of these commands, the contents of both filesystems will respectively resemble the contents of /home directory and the /usr directory.

The device file grants access to the raw contents of the disk and the mounted-on directory provides one with the files on the disk. The mounted-on directory is referred to as the mount point. The mounted-on directory does not need to be empty, but it must be there. Note that any files it contains will be inaccessible by name while the filesystem is mounted. In the event that a filesystem does not need mounting, a umount command can be used to unmount it. This command, “umount” accepts only one argument. That can be mount point or the device file. Both unmounting and mounting require that a user has superuser privileges. By this, it means that it is only root that can do it. This is because if any user were to be let to carry out these tasks, then it would be easy for a malicious person to make a trojan horse that is disguised as /bin/sh using the floppy. That is not desirable.

In circumstances in which users may require to use floppies, there are methods we can use to grant them permissions. For example, the users can be given the root password. This is not good security in as much as it is the natural solution. Nevertheless, it can work well in cases where security is not needed. A case on personal systems that are nonnetworked. Alternatively, the use of sudo can come in handy for users intending to mount or unmount. Like the first method, it is bad security. It just does not give direct superuser privileges to everyone. An administrator needs to think very hard on behalf of a user here. Sudo may be configured to allow users to execute specific commands. Finally, the user can utilize the tool’s utility, which is designed to manipulate MS-DOS filesystems without necessarily mounting them. This is good in cases where only MS-DOS floppies are needed.

### Checking File System Integrity with Fsck

Filesystems are error-prone due to their complex nature. A filesystem's accuracy and validity can be assessed using the fsck command. It can be instructed to quickly repair any minor issues it finds, and to alert the user if there any serious, unrepairable issues. Thankfully, the code to implement filesystems is debugged quite effectively. This means that there are rarely any problems with this process. Most of the problems are brought about by failing hardware, power outages, and errors on the operator’s part. For instance, the operator may not properly shut down the system.

On booting, many systems automatically run fsck to be able to detect and correct any errors before the system starts being used. This is a good thing as it prevents the usage of a filesystem that is corrupt. You do not want to use a corrupt filesystem. In cases where the structures of data  are in a mess, a filesystem that is corrupt will only worsen, then making data loss inevitable. Not that it takes a considerable amount of time to run fsck on big filesystems. In most cases, errors do not occur in filesystems that have been correctly shut down. To avoid these lengthy checks, one can use options explained herein. First, no checks are made if  the file /etc/fastboot is present. The second way is the unique markers present on ext2 filesystems’ superblocks which serve to inform if the filesystem was correctly unmounted after the last mount operation. This means that e2fsck, which is the fsck version in ext2 filesystem will avoid the checks suppose the flag shows that unmounting was properly performed.

Note that automatic checking on filesystems is only possible when they have been automatically mounted at the time of booting. Also, you can use fsck to check other filesystems manually. These can be floppies and many others. On a last note, only run the fsck command on unmounted filesystems. This should never be done on mounted filesystems. Accessing the raw disk can lead to modifications in the filesystem without the knowledge of the operating system, and the consequences can be disastrous.

### Using Blocks to Check for Disk Errors

Periodic checking of disks for bad blocks is a noble idea. To do this, we can make use of the bad blocks command. This command will give us a list of all bad blocks  it will have found in the disk. We can feed that list to fsck for it to be recorded within the data structures in the filesystem. This will keep the operating system from using the bad blocks for data storage.

## Storage Device Management

### Storage Models

It is possible to differentiate the different storage models just by looking at how the devices responsible for keeping the bits in place interacts with the higher layers. We have the following models of storage:

1.  Direct Attached Storage

Let us take the scenario where a hard drive is directly connected to the server via

a bus adapter. Through this connection, the operating system will be able to detect the devices after which it will maintain a file system on it. This provides access, albeit with the smallest level of indirection. Desktop, laptops, and the majority of server systems use this mechanism. All the components sharing the interfaces are under control of a single operating systems’ server. Also, each server has its own storage system. When it comes down to the hardware level, attachment to the storage media is achieved using any of the several technologies present.

A simple application of this storage model is a server having a single hard drive. It is also common to have servers with multiple devices having a direct attachment to it. The configuration here will entirely depend on the strategies of the next higher levels of storage. It is easy to mount the individual disks at different locations within the hierarchy of the file system. The other way of combining the numerous attached disks is by using RAID; this is what is known as Redundant Array of Independent Disks in full, or a Logical Volume Manager. These are famously abbreviated as RAID and LVM respectively. The idea here is to improve the performance of the system, increase redundancy, and also to increase the volume of storage. This type of storage does not need to be located in the same physical place as the server using it. The advantages of direct-attached storage include

*   Possibility of failure is eliminated as there is no other additional layer or network between the hardware and the operating system. 

*   It is also impossible to have a performance penalty caused by network latency.

Away from the advantages now, let us look at the one major disadvantage this model has.

*   The direct attachment of the storage device means that data being used by one machine on the network cannot immediately be made available to other systems.

The shortcoming above has been overcome by using the storage area network or the network-attached storage, which are next up for discussion.

2.  Network Attached Storage

Here, the users’ data is stored on shared disks which are them availed to all clients within a particular network.  This means that any user can access their data at exactly the same location regardless of the device they are using. The following two factors are required to make this work:

1.  There has to be means by which the host’s file system can retrieve the centrally located data.
2.  Access to the central storage all over the network is required.

This model of storage comes with a number of complex issues such as performance and access control.

3.  Storage Area Networks

The already discussed network-attached storage requires all users to make use of one specific file system. With the increased requirements for network-attached storage and storage area network hardware, data availability, performance, data redundancy, and storage size, it becomes necessary to allow access of large chunks of storage on block Levels by users. To this end, dedicated high-performance networks are built to manage data storage. Here, the centrally located storage media can be accessed by way of interfaces and protocols capable of high performance. These include fiber channel and another we call iSCSI, a shortened form for internet small computer systems interface.

SANs are known as an “enterprise solution” because of their distributed nature and notable performance advantages. This is true, especially in cases where a switched fabric has been used. Storage area networks, through encapsulation of protocols, can surmount restrictions to a local area network. For instance, iSCSI permits the linking together of switched storage area network components over a wide area network. System administrators have the responsibility of availing the physical storage devices in all of these models.

4.  Cloud Storage

At every step of the storage model discussion, additional layers of indirection have been introduced. That has led to an increase in the users, disk space, redundancy, and so on. The keen readers should have noticed that we have transitioned from providing block-level access in direct-attached storage to block-level access across a dedicated storage network in distributed file systems.

All this, however, ensures that users are restricted to a specific network. Numerous organizations are transitioning from maintaining their Infrastructure to the model we call IaaS. This ladies and gentlemen is Infrastructure as a Service. The transition is also tending towards cloud computing.

Cloud Storage falls under cloud computing. It can be used to denote commercial services that provide users with file storage and hosting services. Examples include Google Drive and Dropbox. Cloud storage is used by companies requiring flexible storage solutions that can be offered by the existing storage models. To meet these demands, the units doing the storage are swiftly assigned from large storage area networks that span entire data centers. In this storage model, we have three different categories:

*   Services offering block-level access to users. This means that the users can create partitions and file systems as they wish, for instance, Cinder service provided by OpenStack.

*   Services providing object-level access, an example is, Blob Storage provided by Windows Azure.

*   Services providing file system-level access. An example of file hosting services is Amazon simple storage.

All the categories above depend on a specified API to provide the ability to access storage units programmatically.  The numerous distributed storage resources are usually joined together to create a large storage pool. It is from this pool that units are allocated and de-allocated, the units are also re-allocated or relocated, and finally, the units can be duplicated. This is made possible through the use of programs at higher-levels via interfaces that are well-defined over to lower-level storage systems. Cloud storage solutions come with advantages such as:

a)    Entire OS images and applications can be easily imported, exported, or deployed as virtual appliances.

b)    The elimination of individual storage components simplifies cloud storage infrastructure.

c)     The storage units can be availed immediately on a need basis. The availability is dynamic; i.e., it can grow or shrink depending on the usage patterns.

Cloud storage, however, is not immune from failure. This is due to the addition of multiple layers of abstraction. Additionally, the reliance on abstracted storage containers provided by third-parties prevents an end-to-end troubleshooting a system. This means that when we outsource data storage, we shall be inviting numerous security concerns. The concerns can range from the safety of data and privacy. When we gain access to files through the Internet, there is a high chance of us increasing the latency, which will consequently decrease the throughput. The cloud service provider can be a SPOF (single point of failure) falling entirely outside our domain.

### Storage Model Considerations

The architecture of the storage models become more complex as the requirement for storage increases. This is a crucial consideration to take note of. Indirection and additional layers of abstraction bring about exponential costs and complexity. A system with more moving parts is likely to fail spectacularly. It is easy to replace one bad hard drive but not so easy to rebuild an array of storage being used by clients in the hundreds. A storage solution that gives users resilience, reliability, and redundancy comes in handy as the numbers of users continue to rise. The storage models that we have looked at are intertwined. Beneath all storage solutions lie the direct-attached storage as the bits will eventually have to be stored somewhere.

Concepts of network-attached storage are evident in any infrastructure. This spans multiple work stations and storage area networks. Cloud storage uses the two models to provide storage to complex networks. That being said, we create security risks at every layer we add. The privacy and integrity is paramount. Still, on security, cloud storage often transmits and provides access to user data via untrusted networks. This necessitates the use of secure sockets layer or transport layer security protocols to safeguard data. Simple data storage models are safe and more scalable as compared to the more complex ones. So take note. 

### Disk Devices and Interfaces

What we have been discussing about different storage models is that they are a means to access the devices for storage so that we can store data. The following tools are used for data storage: magnetic tapes, DRAM-based storage, the hard-disk drive, solid-state drives, and optical media like DVDs. The most commonly used storage device is the hard drive which does the storage of data on magnetic platters which usually rotate. System administrators are required to have an in-depth understanding of the physical structure of the hard drives. These drives are availed to servers in several ways.

A host bus adapter is connected directly to the individual disks by way of a single data cable and a separate cable for power. SATA, PATA, Fiber Channel, and SCSI are all examples of traditional interfaces. The SCSI has been in existence for over a quarter a century but has been made obsolete by the Advanced Technology Attachment standards. Integrated Device Electronics (IDE), also referred to as Parallel Advanced Technology Attachment, utilizes an 80 or a 40 wire cable made of ribbon. This interface allows a maximum of two devices which are typically the master and the slave. Serial ATA (SATA) interface allows for hot-swapping, smaller cables, and faster throughputs. All the interfaces we have mentioned herein can either be internal or external.

# Chapter 9: Becoming Secure and Anonymous

## Introduction to Becoming Secure and Anonymous

Nearly everything we do today on the internet is tracked. Whoever is doing the tracking, be it Google tracking our online searches, website visits, and email or security agencies cataloging our activities, every move we make online is being recorded, indexed, and then mined to benefit someone. The hacker, in particular, needs to understand how to limit this tracking and remain relatively anonymous on the web to limit this surveillance. In this chapter, we are going to learn how we can stay anonymous while surfing the web using these four methods:

*   The Onion Network
*   Proxy servers
*   Virtual private networks
*   Private encrypted email

No one method is sure to keep your activities safe from prying eyes, and given enough time and resources, and anything can be tracked. However, these methods will likely make the tracker’s job much more difficult.

### How Does the Internet Give Us Away?

Let us discuss at a high level some of the ways our activities on the internet are tracked. We won’t go into all tracking methods, or into too much detail about any one process, as that would be beyond the scope of this book. First, your IP address identifies you as you traverse the internet. Data sent from your machine is always tagged with your IP address, making your activities easy to track. Second, Google, alongside other email services, will “read” your email, looking for keywords to more efficiently serve your ads. Although there are more sophisticated methods that are far more time and resource-intensive, these are the ones we are going to try and prevent in this book.

### How IP Addresses Give Us Away on the Internet

When you send a packet of data across the internet, it contains the IP addresses of the source and destination for the data. In this way, the packet knows where it is going and where to return the response. Each packet hops through multiple internet routers until it finds its destination and then hops back to the sender. For general internet surfing, each hop is a router the packet passes through to get to its destination. There can be as many as 30 hops between the sender and the destination, but usually, any packet will find its way to the destination in fewer than 15 hops. As the packet traverses the internet, anyone intercepting the packet can see who sent it, where it has been, and where it’s going. This is one-way websites that can tell who you are when you arrive and log you in automatically, and it’s also how someone can track where you’ve been on the internet.

1.  The Onion Router System

The US Office of Naval Research in the 1990s set out to develop a method for anonymously navigating the internet for espionage purposes. The plan was to set up a network of routers that was separate from the internet’s routers.  These routers could encrypt the traffic, and that only stored the unencrypted IP address of the previous router meaning all other router addresses along the way were encrypted. The idea was that anyone watching the traffic could not determine the origin or destination of the data. This research became known as The Onion Router Project in 2002, and it’s now available to anyone to use for relatively safe and anonymous navigation on the web.

## How Tor Works

Packets sent over Tor are not sent over the regular routers so closely monitored by so many but instead are sent over a network of over 7,000 routers around the world. On top of using a separate router network, Tor encrypts the data, destination, and sender IP address of each packet. At each hop, the information is encrypted and then decrypted by the next-hop when it’s received. In this way, each packet contains information about only the previous hop along the path and not the IP address of the origin. If someone intercepts the traffic, they can see only the IP address of the previous hop, and the website owner can see only the IP address of the last router that sent the traffic. This ensures relative anonymity across the internet.

Unfortunately, the tradeoff is that surfing via the Tor browser can be a lot slower; because there are not nearly as many routers, the bandwidth is limited in this network. In addition to being capable of accessing almost any website on the traditional internet, the Tor browser is capable of accessing the dark web. The sites that make up the dark web require anonymity, so they allow access only through the Tor browser, and they have addresses ending in .onion for their top-level domain. The dark web is infamous for illegal activity, but several legal services are also available there.

### Security Concerns with TOR

Several intelligence agencies consider the Tor network a threat to national security, believing such an anonymous network enables foreign governments and terrorists to communicate without being watched. Consequently, several robust, ambitious research projects are working to break Tor’s anonymity. Tor’s anonymity has been broken before by these authorities and will likely be broken

again. Americas’ NSA, for instance, runs its own Tor routers, meaning that your traffic may be traversing the NSA’s routers when you use Tor.

If your traffic is exiting the NSA’s routers, that’s even worse, because the exit router always knows your destination. The NSA also has a method known as traffic correlation, which involves looking for patterns in incoming and outgoing traffic, that has been able to break Tor’s anonymity. The attempts to break Tor will not affect its effectiveness at obscuring your identity from commercial services. We have given an example of Google. However, they may restrict a browser’s effectiveness in blocking you from spy agencies.

2.  Proxy Servers

One other way of achieving anonymity is by use of proxies. Proxies are intermediate systems that act as middlemen for traffic: the user connects to a proxy, and the traffic is given the IP address of the proxy before it’s passed on. When the traffic returns from the destination, the proxy sends the traffic back to the source. In this way, traffic appears to come from the proxy and not the originating IP address. The proxy will likely log your traffic, but an investigator would have to get a search warrant to obtain the logs. To make your traffic even harder to trace, you can use more than one proxy, in a strategy known as proxy chaining. The chaining can either be dynamic or random.

### Security Concerns in Using Proxy Servers

If you intend to be anonymous, do not use a free proxy. Hackers use paid for proxies that can be trusted. Free proxies are likely selling your IP address and browsing history. Although the IP address of your traffic leaving the proxy will be anonymous, there are other ways for surveillance agencies to identify you. For instance, the owner of the proxy will know your identity and, if pressured enough by law enforcement agencies, they may offer up your identity to protect their business.

3.  Virtual Private Networks

Using a virtual private network can be an effective way to keep your web traffic relatively anonymous and secure. A VPN is used to connect to an intermediary internet device such as a router that sends your traffic to its ultimate destination tagged with the IP address of the router. Using a VPN can certainly enhance your security and privacy, but it’s not a guarantee of anonymity. The internet device you connect to must record or log your IP address to be able to send the data back to you accurately, so anyone able to access these records can uncover information about you.

The beauty of VPNs is that they are simple and easy to work with. You can open an account with a VPN provider and then seamlessly connect to the VPN each time you log on to your computer. You would use your browser as usual to navigate the web, but it will appear to anyone watching that your traffic is coming from the IP address and location of the internet VPN device and not your own. Besides, all traffic between you and the VPN device is encrypted, so even your internet service provider can’t see your traffic.

Among other things, a VPN can be useful in evading government-controlled Content and information censors. For instance, if your national government limits your access to websites with a particular political message, you can likely use a VPN based outside your country to access that Content. Some media corporations, such as Netflix, limit access to their Content to IP addresses originating from their nation. Using a VPN based in a country that those services allow can often get you around those access limitations. Some of the best VPN services are IPVanish, NordVPN, ExpressVPN, CyberGhost, Golden Frog VPN, Hide My Ass, Private Internet Access, PureVPN, TorGuard, and Buffered VPN.

The strength of a VPN is that all your traffic is encrypted when it leaves your computer, thus protecting you against snooping, and your IP address is cloaked by the VPN IP address when you visit a site. As with a proxy server, the owner of the VPN has your originating IP address.

4.  Encrypted Email

Free commercial email services such as Gmail, Yahoo, among others, are free for a reason. If a service is free, then you must be the product, not the customer. In addition, the servers of the email providers have access to the unencrypted contents of your email, even if you’re using HTTPS. One way to prevent eavesdropping on your email is to use encrypted email such as ProtonMail. This

means that your email is encrypted on ProtonMail servers, even the ProtonMail administrators can’t read your email. ProtonMail was founded by a group of young scientists at the CERN supercollider facility in Switzerland. ProtonMail’s servers are based in the European Union, which has much stricter laws regarding the sharing of personal data than the United States. ProtonMail does not charge for a basic account but offers premium accounts for a nominal fee. It is important to note that when exchanging emails with non-ProtonMail users, there is the potential for some or all of the email not to be encrypted.

# Chapter 10: Advanced Social Engineering and Physical Security

## Introduction to Advanced Social Engineering and Physical Security

Social engineering is increasingly becoming a major threat to virtual entities and is also becoming an effective vector with which to attack information systems.

Most services in use today lay a good foundation for sophisticated social engineering attacks. In every major institution world-wide, the trend is towards bringing your own device to the workplaces, schools, and social places. That may appear an effective way of enabling communication and collaboration in environments that are private or business in nature. This policy has aggravated this problem to a terrifying extent.

Global organizations are no longer staffing geographically but rather use a just-in-time strategy to cater to their staffing demands. Consequently, we have seen personal interaction decreasing as it is being replaced by a plethora of tools that have bridged the communication gap. These tools can be e-mail, Skype, and many more. All of these have resulted in new vectors of attack for social engineering attacks. When social engineering attacks are used in conjunction with zero-day-exploits, they have the potential to be a deadly weapon. This mechanism is what is commonly used by APTs, that is, advanced persistent threats.

### What is Social Engineering?

We define social engineering as a broad range of activities that are malicious in nature that are accomplished via human interactions. This type of attack employs the use of psychological manipulation for purposes of tricking the users into giving away sensitive information or making security-related mistakes. Usually, social engineering attacks are carried out in a number of steps.

As usual, a perpetrator will initially carry out a reconnaissance on the intended victim to enable them to collect necessary information on their background. That background information may include identification of potential entry points and weak security protocols. This step is essential as it will dictate how the attack will proceed. Thereafter, an attacker will speedily move to win the victim’s trust plus offer appealing incentives for subsequent actions that go against the laid down security practices, like exposing information that is sensitive or granting access to resources that are critical. These attacks are deadly due to their reliance on errors committed by humans instead of the vulnerabilities in the operating systems or the software. The human-made mistakes have a characteristic of being less predictable, thus making them difficult to pinpoint and guard against as compared to an intrusion that is malware-based.

### Techniques for Attacks Used by Social Engineering

These types of attacks can be in multiple and different forms. As long as there is human interaction is involved, a  social engineering attack can be carried out. Let us look at the following five commonly perpetrated social engineering attacks.

1.  Pretexting

An attacker will attempt to gain access to information by a sequence of cleverly crafted lies. Pretexting is, in most cases, started by a perpetrator pretending that they require some crucial information from an unsuspecting victim to do a task that is critical. The attacker commences by building or winning the trust of their victim by impersonating police, bank officials, tax officials, co-workers or any other person with a position of authority which gives them the right to know. The pretexter will then ask questions that will require a user to confirm their identity. This way, an attacker is able to collect critical personal data.

2.  Phishing

Popular phishing scams are in the form of text message and email campaigns that are meant to create a feeling of curiosity, compelling urgency, or even instill fear in potential casualties. The victims are then prodded into disclosing information that is deemed sensitive, following the links to malicious websites by clicking on them, or by downloading and opening unknown attachments containing malware. For instance, users of a particular online service can be sent an email to alerts them of a policy violation that requires an action to be done immediately on their part. An example of such an action is a password change. Upon clicking the link, the user will be redirected to an illegitimate website that is almost identical in every aspect as the legitimate one, prompting an unsuspecting user to input his/her credentials to the website. That information is sent to the attacker once the form is submitted.

3.  Baiting

This type of attack utilizes a misleading promise to capitalize on a victim’s curiosity  or greed, mostly greed. Users are lured into a trap which leads to the stealing of their personal information. Also, malware can be send to their systems this way. The most reviled form of baiting uses physical media to disperse malware. For instance, attackers leave the bait, typically malware-infected flash drives, in areas where potential victims are likely to see them. The bait intentionally appears real. Victims who are unsuspecting will take up the bait due to curiosity. Afterward, they are likely to insert the device into a computer either at work or at home. This will lead to an automatic installation of malware on the system. This type of attack can be carried out in the physical or online world.

4.  Scareware

This strategy of attack involves bombarding the victims with numerous false alarms or fictitious threats. Gullible users will be tricked into thinking their system has become malware-infected. This will cause them to install software with no actual benefit or even install the malware itself. An example of a scareware is  “Your computer is infected by a harmful program” banner. Also,  scareware is able to be spread via spam email issuing bogus warnings or offering users a chance to purchase worthless and harmful services.

5.  Spear phishing

Since we now know what phishing is, let us look at spear phishing. Here, an attacker targets specific enterprises or individuals. After identifying a target, they will go ahead and tailor-make their messages factoring issues such as job positions, contacts, and characteristics that can be attributed to their targets so as to make the attack less conspicuous. This type of phishing attack needs a lot of effort from an attacker and usually takes a very long time to pull it off successfully. Such attacks have impressive success rates when they are executed skillfully. They are also more difficult to detect.

### Social Engineering Prevention

When it comes to social engineering, the perpetrators carry out manipulation of human sentiments, which include fear or curiosity, so that they are able to affect their malicious schemes, thereby luring victims into their traps. It is paramount that we be vigilant at all times if we are to keep social engineering attacks at bay. Let us look at tips that can help us deal with these types of attacks below.

Update your antivirus software –engaged automatic updates on your devices. Ensure that you download the latest signatures for your protection software frequently, say every day. Carry out a periodic check to ascertain that the updates you have downloaded have been applied. It goes without saying that you need to scan your system for possible infections.

Adopt a multifactor authentication – this  means  that in the unfortunate event that your systems are compromised, all your accounts will still be safeguarded. User credentials are extremely valuable to attackers, and they more likely than not will seek to obtain them.

Stop accepting of suspect offers – think twice before accepting an offer that sounds too good to be true. A simple google search on the topic can come in handy to help you judge if you are being lured into a trap or whether what you have with you is a legitimate offer.

Don’t open suspicious emails/attachments – When you receive an email from an unknown sender who looks suspicious, do not open it. If the sender in question is known, you may want to crosscheck from them or other sources in cases where it is a company email. You can use a telephone to call for verification. Alternatively, you may opt to get details directly from the provider of the service. As you may have learned now, it is possible to spoof email addresses. That means that an attacker is able to impersonate a genuine email. Never take a chance.

# Chapter 11: Python Scripting Basics for Hackers

## What is Python?

Python is an open-source and high-level language that has been in existence from the late ‘80s. Today, it is being used in web apps, create graphical user interfaces, games, and most importantly, intrusion mitigation and hacking exploits. Most python commands are made up of typical English statements meaning it will be easier for you to understand their functions immediately. Codes in Python are relatively more straightforward and shorter as compared to other high-level languages like Java. Additionally, Python comes with an inbuilt library and features, alongside access to third-party modules and libraries. This is a programming language preferred by hackers due to its robust integrated libraries and availability of shared resources that have been compiled by other users. If you are a first-time programmer, you will find Python uses more straightforward codes and syntax. If you are interested in jumping right into hacking, you will enjoy discovering what you can manipulate with your programs.

### Interacting with the Python Language

You can use Python using the script mode if you want to see how entire files or applications are interpreted. To interact with Python, you can use the integrated development environment that will pull up the Python shell window, or the command line in Windows.

### Interacting Using the Command Prompt

The Terminal in Linux and Mac OS X or the Windows command line is the simplest and straightforward way to start using Python. Please note that this might not be the most preferred interaction with hackers. However, this method will allow you to explore Python’s features quickly.

### Interacting Using the IDLE

When you are using a programming language, such as Python, you will need to develop your code using an integrated development environment or IDE. An IDE is an application that will provide you all the tools that you need to develop a software. The IDLE tool that comes with your installation package serves as a platform where you can efficiently key in your codes and interact with Python. You can easily pull up IDLE by clicking on its icon on your desktop, the Start Menu or locating it on the install folder. IDLE allows you to use these features:

 The Python shell window which allows you to make use of color-coded code input and output and get error messages if you input a wrong statement.

 A debugger that comes with stepping, local and global namespace viewing, and persistent breakpoints

 Browsers and configuration

 A text editor that allows you to use multiple Windows, colorizing for Python, autocompletion, undo, and other features

Using IDLE will allow you to simultaneously use two Windows which are the Shell and the Editor which you can use.

### Other Things You Can Use

You can write your codes in other IDEs or text editors other than IDLE, depending on your needs. Here are other editors and their features that you can use: PyCharm Educational Edition, Sublime Text, VIM, and Coda.

## Python Basics

You need to learn other concepts that are essential in a Python script. You will also want to create a script that is easy for you to understand and review in the future, just in any case you want to improve it and turn it into a working tool for your hacks. Let us see how variables and constants work in Python.

### Comments

These are statements that come after the # symbol. These pieces of texts allow you to:

1) Explain the problems that you are aiming to overcome or solve in your program.

2) Take note of the important assumptions, details, and decisions that you want to perform in the code.

3) Making notes in your code does not only remind you what you want to achieve in your code, but also helps readers that will be using your program to understand what lines of code are supposed to do.

### Literal Constants

Literal constants are named as such because you take these pieces of text for their literal value. These constants can be Numbers, Strings, Variables, Objects, Lists, and Dictionaries.

### Writing Python Programs

Now that you are aware of some basic concepts that you need to grasp in Python, it’s time to learn some guidelines that you need to remember when it comes to writing a Python program.

### Physical and Logical Lines

What you see when you type out a program is called a physical line. What Python gets when you type a statement is called the logical line. With this said, this programming language assumes that every physical line that you see corresponds to a given logical line. While you can use more than one logical line on a physical line by using the semicolon (;) symbol, Python encourages that programmers like you input a single statement in order to make your codes more readable.

### Indentation

Python is one of the programming languages out there where the space at the beginning of each line of code is important. By using indentation, you can group together blocks of statements that belong together. As a rule of thumb, see to it that you are using the same indentation when you are working on similar statements. Also, remember that using the wrong indentation can make your code prone to error.

### Operators and Expressions

Most of the statements you will be writing in your code will include expressions. Expressions are divided into operands and operators. Operators are essentially functions that do something in your code, which are represented by symbols or keywords. They usually require pieces on information that they can work on, which are called operands. For example, if you have the expression 1 + 3, the plus (+) sign is the operator, and the numbers 1 and 3 are operands.

### Expressions

Expressions are combinations of operators and values in your code. You can think of it as anything that “expresses” something that has a value. For example, if you use the function eval(2 +2), you will get a result that provides you the value of these two numbers added together.

### Functions

A function allows you to create a block of code that will be able to do an action. They are also reusable, which means that you can provide a name to that statement block and then run this block using the name that you assigned it anywhere in the program that you are building without any limit. In Python terms, this is called “calling the function.” Functions are probably the most important component of a programming language. In Python, they are usually defined using the keyword def, followed by an identifier name for the function that you want to use.

### Function Parameters

Functions can take in values they will use, which are called parameters. Parameters act in a similar fashion as variables, except that you are defining their values whenever you call the function and that you have already assigned values to them once you run the function. Parameters are specified within a pair of parentheses when you are defining the function and are separated using commas. If you need to call the function in your code, you will need to provide values in a similar fashion. Keep the following in mind, when you are providing value to your function while you are naming it, these values are called parameters; but when you are supplying values as you call the function, these values are called arguments.

### Keyword Arguments

There will be instances when you code where you have too many parameters in your function, if you want to specify some of them, then you can use keyword arguments to give values for some of the parameters. Doing so will provide you with the advantage of efficiently using the function without having to worry about the arguments’ order, and that you can assign values to the parameters that you want to use, especially when the other parameters that are available already contains argument values that are set in default.

### The Return Statement

If you want to break out of the function, or if you want to return a value from the function, then this statement is what you will use.

### DocStrings

This is a tool you can use to document the code that you are creating and make it easier to understand. You can also get a docstring from a function while the code is already running.

### Iteration

There are some instances where you may find it annoying to write the same code multiple times to do a similar function, such as checking different IP addresses or analyze different ports. For this reason, you may want to use a for-loop instead to iterate the same code for different elements.

### Exception Handling

Even if you are already able to write a program with correct syntax, you may still go through some errors upon execution or runtime. For example, when you divide anything by zero, you are likely to experience a runtime error because Python knows that it is impossible to do so. If you want to fix the error while you are already running your code, Python’s ability to perform exception handling will come in handy. Using the example above, you can use the try or except statement to make use of the exception handling so that when the error happens, the exception handling feature will catch the error and then print the message on the screen.

### Modules

If you want to make use of the functions that you have already created from another program to another, instead of having to rewrite the entire code, then you can use modules. The simplest way to make modules is to create a file that contains all the variables and functions that you may need to use in a future program and then save it as a .py file.

*   Sys Module

Sys module is a built-in module that provides you access to all objects that the programming language’s interpreter maintains or uses. This module includes command-line arguments, the maximum size of integers that can be used, flags, path hooks, as well as other available modules. Being able to interact with the sys module will allow you to create different scripts that you can use for different hacking purposes.

*   OS Module

Python’s OS module provides plenty of routines for different operating systems, such as Mac and NT. Using this module, you can allow the programming language to interact on its own with the file-system, permissions, user database, and different OS environments.

## The Python Standard Library

Python’s library is pretty much the collection of almost every element there is in this programming language. This extensive collection has several built-in modules that allow you to access different functionalities in the system. It is also responsible for providing you access to modules, which are designed to enhance Python’s inherent portability.

At this point, you already know the essentials in Python. As you create your codes for hacking or import modules from libraries, you will be able to discover more functionalities and learn what they are used for. Since you are learning how to code to hack, the best way for you to pick up your pace is to learn as you create tools that you can use for hacking.

### Setting Up for Hacking

Learning how to hack entails being able to set up the right environment that you can work in in order to develop your own exploitation tools. Since you have already installed Python and the standard library that comes with it, you are pretty much set up for hacking. All you need to do now is to install other tools and libraries that you can use for the exploits that will be detailed below.

### Installing Third-Party Libraries

Third-party libraries are essentially libraries that do not come native with your installation of Python. All you need to do to get them is to download them from a targeted source, perform uncompressing on the package that you just downloaded, and then change into the target directory. As you might have already guessed, third party libraries are instrumental when it comes to developing your tools out of the resources that are already created by someone else. Since Python is a highly collaborative programming language, you can use libraries that you may find from website sources such as GitHub or the Python website and incorporate them into your code.

### Password Cracker - Your First Python Program

To write this password cracker, you will need to have a crypt() algorithm that will allow you to hash passwords that are in the UNIX format. When you launch the Python interpreter, you will see that the crypt library that you need for this code is already right in the standard library. To compute for an encrypted hash of a UNIX password, all you need to do is to call the function crypt.crypt() and then set password and salt as parameters. The code should return with a string that contains the hashed password.

### Network Hacking

A network attack is any tactic that will allow a hacker to compromise a network’s security. When you perform a network attack, you can utilize a user’s account and the privileges that are attached to it, steal or modify stored data, run a code to corrupt a system or data, or prevent an authorized user from accessing a service.

### Reconnaissance

Hacking a system begins with the discovery of strategic vulnerabilities in a network before launching any cyber-attack. You can think of this as a hacker’s research about their targets. Anyone can be a hacker’s target, which means that learning how hackers perform reconnaissance means being able to protect your system as well. Whenever you connect to the internet and send data over the web, you are leaving behind footprints that hackers can trace back to you. When that happens, hackers may want to study your activities over your network and discover vulnerabilities in your system that will make it easier for them to infiltrate and steal data that can be of value to them.

Here, you will learn how to build simple scripts that will allow you to scan your target’s vulnerable TCP ports. To interact with these open ports, you will also need to create TCP sockets. Python is one of the modern programming languages that allow you to gain access to BSD socket interfaces. By doing a series of socket API utilities, you will be able to connect, listen, create, bind, or send traffic on a target’s TCP/IP sockets. If you can know the IP address and the TCP ports that are associated with the service that you want to target, then you can better plan your attack. Most of the time, this information is available to system administrators in an organization, and this data is also something that admins need to hide from any attacker. Before you can launch an attack on any network, you will need to gain this information first.

### Making Your Port Scanner

Port scanning is a method in which you can assess which of the ports in a targeted computer is open, and what kind of service is running on that specific port. Since computers are operating to communicate with other devices and perform a function by opening a port to send and receive data, open ports can be a vulnerability that hackers will want to exploit. Think of an open port to be similar to an open window to a burglar – these open ports serve as a free passage to any hacker that will want to steal data or set up shop inside a computer to exploit its weaknesses for an extended amount of time. Understand that port scanning is not an illegal activity to do. Network security personnel scan the ports of client computers to learn about their vulnerabilities and apply the security protocol needed.

However, port scanning is also the best way for any hacker to discover new victims and find out the best way to hack their system. At the same time, repetitive port scans can also cause a denial of service, which means that a legitimate user may not be able to use a particular networking service due to the ports exhausting their resources. A port scanner will allow you to look at the hosts and the services that are attached to them. As you may already know, sockets are behind anything that involves network communications. When you pull up a web browser, your computer opens a socket to communicate to a web server. The same thing happens when you communicate with other computers online or send a request to your printer over your Wi-Fi.

### Perform Anonymous Reconnaissance Using the Mechanize Library

Most computer users use a web browser to navigate websites and view content over the Internet. Each website has different features, but will usually read a particular text document, analyze it, and then display it to a user, just like the way a source file interacts with the Python interpreter. Using Python, you can browse the Internet by getting and parsing the HTML source code of a website. Different libraries come with this programming language that can handle Web content, but for this hack, you will be using Mechanize, which includes the primary class called Browser.

### Ensuring Anonymity While Browsing

Now that you know how to get a webpage, you will want to create a script that will allow you to retrieve information from a website anonymously. As you may already know, web servers see to it that they log the IP addresses of different users that view their sites to identify them. This can usually be prevented by using a virtual private network, or by using Tor. What happens when you use a VPN is that all traffic gets routed to the private network automatically. With this concept, you get the idea that you can use Python to connect to the proxy servers instead, which will give your program an added layer of anonymity.

### Wireless Attack: Dnspwn Attack

This attack is created by using the airpwn tool, which is a framework for packet injection for wireless 802.11. This tool is designed to listen to incoming packets and then inject content to the access point when the incoming data matches a pattern that is specified in the config file. To your target, your airpwn looks and behaves like the server that he is trying to communicate to. This tool was first created to target HTTP, but it can also be used to exploit DNS. In essence, using a dnspwn attack entails luring your target to visit a malicious webpage that will install malware to your target through download, or to spoof a particular website to steal your target’s credentials.

### One Final Note

To move beyond script-kiddie status, a hacker must master a scripting language, and Python is generally the right first choice for its versatility and relatively small learning curve. The majority of hacking tools are written in Python, including sqlmap, scapy, and many others. Here, you have learned some Python fundamentals you can use to build some useful, yet simple hacker tools, including a banner grabber and an FTP password cracker.

# Conclusion

May I take this opportunity to thank you for being able to make it to the end of Hacking With Kali Linux. Let’s hope it has been edifying and through it, you have been able to accrue the requisite knowledge to enable you begin your hacking career or improve your skills if you are already one. I sincerely hope that you have enjoyed flipping pages all the way from the first topic which was introduction to Kali Linux, all through vulnerability assessment, wireless network hacking, penetration testing, web security, text manipulation, cracking encryptions, advanced social engineering, to Python scripting basics for hackers. I am also hoping that by studying this book, you have learned plenty of practical concepts that you need to become a hacking expert.

By now, you must have been able to get access to a vast body of theoretical knowledge regarding the various types of attacks that can be launched on your systems, the reason for launching them and how you are able to safeguard your infrastructure against such attacks. These are your first steps towards becoming a professional hacker. The book covers topical issues like wireless network attacks, cyber attacks and penetration testing, among others. Therefore, it means that you are now in a good position to discern network attack mechanisms being perpetrated in the real world and recommend appropriate remedial measures.

I have also given you a variety of security measures that you can implement to ensure your networks are safe and protected. The formatting is such that the language is user-friendly language that you are able to understand the importance of securing your networks. Going forward, the next step is to put the concepts you have acquired from this book into practice. They say practice makes perfect and it is by practicing that one is able to become a master in the field of hacking, more so using Kali Linux. Let the knowledge you have acquired from the book work for you.

Finally, if you found this book useful in any way, a review on Amazon is always appreciated!