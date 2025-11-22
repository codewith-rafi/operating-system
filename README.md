# Operating Systems

## Chapter 1: Introduction to OS

### Basic Elements (Diagram - Figure 1.1)
The **Computer Components: Top-Level View** diagram shows the fundamental architecture:

**CPU Components:**
- **PC (Program Counter)**: Holds address of next instruction
- **IR (Instruction Register)**: Holds current instruction being executed
- **MAR (Memory Address Register)**: Holds memory address for read/write
- **MBR (Memory Buffer Register)**: Holds data being transferred to/from memory
- **I/O AR (Input/Output Address Register)**: Holds I/O device address
- **I/O BR (Input/Output Buffer Register)**: Holds data for I/O operations
- **Execution Unit**: Performs actual computation

**Main Memory:**
- Contains instructions and data
- Organized as sequential addresses (0, 1, 2, ... n-1, n-2)
- Each location stores instruction or data

**I/O Module:**
- Contains buffers for temporary data storage
- Manages communication with external devices
- Connected to system bus

**System Bus:**
- Bidirectional arrows show data flow between CPU, Memory, and I/O
- Central communication pathway

**How they interact**: The CPU fetches instructions from memory using MAR/MBR, decodes them in IR, executes using the execution unit, and communicates with I/O devices through I/O AR/BR.

### 1. What is an Operating System? (Definition)
An Operating System (OS) is system software that acts as an intermediary between computer hardware and application software. It manages hardware resources, provides services to applications, and gives every application the illusion of having its own CPU through time-slicing (switching between applications rapidly, typically 100 times per second or every 10ms).

### 2. Popular Operating Systems (Examples)
- **Windows** (Microsoft) - most popular desktop OS
- **Linux/Unix** - open-source, widely used in servers
- **macOS** (Apple) - used in Apple computers
- **Android** - mobile OS based on Linux
- **iOS** - Apple's mobile OS

### 3. OS vs. Apps (Similarity & Difference)
**Similarities:**
- Both are software programs
- Both execute on computer hardware
- Both serve user needs

**Differences:**
- **OS**: Acts as host/teacher - manages resources, provides platform for apps, runs in privileged mode
- **Apps**: Acts as guest/student - uses OS services, runs in user mode, performs specific tasks
- Metaphor: OS is like a teacher managing a classroom, while Apps are like students using classroom resources

### 4. Interrupts Cycle (Diagram - Figure 1.2 & 1.7)

**Basic Instruction Cycle (Top Diagram):**
```
START → Fetch next instruction → Execute instruction → HALT
        (Fetch stage)            (Execute stage)
```

**Instruction Cycle with Interrupts (Bottom Diagram):**

The complete cycle with interrupt handling:

1. **START** → Begin execution

2. **Fetch Stage**: 
   - Fetch next instruction from memory
   - Load into Instruction Register

3. **Execute Stage**:
   - Execute the instruction
   - Perform required operation

4. **Check for Interrupt**:
   - After execution, CPU checks interrupt flag
   - "Interrupts disabled?" decision point

5. **If Interrupt Enabled**:
   - **Interrupt Stage**: 
     - Check for interrupt signal
     - If interrupt exists → Jump to interrupt handler
     - Process the interrupt
     - Return to fetch next instruction

6. **If No Interrupt**:
   - Continue to fetch next instruction
   - Loop continues until HALT

**Key Points:**
- Interrupts can be temporarily disabled during critical operations
- After handling interrupt, execution resumes
- The cycle repeats: Fetch → Execute → Check Interrupt → (Handle if needed) → Repeat

**Types of Interrupts:**
- **Program**: Division by zero, illegal instruction
- **Timer**: Clock signals at regular intervals
- **I/O**: Device ready, transfer complete, error
- **Hardware Failure**: Power failure, memory parity error

### 5. Memory Hierarchy (Figure 1.14 - Pyramid Diagram)

The pyramid diagram shows memory organized by speed, size, and cost:

**From Top to Bottom (Fastest to Slowest):**

1. **Registers** (Top - smallest section)
   - Fastest access
   - Smallest capacity
   - Most expensive per byte
   - Inside CPU

2. **Cache** 
   - Very fast (L1, L2, L3)
   - Small capacity (KB to MB)
   - Expensive
   - On or near CPU

3. **Main Memory (RAM)**
   - Fast access
   - Moderate capacity (GB range)
   - Moderate cost
   - Primary storage

4. **Magnetic Disk** (Bottom - largest section)
   - Slower access
   - Large capacity (TB range)
   - Cheapest per byte
   - Secondary storage

**Key Relationships:**
- **Speed**: Registers > Cache > RAM > Disk
- **Size**: Disk > RAM > Cache > Registers  
- **Cost per byte**: Registers > Cache > RAM > Disk

**Rule**: As you go UP the pyramid: Speed ↑, Cost ↑, Size ↓

### 6. Cache Memory (Figure 1.16 - VVVI)

**Two Diagrams Shown:**

**(a) Single Cache:**
```
CPU ←→ Cache ←→ Main memory
     (Fast)  (Slow)
```
- Word transfer between CPU and Cache
- Block transfer between Cache and Main memory

**(b) Three-level Cache Organization:**
```
CPU ←→ Level 1 (L1) cache ←→ Level 2 (L2) cache ←→ Level 3 (L3) cache ←→ Main memory
       (Fastest)  (Fast)         (Fast)          (Slower)         (Slowest)
```

**How Cache Works:**

1. **CPU Request**: CPU needs data, checks L1 cache first
2. **Cache Hit (L1)**: Data found → Retrieved in ~1 nanosecond
3. **Cache Miss (L1)**: Not found → Check L2 cache
4. **Cache Miss (L2)**: Not found → Check L3 cache
5. **Cache Miss (L3)**: Not found → Fetch from Main Memory (slow ~100ns)
6. **Data Storage**: Retrieved data stored in all cache levels for future use

