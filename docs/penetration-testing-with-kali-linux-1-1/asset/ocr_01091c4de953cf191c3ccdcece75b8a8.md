Next, we will open up a new tab and visit http://10.5.5.25:8080

![](bbox=[0.13, 0.145, 0.87, 0.205])

![](bbox=[0.25, 0.23, 0.75, 0.53])

*Figure 354: Visiting 10.5.5.25 on Port 8080*

The page that opens up is a Jenkins⁷⁴⁵ login page. This is a very interesting target as Jenkins is an extremely powerful piece of software that might expose some attack surface. Therefore, we will concentrate our efforts on this host next.

# 24.8 Targeting the Jenkins Server

Jenkins is an automation server that can be used to automate a number of tasks related to software development.⁷⁴⁶ Because of their nature, continuous integration and delivery tools like Jenkins are usually able to execute code. This is necessary in order to set up custom repeatable tasks triggered by specific events or actions.

A common use case for a tool like Jenkins is to pull a git repo after a commit is pushed, run a set of tests to ensure nothing broke in the application during the change, and, if everything succeeds, merge the new code into the master branch. In order to do this, Jenkins needs to have the ability

+   ⁷⁴⁵ (Wikipedia, 2019). https://en.wikipedia.org/wiki/Jenkins_(software)
+   ⁷⁴⁶ (Continuous Delivery Foundation, 2020). https://jenkins.io/doc/