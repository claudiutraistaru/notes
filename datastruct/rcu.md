# RCU(Read-Copy-Update)

[source](https://www.kernel.org/doc/Documentation/RCU/whatisRCU.txt)
This data structure is mainly used with read-often data.

## RCU update sequence

1. Remove pointers to a data structure, so that subsequent readers cannot gain a reference to it.
2. Wait for all previous readers to complete their RCU read-side critical sections.
3. At this point, there cannt be any readers who hold references to the data structure, so it now may safely be reclaimed.

## Core RCU API:

1. void rcu_read_lock(void)
2. void rcu_read_unlock(void)
3. void synchronize_rcu(void)/ call_rcu()
4. void rcu_assign_pointer(p, typeof(p) v); macro
5. typeof(p) rcu_dereference(p); macro