**Block vs. Word Transfer:**
- **Word**: Single data unit moved between CPU and cache
- **Block**: Multiple words moved between cache and main memory (exploits spatial locality)

**Cache Levels:**
- **L1 Cache**: Smallest (~32-64 KB), fastest, dedicated per core
- **L2 Cache**: Larger (~256 KB-1 MB), slightly slower, per core
- **L3 Cache**: Largest (~8-32 MB), slower, shared among all cores

**Why Cache Works:**
- **Temporal Locality**: Recently used data likely to be used again
- **Spatial Locality**: Data near recently used addresses likely to be accessed

### 7. Four Major System Development Lines

These systems created problems in timing and synchronization that contributed to the development of the **process concept**:

**A. Serial Processing Systems:**
- No operating system
- Programs run one at a time
- Manual setup and operation
- Inefficient use of resources
- Problems: scheduling time, setup time wasted

**B. Simple Batch Systems:**
- Example: IBM 701
- One job at a time
- No user interaction during execution
- Automatic job sequencing
- **Monitor** controls job flow
- Jobs collected in batches and processed sequentially

**C. Multiprogramming Batch Systems:**
- Multiple jobs in memory simultaneously
- CPU switches between jobs when one waits for I/O
- Better CPU utilization
- No interactive user input
- Increased throughput and resource utilization

**D. Time-Sharing Systems:**
- Multiple users interact simultaneously
- CPU time divided into time slices (quantum)
- Interactive computing enabled
- Each user feels like they have dedicated machine
- Response time is critical
- Example: CTSS (Compatible Time-Sharing System)

**E. Real-time Systems:**
- Must respond within strict time constraints
- Deterministic behavior required
- Used in embedded systems, process control
- Two types: Hard real-time (must meet deadline) and Soft real-time (best effort)

**Answer to MCQ Question 8: A (I, II, and III)** - Serial Processing, Multiprogramming Batch, and Time-Sharing (not Real-time) contributed most to process concept development.

---

## Chapter 2: OS Services and Structure

### OS Objectives
1. **Convenience** - Make computer easier to use
2. **Efficiency** - Optimize resource utilization
3. **Ability to Evolve** - Adapt to new hardware/requirements

### GUI vs. CUI
- **GUI (Graphical User Interface)**: Visual icons, windows, mouse-driven (Windows, macOS)
- **CUI/Shell (Command User Interface)**: Text-based commands (Linux terminal, Command Prompt)

### System Evolution - Batch vs Time-Sharing (Table 2.3)

The comparison table shows:

| **Aspect** | **Batch Multiprogramming** | **Time Sharing** |
|------------|---------------------------|------------------|
| **Principal objective** | Maximize processor use | Minimize response time |
| **Source of directives to OS** | Job control language commands provided with the job | Commands entered at the terminal |

**Key Differences:**
- **Batch Multiprogramming**: Focus on throughput, non-interactive, jobs submitted in advance
- **Time Sharing**: Focus on response time, interactive, commands entered in real-time

### System Evolution - Batch Systems

**Features of Batch Systems:**
- **Without interaction** from users during execution
- Jobs submitted as batches
- Output received after completion

**Simple Batch Systems:**
- Only **one job/task/program/process** at a time
- Example: **IBM 701** (important for MCQ!)
- Monitor program controls execution
- Sequential processing

**Multiprogramming Batch Systems:**
- **More than one job/task/program/process** in memory
- CPU switches between jobs when one waits for I/O
- Improved resource utilization

### System Evolution - Time-Sharing Systems

**Features:**
- **With interaction** from multiple users simultaneously
- Interactive computing
- Time slicing (each user gets CPU time quantum, typically 10-100ms)
- Fast response time for users
- Multiple terminals connected to central computer

### Components of OS

**1. Process Management:**
- Creation, scheduling, termination of processes
- Process synchronization and communication
- Deadlock handling

**2. Memory Management:**
- Allocation and deallocation of memory
- Virtual memory management
- Memory protection
- Paging and segmentation

**3. Information Protection and Security:**
- User authentication
- Access control
- Data encryption and protection
- Security policies

**4. Scheduling and Resource Management:**
- CPU scheduling algorithms
- Resource allocation strategies
- Priority management
- Performance optimization

**5. I/O Management / File System:**
- Device drivers and controllers
- File creation, deletion, reading, writing
- Directory management
- Storage allocation
- Buffering and caching

---

## Chapter 3: Processes

### Theme of the Chapter
Three major lines of computer system development created problems in timing and synchronization that contributed to the development of the **process** concept: multiprogramming batch operation, time-sharing, and real-time transaction systems.

### Why Processes?
Processes emerged from the need for **multiprogramming** and **time-sharing systems** to manage multiple programs efficiently and provide interactive computing.

### What is a Process?
A process is a program in execution. It consists of:
- **Program Code** (text section)
- **Data** (variables, buffers)
- **PCB (Process Control Block)** - contains process state, program counter, CPU registers, memory limits, open files
- **Address Space** - memory allocated to the process

**Formula: CPU → Address Space = PCB + Code + Data**

**Viewing Processes:**
- Windows: Task Manager
- Unix/Linux: `ps`, `top` commands

**Real-Life Example:** Think of a classroom:
- **Running**: Student actively answering question
- **Ready**: Student with hand raised, waiting to be called
- **Blocked**: Student waiting for teacher to explain something
- **Suspend**: Student temporarily sent outside

### Process State Models (VVI for Open-Ended Questions)

**1. Two-State Model [Textbook Fig 3.5]:**
- **Running**: Process is executing on CPU
- **Not Running**: Process is waiting in queue

**Simple but limited** - doesn't distinguish between different waiting reasons.

