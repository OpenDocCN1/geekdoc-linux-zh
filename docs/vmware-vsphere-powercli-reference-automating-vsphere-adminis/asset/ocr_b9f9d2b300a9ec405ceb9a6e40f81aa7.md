# EXPLORING THE SRM CMDLETS

# 809

Last result was: Success

```
# cleanup after the test
Invoke-SrmPlanAction -RecoveryPlan $planName -Cleanup
Starting cleanup......DONE!
Cleanup result: Success
```

You can use this function, with its different actions, to execute a test followed by a cleanup in one simple, concise action. When you combine this with Windows scheduled tasks, as documented in Chapter 25, "Running Scripts," and a bit of extra code to send an email report, you can set up a planned test to occur at regular intervals, such as every Monday morning. This ensures that you always have a validated recovery plan. You can be confident in the event of an emergency, your services will come back online and remain available for your users.

We hope that this chapter has demonstrated some of the actions that are available using the SRM API in vSphere 5.5 and vSphere 6.0. As time goes on, VMware is sure to add more functionality, enabling further management of storage replication adapters, protection groups, and recovery plans. For now, it is a huge benefit to be able to automate adding and removing virtual machines from recovery plans, and testing those plans to ensure that, as your virtual empire grows, your infrastructure's ability to survive a disaster remains intact.

![](bbox=[0.903, 0.573, 0.958, 0.706])