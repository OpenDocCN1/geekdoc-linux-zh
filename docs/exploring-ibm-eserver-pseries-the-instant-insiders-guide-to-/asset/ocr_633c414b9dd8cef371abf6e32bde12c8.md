# 78 Exploring IBM @serverSeries

| | tpmC | $/tpmC |
|---|---|---|
| p660-6H1 | 57346 | 28.47 |
| p660-6M1 | 105025 | 23.45 |
| p690 (1.3 GHz) | 427760 | 17.75 |
| p690 (1.7 GHz) | 763898 | 8.31 |

Figure 1.23. Audited TPC-C Version 5 benchmark results for selected pSeries servers. (Data valid as of May 10, 2003.)

the TPC-C is difficult and costly for a vendor to run and have audited by the council. Therefore, IBM and other vendors publish tpmC results of only a few systems, generally the large SMP servers. TPC-C rules do not permit publishing estimates of tpmC performance.
Many other benchmarks are used to evaluate system performance. In today’s Internet age, two important and frequently used benchmarks managed by the SPEC organization are SPEC99, which measures a system’s performance when used as a Web server, and SPECjb2000, a benchmark for evaluating a server’s ability to run Java-based applications. Java is a popular programming language used in many e-business applications. Also, the TPC organization has transaction-oriented benchmarks other than TPC-C. TPC-H is a decision support benchmark, indicative of the performance of very large (often terabyte) database systems to ad hoc decision support queries. TPC-W is a transactional