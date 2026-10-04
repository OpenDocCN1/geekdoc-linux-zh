# Inventory and Exposure of Corporate Assets · Chapter 2

WARNING
Many of the services running on your internal network will be there whether you like it or not. Internal network security can be difficult for that reason. The only way to handle this situation is to prioritize. Identify your most critical business operations and define their scope, as IP ranges and hosts. Then draw up a plan that details how much you can realistically manage to secure and keep secured. This plan should be based on the personnel and funds you have available.

# A Scenario Requiring Host Exposure Assessment

A recent security team meeting uncovered a nasty truth that you suspected for a while but had no resources to investigate. Development and the QA department replicated last month’s production data to the servers in the StagingTEST network. They did this because they needed to ensure a realistic testing scenario. The asset inventory you reviewed showed multiple systems in the network that were unpatched to allow for protect testing. Your hope was that they have used a device such as a screening router to keep peering eyes or "accidental" trespassers at bay. You need to examine each asset listed in the asset inventory’s exposure level from the CorpPlan.

Figure 2.12 shows System A and System B with an uncerstated visibility between them. System A is the workstation on CorpPlan and System B is in the StagingTEST network. The asset inventory you reviewed shows System B listed as a default installation of Red Hat 6.0 with all the common services running. Unless you understand the exposure that System A has to System B, and System B has to System A, you can’t determine the actual risk. Based on this scenario, System B’s high level of vulnerability actually putting corporate data at high risk of attack from CorpPlan in this scenario? Know exploits for these vulnerabilities are well distributed in the hacker community and very simple to execute. This verified for use that there was threat to this data. You need to examine the exposure level of the corporate assets in StagingTEST that are hosting this data.

# Figure 2.12 CorpPlan with Unknown Visibility to StagingTEST

![](bbox=[0.141, 0.833, 0.882, 0.969])