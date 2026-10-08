# 70 Managing Threats, Vulnerabilities, and Risks

Defining the RTO is not a simple task because executives will always want to have this close to zero, but ultimately, the higher the cost associated. So, be realistic when defining this number to avoid shooting yourself on the foot.

Keep in mind that some executives will try to look for an overall RTO for the entire company. However, you should define RTOs at a lower level (by process, activity, department, or task) that will help you identify gaps or points in which more resources will be required to support it. For example, the RTO to restore the manufacturing line after a disaster must be the RTO to restore email services. In the following table, you can see how to map a service to the criticality of the data managed and the associated RTO and RPO:

| Service | Data Type | RPO | RTO |
|---|---|---|--|
| Transactional website | Critical for Business | 45 minutes | 1 to 2 minutes |
| VoIP | Required for Business | N/A | 10 minutes |
| Email | Important for Business | 1 to 5 minutes | 360 minutes |

Figure 2.16 – The RPO/RTO by the criticality of the data

Now, let's look at the other important metric, the recovery point objective (RPO).

# The recovery point objective (RPO)

This refers to how much data is acceptable after a disaster. In other words, how much data you need to recover after a disaster. However, here is the tricky part; even if we talk about data, that data is not measured in size but in time, so it is not about how many bits you recover, to which point in time you must recover the data. For example, if you have an email server, losing the emails received in the last hour may be acceptable, so an RPO of 1 hour is fine. In contrast, if you lose 1 hour of payment records, then that might not be acceptable. In that situation, the RPO will be between 1 and 10 seconds. In the following diagram, you can see the correlation between the RPO and the RTO:

![](bbox=[0.203, 0.706, 0.794, 0.831])

Figure 2.17 – An example of RPO and RTO