**2. Four-State Model [Textbook Table 3.1, 3.2]:**
Adds process creation and termination:
- **New**: Process being created
- **Running**: Process executing
- **Not Running**: Process waiting
- **Exit**: Process terminated

**3. Five-State Model [Textbook Fig 3.6, 3.8]:**
The most important model - splits "Not Running" into two states:

- **New**: Process being created
- **Ready**: Process waiting for CPU (has all resources except CPU)
- **Running**: Process executing on CPU
- **Blocked**: Process waiting for I/O or event (cannot proceed even if CPU available)
- **Exit**: Process terminated

**State Transitions:**
1. **New → Ready**: Process admitted to ready queue
2. **Ready → Running**: Scheduler dispatches process (Dispatch)
3. **Running → Ready**: Time quantum expired (Timeout/Preemption)
4. **Running → Blocked**: Process requests I/O (Event Wait)
5. **Blocked → Ready**: I/O completes (Event Occurs)
6. **Running → Exit**: Process completes (Terminate)

**Key Insight:**
- **Ready**: Can run but waiting for CPU
- **Blocked**: Cannot run even if CPU available (waiting for resource)

**4. Seven-State Model [Textbook Fig 3.9]:**
Adds **swapping** capability (moving processes to disk to free memory):

All five previous states, plus:
- **Ready/Suspend**: Ready process swapped to disk
- **Blocked/Suspend**: Blocked process swapped to disk

**Additional Transitions:**
- **Ready → Ready/Suspend**: Swap out ready process
- **Blocked → Blocked/Suspend**: Swap out blocked process
- **Ready/Suspend → Ready**: Swap in ready process
- **Blocked/Suspend → Ready/Suspend**: Event occurs while swapped
- **Blocked → Ready**: Event occurs in memory

**Why Suspend?**
- Free up main memory for other processes
- Handle memory shortage
- Reduce multiprogramming level

### Implementation Details

**Implementation Language:**
- **C**: High-level, portable, system programming
- **Assembly Language**: Low-level, hardware-specific, performance-critical sections

**Hardware Platform Requirements:**
- **CPU Mode Bit**: Distinguishes user mode (0) vs kernel mode (1)
  - User mode: Limited privileges, cannot execute privileged instructions
  - Kernel mode: Full privileges, can execute any instruction
- **Exception/Interruption**: Mechanism to handle errors and events

### Paradox: Is the OS itself a process?

**Answer**: The OS kernel is NOT technically a process in the traditional sense.
- The kernel runs in **kernel mode** with special privileges
- The kernel **manages** all processes but doesn't have its own PCB
- However, some OS components (like system daemons) may run as processes
- Modern OS: Kernel is passive code activated by system calls, interrupts, or exceptions

---

## Chapter 4: Threads

### Why Threads?
Same reason as multiprogramming - to **maximize CPU utilization** and improve responsiveness.

**Additional Benefits:**
- Better resource sharing within process
- More efficient than creating multiple processes
- Improved application performance
- Better user interface responsiveness

### What is a Thread?
A thread is a **lightweight process** - an execution path within a process.

**Definition**: A thread is a term in some OS - an execution path within a process; In essence: lightweight process

**What Threads Share (within same process):**
- Code section (program instructions)
- Data section (global variables)
- OS resources (open files, signals)
- Heap memory

**What Each Thread Has (private to thread):**
- Program counter (current instruction)
- Register set (CPU register values)
- Stack (local variables, function calls)

### Multithreading Approaches

**Single-threaded Approach:**
- One execution path per process
- Traditional process model
- Blocking operation halts entire process
- Simple but less efficient

**Multithreaded Approach:**
- Multiple execution paths per process
- One thread blocks, others continue
- Better CPU utilization
- More complex but more efficient

**Example:**
```
Single-threaded Web Browser:
- Download image (BLOCKED - entire browser frozen)

Multi-threaded Web Browser:
- Thread 1: Download image (blocked)
- Thread 2: Display already loaded content (continues)
- Thread 3: Handle user input (responsive)
```

### Thread Implementation Types (VVI)

**1. ULT (User-Level Threads):**
- Example: Linux (some implementations), POSIX threads
- Managed by **thread library** in user space
- Kernel is unaware of threads (sees single process)

**Advantages:**
- Fast thread creation and switching (no kernel involvement)
- No kernel support needed
- Portable across different OS
- Application-specific scheduling possible

**Disadvantages:**
- Blocking system call blocks ALL threads in process
- Cannot take advantage of multiprocessor (kernel schedules process, not threads)
- No true parallelism

**2. KLT (Kernel-Level Threads):**
- Example: Windows, Linux (modern), Solaris
- Managed by **OS kernel**
- Kernel aware of all threads

**Advantages:**
- True parallelism on multiprocessor systems
- One thread blocks, others in same process continue
- Better multiprocessing support
- Kernel can schedule threads independently

**Disadvantages:**
- Slower creation and switching (kernel mode transitions required)
- Higher overhead
- Less portable

**3. Combined Approach:**
- Example: Solaris (two-level model)
- Many ULT mapped to fewer KLT
- **Many-to-many mapping**
- Combines benefits of both approaches

**Advantages:**
- Flexibility in scheduling
- Can have many ULT with reasonable number of KLT
- Good performance and parallelism

### VVI Differences

**Process vs. Thread:**

| **Aspect** | **Process** | **Thread** |
|-----------|-----------|----------|
| **Definition** | Independent execution unit | Execution path within process |
| **Memory** | Separate address space | Shares address space |
| **Overhead** | Heavyweight | Lightweight |
| **Creation time** | Slow | Fast |
| **Context switch** | Expensive | Cheap |
| **Communication** | IPC (Inter-Process Communication) needed | Shared memory directly |
| **Control Block** | PCB | TCB |
| **Protection** | Strong isolation | Less isolation |

