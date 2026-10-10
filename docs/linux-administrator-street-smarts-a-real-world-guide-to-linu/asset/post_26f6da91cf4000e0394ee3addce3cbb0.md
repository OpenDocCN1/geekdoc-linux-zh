` block.

**Tasks:**
1.  **Correct OCR errors**:
    *   "Procdure" -> "Procedure"
    *   "Interneten" -> "Internet"
    *   "chkrtookit" -> "chkrootkit" (likely a typo in OCR or original, but "chkrootkit" is the standard tool name mentioned in this context, though the text says "using Tripwire, and using chkrtookit". Checking context: "chkrtookit" is almost certainly "chkrootkit". Let's look closely at "chkrtookit". It looks like a typo for `chkrootkit`. I will correct it to `chkrootkit`.)
    *   "http://www.cert. org" -> "http://www.cert.org" (remove space)
    *   "http://www.securityfocus.com/archiv e/1" -> "http://www.securityfocus.com/archive/1" (remove space)
    *   Check for other typos. "Beware of suspicious notices..." seems fine.
    *   "crypticide" link seems fine.
    *   "flipping" or other words? No obvious ones.
    *   "Interneten" is clearly "Internet".
    *   "Procdure" is clearly "Procedure".
    *   "chkrtookit" -> `chkrootkit`.
    *   "archiv e" -> `archive`.
    *   "cert. org" -> `cert.org`.

2.  **Merge pages**: Remove `[PAGE X]` markers and join content.

3.  **Identify Headings**:
    *   `# Criteria for Completion` -> `## Criteria for Completion` (based on hierarchy, likely section under a larger chapter). The input uses `#` for major headers like `Task 7.4`. I should map `#` to `##` if the document structure implies it's a subsection, or keep as `#` if it's a top-level title. Given `Task 7.4` is a major task, `Criteria for Completion` is likely part of it. The OCR has `# Criteria for Completion` and `# # Task 7.4`. The double `#` suggests `Task 7.4` is a higher level. Let's standardise. Usually, OCR might get hashes wrong.
    *   Looking at the structure:
        *   `# # Task 7.4: Monitor for Security Breaches` -> This is likely `## Task 7.4...` or `# Task 7.4...`.
        *   `# ## Scenario` -> `### Scenario`
        *   `# ## Scope of Task` -> `### Scope of Task`
        *   `# ## Duration` -> `### Duration`
        *   `# ## Setup` -> `### Setup`
        *   `# ## Caveats` -> `### Caveats`
        *   `# Procdure` -> `### Procedure` (assuming it's a sub-section like the others)
        *   `# Monitoring Internet Security Resources` -> `### Monitoring Internet Security Resources` (or `##` if it's a new major section). Given it follows "Procedure" which lists subtasks, this is likely a sub-section under the task or the procedure.
    *   Let's look at the first page. It ends with `# Criteria for Completion`.
    *   The next page starts with `# # Task 7.4`.
    *   It seems `Task 7.4` is the main header. `Criteria for Completion` might be the end of `Task 7.3` or similar.
    *   I will treat single `#` in OCR as a potential heading level and refine.
    *   `# # Task 7.4` -> `## Task 7.4: Monitor for Security Breaches` (Assuming Task is H2, chapters are H1). Or if `Task 7.4` is H1, then subheaders are H2.
    *   Let's look at the style. "Task 7.4" suggests a numbered task. "Scenario", "Scope", "Duration", "Setup", "Caveats" are sub-parts.
    *   I will format `Task 7.4` as `##` and the sub-parts (`Scenario`, etc.) as `###`.
    *   `Procedure` is listed under the task context, so `###`.
    *   `Monitoring Internet Security Resources` is one of the "four subtasks" mentioned in Procedure. So it should probably be `###` or a bold title. The OCR has `#`. I'll make it `###` to match the hierarchy of the previous sub-sections, or `##` if it's a major section. Given "keeping an eye on Internet security information" is a subtask of the Procedure, and the text describes it in detail, it might be a section. I will use `###` to be safe, consistent with `Scenario` etc.
    *   Wait, `Criteria for Completion` is on page 344. `Task 7.4` starts on page 345. So `Criteria for Completion` belongs to the previous task (likely 7.3). I will format it as `## Criteria for Completion`.

4.  **Lists**:
    *   The text under "Monitoring Internet Security Resources" has bolded terms like **CERT/CC**, **US-CERT**, etc. These act as list items. I will format them as a list with bold headers or just bold text followed by description. The prompt asks for list items with `-`.
    *   Example:
        -   **CERT/CC** The Computer Emergency...
        -   **US-CERT** The United States...
    *   This seems appropriate.

5.  **Tables**: No obvious tables.

6.  **Images**: Keep the image link.

7.  **Output**: Wrap in `[content]`.

**Detailed Correction Pass:**

*   **Page 344**:
    *   "Beware of suspicious notices and activity" -> No change.
    *   "crypticide" link -> No change.
    *   Image -> Keep.
    *   `# Criteria for Completion` -> `## Criteria for Completion`
    *   "hard-to-guess base with modifications that make the password even harder to guess." -> No change.
    *   "ongoing practices" -> No change.

*   **Page 345**:
    *   `# # Task 7.4: Monitor for Security Breaches` -> `## Task 7.4: Monitor for Security Breaches`
    *   "set and forget" -> No change.
    *   `# ## Scenario` -> `### Scenario`
    *   `# ## Scope of Task` -> `### Scope of Task`
    *   `# ## Duration` -> `### Duration`
    *   `# ## Setup` -> `### Setup`
    *   `# ## Caveats` -> `### Caveats`
    *   "risk free" -> "risk-free" (standard spelling, though "risk free" is acceptable, I'll stick to minimal changes unless it's a clear OCR error. "risk free" is fine).
    *   "chkrtookit" is on page 346.

*   **Page 346**:
    *   `# Procdure` -> `### Procedure` (Correcting spelling "Procdure" to "Procedure").
    *   "Interneten" -> "Internet".
    *   "chkrtookit" -> "chkrootkit".
    *   `# Monitoring Internet Security Resources` -> `### Monitoring Internet Security Resources` (Assuming it's a sub-section of the procedure/task).
    *   List items:
        *   **CERT/CC** ... `http://www.cert. org` -> `http://www.cert.org`
        *   **US-CERT** ...
        *   **CIAC** ...
        *   **CVE** ...
        *   **SecurityFocus and Bugtraq** ... `http://www.securityfocus.com/archiv e/1` -> `http://www.securityfocus.com/archive/1`
        *   **Linux Security** ...
        *   **Distributions’ Web sites** ...
        *   **Product Web pages and mailing lists** ...

Let's refine the heading levels.
If `Task 7.4` is `##`, then `Scenario`, `Scope`, `Duration`, `Setup`, `Caveats`, `Procedure` are `###`.
`Monitoring Internet Security Resources` is a specific topic within the procedure. I will make it `###` or just a bold line. The OCR has `#`. I'll use `###` to maintain structure.

Wait, `Criteria for Completion` on page 344 is likely the end of the previous task. I'll make it `##`.

Let's check the image link: `![](img/f430a19bdf014c43ad7c2d594afd5b21_344_0.png)`. Keep as is.

Final check on typos:
- "Procdure" -> "Procedure"
- "Interneten" -> "Internet"
- "chkrtookit" -> "chkrootkit"
- "cert. org" -> "cert.org"
- "archiv e" -> "archive"

Structure:
## Criteria for Completion
(Text...)
![image]
(Text...)

## Task 7.4: Monitor for Security Breaches
(Text...)

### Scenario
(Text...)

### Scope of Task
(Text...)

### Duration
(Text...)

### Setup
(Text...)

### Caveats
(Text...)

### Procedure
(Text...)

### Monitoring Internet Security Resources
(Text...)
- **CERT/CC** ...
- **US-CERT** ...
...

This looks consistent.

One detail: The prompt says "If there is only an image link...". There is text, so I include text.
Prompt says "Do not include [PAGE X]".
Prompt says "Output should be included in [content]...".

Let's double check `chkrtookit`. Is it `chkrtoolkit`? No, `chkrootkit` is the standard rootkit checker. `chkrtookit` is a very likely OCR misread of `chkrootkit` (r->r, o->t? No, `chkr` vs `chk`. `chkrtookit` looks like `chk` + `r` + `toolkit`? Or `chkrootkit` misread as `chkrtookit`?
`chkrootkit` -> `chkr` `ootkit`?
Actually, `chkrtookit` is likely `chkrootkit` with OCR errors (`r` instead of `ro`, `t` instead of `t`).
Or it could be `Chktoolkit`?
In the context of Tripwire and security, `chkrootkit` is the standard companion tool mentioned in older Linux security books (like "Linux System Administration" or similar). I will correct to `chkrootkit`.

"Interneten" -> "Internet".
"Procdure" -> "Procedure".

Ready to generate.

[content]
## Criteria for Completion

To complete this task, you should have generated two new passwords: one for your user account and one for **root**. Both passwords should be built from a hard-to-guess base with modifications that make the password even harder to guess. The final part of this task relates to ongoing practices rather than a single objective; you must employ safe and avoid unsafe practices with respect to protecting your password in day-to-day use. Because all users with regular Linux accounts have passwords, all of your users should be made aware of these password generation and protection practices.

**Beware of suspicious notices and activity** If your login failed but you think you typed the password correctly, change your password at once—especially if you logged in using a public terminal. If somebody’s lurking nearby when you log in, be careful to shield the terminal as you type the password. Never give your password to anybody else. As a general rule, odd occurrences—both in software and in human behavior—should be treated with suspicion. These events may have perfectly innocent explanations, but if in doubt, take appropriate actions to protect your account. Changing your password is cheap insurance against many types of attack.

Many of these protective measures are essentially defenses against social engineering. Others defend against network sniffing or other dangers. All of them must be practiced by ordinary computer users, which means that you, as a system administrator, must find a way to educate your users. In some cases this is easy; for instance, if you’re running Linux on a personal workstation, you may be the only user. In other cases, you may need to include password education in a formal user training program.

One other step you may want to consider as a system administrator is auditing your users’ passwords. You can run a password-cracking program, such as Crack (`http://www.crypticide.org/users/alect/`), to discover weak user passwords. You can then notify users of their weak passwords and give them some time to correct the matter. For the best security, transfer the password file via floppy disk to a computer that’s not connected to the network and run the password-cracker on it. This practice will minimize the chance that a miscreant will stumble upon your password cracking.

![](img/f430a19bdf014c43ad7c2d594afd5b21_344_0.png)

Although discovering weaknesses in your system security in order to correct problems is an admirable goal, most organizations have strict policies forbidding activities such as password cracking. To avoid running afoul of such policies, even though you’re doing it in the service of improving system security, be sure to clear password-cracking activity with somebody who has the proper authority. Obtain this authorization in the form of a written and signed document, not merely a verbal approval. Failure to obtain permission to crack users’ passwords may cost you your job or even result in criminal charges being filed against you.

## Task 7.4: Monitor for Security Breaches

Many Linux features fall into the “set and forget” category—you can configure them in a way that’s reasonable and then leave that configuration in place until new local needs, a software upgrade, or some other factor forces you to make a change. Sadly, this isn’t true of security. Because crackers are constantly discovering new vulnerabilities and means of attack, a configuration that was, to the best of your knowledge, perfectly good yesterday may be hopelessly unsafe today. Even if you believe a computer was reasonably secure, it’s possible that a cracker could exploit a vulnerability you didn’t know about. For these reasons, you should keep on the alert for security breaches and take steps to keep your system secure.

### Scenario

You’ve configured a computer with what you believe is an adequate level of security. You must now plan how to keep the computer’s security level reasonable and monitor it for intrusion in case you’ve overlooked a vulnerability. To do this, you’ll use software update tools, monitor security resources, and monitor your system for signs of intrusion.

### Scope of Task

In some sense, this task is an open-ended one; your security monitoring task is never complete. Creating a basic plan for security monitoring is more bounded, though.

### Duration

Planning your security monitoring regimen should take an hour or two. Actually implementing that plan will require countless hours over the next weeks, months, and years.

### Setup

To plan to monitor your system for security breaches requires little in the way of setup; you’ll just need a regular account on an Internet-connected computer to refer to some Internet resources. Actually doing the monitoring, though, requires user access to the computer and occasionally **root** access.

### Caveats

Planning your monitoring activities is fairly risk free; however, implementing them isn’t. Some parts of this task require **root** access, for which the usual caveats apply. Aside from those caveats, most security monitoring tasks are fairly innocuous and unlikely to cause harm. One exception is installing updated software, which runs the risk of causing a serious cascade of problems if the new software doesn’t work exactly like the old version.

### Procedure

Keeping your system secure can be a full-time job if you do everything that’s possible. To keep this task manageable, I focus on just four subtasks: keeping an eye on Internet security information, maintaining your system software, using Tripwire, and using chkrootkit.

### Monitoring Internet Security Resources

You should get into the habit of reviewing several security Web sites and other resources to learn about new threats:

- **CERT/CC** The Computer Emergency Response Team Coordination Center (http://www.cert.org) hosts general security information, including information on the latest threats. Periodically reviewing this site will help you keep up-to-date with security developments.
- **US-CERT** The United States Computer Emergency Readiness Team (http://www.us-cert.gov) has taken over some of the duties formerly held by CERT/CC. In practice, both sites are worth monitoring.
- **CIAC** The Computer Incident Advisory Capability (http://ciac.llnl.gov/ciac/), run by the U.S. Department of Energy, is similar to CERT/CC and US-CERT in many respects, but its Web page gives greater emphasis to current threats and less coverage of general security practices.
- **CVE** The Computer Vulnerabilities and Exposures (http://cve.mitre.org) site is dedicated to maintaining a dictionary of vulnerability names. This information can be useful in facilitating communication about problems. The CVE contains less in the way of descriptions of the vulnerabilities and exploits it names, though.
- **SecurityFocus and Bugtraq** The SecurityFocus Web site (http://www.securityfocus.com) is yet another general security site. One of its important features is that it hosts the Bugtraq mailing list (http://www.securityfocus.com/archive/1), which can be a good way to keep informed—subscribe, and alerts about new threats will be delivered to your email account soon after they’re made public.
- **Linux Security** The Linux Security site, http://www.linuxsecurity.com, is very similar to CERT/CC, US-CERT, CIAC, and SecurityFocus in many ways. Linux Security, though, caters to Linux in particular and so may be more helpful in addressing Linux-specific issues or in pointing to Linux-specific fixes.
- **Distributions’ Web sites** Most Linux distributions maintain security information on their Web sites. Go to your distribution’s main page and look for links relating to security. These sites can provide specific upgrade instructions for your distribution in particular.
- **Product Web pages and mailing lists** Many programs have Web pages and mailing lists, and these can be good resources for learning of security problems related to these programs. Of course, regularly perusing all of the pages related to the hundreds of programs that make up a Linux system can be a full-time job. You might want to keep an eye on the Web pages or mailing lists for any high-profile server programs that you run, such as the Apache Web server or the sendmail mail server.
