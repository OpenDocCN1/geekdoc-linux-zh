
5. Take an essay exam. This happens at a testing center, like the Programmer exam. The cost was included in your fee.

6. Wait for your results. Patient. All work is assessed in detail, and sometimes there are backlogs. You'll get your results within 30 days of taking the exam.

Of course, from your point of view the most important part is developing the application. Most of the rest of this chapter is devoted to telling you about the assignment...in as much as Sun will allow us.

## The Project Assignment

The most important thing for you to know is that there are lots of ways to fail the Developer exam. One way, of course, is to submit poor work so that your total score is below the minimum passing grade. Other ways are easily avoidable, though for some reason people tragically avoid them. These can be summed up by the saying, “Must means must.” There are numerous places in the assignment that say, “You must...”. Your spec will explain if you don't exactly whatever you're told you must do, you fail. For example, you will receive specific instructions regarding the directory tree you must build, including the location and name of the directory containing your source code. If your source code isn't exactly where it is supposed to be, you'll fail. It won't matter if your application is so great that it glows in the dark, because the assessor won't run your application. Assessment of your project ends the moment any violation of any “must” is detected. So remember...must means must.

The next important thing for you to know about the assignment is that your spec comes from a large pool of documents. Sun created this pool of specs in order to ensure that collaboration likely to lower your grade. If you borrow code from someone, that code probably implements the wrong assignment. Since you are graded on how well you implement your spec, collaboration will likely have a disastrous effect on your score. Resist the temptation to use someone else's work; instead, get good enough that you can pass all on yours.

There is a common structure to all the specs in the pool. No which assignment you will consist of three:

- A GUI front end, call the "client”
- A server back end, accessing a data file that is provided to you
- Communication between the client and the server

Your finished project will look like Figure 10.1.

The client must be built from Swing components. Chapter 11, “Swing Components,” and Chapter 12, “Layout Managers,” discuss what you need to know to create your front end. Earlier in this book Chapter 9, “IO and Streams,” discussed file access, which will be the heart of your server. Your client and server will communicate via your choice of object streams RMI. You will read about object streams in Chapter 9; Chapter 13, “Networking,” explains using object streams for your network communication introduces RMI. Be aware that RMI is a huge topic, and it would take a thick book to cover it fully.

## FIGURE 10.1 The assignment

![](img/09f8389b7ae2705d1ab14be2d5e857e3_387_0.png)

In addition to all the programming you have to do, you will be required to submit API pages for your classes, created using Javadoc. Chapter 14, “Putting It All Together,” covers several miscellaneous topics, including the Javadoc tool.

Before we dive into the technical information of the next four chapters, let's look at the follow-up essay exam and the grading process.

## The Essay Exam

The follow-up essay exam requires you to do something you might not have done for a very long time: write essays. Like the assignment specs, the essay topics are selected from a pool, so you'll probably get different essay questions from the ones your colleagues get.

Did you have writing essays in high school? Do you believe that one of the benefits of graduating from high school is a lifetime of freedom from any of them? Don't panic! And if English isn't your native language, please don't worry. You won't be graded on spelling or grammar style. You don't have to worry about organization, because the essay topics are very narrow, and there won't be much information for you to organize. You can't go wrong if you keep in mind what it is that the assessors want to see in your essays.

The assessors want to see two things. First of course, they want to make sure you know the information you are being asked. Second, they want confirmation that you, walking into a testing center and showing a photo ID, are really the people who submitted a project under your name. (Remember, you follow the follow-up exam after submitting your project.) There is no way to prevent you from paying someone else to write your project, but people who do so are unlikely to be unfamiliar with the details of the project. Some of the essays ask you to briefly describe design choices that you made. For example, you know that for your client/server communication, you may choose either object streams or RMI. In the follow-up exam, you might be asked to write an essay describing which protocol you use and. Of course, the “why” part is test of your technical knowledge. The “which” is a honesty test. Nobody in their right mind could possibly implement RMI communication and then accidentally say they used object streams. Equally, nobody would use... If your answer to any “describe how your project does such-and-such” question doesn't match your actual project, automatically fail.

The essay questions don't require you to do any unreasonable memorization. For example, you won't be asked to list the names of all the custom exceptions you created. You'll only be asked to write about implementations details that would stick in your mind because you took the time to implement them. To be safe, consider reviewing your source code the day before you take the follow-up exam.

## Grading

Grading of your exam begins when you complete the essay exam. Your essays and your project submission are sent to an assessor, along with information about which project spec was assigned to you.

Your project is to be submitted as a single jar archive. The examiner begins by extracting this archive and making sure that you have provided the required files (source, class, data, and documentation) and that files are in the required directory locations within the archive. If anything is missing or in the wrong place, your project fails. As with automatic failure criterion (the are "musts means must" criteria in your project spec), if you fail, the assessor immediately stops your project. Misplaced files are the most tragic way to fail the Developer exam.

Next, the assessor reads the essays that you wrote for the follow-up exam. If your project doesn't match the description in the essays, you get a failing grade.

Now the deduction of grading begins. You are initially given a perfect score of 400 points. As the assessors find problems with your project, they deduct points according to some extensive and specific guidelines. Sun recognizes that grading the Developer exam requires assessors to make judgments about the quality of various parts of your work. Every effort has been made to make the deductions as objective.

During the deduction, the assessor executes your application, reads your source code, and inspects your Java API pages. This happens in no particular order. When's done, your score is 320 or better you pass.

We can't tell you the deductions are; Sun keeps that information proprietary. However, we can tell that the deductions fall into broad categories, which in turn have sub- and sub-categories:

**General Considerations** Covers miscellaneous factors such as readability and maintainability of your source code. These are reviewed in Chapter 14.

**Documentation** Covers your source-code comments and your Javadoc pages. You'll get some guidelines in Chapter 14.

**Object-Oriented Design** Covers your knowledge of Java's object-oriented facilities, as well as your ability to use them. The object-oriented facilities were presented in Chapter 6. You'll get some general programming suggestions in Chapter 14.

**GUI** Covers the appearance, behavior, and ease-of-use of your GUI. We look at GUIs in Chapters 10 and 11.
