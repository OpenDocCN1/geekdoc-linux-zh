Notice that there are several areas of overlap between the traditional top-down methodology and this newer principle-based approach. One important difference is that the principle-based tuning approach recognizes the fact that changes to an application’s design are difficult, if not impossible, after a production system is in use. As packaged business applications become more prevalent, this tuning methodology becomes increasingly important since the highest priority tuning factors considered by the traditional top-down approach (data and application design) are almost entirely outside the control of the DBA when working with a packaged application.

Most of the objectives for the Oracle9i Performance Tuning OCP Exam are related to the *second, fourth, and fifth principles* (as listed in Table 1.2). They generally focus on examining the database for wait events—*users or processes who are waiting for access to a database resource*—and then trying to minimize these waits by making the *appropriate changes* to the system’s configuration.

# ## Goal-Oriented Tuning

Whichever tuning methodology you choose, it is important to set specific tuning goals and then measure your progress toward those goals throughout the tuning process. This is not unlike the process a physician uses when treating a patient, where the physician records standard “*performance*" measures (i.e., blood pressure, temperature, respiration, heart rate, etc.) and then uses these measures throughout the course of treatment to track the progress of the patient’s condition.

This process includes establishing benchmarks and gathering baseline statistics or timings against which you can measure your tuning progress, and setting measurable tuning goals.

# ## Establishing a Benchmark

You should measure exactly how the system is currently performing before beginning any tuning effort. Using this benchmark, it is then possible to