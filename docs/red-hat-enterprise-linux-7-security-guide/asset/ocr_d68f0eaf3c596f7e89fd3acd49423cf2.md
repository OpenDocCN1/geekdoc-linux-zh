- where the `results.xml` file contains results of the scan obtained when scanning with the `--results` option and the `result-id` option contains an ID of the `TestResult` component in the file with results. To obtain the ID of the `TestResult` component, use the `oscap_info` command on the `results.xml` file:

```
```
$ oscap_info results.xml | grep "Result ID"
```
```

To apply the Ansible playbook, enter the following command:

```
```
$ ansible-playbook playbook.yml
```
```

Note that the `ansible-playbook` command is provided by the `ansible` package. See the `ansible-playbook(1)` man page and the `Ansible Tower User Guide` for more information.

# Filtering Tasks

Tasks contained in playbooks are tagged with the same metadata as rules in an Extensible Configuration Checklist Description Format (XCCDF) file. These tags refer to rule ID, strategy, complexity, disruption, and references, and they can be used to filter the tasks to apply.

For example, to remediate only the rules from the PCI-DSS policy requirement 6.2, enter the following command:

```
```
$ ansible-playbook --tags=PCI-DSS-Req-6.2 /usr/share/scap-security-guide/ansible/ssg-rhel7-role-pci-dss.yml
```
```

To remediate only high-severity rules from the RHEL7 OSPP playbook that are not highly disruptive, enter the following command:

```
```
$ ansible-playbook --tags=high_severity --skip-tags=high_disruption /usr/share/scap-security-guide/ansible/ssg-rhel7-role-ospp-rhel7.yml
```
```

# Customizing Playbooks

You can choose between two approaches to customize your playbooks. The first is to generate playbooks from already customized profiles. This approach is better if a customization changes selected rules.

The second approach is just to change the variables in a playbook. This is the Ansible way to customize a playbook.

To generate Ansible playbooks for tailored profiles, use the `--profile` option to specify an ID of a customized profile, and use the `--tailoring-file` option to indicate where a tailoring file is located. These arguments are the same as when performing a scan using a tailored profile, for example:

```
```
$ oscap xccdf generate fix --fix-type ansible --profile xccdf_org.ssgproject.content_profile_common_customized --tailoring-file ssg-rhe17-ds-tailoring.xml --output tailored-playbook.yml /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml
```
```

To customize variables, use a text editor to edit a playbook. All used variables are listed at the beginning of a playbook, located after the `vars :` string.

# 7.8. USING OPENSCAP WITH RED HAT SATELLITE