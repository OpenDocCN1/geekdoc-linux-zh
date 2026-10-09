
## 10.5 More on Collective Operations

213

## 10.6 Parallel I/O

215

### 10.6.1 A Simple Example

217

### 10.6.2 A More Complex Example

219

## 10.7 Remote Memory Access

221

## 10.8 Using C++ and Fortran 90

224

## 10.9 MPI, OpenMP, and Threads

226

## 10.10 Measuring MPI Performance

227

### 10.10.1 mppitest

227

### 10.10.2 SKaMPI

227

### 10.10.3 High Performance LINPACK

228

## 10.11 MPI-2 Status

229

## 10.12 MPI Routine Summary

229

## 11 Parallel Programming with PVM—Al Geist and Stephen Scott

235

### 11.1 Overview

235

### 11.2 Program Examples

240

### 11.3 Fork/Join

240

### 11.4 Dot Product

244

### 11.5 Matrix Multiply

249

### 11.6 One-Dimensional Heat Equation

255

### 11.7 Using PVM

263

#### 11.7.1 Setting Up PVM

263

#### 11.7.2 Starting PVM

265

#### 11.7.3 Running PVM Programs

267

### 11.8 PVM Console Details

268

### 11.9 Host File Options

270

### 11.10 XPVM

273

#### 11.10.1 Network View

275

#### 11.10.2 Space-Time View

275

#### 11.10.3 Other Views

276

## 12 Fault-Tolerant and Adaptive Programs with PVM—Al Geist and Jim Kohl

279

- 12.1 Considerations for Fault Tolerance
  280
- 12.2 Building Fault-Tolerant Parallel Applications
  281
- 12.3 Adaptive Programs
  287

## III Managing Clusters

## 13 Cluster Workload Management—James Patton, David Liffka, Bill Nitzeberg, and Todd Tannenbaum

299

- 13.1 Goal of Workload Management Software
  299
- 13.2 Workload Management Activities
  300
  - 13.2.1 Queueing
    300
  - 13.2.2 Scheduling
    301
  - 13.2.3 Monitoring
    302
  - 13.2.4 Resource Management
    304
  - 13.2.5 Accounting
    305

## 14 Condor: A Distributed Job Scheduler—Todd Tannenbaum, Derek Wright, Karen Miller, and Miron Livny

307

- 14.1 Introduction to Condor
  307
  - 14.1.1 Features of Condor
    308
  - 14.1.2 Understanding Condor ClassAds
    309
- 14.2 Using Condor
  312
  - 14.2.1 Roadmap to Using Condor
    312
  - 14.2.2 Submitting a Job
    313
  - 14.2.3 Overview of User Commands
    316
  - 14.2.4 Submitting Different Types of Jobs: Alternative Universes
    322
  - 14.2.5 Giving Your Job Access to Its Data Files
    323
  - 14.2.6 The DAGMan Scheduler
    325
- 14.3 Condor Architecture
  326
  - 14.3.1 The Condor Daemons
    327
  - 14.3.2 The Condor Daemons in Action
    328
- 14.4 Installing Condor under Windows 2000
  330
- 14.5 Configuring Condor
  332
  - 14.5.1 Location of Condor's Configuration Files
    332
  - 14.5.2 Recommended Configuration File Layout for a Cluster
    333
  - 14.5.3 Customizing Condor's Policy Expressions
    334
  - 14.5.4 Customizing Condor's Other Configuration Settings
    336
- 14.6 Administration Tools
  337
  - 14.6.1 Remote Configuration and Control
    337
  - 14.6.2 Accounting and Logging
    338
  - 14.6.3 User Priorities in Condor
    338
- 14.7 Cluster Setup Scenarios
  339
  - 14.7.1 Basic Configuration: Uniformly Owned Cluster
    340
  - 14.7.2 Using Multiprocessor Compute Nodes
    340
  - 14.7.3 Scheduling a Distributively Owned Cluster
    341
  - 14.7.4 Submitting to the Cluster from Desktop Workstations
    342
  - 14.7.5 Expanding the Cluster to Non-dedicated (Desktop) Computing Resources
    343
- 14.8 Conclusion
  343

## 15 Maui Scheduler: A Multifunction Cluster Scheduler—David B. Jackson

345

- 15.1 Overview
  345
- 15.2 Installation and Initial Configuration
  346
  - 15.2.1 Basic Configuration
    346
  - 15.2.2 Simulation and Testing
    346
  - 15.2.3 Production Scheduling
    347
- 15.3 Advanced Configuration
  347
  - 15.3.1 Assigning Value: Job Prioritization and Node Allocation
    348
  - 15.3.2 Fairness: Throttling Policies and Fairshare
    350
  - 15.3.3 Managing Resource Access: Reservations, Allocation Managers, and Quality of Service
    352
  - 15.3.4 Optimizing Usage: Backfill, Node Sets, and Preemption
    355
  - 15.3.5 Evaluating System Performance: Diagnostics, Profiling, Testing, and Simulation
    357
- 15.4 Steering Workload and Improving Quality of Information
  359
- 15.5 Troubleshooting
  361
- 15.6 Conclusions
  361

## 16 PBS: Portable Batch System — James Patton Jones

363

- 16.1 History of PBS
  363
  - 16.1.1 Acquiring PBS
    364
  - 16.1.2 PBS Features
    364
  - 16.1.3 PBS Architecture
    366
