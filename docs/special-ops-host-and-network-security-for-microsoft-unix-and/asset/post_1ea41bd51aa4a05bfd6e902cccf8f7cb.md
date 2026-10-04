
## Chapter 18 • Creating Effective Corporate Security Policies

be careful to do so in a way that you can easily update all the policies at once. Breaking policies and procedures into manageable pieces also helps to make them more easily accessible.

Finally, we need to consider education in our policy distribution program. Some employees may take their own initiative to familiarize themselves with the corporate security policies. The rest of them, which is usually most of them, will require a fair amount of coaxing and convincing to get them to read the policies. Ever more coaxing and convincing will be required if you want them to sign a form acknowledging their receipt and understanding. Fortunately, a variety of tools are available to help you coax and convince.

First of all, you can play a variety of games with how you present the policies to employees. For example, if you request employees to review only a small number of policies immediately relevant to them, they may be more likely to do so. This is effective if you first show them the number of policies that apply to everyone else. Another way of presenting policies is to deliver them in installments, with a statement of receipt and understanding. By presenting them in bite-sized chunks, employees may be more receptive to the idea of reading the policies. For example, bite-sized chunks of policy may come in the form of posters, screensavers, or newsletters, informing them of one small but important piece of the policy program. Given enough time, most of your important policies can be distributed through the organization.

Finally, usually more effective than requiring a statement of understanding is to require that employees take a quiz on their policy knowledge. A quiz initially appears to be a part of the enforcement section but is really awareness in disguise. Questions are usually simple enough that employees can guess the correct answer, but enough that they need to think about the question. This puts an additional burden on employees, it will usually result in a more secure and productive environment in the long run. I have seen some clients that take this as far as restricting the intranet, Internet, even terminal access before the appropriate policy quizzes are passed. Another advantage is that this provides an audit trail which you can check to see how many of your employees have taken and passed the quiz. Not required, some tools can help you in quizzing your employees. They allow you to dig deeper, identify areas in the policies where employees are having particular trouble.

Here are some links that are useful in creating an awareness program:

- www.pentasafe.com/products/vpc/ An example of a tool you can use to quiz your employees on your vpc security policies.
- http://csc.nist.gov/ATE/awareness.html NIST created a small guide to help assemble an awareness program.
- http://csc.nist.gov/publications/drafts/draft800-50.pdf NIST guidelines for creating an awareness program.
- http://rr.sans.org/aware/aware_list.php SANS has a section dedicated to security awareness.
- http://nativeintelligence.com/awareness/cschch29kr.PDF An excerpted chapter that reviews the basics of a security awareness program.

## Creating Effective Corporate Security Policies • Chapter 18

## Policy Enforcement

Policy enforcement was alluded to in the previous section, when requiring your employees to take policy comprehension quizzes. Quizzes can act as both a means of education and enforcement, depending on how they are structured. Usually, they perform both roles. Quizzes can be given using either manual or automated tools, discussed below.

There are two sections we can address under policy enforcement. One is the old-fashioned way of policy enforcement, using manual techniques, such as quizzes, spot checks, and discipline. The other means is using automated policy enforcement techniques, of which there are multiple vendors of software that performs checks, produces quizzes, and tracks individual employee's compliance.

## Manual Techniques for Enforcing Policies

There are a wide variety of tools and techniques available to policy administrators to help them check for policy compliance and enforce those policies. I already addressed the utility of utilizing employees on their policy knowledge. This can be performed on either a one-time basis, or on any schedule that is appropriate. Quizzes can be created on intranet sites, issued as stand-alone software, or performed on paper.

The most popular, and essential, tool for enforcing policies is to perform a policy and procedure review. This is usually performed through means of a gap analysis against some baseline standard. Once a review is performed, your security policy administrator can take note of the areas where policies, procedures, or procedural enforcement are lacking.

One proposed method of policy enforcement, by Char van der Walt, is of the “Resource Centre Model,” whereby the policy itself is self-policing. The guidelines are located in a central resource, and the individuals have access to the policies, and are responsible for bringing themselves in compliance. Compliance is then enforced through the audit department, by means of spot checks or network scans, to check up on users.

One of the more effective, expensive, techniques in policy enforcement brings up one of the themes in this chapter: to have a designated individual responsible for policy and procedure enforcement. This humanforcer, call them the policy police, is responsible for knowing the current policies and checking employees for compliance. This person may become one of the least liked people in the company, if they are not careful how they go about enforcing the policies.

The policy police have a wide array of tools to detect and enforce policy violations. Some groups perform red penetration tests at unexpected times, to check that network controls are properly in place and patches are up-to-date. Some groups hire external consultants to perform these penetration tests, if the resources are not available internally. A multitude of companies, such as Stone, ISS, and @stake, offer penetration testing services. Performing your policy review is covered more in the “Reviewing Corporate Security Policies” section.

Once the policy police have identified the areas where policies and procedures are not being followed, they need to take action. We are assuming that the policies and procedures are complete and do not have any gaping holes. Resolution may be as simple as reissuing the policies or procedures, or requiring the offending individuals to take or retake the policy quizzes. If this appears to be a habitual problem, the policy police need to be both authorized and capable of taking more severe action. This may range from removing or restricting information access, to employment termination, to criminal prosecution. Employment contracts usually have specified grounds for termination; it is up to the policy police to take appropriate action if warranted by the employee’s actions. The individuals responsible for enforcing policies, the policy police, must be given the appropriate tools and jurisdiction to affect consequences on offending individuals. If there are no means of leaving consequences in the current policy program, it may be as effective as a dog without teeth. There must be consequences for violating corporate policies, and those consequences should be clearly explained in the policy document and in employee contracts.

Finally, manually policy techniques can catch violations that automated scanners miss. Usually this takes place during the policy interviews, during the policy review process. For example, if the interviewer asks “Are your passwords stored in a secure location,” and the response is “Yes, right here under my keyboard,” it becomes clear that policies are not being distributed or enforced properly. Errors or oversights in organizational structure, information handling, and physical security can be identified and remediated through the interview process.

## Automated Techniques for Enforcing Policies

Automated policy tools have only recently been introduced into the market, and can be thought of as a subset of vulnerability scanners. They can be very helpful if used properly, like most tools, can hurt if you use improperly. Policy scanners are available from a variety of companies, including NetIQ (Formerly Pentasafe, purchased October 2002; the new brand name is NetIQ VigilEnt), Symantec and PoliVec. As discussed previously, NetIQ and PoliVec can help you create your policy builder software and deploy them to employees. This allows you to develop your policy and deploy it using the same software. Symantec, a relatively new player in the automated security market, provides the user with templates based on industry standards or government guidelines, and scans your network for compliance with those standards or guidelines. BindView, also a new player in this field, has created the Policy Operations Center, which helps you to manage your policies in one resource and track how they are used.

Network scanning for policy compliance can involve deploying an agent on each machine, which may be difficult for a large network that does not have push software already installed. These scanners can check for Registry settings, version and patch updates, even password complexity requirements. Some scanners include password cracking software, so you can also audit your users' password strength. Descriptions of different policy scanners are available at the following Web:

- NetIQ (Formerly Pentasafe) www.netiq.com/solutions/security/default.asp
- Symantec http://enterprisesecurity.symantec.com/products/products.cfm?productID=45
- PoliVec www.polivec.com
- BindView www.bindview.com/products/PolicyCenter/operations.conf
