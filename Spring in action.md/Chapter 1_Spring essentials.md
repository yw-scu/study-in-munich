2 core feature:
- inversion of controller(IoC)
- aspect_oriented programming(AOP)

the fac that we have to start the J2EE container for each batch of tests reallt slows down our development cycle.
# Spring Modules
## The core container - makes Spring a container
In this module you will find Spring's ```BeanFactory``` , the heart of any Spring-based application. A ```BeanFactory``` is an implementation of the factory pattern that applies IoC to seperate your application's configuration and  dependency specification rom the actual application code.
## Application context module - makes Spring a framework
It adds support for internatitionalization messages, application file cycle events, and validation.  
## Spring's AOP module
## Spring's web module
This module contains support for several web-oriented tasks such as transparntly handling multipart requests for file uploads and programmic binding of request parameters to your business objects.
## The Spring MVC Framework
It uses IoC(Inversion of Controller) to provide for a clean separation of controller logic from business objects. I s also allows you to declaratively bind requests parameters to your business objects.
# Understanding inversion of control
## Injecting dependencies
Applying IoC(Dependency injection), objects are given thier dependencies at creation time by some external entity that cooedinates each object in the system. That is, dependencies are injeted into objects.
## IoC in action
