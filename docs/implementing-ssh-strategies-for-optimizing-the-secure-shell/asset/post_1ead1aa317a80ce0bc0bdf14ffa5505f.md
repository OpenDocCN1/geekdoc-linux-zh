
# Implementing SSH
Strategies for Optimizing the Secure Shell

![](img/c99d6f526a5f9fa62f2c34daada85ad7_0_0.png)
![](img/c99d6f526a5f9fa62f2c34daada85ad7_0_1.png)

Himanshu Dwivedi

## Implementing SSH®
Strategies for Optimizing the Secure Shell

Himanshu Dwivedi

![](img/c99d6f526a5f9fa62f2c34daada85ad7_1_0.png)

### Implementing SSH®
Strategies for Optimizing the Secure Shell

![](img/c99d6f526a5f9fa62f2c34daada85ad7_5_0.png)

## Implementing SSH®
Strategies for Optimizing
the Secure Shell

Himanshu Dwivedi

WILEY
Wiley Publishing, Inc.

Vice President and Executive Group Publisher: Richard Swadley
Vice President and Executive Publisher: Bob Ipsen
Vice President & Publisher: Joseph B. Wikert
Executive Editorial Director: Mary Bednarek
Executive Editor: Carol Long
Development Editor: Scott Amerman
Editorial Manager: Kathryn A. Malm
Production Editor: Felicia Robinson
Media Development Specialist: Travis Silvers
Permissions Editor: Laura Moss
Text Design & Composition: Wiley Composition Services

Copyright © 2004 by Wiley Publishing, Inc. All rights reserved.

Published by Wiley Publishing, Inc., Indianapolis, Indiana

Published simultaneously in Canada

No part of this publication may be reproduced, stored in a retrieval system, or transmitted in any form or by any means, electronic, mechanical, photocopying, recording, scanning, or otherwise, except as permitted under Section 107 or 108 of the 1976 United States Copyright Act, without either the prior written permission of the Publisher, or authorization through payment of the appropriate per-copy fee to the Copyright Clearance Center, Inc., 225 Rosewood Drive, Danvers, MA 01923, (978) 750-8400, fax (978) 646-8600. Requests to the Publisher for permission should be addressed to the Legal Department, Wiley Publishing, Inc., 10475 Crosspoint Blvd., Indianapolis, IN 46256, (317) 572-3447, fax (317) 572-4447, E-mail: permcoordinator@wiley.com.

Limit of Liability/Disclaimer of Warranty: While the publisher and author have used their best efforts in preparing this book, they make no representations or warranties with respect to the accuracy or completeness of the contents of this book and specifically disclaim any implied warranties of merchantability or fitness for a particular purpose. No warranty may be created or extended by sales representatives or written sales materials. The advice and strategies contained herein may not be suitable for your situation. You should consult with a professional where appropriate. Neither the publisher nor author shall be liable for any loss of profit or any other commercial damages, including but not limited to special, incidental, consequential, or other damages.

For general information on our other products and services please contact our Customer Care Department within the United States at (800) 762-2974, outside the United States at (317) 572-3993 or fax (317) 572-4002.

Trademarks: Wiley, the Wiley Publishing logo, and related trade dress are trademarks or registered trademarks of John Wiley & Sons, Inc. and/or its affiliates in the United States and other countries, and may not be used without written permission. All other trademarks are the property of their respective owners. Wiley Publishing, Inc. is not associated with any product or vendor mentioned in this book.

Wiley also publishes its books in a variety of electronic formats. Some content that appears in print may not be available in electronic books.

Library of Congress Control Number available from publisher.

ISBN: 0-471-45880-5

Printed in the United States of America
10 9 8 7 6 5 4 3 2 1

![](img/c99d6f526a5f9fa62f2c34daada85ad7_7_0.png)

## Dedication

This book is dedicated to my wife, Kusum. Without her, this book would not have been possible. Kusum, you are truly special to me.

I would like to especially thank my parents, Chandradhar and Prabha Dwivedi. Without their guidance, support, and inspiration, I would not be where I am today. Lastly, I would like to thank my brother and sister, Sudhan-shu and Neeraja Dwivedi, from whom I have learned every important lesson in life. Without their influence and experiences, I could not have learned so much.

