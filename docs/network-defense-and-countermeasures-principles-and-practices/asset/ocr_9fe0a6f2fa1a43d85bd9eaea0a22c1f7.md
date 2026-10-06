The Bell-LaPadula model also has a third rule that is applied to discretionary access control (DAC), called the discretionary security property. Discretionary access is defined as the policies that control access based on named users and named objects.

+   - **Discretionary security property (also called ds-property):** Each element of the set of current accesses, as well as the specific access mode (for example, read, write, or append), is included in the access matrix entry for the corresponding subject-object pair.

#  Biba Integrity Model

The Biba Integrity Model is also an older model, having been first published in 1977. This model is similar to the Bell-LaPadula model in that it uses subjects and objects; in addition, it controls modification in the same way that Bell-LaPadula controls data disclosure, the Bell-LaPadula model referred to as write up.

The Biba Integrity Model consists of three parts. The first two are very similar in wording and concept to the Bell-LaPadula model but wider applications.

+   - A subject cannot execute objects that have a lower level of integrity than the subject.
- A subject cannot modify objects that have a higher level of integrity.
- A subject may not request service from objects that have a higher level of integrity.

Essentially this last item means that a subject that has a confidential clearance cannot even request a service from any object with a secret or top secret clearance. The idea is to prevent subjects from even requesting data from objects with higher security levels.

# Clark-Wilson Model

The Clark-Wilson Model was first published in 1987. Like the Bell-LaPadula model it is a subject-object model. However, it introduces a new element, programs. In addition to considering subjects (systems accessing data) and objects (the data), it also considers subjects accessing programs. With the Clark-Wilson model there are two primary elements for achieving data integrity:

+   - Well-formed transaction
- Separation of duties

Well-formed transaction simply means users cannot manipulate or change the data without careful restrictions. This prevents transactions from inadvertently altering secure data. Separation of duties prevents authorized users from making improper modifications, thus preserving the external consistency of data.