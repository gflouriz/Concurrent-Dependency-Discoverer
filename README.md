# Concurrent-Dependency-Discoverer

Large-scale systems developed in C and C++ tend to include a large number of “.h” files, both of a system variety (enclosed in < >) and non-system (enclosed in “ ”). The make utility and Makefiles are a convenient way to record dependencies between source files, and to minimize the amount of work that is done when the system needs to be rebuilt.  Of course, the work will only be minimized if the Makefile exactly captures the dependencies between source and object files. 

Some systems are extremely large and it is difficult to keep the dependencies in the Makefile correct as many people concurrently make changes.  Therefore, there is a need for a program that can crawl over source files, noting any #include directives, and recurse through files specified in #include directives, and finally generate the correct dependency specifications.

#include directives for system files (enclosed in < >) are normally NOT specified in dependencies.  Therefore, this system will focus on generating dependencies between source files and non-system #include directives (enclosed in “ ”).

For very large software systems, a singly-threaded application to crawl the source files may take a very long time.  The final program is a concurrent include file crawler in C++.

The key data structures, data flows, and threads in the concurrent version are shown in the figure below. This is a common master/worker concurrency pattern. The main thread (master) places file names to be processed in the work queue. Worker threads select a file name from the work queue, scan the file to discover dependencies, add these dependencies to the result Hash Map and, if new to the work queue.

It is possible to adjust the number of worker threads to process the accumulated work queue in order to speed up the processing.  Since the Work Queue and the Hash Map are shared between threads, concurrency control mechanisms were used to implement thread safe access.

