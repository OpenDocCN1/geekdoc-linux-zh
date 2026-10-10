
# Developing multiplatform desktop applications with .NET Core 3 and Visual Studio 2019

## Build C# GUI applications for macOS, Linux and Windows

- Avalonia
- Electron.NET
- GTK
- QT
- and many more ...

Dimitri Laslo

---

ALL RIGHTS RESERVED. NO PART OF THIS PUBLICATION MAY BE REPRODUCED, DISTRIBUTED, OR TRANSMITTED IN ANY FORM OR BY ANY MEANS, INCLUDING PHOTOCOPYING, RECORDING, OR OTHER ELECTRONIC OR MECHANICAL METHODS, WITHOUT THE PRIOR WRITTEN PERMISSION OF THE PUBLISHER, EXCEPT IN THE CASE OF BRIEF QUOTATIONS EMBODIED IN CRITICAL REVIEWS AND CERTAIN OTHER NONCOMMERCIAL USES PERMITTED BY COPYRIGHT LAW.

Although the author and publisher have made every effort to ensure that the information in this book was correct at press time, the author and publisher do not assume and hereby disclaim any liability to any party for any loss, damage, or disruption caused by errors or omissions, whether such errors or omissions result from negligence, accident, or any other cause.

This publication is meant as a source of valuable information for the reader, however it is not meant as a substitute for direct expert assistance. If such level of assistance is required, the services of a competent professional should be sought.

ALL TRADEMARKS, MARKS MENTIONED IN THIS BOOK, ARE PROPERTY OF THEIR RESPECTIVE OWNERS.

## Preamble

The present book offers a detailed review of the new technologies for the development of desktop GUI application with .NET Core 3. At the time this book is written the .NET Core 3 final version has just been released, and the impact on the .NET developer community is already huge. The perspectives offered by the use of this new major release of .NET Core expand its potential fields of application.

The subject is evolving very quickly but we are pretty confident that the technics and fundamentals presented will remain relevant for the next version of the Core framework (it should be the 3.1 according to the Microsoft roadmap).

.NET Core 3 is a major step for the Microsoft’s developer community and its integration in Visual Studio 2019 seems to indicate that it will become the main development technology of the Redmond editor for the coming years.

Be assure that we will follow the future versions of these developments to keep you up to date with this, always evolving, amazing technology.

## TABLE OF CONTENTS

Target public for this book....................................................10
How to read that book......................................................11
Technical options.............................................................12
Technical notations.........................................................13

### Chapter 1. Introduction.................................................15
- 1.1 General overview.....................................................15
- 1.2 Why develop multiplatform apps?....................................18

### Chapter 2. Presentation of .NET Core 3................................22
- 2.1 Little historic of the Microsoft .NET framework..............22
- 2.2 Why .NET Core?.....................................................25
- 2.3 New Features...........................................................27
- 2.4 .NET Core 3 Roadmap..................................................30

### Chapter 3. Projects managements essentials........................34
- 3.1 The planification of your project...................................35
- 3.2 The Software Development Life Cycle...............................37
- 3.3 Define multiple environments.........................................40
- 3.4 Source control................................................................41

### Chapter 4. GUI development best practices: User eXperience 45
- 4.1 Best practices for interface definition.............................47
- 4.2 General screen design and ergonomic concepts....................49
- 4.3 Layout recommandations..............................................50
  - 4.3.3 Sketch the application window. 54
  - 4.3.4 Typography. 56
  - 4.3.5 Color scheme. 57
- 4.4 The challenge for multiplatform GUI design 58

### Chapter 5. Basic coding techniques for C# application 60
- 5.1 Application Configuration . 61
- 5.2 Logging and Tracing. 65
  - 5.2.1 Microsoft .NET Core logging system 66
  - 5.2.2 Advanced structured logging system: Serilog. 67
- 5.3 Data access: Entity Framework Core . 71
  - 5.3.1 Database Provider 72
  - 5.3.2 Architecture of the EF Core . 72
  - 5.3.3 EF Core Installation 73
  - 5.3.4 Data model 74
  - 5.3.5 Recommendations for the use of EF Core 76
  - 5.3.6 Basic sample usage of EF core 77
  - 5.3.7 Entity Framework Core: tutorials and learning. 80