**PCB vs. TCB:**

| **Aspect** | **PCB (Process Control Block)** | **TCB (Thread Control Block)** |
|-----------|-------------------------------|------------------------------|
| **Contains** | All process information | Thread-specific information |
| **Includes** | Process state, memory limits, open files, etc. | PC, registers, stack pointer, thread state |
| **Size** | Large | Small |
| **Scope** | Entire process | Single thread |

**ULT vs. KLT:**

| **Aspect** | **ULT (User-Level Threads)** | **KLT (Kernel-Level Threads)** |
|-----------|----------------------------|------------------------------|
| **Management** | Thread library (user space) | OS kernel |
| **Kernel awareness** | Kernel unaware | Kernel aware |
| **Switching speed** | Fast (no mode switch) | Slow (kernel involvement) |
| **Blocking** | Blocks entire process | Blocks only that thread |
| **Multiprocessor** | No true parallelism | True parallelism |
| **Example** | Early POSIX threads | Windows threads |
| **Overhead** | Low | High |
| **Scheduling** | User-level scheduler | Kernel scheduler |

---

## Chapter 5: Concurrency

### Key Concepts

**Concurrency:**
Execution of multiple processes simultaneously using time-sharing on a uni-processor. In reality, processes take turns very quickly, giving the appearance of simultaneous execution.

**Types:**
- **Multiprogramming**: Multiple programs in memory, CPU switches between them
- **Multiprocessing**: Multiple CPUs/cores execute simultaneously
- **Distributed Processing**: Multiple systems networked together

### Concurrent vs. Parallel Programming
- **Concurrent**: Tasks appear to run simultaneously (single CPU, time-sharing) - interleaved execution
- **Parallel**: Tasks actually run simultaneously (multiple CPUs) - true simultaneous execution

### Problems in Concurrency (VVVI Table 5.1)

The **Some Key Terms Related to Concurrency** table defines critical concepts:

| **Term** | **Definition** |
|----------|---------------|
| **Atomic operation** | A function or action implemented as a sequence of one or more instructions that appears to be indivisible; other processes can see the operation as complete or not complete, they cannot see an intermediate state. Guarantees isolation from concurrent processes. |
| **Critical section** | A section of code within a process that requires access to shared resources and must not be executed while another process is in a corresponding section of code. |
| **Deadlock** | A situation in which two or more processes are unable to proceed because each is waiting for one of the others to do something. |
| **Livelock** | A situation in which two or more processes continuously change their states in response to changes in other processes without doing any useful work. |
| **Mutual exclusion** | The requirement that when one process is in a critical section that accesses shared resources, no other process may be in a critical section that accesses any of those shared resources. |
| **Race condition** | A situation in which multiple threads or processes read and write a shared data item and the final result depends on the relative timing of their execution. |
| **Starvation** | A situation in which a runnable process is overlooked indefinitely by the scheduler; although it is able to proceed, it is never chosen. |

### Example: Race Condition (Pages 8-9 of Chapter 5 PDF)

**Scenario 2: A Simple Example of a Shared Variable**

The diagrams show what happens when two processes access a shared variable without proper synchronization:

**Setup:**
```c
/* Process P1 */
void echo() {
    int x, y;
    x = value;
    y = x + 1;
    value = y;
    print(value);
}

/* Process P2 - same code */
void echo() {
    int x, y;
    x = value;
    y = x + 1;
    value = y;
    print(value);
}
```

**Initial state**: `value = 1` (shared variable)

**Race Condition Illustrated:**

The diagrams show different execution orderings:

**Scenario 1 (Correct - No Interference):**
```
Process P1:                    Process P2:
x = value (x=1)
y = x+1 (y=2)
value = y (value=2)
print(2) ✓
                               x = value (x=2)
                               y = x+1 (y=3)
                               value = y (value=3)
                               print(3) ✓
Result: value = 3 (CORRECT)
```

**Scenario 2 (Race Condition - Interference):**
```
Process P1:                    Process P2:
x = value (x=1)
                               x = value (x=1) ← Read same value!
y = x+1 (y=2)
                               y = x+1 (y=2) ← Same calculation!
value = y (value=2)
print(2)
                               value = y (value=2) ← Overwrites!
                               print(2)
Result: value = 2 (WRONG! Should be 3)
```

**What went wrong:**
- Both processes read the same initial value
- Both independently incremented
- Both wrote back, one overwriting the other
- One increment was "lost"

### Example: Race Condition (Chapter 5 Diagrams)

The detailed execution traces shown in the PDF demonstrate:
- Six possible execution orderings
- Some produce correct results (value=3)
- Some produce incorrect results (value=2)
- Result depends on timing - this is the essence of a race condition

**Solution**: Use **mutual exclusion** to ensure only one process accesses the shared variable at a time.

### VVVI: Mutual Exclusion

**Definition:** A property of concurrency control that ensures only one process can access a critical section (shared resource) at a time, preventing race conditions.

**Critical Section:** Code segment where shared resources are accessed.

**Requirements for Mutual Exclusion:**
1. **Mutual Exclusion**: Only one process in critical section at a time
2. **Progress**: No process outside critical section can block others from entering
3. **Bounded Waiting**: No indefinite waiting (no starvation) - must eventually enter
4. **No Assumptions**: Solution must work regardless of number of processes or relative speeds

**Structure:**
```c
// Entry section
acquire_lock();
    /* Critical Section - access shared resource */
release_lock();
// Exit section
    /* Remainder section */
```

### Synchronization
A technique to coordinate processes using shared data, ensuring correct order of execution.

**Purpose:**
- Coordinate timing of events
- Ensure operations occur in correct sequence
- Signal between processes

**Example**: Producer-Consumer
- Producer must produce before consumer can consume
- Consumer must wait if buffer empty
- Producer must wait if buffer full

