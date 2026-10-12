
## 7.1 User Classes

### Table 7-1 User Classes

| User class | Explanation |
| :--- | :--- |
| Class 0 | This class indicates the users that were added to the dispatch list with no delay in the eligible list, regardless of the length of their current transaction. |
| Class 1 | This class indicates the users who have just begun a transaction, and therefore are assumed to be currently processing short transactions. |
| Class 2 | This class indicates the users who did not complete their current transactions during their first dispatch list stay and therefore are assumed to be running medium-length transactions. |
| Class 3 | This class indicates the users who did not complete their current transactions during their second dispatch list stay and therefore are assumed to be running long transactions. |

If you have command privilege class E, you can issue the `CP INDICATE LOAD` command to view information about these classes of user. See Example 7-1. Qn indicates users in the dispatch list. En indicates users in the eligible list, where n is the class of the user (0, 1, 2, or 3).

### Example 7-1 INDICATE LOAD command

```text
ind
AVGPOC-000% 04
XSTORE-000000/SEC MIGRATE-0000/SEC
MDC READS-000001/SEC WRITES-000000/SEC HIT RATIO-084%
PAGING-0/SEC STEAL-000%
Q0-000000(000000) DORMANT-00016
Q1-000000(000000) E1-000000(000000)
Q2-000000(000000) EXPAN-001 E2-000000(000000)
Q3-000000(000000) EXPAN-001 E3-000000(000000)
PROC 0000-000% CP PROC 0001-000% CP
PROC 0002-000% CP PROC 0003-000% CP
LIMITED-00000
```

### Thrashing

Thrashing is a situation caused by servers wanting more storage all at one time than exists on a box. At the point where VM does not have enough storage to meet each server's needs, VM starts paging. There is a point where VM could spend more time doing paging than performing work.

The VM scheduler has a very sophisticated mechanism to stop users from thrashing. It will control thrashing from three different perspectives: storage, paging, and processor.

The mechanism for controlling thrashing is to put users on an eligible list, meaning that these users want to consume resource, but there is not enough resource to sustain them, so they will not be dispatched. When there is enough resource or certain deadlines pass, the user will be dispatched. This can look like users are hung. They are not hung, they are waiting until there is sufficient resource to run efficiently.

## 7.2 SRM controls

Use `SET SRM` (system resource manager) to change system parameters. These parameters define the size of the time slice—the access to resources for different user classes as seen by the scheduler. This is a complex command and you should clearly understand its effects before using it.

### 7.2.1 SRM STORBUF

One of the ways to solve the thrashing problem is to set the `SRM STORBUF` command. Basically, this controls the VM guest users who are not to be sent to the eligible list in spite of memory overcommitment.

The default value for `SRM STORBUF` is `Q1=125% Q2=105% Q3=95%`. Usually, users are moved to the eligible list when real storage utilization is over the setting value. When we set the values for the various queues as `Q1=aaa%`, `Q2=bbb%`, and `Q3=ccc%`, users are moved to the dispatch list from the eligible list with the following conditions.

- User is E1: total WSS + target E1 user's WSS <= DPA x aaa%
- User is E2: total WSS + target E2 user's WSS <= DPA x bbb%
- User is E3: total WSS + target E3 user's WSS <= DPA x ccc%

WSS means working sets and DPA means dynamic paging area.

![](img/f332344337ca8bf6846cb313a66ee0b3_253_0.png)

Figure 7-2 Example SET SRM STORBUF

For larger production Linux guests or servers, we recommend setting the `SRM STORBUF` value. See Example 7-2.

### Example 7-2 Example SRM STORBUF setup for large servers

```text
SET SRM STORBUF 300 250 200
```

### 7.2.2 SRM LDUBUF

By setting up `SRM LDUBUF` appropriately, we can avoid sending the users to the eligible list, and instead allow all users (E1–E3) with more paging space. The default `LDUBUF` encourages a thrashing situation. If you are thrashing and you raise the `LDUBUF`, you will in effect reduce the amount of work that you will get done.

