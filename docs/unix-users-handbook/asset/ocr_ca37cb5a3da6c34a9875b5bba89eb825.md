# Access Control

When one class inherits from another, the members of the base class become members of the derived class. The ability to access the base class members inside the derived class is determined by the access specifier used in the inheritance declaration.

The base class can have access specifiers of public, private, or protected. If the access specifier is not included in the inheritance declaration, the default of private is used. But this is only true if the derived class is a class. A derived class may also be a structure, and in that case, the default access is public.

What are the implications of all this specification? The access specifier affects the ability of the derived class to access members of the base class.

First of all, individual members of a class can be declared as public, private, or protected. A public member of a class is accessible by the class and anything external to the class. A private member of the class is only accessible by member functions of the class. A protected class member allows access to a derived class when inherited; otherwise, it behaves like a private member of the class.

Inheritance affects the access of base class member functions, and the base class also has an access specifier associated with it. When a class is derived or inherits from a base class, a base class access specifier of public, private, or protected is chosen. The impact to the base class members can be described in a total of nine combinations of base class access and member function access.

When the inheritance of the base class is public, the access status of the inherited members is unchanged. (1.) Inherited public members are public, (2.) inherited protected members are protected, and (3.) inherited private members are private.

When the inheritance of the base class is protected, (4.) inherited public members of the base class become protected members in the derived class. (5.) The inherited protected members of the base class remain protected. (6.) The inherited private members of the base class remain private.

When the inheritance of the base class is private, (7.) inherited public and (8.) protected members of the base class become private to