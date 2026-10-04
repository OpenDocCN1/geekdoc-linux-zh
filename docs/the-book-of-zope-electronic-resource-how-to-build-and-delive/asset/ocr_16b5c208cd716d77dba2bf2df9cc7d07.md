# 9.1 Why Use ZClasses?

In a nutshell, ZClasses are special classes in Zope that can be used to describe your objects—such as cars, jobs, CDs—and to develop unique solutions to your tasks, such as selling cars on the Internet or creating an online job bank.
ZClasses are special because you don't need to know how to program in Python to you simply create a new product using the Product Management screen in the Control_Panel and then create the necessary ZClasses in this product. You can also export your ZClasses to other Zope installations for other users to use. ZClasses also allow you to easily reuse components from one application to another or distribute your components online.
You might use ZClasses in a company application to create objects that describe the work of individual employees, groups, or entire departments. For example, a class called Sales Staff could be used to create objects that describe the employees responsible for sales. Or you could create a ZClass Software to describe software objects as graphics applications, computer games, photo CDs, and so on, or a ZClass called Jobs to describe job advertisements.

# 9.1.1 Example ZClass Application: Bookstore

This application will allow you to manage pages and create objects to sell books. You can add and delete objects as well as change the individual specifications of an object or an entire object class using a web browser. You can also specify how the objects (the individual books, CDs, and so on) are listed: for example, by price, name, or publication date. Figures 9-1 show where 9-4 show where we will end up with our online bookstore.

| Title | Book Id | Author | Publisher | Year of Publication | Genre | Price | Delivery Time | Photo |
|---|---|---|---|---|---|---|---||}{
| The Sickness Unto Death | B09362 | Soren Kierkegaard | Penguin USA | 1989 | Philosophy | 13.95 | 3 days | No Photo Available |
| A Man in Full | B16630 | Tom Wolfe | Jonathan Cape | 1998 | Mystery | 19.99 | 5 days | No Photo Available |

Figure 9-1: Website from which users can order merchandise

# 9.2 Classes and Objects

Before you start creating your ZClasses, you need to familiarize yourself with several basic principles. As mentioned in Section 9.1, you first create a product and then add your ZClasses to it. A ZClass (like all classes) determines certain properties for objects. For example: