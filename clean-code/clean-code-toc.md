---
description: 2016.08.19
---

# Clean Code TOC

The table of contents of the book [Clean Code: A Handbook of Agile Software Craftsmanship \(Robert C. Martin, 1994\)](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/2). It is a good overview of the rules recommended by the book.

### Clean Code

* There Will Be Code
* Bad Code
* The Total Cost of Owning a Mess
  * The Grand Redesign in the Sky
  * Attitude
  * The Primal Conundrum
  * The Art of Clean Code?
  * What Is Clean Code?
* Schools of Thought
* We Are Authors
* The Boy Scout Rule
* Prequel and Principles
* Conclusion
* Bibliography

### Meaningful Names

* Introduction
* Use Intention-Revealing Names
* Avoid Disinformation
* Make Meaningful Distinctions
* Use Pronounceable Names
* Use Searchable Names
* Avoid Encodings
  * Hungarian Notation
  * Member Prefixes
  * Interfaces and Implementations
* Avoid Mental Mapping
* Class Names
* Method Names
* Don’t Be Cute
* Pick One Word per Concept
* Don’t Pun
* Use Solution Domain Names
* Use Problem Domain Names
* Add Meaningful Context
* Don’t Add Gratuitous Context
* Final Words

### Functions

* Small!
  * Blocks and Indenting
* Do One Thing
  * Sections within Functions
* One Level of Abstraction per Function
  * Reading Code from Top to Bottom: The Stepdown Rule
* Switch Statements
* Use Descriptive Names
* Function Arguments
  * Common Monadic Forms
  * Flag Arguments
  * Dyadic Functions
  * Triads
  * Argument Objects
  * Argument Lists
  * Verbs and Keywords
* Have No Side Effects
  * Output Arguments
* Command Query Separation
* Prefer Exceptions to Returning Error Codes
  * Extract Try/Catch Blocks
  * Error Handling Is One Thing
  * The Error.java Dependency Magnet
* Don’t Repeat Yourself
* Structured Programming
* How Do You Write Functions Like This?
* Conclusion
* SetupTeardownIncluder
* Bibliography

### Comments

* Comments Do Not Make Up for Bad Code
* Explain Yourself in Code
* Good Comments
  * Legal Comments
  * Informative Comments
  * Explanation of Intent
  * Clarification
  * Warning of Consequences
  * TODO Comments
  * Amplification
  * Javadocs in Public APIs
* Bad Comments
  * Mumbling
  * Redundant Comments
  * Misleading Comments
  * Mandated Comments
  * Journal Comments
  * Noise Comments
  * Scary Noise
  * Don’t Use a Comment When You Can Use a
  * Function or a Variable
  * Position Markers
  * Closing Brace Comments
  * Attributions and Bylines
  * Commented-Out Code
  * HTML Comments
  * Nonlocal Information
  * Too Much Information
  * Inobvious Connection
  * Function Headers
  * Javadocs in Nonpublic Code
  * Example
* Bibliography

### Formatting

* The Purpose of Formatting
* Vertical Formatting
  * The Newspaper Metaphor
  * Vertical Openness Between Concepts
  * Vertical Density
  * Vertical Distance
  * Vertical Ordering
  * Horizontal Formatting
  * Horizontal Openness and Density
  * Horizontal Alignment
  * Indentation
  * Dummy Scopes
* Team Rules
* Uncle Bob’s Formatting Rules

### Objects and Data Structures

* Data Abstraction
* Data/Object Anti-Symmetry
* The Law of Demeter
  * Train Wrecks
  * Hybrids
  * Hiding Structure
* Data Transfer Objects
  * Active Record
* Conclusion
* Bibliography

### Error Handling

* Use Exceptions Rather Than Return Codes
* Write Your Try-Catch-Finally Statement First
* Use Unchecked Exceptions
* Provide Context with Exceptions
* Define Exception Classes in Terms of a Caller’s Needs
* Define the Normal Flow
* Don’t Return Null
* Don’t Pass Null
* Conclusion
* Bibliography

### Boundaries

* Using Third-Party Code
* Exploring and Learning Boundaries
* Learning log4j
* Learning Tests Are Better Than Free
* Using Code That Does Not Yet Exist
* Clean Boundaries
* Bibliography

### Unit Tests

* The Three Laws of TDD
* Keeping Tests Clean
  * Tests Enable the -ilities
* Clean Tests
  * Domain-Specific Testing Language
  * A Dual Standard
* One Assert per Test
  * Single Concept per Test
* F.I.R.S.T
* Conclusion
* Bibliography

### Classes

* Class Organization
  * Encapsulation
* Classes Should Be Small!
  * The Single Responsibility Principle
  * Cohesion
  * Maintaining Cohesion Results in Many Small Classes
* Organizing for Change
  * Isolating from Change
* Bibliography

### Systems

* How Would You Build a City?
* Separate Constructing a System from Using It
  * Separation of Main
  * Factories
  * Dependency Injection
* Scaling Up
  * Cross-Cutting Concerns
* Java Proxies
* Pure Java AOP Frameworks
* AspectJ Aspects
* Test Drive the System Architecture
* Optimize Decision Making
* Use Standards Wisely, When They Add DemonstrableValue
* Systems Need Domain-Specific Languages
* Conclusion
* Bibliography

