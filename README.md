# SRP - Single Responsibility Principle
A class should have one, and only one, reason to change.
     
# OCP (Open-Closed Principle): 
A software module/class is open for extension and closed for modification
      
# LSP (Liskov's Substitution Principle)
The Liskov Substitution Principle (LSP) states that "you should be able to use any derived class instead of a parent class and have it 
behave in the same manner without modification". It ensures that a derived class does not affect the behavior of the parent class, 
in other words that a derived class must be substitutable for its base class

# ISP (Interface Segregation Principle)
Clients should not be forced to implement interfaces they don't use. Instead of one fat interface many small interfaces are preferred 
based on groups of methods, each one serving one sub module.

# DIP (Dependency Injection/Inversion)
High-level modules/classes should not depend upon low-level modules/classes. Both should depend upon abstractions. Secondly, 
abstractions should not depend upon details. Details should depend upon abstractions.
