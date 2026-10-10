
## Binary Searches
55

## Partitioned Tables
56

## The B-Tree Algorithm
58

## Sparse Tables
61

## The Skip List
63

## Operations Arrays
65

## The HP-UX Kernel Overview
66

## Fundamental Kernel Data Structures: A First Pass
67

### Kernel Memory Tables
67

### Physical Memory
68

### Process Logical Memory Space
69

### Managing Memory for Internal Kernel Usage
70

### All Together Now
70

## Kernel Process Tables
70

### The Process Table
70

### The kthread Table
71

### The vas and vregion Tables
72

### Process File Descriptors
72

### The uarea Structure
72

## The Kernel File System Tables
73

### The System File Table
73

### The Virtual File System
73

### The Inode Cache
74

### The Buffer Cache
74

## The Kernel Input/Output Tables
74

### The I/O Tree
75

### System Interruptions
75

## Drivers and Switch Tables
76

## Summary
77

## Chapter 4 Programs, Processes, and Threads
79

## The Players
79

### The Program
79

### The Process
80

### The Thread
82

## A Process and Its Threads
83

## Threading Models and HP-UX
84

## The System Call Interface
86

## The System Call Stub
88

## The Gateway Page
88

## Promotion Blocks
89

## Lightweight System Calls
91

## gateway_page on a Narrow Kernel
91

## Selected Portions of the gateway_page from a 32-Bit HP-UX 11.0 Kernel
91

## The Wide Gateway: gateway_page, sysvec, and gateway64_page on a 64-bit Kernel
93

## Listing the gateway_page on a Wide System
94

## Selected Portions of the sysvec Page from a 64-Bit HP-UX 11.0 Kernel
94

## The gateway64_page from a 64-Bit HP-UX 11.0 Kernel
95

## Low-Level Initialization
99

## High-Level Initialization
99

## The System Call
99

## High-Level Return
100

## Low-Level Return
100

## Summary
101

# Chapter 5 Process and Thread Management from the Process's Viewpoint
103

## A Process and Its Resources
103

## The proc Table
104

## The kthread Table
108

## The Process's Logical View
110

## SHARE_MAGIC, EXEC_MAGIC, and SHMEM_MAGIC
112

### SHARE_MAGIC
113

### EXEC_MAGIC
114

### SHMEM_MAGIC
115

## More Magic
115

## Memory Windows
115

## Q3 Private Address Space
118

## Building the Logical map
119

### The va
119

### The pregion (pseudo-region)
123

### The uarea
125

## Additional Resource Pointers
128

## Process/Thread Scheduling
128

## SCHED_TIMESHARE and SCHED_NOAGE
131

## System-Level and User-Level Priorities
132

## Time Basics in HP-UX Scheduling: The Tick
132

## Time Slicing or Round-Robin Queuing
133

## Priority Decay, N ice and User-Level Priorities
133

## SCHED_NOAGE
135

## SCHED_RTPRIO
135

## POSIX Real-Time Scheduler
137

## Sizing the POSIX Queues
137

## SCHED_FIFO
138

## SCHED_RR
138

## SCHED_RR2
138

## Run Queues
138

### The Systemwide POSIX Run Queues
139

### Per-Processor Run Queues
141

## Summary
142

# Chapter 6 Managing Memory
143

## Types of Memory
144

### Logical Memory
144

### Virtual Memory
144

### Physical Memory
145

### Front Store and Back Store
145

## The System’s Virtual Address Space
146

## Virtual-to-Physical Page Tables
147

## The Kernel View: The Hash Table
152

### Page Frame to Virtual Page Frame Tables
154

### Virtual Address Aliasing
156

### Regions of Pages
157

## Shared Objects
161

### Virtual Page Locator, VFD, and DBD
161

## The b-tree
163

## broot, bnodes, and chunks
164

## Page Lists
166

## Connecting the Kernel View to the Process View
167

### Managing Page Frames: Many Points of View
168

## Keeping Track of Free Physical Page Frames
169

## Is a Page I/O Really Needed? (f hash and fhead)
172

## Views, Ponds, Pools, Pages
173

## Physical Memory View
174

## Logical Memory Views
174

## Memory Pools
175

## Memory Ponds
175

## The Nested Structures
175

## Variable Page Size
177

## Physical Memory Allocator at HP-UX 11.0
178

## Allocating Memory
179

## Freeing Memory
180

## Coalescing Free Pages
180

## Summary
181

# Chapter 7 The HP-UX Paging System
183

## Pages on Demand
183

## Faulting in a Page from Front Store
184

## Faulting in a Page from Back Store (Swap)
184

## Faulting in a Zero-Fill Page
184

## Faulting in a No-Fill Page
185

