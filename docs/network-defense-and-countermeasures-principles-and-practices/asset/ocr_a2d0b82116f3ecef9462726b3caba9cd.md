# Anomaly Detection

Anomaly detection involves actual software that works to detect intrusion attempts and notify the administrator. This is what many people think of when they talk about intrusion-detection systems. The general process is simple: The system looks for any anomalous behavior. Any activity that does not match the pattern of normal user activity is noted and logged. The software compares activity against expected normal usage profiles. Profiles are usually developed for specific users, groups of users, or applications. Any activity that does not match the definition of normal behavior is considered an anomaly and is logged. Sometimes we refer to this as "trace back" detection or process. We are able to establish from when this packet was delivered. The specific ways in which an anomaly is detected include:

+   - Threshold monitoring
- Resource profiling
- User/group work profiling
- Executable profiling

# Threshold Monitoring

Threshold monitoring presets acceptable behavior levels and observes whether these levels are exceeded. This could include something as simple as a finite number of failed login attempts or something complex as monitoring the time a user is connected and the amount of data that user downloads. Thresholds provide a definition of acceptable behavior. Unfortunately, characterizing intrusive behavior solely by the threshold limits can be somewhat challenging. It is often quite difficult to establish proper threshold values or the proper time frames at which to check those values. This can result in a high rate of false positives in which the system misidentifies usage as a probable attack.

# Resource Profiling

Resource profiling measures system-wide use of resources and develops a historic usage profile. Looking at how a normal utilizes system resources enables the system to identify usage levels that are outside normal parameters. Some abnormal readings can be indicative of illicit activity underway. However, it may be difficult to interpret the meaning of changes in overall system usage. An increase in usage might indicate benign like increased workflow rather than an attempt to breach security.

# User/Group Work Profiling

In user/group work profiling, the IDS maintains individual work profiles about users and groups. These users are expected to adhere to these profiles. As the user changes his activities, his expected profile is updated to reflect these changes. Some systems attempt to monitor the interaction of short-term versus long-term profiles. The short-term profiles capture recent changing work patterns, whereas the long-term profiles provide a view of usage over an extended period of