### Concurrency Implementation Methods

**1. Hardware Approaches:**

**Interrupt Disabling:**
```c
disable_interrupts();
/* Critical section */
enable_interrupts();
```
- Simple but crude
- Only works on single processor
- Cannot be used in user mode

**CAS (Compare-And-Swap):**
```c
int CAS(int *ptr, int expected, int new_value) {
    int actual = *ptr;
    if (actual == expected) {
        *ptr = new_value;
        return actual;
    }
    return actual;
}
```
- Atomic operation
- Compares value before swapping (conditional)
- Returns actual value
- Modern processors support this

**XCHG (Exchange):**
```c
int XCHG(int *ptr, int new_value) {
    int old_value = *ptr;
    *ptr = new_value;
    return old_value;
}
```
- Atomic operation
- Unconditionally swaps values
- Simpler than CAS

**CAS vs. XCHG:**
- **CAS**: Conditional - checks expected value before swapping
- **XCHG**: Unconditional - always swaps regardless of current value
- **CAS**: More flexible, can detect if value changed
- **XCHG**: Simpler, always succeeds

**2. Software Approaches:**

**Dekker's Algorithm:**
- First correct software solution for mutual exclusion
- Works for 2 processes
- Uses shared variables and busy waiting
- Complex but historically important

**Peterson's Algorithm:**
- Simpler than Dekker's
- Works for 2 processes
- Uses two shared variables: flag[] and turn
- Easier to understand and prove correct

```c
// Peterson's Algorithm (Process i)
flag[i] = true;
turn = j; // Give priority to other process
while (flag[j] && turn == j); // Busy wait
    /* Critical Section */
flag[i] = false;
```

**3. OS and Programming Language Mechanisms:**

**Semaphore (by Edsger Dijkstra, 1965):**

A programming construct that helps achieve concurrency by implementing both mutual exclusion and synchronization.

**Definition**: Integer variable with two atomic operations:
- **wait() / P() / down()**: Decrement semaphore, block if negative
- **signal() / V() / up()**: Increment semaphore, wake up waiting process

**Operations:**
```c
wait(S):              signal(S):
  S = S - 1             S = S + 1
  if (S < 0)            if (S <= 0)
    block process         wake up a waiting process
```

**Types of Semaphores:**

**Binary Semaphore:**
- Value: 0 or 1
- Similar to mutex
- Used for mutual exclusion

**Counting Semaphore:**
- Value: Any non-negative integer
- Used to control access to resource pool
- Value represents number of available resources

**Example - Mutual Exclusion with Binary Semaphore:**
```c
semaphore mutex = 1; // Initialize to 1

Process:
  wait(mutex);        // Decrement, enter if 1, block if 0
    /* Critical Section */
  signal(mutex);      // Increment, allow next process
```

**Example - Producer-Consumer with Counting Semaphore:**
```c
semaphore empty = N;  // N empty slots
semaphore full = 0;   // 0 full slots

Producer:             Consumer:
  wait(empty);          wait(full);
  /* produce item */    /* consume item */
  signal(full);         signal(empty);
```

**Monitor:**
- High-level synchronization construct
- Encapsulates shared data and procedures
- Only one process can be active in monitor at a time
- Automatic mutual exclusion
- Condition variables for synchronization
- Easier to use than semaphores, less error-prone

**Message Passing:**
- Processes communicate by sending/receiving messages
- No shared memory required
- Useful in distributed systems
- Two operations: send(message) and receive(message)
- Can be synchronous (blocking) or asynchronous (non-blocking)

### Binary Semaphore vs. Mutex (Important Table from PDF)

| **Aspect** | **Binary Semaphore** | **Mutex (Mutual Exclusion)** |
|-----------|---------------------|------------------------------|
| **Value** | 0 or 1 | Locked or Unlocked |
| **Ownership** | No ownership concept | Has ownership - only the thread that locked can unlock |
| **Purpose** | Signaling/synchronization between processes | Mutual exclusion (protecting critical section) |
| **Operation** | Any process can signal() | Only owner can unlock |
| **Use Case** | Producer-consumer synchronization | Protecting shared resource |
| **Releasing** | Can be signaled by different process | Must be released by same process that acquired it |

**Key Difference:**
- **Binary Semaphore**: Process A can wait(), Process B can signal() - used for synchronization
- **Mutex**: Same process/thread must both lock and unlock - used for mutual exclusion ownership matters

**Example:**
```c
/* Binary Semaphore (Synchronization) */
semaphore item_ready = 0;
Producer:                Consumer:
  produce_item();          wait(item_ready);
  signal(item_ready);      consume_item();

/* Mutex (Mutual Exclusion) */
mutex lock;
Process:
  lock(lock);
  /* critical section */
  unlock(lock);  // MUST be same process
```

---

## Chapter 6: Deadlock

### Why Deadlock?
Permanent blocking of a set of processes that compete for system resources or communicate with each other.

**Definition**: A set of processes is deadlocked when each process is waiting for an event that only another process in the set can cause.

### When Deadlock Occurs
Deadlock occurs when: **each process holds 1 resource & requests the other.**

### Deadlock Examples (Scenarios 1 & 2 from PDF)

**Scenario 1: Disk File, Tape Drive**
```
Process P  | Process Q
-----------+-----------
Request(T) | Request(D)
Request(D) | Request(T)
Lock(T)    | Lock(D)
Lock(D)    | Lock(T)
Unlock(T)  | Unlock(D)
Unlock(D)  | Unlock(T)
```

**What happens:**
- P gets tape drive (T), requests disk (D)
- Q gets disk (D), requests tape (T)
- **Deadlock!** Both waiting for each other

**Scenario 2: Main Memory**
```
200K bytes of memory available
P1 needs 140K total, 80K blocks
P2 needs 150K total, 70K blocks
```

