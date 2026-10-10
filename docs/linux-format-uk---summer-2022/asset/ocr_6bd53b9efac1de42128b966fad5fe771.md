# # ONeOffice plugins TUTORIALS

![](bbox=[0.35, 0.06, 0.9, 0.48])

+   - Go to **customize** bar. at 4 **customize** screens on left:
+     - **org.\*.org/office/document/Basic/Help\*/help\*/\*\*/\*/\*/\*\*/index.html**
+     - **http://wiki.openoffice.org/Confluence/Space/Basic\*/Help/\*/\*/\*/\*/\*/index.html**
+     - **https://openoffice.org/docs/Release/6.1/Help/en/help\\index.html**
+     - **https://api.openoffice.org/Confluence/Space/Basic\*/Help/\*/\*/\*/\*/\*/index.html**

# ## Install .oxt files

If you do not want to build, the best option is to download the .oxt file from the project page in [Gentoo Bugzilla](https://bugs.gentoo.org/show_bug.cgi?id=962548).

# ### Helper for .oxt files

**OfficeOxt** is a Python program that helps install .oxt files into OpenOffice. It supports all major versions of OpenOffice, and it works with both Windows and Linux. It is available from [OfficeOxt](http://www.librewriter.com) (version 2.1 or later).

# ### Manual installation

The manual installation process is:

1. **Extract** the .oxt file (which is just a zip file) into a folder
2. Create a new **extension folder** in your OpenOffice user profile: `~/.openoffice/share/extension` on Linux, or `%APPDATA%\OpenOffice\share\extension` on Windows
3. Copy the extracted contents into the new folder
4. Run the command `soffice --install --user-install --norestore` to install the extension

Note: If you use the `--norestore` flag, you can safely run the command from a script. Without it, you must run it from the command line.

# ## Enhancing data security

The `security` extension allows you to protect your documents by:

- **Encrypting** them with a password
- **Adding** a digital signature to verify authenticity
- **Tracking** changes with a log file
- **Disabling** printing or copying

![](bbox=[0.04, 0.86, 0.25, 0.95])

![](bbox=[0.26, 0.86, 0.47, 0.95])