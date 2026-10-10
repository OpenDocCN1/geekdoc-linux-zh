# # BUGS

Non-superusers cannot increase scheduling priorities of their own processes, even if they were the ones that decreased the priorities in the first place.

The Linux kernel (at least version 2.0.0) and linux libc (at least version 5.2.18) does not agree entirely on what the specifics of the systemcall interface to set nice values is. Thus causes renice to report bogus previous nice values.