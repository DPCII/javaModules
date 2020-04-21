## Java Modules

#### The Problem
Prior to Java 9, there was no way to break up the Java Runtime Environment (JRE) into
needed and un-needed groups of classes. This meant that when you shipped a Java product,
you shipped an entire JRE with it. As Java grew in size, this became a problem for many
smaller systems. The compiler also had no way to tell whether the necessary dependencies
were present until it tried to use a missing class. 

#### The Solution
After a long time in development, Java 9 introduced the Java Platform Module System (JPMS).
This systems allows you to write a program and package a Jar which only includes the
necessary modules rather than an entire JRE. It also added a compile-time check to ensure
all necessary modules are present.

#### Note
Avoid this confusion: Maven, Intellij, and Java all have a "module" concept.
They do different things. This document is referring to Java modules from the JPMS. 

#### Architecture
1. Modules are defined by a module-info.java file at each module source root. (ie
exampleModule/src/module-info.java)

2. Packages that will be needed by other modules should be exported by the module that
possesses it.

3. Modules that need a package from another module will always require in the entire
module, not just the package.

4. In multi-level modules, a module may need access to packages it does not directly import,
but is instead required by one of the modules it requires. The module system is strict,
and would not allow the module to pass through. This is where the ```require transitive```
keyword comes into play. The middle module would require transitive the module it wants
to pass through to the top level. Here's a helpful picture:
![transitive](https://i.stack.imgur.com/fbZwV.png)
[StackOverflow](https://stackoverflow.com/a/46504020/11857649)

5. ```Exports <package> to <module>```: Allows for strict exporting to only one module
or a comma separated list of modules.

6. ```uses <module>``` -> and <-```provides <module> with <service>```: 
When we create dependencies in our project, the interfaces and abstractions we
are relying on in the dependency are loaded into our project at Runtime using
a ServiceLoader. In a module system, the module-info file in an service-using
module explicitly names the service-providing module, and the service-providing
module names the requiring module and the service it provides.
[Reference](http://openjdk.java.net/projects/jigsaw/spec/sotms/#services)

#### Cheatsheet
[Link to PDF](https://www.jrebel.com/system/files/java-9-modules-cheat-sheet.pdf)