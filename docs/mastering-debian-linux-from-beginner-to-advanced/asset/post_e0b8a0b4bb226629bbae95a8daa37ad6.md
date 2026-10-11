
## 1. Debian will remain 100% free software
- All software in the main distribution must comply with the DFSG
- Debian will not make the system depend on non-free software

## 2. We will give back to the free software community
- Improvements and fixes will be submitted back to upstream projects
- Debian will contribute to the development and spread of free software

## 3. We will not hide problems
- Bug reports and security issues will be made publicly available
- Transparency is a key principle in Debian's operation

## 4. Our priorities are our users and free software
- The needs of users and the free software community guide Debian's decisions
- Debian strives to create a robust, high-quality operating system

## 5. Works that do not meet our free software standards
- Debian maintains separate areas for non-free software and contrib packages
- These areas are not part of the Debian system proper but are provided for users who may need them

## Debian Free Software Guidelines (DFSG)

The Debian Free Software Guidelines are a set of criteria that Debian uses to determine if a software package can be included in the main distribution. These guidelines are an integral part of the Social Contract and serve as a definition of "free software" in the context of Debian.

## Key Points of the DFSG

### 1. Free Redistribution
- The license must allow free redistribution of the software
- This includes selling or giving away the software as part of a larger distribution

### 2. Source Code
- The program must include source code and allow distribution in source code as well as compiled form
- If the product is distributed without source code, there must be a well-publicized means of obtaining the source code

### 3. Derived Works
- The license must allow modifications and derived works, and must allow them to be distributed under the same terms as the original software

### 4. Integrity of The Author’s Source Code
- The license may restrict source-code from being distributed in modified form only if the license allows the distribution of “patch files” with the source code for modifying the program at build time

### 5. No Discrimination Against Persons or Groups
- The license must not discriminate against any person or group of persons

### 6. No Discrimination Against Fields of Endeavor
- The license must not restrict anyone from making use of the program in a specific field of endeavor (e.g., business or genetic research)

### 7. Distribution of License
- The rights attached to the program must apply to all to whom the program is redistributed without the need for execution of an additional license

### 8. License Must Not Be Specific to Debian
- The rights attached to the program must not depend on the program being part of a Debian system

### 9. License Must Not Contaminate Other Software
- The license must not place restrictions on other software that is distributed along with the licensed software

## Impact and Significance

The Social Contract and DFSG have had a significant impact not only on Debian but on the broader free software community:
- They provide a clear ethical framework for the Debian project
- They have influenced other free software and open source projects and licenses
- The DFSG formed the basis for the Open Source Definition
- They help maintain Debian’s reputation for commitment to free software principles

## Applying the Social Contract and DFSG

In practice, these documents guide many aspects of Debian’s operations:
- **Package inclusion**: All packages in the main Debian repository must comply with the DFSG
- **Decision making**: Project decisions are made with consideration of the Social Contract
- **Community interaction**: The commitment to transparency and giving back shapes how Debian interacts with users and other projects
- **License evaluation**: New software licenses are evaluated against the DFSG to determine if they are free

## Challenges and Debates

While the Social Contract and DFSG provide clear guidelines, their application can sometimes lead to debates within the community:
- Interpretation of certain licenses and their compliance with the DFSG
- Balancing user needs with strict adherence to free software principles
- Handling of firmware and driver issues, especially for hardware support

These ongoing discussions help to keep the Debian project true to its principles while adapting to changing technological landscapes.

Understanding the Debian Social Contract and Free Software Guidelines is essential for anyone involved with Debian, as they form the philosophical and practical foundation of the project. They ensure that Debian remains a truly free operating system and continues to serve the interests of its users and the broader free software community.

## Working with the Debian Bug Tracking System

The Debian Bug Tracking System (BTS) is a critical component of Debian's quality assurance process. It allows users, developers, and maintainers to report, track, and resolve issues in Debian packages and the overall system. Understanding how to work with the BTS is essential for both users and contributors to Debian.

### Overview of the Debian BTS

The Debian BTS is a public, email-based system that tracks bugs and requests for improvement in Debian packages. Key features include:
- Each bug is assigned a unique number
- Bugs are categorized by severity, tags, and package
- All communication about a bug is publicly visible
- The system is integrated with Debian's mailing lists and web interface

### Reporting a Bug

Reporting bugs is an important way for users to contribute to Debian's quality. Here's how to report a bug effectively:

#### 1. Prepare Information
- Identify the affected package
- Gather system information (Debian version, architecture, etc.)
- Reproduce the issue and document the steps

#### 2. Use the reportbug Tool
- Install it with `sudo apt install reportbug`
- Run `reportbug package-name`
- Follow the prompts to provide necessary information

#### 3. Manual Reporting
- If you can't use `reportbug`, send an email to `submit@bugs.debian.org`
- Use a clear subject line: `Package: package-name`
- Include a detailed description of the issue in the body

#### 4. Provide Essential Information
- Debian version and architecture
- Package version
- Steps to reproduce the issue
- Expected vs. actual behavior
- Any relevant error messages or logs

### Bug Severity Levels

Understanding severity levels helps in appropriately categorizing bugs:
- **Critical**: Affects the whole system, causes data loss, or poses security risks
- **Grave**: Makes the package unusable or causes severe data loss
- **Serious**: Violates Debian policy or makes the package unsuitable for release
- **Important**: Major problems that don't render the package completely unusable
- **Normal**: Default severity for most bugs
- **Minor**: Minor issues that don't affect the package's usefulness
- **Wishlist**: Suggestions for new features or improvements

### Searching for Existing Bugs

Before reporting a new bug, it’s important to check if it’s already been reported:
1. Use the web interface at `https://bugs.debian.org`
2. Search by package name, bug number, or keywords
3. Check both open and closed bugs

### Working with Existing Bugs

Once a bug is reported, various actions can be taken:

#### Adding Information to a Bug
- Reply to the bug email or use the web interface
- Provide additional details, test results, or patches

#### Tagging Bugs

Tags help categorize and manage bugs. Common tags include:
- **patch:** A fix is included in the bug report
- **security:** Relates to a security issue
- **upstream:** The bug is present in the upstream source
- **pending:** A fix is ready but not yet applied

To add a tag, email `control@bugs.debian.org` with:
