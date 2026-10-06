
# EXERCISE 11.3: Departing Student Policy

- 1. Using the guidelines provided in this chapter (and other resources as needed), create a step-by-step IT security policy for handling user accounts/rights for a student that is leaving prematurely (drops, is expelled, etc.).
- 2. You will need to consider specialized student scenarios, such as a student who works as an assistant to a faculty member or as a lab assistant in a computer lab who may have access to resources most students do not.

# EXERCISE 11.4: New Faculty/Staff Policy

- 1. Using the guidelines provided in this chapter (and other resources as needed), create a step-by-step IT security policy for implementing a new user account for a faculty or staff member.
- 2. The policy should define what resources the employee will have access to, what she will not have access to, and any restrictions. (Hint: Unlike student policies, you will not need to define time length since it should be indefinite).

# EXERCISE 11.5: Leaving Faculty/Staff Policy

- 1. Write a policy for how to handle a faculty or staff member's departure (e.g., quit, fired, retired, etc.). Use the guidelines in this chapter and any other resources you like to get you started.
- 2. Make certain you consider not only shutting down access but the possibility of proprietary research material existing on the faculty or staff member's workstation.

# EXERCISE 11.6: Student Lab Use Policy

- 1. Considering the material in this chapter, create a set of policies for acceptable use of computer computers.
- 2. Make sure to specify web use, e-mail use, and any other acceptable uses.
- 3. Carefully spell out unacceptable usage (e.g., is game playing acceptable?).

# PROJECTS

# PROJECT 11.1: Examining Policies

- 1. Examine the following web resources that discuss security policies:
    * AT&T Acceptable use policy: https://www.att.com/legal/terms.au.html
    * Brown University Acceptable use policy: https://it.brown.edu/computing-policies/acceptable-use-policy/
    * SANS institute policies: https://www.sans.org/security-resources/policies/
- 2. Summarize the main theme of these policy recommendations. Pay particular attention to the area in which these recommendations differ from or exceed the recommendations of this chapter.
- 3. Choose the policy recommendation you believe is the most secure, and state the reasons for your choice.

# PROJECT 11.2: Examining Security Policies

- 1. Ask a local business or your college for a copy of its security policies. Study the policies carefully.
- 2. Summarize the main theme of these policy recommendations. Pay particular attention to any area in which these recommendations differ from or exceed the recommendations of this chapter.
- 3. Choose the policy recommendation you believe is the most secure, and state the reasons for your choice.

# PROJECT 11.3: Create Your Own Policies

Note: This project works well as a group project.

- 1. At this point in the book you have studied security, including policies. After this chapter and the preceding exercises and projects, you have examined several polices from various resources, as well as the policies of some actual organizations.
- 2. Take the brief policies created for the exercises in this chapter and expand them to create an entire working security policy for your academic institution. You will need to add administrative policies, developmental policies, and more.

# Chapter 12

# Assessing System Security

# Chapter Objectives

After reading this chapter and completing the exercises, you will be able to do the following:

* Evaluate a system's security.
* Scan a system for vulnerabilities.
* Evaluate the overall security of a network.
* Use the "Six Ps" of security.
* Apply a patch to your system.
* Document your security.

# Introduction

As you learn more about computer security, you will learn new techniques for securing a particular system. However, the ability to assess a system's security is critical. Before you can begin administering system, you must have a realistic assessment of the system's current state of security. This chapter discusses the essential steps that you should follow in assessing a system's security level. It is very important to assess a system's security level prior to implementing any security measures. You must be cognizant of the current state of affairs in order to properly address vulnerabilities. You should also conduct periodic security audits to ensure that the appropriate level of security is maintained.

It is commonplace for security professionals and firms to be contracted to audit a system's security. Whatever your purpose for assessing a system's security, you will need to have some framework within which to conduct your review.

# Risk Assessment Concepts

Evaluating the security of a network always starts with a risk assessment. This involves considering the assets you are trying to protect, the threats against them, vulnerabilities, and what measures you can take. The basic calculation is single loss expectancy (SLE), which is calculated by multiplying asset value (AV) by the exposure factor (EF). For example, if a laptop is $800 and the exposure factor is .9, then the SLE is:

SLE = AV × EF = $720

The next formula is annualized loss expectancy (ALE). This is SLE multiplied by annual rate of occurrence (ARO). For example, if you think you will lose six laptops per year, the calculation is:

ALE = SLE × ARO = $720 × 6 = $4320

- Mitigation: This means you take steps to lessen the risk. No matter what you do, there is likely to be some risk left. For example, if you are concerned about malware, then running antivirus is a common solution.
- Avoidance: This is difficult to do. It means you have zero risk. For example, if you are concerned about users downloading a virus from a website, the only way to completely avoid that is not giving them access.
- Transfer: This is transferring the risk to someone else. The most clear example is cyber insurance. If you have such insurance, then the cost of a risk being realized will be passed to the insurance company.
- Acceptance: If the probability of the risk is very remote, or the cost of mitigation is higher than the cost of the risk being realized, you may choose to do nothing and simply accept it.

# Evaluating the Security Risk

In Chapter 1, “Introduction to Network Security,” we provided a method for assigning a numeric value to your system’s security based on several factors. In this section we will expand upon that system. Recall we evaluated three aspects of your system:

- Attractiveness to attackers
- Nature of information
- Level of security

The system being evaluated was given a numeric designation between 1 and 10 for each of these factors. The first two are added together, and then the third number (level of security) is subtracted. The lower the number, the more secure your system; the higher the number the greater your risk.

The best rating is for a system that:

- Receives a 1 in attractiveness to hackers (i.g., a system that is virtually unknown, has no political or ideological significance, etc.)
- Receives a 1 in informational content (i.g., a system that has no confidential or sensitive data on it)
- Receives a 1 in security (i.e., a system with an extensive layered, proactive security system complete with firewalls, ports blocked, antivirus software, IDS, anti-spyware, appropriate policies, all workstations and servers hardened, etc.)

This hypothetical system would get a score of 1 + 1 – 10, or –8. This is the lowest threat score possible. Conversely, the worst rating is for a system that:

- Receives a 10 in attractiveness (i.g., a well-known system that has a very controversial ideological or political significance)
- Receives a 10 in informational content (i.g., a system that contains highly sensitive financial records or classified military data)
- Receives a 1 in security (no firewall, no antivirus, no system hardening, etc.)
