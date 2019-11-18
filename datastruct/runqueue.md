# Run Queue

In modern OS, processes are placed into __runqueue__. The runqueue may contains priority values for each process, which will be used by the scheduler to determine which process to run next.

In Linux, each CPU in the system is given a runqueue. Each runqueue maintains both an active and expired array of processes. Each such array contains 140 (one for each priority level) pointers to doubly linked lists. These doubly linked lists reference all processes with the given priority.