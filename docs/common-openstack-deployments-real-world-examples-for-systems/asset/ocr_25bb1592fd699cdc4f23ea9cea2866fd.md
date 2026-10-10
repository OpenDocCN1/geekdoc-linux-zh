instances, which we will want. We’ll also add a **rule** to allow TCP traffic over port 80 for when we set up a web server in a later step. We’ll start with allowing ICMP ping to the systems, as illustrated in Figure 6.5. Rather than allowing all ICMP traffic, which is an option in the Rule dropdown, we can create a custom ICMP rule to only allow ping. To do this, use the following values:

+   * **Rule:** Custom ICMP Rule
+   * **Direction:** Ingress
+   * **Type:** 8
+   * **Code:** 0
+   * **Remote:** CIDR
+   * **CIDR:** 0.0.0.0/0

The Type and Code are not obvious, but these come from RFC 792 which define this information for ICMP. With the rest of the options set we’re allowing traffic from anywhere to ping our instance. Click **Add** to add this to the list of rules.

The next two rules we want to add are easier, since they have default configurations already loaded. Click Add Rule again from the main screen and when the Add Rule screen shows up, go through the list in the Rule dropdown and select **HTTP**. Keep everything else at default and add this rule. Do the same for SSH. That is all you want to add to the Security Group at this time, but you now know how to adjust the rules for your

![](bbox=[0.15, 0.55, 0.85, 0.9])

Figure 6.5  Adding ICMP ping