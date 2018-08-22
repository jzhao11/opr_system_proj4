# Build Instructions:
make
By using the original Makefile (with gcc command included) in the repo, the instruction "make" (under the repo csc415-p4-jzhao11) can build the program and generate the executable file "threadracer".


# Run Instructions:
./threadracer
This instruction is also executed under csc415-p4-jzhao11, which runs the executable file "threadracer".


# Explanation for Race Condition:
By inserting nanosleep() into the thread code, we are inducing race conditions, which leads to interleaved order of execution and non-zero value as the final result.

Among ~30 times of threadracer running, the final value of the shared global variable is non-zero in most cases and ranges from -69 to 19. Such output is due to the fact that multiple threads are trying to access the same shared variable (g_variable). Specifically, each thread iteratively reads g_variable into tmp, and adds to (or subtracts from) tmp, and then writes it back to g_variable. However, the existence of nanosleep() will force inappropriate interleaved execution of threads, during which the g_variable in one thread may have already been changed by other threads. As a result, an unpredictable non-zero value will be printed at last, with a trace of output listed in detail. And how far it goes away from 0 depends on the actual execution sequence of thread code.
