
# Contents

- Foreword xv
- Preface xix
- About the Authors xxi

## PART I INTRODUCTION 1

### Chapter One Understanding the LSB 3

- 1.1 Background 3
- 1.2 The Value of Standards 4
- 1.3 The Free Standards Group 5
- 1.4 Organizational Structure of the LSB 5
    - 1.4.1 Chair 5
    - 1.4.2 Election Committee 6
    - 1.4.3 Steering Committee 7
    - 1.4.4 Project Manager/Release Manager 7
- 1.5 LSB Specification Overview 7
- 1.6 Benefits for Application Developers 8
    - 1.6.1 Increasing Confidence in Your Application 8
    - 1.6.2 Reducing Expenses 9
    - 1.6.3 Enhancing Market Opportunities 9
- 1.7 Benefits for Users 10
- 1.8 Benefits for Distributions 10
- 1.9 Brief History of the LSB Project 10

### Chapter Two Ensuring Binary Compatibility 13

- 2.1 Illustration of Binary Compatibility 13
    - 2.1.1 Coding to the Portability Layer 14
    - 2.1.2 Using the Correct ABIs 15
    - 2.1.3 Testing with the LSB Application Checker 16
    - 2.1.4 Following LSB Packaging Guidelines 17
    - 2.1.5 Seeking LSB Certification 18
- 2.2 Source Code Standards 19
    - 2.2.1 POSIX 19
    - 2.2.2 Single UNIX Specification 21
- 2.3 Binary Standards 22
- 2.4 LSB Binary Compatibility 23
    - 2.4.1 Binary versus Source Compatibility 23
    - 2.4.2 Coding Compatible Applications 23
    - 2.4.3 Looking Forward 24
    - 2.4.4 Value Proposition 24
    - 2.4.5 Shrink-Wrapped Applications 24

## PART II DEVELOPING LSB APPLICATIONS 25

### Chapter Three Using LSB Coding Practices 27

- 3.1 C and C++ 27
- 3.2 Internationalization 28
- 3.3 PAM 30
- 3.4 Java 31
- 3.5 kill(3) 31
- 3.6 ioctl(3) 31
- 3.7 IP Information 32
- 3.8 O_LARGEFILE 33
- 3.9 EISDIR(3) 34
- 3.10 waitpid(3) 35
- 3.11 Parsing of Command Options 35
- 3.12 LSB Don'ts 35
    - 3.12.1 /proc 35
    - 3.12.2 Berkeley Database 38
    - 3.12.3 Kernel 38
    - 3.12.4 Drivers 38
    - 3.12.5 Desktop 39
    - 3.12.6 Threads 39
    - 3.12.7 gets(3) 39
    - 3.12.8 system(3) 39
    - 3.12.9 ncurses 39
    - 3.12.10 malloc(3) 40

### Chapter Four Packaging Your LSB Application 41

- 4.1 Using RPM for Packaging 41
    - 4.1.1 RPM Checking 42
- 4.2 Installing Your Application in the Right Place 42
- 4.3 Package Naming 44
    - 4.3.1 Init Script Naming 44
    - 4.3.2 Cron Script Naming 45
- 4.4 Example: Packaging and Installing an Application 45
- 4.5 Advanced Packaging 48
    - 4.5.1 Packaging Multiple Products 48
    - 4.5.2 Packaging for Multiple Architectures 49
    - 4.5.3 Packaging Multiple Product Versions 50
    - 4.5.4 Packaging Multiple Versions of Multiple Products for Multiple Architectures 51

### Chapter Five Migrating Solaris Applications to Linux 53

- 5.1 Roadmap to Port 53
    - 5.1.1 Step 1: Obtain the Necessary Linux Distributions 54
    - 5.1.2 Step 2: Download the Necessary GNU Tools 54
    - 5.1.3 Step 3: Build the C/C++ Applications on Solaris 55
    - 5.1.4 Step 4: Build the Application on Linux for the Target Platform 57
- 5.2 Issues with Porting 57
    - 5.2.1 Byte Ordering 57
- 5.3 Signal Handling 60
- 5.4 Runtime Libraries 63
- 5.5 Filesystems 64
- 5.6 Threads 64
- 5.7 Absolute Addresses 65
- 5.8 Padding 65
- 5.9 Toolset 66
    - 5.9.1 C/C++ Resources 66

## PART III CERTIFYING FOR THE LSB 71

### Chapter Six LSB Certification for Linux Distributions 73

- 6.1 Introduction 73
    - 6.1.1 Highlights 74
- 6.2 Achieving LSB Certification 74
    - 6.2.1 Understanding the Certification Program 75
    - 6.2.2 Confidentiality 76
    - 6.2.3 Informal Testing 76
    - 6.2.4 Certification 77
    - 6.2.5 The Trademark License Agreement 78
    - 6.2.6 The Certification Agreement 78
- 6.3 Product Registration 79
    - 6.3.1 The Trademark License Agreement 79
    - 6.3.2 The Conformance Statement 79
    - 6.3.3 Submitting Initial Certification Information 80
    - 6.3.4 Registering Your Product within the Web Certification System 81
    - 6.3.5 Uploading Your Conformance Statement 82
    - 6.3.6 Formal Testing for Certification 82
    - 6.3.7 Confirming Your Submission 85
    - 6.3.8 Completion of Certification 86
    - 6.3.9 Appeals Process 87