I thank you and love you all very much.

## Contents

- Acknowledgments xv
- About the Author xvii
- Introduction xix
- Part 1 SSH Basics 1
- Chapter 1 Overview of SSH 3
  - Differences between SSH1 and SSH2 4
  - Various Uses of SSH 5
  - Security 5
  - Remote Command Line Execution 7
  - Remote File Transfer 8
  - Remote Network Access 10
  - Secure Management 10
  - Proxy Services 11
  - Client/Server Architecture for SSH 12
  - SSH’s Encryption Architecture 13
  - Basic Misues with SSH 14
  - Types of SSH Clients/Servers 14
  - Basic Setup of SSH 15
  - OpenSSH 16
  - Red Hat Linux 8.0 16
  - OpenBSD 3.1 18
  - Windows 2000 Server 19
  - Commercial SSH 23
  - OpenBSD 3.1 and Red Hat Linux 8.0 23
  - Windows 2000 24
  - VShell SSH Server 27
  - Optimal Uses of SSH 29
  - Summary 30

- Chapter 2 SSH Servers 31
  - OpenSSH 32
  - SSH Communications' SSH server 39
    - SSH Communications' SSH Server: Unix 39
      - General 40
      - Network 40
      - Crypto 42
      - Users 43
      - User Public Key Authentication 44
      - Tunneling 46
      - Authentication 46
      - Host Restrictions 47
      - Users Restrictions 48
      - SSH1 Compatibility 49
      - Chrooted Environment 50
      - Subsystem Definitions 50
    - SSH Communications' SSH server: Windows 51
      - General Settings 52
      - Network Settings 54
      - Crypto Settings 56
      - Users Settings 57
      - Server Public Key Configuration 60
      - Server Certificate Configurations 61
      - Tunneling Configurations 62
      - Authentication Methods 63
      - Host Restrictions 64
      - User Restrictions 65
      - Subsystem Definitions 67
  - VanDyke Software's VShell SSH Server 69
    - General Settings 69
    - General—Host Key 70
    - General—Key Exchanges 71
    - General—Cipher 72
    - General—MAC 73
    - General—Compression 74
    - Authentication 75
    - Access Control 77
    - SFTP Section 78
    - Triggers 79
    - Connection Filters 80
    - Port-Forward Filters 81
    - Logging 83
    - Comparison of OpenSSH, SSH Server, and VShell 84
    - Summary 85

- Chapter 3 Secure Shell Clients 87
  - Command-Line SSH Clients 88
    - Windows Installation 89
    - Unix Installation 89
    - SSH Client Configuration File 94
      - General 95
      - Network 95
      - Crypto 96
      - User Public Key Authentication 96
      - Tunneling 97
      - SSH1 Compatibility 97
      - Authentication 98
  - GUI SSH Clients 98
    - Windows Installation 98
    - SSH Communications 99
    - Profile Settings 100
    - Global Settings 101
    - VanDyke Software’s SecureCRT 104
    - PuTTY 110
    - WinSCP 112
    - MindTerm 113
    - MacSSH 116
    - Summary 116

- Chapter 4 Authentication 117
  - General Options 118
    - SSH Communications’ SSH Server (Windows) 118
    - SSH Communications’ SSH Server (Unix) 120
    - VShell SSH Server 121
    - OpenSSH (Unix and Windows) 122
  - Passwords 123
  - Host-Based Authentication 127
  - Server Authentication 129
  - Public Keys 131
    - Creating Keys with OpenSSH 134
    - How to Use an OpenSSH Key on an OpenSSH Server 135
    - How to Use an OpenSSH Key on SSH Communications’ SSH Server 136
    - How to Use an OpenSSH Key on a VShell SSH Server 137
    - Creating Keys with SSH Communications’ SSH Client 138
    - (Unix and Windows Command Line)
    - How to Use SSH Client Keys with SSH Communications’ SSH Server 139
    - How to Use SSH Client Keys with an OpenSSH Server 140
    - How to Use SSH Client Keys with a VShell SSH Server 140
