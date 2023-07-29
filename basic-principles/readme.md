# Basic Principles

* Code reuse
    - functions
    - classes
    - libraries
    - frameworks
    - microservices
* Extensibility
    - Accomodate changes
* Encapsulate changing behaviour
    - extract out changing stuff and make changes there rather than changing the whole thing
* Depend upon Abstractions/Interfaces rather than Implementations
    - a class should depend upon Interface/Abstract class rather than actual class object

* Inheritance is great, but Composition is even better
    - Idea is to reuse code between classes
    - Inheritance helps but has caveats
        + it represents "is a/an" relationship (car is a vehicle)
        + implement all abstract methods of superclass even if not needed
        + override methods carefully
            - assume you're passing subclass object to a function that expects superclass object. It shouldn't break
        + breaks encapsulation
            - subclass knows internal details of superclass
            - superclass may know details of subclass when we try to extend the superclass to make it compatible with new subclass
        + subclasses are tightly coupled to superclass
            - whenever making change in superclass, need to check whether subclasses are now compatible
        + multiple inheritance can create issues (diamond problem)
    - Composition is better
        + it represents "has a/an" relationship (car has an engine)
        + create various parts (rather than subclasses) of the entity and make entity use them

# SOLID Principles

* Single Responsibility
    - Class should have just one reason to change
    - make every class responsible for a single part of the functionality provided by the software, and make that responsibility entirely encapsulated/hidden by the class
* Open/Closed
    - Class should be open for extension, but closed for modification
    - Keep existing code from breaking when you implement new features
    - A class that is already developed -> tested -> reviewed -> included in framework -> used in an app should not be changed. Instead create a subclass and override parts that need to behave differently
* Liskov Substitution
    - When extending a class, one should be able to pass objects of the subclass in place of objects of the parent class without breaking the client code
    - When overriding a method, extend the base behavior rather than replacing it with something entirely different
    - Principles to ensure this
        + Parameters of a subclass method should match/be supertypes of the parameter types of superclass method
        + Return type of a subclass method should match/be subtype of the return type of superclass method
        + Subclass method shouldn't throw exceptions which are not expected to be thrown by Superclass method
        + Subclass shouldn't strengthen pre-conditions (superclass method with generic int argument, subclass method with +ve int argument is bad)
        + Sublclass shouldn't weaken post-conditions (superclass method returns only +ve int, subclass method can return all int is bad)
        + Preserve superclass invariants (try not to mess with superclass members, introduce new fields and methods - not always possible though)
        + Subclass shouldn't change private fields of superclass (Python allows that, Java has reflection to allow that)
* Interface Segregation
    - Don't force client classes (that depend on server class interface) to depend on methods they don't use
    - Break down "fat" interfaces into "lean" ones (classes can inherit only from single class in Java, but they can inherit from multiple interfaces due to this reason)
* Dependency Inversion
    - Details/Low Level Classes should depend on abstractions/High Level Classes rather than reverse
    - Low Level Classes - working with db/network etc
    - High Level Classes - business logic that directs Low Level Classes to do work
    - Idea: generally we write logic to connect to db first, fetchTableRow and updateTableRow generic methods. Then business logic is added to rely on these methods. We need to reverse this approach.
    - Process to follow -
        + describe interfaces for low-level operations (add updateEntity method, rather than series of fetchTableRow and updateTableRow methods)
        + make business logic use those interfaces (bussiness logic should call udpateEntity rather than calling fetchTableRow and updateTableRow methods)
        + implement low-level interfaces now, so that they're dependent on business logic, hence, leading to dependency inversion