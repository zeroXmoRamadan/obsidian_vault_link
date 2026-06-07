> **Course**: Introduction to Parallel Programming (Peter Pacheco)
> **Chapters Covered**: 1, 2, 3, 5
> **Optimized for**: Final exam preparation — last-minute cramming & comprehensive coverage

---

# 📋 Table of Contents

1. [Chapter 1 — Why Parallel Computing](#chapter-1--why-parallel-computing)
2. [Chapter 2 — Parallel Hardware and Parallel Software](#chapter-2--parallel-hardware-and-parallel-software)
3. [Chapter 3 — Distributed Memory Programming with MPI](#chapter-3--distributed-memory-programming-with-mpi)
4. [Chapter 5 — Shared Memory Programming with OpenMP](#chapter-5--shared-memory-programming-with-openmp)
5. [High-Yield Revision Sheet](#-high-yield-revision-sheet)
6. [Likely Exam Questions & Answers](#-likely-exam-questions--answers)

---

# Chapter 1 — Why Parallel Computing

## 📝 Summary

This chapter motivates the need for parallel computing. Due to physical limits (heat, power consumption, transistor size approaching atomic scales), single-core performance improvements have stalled. The solution is **multicore processors**. However, serial programs do **not** automatically benefit from multiple cores — programmers must explicitly write parallel programs. The chapter introduces key concepts: **task parallelism vs. data parallelism**, **coordination** (communication, load balancing, synchronization), and the three main parallel programming extensions: **MPI, Pthreads, and OpenMP**.

## 🔑 Key Definitions

| Term                      | Definition                                                                               |
| ------------------------- | ---------------------------------------------------------------------------------------- |
| **Concurrent computing**  | A program in which multiple tasks can be **in progress** at any instant                  |
| **Parallel computing**    | A program in which multiple tasks **cooperate closely** to solve a problem               |
| **Distributed computing** | A program that may need to **cooperate with other programs** to solve a problem          |
| **Core**                  | A central processing unit (CPU) on a chip                                                |
| **Data parallelism**      | Partitioning the **data** among cores; each core performs similar operations on its part |
| **Task parallelism**      | Partitioning the **tasks** (different operations) among cores                            |
| **Communication**         | Cores send/receive partial results to/from other cores                                   |
| **Load balancing**        | Distributing work evenly so no single core is overloaded                                 |
| **Synchronization**       | Ensuring cores don't get too far ahead of others                                         |

## 💡 Important Concepts

### Why Parallel Computing?
- **1986–2002**: Microprocessor performance increased ~**50% per year**
- **After 2002**: Dropped to ~**20% per year**
- **Solution**: Put multiple processors on a single chip (multicore)

### Moore's Law
- Gordon Moore (1965): Transistor density on a chip **doubles roughly every 2 years**
- It's about **number of transistors**, NOT performance
- Held true for **40+ years**
- Current technology: **3 nanometers** (approaching atomic scales — Si-Si bond is ~0.5nm)

### The Power/Heat Problem
- **Smaller transistors → faster processors → more power → more heat → unreliable processors**
- This chain of consequences is why we moved to multicore

### Global Sum Example ⚡ LIKELY EXAM TOPIC
- **Naive approach**: Master core receives from all p-1 cores and adds → **(p-1) receives and additions**
- **Tree-structured approach**: Pair cores, each pair sums, repeat → **log₂(p) receives and additions**
- **Example**: 8 cores → Naive: 7 ops, Tree: 3 ops; 1000 cores → Naive: 999 ops, Tree: 10 ops

### Parallel Programming Extensions
| Extension | Memory Model | Type |
|-----------|-------------|------|
| **MPI** (Message-Passing Interface) | Distributed memory | Library |
| **Pthreads** (POSIX Threads) | Shared memory | Library |
| **OpenMP** (Open Multi-Processing) | Shared memory | Compiler directives + library |

### Shared vs. Distributed Memory
- **Shared memory**: All cores access the same memory; coordinate via shared data structures
- **Distributed memory**: Each core has private memory; cores communicate via explicit messages over a network

## ⚠️ Common Mistakes & Tricky Points
- **Don't confuse concurrent with parallel**: Concurrent = tasks in progress at same time (may interleave on 1 core); Parallel = tasks actively execute simultaneously
- Serial programs do **NOT** automatically benefit from more cores
- Automatic parallelization from serial code has had **limited success**
- Sometimes the best parallel solution requires designing a **completely new algorithm** (not just parallelizing the serial one)

---

# Chapter 2 — Parallel Hardware and Parallel Software

## 📝 Summary

This chapter covers the foundational hardware and software concepts for parallel computing. It begins with the **von Neumann architecture**, then discusses key performance optimizations: **caching** (locality, mappings, write policies), **virtual memory**, and **instruction-level parallelism (ILP)**. It introduces **Flynn's Taxonomy** (SISD, SIMD, MISD, MIMD), the two major MIMD architectures (**shared memory** with UMA/NUMA and **distributed memory** with clusters), and parallel software concepts including **threads, processes, nondeterminism, race conditions, mutual exclusion**. The chapter concludes with critical **performance metrics** (speedup, efficiency, scalability) and **Foster's methodology** for designing parallel programs.

## 🔑 Key Definitions

| Term | Definition |
|------|-----------|
| **Von Neumann Architecture** | CPU (Control Unit + ALU) + Main Memory, connected by a Bus |
| **Register** | Very fast storage, part of the CPU |
| **Program Counter** | Stores address of the next instruction to execute |
| **Bus** | Wires and hardware connecting CPU and memory |
| **Process** | An instance of a computer program being executed (includes: executable, memory block, OS-allocated resources, state info) |
| **Thread** | Lightweight sub-unit of a process; threads within a process share memory |
| **Multitasking** | Illusion of running multiple programs simultaneously via time slicing |
| **Forking** | Starting/creating a new thread |
| **Joining** | Terminating/waiting for a thread to finish |
| **Cache** | Collection of memory locations that can be accessed faster than main memory; located on or near the CPU chip |
| **Spatial locality** | Accessing a nearby memory location after the current one |
| **Temporal locality** | Accessing the same memory location again in the near future |
| **Cache hit** | Requested data is found in cache |
| **Cache miss** | Requested data is NOT in cache; must fetch from lower level |
| **Virtual memory** | Uses main memory as a cache for secondary storage (disk) |
| **Page** | Block of data/instructions in virtual memory (typically 4–16 KB) |
| **Swap space** | Secondary storage area for idle pages |
| **Page table** | Maps virtual page numbers to physical addresses |
| **ILP** | Instruction-Level Parallelism — multiple processor components executing instructions simultaneously |
| **Latency** | Time from source beginning transmission to destination starting to receive first byte |
| **Bandwidth** | Rate at which destination receives data after first byte arrives |
| **Race condition** | When the outcome of a computation depends on the unpredictable timing/ordering of threads |
| **Critical section** | Code that can only be executed by one thread at a time |
| **Mutex (lock)** | Mutual exclusion lock — ensures only one thread enters a critical section |
| **SPMD** | Single-Program Multiple-Data — one program, branching controls different behavior per process |
| **Nondeterminism** | Different runs may produce different output orderings |

## 💡 Important Concepts

### Cache Write Policies
| Policy | Behavior |
|--------|----------|
| **Write-through** | Updates main memory **immediately** when cache is written |
| **Write-back** | Marks cache line as **dirty**; writes to memory only when line is **evicted** |

### Cache Mappings ⚡ LIKELY EXAM TOPIC
| Mapping | Description |
|---------|-------------|
| **Fully associative** | A new cache line can go **anywhere** in cache |
| **Direct mapped** | Each memory line maps to exactly **one specific** cache location |
| **n-way set associative** | Each memory line can map to one of **n** locations |

### ILP — Multiple Issue
- **Static multiple issue**: Functional units scheduled at **compile time**
- **Dynamic multiple issue**: Functional units scheduled at **run-time**

### Flynn's Taxonomy ⚡ HIGHLY LIKELY EXAM TOPIC

| Type | Instruction Streams | Data Streams | Description |
|------|-------------------|--------------|-------------|
| **SISD** | Single | Single | Traditional serial computer |
| **SIMD** | Single | Multiple | Same instruction on multiple data (GPUs, vector processors) |
| **MISD** | Multiple | Single | Rarely used in practice |
| **MIMD** | Multiple | Multiple | Most common parallel architecture today |

### SIMD Details
- One control unit, multiple ALUs
- All ALUs execute the **same instruction** or remain **idle**
- Efficient for **large data-parallel** problems
- **Drawback**: Not suitable for complex/irregular parallel problems
- If more data items than ALUs → divide work iteratively in rounds

### GPUs
- Use SIMD parallelism (but not purely SIMD)
- Graphics pipeline converts geometry → pixels
- Shader functions are implicitly parallel

### MIMD Architectures ⚡ LIKELY EXAM TOPIC

#### Shared Memory Systems
- Collection of autonomous processors connected to memory via interconnection network
- Each processor can access **each memory location**
- Communicate **implicitly** via shared data structures

| Sub-type | Description |
|----------|-------------|
| **UMA** (Uniform Memory Access) | All cores access all memory at the **same speed** |
| **NUMA** (Non-Uniform Memory Access) | Directly connected memory is **faster** than memory through another chip |

#### Distributed Memory Systems
- **Clusters**: Collection of commodity systems connected by a network
- Each node is an individual computation unit
- Also called **hybrid systems**

### Message Transmission Time Formula ⚡ EXAM FORMULA

$$\text{Message time} = l + \frac{n}{b}$$

Where:
- **l** = latency (seconds)
- **n** = message length (bytes)
- **b** = bandwidth (bytes/second)

### Parallel Software Concepts

#### Shared Memory Programs
- Start a single process, **fork threads**
- Threads carry out tasks
- **Dynamic threads**: Created/terminated as needed (efficient resources, slow creation)
- **Static threads**: Pool created at start, don't terminate until cleanup (better performance, potential resource waste)

#### Distributed Memory Programs
- Start **multiple processes**
- Processes carry out tasks

#### Nondeterminism & Race Conditions
```c
// UNSAFE - Race condition!
my_val = Compute_val(my_rank);
x += my_val;  // Multiple threads writing to x simultaneously

// SAFE - With mutex
my_val = Compute_val(my_rank);
Lock(&add_my_val_lock);
x += my_val;
Unlock(&add_my_val_lock);
```

#### Busy-Waiting Pattern
```c
my_val = Compute_val(my_rank);
if (my_rank == 1)
    while (!ok_for_1);     /* Busy-wait loop */
x += my_val;              /* Critical section */
if (my_rank == 0)
    ok_for_1 = true;      /* Let thread 1 proceed */
```

#### Message-Passing Pattern
```c
char message[100];
my_rank = Get_rank();
if (my_rank == 1) {
    sprintf(message, "Greetings from process 1");
    Send(message, MSG_CHAR, 100, 0);
} else if (my_rank == 0) {
    Receive(message, MSG_CHAR, 100, 1);
    printf("Process 0 > Received: %s\n", message);
}
```

### Performance Metrics ⚡ CRITICAL EXAM TOPIC

#### Speedup
$$S = \frac{T_{serial}}{T_{parallel}}$$

- Ideal (linear) speedup: **S = p** (where p = number of cores)

#### Efficiency
$$E = \frac{S}{p} = \frac{T_{serial}}{p \cdot T_{parallel}}$$

- Ideal efficiency: **E = 1** (or 100%)

#### Scalability ⚡ LIKELY EXAM TOPIC
| Type | Definition |
|------|-----------|
| **Strongly scalable** | Efficiency stays constant as p increases **without** increasing problem size |
| **Weakly scalable** | Efficiency stays constant if problem size increases **at the same rate** as p |

### Timing Functions
| Context | Function |
|---------|----------|
| MPI | `MPI_Wtime()` |
| OpenMP | `omp_get_wtime()` |

### Foster's Methodology ⚡ LIKELY EXAM TOPIC

| Step | Name | Description |
|------|------|-------------|
| 1 | **Partitioning** | Divide computation and data into small tasks that can execute in parallel |
| 2 | **Communication** | Determine what communication is needed between tasks |
| 3 | **Aggregation** | Combine tasks and communications into larger composite tasks (e.g., aggregate dependent tasks) |
| 4 | **Mapping** | Assign composite tasks to processes/threads; minimize communication, balance load |

### I/O Rules
- **stdin**: Only process 0 (MPI) or master thread (OpenMP) can access
- **stdout/stderr**: All processes/threads can access (but usually only one does for determinism)
- **Files**: Each process/thread should access only its own private files

## ⚠️ Common Mistakes & Tricky Points
- **UMA vs NUMA**: In UMA all memory accesses are equal speed; in NUMA local memory is faster
- **Speedup cannot exceed p** in normal circumstances (superlinear speedup is rare and usually due to cache effects)
- **Efficiency decreases** as p increases for fixed problem size (overhead grows)
- **Larger problem sizes** generally give better speedup/efficiency
- **Write-through vs Write-back**: Write-through is simpler but slower; write-back is faster but more complex
- Fully associative is most flexible but most expensive; direct mapped is simplest but has most conflicts
- **PGAS** (Partitioned Global Address Space) languages allow shared variables with private index ranges

---

# Chapter 3 — Distributed Memory Programming with MPI

## 📝 Summary

This chapter covers **MPI (Message-Passing Interface)** programming for distributed memory systems. It covers: the basic MPI program structure (`MPI_Init`, `MPI_Finalize`, communicators), **point-to-point communication** (`MPI_Send`, `MPI_Recv`), the **Trapezoidal Rule** as a parallel example, **collective communication** operations (`MPI_Reduce`, `MPI_Allreduce`, `MPI_Bcast`, `MPI_Scatter`, `MPI_Gather`, `MPI_Allgather`), **MPI derived datatypes**, performance evaluation with `MPI_Wtime` and `MPI_Barrier`, **parallel sorting** (odd-even transposition sort), and **safety** issues (buffering, deadlock, `MPI_Ssend`, `MPI_Sendrecv`).

## 🔑 Key Definitions

| Term | Definition |
|------|-----------|
| **MPI** | Message-Passing Interface — a library of functions callable from C/C++/Fortran |
| **Communicator** | A collection of processes that can send messages to each other |
| **MPI_COMM_WORLD** | Default communicator containing all processes |
| **Rank** | A nonnegative integer identifying a process (0 to p-1) |
| **SPMD** | Single-Program Multiple-Data — all processes run the same program, branch by rank |
| **Point-to-point communication** | Communication between exactly two processes (sender and receiver) |
| **Collective communication** | Communication involving ALL processes in a communicator |
| **Tag** | Integer label used to match sends with receives in point-to-point communication |
| **Blocking** | A function call that doesn't return until the operation completes |
| **Buffering** | MPI copies the message to an internal buffer, allowing Send to return before the matching Recv |
| **Deadlock** | Each process is blocked waiting for an event that will never happen |
| **Unsafe program** | A program whose correctness depends on MPI-provided buffering |
| **Derived datatype** | Custom MPI type representing a collection of data items with different types and memory locations |

## 💡 Important Concepts

### MPI Program Structure ⚡ LIKELY EXAM TOPIC

#### Compilation & Execution
```bash
# Compilation
mpicc -g -Wall -o mpi_hello mpi_hello.c

# Execution
mpiexec -n <number_of_processes> <executable>
mpiexec -n 4 ./mpi_hello
```

#### Basic Outline
```c
#include <mpi.h>

int main(int argc, char* argv[]) {
    MPI_Init(&argc, &argv);
    
    int my_rank, comm_sz;
    MPI_Comm_rank(MPI_COMM_WORLD, &my_rank);  // My rank
    MPI_Comm_size(MPI_COMM_WORLD, &comm_sz);  // Total processes
    
    // ... parallel work ...
    
    MPI_Finalize();
    return 0;
}
```

### Key MPI Functions

| Function | Purpose |
|----------|---------|
| `MPI_Init(&argc, &argv)` | Initialize MPI |
| `MPI_Finalize()` | Clean up MPI |
| `MPI_Comm_rank(comm, &rank)` | Get process rank |
| `MPI_Comm_size(comm, &size)` | Get number of processes |
| `MPI_Send(buf, count, type, dest, tag, comm)` | Send a message |
| `MPI_Recv(buf, count, type, src, tag, comm, &status)` | Receive a message |
| `MPI_Reduce(sendbuf, recvbuf, count, type, op, dest, comm)` | Reduce to one process |
| `MPI_Allreduce(sendbuf, recvbuf, count, type, op, comm)` | Reduce to ALL processes |
| `MPI_Bcast(buf, count, type, root, comm)` | Broadcast from one to all |
| `MPI_Scatter(sendbuf, sendcount, sendtype, recvbuf, recvcount, recvtype, root, comm)` | Distribute data from one to all |
| `MPI_Gather(sendbuf, sendcount, sendtype, recvbuf, recvcount, recvtype, root, comm)` | Collect data from all to one |
| `MPI_Allgather(sendbuf, sendcount, sendtype, recvbuf, recvcount, recvtype, comm)` | Gather data to ALL processes |
| `MPI_Barrier(comm)` | Synchronize all processes |
| `MPI_Wtime()` | Get wall clock time |
| `MPI_Ssend(...)` | Synchronous send (guaranteed to block until matching recv starts) |
| `MPI_Sendrecv(...)` | Combined send and receive (prevents deadlock) |
| `MPI_Get_count(&status, type, &count)` | Get count of received data |

### MPI_Send / MPI_Recv Details ⚡ LIKELY EXAM TOPIC

#### MPI_Send
```c
int MPI_Send(
    void*         msg_buf_p,    // pointer to message
    int           msg_size,     // number of elements
    MPI_Datatype  msg_type,     // type of elements
    int           dest,         // destination rank
    int           tag,          // message tag
    MPI_Comm      communicator  // communicator
);
```

#### MPI_Recv
```c
int MPI_Recv(
    void*         msg_buf_p,    // pointer to receive buffer
    int           buf_size,     // max number of elements
    MPI_Datatype  msg_type,     // type of elements
    int           source,       // source rank (or MPI_ANY_SOURCE)
    int           tag,          // message tag (or MPI_ANY_TAG)
    MPI_Comm      communicator, // communicator
    MPI_Status*   status_p      // status info
);
```

#### Message Matching Rules
- `MPI_Send` with `dest = r` matches `MPI_Recv` with `source = q` (where q sent to r)
- Receiver **can use wildcards**: `MPI_ANY_SOURCE`, `MPI_ANY_TAG`
- Sender **cannot use wildcards**
- `MPI_Recv` **always blocks** until a matching message is received
- `MPI_Send` may buffer (small messages) or block (large messages) — **implementation-dependent**

#### MPI_Status Fields
- `status.MPI_SOURCE` — rank of sender
- `status.MPI_TAG` — tag of message
- `status.MPI_ERROR` — error code

### MPI Data Types
| MPI Type | C Type |
|----------|--------|
| `MPI_CHAR` | `char` |
| `MPI_INT` | `int` |
| `MPI_FLOAT` | `float` |
| `MPI_DOUBLE` | `double` |
| `MPI_LONG` | `long` |
| `MPI_UNSIGNED` | `unsigned int` |

### Collective Communication ⚡ CRITICAL EXAM TOPIC

#### Tree-Structured Global Sum
- Phase 1: Pairs of processes sum (1→0, 3→2, 5→4, 7→6)
- Phase 2: Even-ranked processes sum with partner (2→0, 6→4)
- Phase 3: Final sum (4→0)
- Total phases: **log₂(p)**

#### MPI_Reduce
```c
MPI_Reduce(&local_val, &global_val, 1, MPI_DOUBLE, MPI_SUM, 0, MPI_COMM_WORLD);
```

#### Predefined Reduction Operators
| Operator | Meaning |
|----------|---------|
| `MPI_SUM` | Sum |
| `MPI_PROD` | Product |
| `MPI_MAX` | Maximum |
| `MPI_MIN` | Minimum |
| `MPI_LAND` | Logical AND |
| `MPI_LOR` | Logical OR |
| `MPI_BAND` | Bitwise AND |
| `MPI_BOR` | Bitwise OR |
| `MPI_MAXLOC` | Max and location |
| `MPI_MINLOC` | Min and location |

#### Collective Communication Rules ⚡ TRICKY EXAM POINT
1. **ALL** processes in the communicator **must call** the same collective function
2. Arguments must be **"compatible"** (e.g., same dest_process in MPI_Reduce)
3. **No tags** in collective communication — matching is by **communicator + call order**
4. `output_data_p` is only used on the destination process, but **all processes must pass an argument** (even NULL)
5. MPI_Reduce calls are matched by **order of invocation**, NOT by variable names

#### MPI_Reduce Matching Example ⚡ TRICKY
```
Process 0:  MPI_Reduce(&a, &b, ..., 0, ...);   // a=1
            MPI_Reduce(&c, &d, ..., 0, ...);   // c=2
Process 1:  MPI_Reduce(&a, &b, ..., 0, ...);   // a=2
            MPI_Reduce(&c, &d, ..., 0, ...);   // c=1
Process 2:  MPI_Reduce(&a, &b, ..., 0, ...);   // a=1
            MPI_Reduce(&c, &d, ..., 0, ...);   // c=2
```
Result: **b = 1+2+1 = 4, d = 2+1+2 = 5** (matched by ORDER, not variable name)

#### MPI_Allreduce
- Like MPI_Reduce but the result is stored on **ALL** processes
- Implementations: (1) Reduce then Broadcast, or (2) **Butterfly structure** (more efficient)

#### MPI_Bcast
```c
MPI_Bcast(&data, count, datatype, root, communicator);
```
- Data from `root` process is sent to **all** processes
- Uses tree-structured broadcast internally

#### Data Distribution / Partitioning ⚡ LIKELY EXAM TOPIC
| Type | Description | Example (12 elements, 3 processes) |
|------|-------------|-----------------------------------|
| **Block** | Consecutive chunks | P0:[0-3], P1:[4-7], P2:[8-11] |
| **Cyclic** | Round-robin | P0:[0,3,6,9], P1:[1,4,7,10], P2:[2,5,8,11] |
| **Block-cyclic** | Cyclic distribution of blocks | Depends on block size |

#### MPI_Scatter & MPI_Gather
- `MPI_Scatter`: Root process distributes equal-sized chunks to all processes
- `MPI_Gather`: Root process collects equal-sized chunks from all processes
- `MPI_Allgather`: Every process gets all data from all processes (like Gather + Bcast)

### MPI Derived Datatypes
```c
int MPI_Type_create_struct(
    int count,                     // number of elements
    int array_of_blocklengths[],   // length of each block
    MPI_Aint array_of_displacements[], // displacement of each block
    MPI_Datatype array_of_types[], // type of each block
    MPI_Datatype* new_type_p       // output: new datatype
);

MPI_Get_address(&variable, &address);  // Get memory address
MPI_Type_commit(&new_type);            // Commit the type
MPI_Type_free(&new_type);              // Free the type
```

### The Trapezoidal Rule in MPI

**Parallel approach using Foster's methodology:**
1. **Partition**: Each trapezoid computation is an independent task
2. **Communication**: Each task sends its area to a collecting task
3. **Aggregation**: Assign contiguous blocks of trapezoids to each process
4. **Mapping**: One process per core

**Parallel pseudocode:**
- Each process computes its local integral over its subinterval
- Process 0 collects all partial results (via Send/Recv or MPI_Reduce)

### Performance Evaluation ⚡ EXAM TOPIC

#### Timing
```c
double start = MPI_Wtime();
// ... computation ...
double end = MPI_Wtime();
double elapsed = end - start;
```

#### MPI_Barrier
```c
MPI_Barrier(MPI_COMM_WORLD);  // All processes wait until everyone reaches this point
```
- Used to synchronize before timing measurements

### Parallel Sorting: Odd-Even Transposition Sort ⚡ LIKELY EXAM TOPIC

#### Algorithm
- A sequence of **n phases** (for n elements)
- **Even phases**: Compare-swap elements at positions (0,1), (2,3), (4,5), ...
- **Odd phases**: Compare-swap elements at positions (1,2), (3,4), (5,6), ...

#### Example
```
Start:        5, 9, 4, 3
Even phase:   compare-swap (5,9) and (4,3) → 5, 9, 3, 4
Odd phase:    compare-swap (9,3)           → 5, 3, 9, 4
Even phase:   compare-swap (5,3) and (9,4) → 3, 5, 4, 9
Odd phase:    compare-swap (5,4)           → 3, 4, 5, 9  ✓
```

#### Parallel Version
- **n keys, p processes**, each gets **n/p keys**
- Each process sorts its local keys first
- In each phase, processes exchange data with partner and keep appropriate half
- Partner in **even phase**: even-ranked processes partner with rank+1
- Partner in **odd phase**: odd-ranked processes partner with rank+1

### MPI Safety ⚡ CRITICAL EXAM TOPIC

#### The Problem
- `MPI_Send` may **buffer** (copy to internal buffer, return immediately) OR **block** (wait for matching Recv)
- Small messages → typically buffered
- Large messages → typically blocked
- **Threshold is implementation-dependent**

#### Deadlock Scenario
```c
// DEADLOCK if both Sends block!
// Process 0:          Process 1:
MPI_Send(to 1);       MPI_Send(to 0);    // Both block!
MPI_Recv(from 1);     MPI_Recv(from 0);  // Never reached!
```

#### Solutions

1. **MPI_Ssend** (Synchronous Send)
   - **Guaranteed to block** until matching Recv starts
   - Use to test if your program is safe

2. **Restructure communication** (alternate Send/Recv order)
   ```c
   // Process 0:         Process 1:
   MPI_Send(to 1);      MPI_Recv(from 0);
   MPI_Recv(from 1);    MPI_Send(to 0);
   ```

3. **MPI_Sendrecv**
   - Combined blocking send and receive in a single call
   - MPI handles scheduling to prevent deadlock
   - `dest` and `source` can be the same or different
   ```c
   MPI_Sendrecv(sendbuf, sendcount, sendtype, dest, sendtag,
                recvbuf, recvcount, recvtype, source, recvtag,
                comm, &status);
   ```

#### Safety Definition
- A program is **unsafe** if its correct behavior depends on MPI buffering the send data
- An unsafe program may work for some inputs but **hang/crash for others**

## 🔢 Important Formulas

| Formula | Meaning |
|---------|---------|
| `S = T_serial / T_parallel` | Speedup |
| `E = S / p = T_serial / (p × T_parallel)` | Efficiency |
| `Message time = l + n/b` | Transmission time |
| Tree global sum phases = `log₂(p)` | Number of communication rounds |

## ⚠️ Common Mistakes & Tricky Points
- **MPI_Recv always blocks**, but MPI_Send behavior is implementation-dependent
- Collective operations must be called by **ALL** processes — mixing MPI_Reduce with MPI_Recv will crash/hang
- MPI_Reduce matching is by **call order**, NOT variable names
- Only process 0 can access **stdin**; all can access stdout but usually only one should for determinism
- A program relying on MPI buffering is **unsafe**, even if it works in testing
- In MPI_Scatter/Gather, `sendcount`/`recvcount` is the count **per process**, not total
- `MPI_Barrier` is used for synchronization, especially before timing

---

# Chapter 5 — Shared Memory Programming with OpenMP

## 📝 Summary

This chapter covers **OpenMP** for shared-memory parallel programming. OpenMP uses **compiler directives (pragmas)** and library functions to parallelize programs with minimal source code changes. Key topics: the `#pragma omp parallel` directive, the **fork-join model**, **variable scope** (shared vs. private), **critical sections** and mutual exclusion (critical, atomic, locks), the **reduction clause**, the **parallel for directive** (with caveats about data dependencies), **loop scheduling** (static, dynamic, guided, runtime), the **producer-consumer pattern** with message queues, and **thread safety**.

## 🔑 Key Definitions

| Term | Definition |
|------|-----------|
| **OpenMP** | An API for shared-memory parallel programming (MP = multiprocessing) |
| **Pragma** | Special preprocessor instruction; compilers that don't support it ignore it |
| **Team** | Collection of threads executing a parallel block (master + slaves) |
| **Master thread** | The original thread that starts the parallel region |
| **Slave threads** | Additional threads created for the parallel region |
| **Fork** | Creating new threads for a parallel region |
| **Join** | Threads finishing and merging back to master |
| **Shared scope** | Variable accessible by ALL threads in the team |
| **Private scope** | Variable accessible by only ONE thread |
| **Reduction variable** | A variable where all intermediate results of a reduction operation are stored |
| **Reduction operator** | A binary operation (e.g., +, *, -, &, \|, ^, &&, \|\|) |
| **Critical section** | Code block where only one thread can execute at a time |
| **Atomic directive** | Lightweight protection for single load-modify-store operations |
| **Lock** | Explicit data structure + functions for mutual exclusion |
| **Schedule clause** | Controls how loop iterations are distributed among threads |
| **Data dependency** | When one iteration's result depends on another iteration's result |
| **Thread-safe** | Code that can be called simultaneously by multiple threads without errors |

## 💡 Important Concepts

### OpenMP Compilation & Execution
```bash
# Compilation
gcc -g -Wall -fopenmp -o omp_hello omp_hello.c

# Execution (4 threads)
./omp_hello 4
```

### Basic Parallel Directive ⚡ LIKELY EXAM TOPIC
```c
#pragma omp parallel num_threads(thread_count)
{
    // This block is executed by thread_count threads
    int my_rank = omp_get_thread_num();      // 0 to thread_count-1
    int num_threads = omp_get_num_threads();
}
```

### Key OpenMP Functions
| Function | Purpose |
|----------|---------|
| `omp_get_thread_num()` | Get current thread's rank (0-based) |
| `omp_get_num_threads()` | Get total number of threads in team |
| `omp_get_wtime()` | Get wall clock time |

### Compiler Compatibility Guard
```c
#ifdef _OPENMP
    #include <omp.h>
    int my_rank = omp_get_thread_num();
    int thread_count = omp_get_num_threads();
#else
    int my_rank = 0;
    int thread_count = 1;
#endif
```

### Variable Scope ⚡ CRITICAL EXAM TOPIC

- **Default**: Variables declared **before** a parallel block have **shared** scope
- Variables declared **inside** a parallel block have **private** scope
- Use `private(var)`, `shared(var)` clauses to override
- Use `default(none)` to force explicit specification of ALL variable scopes

```c
// With default(none) - must explicitly declare scope for every variable
#pragma omp parallel for default(none) \
    private(i, factor) shared(n, sum) reduction(+:sum)
```

### Critical Section ⚡ LIKELY EXAM TOPIC
```c
// Only one thread at a time can execute the critical section
#pragma omp critical
    global_result += my_result;
```

### The Trapezoidal Rule with OpenMP
```c
global_result = 0.0;
#pragma omp parallel num_threads(thread_count)
{
    double my_result = Local_trap(a, b, n);  // Each thread computes partial sum
    
    #pragma omp critical
        global_result += my_result;  // Safely add to global result
}
```

**Key insight**: Compute locally first, then enter critical section only for the final addition — avoids making the critical section a bottleneck.

### The Reduction Clause ⚡ CRITICAL EXAM TOPIC

Instead of manually managing critical sections:
```c
// BAD - forces sequential execution
#pragma omp parallel for num_threads(thread_count)
for (i = 0; i < n; i++) {
    #pragma omp critical
        global_result += f(i);  // Critical section inside loop = serial!
}

// GOOD - using reduction clause
#pragma omp parallel for num_threads(thread_count) \
    reduction(+: global_result)
for (i = 0; i < n; i++)
    global_result += f(i);  // Each thread has private copy, combined at end
```

**Available reduction operators**: `+`, `*`, `-`, `&`, `|`, `^`, `&&`, `||`

### The Parallel For Directive ⚡ CRITICAL EXAM TOPIC

```c
#pragma omp parallel for num_threads(thread_count) \
    reduction(+: approx)
for (i = 0; i < n; i++)
    approx += f(x_i);
```

#### Legal For Loop Forms
- Loop variable must be **integer or pointer type** (NOT float)
- `start`, `end`, `incr` must have compatible types
- `start`, `end`, `incr` **must not change** during loop execution
- Loop variable can **only be modified** by the increment expression

### Data Dependencies ⚡ CRITICAL EXAM TOPIC — TRICKY

```c
// CANNOT be parallelized — data dependency!
fibo[0] = fibo[1] = 1;
#pragma omp parallel for num_threads(2)
for (i = 2; i < n; i++)
    fibo[i] = fibo[i-1] + fibo[i-2];  // Depends on previous iterations!
```

**Result with 2 threads**:
- Correct:   `1 1 2 3 5 8 13 21 34 55`
- Sometimes: `1 1 2 3 5 8 0 0 0 0` ← Thread 1 may read uninitialized values!

> [!CAUTION]
> **OpenMP does NOT check for data dependencies!** The programmer is responsible for ensuring loop iterations are independent.

### Estimating π Example
```c
// Version with loop dependency (WRONG):
factor = 1.0;
sum = 0.0;
#pragma omp parallel for num_threads(thread_count) \
    reduction(+: sum)
for (i = 0; i < n; i++) {
    sum += factor / (2*i + 1);
    factor = -factor;    // DATA DEPENDENCY — factor depends on previous iteration!
}

// Correct version (factor made private):
sum = 0.0;
#pragma omp parallel for num_threads(thread_count) \
    reduction(+: sum) private(factor)
for (i = 0; i < n; i++) {
    if (i % 2 == 0) factor = 1.0; else factor = -1.0;
    sum += factor / (2*i + 1);
}
```

### Loop Scheduling ⚡ LIKELY EXAM TOPIC

```c
#pragma omp parallel for schedule(type, chunksize)
```

| Type | Description | When to Use |
|------|-------------|-------------|
| **static** | Iterations assigned **before** loop executes; default: block partition; with chunksize: cyclic-like | Iterations have **uniform** workload |
| **dynamic** | Each thread gets a chunk; when done, requests another; default chunksize=1 | Iterations have **varying** workload |
| **guided** | Like dynamic but chunk size **decreases** over time | Large loops with **decreasing** per-iteration cost |
| **auto** | Compiler/runtime decides | When unsure |
| **runtime** | Determined by `OMP_SCHEDULE` environment variable | Testing different schedules without recompiling |

#### Static Schedule Examples (12 iterations, 3 threads)

| Schedule | Thread 0 | Thread 1 | Thread 2 |
|----------|----------|----------|----------|
| `static` (default block) | 0,1,2,3 | 4,5,6,7 | 8,9,10,11 |
| `static,1` (cyclic) | 0,3,6,9 | 1,4,7,10 | 2,5,8,11 |
| `static,2` | 0,1,6,7 | 2,3,8,9 | 4,5,10,11 |

#### Performance Impact Example
- `f(i)` takes time proportional to `i`
- n=10,000; 1 thread: 3.67s
- 2 threads, default (block): 2.76s, **speedup=1.33** (unbalanced!)
- 2 threads, cyclic: 1.84s, **speedup=1.99** (nearly perfect!)

### Sorting with OpenMP: Odd-Even Transposition Sort

```c
for (phase = 0; phase < n; phase++) {
    if (phase % 2 == 0) {
        #pragma omp parallel for num_threads(thread_count) \
            default(none) shared(a, n) private(i, tmp)
        for (i = 1; i < n; i += 2)
            if (a[i-1] > a[i]) { tmp = a[i]; a[i] = a[i-1]; a[i-1] = tmp; }
    } else {
        #pragma omp parallel for num_threads(thread_count) \
            default(none) shared(a, n) private(i, tmp)
        for (i = 1; i < n-1; i += 2)
            if (a[i] > a[i+1]) { tmp = a[i+1]; a[i+1] = a[i]; a[i] = tmp; }
    }
}
```

### Mutual Exclusion Mechanisms ⚡ LIKELY EXAM TOPIC

| Mechanism | Syntax | Use Case |
|-----------|--------|----------|
| **critical** | `#pragma omp critical` | General critical sections |
| **named critical** | `#pragma omp critical(name)` | Different named sections can run in parallel |
| **atomic** | `#pragma omp atomic` | Single load-modify-store statement only |
| **locks** | `omp_set_lock(&lock)` / `omp_unset_lock(&lock)` | Fine-grained, programmatic control |

#### Atomic Directive
```c
#pragma omp atomic
x += expr;  // Only single C assignment with: +, *, -, &, |, ^, ++, --
```
- More efficient than critical (uses hardware atomic instructions)
- **Cannot protect** multi-statement critical sections

#### Lock Functions
```c
omp_lock_t lock;
omp_init_lock(&lock);     // Initialize
omp_set_lock(&lock);      // Acquire (blocking)
omp_unset_lock(&lock);    // Release
omp_destroy_lock(&lock);  // Destroy
```

### Producer-Consumer Pattern with Message Queues
- Each thread has its own message queue (shared array of queues)
- Producer enqueues messages to destination thread's queue
- Consumer dequeues messages from its own queue
- Must use locks (not named critical sections) because each queue needs independent protection
- Need explicit **barrier** after queue allocation to ensure all queues exist before sending

### OpenMP Barrier
```c
#pragma omp barrier
// All threads wait here until every thread reaches this point
```

### Caveats for Mutual Exclusion ⚡ TRICKY
1. **Don't mix** different mutual exclusion types for the same critical section
2. **No fairness guarantee** — a thread may starve
3. **Don't nest** mutual exclusion constructs (potential deadlock)

## ⚠️ Common Mistakes & Tricky Points

- Putting `#pragma omp critical` **inside** a parallel for loop effectively makes it **sequential** — always compute locally first, then use critical section
- Variables declared **before** a parallel block default to **shared** — this is a common source of bugs
- `#pragma omp parallel for` is NOT the same as `#pragma omp parallel` + `#pragma omp for` (though they can be combined)
- **Data dependencies between loop iterations** will produce wrong results — OpenMP does NOT check!
- The Fibonacci example produces wrong results because thread 1's iterations depend on thread 0's results
- `default(none)` is a best practice — forces you to think about every variable's scope
- `atomic` can only protect **single** load-modify-store statements, NOT multi-line blocks
- Block scheduling with non-uniform workloads leads to **load imbalance** → use cyclic or dynamic
- `num_threads` is a **request**, not guaranteed (system may give fewer)

---

# 🏆 High-Yield Revision Sheet

> **This section contains the absolute minimum you need to know. If you're short on time, focus here.**

## The Big Picture
- **Why parallel?** → Physical limits (heat/power) → multicore CPUs → must write parallel programs
- **Moore's Law**: Transistor count doubles ~every 2 years (NOT performance)
- **3 programming models**: MPI (distributed), OpenMP (shared), Pthreads (shared)

## Must-Know Formulas

| Formula | What |
|---------|------|
| **S = T_serial / T_parallel** | Speedup |
| **E = S / p** | Efficiency |
| **Message time = l + n/b** | Network transmission |
| **Tree-sum rounds = log₂(p)** | Communication phases |

## Flynn's Taxonomy
**SISD** (serial) → **SIMD** (data parallel, GPUs) → **MIMD** (most common: shared or distributed memory)

## UMA vs NUMA
- **UMA**: All memory same speed
- **NUMA**: Local memory faster

## Strong vs Weak Scalability
- **Strong**: Constant efficiency, fixed problem size
- **Weak**: Constant efficiency, growing problem size proportional to p

## Foster's Methodology
**Partition → Communication → Aggregation → Mapping**

## MPI Essentials
```c
MPI_Init / MPI_Finalize / MPI_Comm_rank / MPI_Comm_size
MPI_Send / MPI_Recv            // Point-to-point
MPI_Reduce / MPI_Allreduce     // Collective reduction
MPI_Bcast                      // One-to-all
MPI_Scatter / MPI_Gather       // Data distribution/collection
MPI_Barrier / MPI_Wtime        // Sync & timing
MPI_Sendrecv                   // Safe combined send+receive
```

**Safety rule**: Never rely on MPI_Send buffering → use MPI_Sendrecv or restructure communication

## OpenMP Essentials
```c
#pragma omp parallel num_threads(N)           // Fork N threads
#pragma omp parallel for reduction(+: var)    // Parallelize loop with reduction
#pragma omp critical                          // Mutual exclusion
#pragma omp atomic                            // Single-statement protection
#pragma omp barrier                           // Synchronize threads
```

**Scope**: Shared by default (before block), Private if declared inside block.
**Schedule types**: `static` (uniform work), `dynamic` (varying work), `guided` (decreasing chunks)

## Collective Communication Rules
1. ALL processes must call the same collective function
2. No tags — matched by order of calls
3. MPI_Reduce matching is by call ORDER, not variable names

## Top 5 Pitfalls
1. **Race conditions** in shared memory → use critical/atomic/locks
2. **Data dependencies** in parallel for → check before parallelizing
3. **Deadlock** in MPI → don't have all processes Send before Recv
4. **Unsafe MPI** → don't rely on buffering
5. **Load imbalance** → use appropriate scheduling

---

# 📝 Likely Exam Questions & Answers

## Question 1: Definitions
**Q: Define concurrent computing, parallel computing, and distributed computing. What is the key difference between them?**

**A:**
- **Concurrent computing**: Multiple tasks can be **in progress** at any instant (may time-share one CPU)
- **Parallel computing**: Multiple tasks **cooperate closely** to solve a single problem (execute simultaneously)
- **Distributed computing**: Multiple programs may need to **cooperate** to solve a problem (possibly across a network)

Key difference: Concurrent doesn't require simultaneous execution; Parallel requires simultaneous execution to solve one problem; Distributed may involve separate programs across different machines.

---

## Question 2: Flynn's Taxonomy
**Q: Explain Flynn's Taxonomy. Which category do modern multicore processors fall into?**

**A:** Flynn's Taxonomy classifies computer architectures by instruction and data streams:
- **SISD**: Single instruction, single data (traditional serial)
- **SIMD**: Single instruction, multiple data (GPUs, vector processors)
- **MISD**: Multiple instructions, single data (rarely used)
- **MIMD**: Multiple instructions, multiple data

Modern multicore processors are **MIMD** — each core has its own control unit and ALU, executing different instructions on different data independently.

---

## Question 3: Speedup & Efficiency Calculation
**Q: A serial program runs in 120 seconds. The parallel version with 8 processors runs in 20 seconds. Calculate the speedup and efficiency.**

**A:**
- Speedup: S = T_serial / T_parallel = 120 / 20 = **6**
- Efficiency: E = S / p = 6 / 8 = **0.75 (or 75%)**

---

## Question 4: Tree-Structured Global Sum
**Q: Given 16 processes, how many communication phases does a tree-structured global sum require? How many receives does the master perform in the naive approach vs. the tree approach?**

**A:**
- Tree approach: **log₂(16) = 4 phases**, master performs **4 receives**
- Naive approach: Master performs **15 receives** (p-1)
- Improvement factor: 15/4 ≈ **3.75×** better

---

## Question 5: Cache Concepts
**Q: Explain spatial locality and temporal locality. Give an example of each.**

**A:**
- **Spatial locality**: If you access address X, you're likely to soon access nearby addresses. *Example*: Iterating through an array — `a[0], a[1], a[2], ...`
- **Temporal locality**: If you access address X, you're likely to access it again soon. *Example*: A loop counter variable that is read/updated every iteration.

---

## Question 6: UMA vs NUMA
**Q: What is the difference between UMA and NUMA shared memory systems?**

**A:**
- **UMA (Uniform Memory Access)**: All cores access all memory locations at the **same speed**. Time to access any memory location is the same regardless of which core makes the request.
- **NUMA (Non-Uniform Memory Access)**: Memory directly connected to a core is accessed **faster** than memory connected through another chip. Access time depends on the distance between the core and the memory.

---

## Question 7: MPI Safety & Deadlock
**Q: Explain why the following code might deadlock. How would you fix it?**
```c
// Process 0:              Process 1:
MPI_Send(to 1);            MPI_Send(to 0);
MPI_Recv(from 1);          MPI_Recv(from 0);
```

**A:** If both `MPI_Send` calls block (waiting for the matching `MPI_Recv`), neither process reaches its `MPI_Recv`, causing **deadlock** — each process waits for an event that never happens.

**Three fixes:**
1. **Reorder**: Have one process Send first, other Recv first:
   ```c
   // Process 0:           Process 1:
   MPI_Send(to 1);         MPI_Recv(from 0);
   MPI_Recv(from 1);       MPI_Send(to 0);
   ```
2. **Use MPI_Sendrecv**: Combines send and receive in one safe call.
3. **Use non-blocking operations** (MPI_Isend/MPI_Irecv).

---

## Question 8: MPI Collective Communication
**Q: What is the difference between MPI_Reduce and MPI_Allreduce?**

**A:**
- **MPI_Reduce**: Performs a reduction operation and stores the result on a **single designated process** (dest_process).
- **MPI_Allreduce**: Performs the same reduction but stores the result on **ALL processes**.

MPI_Allreduce can be implemented as MPI_Reduce followed by MPI_Bcast, or more efficiently using a **butterfly** structure.

---

## Question 9: OpenMP Data Dependencies
**Q: Why can't the following loop be parallelized with `#pragma omp parallel for`?**
```c
for (i = 2; i < n; i++)
    fibo[i] = fibo[i-1] + fibo[i-2];
```

**A:** There is a **data dependency** between iterations: `fibo[i]` depends on `fibo[i-1]` and `fibo[i-2]`, which are computed in previous iterations. If iterations run on different threads simultaneously, a thread may try to read values that haven't been computed yet. OpenMP **does not check** for data dependencies — the programmer is responsible. The result would be nondeterministic (likely incorrect).

---

## Question 10: OpenMP Reduction
**Q: Write OpenMP code to compute the sum of an array of n doubles using a reduction clause.**

**A:**
```c
double sum = 0.0;
#pragma omp parallel for num_threads(thread_count) \
    reduction(+: sum)
for (int i = 0; i < n; i++)
    sum += a[i];
```
Each thread maintains a **private copy** of `sum`, computes its partial sum, and they are all combined with the `+` operator at the end of the parallel region.

---

## Question 11: Scheduling
**Q: If loop iterations have increasing workload (iteration i takes time proportional to i), which OpenMP schedule should you use and why?**

**A:** Use **`schedule(static,1)`** (cyclic) or **`schedule(dynamic)`**.

With the **default block** schedule, the last thread gets all the expensive iterations and becomes a bottleneck. **Cyclic** distributes iterations round-robin (0→T0, 1→T1, 2→T0, 3→T1...) so each thread gets a mix of cheap and expensive iterations, achieving near-perfect load balance.

Example: n=10000, 2 threads — block schedule gives speedup=1.33, cyclic gives speedup=1.99.

---

## Question 12: Foster's Methodology
**Q: List and explain the four steps of Foster's methodology for designing parallel programs.**

**A:**
1. **Partitioning**: Divide the computation and data into small, independent tasks. Focus on identifying tasks that can execute in parallel.
2. **Communication**: Determine what data needs to be communicated between the tasks identified in step 1.
3. **Aggregation**: Combine small tasks and their communications into larger composite tasks. For example, dependent tasks should be aggregated together.
4. **Mapping**: Assign composite tasks to processes/threads, minimizing communication while balancing the workload evenly across processes.

---

## Question 13: Strong vs Weak Scalability
**Q: Define strong scalability and weak scalability. Give an example scenario for each.**

**A:**
- **Strong scalability**: Efficiency remains constant as p increases **without** increasing problem size. Example: A matrix multiplication that maintains 80% efficiency going from 4 to 64 cores on the same 1000×1000 matrix.
- **Weak scalability**: Efficiency remains constant when problem size grows **at the same rate** as p. Example: Going from 4 cores with a 1000×1000 matrix to 16 cores with a 2000×2000 matrix while maintaining 80% efficiency.

---

## Question 14: MPI_Scatter vs MPI_Bcast
**Q: What is the difference between MPI_Scatter and MPI_Bcast?**

**A:**
- **MPI_Bcast**: Sends the **same complete data** from root to all processes. Every process gets an identical copy.
- **MPI_Scatter**: Divides the data on root into **equal chunks** and sends a **different chunk** to each process. Each process gets only its portion.

---

## Question 15: OpenMP Mutex Mechanisms
**Q: Compare and contrast `#pragma omp critical`, `#pragma omp atomic`, and OpenMP locks.**

**A:**
| Feature | critical | atomic | locks |
|---------|----------|--------|-------|
| **Protects** | Any block of code | Single load-modify-store statement | Any block of code |
| **Granularity** | Coarse | Fine (hardware instruction) | Fine |
| **Performance** | Slower | Fastest | Medium |
| **Named variants** | Yes (`critical(name)`) | No | Each lock is independent |
| **Flexibility** | Medium | Lowest | Highest |

**Caveat**: Never mix these mechanisms for the same critical section. Don't nest them (deadlock risk). No fairness guarantee.

---

## Question 16: Message Transmission Time
**Q: Calculate the time to send a 10,000-byte message if the latency is 50 microseconds and the bandwidth is 100 MB/s.**

**A:**
- Message time = l + n/b
- l = 50 μs = 50 × 10⁻⁶ s
- n = 10,000 bytes
- b = 100 MB/s = 100 × 10⁶ bytes/s
- **Time = 50×10⁻⁶ + 10,000 / (100×10⁶) = 50×10⁻⁶ + 100×10⁻⁶ = 150 μs**

---

## Question 17: Write-Through vs Write-Back Cache
**Q: Explain write-through and write-back cache policies. What is the advantage of each?**

**A:**
- **Write-through**: When CPU writes to cache, main memory is updated **immediately**. *Advantage*: Memory always consistent with cache. *Disadvantage*: Slower (every write hits memory).
- **Write-back**: Written cache line is marked **dirty**. Memory is updated only when the dirty line is **evicted**. *Advantage*: Faster (fewer memory writes). *Disadvantage*: Memory may be stale; more complex.

---

## Question 18: Odd-Even Transposition Sort
**Q: Sort the list [7, 3, 5, 1] using odd-even transposition sort. Show each phase.**

**A:**
```
Start:       7, 3, 5, 1

Even phase:  compare-swap (7,3) and (5,1) → 3, 7, 1, 5
Odd phase:   compare-swap (7,1)           → 3, 1, 7, 5
Even phase:  compare-swap (3,1) and (7,5) → 1, 3, 5, 7
Odd phase:   compare-swap (3,5)           → 1, 3, 5, 7  ✓ (sorted!)
```

---

## Question 19: MPI_Reduce Matching Trap
**Q: Process 0 has a=1,c=2. Process 1 has a=2,c=1. Both call:**
```c
MPI_Reduce(&a, &b, 1, MPI_INT, MPI_SUM, 0, comm);
MPI_Reduce(&c, &d, 1, MPI_INT, MPI_SUM, 0, comm);
```
**What values do b and d have on Process 0?**

**A:** MPI_Reduce matches by **call order**, not variable names:
- First call: b = Process 0's a + Process 1's a = 1 + 2 = **3**
- Second call: d = Process 0's c + Process 1's c = 2 + 1 = **3**

(If Process 1 swapped the order of a and c in its calls, then b and d would be different!)

---

## Question 20: Complete MPI Program
**Q: Write a complete MPI program where each process computes its rank squared and process 0 prints the sum of all squared ranks.**

**A:**
```c
#include <stdio.h>
#include <mpi.h>

int main(int argc, char* argv[]) {
    int my_rank, comm_sz;
    int my_val, global_sum;
    
    MPI_Init(&argc, &argv);
    MPI_Comm_rank(MPI_COMM_WORLD, &my_rank);
    MPI_Comm_size(MPI_COMM_WORLD, &comm_sz);
    
    my_val = my_rank * my_rank;
    
    MPI_Reduce(&my_val, &global_sum, 1, MPI_INT, 
               MPI_SUM, 0, MPI_COMM_WORLD);
    
    if (my_rank == 0)
        printf("Sum of squared ranks = %d\n", global_sum);
    
    MPI_Finalize();
    return 0;
}
```

---

> **Good luck on your exam! 🍀**
> Remember: Focus on **definitions**, **formulas** (speedup/efficiency), **Flynn's Taxonomy**, **MPI collective communication rules**, **OpenMP data dependencies**, **scheduling types**, and **safety/deadlock** scenarios — these are the highest-yield topics.
