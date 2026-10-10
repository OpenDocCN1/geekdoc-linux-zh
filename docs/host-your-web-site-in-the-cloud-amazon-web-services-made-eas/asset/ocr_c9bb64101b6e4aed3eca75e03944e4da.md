power in advance of the flood. Right-click the DB Instance and select the **Modify** option; you'll be led to the screen shown in Figure 9.13.

![](bbox=[0.15, 0.15, 0.87, 0.56])

Figure 9.13. Scaling up a DB Instance

Select the new DB Instance Class and check **Apply Immediately**, then press the **OK** button. The state of the DB Instance will change to **modifying**, and a new entry will appear in the **Recent Events** tab to indicate that the Instance Class is being modified. Once the modification is complete, the state will be **available** and a corresponding event will appear. As you can see from my event log—shown in Figure 9.14—the entire scaling operation took just six minutes.