- 5.4 External Services Consumption. 81
  - 5.4.1 Building the Web request . 82
  - 5.4.2 Processing the request and retrieve data. 82
  - 5.4.3 Processing JSON result 82
  - 5.4.4 Sample code for a REST client 83
- 5.5 Threading GUI . 84
- 5.6 Using unmanaged dependencies 86
  - 5.6.1 P/Invoke ...87
  - 5.6.2 Marshalling ...89
  - 5.6.3 OS detection and identification ...91

### Chapter 6. Setup development environment ...94
- 6.1 Create developer account for each platform you target ...95
- 6.2 Physical computer Vs virtual machine ...97
- 6.3 Multiplatform development environment architecture ...98
- 6.4 .NET Core 3 install: Runtime or SDK? ...99
  - 6.4.1 On Windows ...101
  - 6.4.2 On Linux Ubuntu (or other Debian distribution) ...102
  - 6.4.3 On macOS Mojave ...104
- 6.5 Install development stations ...106
  - 6.5.1 The Windows station (main) ...106
  - 6.5.2 The Linux station ...109
  - 6.5.3 The macOS station ...110
- 6.6 Configuration for remote debugging ...111
- 6.7 Setup target test machine ...115

### Chapter 7. Testing your program ...116
- 7.1 Unit testing ...117
  - 7.1.1 What to test? ...118
  - 7.1.2 MSTest (Visual Studio test framework) ...118
  - 7.1.3 Mock concept ...123
- 7.2 Functional testing ...126

### Chapter 8. Multiplatform Development solutions ...128
- 8.1 Choose the multiplatform application type: The right tool for the job. 129
- 8.2 Console GUI applications. 130
  - 8.2.1 What is Terminal.GUI ? 133
  - 8.2.2 Terminal.GUI screen design. 135
  - 8.2.3 Console GUI example applications... 137
  - 8.2.4 Pro/cons console GUI... 146
- 8.3 Electron.NET: ASP.NET GUI applications. 147
  - 8.3.1 What is Electron? 148
  - 8.3.2 Presentation Electron.NET. 148
  - 8.3.3 Setup of NPM and Node.JS. 150
  - 8.3.4 Electron.NET QuickStart.... 155
  - 8.3.5 Electron.NET application example. 158
  - 8.3.6 Pro/cons Electron.NET application. 165
- 8.4 C++ native GUI applications. 166
  - 8.4.1 Presentation of LibUI. 169
  - 8.4.2 .NET Core wrapper for LibUI. 170
  - 8.4.3 Form/Screen Design... 173
  - 8.4.4 Sample Projects.... 175
  - 8.4.5 Review of LibUI based .NET Core 3 application 182
- 8.5 GTK GUI applications. 182
  - 8.5.1 Presentation of GTK.... 183
  - 8.5.2 GTK Install. 186
  - 8.5.3 Presentation of GTK#. 196
  - 8.5.4 Glade: The user interface designer. 200
  - 8.5.5 GTK# samples applications...................206
  - 8.5.6 GTK Themes: Installation and Configuration.............215
  - 8.5.7 Recommendations for Gtk application development 216
- 8.6 QT/QML GUI applications............................217
  - 8.6.1 QT presentation...................................218
  - 8.6.2 Presentation of QML.NET.........................220
  - 8.6.3 QT Design Studio...................................224
  - 8.6.4 Using Photoshop resources as GUI..................226
  - 8.6.5 Samples program GUI with QML.NET.................229
- 8.7 Avalonia GUI applications (XAML)........................246
  - 8.7.1 What is Avalonia?....................................246
  - 8.7.2 Avalonia Visual Studio Extension...................247
  - 8.7.3 Avalonia Studio.......................................249
  - 8.7.4 Avalonia ThemeEditor..................................251
  - 8.7.5 Sample GUI program with Avalonia...................252
- 8.8 Comparison of the solutions reviewed...................259

### Chapter 9. Compilation and Build with .NET Core 3................261
- 9.1 .NET Core CLI local tools...............................264
- 9.2 .NET Core CLI building options.........................265
  - 9.2.1 dotnet build.........................................266
  - 9.2.2 dotnet publish........................................266
- 9.3 Structures of the CSPROJ file..........................268
- 9.4 CoreRT (Ahead Of Time) compilation....................274
  - 9.4.1 Architecture..........................................275
