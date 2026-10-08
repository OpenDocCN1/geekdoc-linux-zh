Like any other authentication system, Passport is also potentially vulnerable to password guessing attacks (the minimum password length is six characters, with no requirements for different case, numbers, or special characters). Although there is no permanent account lockout feature, after a certain number of failed login attempts, an account will be temporarily prevented from logging in this lasts “a few moments” according to the error message). This is designed to add significant time to password guessing attacks. Attackers may attempt to reset their passwords during a block, but must answer a “secret question” set by the Passport account owner during registration.

Despite these issues, we owe Passport is a strong option for Web sites that don’t mind if else owns their customers' authentication credentials.

# ATTACKING WEB AUTHENTICATION

So far, we’ve described the major authentication mechanisms in the Internet. How are such mechanisms attacked? In this section, we discuss techniques that can be used to exploit common vulnerabilities in Web authentication and conclude with recommendations on how to avoid these pitfalls.

A quick note before we begin—that authentication exists for an application suggests that the application developer has created some security infrastructure to prevent the casual hacker from easily accessing other users' data. Hence, attacking-Web authentication is not going to be a walk in the park. As always, however, it’s the implementation that brings down the house, as we will see next.

# Password Guessing

Although not the sextiest of attacks, password guessing is the most effective technique to defeat Web authentication. Assuming there isn’t some flaw in the selection of authentication protocol or its implementation, the most vulnerable aspect of most authentication systems is user password selection.

Password guessing can be carried out manually or via automated means. Manual password guessing is tedious, but when human intuition frequently beats automated tools, especially when customized error pages are used in response to failed forms-based login attempts. When performing password guessing, our favorite choices are shown in Table 5-3.

As you can see, this is a rather limited list. With an automated tool, an entire dictionary of username/password guesses can be thrown at an application more quickly than human can type them.

Password guessing can be performed against almost all types of Web authentication covered in this chapter. We will discuss two that attack Basic and Forms-based auth presents, but tools to attack Digest and NTLM are also feasible.