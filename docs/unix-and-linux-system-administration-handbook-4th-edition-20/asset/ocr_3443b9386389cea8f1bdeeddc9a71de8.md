# Chapter 28 Green IT

# Table 28.1 Functional breakdown of three applications

| Function | EL | AA | EC |
|---|---|---||}{
| Accounts payable/receivable | | X | |
| Benefits management | X | X | |
| Employee time tracking | X | X | X |
| General ledger | | X | |
| Payroll | X | | |
| Time reporting | X | X | |
| Vacation/sick day tracking | | X | X |

complicates or forests integration of data from among departments. In this case, moving the organization to a single application trimmed software, hardware, and energy costs by over 60% resulted in smoother data flow within the company.

Your situation is not this dramatic, but if you take the time to map out your application domains, chances are you'll find some significant overlap. The business case for consolidating applications is easy to make because the projected results can (at least in part) be expressed in dollars saved. Data integration and operational improvements are just icing on the cake.

# Server consolidation

Most organizations have at least few "single purpose" servers that operate at 10% utilization or for example, we've seen many organizations that have dedicated NTP (network time protocol) servers. NTP is a low-overhead protocol that requires very little effort. Reserving a server for NTP is like flying a Boeing 767 cross-country with only one passenger.

Server consolidation is a close cousin of application consolidation and is equally effective. Instead of bundling multiple functions into one application, you bundle multiple services onto one server.

Unlike Windows, UNIX and Linux excel at preemptive multitasking. A good solution in the NTP case is to run the NTP daemon on the same servers that provide common infrastructural services such as DNS and Kerberos.

Another opportunity for server consolidation is presented by database servers that are dedicated to a single application. If you have competent systems and DBAs (as good monitoring), a single database server should be able to host the databases for many applications. Again, this consolidation reduces license fees, capital costs, and energy consumption.

> 5. NTP is a special case in that response latency is kept low. That doesn't mean you can't run other services on the same machine. NTP server daemons are commonly needed to give them ready access to the CPU when they want it (see page 129). You can achieve similar ends—perhaps even a bit more reliably—through server virtualization.