## Digging a Memory Hole
185

## Monitoring Free Memory
185

## slot_sfree
186

## des_free
186

## min_free
186

## ggss_lim
186

## Other Kernel Paging Parameters
187

## A Thief in the Night: vh
188

## The Linked p region List
189

## Reservation Versus Allocation
191

## A Simple Swap Example
193

## Pseudo-Swap
194

## Interpreting the Output of swapinfo
196

## Device Swap
197

## File System Swap
197

## Swap Priority
197

## Tracking swap in the Kernel Structures
198

## Summary
201

# Chapter 8 Files and File Systems
203

## File System Concepts
204

# The New and Improved UNIX File System
211

## HP-UX's HFS
211

## Direct and Indirect Block Pointers
213

## The HFS inode
214

## Following Metadata Using fsdb
216

## Blocks and Fragments
218

## Allocation Policy
219

## Other File System Types
220

## File System Utility Wrappers
221

# The Kernel View of File Systems
221

## The vfs Mount Table
221

## The Type-Specific In-Core Data Structures
224

## The vnode
228

## The HFS In-Core inode Contains Its vnode
230

## Caching inode/vnode Data in the Kernel
231

## Smoke and Mirrors: Tying Together the File Subsystem Abstractions
231

## Connecting an Open File to a Process
233

## The Buffer Cache
235

## Being Flexible: The Dynamic Buffer Cache
235

## The Buffer Cache Hash
236

## Free Lists: Allocating a New Buffer
239

## Bigger Isn't Always Better
240

## The Directory Name Lookup Cache, DNLC
240

## Summary
242

# Chapter 9 The Process Life Cycle, Cradle to Grave
243

## The Birth of a Process
243

## A Simple Scenario
245

## Which Came First?
246

## A Historic Look at the fork() Call
246

## Another Approach: The Berkeley Virtual Fork
247

## HP's New and Improved fork()
247

## The fork1() Kernel Routine
249

## The fork() System Call Mechanics
250

## Copying a Process Memory View
251

## Copy-on-Write, First Read Access from the Parent
251

## Copy-on-Write, First Read Access from a Child
252

## Copy-on-Write, First Write Access
252

## Copy-on-Write for the Parent, Copy-on-Access for the Child
253

## Creating the New uarea
253

## Ready, Set, Run Queue
253

## The vfork() System Call Mechanics
254

## Process and Thread States: Idle Hands
257

## Process Identity Crisis: The exec() System Call
258

## The Kernel’s Draft Horse, getFile()
258

## Calling exec() Immediately After vfork()
259

## Calling exec() after a fork()
259

## Removing pregress, regions, and b-trees
259

## Building the New Logical View
260

## Shared Memory Objects Revisited
261

## Shared Memory, System-V, and POSIX
262

## The exit() System Call Mechanics
264

## Walk, Don’t Run, to the exit()
264

## Night of the Zombies: Responsible Parenting
265

## The Grim Reaper Pays a Visit
266

## Summary
267

# Chapter 10 I/O and Device Management
269

## PA-RISC I/O Architecture
269

## IODC and PDC
271

### Processor-Dependent Code (PDC)
271

### I/O Address Space
271

### Modes of Operation
273

## External I/O Interrupts
274

## I/O Framework
276

## General I/O
278

## Context-Dependent I/O
281

## Central Bus CDIO
283

## I/O Odds and Ends
284

## Device Files and the Device Switch Table
284

## The iooconf ig File
284

## Instance Numbers
285

# Chapter 11 The Logical Volume Manager
287

## LVM Design Concept
287

### The LVM Extent
289

### LVM’s Smoke and Mirrors
289

### Building a Volume Group
290

## Disk-Resident Data Structures
292

### The PVRA and VGRA
293

## LVM: The Kernel View
301

### Work Queues: Keeping a Request on Track
302

### Kernel Resident Data Structures
303

### One-Way and Two-Way Mirroring Mechanics and Options
309

## Summary
311

# Chapter 12 Multiprocessing and HP-UX
313

## Hardware Overview
313

## Multiprocessing Data Structures
315

## Synchronization
318

### Spinlocks
319

### Arbitration
320

### Preadbitration
321

### Semaphores
322

#### Alpha Semaphores
323

#### Beta Semaphores
326

### Synchronization Semaphores
328

## Summary
328

# Chapter 13 Kernel Services
329

## The Callout Table
329

### Interface
329

### Data Structures
330

### Callout Processing and Expiration
331

## Kernel Memory Allocation
333

### The Bucket Allocator
333

### The Arena Allocator
334

### Objects and Object Headers
336

### Object Free Lists
337

### Managing Kernel Virtual Addresses: The Sysmap
338

## Summary
340
