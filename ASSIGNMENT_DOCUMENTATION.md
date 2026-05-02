# Assignment 3 - Complete Documentation

**Student Name**: [Rwaida Farhan]  
**Student ID**: [445052062]  
**Date Submitted**: [Submission Date]

---

## 🎥 VIDEO DEMONSTRATION LINK (REQUIRED)

> **⚠️ IMPORTANT: This section is REQUIRED for grading!**
> 
> Upload your 3-5 minute video to your **PERSONAL Gmail Google Drive** (NOT university email).
> Set sharing to "Anyone with the link can view".
> Test the link in incognito/private mode before submitting.

**Video Link**: [Paste your personal Gmail Google Drive link here]

**Video filename**: `[YourStudentID]_Assignment3_Synchronization.mp4`

**Verification**:
- [ ] Link is accessible (tested in incognito mode)
- [ ] Video is 3-5 minutes long
- [ ] Video shows code walkthrough and commits
- [ ] Video has clear audio
- [ ] Uploaded to PERSONAL Gmail (not @std.psau.edu.sa)

---

## Part 1: Development Log (1 mark)

Document your development process with **minimum 3 entries** showing progression:

### Entry 1 - [1 May, 6:00 AM]
**What I implemented**:
 I found shared resources that need to be synchronized after analyzing the code.

**Challenges encountered**: 
Recognizing potential racial situations
**How I solved it**: 
I looked over common variables and noted important passages.
**Testing approach**: 
To examine behavior, the software was run without synchronization.
**Time spent**: 
1.5 hours
---

### Entry 2 - [1 May, 9:10 AM]
**What I implemented**: 
ReentrantLock was added to safeguard the execution log and shared counters.
**Challenges encountered**: 
Making sure locks are always unlocked
**How I solved it**: 
Used try-finally blocks
**Testing approach**: 
After execution, the right counter values were verified.
**Time spent**: 
2 hours
---

### Entry 3 - [1 May, 12:30 PM]
**What I implemented**: 
Semaphore was included to regulate CPU access.
**Challenges encountered**: 
Managing the InterruptedException
**How I solved it**: 
Try-catch wrapped acquire()
**Testing approach**: 
Verified only one process runs at a time
**Time spent**: 
1.5 hours
---

### Entry 4 - [1 May, 5:30 PM]
**What I implemented**: 
RunToCompletion() synchronization has been fixed.
**Challenges encountered**: 
Try-catch structure that is nested
**How I solved it**: 
Correctly reorganized code
**Testing approach**: 
Last process execution was tested.
**Time spent**: 
2.5 hours
---

### Entry 5 - [1 May, 10:30 PM]
**What I implemented**: 
Final verification and testing
**Challenges encountered**: 
Maintaining uniformity
**How I solved it**: 
Ran program multiple times
**Testing approach**: 
Confirmed counters and logs
**Time spent**: 
1 hour
---

## Part 2: Technical Questions (1 mark)

### Question 1: Race Conditions
**Q**: Identify and explain TWO race conditions in the original code. For each:
- What shared resource is affected?
- Why is concurrent access a problem?
- What incorrect behavior could occur?

**Your Answer**:

When several threads access shared data at the same time, a race condition arises.
ContextSwitchCount is the first example. It is incremented by many threads, which could result in inaccurate values.
ExecutionLog is the second example. Concurrent access could harm data since ArrayList is not thread-safe.
---

### Question 2: Locks vs Semaphores
**Q**: Explain the difference between ReentrantLock and Semaphore. Where did you use each in your code and why?

**Your Answer**:

ReentrantLock only permits one thread at a time and offers mutual exclusion.
I utilized ReentrantLock for counters and Semaphore for CPU control. Semaphore regulates the number of threads that can access a resource.

---

### Question 3: Deadlock Prevention
**Q**: What is deadlock? Explain TWO prevention techniques and what you did to prevent deadlocks in your code.

**Your Answer**:

When threads wait indefinitely, it's called deadlock.

