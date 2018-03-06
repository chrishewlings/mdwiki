##Definitions:

- **Process** : abstract environment for program execution
    + Gets own address space, FDs, registers, etc.
- **Thread** : lightweight unit of execution
    + Shares address space, code, data with process. Gets its own register and stack.
- **Protection**: ensuring the **reliability** of the system
- **Security**: ensuring the **coherency and integrity** of the system

## Stack:

- Apps
- System
- OS
- Hardware

## OS Categories:

- Multiprogrammed Batch:
    - Multiple jobs in memory, managed by 'resident monitor'
    - Jobs interrupted by blocking IO
- Time Sharing:
    - Fixed time quantum
    - Interrupted users wait in queue
- Client-Server:
    - Information sharing between client/server
- Multiprocessing:
    - SMP: Each core executes kernel
    - AMP: One core executes kernel, others are slaved to it
- Distributed:
    - Balances load between similar systems
- Personal
- Real time:
    - Hard RT: fail if time deadline not met
    - Soft RT: Proceeds even if deadline expired

## OS Structures:

- **Layered**: 
    + Each layer requests services only from lower levels
- **Monolithic**:
    + OS procedures in single executable module
    + No protection, encapsulation
- **Microkernel**:
    + More stable, more secure, faster
- **Hybrid**

## Processes

### Process Lifecycle:

- New process is **admitted** to **ready** queue.
- If scheduler selects process, it's **dispatched** to **running** state.
- From **running** state:
    - **Interrupted**: returns to **ready**
    - **IO blocking**: goes to **waiting**
- From **waiting** state: returns to **ready** when IO completes.
- Finally, **running** -> **terminated** 

### Process Relationships:

- **Hierarchical** : 
    + May communicate
    + Parents control execution
    + Children share some resources
- **Independence** :
    + Can't communicate
    + Don't share resources
- **Cooperation** :
    + Share resources
    + Can communicate

### Unix processes:
- **Zombie** : terminated child proc waiting for parent to respond