**Execution:**
1. P1 requests 80 Kbytes → granted (120K remaining)
2. P2 requests 70 Kbytes → granted (50K remaining)
3. P1 requests 60 Kbytes → **BLOCKED** (needs 60K, only 50K available)
4. P2 requests 80 Kbytes → **BLOCKED** (needs 80K, only 50K available)
- **Deadlock!** Both blocked, neither can release their held memory

### Resource Allocation Graph (Critical for Understanding Deadlock)

**Directed Graph Components:**
- **Circles (○)**: Processes (P1, P2, P3, P4)
- **Squares (□)**: Resource types (R1, R2, R3)
- **Dots inside squares**: Number of instances of that resource
- **Arrows**:
  - **Process → Resource** (Request edge): Process requesting resource
  - **Resource → Process** (Assignment edge): Resource allocated to process

**Example from PDF Diagrams:**

**Left Diagram (No Deadlock):**
```
P1 holds R2, requests nothing
P2 holds nothing, requests R1
P3 holds R3, requests R2
P4 holds R1, R3, requests R2
```
- Multiple resources have multiple instances
- Can be resolved by reallocating resources
- **No cycle or cycle can be broken**

**Right Diagram (Deadlock Exists - Coffman Deadlock):**
```
Circular chain:
P1 → R1 → P2 → R3 → P3 → R2 → P1
```
This shows a **cycle**:
- P1 holds R2, requests R1
- P2 holds R1, requests R3
- P3 holds R3, requests R2
- **Circular wait detected = DEADLOCK!**

**Additional Diagram (Dining Philosophers):**
The circular table diagram shows 5 philosophers (P1-P5) with 5 forks (R1-R5) between them - classic deadlock scenario.

**How to Use Resource Allocation Graphs:**
1. Draw circles for processes, squares for resources
2. Draw dots inside squares for multiple resource instances
3. Draw request arrows (process → resource)
4. Draw assignment arrows (resource → process)
5. **Check for cycles:**
   - If cycle exists with **single-instance resources** → Definite Deadlock
   - If cycle exists with **multiple-instance resources** → Potential Deadlock (need further analysis)
   - If no cycle → No Deadlock

**Key Rule:**
- **Cycle + Single instance per resource type = DEADLOCK**
- **Cycle + Multiple instances = MAYBE deadlock** (requires additional analysis)
- **No Cycle = NO DEADLOCK**

### The Conditions for Deadlock

**All FOUR conditions must be present simultaneously** for deadlock to occur:

1. **Mutual Exclusion**: 
   - Only one process can use a resource at a time
   - Resources are non-shareable
   - Example: Printer, write access to file

2. **No Preemption**: 
   - Resources cannot be forcibly taken from a process
   - Process must voluntarily release resources
   - Cannot force process to give up held resources

3. **Hold-and-Wait**: 
   - Process holds at least one resource while waiting for additional resources
   - Process doesn't release currently held resources when requesting new ones

4. **Circular Wait**: 
   - Circular chain of processes exists
   - Each process waiting for resource held by next process in chain
   - Forms a cycle: P1→P2→P3→...→Pn→P1

**Remember**: All 4 must exist together. **Eliminate any ONE condition → No deadlock possible!**

### Deadlock Prevention (Detailed)

Strategy: **Eliminate one of the four necessary conditions**

**1. To Eliminate Mutual Exclusion:**
- **We can't eliminate this condition** (highlighted in yellow in PDF)
- Some resources are inherently non-shareable (e.g., printer, write access to file)
- Making resources shareable when possible (e.g., read-only files can be shared)
- **Conclusion**: Not a practical general solution for most resources

**2. To Eliminate No Preemption:**

**Approach:**
- Allow OS to preempt (forcibly take) resources from processes
- If process requests unavailable resource, preempt its currently held resources
- Process must request all resources again when available

**How it works:**
- Process holds R1, requests R2 (unavailable)
- OS preempts R1 from process
- Process added to waiting list for both R1 and R2
- When both available, process can restart

**Advantages:**
- Works for resources whose state can be saved/restored (CPU, memory)

**Disadvantages:**
- Doesn't work for resources like printers (can't save half-printed document)
- Wasted work when preemption occurs
- Process may have to restart from beginning

**3. To Eliminate Hold-and-Wait:**

**Approach 1: Request all at once**
- Require process to request ALL resources at once before execution starts
- If any resource unavailable, process waits and holds nothing
- Only start execution when all needed resources available

**Approach 2: Release before requesting**
- Process must release all currently held resources before requesting new ones
- Can only request resources when holding nothing

**Advantages:**
- Simple to implement
- Prevents hold-and-wait situation

**Disadvantages:**
- **Low resource utilization**: Resources held but not used immediately
- **Starvation possible**: Process may never get all resources simultaneously
- **Inconvenient**: Process may not know all needed resources in advance
- Reduces degree of multiprogramming

**4. To Eliminate Circular Wait:** ✓ **Most Practical Approach**

**Method:**
- Impose **total ordering** on all resource types
- Assign each resource type a unique number: R1 < R2 < R3 < ... < Rn
- Process must request resources in **increasing order only**
- If process holds resource Ri, it can only request Rj where j > i

**Example:**
```
Resource ordering:
R1 = Tape drive (priority 1)
R2 = Disk drive (priority 2)
R3 = Printer (priority 3)

Valid requests:
- Request Tape → Disk → Printer ✓
- Request Tape → Printer ✓
- Request Disk → Printer ✓

Invalid requests:
- Request Printer → Disk ✗ (violates order: 3 > 2)
- Request Disk → Tape ✗ (violates order: 2 > 1)
```

**Why it works:**
- Prevents circular chain formation
- No cycle possible in resource allocation graph
- If P1 holds Ri and P2 holds Rj (j > i), P1 cannot request Rj (already held by P2) and P2 cannot request Ri (lower number)