Avoidance:
To release locks, use try-finally
Steer clear of nested locks
I used to eventually release locks and semaphores in my code.

---

### Question 4: Lock Granularity Design Decision 
**Q**: For Task 1 (protecting the three counters), explain your lock design choice:
- Did you use ONE lock for all three counters (coarse-grained) OR separate locks for each counter (fine-grained)?
- Explain WHY you made this choice
- What are the trade-offs between the two approaches?
- Given that the three counters are independent, which approach provides better concurrency and why?

**Your Answer**:

I utilized a single coarse-grained lock.
It makes implementation easier.

Trade-off
Reduced concurrency
Increased security
More complexity but improved performance are possible with fine-grained

---

## Part 3: Synchronization Analysis (1 mark)

### Critical Section #1: Counter Variables

**Which variables**: 
contextSwitchCount, completedprocessCount, totalWaitingTime
**Why they need protection**: 
they are shared among threads
**Synchronization mechanism used**: 
ReentrantLock
**Code snippet**:
```java
// Paste your implementation here
```lock.lock();
try {
    contextSwitchCount++;
} finally {
    lock.unlock();
}

**Justification**: 
Ensures mutual exclusion and prevents race conditions
---

### Critical Section #2: Execution Log

**What resource**: 
executionLog
**Why it needs protection**: 
ArrayList not thread-safe
**Synchronization mechanism used**: 
Lock
**Code snippet**:
```java
// Paste your implementation here
```lock.lock();
try {
    executionLog.add(message);
} finally {
    lock.unlock();
}

**Justification**: 
prevents data corruption and exceptions
---

### Critical Section #3: CPU Semaphore

**Purpose of semaphore**: 
control CPU access
**Number of permits and why**: 
single CPU 1
**Where implemented**: 
inside run() method
**Code snippet**:
```java
// Paste your implementation here
```cpuSemaphore.acquire();
...
cpuSemaphore.release();

**Effect on program behavior**: 
make sure only one process executes at a time
---

## Part 4: Testing and Verification (2 marks)

### Test 1: Consistency Check
**What I tested**: Running program multiple times to verify consistent results

