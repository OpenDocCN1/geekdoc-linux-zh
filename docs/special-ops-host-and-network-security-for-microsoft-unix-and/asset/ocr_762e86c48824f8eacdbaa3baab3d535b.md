(see Figure 11.20). Clearly the application was keeping state, checking to make sure that the GUID in value matched the Customer ID that made a request.

# Figure 11.20 State Checking Detected Modifications

![](bbox=[0.296, 0.153, 0.703, 0.393])

We tried this approach on multiple form-actions, from full balance inquiries to mini statements, and always got back an error message. Surprisingly, however, we found two places where no error message was returned. The first of these places was when we tried to transfer a balance from "our" account, to another one. The transaction appeared to go through, even though we were submitting someone else's CustomerID. Our balance didn't reflect the negative change so things were clearly looking up. We tried the transfer again, this time sending the money to another account of ours, waited a while and voila, now our balance reflected the one-dollar increase. As weird as it may seem in retrospect, the developers of the application had checked and managed state correctly for every permutation of commands, except for a simple (and probably the most disastrous of all) money transfer transaction. They knew the value of tracking state, and they were eventually bitten by the fact that they hadn't managed state consistently throughout the application.

# Executing and Examining

One of the major obstacles that an attacker faces when attempting to abuse custom Web applications is working blindly. An attacker can issue commands that could very well be successful and never receive feedback to indicate her success. Reverse engineering a Web application that gives no feedback can be linked to performing repairs on an automobile engine by going through the exhaust pipe. As mentioned earlier, one method of overcoming this with regards to SQL