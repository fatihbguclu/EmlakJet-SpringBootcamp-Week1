# New Features Coming With Java 11 and 17

## Java 11 Features

### 1. Local-Variable Syntax for Lambda Parameters
JEP 323 allows var to be used to declare the formal parameters of an implicitly typed lambda expression.<br>
We can now define :
```
(var s1, var s2) => s1 + s2
```
<br>

### 2. Nested Based Access Control
Previous Java versions allowed access of private members to nested classes(nestmates), but we cannot use them with the Reflection API. Java 11 no longer uses bridge methods and provides the getNestHost(), getNestMembers(), and isNestmatOf() methods for the Reflection API.
<br><br>

### 3. New String Methods
- ```isBlank()``` => This method is used to check whether a string is blank or not. Empty strings and strings with just whitespace are considered blank.
- ```lines()``` => This method splits a string using line terminators and returns a stream.
- ```repeat()``` => This method is used to duplicate or repeat a string.
- ```strip() stripLeading() stripTrailing()``` => These methods are used to remove whitespace from the strings. They are very similar to the existing trim() method, but provide Unicode support.
<br><br>

### 4. Running Java File With Single Command
One major change is that you don’t need to compile the java source file with javac tool first. You can directly run the file with java command and it implicitly compiles.This feature comes under JEP 330.

### 5. JEP 318: Epsilon: A No-Op Garbage Collector
Unlike the JVM GC which is responsible for allocating memory and releasing it, Epsilon only allocates memory.<br>It allocates memory for the following things:

- Performance Testing
- Memory Pressure Testing
- VM interface testing
- Extremely short lived jobs
- Last-drop latency improvements
- Last-drop throughput improvements

Now Elipson is good only for test environments. It will lead to OutOfMemoryError in production and crash the applications.
The benefit of Elipson is no memory clearance overhead. Hence it’ll give an accurate test result of performance and we can no longer GC for stopping it.

### 6. JEP 328: Flight Recorder
Flight Recorder which earlier used to be a commercial add-on in Oracle JDK is now open-sourced since Oracle JDK is itself not free anymore.
JFR is a profiling tool used to gather diagnostics and profiling data from a running Java application.
Its performance overhead is negligible and that’s usually below 1%. Hence it can be used in production applications.

### 7. JEP 321: HTTP Client
Java 11 standardizes the Http CLient API.
The new API supports both HTTP/1.1 and HTTP/2. It is designed to improve the overall performance of sending requests by a client and receiving responses from the server. It also natively supports WebSockets.

### 8. JEP 329: ChaCha20 and Poly1305 Cryptographic Algorithms
Java 11 provides ChaCha20 and ChaCha20-Poly1305 cipher implementations. These algorithms will be implemented in the SunJCE provider.

### 9. JEP 315: Improve Aarch64 Intrinsics
Improve the existing string and array intrinsics, and implement new intrinsics for the java.lang.Math sin, cos, and log functions, on AArch64 processors.

### 10. JEP 335: Deprecate the Nashorn JavaScript Engine
Nashorn JavaScript script engine and APIs are deprecated thereby indicating that they will be removed in the subsequent releases.

<br>

## Java 17 Features
<hr><br>

### 1. JEP 306: Restore Always-Strict Floating-Point Semantics
This JEP is mainly for scientific applications, and it makes floating-point operations consistently strict. The default floating-point operations are strict or strictfp, both of which guarantee the same results from the floating-point calculations on every platform.

Before Java 1.2, strictfp behavior was the default one as well. However, because of hardware issues, the architects changed, and the keyword strictfp was necessary to re-enable such behavior. So, there is no need to use this keyword anymore.

### 2. JEP 356: Enhanced Pseudo-Random Number Generators
Also related to more special use cases, JEP 356 provides new interfaces and implementations for Pseudo-Random Number Generators (PRNG).

