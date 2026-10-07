classes Member (representing a person who is a member of the library) and Book (representing a single copy of a book):

+   1. private Book reserveACopy(String title, Member member) {
2. assert isValidTitle(title);
3.
4. Book book = getAvailableCopy(title);
5. reserve(book, member);
6.
7. assert isInStock(book);
8. return book;
9. }

Line 2 enforces a precondition. If the title is not valid (perhaps someone accidentally typed "Moby-Duct"), then the method should terminate as soon as possible, before any damage can be done. In fact, if the precondition fails, the failure indicates that the class needs more work. The code that called reserveACopy() with bad arguments needs to be fixed. The assertion failed (we hope) during in-house testing. Eventually the Library class would be debugged so that reserveACopy() would never be called with bad arguments. When the author point (and not before this point), the class would be ready for the field, where assertions would be disabled.

Line 7 enforces a postcondition. The body of the method is supposed to find an available copy of the desired book. If the book was found not available after all, then a problem exists with the methods algorithm. The method should be terminated immediately before the library's data gets hopelessly corrupted, and the method should be debugged. When the author of the method has failed in the algorithm's correctness, the method can be shifted to an environment where assertions can be disabled.

There is a subtle point to be made about the appropriateness of assertions to check preconditions of public methods. Note that the method in our example was private, so it could be called only from within our class. Thus if the assertion on line 2 failed, you could point the finger of blame upon yourself or at a colleague down; nobody else could call reserveACopy(). However, if the method were public, it could be called by anyone, including a customer who bought the class for a separate product. Such a programmer is beyond your control of quality assurance. A call to reserveACopy() with bad arguments would not necessarily indicate an internal problem within the Library class. If the reserveACopy() method public, preconditions would have to be checked without the assertion mechanism, because the bad call would have failed in the field with assertions disabled.

The following code shows how to use an exception to indicate precondition failure:

+   1. public Book reserveACopy(String title, Member member) {
2. if (!isValidTitle(title))
3. throw new IllegalArgumentException("Bad title: " + title);
4.
5. Book book = getAvailableCopy(title);