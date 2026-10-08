# Chapter 7: Attacking Session State Management

Decipher the State Information If the state information is stored in a nonobvious manner, then you will have to perform some type of analysis.

Before we try to attack the session state mechanism, we first have to figure out where to find it. The next two sections describe common methods for handling state via the client and the server.

# CLIENT-SIDE TECHNIQUES

In the James Bond movies just about every villain explains his nefarious plot of world domination to 007, trusting that an elaborate trap or eccentric mercenary will silence Bond before he foils the plan. Web applications often share the villain's character flaw of

| Session Attribute | Description |
| --- | --- |
| Username | A rather obvious field, but sometimes used to track the user in order to customize pages. For example, inserting "Welcome back, Tori!" when a user logs in the application. |
| User Identifier | Web applications that use databases to track users have some form of numeric index that uniquely identifies the user. In many cases, this could simply be the row number in a database table where the user's information is stored. |
| User Roles | What type of users are accessing the application? Can they view data? Modify data? Manage other user accounts? |
| User Profile | The profile could contain innocuous information, such as the preferred background color for the Web site, or sensitive information as home address and credit card number. |
| Shopping Cart | For online shopping, this is the driving force for session management. The cart contains everything the user wishes to buy. The Username and User Identifier will not change during subsequent visits to the application, but the Shopping Cart needs to track dynamic information. |
| Session Identifier | The application or the Web server sometimes assigns a session value that is valid for a short time frame. |
| Table 7-1. | Common Information Tracked During a Session |