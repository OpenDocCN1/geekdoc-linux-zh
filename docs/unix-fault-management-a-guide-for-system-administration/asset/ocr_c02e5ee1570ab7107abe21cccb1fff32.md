programs to generate alarms to warn of potential performance problems. By using the historical data, trends can be discovered, which can help to solve resource issues before they affect system performance.

# Monitored Components

MeasureWare agents collect data at three different levels: global system metrics, application met-rics, and process metrics. Global and application data is summarized at five-minute intervals, whereas process data is summarized at one-minute intervals. Important applications can be defined by an administrator by listing the processes that make up the application in a configuration file.

In addition, optional modules for database and networking support are offered. MeasureWare also provides a DSI interface that enables you to pass your own data to the MeasureWare Agent.

MeasureWare has database modules for collecting database metrics for Oracle, Sybase, and Informix databases. These modules can take advantage of all the standard monitoring fea-tures of MeasureWare, such as timestamping data, logging, and forwarding alarms to HP Perf-View. However, this product is similar to another HP product for database performance informa-tion, the OpenView SMART Plug-Ins for databases. SPIs also feed information into Measure-Ware, providing a consistent interface with other IT/O products.

A more detailed list of metrics in each category can be found in the next few chapters on systems, disks, networks, applications, and databases. Although MeasureWare provides exten-sive performance and resource information, it offers limited configuration information and no data about system faults.

# Monitoring Features

HP MeasureWare Agent software is installed on each managed system. The agents keep a history of a system's resource utilization, and the information can then be exported to spreadsheets or to performance analysis programs, such as HP PerfView. The data can be used by these programs to generate alarms to warn of potential performance problems. By using historical data, trends can be discovered, which can help to solve resource issues before they affect system performance.

MeasureWare allows you to define alarm conditions. You can have alarms sent based on conditions that involve a combination of metrics. For example, a CPU bottleneck alarm can be based on the CPU use and CPU run queue length.

MeasureWare agents provide alarms to PerfView for analysis, and to the IT/O management console. SNMP traps can also be sent by the MeasureWare Agent at the time threshold conditions are met. Automated actions can be taken, or the operator can choose to take a suggested action.

You can configure alarms based on a combination of multiple metrics and on duration. In this way, rules can be used to ensure that messages are sent to an operator only when a real prob-lem occurs.

MeasureWare's extract command can be used to export data to other tools, such as spread-sheet programs.