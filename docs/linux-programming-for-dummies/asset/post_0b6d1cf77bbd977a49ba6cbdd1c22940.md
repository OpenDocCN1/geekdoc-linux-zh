
You need to use a little common sense in deciding the number of subprograms to create for your program. If you find that you're losing track of the subprograms that you create, you're probably making too many of them (although no particular rule tells you how many subprograms are too many). If you feel that tracking subprograms is getting out of control, you probably need to consolidate some of them or devise a better planning tool to help you organize your subprograms. Probably the best planning tool is the *flowchart*, which graphically organizes your program plan.

## Creating a Program Plan by Using a Flowchart

Just the mention of creating a Linux program plan can send most new programmers off to get a bottle of aspirin. Why must computers be so complicated? I thought that I'd never figure out Microsoft Project (a tool that many programming gurus love to use in building a plan), but with a little patience, I overcame this perceived obstacle. You, too, may find creating a Linux program plan daunting at first, but it's really pretty easy.

First, you want to figure out what you need Linux to do and then break down the overall plan into individual functions. The flowchart helps you organize your program and place the subprograms to maximize efficiency.

### Divide and conquer

How do you eat an elephant? One bite at a time, of course. How then do you plan a large, complex Linux program? You break the program down into its individual functions and create a list of what you want Linux to do. (You can also chomp on the program, but you quickly find that it's rather stringy and in need of garlic.) By dividing your Linux program into logical chunks, with each performing a unique and important task, you make your overall programming task much easier.

Suppose, for example, that you want to create a Linux program with the overall objective of maintaining your telephone directory. You can further divide this overall program objective into the individual tasks that you want the program to perform, which may include some of the following:

- Logging into the program.
- Displaying a main menu that enables the user to make a selection.
- Finding a listing in the telephone directory.
- Adding a listing to the telephone directory.
- Modifying a listing in the telephone directory.
- Printing the telephone directory.

Your Linux program may have more or fewer tasks than appear in the preceding list. Most programs that work with data, however, incorporate subprograms that find data, add data, modify existing data, and print data.

### Plugging a task list into a flowchart

You need to take pencil in hand and organize your thoughts about how your program is going to work. The simplest approach is to draw a flowchart where each box in the flowchart represents a task that your program must accomplish. You must arrange each box on the flowchart in the order that you want your program to accomplish the task, and then you can draw lines connecting the boxes.

Take an example close to my heart (actually close to my stomach). I call this creation the Get a Snack program. The examples in this section describe how I organize this nightly trip. (Now if I could only get my computer to do the fetching, I'd have it made.)

A flowchart for the Get-a-Snack program, for example, may look something like the chart shown in Figure 14-1.

![](img/05279073f26be7df99b3c487360dec6a_171_0.png)

**Figure 14-1:** The Get-a-Snack program's flowchart.

To start your program flowchart, then, you first need to assemble the long list of tasks that you want your Linux program to perform. The next step is to draw a picture of your program. All you need to draw is a box for each task; then you place the name of the task inside the box, similar to what you see in Figure 14-2 — just as I’m doing with the Get-a-Snack program. (And this time, I’m starting from the very beginning.)

![](img/05279073f26be7df99b3c487360dec6a_172_0.png)

This little task doesn’t add much to your plan, but you’re just on the first step. The next step in creating a flowchart is to map out how each task relates to the other tasks. Now the process is getting a little more complicated, isn’t it?

The flowchart in Figure 14-3 shows how the Linux user progresses through your program. The user first logs in (*Login Task*), and the main menu appears (*Display Menu*). From the main menu, the user can then choose one of the four options that you provide in the program: *Find Listing*, *Add Listing*, *Modify Listing*, or *Print Listing*.

### Adding detail to a flowchart

You can further divide each task on your flowchart into more specific tasks. The task *Find Listing*, for example, requires that your program perform the following more-detailed tasks:

- Prompt the user to enter a name to find.
- Search the database for the name the user enters.
- If the search is successful, display the listing.
- If the search is unsuccessful, tell the user that it can’t find the listing.
- Return to the main menu.

Draw another flowchart that shows each of these more detailed tasks and how each task logically follows from the preceding one. Figure 14-4 shows how the *Find Listing* flowchart looks.

![](img/05279073f26be7df99b3c487360dec6a_173_0.png)

**Figure 14-3:**  
Fleshing out your flowchart.

The shape of the flowchart in Figure 14-4 is a little different than that of Figure 14-3 because the relationships among the tasks are now different.

![](img/05279073f26be7df99b3c487360dec6a_173_1.png)

**Figure 14-4:**  
Adding more functions to a flowchart.

As you become more specific about what each task (subprogram) does in your Linux program, the flowchart that depicts that task also becomes more detailed — kind of like branches sprouting from the trunk of a healthy tree.

## Arrow your flowcharts

You can dress up your drawings by placing arrows on the lines that connect tasks. The arrows show the direction of the next task. Using these arrows isn't a requirement, but they do add clarity to your drawing.

Each box in the flowchart is a task that associates with other boxes (tasks) on your flowchart by a connecting line. The line does more than just join boxes. The line shows how each box relates to another box by using an arrow at the end of the line. The task of displaying the menu, for example, comes before the user enters one of the selections from the menu. So you draw a line connecting the first box (displaying the menu) to the second box (selecting from the menu) with an arrow pointing to the second box because this task comes after the first task.

## Linking subprograms in a flowchart

As you map out more and more tasks on your Linux program flowchart, keeping track of all those subprograms may become tough. By numbering a subprogram, as shown in Figure 14-5, you can refer to another flowchart that contains more details about that subprogram.

Suppose that you're building a program that requires a user to enter a name and password into the program before using the program. So you label the first box on the flow chart *Login Task*. This label tells you generally what takes place at this portion of your program.

But what exactly does the Login Task involve? You need to know this information as you build the subprogram that handles the login task. You don't, however, have enough room in the Login Task box on your flowchart to place all these details.

Here's the solution: Number each box on your flow chart. The first box is 1; the second is 2; and you get the idea from there. If a box needs more detail, you can create a separate flowchart for that box. You have plenty of room on the second flowchart to identify all the tasks relating to that box on the previous flowchart.

Suppose that you assign a number 1 to the Login Task on the first flowchart. You then create an entirely new flowchart just for the Login Task box. The first box on the Login Task flowchart you number as 1.0, and this box contains the same text that you use on the corresponding box on the first flowchart — Login Task.
