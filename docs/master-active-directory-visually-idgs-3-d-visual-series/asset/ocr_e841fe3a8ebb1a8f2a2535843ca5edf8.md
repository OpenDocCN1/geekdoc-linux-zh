# TIPS

# What is a transitive trust?

A transitive trust is a feature of the Kerberos security protocol built into Windows 2000. A transitive trust is two-way between two domains. Also, Kerberos trusts are transitive—this means that a domain can automatically trust another domain without a direct trust relationship. For example, if Domain1 trusts Domain2 and Domain2 trusts Domain3, then Domain1 automatically trusts Domain3. Transitive trusts are automatically created for Active Directory domain controllers in a tree or forest. This is a new way of establishing trust relationships in Windows 2000; Windows NT did not allow any type of transitive trusts.

# What is a nontransitive trust?

Nontransitive trusts are trust relationships that do not support the Kerberos security protocol. Administrators on each side of the trust relationship must configure a nontransitive trust. If DomainA trusts DomainB, this doesn't mean that DomainB trusts DomainA as it does in a transitive trust relationship. Nontransitive trusts are also static. In other words, if DomainA trusts DomainB and DomainB trusts DomainC, DomainA does not automatically trust DomainC.

![](bbox=[0.01, 0.5, 0.97, 0.81])

+   * 1 On the Trusts tab, select a trust relationship and click Edit to see the properties page.
+   * 5 Click the SPN Suffixes tab.
+   * 6 Click Add.
+   * 7 Enter trusted SPN suffixes as desired.
+   * The properties sheet appears. The General tab gives you information about the trust relationship.