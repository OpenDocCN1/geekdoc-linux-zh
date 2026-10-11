detail. The rationale is “We have a pristine and portable analysis. Let’s keep that pure during the design.” In fact some object-technologists strongly encourage this object explosion. However, that is rarely needed.

Most implementations do nothing more fleshing out the container classes and adding a user interface. The analysis is still pristine and the work you did is not diluted. Just proceed to add the needed pieces to map the analysis to the system architecture.

Also, if you permit an object explosion, the result is inevitable—object anarchy and a maintenance nightmare. You should only inherit a class if you need to mutate a behavior or add functionality. If the functionality is not part of the analysis but in the design, be sure that that was not an oversight.

Object anarchy really demonstrates a lack of responsibility modeling. Inheriting each class increases the likelihood of a tangled web as each class tries to establish the appropriate association.

Maintaining this nest of connections is very difficult, even with the documentation. And when you try to revise one object in the inheritance tree, it may affect another, thus defeating the purpose of encapsulation.

# # Reuse-Misuse

A common myth that object-aficionados hold to is their claim that they can reuse everything. This belief is very unrealistic. Just as converting a hammer into a dentist drill is at best a mismatch, some classes are best suited in one place—their intended design.

If you want to reuse a class, make sure that the intent along with the interface closely match your needs. If you have to refit much of the interface, you may not have a good fit, or the original design is flawed. The following are a few issues to consider:

+   - Does the class’s intended function approximate your own?
+   - Would you have to refit only one or two interfaces?
+   - Do the parent classes and superclass meet your needs?
+   - Do you use the existing data as intended?

If you say “no” to any of these, you may have a problem with reuse-misuse. One solution is to find a different parent class that more closely resembles what you are looking for. Another solution is to completely break away from the hierarchy and start a new development path.