### Emergence

* Getting Clean via Emergent Design
* Simple Design Rule 1: Runs All the Tests
* Simple Design Rules 2–4: Refactoring
* No Duplication
* Expressive
* Minimal Classes and Methods
* Conclusion
* Bibliography

### Concurrency

* Why Concurrency?
* Myths and Misconceptions
* Challenges
* Concurrency Defense Principles
  * Single Responsibility Principle
  * Corollary: Limit the Scope of Data
  * Corollary: Use Copies of Data
  * Corollary: Threads Should Be as Independent as Possible
* Know Your Library
  * Thread-Safe Collections
* Know Your Execution Models
  * Producer-Consumer
  * Readers-Writers
  * Dining Philosophers
* Beware Dependencies Between Synchronized Methods
* Keep Synchronized Sections Small
* Writing Correct Shut-Down Code Is Hard
* Testing Threaded Code
  * Treat Spurious Failures as Candidate Threading Issues
  * Get Your Nonthreaded Code Working First
  * Make Your Threaded Code Pluggable
  * Make Your Threaded Code Tunable
  * Run with More Threads Than Processors
  * Run on Different Platforms
  * Instrument Your Code to Try and Force Failures
  * Hand-Coded
  * Automated
* Conclusion
* Bibliography

### Successive Refinement

* Args Implementation
  * How Did I Do This?
* Args: The Rough Draft
  * So I Stopped
  * On Incrementalism
* String Arguments
* Conclusion

### JUnit Internals

* The JUnit Framework
* Conclusion

### Refactoring SerialDate

* First, Make It Work
* Then Make It Right
* Conclusion
* Bibliography

### Smells and Heuristics

* Comments
  * Inappropriate Information
  * Obsolete Comment
  * Redundant Comment
  * Poorly Written Comment
  * Commented-Out Code
* Environment
  * Build Requires More Than One Step
  * Tests Require More Than One Step
* Functions
  * Too Many Arguments
  * Output Arguments
  * Flag Arguments
  * Dead Function
* General
  * Multiple Languages in One Source File
  * Obvious Behavior Is Unimplemented
  * Incorrect Behavior at the Boundaries
  * Overridden Safeties
  * Duplication
  * Code at Wrong Level of Abstraction
  * Base Classes Depending on Their Derivatives
  * Too Much Information
  * Dead Code
  * Vertical Separation
  * Inconsistency
  * Clutter
  * Artificial Coupling
  * Feature Envy
  * Selector Arguments
  * Obscured Intent
  * Misplaced Responsibility
  * Inappropriate Static
  * Use Explanatory Variables
  * Function Names Should Say What They Do
  * Understand the Algorithm
  * Make Logical Dependencies Physical
  * Prefer Polymorphism to If/Else or Switch/Case
  * Follow Standard Conventions
  * Replace Magic Numbers with Named Constants
  * Be Precise
  * Structure over Convention
  * Encapsulate Conditionals
  * Avoid Negative Conditionals
  * Functions Should Do One Thing
  * Hidden Temporal Couplings
  * Don’t Be Arbitrary
  * Encapsulate Boundary Conditions
  * Functions Should Descend Only One Level of Abstraction
  * Keep Configurable Data at High Levels
  * Avoid Transitive Navigation
* Java
  * Avoid Long Import Lists by Using Wildcards
  * Don’t Inherit Constants
  * Constants versus Enums
* Names
  * Choose Descriptive Names
  * Choose Names at the Appropriate Level of Abstraction
  * Use Standard Nomenclature Where Possible
  * Unambiguous Names
  * Use Long Names for Long Scopes
  * Avoid Encodings
  * Names Should Describe Side-Effects.
* Tests
  * Insufficient Tests
  * Use a Coverage Tool!
  * Don’t Skip Trivial Tests
  * An Ignored Test Is a Question about an Ambiguity
  * Test Boundary Conditions
  * Exhaustively Test Near Bugs
  * Patterns of Failure Are Revealing
  * Test Coverage Patterns Can Be Revealing
  * Tests Should Be Fast
* Conclusion
* Bibliography

### Appendix A: Concurrency II

* Client/Server Example
  * The Server
  * Adding Threading
  * Server Observations
  * Conclusion
* Possible Paths of Execution
  * Number of Paths
  * Digging Deeper
  * Conclusion
* Knowing Your Library
  * Executor Framework
  * Nonblocking Solutions
  * Nonthread-Safe Classes
* Dependencies Between Methods
* Can Break Concurrent Code
  * Tolerate the Failure
  * Client-Based Locking
  * Server-Based Locking
* Increasing Throughput
  * Single-Thread Calculation of Throughput
  * Multithread Calculation of Throughput
* Deadlock
  * Mutual Exclusion
  * Lock & Wait
  * No Preemption
  * Circular Wait
  * Breaking Mutual Exclusion
  * Breaking Lock & Wait
  * Breaking Preemption
  * Breaking Circular Wait
* Testing Multithreaded Code
* Tool Support for Testing Thread-Based Code
* Conclusion
* Tutorial: Full Code Examples
  * Client/Server Nonthreaded
  * Client/Server Using Threads

### Appendix B: org.jfree.date.SerialDate

### Appendix C: Cross References of Heuristics

### Epilogue

