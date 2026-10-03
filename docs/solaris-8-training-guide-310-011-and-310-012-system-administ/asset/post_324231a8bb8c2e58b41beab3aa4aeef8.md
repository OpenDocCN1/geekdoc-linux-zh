
## Commonsense Strategies

Finally, you also should follow commonsense practices when studying. Study when you are alert, reduce or eliminate distractions, take breaks when you become fatigued, and so on.

## Pre-Testing Yourself

Pre-testing enables you to assess how well you are learning. One of the most important aspects of learning is what has been called meta-learning. Meta-learning has to do with realizing when you know something well or when you need to study some more. In other words, you recognize how well or how poorly you have learned the material you are studying.

For most people, this can be difficult to assess objectively on their own. Practice tests are useful in that they reveal more objectively what you have learned and what you have not learned. You should use this information to guide review and further study. Developmental learning takes place as you cycle through studying, assessing how well you have learned, reviewing, and assessing again until you think you are ready to take the exam.

You may have noticed the practice exam included in this book. Use it as part of the learning process. The ExamGear software on the CD-ROM also provides a variety of ways to test yourself before you take the actual exam. By using the practice exam, you can take an entire timed, practice test quite similar in nature to that of the actual Solaris exam. The ExamGear Adaptive Exam option can be used to take the same test in an adaptive testing environment. This mode monitors your progress as you are taking the test to offer you more difficult questions as you succeed. By using the Study Mode option, you can set your own time limit, focus only on a particular domain (for instance, System Security), and also receive instant feedback on your answers.

Set a goal for your pre-testing. A reasonable goal would be to score consistently in the 90% range.

See Appendix F, “Using the ExamGear, Training Guide Edition Software,” for a more detailed explanation of the test engine.

## Exam Prep Tips

The Solaris certification exam reflects the knowledge domains established by Sun. The exam is based on a fixed set of exam questions. The individual questions are presented in random order during a test session. If you take the same exam more than once, you will see the same number of questions, but you won’t necessarily see the same questions.

Solaris exams are identical in terms of content coverage, number of questions, and allotted time, but the questions differ. You might notice, however, that some of the same questions appear on, or rather are shared among, different final forms. When questions are shared among multiple final forms of an exam, the percentage of sharing is generally small.

Solaris exams also have a fixed time limit in which you must complete the exam. The ExamGear test engine on the CD-ROM that accompanies this book provides fixed-form exams.

Finally, the score you achieve on a fixed-form exam is based on the number of questions you answer correctly. The exam’s passing score is the same for all final forms of a given fixed-form exam.

Table 1 shows the format for the exam.

### TABLE 1
### Time, Number of Questions, and Passing Score for Exam

| Exam | Time Limit in Minutes | Number of Questions | Passing % |
|---|---|---|---|
| Solaris 8 Certified System Administrator for the Solaris 8 Operating environment: Part 1 | 90 | 57 | 66 |
| Solaris 8 Certified System Administrator for the Solaris 8 Operating environment: Part 2 | 90 | 61 | 70 |

Question types on both exams are multiple choice, fill in the blank, and matching.

Remember that you do not want to dwell on any one question for too long. Your 120 minutes of exam time can be consumed very quickly.

## Putting It All Together

Given all these different pieces of information, the task now is to assemble a set of tips that will help you successfully tackle the Solaris certification exam.

## More Pre-Exam Prep Tips

Generic exam-preparation advice is always useful. Tips include the following:

- Become familiar with general terminology, commands, and equipment. Hands-on experience is one of the keys to success; it will be difficult, but not impossible, to pass the exam without that experience. Review the chapter-specific study tips at the beginning of each chapter for instructions on how to best prepare for the exam.
- Review the current exam-preparation guide on the Sun web site. Visit my web site, www.unixed.com, for late-breaking changes and up-to-date study tips from other administrators who have taken the exam.
- Memorize foundational technical detail, but remember that you need to be able to think your way through questions as well.
- Take any of the available practice tests. I recommend the ones included in this book and the ones you can create using the ExamGear software on the CD-ROM. The test engine on this CD is designed to complement the material in this book and help you prepare for the real exam. For more sample test questions, you can visit my web site, www.unixed.com. I'll try to keep the questions up-to-date and relevant. In addition, you can share your experiences with other Solaris administrators who are preparing for the exam, just like you. In addition, this web site will provide up-to-date links to the official Sun certification web sites.

## During the Exam Session

The following generic exam-taking advice that you have heard for years applies when taking this exam:

- Take a deep breath, and try to relax when you first sit down for your exam session. It is important to control the pressure you might (naturally) feel when taking exams.
- You will be provided with scratch paper. Take a moment to write down any factual information and technical detail that you committed to short-term memory.
- Carefully read all information and instruction screens. These displays have been put together to give you information relevant to the exam you are taking.
- Read the exam questions carefully. Reread each question to identify all relevant details.
- Tackle the questions in the order they are presented. Skipping around will not build your confidence; the clock is always counting down.
- Do not rush, but also do not linger on difficult questions. The questions vary in degree of difficulty. Don’t let yourself be flustered by a particularly difficult or verbose question.
- Note the time allotted and the number of questions appearing on the exam you are taking. Make a rough calculation of how many minutes you can spend on each question, and use this to pace yourself through the exam.
- Take advantage of the fact that you can return to and review skipped or previously answered questions. Record the questions you cannot answer confidently, noting the relative difficulty of each question, on the scratch paper provided. After you have made it to the end of the exam, return to the more difficult questions.
- If session time remains after you have completed all questions (and if you aren’t too fatigued!), review your answers. Pay particular attention to questions that seem to have a lot of detail or that involve graphics.
- As for changing your answers, the general rule of thumb here is don’t! If you read the question carefully and completely the first time and felt like you knew the right answer, you probably did. Do not second-guess yourself. If as you check your answers, one clearly stands out as incorrectly marked, then change it. If you are at all unsure, however, go with your first instinct.

If you have done your studying and follow the preceding suggestions, you should do well. Good luck!

## Practice Exam

### PRACTICE EXAM QUESTIONS

1. The kernel consists of which of the following?
A. The shell and environment variables
B. A small static core and many dynamically loadable modules
C. Boot PROM and the operating system
D. System run states 0, 1, and s

2. What are the characteristics of changing to run level s? Choose all that apply.
A. Single-user mode.
B. Shutdown state.
C. All users are logged out.
D. File systems remain mounted.

3. Which command is used to change run levels?
A. sudo
B. kill
C. init
D. run

4. Which of the following restricts the set of operations that users are allowed to perform at the OpenBoot prompt?
A. security-password
B. set-security
C. set-secure
D. security-mode

5. The bootstrap procedure consists of which of the following basic phases? Choose all that apply.
A. Load the kernel.
B. autoboot (if autoboot? is set).
C. Hardware power-up.
D. Execute Power-on self-test (POST).

6. What is the best command to find your hardware platform and current operating system release?
A. init -q
B. sysdef
C. uname -a
D. arch

7. What information will you need during the installation process? Choose all that apply.
A. IP address
B. Product code
C. Timezone
D. Root password

8. Which of the following conditions will not prevent a patch from being installed? Choose all that apply.
A. The patch being installed requires another patch that is not installed.
B. The patch is incompatible with another, already installed patch.
C. The patch was removed.
D. The patch version is not the most up-to-date version.

9. What does the pkgchk command do?
A. Displays software package information
B. Stores answers in a response file so that they can be supplied automatically during an installation
C. Determines the accuracy of a software package installation
D. Displays package parameter values
