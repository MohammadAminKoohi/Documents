
2025-11-15 16:43

Tags: #Course_Operating_Systems


## Short-Term Scheduler
selects processes that are in ready queue and allocates one of them to CPU

CPU Scheduling decisions can take place on different scenarios like:
- Switches from running to waiting state
- Switches from running to ready state
- Switches from waiting to ready state
- Terminates


#### Non-preemptive Scheduling
- Scheduling only under case 1 and 4 (running to waiting, Termination)
- aka, cooperating scheduling
- Used in Windows 3.x

when we call the process in case 1 or 4 we had nothing to do with the process previously.

## Scheduling Criteria
- **CPU Utilization**: keep CPU as busy as possible
- **Throughput**: number of processes that complete their execution per time unit
- **Turnaround Time**: amount of time to execute a particular process
- **Waiting Time**: amount of time a process has been waiting in ready queue
- **Response Time**: amount of time it takes from when a request was submitted until its first response is produced, not output.
	for example when you click on an application and you are waiting for response

improving one criteria doesn't usually mean improving others.

different use cases require different **optimization**.
for example for Minimize Response Time, We might need to optimize its _Average_, _Maximum_ or _Variance_.

# Scheduling Algorithms

## First-Come, First-Served(FCFS)
if processes arrive in order: P1, P2 and P3, they will be scheduled like:
P1 -> P2 -> P3

**FCFS**: non-preemptive -> not suited for time-sharing or real-time systems
## Shortest-Job-First
Associate with each Process Length of its Next CPU Burst
It uses these lengths to schedule process with shortest time.

**SFJ** is optimal. It gives _minimum average waiting time_ for a given set of processes.
- Difficulty is knowing length of **Next CPU Request**
- Possible Starvation, why?
	because of the scenario of spamming short processes before the main process

## Shortest-remaining-time-first
every time a new process comes, it compares it to the previous processes and choose the one with the shortest remaining bust time.


# Priority Scheduling

in this method, a priority number is associated with each Process and CPU will be allocated to the process with Highest Priority. (smallest integer = highest priority)

**SFJ** is Priority Scheduling where our priority is Inverse of Predicted next CPU Burst Time.

*Problem?* **Starvation**, low priority processes may never execute.
*Solution?* **Aging**, as time progresses increase process priority. with this method, every process will get its chance to execute after a certain time.

### Round Robin (RR)
Each Process Gets a Small Unit of CPU Time (time quantum q)
- Usually 10-100 milliSeconds Units of Time
- After the time has ended, process is added to end of ready queue

for example if there are n processes in ready queue and our quantum time is q, each process gets 1/n of q.

Time Interrupts every Quantum to Schedule next Process.???

#### performance
- q very large -> FIFO(FCFS)
- q small -> q must be large with respect to context switch, otherwise overhead is too high


##### **RULE OF THUMB:**
 80% of CPU Bursts should be shorter than q.
 _why?_


## Multilevel Queue
Processes can be classified into Different Groups. Processes have different response time requirements -> different scheduling needs

ready queue is partitioned into 2 queue:
- Foreground
- Background

for examples for processes that are interactive and need constant cpu times, we use **Round Robin** or for scenarios when we need batch or heavy processes we can use **FCFS**.


A process can move between queues. **Aging** can be implemented this way.


### What is the priority of the Schduler
Scheduler is called after a process is finished. when the timer ticks for a process, it will first start looking for interrupts and will handle them and when there is none, it will give the cpu back to the scheduler.


## Multiple-Processor Scheduling


### Asymetric MultiProcessing
a single core is in charge of making all scheduling, IO and ... decisions for all other cores.

### Symmetric MultiProcessing
Each Processor is self-scheduling
all process in comon ready queue or each


## Processor Affinity
Process has affinity for processor on which it is currently running.

**Why Have Affinity?** 
Because Process Migrations are very **costly**. each Process has its own **Cache**. so we need to move them to another process's cache.
- Cache _invalidation_ in source processor
- Cache _repopulation_ in destination processor

### Types of Affinity