- 6.4 Renewals and Certified Product Updates 87
    - 6.4.1 The Renewals Process 87
    - 6.4.2 Certified Product Updates 87
- 6.5 Currently Supported Systems 89
    - 6.5.1 Summary of Web References 89

### Chapter Seven LSB Certification for Software Products 91

- 7.1 Introduction 91
    - 7.1.1 Highlights 92
- 7.2 Achieving LSB Application Certification 92
    - 7.2.1 Understanding the Certification Program 93
    - 7.2.2 Informal Testing 93
    - 7.2.3 Registering an LSB Application Product within the Web Certification System 96
    - 7.2.4 Uploading a Conformance Statement 97
    - 7.2.5 Formal Testing for LSB Application Certification 97
    - 7.2.6 Completion of Certification 98
- 7.3 Currently Supported Systems 99
    - 7.3.1 Summary of Web References 99

## PART IV CONTRIBUTING TO THE LSB PROJECT 101

### Chapter Eight Adding New Interfaces to the LSB Written Specification 103

- 8.1 Moving Forward 103
- 8.2 LSB Selection Criteria 104
    - 8.2.1 Phase 1: Identification 104
    - 8.2.2 Phase 2: Investigation 105
    - 8.2.3 Phase 3: Implementation 106
    - 8.2.4 Final Steps 107
- 8.3 Candidate Identification 107
    - 8.3.1 Input from Specification Audience 107
    - 8.3.2 Analysis of Existing Code 108
    - 8.3.3 Standards Ideas 108
- 8.4 Candidate Tracking 109
- 8.5 Problem Cases 109
    - 8.5.1 Linux Specific Requests 109
    - 8.5.2 Interpreted Languages 110
    - 8.5.3 License Issues 110
- 8.6 How to Get Your Favorite Interface Added to the LSB 111

### Chapter Nine Adding New Architectures to the LSB Portfolio 113

- 9.1 Architecture-Specific Supplement 113
- 9.2 Architecture-Specific ELF 114
- 9.3 Architecture-Specific Symbol Versions 114
- 9.4 Architecture-Specific Headers 115
- 9.5 Architecture-Specific Packaging 115
- 9.6 Architecture-Specific Sample Implementation 116
- 9.7 Architectural Checklist 116

## PART V USING LSB RESOURCES 119

### Chapter Ten Using the LSB Written Specification 121

- 10.1 Understanding the LSB Written Specification 121
- 10.2 Product Standard Descriptions 123
- 10.3 Specification Module Descriptions 123
- 10.4 Functional Area Descriptions 124
- 10.5 Specification Amalgamation 125
- 10.6 Expanding the LSB Written Specification 126
- 10.7 Downloading the LSB Written Specification 127

### Chapter Eleven Using the LSB Test Suites 129

- 11.1 Understanding the LSB Test Suites 129
    - 11.1.1 TET-Based Tests 129
    - 11.1.2 Non-TET-Based Tests 130
- 11.2 Using TET-Based Tests 131
    - 11.2.1 Directory Hierarchy Description 131
    - 11.2.2 Installing lsb-runtime-test 133
    - 11.2.3 Running lsb-runtime-test 133
    - 11.2.4 Interpreting TET-Based Test Results 134
    - 11.2.5 Debugging TET-Based Test Suites 137
    - 11.2.6 Installing the Source of lsb-runtime-test 142
    - 11.2.7 Configuring lsb-runtime-test 143
    - 11.2.8 Building lsb-runtime-test 144
- 11.3 Using Non-TET-Based Tests 145
    - 11.3.1 Using lslblchek 145
    - 11.3.2 Using lsb-test-pam 147
- 11.4 Expanding the LSB Test Suites 149
    - 11.4.1 Criteria for New Test Suites 149
    - 11.4.2 Writing TET-Based Test Suites 151
    - 11.4.3 Converting Existing Test Suites to Use the TET/VSXgen 152
- 11.5 Downloading the LSB Test Suites 153

### Chapter Twelve Using the Sample Implementation 155

- 12.1 Understanding the Sample Implementation 155
- 12.2 Setting Up the Sample Implementation 156
    - 12.2.1 Sample Implementation Using chroot(1) 157
    - 12.2.2 Sample Implementation Using UML 160
    - 12.2.3 Using a Bootable Sample Implementation 161
    - 12.2.4 Sample Implementation Using Knoppix 163
- 12.3 Application Testing Using the Sample Implementation 163
- 12.4 Building the Sample Implementation 164
    - 12.4.1 Sample Implementation Build Process 167
    - 12.4.2 Sample Implementation Build Steps 168
- 12.5 Testing the Sample Implementation 169
- 12.6 Packaging the Sample Implementation 171
- 12.7 Downloading the Sample Implementation 172

### Chapter Thirteen Using the LSB Development Environment 175

- 13.1 Understanding the LSB Development Environment 175
- 13.2 Getting the LSB Development Environment 176
- 13.3 Using the LSB Development Environment 176
    - 13.3.1 LSB Shared Stub Libraries 176
    - 13.3.2 LSB Header Files 177
    - 13.3.3 Using the Development Tools 177
- 13.4 Shared Libraries 182
- 13.5 Case Study: rsync 183
    - 13.5.1 Building an rsync Binary with lsbcc 183
    - 13.5.2 Checking the Binary 186
    - 13.5.3 FHS Issues 187
    - 13.5.4 Further Examples 187
- 13.6 Building the LSB Development Environment 188
- 13.7 Expanding the LSB Development Environment 188
