
# 4 Patching Layer 8

Understanding layer 8 – the insider threat 112

- The inadvertent user 112
- The malicious insider 113
- How do you spot a malicious insider? 114
- Protecting your infrastructure against malicious insiders 115

# Mastering the art of social engineering 122

- The social engineering cycle 123
- Social engineering techniques 124
- Types of social engineering attacks 126

# Defending against social engineering attacks (patching layer 8) 140

- Creating your training strategy 141
- Admin rights 141
- Implementing a strong BYOD policy 142
- Performing random social engineering campaigns 142

# Summary 143

- Further reading 143

# 5 Cybersecurity Technologies and Tools

## Technical requirements 146

## Advanced wireless tools for cybersecurity 146

- Defending from wireless attacks 147

## Pentesting tools and methods 153

- Metasploit framework 153
- Social engineering toolkit 153
- exe2hex 158

## Applying forensics tools and methods 158

- Dealing with evidence 159
- Forensic tools 159
- Recovering deleted files 164

## Dealing with APTs 165

- Defensive techniques 166

## Leveraging security threat intelligence 167

- Threat intelligence 101 168
- Implementing threat intelligence 168

## Converting a threat into a solution 169

- The problem 169
- The solution 170

# Summary 170

- Further reading 171

# Section 2: Applying Defensive Security

## 6 Securing Windows Infrastructures

| Technical requirements | 176 | Mastering endpoint security | 193 |
| Applying Windows hardening | 176 | Windows updates | 193 |
| Hardening by the infrastructure team | 176 | Why move to Windows 10? | 194 |
| Creating a hardening checklist | 177 | Physical security | 194 |
| Creating a patching strategy | 182 | Antivirus solutions | 195 |
| The complexity of patching | 182 | Windows Defender Firewall | 196 |
| Distribution of tasks (patching roles and assignments) | 184 | Application control | 197 |
| Distribution and deployment of patches | 185 | URL filtering | 197 |
| Types of patches | 188 | Spam filtering | 197 |
| Applying security to AD | 190 | Client-facing systems | 198 |
| Secure administrative hosts | 192 | Backups | 198 |
| Windows Server Security documentation | 193 | Users | 199 |
| | Leveraging encryption | 199 |
| | Configuring BitLocker | 200 |
| | Summary | 201 |

## 7 Hardening a Unix Server

| Technical requirements | 204 | Changing default permissions with umask | 215 |
| Securing Unix services | 204 | Permissions hierarchy | 217 |
| Defining the purpose of the server | 205 | Comparing directory permissions | 218 |
| Secure startup configuration | 205 | Changing permissions and ownership of a single file | 219 |
| Managing services | 205 | Useful commands to search for unwanted permissions | 219 |
| Applying secure file permissions | 210 | Enhancing the protection of the server by improving your access controls | 221 |
| Understanding ownership and permissions | 210 | |
| Default permissions | 213 | | |
| Permissions in directories (folders) | 214 | |

# Table of Contents xi

- Viewing ACLs 221
- Managing ACLs 222
- Default ACL on directories 222
- Removing ACLs 223
- Enhanced access controls 224
- SSH brute-force protection with iptables 230
- Protecting from port scanning with iptables 230
- Advanced management of logs 231
- Leveraging the logs 232
## Configuring host-based firewalls 225

- Understanding iptables 225
- Configuring iptables 226
- Summary 232
- Further reading 233

## 8 Enhancing Your Network Defensive Skills

## Technical requirements 236

- Using the master tool of network mapping – Nmap 237
- Finding users using insecure protocols 260
- FTP, HTTP, and other unencrypted traffic 266
- Wireshark for defensive security 267
- Phases of a cyber attack 237
- Nmap 239
- Nmap scripts 242
- Working with IPS/IDS 268
- What is an IDS? 268
- What is an IPS? 269
- Free IDS/IPS 270
- IPS versus IDS 270
- Improving the protection of wireless networks 246
- Wireless network vulnerabilities 246
- User’s safety guide for wireless networks 250
- Summary 271

## 9 Deep Diving into Physical Security

## Technical requirements 274

- Understanding physical security and associated threats 274
- The amazing Screen Crab 277
- The advanced Key Croc 279
- USB threats 280
- Equipment theft 281
- Environmental risks 282
- The powerful LAN Turtle 274
- The stealthy Plunger Bug LAN Tap 275
- The dangerous Packet Squirrel 276
- The portable Shark Jack 277
- Physical security mechanisms 282
- Mastering physical security 284
- Clean desk policy 284
- Physical security audits 285
- Summary 286
- Further reading 286

