# Types of patches

Let's review the different types of updates available for Windows-based systems.

Take into consideration that to help you prioritize the deployment, they include a categorization based on importance (from a cybersecurity point of view).

The categories are Critical (meaning they must be installed ASAP), Required (must be prioritized on the upcoming patching window), and Minor (optional updates). These updates are explained in more detail here:

+   * Update: A fix to a specific problem that is considered non-security-related bug. Since a lack of this update will not impact the performance or security of the server, these updates are considered of minor importance.

+   * Critical update: This aims to fix a specific non-security-related bug. Normally, this is released to a wide audience of users. Even if this is not security-related, it may fix some issues related to performance and stability, and therefore this should be considered critical.

+   * Definition update: This is normally a software update that contains additions to a product's definition database. As seen in the following screenshot, these definition databases are often to prevent attacks resulting from malicious code, phishing websites, or junk mail:

# Windows Update

+   - Definition Updates (2)

| Security Intelligence Update for Microsoft Defender Antivirus - KB2267602 (Version 1.325.939.0) |
| Successfully installed on 10/16/2020 |
| Security Intelligence Update for Microsoft Defender Antivirus - KB2267602 (Version 1.325.867.0) |
| Successfully installed on 10/16/2020 |

> Figure 6.8 – Windows definition updates

Since some of them could prevent some known security attack vectors, they are considered a critical update.

+   * Security update: This update aims to fix a product-specific, security-related vulnerability.

Normally, those vulnerabilities are rated by their severity as critical, important, moderate, or low, as indicated in the Microsoft security bulletin.