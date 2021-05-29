JNA build helper

This software can help to compile and shared native libraries so that they can
be used with the Java Native Access (JNA) library in Apache Maven projects.

To use from a Maven module:

1. Declare the parent of the module in pom.xml as follows:
	<parent>
		<groupId>com.github.liveontologies</groupId>
		<artifactId>jna-build-helper</artifactId>
		<version>...</version>
	</parent>

2. Put all files necessary to compile the native library to the project folder:

   src/main/native
   
   The root of this folder should contain a file "makefile". Issuing command
   "make" from this folder, should create a shared library for the target
   platform (e.g., libXXX.so, libXXX.dylib, or XXX.dll) in the root of this
   folder.
   
If done this way, then "mvn install" should compile the shared library, put it
in a folder corresponding the JNA prefix {OS}-{ARCH} (e.g., linux-x86-64, or
darwin, or win32-x86) defined by JNA (see
https://github.com/java-native-access/jna/blob/master/www/GettingStarted.md) and
packages it in a jar file. This jar file can be used from other Maven project
using a dependency with <groupId>, <artifiactId>, and <version> as defined for
this module and <qualifier>[prefix]<\qualifier>, where [prefix] is the JNA 
prefix for the corresponding platform (see above).