## 10 Applying IoT Security

- Understanding the Internet of Things 288
- The risks 289
- The vulnerabilities 291
- Defensive security systems for industrial control systems (SCADA) 305
- Secure USB-to-USB copy machine 305
- Creating a $10 honeypot 306
- Advanced monitoring of web apps and networks 308
- Understanding IoT networking technologies 291
- LoRaWAN 292
- Zigbee 293
- Sigfox 294
- Bluetooth 295
- Security considerations 296
- Creating an internet ad blocker 309
- Access control and physical security systems 310
- > Bonus track – the danger of unauthorized IoT devices 311
- Detecting IoT devices 311
- Detecting a Raspberry Pi 312
- Disabling rogue Raspberry Pi devices 313
- Improving IoT security 297
- Creating cybersecurity hardware using IoT-enabled devices 300
- Raspberry Pi firewall and intrusion detection system 304
- Summary 313
- Further reading 313

## 11 Secure Development and Deployment on the Cloud

## Technical requirements 316

- Secure deployment and implementation of cloud applications 316
- Security by cloud models 316
- Data security in the cloud 318
- Cloud-native security 322
- Controlling access to the Kubernetes 323
- Controlling access to kubelet 323
- Preventing containers from loading unwanted kernel modules 323
- Restricting access to etcd 324
- Securing Kubernetes and APIs 321
- Avoiding the use of alpha or beta features in production 324

# Table of Contents xiii

- Third-party integrations 316
- AppDynamics 328
- Hardening database services 325
- Nessus scanner 329
- Testing your cloud security 326
- InsightVM 330
- Azure Security 327
- Intruder 331
- Amazon Cloud 327
- Summary 332
- Further reading 332

## 12 Mastering Web Security

## Technical requirements 334

- Exploring XSS attacks 347
- Gathering intelligence about your site/web application 335
- Using Burp Suite 350
- Importance of public data 335
- Setting up Burp Suite on Kali 351
- Open Source Intelligence 335
- SQL injection 352
- Hosting information 337
- Fixing a common error 358
- Checking data exposure with google dorks 339
- Leveraging DVWA 342
- Brute forcing web applications' passwords 359
- Installing DVWA on Kali 342
- Analyzing the results 363
- Overview the most common attacks on web applications 347
- Summary 364
- Further reading 364

# Section 3: Deep Dive into Defensive Security

## 13 Vulnerability Assessment Tools

Technical requirements 368

- Using a vulnerability scanner (OpenVAS) 372
- Dealing with vulnerabilities 368
- Who should be looking for vulnerabilities? 368
- Authenticated tests 373
- Bug bounty programs 369
- Installing OpenVAS 374
- Internal vulnerabilities 370
- Using OpenVAS 377
- Vulnerability testing tools 371
- Updating your feeds 379

# Table of Contents

| Overview of Nexpose Community | 380 | Summary | 383 |
| Further reading | 384 |

## 14 Malware Analysis

| Technical requirements Why should I analyze malware? | 386 | Fully automated analysis | 390 |
| Manual code reversing | 390 | |

| Best malware analysis tools | 391 | Malware functionality | 386 |
| Process Explorer | 391 | Malware objectives | 386 |
| Process Monitor | 392 | Malware connections | 387 |
| ProcDOT | 393 | Malware backdoors | 387 |
| Ghidra | 394 | Affected systems | 388 |
| PeStudio | 394 | |

| Types and categories of malware analysis | 388 | Performing malware analysis | 394 |
| Static malware analysis | 395 | Dynamic malware analysis | 396 |
| Hybrid malware analysis | 389 | Static properties analysis | 390 |
| Interactive behavior analysis | 390 |

| Summary | 400 | Further reading | 400 |

## 15 Leveraging Pentesting for Defensive Security

| Technical requirements Understanding of logs | 402 | Metasploit exploits | 407 |
| Installing Armitage | 408 | Configuring Metasploit for the first time | 408 |
| Log files | 402 | Installing Armitage (continued) | 409 |
| Log management | 403 | Exploring Armitage | 410 |
| Importance of logs | 405 | Launching an attack with Armitage | 413 |
| Executing Metasploit | 417 |

# Knowing your enemy's best friend – Metasploit

| Other offensive hacking tools | 421 | Metasploit | 406 |
| Searchploit | 421 |
