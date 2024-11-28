# OpenMP Learning Repository

This repository contains my notes and learning materials from my OpenMP course. OpenMP (Open Multi-Processing) is a powerful programming interface for parallel computing in shared-memory environments.

## Table of Contents

1. [Introduction to OpenMP](#introduction-to-openmp)
2. [Core Concepts](#core-concepts)
3. [Key Constructs](#key-constructs)
4. [Data Environment](#data-environment)
5. [Synchronization](#synchronization)
6. [Common Issues and Solutions](#common-issues-and-solutions)
7. [Performance Tips](#performance-tips)
8. [Code Examples](#code-examples)

## Introduction to OpenMP

OpenMP is a multi-threaded programming model designed for shared memory systems. It enables parallel programming through a set of compiler directives, library routines, and environment variables.

### Key Features
- Thread-based parallelism
- Shared memory architecture
- Fork-Join execution model
- SPMD (Single Program, Multiple Data) pattern

## Core Concepts

### Fork-Join Model
- Program starts with a single master thread
- Additional threads fork at parallel regions
- All threads join back at the end of parallel regions

### Thread Management
- `omp_get_thread_num()`: Get current thread ID
- `omp_get_num_threads()`: Get total number of threads
- `omp_set_num_threads(n)`: Set number of threads

## Key Constructs

### Parallel Construct
```c
#pragma omp parallel
{
    int ID = omp_get_thread_num();
    printf("Hello from thread %d\n", ID);
}
```

## Data Environment

### Variable Scoping
- **Private Variables**: Local to each thread (declared inside parallel block)
- **Shared Variables**: Accessible by all threads (declared outside parallel block)

## Synchronization

### Available Constructs

1. **Barrier**
```c
#pragma omp barrier
```

2. **Critical Section**
```c
#pragma omp critical
{
    // Code executed by one thread at a time
}
```

3. **Atomic Operations**
```c
#pragma omp atomic
shared_variable += value;
```

## Common Issues and Solutions

### False Sharing
- **Problem**: Multiple threads writing to different elements on the same cache line
- **Solutions**:
  - Use thread-local variables
  - Implement array padding
  - Minimize use of shared arrays

### Critical Section Performance
- Keep critical sections outside loops when possible
- Use atomic operations for simple updates
- Minimize synchronization overhead

## Performance Tips

1. Minimize synchronization
2. Use local variables when possible
3. Be mindful of data sharing patterns
4. Choose appropriate synchronization constructs
5. Monitor and measure performance using `omp_get_wtime()`

## Code Examples

### Pi Calculation Example
```c
// Serial Version
for (i = 0; i < num_steps; i++) {
    x = (i + 0.5) * step;
    sum += 4.0 / (1.0 + x * x);
}
pi = sum * step;

// Parallel Version with Atomic
#pragma omp parallel
{
    double sum = 0.0;
    for (int i = id; i < num_steps; i += nthrds) {
        double x = (i + 0.5) * step;
        sum += 4.0 / (1.0 + x * x);
    }
    #pragma omp atomic
    pi += sum * step;
}
```

### Performance Measurement
```c
double start = omp_get_wtime();
// Parallel code here
double end = omp_get_wtime();
printf("Elapsed time: %f seconds\n", end - start);
```

## Additional Resources

- OpenMP Official Documentation
- Course Materials (to be added)
- Example Programs (to be added)

---

**Note**: This repository is actively maintained as I progress through my OpenMP course. Contributions and suggestions are welcome!
