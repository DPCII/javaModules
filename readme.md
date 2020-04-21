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
They are different things. This document is referring to Java modules from the JPMS. 

#### Architecture
Modules are defined by a module-info.java file at the module root. 