### Example 7-3 Default SRM LDUBUF values

```text
LDUBUF : Q1=100% Q2=75% Q3=60%
```

In the Example 7-3 on page 238, `LDUBUF` figures mean that guests in Q3 are only allowed to use 60% of your paging capacity. Since Linux guests are always in Q3, we would be able to use only 60% paging capacity with our Linux guests, so we should raise the `LDUBUF` settings, which would mean that all guests in any queue would all be able to compete for 100% of your paging capacity. See Example 7-4.

### Example 7-4 Example SRM LDUBUF setup for Linux guests

```text
SET SRM LDUBUF 100 100 100
```

### 7.2.3 QUICKDSP

Use `SET QUICKDSP` to assign or unassign a user's immediate access to system resources. This option, when set for a server, allows the server to bypass all governors set by the CP scheduler. In this way, the server is always dispatched when necessary, even under a thrashing situation. Users such as TCP/IP and your more important production Linux servers should have this option.

Points to note are:

- The user ID becomes transaction class 0 and never waits in the eligible list.
- This impacts the decision to move from E-list to D-list on a user ID basis.
- Used for key server virtual machine (process synchronous requests from users) and virtual machines that demand the best performance.

### Example 7-5 Syntax for SET QUICKDSP

```text
SET QUICKDSP userid ON
```

The `QUICKDSP` setting impacts a single user ID. It should be used for any server virtual machine that is critical to user response time or holds key system resources. Overuse of this control for other users can take away the effectiveness of the scheduler.

We can also, by default, set the `QUICKDSP` option set for a user by including the `SET QUICKDSP` option in the USER DIRECTORY definition of the particular user.

## 7.3 Other recommendations

In general, we recommend setting `QUICKDSP` on for production guests and server virtual machines that perform critical system functions. However, you may not want to set it on for all your test or non-critical guests. Allowing the VM scheduler to create an eligible list allows it to avoid some thrashing situations that could occur from over committing real storage.

Solve this with one of two approaches: use of `QUICKDSP` or changing the `SRM STORBUF` settings. The choice is dependent on where you want the responsibility of protecting the system from thrashing. The more you use `QUICKDSP`, the greater the responsibility on yourself. Setting appropriate `STORBUF` settings puts the responsibility on the VM scheduler.

The next line of defense is to set up the Linux guests conservatively as regards the virtual storage sizes and to set up the VM system well for paging. Here are some guidelines:

- Set each Linux machine's virtual storage size only as large as it needs to be to let the desired Linux applications run. This will suppress the Linux guest's tendency to use its entire address space for file cache. Make up for this with MDC if the Linux file system is hit largely by reads. Otherwise, turn MDC off, because it induces about an 11% instruction path length penalty on writes, consumes storage for the cached data, and pays off little because the read fraction is not high enough.
- Use whole volumes for VM paging, instead of fractional volumes. In other words, never mix paging I/O and non-paging I/O on the same pack.
- Implement a one-to-one relationship between paging CHPIDs and paging volumes.
- Spread the paging volumes over as many DASD control units as possible.
- If the paging control units support NVS or DASDFW, turn them on (applies to RAID devices).
- Provide at least twice as much DASD paging space (`CP QUERY ALLOC PAGE`) as the sum of the Linux guests' virtual storage sizes.
- Having at least one paging volume per Linux guest is a great thing. If the Linux guest is using synchronous page faults, exactly one volume per Linux guest will be enough. If the guest is using asynchronous page faults, more than one per guest might be appropriate—one per active Linux application would be more like it.
- In QDIO-intensive environments, plan that 1.25 MB per idling real QDIO adapter will be consumed out of CP below 2 GB free storage for CP control blocks (shadow queues). If the adapter is being driven very hard, this number could rise to as much as 40 MB per adapter. This tends to hit the below 2 GB storage hard. CP prefers to resolve below 2 GB contention by using XSTORE. Consider configuring at least 2 GB to 3 GB of XSTORE so as to back the below 2 GB main storage, even if main storage is otherwise large.