### Windows processes:
- **Executive** : handles objects, io, security, etc.
- States are divided into *runnable*/*not runnable*


## Threads:

- **User threads**: fast switching, no parallelism
- **Kernel threads**: slow switching, real parallelism

### User threads to kernel threads:

- **Many to one**: 
    + many user --> one kernel.
    + No parallelism.
    + Blocked thread -> blocked process
- **One to one**: 
    + one user -> one kernel.
    + Blocked thread -> process continues.
    + Parallelism.
- **Many to Many**:
    + Good shit.

## Scheduling

- **Short term** : All the main stuff
- **Med term**: Swap in/out processes from main memorry
- **Long term**: Select processes to be admitted and moved to ready

### Non-Preemptive

- FCFS:
    - Long avg waiting time
- Shortest job first:
    - Minimal avg wait time
- External Priority:
    - Low priority processes might block a long time
- Deadline:
    - Good for RT. Guaranteed waiting time before execution.

### Preemptive

- RR:
    - *Long time*: High wait, low TAT
    - *Short time*: Low wait, high TAT
- Shortest remaining time:
    - Avg wait time minimal
    - For avg: (Sum (start_time - arrival_time))/n
- Internal priority: 
    - Priority recalculated at interval
- Multilevel queues:
    - method 1: priority queues
    - method 2: each queue gets a timeslice
    - method 3: multilevel feedback 

### Equations:

next service time = (last cpu weight)(last cpu time) + (1-last cpu weight)(avc svc time)  
quantum = ((intvl - (numProc)(switchTime))/numProc  

## Synchronization

### Critical Section

A solution to critical section problem must satisfy:

1. **Mutual exclusion**: If process P is executing critical section, no other process can be executing their critical sections.
2. **Progress**: If no process is executing its CS and some wish to enter their CS, only those that are not executing in their remainder sections can participate in deciding which will enter its critical section next.
3. **Bounded waiting**: There exists an upper bound on the number of times that other processes are allowed to enter their CS after a process has made a request to enter it (and before that request is granted).

### Deadlock

Four conditions:

1. Mutex: Resources cannot be shared 
2. Hold+Wait: Process is holding resources and requesting resources held by other process
3. No preemption: Resource can only be released voluntarily
4. Circular wait: Each process is waiting for the next one to release resources

### Dekker's Algorithm

#### PROS:
- No special hardware required
- Guarantees:
    - Mutual exclusion
    - No deadlock
    - No starvation

#### CONS:
- Only works for two processes
- Causes busy waiting, wasting cpu time
- Doesn't work on SMP

#### Implementation:

- Uses two booleans to indicate whether process wants to enter CS.
- Uses a 'token' to indicate priority if both are equal at same time

```c
bool goT1, goT2 = {false, false}
int token = 1;

//T1

do {
    goT1 = true;

    //wait until t2 wants to enter CS
    while(goT2 == true) {

        // Check if other thread has priority
        if(token == 2) {
            goT1 = false;
        }

        // Wait until our thread is picked

        while(token == 2);

        goT1 = true;
    }

    // Critical Section //

    // change priority
    token = 2;

    // indicate t1 has completed CS
    goT1 = false;

} while(completed == false);

//T2

do {
    goT2 = true;

    //wait until t1 wants to enter CS
    while(goT1 == true) {

        // Check if other thread has priority
        // if so, stop trying until it swaps
        if(token == 1) {
            goT2 = false;
        }

        // Wait until our thread is picked

        while(token == 1);

        goT2 = true;
    }

    // Critical Section //

    // change priority
    token = 1;

    // indicate t2 has completed CS
    goT2 = false;

} while(completed == false);
```

### Peterson's Algorithm

#### PROS:
- Can be adapted for 2+ processes  

#### Implementation:

- Uses two variables:
    - `interested[]`: `interested[n] == true` means `n` wants to enter CS.
    - `turn`: indicates with process has priority

- n.b. for 2+ processes, uses an integer variable per process, and n-1 additional variables

```c
int turn; 
int interested[2];

void enter_region(int process) {
    int other;

    other = 1 - process;
    interested[process] = TRUE;
    turn = process;
    while(turn == process && interested[other] == TRUE);
}

void exit_region() {
    interested[process] = FALSE;
}
```

#### Proof

- Mutex? **Y**. If both processes could execute CS at the same time, it would mean the value of `turn` was both 0 and 1, which makes no sense
- P_i doesn't change the value of `turn` while executing `while`, so P_i will enter the CS (progress) after at more one entry by P_j (bounded waiting).

### Semaphores - Readers and Writers

#### Problem:

- Readers and writers share a file
- If a reader is reading: no other process may write
- If a writer is writing: no other process may read, and no other processes may write. 

#### Solution 1: Prioritize Readers

```c
semaphore mutex;   // ensures readcnt is updated properly
sempahore wrt;     // protects critical section

int readcnt;       // how many readers are reading

/* WRITER */

do {
    // Wait until allowed
    wrt.wait();

    /* CRITICAL SECTION */
        // Do write //
    /* END CRITICAL SECTION */

    // Allow others to continue
    wrt.signal();
} while(true);

/* READER */

do {

    // Request entry
    mutex.wait();

    // Increment to indicate there's a reader in CS.
    readcnt++;

    // As long as there is >=1 reader, need to block writers.
    if(readcnt == 1)
        wrt.wait();

    // However, other readers are free to enter
    mutex.signal();

        // Do reading //

    //Decrement once read is done.
    readcnt--;

    //If we're the last one, hand over execution to writers.
    if(readcnt == 0) 
        wrt.signal();

    mutex.signal(); // indicate we're leaving
} while(true);
```

### Semaphores - Producers and Consumers

- Two processes share a common buffer
- If buffer full: producer can't add to buffer
- If buffer empty: consumer can't read from buffer

```c
#define BUF_SIZE 100

semaphore mutex = 1;            // control access to CS
semaphore empty = BUF_SIZE      // counts empty buffer slots
semaphore full = 0;

void producer(void) {
    int item;

    while(TRUE) {
        item = produce_item();  // generate something to put in buffer
        empty.wait();           // decrement empty count, stall if no empty
        mutex.wait();           // enter CS
            insert_item(item);
        mutex.signal();         // exit CS;
        empty.signal();         // increment full slot count
    }
}

