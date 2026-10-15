**Table 28.1 Functional breakdown of three applications**

| Function | EL | AA | EC |
|---|---:|---:|---:|
| Accounts payable/receivable |  | X |  |
| Benefits management | X | X |  |
| Employee time tracking | X | X | X |
| General ledger |  | X |  |
| Payroll | X | X |  |
| Time reporting | X | X | X |
| Vacation/sick day tracking |  | X | X |

also complicates or forestalls integration of data among departments. In this case, moving the organization to a single application trimmed software, hardware, and energy costs by over 60% and resulted in smoother data flow within the company.

Your situation is probably not this dramatic, but if you take the time to map out your application domains, chances are that you’ll find some significant overlap. The business case for consolidating applications is easy to make because the projected results can (at least in part) be expressed in dollars saved. Data integration and operational improvements are just icing on the cake.

# Server consolidation

Most organizations have at least a few “single purpose” servers that operate at 10% utilization or less. For example, we’ve seen many organizations that have dedicated NTP (network time protocol) servers. NTP is a low-overhead protocol that requires very little computational effort. Reserving a server for NTP is like flying a Boeing 767 cross-country with only one passenger.

Server consolidation is a close cousin of application consolidation and is equally effective. Instead of bundling multiple functions into one application, you bundle multiple services onto one server machine.

Unlike Windows, UNIX and Linux excel at preemptive multitasking. A good solution in the NTP case is to run the NTP daemon on the same servers that provide common infrastructural services such as DNS and Kerberos.

Another common opportunity for server consolidation is presented by database servers that are dedicated to a single application. If you have competent sysadmins and DBAs (and good monitoring), a single database server should be able to host the databases for many applications. Once again, this consolidation reduces license fees, capital costs, and energy consumption.

> 5. NTP is a special case in that its response latency must be kept low. However, that doesn’t mean you can’t run other services on the same machine. NTP server daemons are commonly mined to give them ready access to the CPU whenever they want it (see page 129). You can achieve similar ends—perhaps even a bit more reliably—through server virtualization.