So, it's easier to use different algorithms interchangeably, and it also offers better support for stream-based programming:

### 3. JEP 382: New macOS Rendering Pipeline
This JEP implements a Java 2D internal rendering pipeline for macOS since Apple deprecated the OpenGL API (in macOS 10.14), used internally in Swing GUI. The new implementation uses the Apple Metal API, and apart from the internal engine, there were no changes to the existing APIs.

### 4. JEP 391: macOS/Arch64 Port
Apple announced a long-term plan to transition its computer line from X64 to AArch64. This JEP ports the JDK to run on AArch64 in macOS platforms.

### 5. JEP 398: Deprecate the Applet API for Removal
Although this may be sad for many Java developers who started their development career using Applet APIs, many web browsers have already removed their support for Java plugins. As the API became irrelevant, this version marked it for removal even though it has been marked as deprecated since version 9.

### 6. JEP 403: Strongly Encapsulate JDK Internals
JEP 403 represents one more step toward strongly encapsulating JDK internals since it removes the flag –illegal-access. The platform will ignore the flag, and if the flag is present, the console will issue a message informing the discontinuation of the flag.

This feature will prevent JDK users from accessing internal APIs, except for critical ones like sun.misc.Unsafe.

### 7. JEP 406: Pattern Matching for Switch
This is another step toward pattern matching by enhancing pattern matching for switch expressions and statements. It reduces the boilerplate necessary to define those expressions and improves the expressiveness of the language.

### 8. JEP 407: Remove RMI Activation
Marked for removal in version 15, this JEP removed the RMI activation API from the platform in version 17.

### 9. JEP 409: Sealed Classes
Sealed classes are part of Project Amber, and this JEP officially introduces a new feature to the language, although it was available in preview mode in the JDK versions 15 and 16.

The feature restricts which other classes or interfaces may extend or implement a sealed component. Showing another improvement related to pattern matching combined with the JEP 406 will allow a more sophisticated and cleaner inspection of the type, cast and act code pattern.

### 10. JEP 410: Remove the Experimental AOT and JIT Compiler
Introduced into JDK 9 and JDK 10, respectively, as experimental features, the Ahead-Of-Time (AOT) compilation (JEP 295) and Just-In-Time (JIT) compiler from GraalVM (JEP-317) were features with a high cost of maintenance.

On the other hand, they had no significant adoption. Because of that, this JEP removed them from the platform, but developers can still leverage them using GraalVM.

### 11. JEP 411: Deprecate the Security Manager for Removal
The security manager aimed to secure client-side Java code is yet another feature marked for removal due to not being relevant anymore.

### 12. JEP 412: Foreign Function and Memory API (Incubator)
The Foreign Function and Memory API allow Java developers to access code from outside the JVM and manage memory out of the heap. The goal is to replace the JNI API and improve the security and performance compared to the old one.
This API is another feature developed by Project Panama, and it has been evolved and predeceased by JEPs 393, 389, 383 and 370.
With this feature, we can make a call to a C library from a Java class.

### 13. JEP 414: Vector API (Second Incubator)
The Vector API deals with the SIMD (Single Instruction, Multiple Data) type of operation, meaning various sets of instructions executed in parallel. It leverages specialized CPU hardware that supports vector instructions and allows the execution of such instructions as pipelines.

As a result, the new API will enable developers to implement more efficient code, leveraging the potential of the underlying hardware.

Everyday use cases for this operation are scientific algebra linear applications, image processing, character processing, and any heavy arithmetic application or any application that needs to apply an operation for multiple independent operands.

### 14. JEP 415: Context-Specific Deserialization Filters
JEP 290, first introduced in JDK 9, enabled us to validate incoming serialized data from untrusted sources, a common source of many security issues. That validation happens at the JVM level, giving more security and robustness.

With JEP 415, applications can configure context-specific and dynamically selected deserialization filters defined at the JVM level. Each deserialization operation will invoke such filters.