Reporting bugs is an important way for users to contribute to Debian's quality. Here's how to report a bug effectively:

# 1. Prepare Information

+   - Identify the affected package
+   - Gather system information (Debian version, architecture, etc.)
+   - Reproduce the issue and document the steps

# 2. Use the reportbug Tool

+   - Install it with `sudo apt install reportbug`
+   - Run `reportbug package-name`
+   - Follow the prompts to provide necessary information

# 3. Manual Reporting

+   - If you can't use `reportbug`, send an email to `submit@bugs.debian.org`
+   - Use a clear subject line: `Package: package-name`
+   - Include a detailed description of the issue in the body

# 4. Provide Essential Information

+   - Debian version and architecture
+   - Package version
+   - Steps to reproduce the issue
+   - Expected vs. actual behavior
+   - Any relevant error messages or logs

# Bug Severity Levels

Understanding severity levels helps in appropriately categorizing bugs:

+   - **Critical**: Affects the whole system, causes data loss, or poses security risks
+   - **Grave**: Makes the package unusable or causes severe data loss
+   - **Serious**: Violates Debian policy or makes the package unsuitable for release