**Testing procedure**: 
```bash
# Commands used (run the program at least 5 times)
# Run the program at least 5 times
javac SchedulerSimulationSync.java

java SchedulerSimulationSync
java SchedulerSimulationSync
java SchedulerSimulationSync
java SchedulerSimulationSync
java SchedulerSimulationSync

**Results**: 
═══ Synchronization Statistics ═══
Total Context Switches: 38
Total Completed Processes: 17
Total Waiting Time: 1487333ms
Average Waiting Time: 87490ms

═══ Process Summary Table ═══
Process    Priority     Burst Time   Waiting Time
────────────────────────────────────────────────
P1         5            5192         63039       
P2         3            6399         64263       
P3         3            8489         103276      
P4         2            9610         103815      
P5         1            6386         74842       
P6         4            4437         77289       
P7         4            7073         77738       
P8         1            9600         105497      
P9         2            9949         107148      
P10        3            6553         89009       
P11        1            9933         109181      
P12        3            2698         44591       
P13        1            5810         95701       
P14        4            6058         97541       
P15        2            8048         111167      
P16        2            3350         59558       
P17        1            7568         103678      

═══ Execution Log Summary ═══
Total log entries: 76

**Why synchronization is necessary**: 
Race conditions could result from several threads accessing and changing shared resources at the same time in the absence of synchronization.
For instance:
Increments may be missed since contextSwitchCount++ is not atomic.
Because executionLog.add() is not thread-safe, it may corrupt the ArrayList.
Inaccurate accumulated values could result from totalWaitingTime += time.
These problems might arise unexpectedly and lead to inaccurate outcomes, even if they are not always apparent.

**Conclusion**: 
ReentrantLock and Semaphore are used to guarantee thread-safe operations, which produce dependable and consistent results throughout all executions.
---

### Test 2: Exception Testing
**What I tested**: Checking for ConcurrentModificationException
I checked to see if the software threw any runtime errors relating to concurrency, such as ConcurrentModificationException.

**Testing procedure**: 
ran the application several times.
concentrated on executionLog (shared ArrayList) operations.
looked for any exceptions in the console output.

**Results**: 
During execution, no exceptions were made. Every time, the application operated without a hitch.

**What this proves**: 
This demonstrates that ReentrantLock is appropriately used to safeguard the shared resource executionLog.
Concurrent changes without synchronization may result in errors because ArrayList is not thread-safe.
The lack of mistakes attests to the proper implementation of synchronization.
---

### Test 3: Correctness Verification
**What I tested**: Verifying correct final values (total burst time, context switches, etc.)
I confirmed that all computed data and final statistics are accurate.

**Expected values**: 
Total number of processes created = total number of processes completed
Waiting time overall ≥ 0
Count of context switches > 0
Every process execution is recorded in the execution log.
**Actual values**: 
Total Context Switches: 38
Total Completed Processes: 17
Total Waiting Time: 1487333ms
Average Waiting Time: 87490ms

**Analysis**: 
The outcomes verify that the scheduler operates as intended.
The fact that all shared variables were correctly updated shows that synchronization was effective in avoiding race situations.
The behavior is consistent with what a Round Robin scheduling simulation would provide.
---

### Test 4: Different Scenarios
**Scenario tested**: [e.g., different time quantum, more processes, etc.]
Various methods (randomized using student ID)
Various time quantum values
RunToCompletion() is used to execute the final process.
**Purpose**: 
To guarantee that the synchronization logic functions properly in all workloads and scheduling scenarios

**Results**: 
All variants were handled flawlessly by the application.
There were no deadlocks; CPU access was appropriately restricted to one process at a time using the semaphore; output was accurate and consistent in every situation.

**What I learned**: 
I discovered that sustaining correctness in concurrent systems requires synchronization techniques.
Appropriate synchronization guarantees stability and stops unexpected behavior even when circumstances change (additional processes or changing timing).
---

## Part 5: Reflection and Learning

### What I learned about synchronization:
[6-8 sentences about key concepts, challenges, insights]

When several threads share resources, synchronization is crucial. Inadequate synchronization may result in race conditions and inaccurate outcomes.
I gained knowledge on how to guarantee mutual exclusion and safeguard important areas using ReentrantLock.
I also learnt how to manage access to scarce resources, such as CPU, using semaphores.
The fact that even basic actions, like increasing a counter, are not thread-safe was a crucial realization.
Another important idea is that, in order to avoid deadlocks, locks must always be released using finally blocks.
I also realized how crucial it is to carefully plan synchronization in order to strike a balance between performance and safety.
All things considered, synchronization is essential to creating dependable multithreaded applications.
---

### Real-world applications:

Give TWO examples where synchronization is critical:

**Example 1**: 
banking systems that allow several users to concurrently view and modify account balances. Synchronization guarantees accurate transaction processing without data loss.
**Example 2**: 
operating systems in which a number of processes share memory and CPU resources. Synchronization avoids conflicts and guarantees appropriate scheduling.
---

### How I would explain synchronization to others:

[Explain to someone who just finished Assignment 1 - use simple terms and analogies]

Organizing access to a shared resource is similar to synchronization.
Consider several people attempting to use the same printer simultaneously. They could get in the way of one another if there were no restrictions.
When a lock is used, only one person can use it at a time, much like when you give someone the key to the printer room.
A semaphore is similar to letting only a certain number of people enter a space.
This guarantees that there are no problems or disputes and that everything runs smoothly.
---

## Part 6: GitHub Repository Information

**Repository URL**: 

**Number of commits**: 

**Commit messages**: 
1. 
2. 
3. 
4. 

---

## Summary

**Total time spent on assignment**: 

**Key takeaways**: 
1. 
2. 
3. 

**Most challenging aspect**: 

**What I'm most proud of**: 

---

**End of Documentation**
