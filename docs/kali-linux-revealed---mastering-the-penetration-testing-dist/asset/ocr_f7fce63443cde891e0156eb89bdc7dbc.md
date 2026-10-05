these sorts of assessments and this is where you really take advantage of the many Kali Linux customization features. Many organizations that conduct these sorts of assessments will maintain highly customized versions of Kali Linux for internal use to speed up deployment of systems before a new assessment.

Customizations that organizations make to their Kali Linux installations will often include:

+   - Pre-installation of commercial packages with licensing information. For instance, you may have a package such as a commercial vulnerability scanner that you would like to use. Avoid having to install this package with each build, you can do it once^{21} and show it have up in every Kali deployment you do.
- Pre-configured connect-back virtual networks (VPN). These are very useful leave-behind devices that allow you to conduct "remote internal" assessments. In most cases, these systems will connect back to an assessor-controlled system, creating a tunnel that the assessor can use to access internal systems. Kali Linux ISO of Doom^{22} is an example of this exact type of customization.
- Pre-installed internally-developed software tools. Many organizations have private toolsets, setting these up once in a customized Kali install^{23} saves time.
- Pre-configured OS configurations such as hash settings, desktop wallpaper, proxy settings, etc. Many Kali users have specific settings^{24} they like to have tweaked just so. If you are going to do a re-deployment of Kali on a regular basis, capturing these changes makes a lot of

# 11.2.4. Application Assessment

While most assessments have a broad scope, an application assessment is a specialty that is narrowly focused on a single application. These sorts of assessments are becoming more common due to the complexity of mission-critical applications that organizations use, which of which are built in house. An application assessment is usually added to a broader assessment, as required. Applications that may be assessed in this manner, but are limited to

+   - Web applications: The most common externally-facing attack surface, web applications make great targets simply because they are accessible. Often, standard assessments find basic problems in web applications, however a more focused review is worth the time to identify issues relating to the workflow of the application. The kali-linux-web-package has a number of tools to help with these assessments.
- Compiled desktop applications: Server software is not the only target; desktop applications also make a wonderful attack surface. In years past, many desktop applications such as

> 21http://docs.kali.org/kali-dojo/02-mastering-live-build
22https://www.offensive-security.com/kali-linux/kali-rolling-a-custom-kali-iso
23http://docs.kali.org/development/live-build-a-custom-kali-iso
24http://www.offensive-security.com/kali-linux/kali-linux-recipes/