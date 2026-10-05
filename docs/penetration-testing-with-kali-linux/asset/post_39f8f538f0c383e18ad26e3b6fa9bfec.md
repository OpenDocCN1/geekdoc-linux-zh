
In this case, the answers to these questions may reveal keys to future successful study sessions.

Let's say we studied for one hour in the morning after a light breakfast at the dining room table with a cup of coffee, using our own version of the Feynman Technique. If that led to a successful session, it's worth making a note of this and then planning the next study session to recreate as much of the scenario as possible.

Finally, as a closing note, we want to acknowledge that we can't possibly cover every effective strategy or give a full picture of all the things involved in learning a new set of skills. We hope that the items presented in this Module are useful and helpful in some way.

If you are a learner just starting out with OffSec's training, we want to wish you the best of luck on your journey.

## Report Writing for Penetration Testers

We will cover the following Learning Units in this Learning Module:

- Understanding Note-Taking
- Writing Effective Technical Penetration Testing Reports

This Module is designed to help Penetration Testers understand how to deliver effective reports to their clients.

## 5.1 Understanding Note-Taking

In this Learning Unit we will cover the following Learning Objectives:

- Review the deliverables for penetration testing engagements
- Understand the importance of note portability
- Identify the general structure of pentesting documentation
- Choose the right note-taking tool
- Understand the importance of taking screenshots
- Use tools to take screenshots

### 5.1.1 Penetration Testing Deliverables

A penetration test or red team exercise is difficult to scope in advance. This is because the tester cannot consistently anticipate exactly what kind of machines or networks the client will want to be tested.

> Even though the outcome of our assessment is often unpredictable, it is often recommended to define a detailed scope during the preliminary meetings with the customer. This process is especially verify when prioritizing business critical targets within large networks.

While the general execution plan for a penetration test will often follow a pattern maxim, "no plan survives first contact with the enemy"195. This means that any specific activities we might expect during the engagement might not actually happen, since the reality of the testing environment is almost certainly different than our initial ideas and hypotheses about. It is therefore difficult to report on penetration tests using standard forms. This is especially the case when the test is carried out with little discussion with the client, for example, if the client is looking to support their defending teams in some manner.

194 (Aon, 2022), https://www.a.com/cyber-solutions/thinking/penetration-testing-or-red-team/
195 (Helmut von Moltke, 1871), https://quoteinvestigator.com/2021/05/04/no-plan

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

## OffSec

As such, instead of preparing a report in advance ensure that the penetration test is executed and notes are taken as it proceeds to ensure a detailed record of what was done. This makes sure that:

- the penetration test can be repeated if it becomes necessary to demonstrate that an issue is real.
- the penetration test can be repeated after remediation to confirm that an issue has been fixed.
- if there's a system failure during the period of the penetration test, the client and tester can determine if the testing was the cause of the failure.

During a network, some activities may not be permitted. We have to be very clear about the Rules of Engagement (RoE)¹¹⁹⁶ under which the testing is done. When conducting red team, a person will be assigned the role of “referee” to ensure that the rules of engagement are observed. There may be constraints placed on testing such as not carrying out denial of service attacks, or not engaging in social engineering. Furthermore, the testing work may be in response to the client's regulatory compliance requirements and may need to follow a specific methodology such as the OWASP Penetration Testing Execution Standard.¹¹⁹⁷ Any constraints need to be very clear from the outset.

### 5.1.2 Note Portability

Portability of penetration testing notes meaning able to pass notes on to others. Writing notes that are concise and coherent is an integral part of successful note-taking, and enables the notes to be used by ourselves but also by others. Additionally, concise notes can be quickly adapted for technical reporting.

The need for portability is particularly emphasized when a penetration tester has to leave an engagement because of sickness, illness, or other issues. Having a shared understanding of how notes should be taken is especially important for large penetration testing teams, where individuals need to be able to understand the details of other team members' engagements at will.

### 5.1.3 The General Structure of Penetration Testing Notes

We need to use a structured approach to note-taking that is both concise and precise. There are an uncountable of ways in which we might organize our notes, and it would be futile to attempt to provide a one-size-fits-all set of recommendations. Nevertheless, here are some principles that one needs to consider:

- Rather than taking a few general notes assuming that we will remember to perform certain actions in time, we should record exactly what we did.
- This means that every command that we type, every line of code that we modify, and even anywhere we click in the GUI be recorded so that we can reproduce our actions.

¹¹⁹⁶ (Microsoft, 2022), https://www.microsoft.com/en-us/msrc/penetest-tests-of-engagement
¹¹⁹⁷ (OWASP, 2022), https://www.owasp.org/project-web-security-testing-guide/latest/3-The_OWASP_Testing_Framework

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

## OffSec

## Penetration Testing with Kali Linux

- Even if we've taken a lot of notes, looking at them later doesn't help us.
- The notes need to be structured and sufficiently detailed to remove any ambiguity.
- To write a convincing and substantial technical report, we need to provide sufficient technical details within our notes.
- If the notes are not written coherently, it will be difficult for someone else to repeat the test.

The structure we recommend here for note-taking is sufficiently abstract to allow for personal preferences. As a general rule, we would like to remind us of what occurred, and also allow us to replicate the notes. A note-taking structure that starts broad and drills down into each section is an easy and expandable method of taking. The top-down approach allows us to start with the broadest activity, and then narrow our focus and expand the level of detail until we have everything we need.

Let's now look at an example of the notes we might take for a web vulnerability:

- Application Name: This is important in a multi-application test, and a good habit to get into. The application names also lends itself to building a natural folder and file structure nicely.
- URL: This is the exact URL that would be used to locate the vulnerability that we've detected.
- Request Type: This represents both the type of request (i.e. GET, POST, OPTIONS, etc) that was made, as well as any manual changes we made to it. For example, we might intercept a POST request message and change the username or password before forwarding it on.
- Issue Detail: This is the overview of the vulnerability that will be triggered by our actions. For example, we may point to a CVE describing the vulnerability if one exists, or explain the impact we observe. We may categorize the impact as denial of service, remote code execution, privilege escalation, and so on.
- Proof of Concept: This is a string or code block that will trigger the vulnerability. This is the most important part of the note, as it will drive the issue home and allow it to be replicated. It should list all of the necessary preconditions, and provide the exact code or commands that would need to be used to perform the vulnerability again.

Let's get more specific and review an example of testing for a Cross-Site Scripting (XSS) vulnerability. The target we tested has a web page named XSSblog.html. When we navigate to it, we can enter a blog entry.