void consumer(void) {
    int item;

    while(TRUE) {
        full.wait();            // decrement full count, stall if no items in buffer
        mutex.wait();           // Enter CS
            item = remove_item();   
        mutex.signal();         // exit CS
        empty.signal();         // increment empty slot count
        consume_item(item);
    }
}
```


### Semaphores - Dining philosophers

#### Problem:

- 5 around a table, who can eat or wait
- to eat: a chopstick on left and right required
- 1 chopstick can be picked up by any one of its adjacent followers but not both
- Circular table: think modular arithmetic.

#### Implementation - Single semaphore:

```c

wait(mutex);
take_fork();
eat();
put_down_fork();
signal(mutex);
```

- The problem with this is that only one philosopher can eat at a time. 

#### Implementation - One semaphore per philosopher

- Defines three states: thinking, hungry, eating

```c
#define N 5
#define LEFT (1+N-1)%N   // left neighbour
#define RIGHT (1+N-1)%N  // right neighbour

#define THINKING 0
#define HUNGRY 1         // wants forks
#define EATING 2         // has forks

int state[N];            // Keeps track of everyone's state
semaphore mutex = 1;     // Controls critical region
semaphore s[N];

void philosopher(int i) {
    while(TRUE) {
        think();
        take_forks(i);   // take two forks, or block.
        eat();
        put_forks(i);
    }
}

void take_forks(int i) {
    wait(mutex);        // enter CS
    state[i];           // indicate hunger
    test(i);            // try to acquire two forks
    signal(mutex);      // exit CS
    wait(s[i]);         // go from hungry-> eating, or block if forks were not acquired
}

void put_forks(int i) {
    wait(mutex);        // enter CS
    state[i] = THINKING;// indicate eating has finished
    test(LEFT);
    test(RIGHT);        // can neighbours eat?
    signal(mutex);
}

void test(int i) {
    if(  state[i] == HUNGRY &&
         state[LEFT] != EATING &&
         state[RIGHT] != EATING) {
            state[i] = EATING;
            signal(s[i]);
         }
}
```

## Monitors

### Monitors - Producer/Consumer problem

- Only one process can be active in a monitor at any instant
    + `signal` statement may only be the final statement in a monitor procedure
- Easy in Java - use `synchronized` keyword 
- They make the mutual exclusion of critical regions automatic


```c
monitor ProducerConsumer 
{
    int itemCount = 0;
    condition full;
    condition empty;

    procedure add(item) 
    {
        if (itemCount == BUFFER_SIZE) 
        {
            wait(full);
        }

        putItemIntoBuffer(item);
        itemCount = itemCount + 1;

        if (itemCount == 1) 
        {
            notify(empty);
        }
    }

    procedure remove() 
    {
        if (itemCount == 0) 
        {
            wait(empty);
        }

        item = removeItemFromBuffer();
        itemCount = itemCount - 1;

        if (itemCount == BUFFER_SIZE - 1) 
        {
            notify(full);
        }


        return item;
    }
}

procedure producer() 
{
    while (true) 
    {
        item = produceItem();
        ProducerConsumer.add(item);
    }
}

procedure consumer() 
{
    while (true) 
    {
        item = ProducerConsumer.remove();
        consumeItem(item);
    }
}
```

## Random


- threads in user space : each process needs a thread table

- Compute bound processes have long CPU bursts, infrequent IO waits
- IO bound processes have short CPU bursts, frequent IO waits

- Throughput is numJobs/time


Simple design           ->  Layered
Efficient performance   ->  Monolithic
Security                ->  Micro-kernel
Extensibility           ->  Modular structure 

- user threads vs kernel threads:
    - when kernel thread blocks, other app threads can continue
    - kernel threads usually have larger time quantum
    - combined threads : 
        - managed mostly in user space, better performance
        - dispatched mostly in kernel, better concurrency

- Multiprogramming: multiple programs in memory for later execution
- Multitasking: multiple programs in memory for concurrent execution

- SMP > AMP, bc jobs can be blocked waiting for the master system to dispatch them.
- Other registers must be restored before PC, because once PC is restored process gets execution control and dispatcher can't do anything more

- mutex is violated if process executes in CS something thats not related to CS stuff. 
- getting value of semaphore isn't atomic and should not be done