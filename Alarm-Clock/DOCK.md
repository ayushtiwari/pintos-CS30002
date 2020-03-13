# Alarm Clock
## Requirements
Reimplement timer_sleep(), defined in devices/timer.c, avoiding busy wait.

## Preliminaries
None
## Data Structures
```C
struct thread {
  /* some stuff */
  
  struct list_elem waitelem;     /* To be stored in the waiting_list */
  int64_t sleep_endtick;         /* The tick after which the thread should awake (if the thread is in sleep) */
  
  /* more stuff */
};  
```
## Algorithms
```
timer_sleep (time_t x):
  Save waitelem to waiting_list
  Set current_thread->sleep_endtick to ( current_time + x )
  current_thread->status = BLOCKED
```
```
thread_tick (time_t x):
  /* do some stuff */
  traverse the waiting_queue and unblock all threads which have slept enough
```

## Synchronization
None
## Rationale
1. Changing thread status to blocked prevents it from scheduling.
2. thread_tick is timer interrupt driven
3. Threrefore, it will unblock threads periodically