- 16.2 Using PBS
  367
  - 16.2.1 Creating a PBS Job
    368
  - 16.2.2 Submitting a PBS Job
    368
  - 16.2.3 Getting the Status of a PBS Job
    370
  - 16.2.4 PBS Command Summary
    370
  - 16.2.5 Using the PBS Graphical User Interface
    370
  - 16.2.6 PBS Application Programming Interface
    371
- 16.3 Installing PBS
  372
- 16.4 Configuring PBS
  373
  - 16.4.1 Network Addresses and PBS
    373
  - 16.4.2 The Qmgr Command
    373
  - 16.4.3 Nodes
    374
  - 16.4.4 Creating or Adding Nodes
    376
  - 16.4.5 Default Configuration
    377
  - 16.4.6 Configuring MOM
    378
  - 16.4.7 Scheduler Configuration
    378
- 16.5 Managing PBS
  379
  - 16.5.1 Starting PBS Daemons
    379
  - 16.5.2 Monitoring PBS
    380
  - 16.5.3 Tracking PBS Jobs
    380
  - 16.5.4 PBS Accounting Logs
    381
- 16.6 Troubleshooting
  381
  - 16.6.1 Clients Unable to Contact Server
    381
  - 16.6.2 Nodes Down
    382
  - 16.6.3 Nondelivery of Output
    383
  - 16.6.4 Job Cannot Be Executed
    383

## 17 MPI Software Technology, Inc., Cluster CoNTroller—David Lafka

385

- 17.1 Overview of Cluster CoNTroller
  385
  - 17.1.1 Strengths
    386
  - 17.1.2 Availability
    386
- 17.2 Installation Configuration
  386
  - 17.2.1 Login Nodes
    386
  - 17.2.2 File Servers
    387
  - 17.2.3 Compute Nodes
    387
  - 17.2.4 Scheduler Node
    388
  - 17.2.5 Security and Management
    388
- 17.3 Administrative Features
  388
- 17.4 User Commands
  389
  - 17.4.1 Batch File Syntax
    390
  - 17.4.2 Lifecycle of a Job
    394
- 17.5 Future Enhancements
  397

## 18 Cornell Theory Center—David Lafka

399

- 18.1 CTIC Users
  399
- 18.2 Systems Overview
  400
  - 18.2.1 File Servers
    400
  - 18.2.2 Login Nodes
    400
  - 18.2.3 Development Cluster
    400
  - 18.2.4 Serial Nodes
    401
  - 18.2.5 General-Purpose Compute Cluster, Velocity I
    401
  - 18.2.6 Strategic Application Compute Cluster, Velocity I Plus
    402
- 18.3 Dedicated Clusters
  402
  - 18.3.1 Computational Materials Institute Cluster
    402
  - 18.3.2 Social Sciences and Economics Research Cluster
    403
  - 18.3.3 Agricultural Bioinformatics Cluster
    403
  - 18.3.4 Corporate Cluster
    404
  - 18.3.5 Computational Finance Cluster
    404
- 18.4 Other Cluster Resources
  404
  - 18.4.1 Web Clusters
    404
  - 18.4.2 Windows 2000-Based Cave Environment
    405
- 18.5 Providing a Consistent User Interface
  405
  - 18.5.1 Remote Access Mechanisms
    406
  - 18.5.2 Programming Environment
    407
  - 18.5.3 Application Software
    408
- 18.6 Helping Users Get Started
  409
- 18.7 Batch and Interactive Job Scheduling
  409
- 18.8 CTC Success Story
  409

## 19 Conclusions — Thomas Sterling

411

- 19.1 Future Directions for Hardware Components
  411
- 19.2 Future Directions for Software Components
  413
- 19.3 Final Thoughts
  416

## A Glossary of Terms

419

## B Annotated Reading List

431

## C Annotated URLs

433

## References

437

## Index

439

## Series Foreword

The world of modern computing potentially offers many helpful methods and tools to scientists and engineers, but the fast pace of change in computer hardware, software, and algorithms often makes practical use of the newest computing technology difficult. The Scientific and Engineering Computation series focuses on rapid advances in computing technologies, with the aim of facilitating transfer of these technologies to applications in science and engineering. It will include books on theories, methods, and original applications in such areas as parallelism, large-scale simulations, time-critical computing, computer-aided design and engineering, use of computers in manufacturing, visualization of scientific data, and human-machine interface technology.

The series is intended to help scientists and engineers understand the current world of advanced computation and to anticipate future developments that will affect their computing environments and open up new capabilities and modes of computation.

This volume in the series describes the increasingly successful distributed/parallel system called Beowulf. A Beowulf is a cluster of PCs interconnected by network technology and employing the message-passing model for parallel computation. Key advantages of this approach are high performance for low price, system scalability, and rapid adjustment to new technological advances.

This book includes how to build, program, and operate a Beowulf system based on the Windows 2000 operating system. A companion volume in the series provides the same information for Beowulf clusters based on the Linux operating system.

Beowulf hardware, operating system software, programming approaches and libraries, and machine management software are all covered here. The book can be used as an academic textbook as well as a practical guide for designing, implementing, and operating a Beowulf for those in science and industry who need a powerful system but are reluctant to purchase an expensive massively parallel processor or vector computer.

Janusz S. Kowalik
