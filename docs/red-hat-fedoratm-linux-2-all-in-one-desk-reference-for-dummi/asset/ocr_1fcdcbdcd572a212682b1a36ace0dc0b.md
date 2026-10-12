+   - Third-party network providers (ISPs, long-distance carriers) with looser security
+   - Operating-system security holes (potential holes in Internet servers, such as those associated with sendmail, named, bind, and so on)
+   - Application security holes (known security holes in specific applications)

# The 1-2-3 of risk analysis (probability and impact)

To perform risk analysis, assign a numeric value to the probability and impact of each potential vulnerability. To develop a workable risk analysis, do the following for each vulnerability or risk:

+   1. Assign subjective ratings of Low, Medium, and High for the probability. As the ratings suggest, Low probability means a lesser chance that the vulnerability will be exploited; High probability means a greater chance.
+   2. Assign similar ratings to impact. What you consider impact is up to you. If the exploitation of a vulnerability will affect your business greatly, assign it a High impact.
+   3. Assign a numeric value to the three levels — Low = 1, Medium = 2, and High = 3 — for both probability and impact.
+   4. Multiply the probability by the impact — you can think of this product as the risk level. Then make a decision to develop protections for vulnerabilities that exceed a specific threshold for the product of probability and impact. For example, you may choose to handle all vulnerabilities with a probability-times-impact greater than 6.

If you want to characterize the probability and impact with finer gradations, pick a scale of 1 through 5 (for example) instead of 1 through 3, and follow the same steps as before.

# Establish security policy

Using risk analysis and any business requirements you may have to address (regardless of risk level) as a foundation, you can craft a security policy for the organization. The security policy typically addresses the following areas:

+   - **Authentication**: What method is used to ensure that a user is the real user? Who gets access to the system? What is the minimum length and complexity of passwords? How often do users change passwords? How long can a user be idle before that user is logged out automatically?
+   - **Authorization**: What can different classes of users do on the system? Who can have the root password?
+   - **Data protection**: What data must be protected? Who has access to the data? Is encryption necessary for some data?