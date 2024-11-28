Definitions of Key OpenMP Concepts
1. OpenMP (Open Multi-Processing)

A programming interface for parallel computing in shared-memory environments, enabling the use of multiple threads to execute code simultaneously.
2. Thread

A lightweight execution unit within a program. Multiple threads can run concurrently, sharing global memory but having their own private stack.
3. Fork-Join Model

A parallel programming model:
Fork: A master thread creates a team of threads to execute a parallel region.
Join: Threads finish execution and merge back into a single thread (master).
4. Parallel Region

A block of code executed by multiple threads simultaneously.
Defined by the #pragma omp parallel construct.
5. SPMD (Single Program, Multiple Data)

An algorithm where the same program runs on all threads but operates on different parts of the data. Threads use their ID to determine what portion of the work they handle.
6. Race Condition

A bug where multiple threads access and update a shared variable simultaneously, causing unpredictable results.
Example: Two threads incrementing the same counter variable.
7. False Sharing

A performance issue where different threads access distinct elements of a shared array, but the elements reside on the same cache line, leading to unnecessary cache invalidation.
Solution: Use thread-local variables or padding to separate cache lines.
8. Synchronization

Mechanism to coordinate thread execution and prevent race conditions.
Example: Ensuring only one thread updates a shared variable at a time.
9. Barrier

A synchronization point where all threads must arrive before any thread can proceed.
Syntax: #pragma omp barrier
10. Critical Section

A block of code that allows only one thread to execute at a time, ensuring mutual exclusion.
Syntax:
#pragma omp critical
{
    // Code executed by one thread at a time
}
11. Atomic

A lightweight synchronization construct for simple operations (e.g., increments or updates).
Syntax:
#pragma omp atomic
shared_variable += value;
12. Shared Variable

A variable accessible by all threads in a parallel region. Declared outside the parallel block.
13. Private Variable

A variable local to each thread, ensuring no overlap or interference between threads.
Declared inside the parallel region.
14. omp_get_thread_num()

A function that returns the ID of the thread currently executing.
15. omp_get_num_threads()

A function that returns the total number of threads in a team.
16. omp_set_num_threads(n)

A function to request a specific number of threads for parallel execution.
17. False Sharing Mitigation

Padding: Adding extra unused space between elements in shared arrays to ensure each element is on a separate cache line.
18. Timing with omp_get_wtime()

A function to measure execution time by returning the wall clock time since an arbitrary point in the past.
Example:
double start = omp_get_wtime();
// Code to time
double end = omp_get_wtime();
printf("Time: %f seconds\n", end - start);
19. Nested Parallelism

A feature where threads within a parallel region can create their own threads.
Enabled by setting OMP_NESTED = TRUE.
20. Work Distribution

Static Scheduling: Threads are assigned fixed iterations of the loop in advance.
Dynamic Scheduling: Threads request work dynamically as they finish their assigned tasks.
