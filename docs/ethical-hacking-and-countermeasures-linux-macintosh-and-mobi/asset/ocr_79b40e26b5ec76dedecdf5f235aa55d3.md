The first line is simply a continuation of the original query; it contains a quote to start the SQL injection. The actual virus starts after the semicolon. On the second line, a variable named "@s" is created and initialized. It contains the code on the third line, in textual form.

# ### RFID Exploits

RFID exploits include SQL injection, client-side scripting, and buffer overflows.

# ### SQL Injection

RFID systems use databases to store information, which can be read from tags. Data read from the tags should be properly processed by middleware. Otherwise, there is a possibility of exploiting the database by executing the SQL code on the tag. This is called SQL injection.

# ### Client-Side Scripting

User interfaces and query databases are provided by middleware systems using Web-based components. Web browsers show the attacks caused directly or indirectly through the database. Modern Web browsers have dynamic features that are misused for writing JavaScript code on the tag. This is called client-side scripting.

# ### Buffer Overflows

If too much data is read from the limited memory of the RFID tag, a buffer overflow occurs. The code that binds the RFID reader interface with middleware is written in a low-level language such as C or C++, which are vulnerable to buffer overflows.

# ## RFD Hacking Tool

The RFD hacking tool RFDump can be used to exploit RFID tag information.

# ### RFDump

RFDump is a back-end GPL (General Public License) tool that works directly with any RFID ISO-Reader to make the content stored on the RFID tags accessible. It can be used to read and display all metadata (tag ID, tag type, and manufacturer) within an RFID tag. The user data memory can also be displayed and modified using a text or hex editor. In addition, the integrated cookie feature demonstrates how easy it is for a company to abuse RFID technology to spy on their customers. It works with the ACG Multi-Tag Reader or similar card-reader hardware.

Figure 6-1 shows the interface for the RFDump tool.

# ## RFID Security Controls

# ### Management Controls

Management controls are typically involved in risk assessment, system planning, and system acquisition, as well as security certifications, accreditations, and assessments.

# ### RFID Usage Policy

+   Benefits: The policy establishes the framework for many other security controls. It provides a vehicle for management to communicate its expectations regarding the RFID system and its security. It enables management to take legal or disciplinary action against individuals or entities that do not comply with the policy.

+   Weaknesses: The existence of a policy does not ensure compliance with the policy. A policy needs to be coupled with the implementation and enforcement of appropriate operational and technical controls to be effective.

# ### IT Security Policies

Control: IT security policies describe the approach to achieve high-level security objectives of the usage policy. The IT security policies related to the RFID should cover each RFID subsystem, including network, database and application security in the enterprise, and interenterprise subsystems. They should not just be limited to the security of the tags and readers in the RF subsystem.