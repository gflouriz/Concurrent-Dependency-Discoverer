# Concurrent-Dependency-Discoverer

Large-scale systems developed in C and C++ tend to include a large number of “.h” files, both of a system variety (enclosed in < >) and non-system (enclosed in “ ”). The make utility and Makefiles are a convenient way to record dependencies between source files, and to minimize the amount of work that is done when the system needs to be rebuilt.  Of course, the work will only be minimized if the Makefile exactly captures the dependencies between source and object files. 

Some systems are extremely large and it is difficult to keep the dependencies in the Makefile correct as many people concurrently make changes.  Therefore, there is a need for a program that can crawl over source files, noting any #include directives, and recurse through files specified in #include directives, and finally generate the correct dependency specifications.

#include directives for system files (enclosed in < >) are normally NOT specified in dependencies.  Therefore, this system will focus on generating dependencies between source files and non-system #include directives (enclosed in “ ”).

For very large software systems, a singly-threaded application to crawl the source files may take a very long time.  The final product should be a concurrent include file crawler in C++.

