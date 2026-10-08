# # Tutorial

![](bbox=[0.07, 0.09, 0.87, 0.45])

![](bbox=[0.08, 0.48, 0.33, 0.63])

**04 Leave management**

The next section is the Leave section. When you go to the Leave tab, new subsections are visible: Entitlements, Reports, Configuration, Leave List and Leave Assignment. To set up Leaves, you can start with the Configuration tab.

Here you can create leave types (like sick, casual and more), list out holidays for the year, configure *one year durations with leave entitlements* as valid. After Configuration, you can then head over to the Entitlements section; this is the place to add leave entitlement to employees. Based on these entitlements and corresponding leave balances, employees can then apply their leaves. The Leave List section shows the leave data for the total leave period. The Assign Leave section allows the admin to grant leave without the employee applying for it.

**05 Time writing – attendance**

Attendance tracking is a very sensitive issue, even a small error in logging the in and out times can cause big problems (at least for the reputation of an employee). OranageHRM provides a neat way to track the attendance. Just head over to the *Time* tab and you can see the Attendance section inside. Here you can view employee attendance records or configure things like whether or not an employee or supervisor can modify the attendance records.

Note that if you're currently logged in as admin, and to log attendance then you should be logged in to the system as an ESS user. Just make a user with the ESS role and log in. After that, just go to *Time > Attendance > Punch in/out* and click In. The system automatically logs the date and time. The page refreshes to show the Out option now.

**06 Time writing – timesheets**

While attendance is used to track the actual hours spent in office, timesheets generally track the time spent on various activities inside the office, and the data is used for budgeting purposes. So before adding timesheets, you need to add customers and corresponding projects. Also, with each project the related activities should be added. To add these details, head over to *Time > Project Info > Customers*. After adding the customer, add projects using the Project link just below Customers – activities can also be added in the same page. Now you are ready to add timesheets. As an admin, you can add or view the timesheets of all the employees just by going to *Time > Timesheets > Employee Timesheets*. This page also shows the submitted timesheets, which have actions pending from your end. An ESS user can add and edit their timesheets using their own login.

![](bbox=[0.63, 0.56, 0.87, 0.68])

**07 Performance management – employer**

In this section we will have a look at how to set up performance management using the admin interface. The performance management in OranageHRM is based on KPIs, ie the key performance indicators. For every job title in the organisation, the corresponding KPIs, along with the maximum and minimum rating points, need to be created. Every employee can then be automatically evaluated based on the KPI of their job title. To select KPI go to *Performance > Add KPI*; You can select the job title and then add the KPI; the maximum and minimum ratings are optional but should be added to ensure uniformity in