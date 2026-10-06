# Chapter 1 • PLANNING YOUR ARCHITECTURE

+   1. Load-test current Web server architecture using existing Web server load testing software-

+   2. If we can't support one million hits per day, use test data to extrapolate how much processing power, memory, and network capacity we will need to support the load.

+   3. Specify and purchase appropriate hardware and/or network capacity from vendors.

+   4. Install new hardware in a sandbox environment and load test again.

+   5. Assuming the load can be handled, perform regression tests on new servers and deploy into production.

Chapter 4, "Testing Your Systems," discusses load testing and regression testing in detail. You learn more about working in sandbox environments in Chapter 7, "Patches, Upgrades, and Decomissions."

You can see that a business goal that fits into a single sentence can result in an incredible amount of technical planning. Technical planning takes time and effort, but by carefully listing all of the technical steps necessary to achieve the business goal, you can avoid many headaches and surprises as the project moves along.

# Gathering Details About Specific Business Goals

Once you've defined your technical goals, it's time to crush goals into real numbers. In order to do that, you need to get more information from management about the specifics of its business goals, its priorities for the project, and its willingness to support the technical requirements for meeting those business goals.

Many details go into the design of technical solutions for meeting business goals. If a Web server must support one million hits per day, for example, what are the criteria for meeting that goal? Page retrieval in less than seven seconds? Low load on the servers? No client-outs during the browsing session? To know the answers to these questions, you must find out exactly what management expects from the technical solution for meeting its business goals.

# Being Prepared with Solution Details

You need to provide management with specific details regarding your technical solutions. For the "one-millioned" Web server, management will want to know what resources you need and why you need them. To provide that information, you must answer many questions. How many servers should you buy, and from what vendor? What operating system should they run? How many processors should they have? How much memory should they have? What software stack should you run? What are you are the timelines for deployment? How much staffing do you need to meet those timelines?

That's a lot of questions, and any good IT manager or CTO will expect you to answer all of them before moving ahead with your project. Performance management and capacity planning are an integral part of the design of any system architecture, and you learn more about those processes in Chapter 11, "Performance Tuning and Capacity Planning."

![](bbox=[0.193, 0.714, 0.375, 0.803])