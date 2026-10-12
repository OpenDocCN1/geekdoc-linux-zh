# Sizing the RAC System

There is a tendency to treat sizing servers as some form of mystic science. Most people assume that the more statistics, benchmarks, and technical specifications that you can arm yourself with, the better. There is more to sizing a RAC system than just gathering all the information you can.

Here are the steps you should follow for sizing a RAC system, or for that matter, any system:

+   - **Define customer requirements** This is one of the most important steps. You must have a proper starting place before you proceed. Most customers will not deliver their requirements to you on a silver platter. You must be proactive in obtaining the input you require. You must be prepared to translate from business terms into technical terms.

+   - **Analyze system data** You should always gather as much technical information as possible from a comparable or current production system. This is true even if the hardware platform will be different from your target system, or even if you expect your new system to have significantly improved performance characteristics. You should make sure you gather statistics for CPU utilization, memory utilization, and I/Os per second (IOPS). If the comparison system is Microsoft Windows-based, you may use Performance Monitor to obtain the required data.

+   - **System determination** The next step is to design a system that will meet the customer requirements according to the system information you have gathered. You will need to predict total CPU usage, total memory usage, and the total I/O load. You may estimate storage resources required for capacity and performance in terms of the I/O load and the total size estimate of customer data. You will want to pull together all of your sizing guidelines. This includes any relevant “rules of thumb” and benchmarks. Compare your requirements to similar existing implementations if possible. The design should cover all aspects of the customer requirements. You should make sure that all of the requirements have been met in the initial design. It is far more expensive to find out you have missed a requirement after the hardware has been purchased.

+   - **Implementation** Try to deliver the design in incremental steps. Deliberately stagger the full implementation. This allows you to tune performance as you implement.