**Advantages:**
- **Most practical** prevention method
- Provably prevents deadlock
- Relatively low overhead

**Disadvantages:**
- May require requesting resources in inconvenient order
- May need to request resources earlier than needed
- Requires knowledge of resource numbering scheme

### Deadlock Avoidance (Two Approaches)

Strategy: **Don't allocate resource if it leads to unsafe state**

**Safe State vs. Unsafe State:**
- **Safe State**: System can allocate resources to all processes in some order without deadlock
- **Unsafe State**: No guarantee that deadlock can be avoided; may lead to deadlock

**1. Process Initiation Denial:**
- Don't start process if its maximum resource claims lead to deadlock
- Very conservative approach
- Check: Can system satisfy maximum claims of all processes including new one?
- If no, don't start new process

**2. Resource Allocation Denial (Banker's Algorithm):**

**Concept:**
- Before allocating resource, check if allocation leaves system in safe state
- Only allocate if system remains safe after allocation
- Named after banking principle: don't lend money if you can't satisfy all depositors

**Safe State Definition:**
- There exists a sequence of processes <P1, P2, ..., Pn> such that:
  - For each Pi, resources it may still request can be satisfied by currently available resources + resources held by all Pj where j < i
  - If Pi's resources not immediately available, Pi waits until all Pj finish
  - When Pj finishes, Pi gets needed resources, executes, returns resources, terminates

**Algorithm Steps:**
1. Process requests resources
2. Pretend to allocate resources
3. Check if resulting state is safe (using safety algorithm)
4. If safe, actually allocate; if unsafe, deny request

**Advantages:**
- Less restrictive than prevention
- Better resource utilization than prevention
- No deadlock possible

**Disadvantages:**
- Must know maximum future resource requests in advance (often impractical)
- Runtime overhead for safety checking
- Reduces concurrency (conservative allocations)
- Not always practical in real systems

### Deadlock Detection and Recovery

Strategy: **Allow deadlock to occur, then detect and recover**

**Detection:**
- Periodically run detection algorithm
- Check resource allocation graph for cycles
- For single-instance resources: Simple cycle detection
- For multiple-instance resources: Use reduction algorithm similar to Banker's

**When to Run Detection:**
- Every time resource request is made (high overhead)
- Periodically (e.g., every hour)
- When CPU utilization drops (sign processes may be deadlocked)

**Recovery Methods:**

**1. Process Termination:**
- **Abort all deadlocked processes**: Simple but wasteful
- **Abort one process at a time**: Less wasteful, but higher overhead (must detect after each abortion)

**Factors in choosing victim:**
- Priority of process
- How long process has run
- How much longer to completion
- Resources held by process
- Resources needed by process
- How many processes must be terminated
- Is process interactive or batch?

**2. Resource Preemption:**
- Preempt resources from deadlocked processes
- Give preempted resources to other processes

**Issues:**
- **Selecting victim**: Which process to preempt from?
- **Rollback**: Must rollback process to safe state before preemption
- **Starvation**: Same process may always be picked as victim (use rollback count in selection)

**Advantages:**
- No restrictions on resource requests
- Maximum resource utilization
- Flexible approach

**Disadvantages:**
- Detection overhead
- Recovery cost (lost work, process termination)
- Potential data loss or inconsistency

### VVVI Summary Table (Image 12 - Deadlock Handling Strategies)

The comprehensive comparison table from the PDF:

| **Approach** | **Resource Allocation Policy** | **Different Schemes** | **Major Advantages** | **Major Disadvantages** |
|--------------|-------------------------------|----------------------|---------------------|------------------------|
| **Prevention** | Conservative; undercommits resources | Requesting all resources at once; Preemption; Resource ordering | • Works well for processes that perform a single burst of activity<br>• No preemption necessary | • Inefficient<br>• Delays process initiation<br>• Future resource requirements must be known by processes |
| **Avoidance** | Midway between prevention and detection | Manipulation of resource allocation to find at least one safe path | • Less restrictive than prevention<br>• No preemption necessary | • Future resource requirements must be known<br>• Processes can be blocked for long periods |
| **Detection** | Very liberal; requested resources are granted when possible | Invoke periodically to test for deadlock | • Never delays process initiation<br>• Facilitates online handling | • Inherent preemption losses<br>• Must be invoked periodically for lost cycles |

**When to Use Each Strategy:**

**Prevention**: 
- Safety-critical systems (nuclear plants, medical devices, aircraft)
- Systems where deadlock is unacceptable
- Small systems with predictable resource needs

**Avoidance**: 
- Systems with predictable maximum resource needs
- Batch systems
- Systems where processes can wait

**Detection**: 
- Large interactive systems with occasional deadlocks
- Systems where deadlock is rare
- Database systems (use detection with rollback)

**Ignore (Ostrich Algorithm)**: 
- Desktop systems (Windows, UNIX, Linux)
- Systems where deadlock is very rare
- Cost of prevention/avoidance exceeds cost of occasional reboot
- User can manually restart if deadlock occurs

**Most Common in Practice**: 
Many modern operating systems use **"Ignore"** strategy because:
- Deadlocks are rare in practice
- Prevention/avoidance overhead is high
- Detection/recovery is complex
- Users can restart applications or reboot system if needed
- Cost-benefit analysis favors ignoring over preventing

### Brainstorm: Dining Philosophers Problem

**Classic synchronization and deadlock problem:**

**Setup:**
- 5 philosophers sit at a round table
- 5 forks placed between philosophers (one between each pair)
- Each philosopher alternates between thinking and eating
- **To eat**: Philosopher needs **BOTH** forks (left and right)
- **After eating**: Philosopher puts down both forks and thinks

**The Problem:**
```
Philosopher 1 picks up fork 1 (between P1 and P2)
Philosopher 2 picks up fork 2 (between P2 and P3)
Philosopher 3 picks up fork 3 (between P3 and P4)
Philosopher 4 picks up fork 4 (between P4 and P5)
Philosopher 5 picks up fork 5 (between P5 and P1)

Now each philosopher holds ONE fork and needs another fork...
All philosophers waiting forever = DEADLOCK!
```

**Why Deadlock Occurs:**
1. **Mutual Exclusion**: Fork can be held by only one philosopher ✓
2. **No Preemption**: Philosopher won't give up fork voluntarily ✓
3. **Hold-and-Wait**: Philosopher holds one fork while waiting for another ✓
4. **Circular Wait**: P1→P2→P3→P4→P5→P1 ✓

All four conditions present → Deadlock!

**Solutions:**

**1. Allow only 4 philosophers to sit:**
- At most 4 can try to eat simultaneously
- Guarantees at least one can get both forks
- Eliminates some hold-and-wait situations

**2. Pick up both forks atomically (Critical Section):**
- Philosopher must acquire lock before picking up any fork
- Pick up both forks together or neither
- Release lock after picking up both
- Eliminates hold-and-wait

```c
lock(mutex);
  pickup(left_fork);
  pickup(right_fork);
unlock(mutex);
eat();
putdown(left_fork);
putdown(right_fork);
```

**3. Asymmetric solution (Odd/Even):**
- **Odd-numbered philosophers**: Pick up left fork first, then right
- **Even-numbered philosophers**: Pick up right fork first, then left
- Breaks circular wait pattern
- At least one philosopher can always get both forks

**4. Resource ordering:**
- Number forks 1 through 5
- Always pick up lower-numbered fork first
- Example: Between forks 1 and 5, always pick up 1 first
- Prevents circular wait
- Similar to "eliminate circular wait" prevention strategy

**Real-World Applications:**
- Process synchronization
- Database transaction management
- Resource allocation in distributed systems
- Network routing algorithms

---

## Quick Review Tips

### Most Important Topics (VVVI):
1. **Memory Hierarchy** - speed, size, cost relationships (pyramid)
2. **Cache Memory** - what it is and how it works (L1/L2/L3)
3. **Interrupt Cycle** - fetch-execute with interrupt handling
4. **Process State Models** - especially five-state and seven-state with transitions
5. **Mutual Exclusion** - definition, requirements, and race conditions
6. **Semaphores** - how they work, wait/signal operations, binary vs counting
7. **Four Conditions for Deadlock** - memorize all four (must all be present)
8. **Deadlock Prevention** - which conditions can/cannot be eliminated
9. **Resource Allocation Graphs** - how to draw and interpret, detect cycles
10. **Process vs Thread** differences (PCB vs TCB)
11. **ULT vs KLT** differences and trade-offs

### For MCQs:
- **Names of OS during evolution**: IBM 701 for Simple Batch Systems
- **Three lines contributing to process concept**: Serial, Multiprogramming, Time-Sharing (Answer: A - I, II, and III)
- **Basic elements**: CPU (PC, IR, MAR, MBR, etc.), Memory, I/O, System Bus
- **Batch vs Time-Sharing**: Maximize processor use vs Minimize response time
- **Definitions**: All terms from concurrency table (atomic operation, critical section, deadlock, livelock, mutual exclusion, race condition, starvation)
- **Four deadlock conditions**: Must know all four
- **Thread types**: ULT (Linux), KLT (Windows), Combined (Solaris)
- **CAS vs XCHG**: Conditional vs Unconditional

### For Open-Ended Questions:
1. **Draw and explain process state models**:
   - Five-state: New, Ready, Running, Blocked, Exit with all transitions
   - Seven-state: Add Ready/Suspend and Blocked/Suspend
   - Explain each transition with examples

2. **Explain mutual exclusion with race condition example**:
   - Use the shared variable increment example
   - Show how race condition occurs
   - Explain solution with mutex/semaphore

3. **Describe deadlock scenarios**:
   - Give real example (disk and tape, or memory allocation)
   - Draw resource allocation graph
   - Identify all four conditions present
   - Explain prevention/avoidance/detection approaches

4. **Compare ULT vs KLT**:
   - Management (user space vs kernel)
   - Advantages and disadvantages of each
   - Give examples (Linux ULT, Windows KLT)

5. **Explain semaphore operations**:
   - Wait() and Signal() operations
   - Binary vs Counting semaphores
   - Example: mutex or producer-consumer

6. **Memory hierarchy and cache**:
   - Draw pyramid: Registers → Cache → RAM → Disk
   - Explain speed, size, cost relationships
   - Describe cache hit/miss
   - Explain principle of locality

7. **Interrupt handling**:
   - Draw instruction cycle with interrupts
   - Explain fetch-execute-interrupt checking
   - Describe what happens during interrupt

8. **Dining Philosophers Problem**:
   - Describe the setup and deadlock scenario
   - Identify four deadlock conditions
   - Provide at least 2-3 solutions

### Key Diagrams to Practice Drawing:
1. Basic computer elements (CPU, Memory, I/O, System Bus)
2. Instruction cycle with interrupts
3. Memory hierarchy pyramid
4. Cache organization (single and three-level)
5. Five-state process model with all transitions
6. Seven-state process model with suspend states
7. Resource allocation graphs (with and without cycles)
8. Race condition execution sequences
9. Dining philosophers circular arrangement

### Important Formulas/Concepts:
- **Process = PCB + Code + Data**
- **Thread shares**: Code, Data, Files (within process)
- **Thread private**: PC, Registers, Stack
- **Deadlock requires**: ALL 4 conditions simultaneously
- **Safe state**: Can allocate to all processes in some order
- **Race condition**: Final result depends on execution timing

---
