select custom rules that are applied for the system evaluation by clicking this combo box. The default value is (no customization), which means that there are no changes to the used security policy. If you make any changes to the selected security profile, you can save those changes as an XML file by clicking the Save Customization Only item in the File menu.

# Profile

This combo box contains the name of the selected security profile. You can select the security profile from a given XCCDF or data-stream file by clicking this combo box. To create a new profile that inherits properties of the selected security profile, click the Customize button.

# Target

The two radio buttons enable you to select whether the system to be evaluated is a local or remote machine.

# Rules

This field displays a list of security rules that are subject of the security policy. Expanding a particular security rule provides detailed information about that rule.

# Status bar

This is a graphical bar that indicates status of an operation that is being performed.

# Generate remediation role

This pop-up menu enables you to export profile-based remediations to a file. This file contains all available fixes for all rules in the currently selected profile. You can choose the output as a Bash script, an Ansible playbook, or a Puppet manifest. A remediation performed during a system evaluation is based on bash remediations.

This feature enables you to examine individual remediations and possibly edit or cherry-pick them. Therefore, it puts you in full control over the remediation process.

# Dry run

Use this check box to get command line arguments to the diagnostics window instead of running the scan.

# Fetch remote resources

This check box allows to instruct the scanner to download a remote OVAL content defined in an XML file.

# Remediate

This check box enables the remediation feature during the system evaluation. If you check this box, SCAP Workbench attempts to correct system settings that failed to match the state defined by the policy.

# Scan

This button enables you to start the evaluation of the specified system.