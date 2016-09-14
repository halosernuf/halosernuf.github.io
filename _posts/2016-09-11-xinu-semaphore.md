---
layout: post
title: "Xinu Semaphore & Mutex"
date: 2016-09-11 08:29:10
---

## Xinu Semaphore API

* each semaphore has a count:
  * initial count when created
  * current count during use(held in a kernel var)
* sid32 semid = semcreate(int inicount); //Xinu syscall
* sid32 wait(semid): decrement sem’s count, blocks the callers(caller waits) if new count < 0 a process “blocks”(only happens via OS action) meaning it waits without using CPU(OS runs other process)
* sid32 signal(semid): increment sem’s count, allow one blocked process to run (if any waiters)
* sid32 count = semcount(semid): get semaphore’s current count
* sid32 status = delete(semid)

## Mutex is easy

* sid32 mutex = semcreate(1)
* sid32 wait(mutex) //acquire lock
* sid32 signal(mutex) //release lock

[<img src="images/xinu/mutex.png">](images/xinu/mutex.png)

## Producer & consumer example

```c
/* prodcons.c - main, prod2, cons2, with N spots in shared buffer  */
#include <stdio.h>
#define N 10
/* Note that this simple queue is meant to be used with semaphores--
 * on its own, it doesn't know if it's empty or full!  Both cases
 * have head == tail.  One semaphore is enough to keep track of this.
 * Two semaphores are needed for control of both producer and consumer.
 */
int a[N];  /* shared buffer */
int head, tail; /* for buffer used as queue */
void prod2(int consumed, int produced, int mutex);
void cons2(int consumed, int produced, int mutex);
 
/*--------------------------------------------------------------------------
 *    main --  producer and consumer process synchronized with semaphores
 *--------------------------------------------------------------------------
*/
void main(void)
{
  int produced, consumed, mutex;
 
  consumed = screate(N);        /* scount = number of empty spots in buffer */
  produced = screate(0);        /* scount = number of filled spots in buffer */
  mutex = screate(1);
  head = tail = 0;              /* initialize buffer as queue */
  resume( create(cons2, 1000, 20, "cons", 3, consumed, produced, mutex));
  resume( create(prod2, 1000, 20, "prod", 3, consumed, produced, mutex));
}
 
/*----------------------------------------------------------------------------
 *    prod2   --  increment n 200 times, waiting for space in buffer
 *----------------------------------------------------------------------------
 */
void prod2(int consumed, int produced, int mutex)
{
    int i, n = 0;
 
    for( i=1; i<=200; i++ )  {
        wait(consumed);
        n++;                    /* "produce" another number */
        wait(mutex);
        a[head++] = n;          /* enqueue(n) */
        if (head >= N)          /* ... */
            head = 0;           /* ... */
        signal(mutex);
        signal(produced);
    }
}
 
/*----------------------------------------------------------------------------
 *  cons2 -- print 200 times, waiting as needed for some numbers to be produced
 *----------------------------------------------------------------------------
 */
void cons2(int consumed, int produced, int mutex)
{
    int i, n;
 
    for( i=1;  i<=200; i++ )  {
        wait(produced);
        wait(mutex);
        n = a[tail++];          /* n = dequeue() */
        if (tail >= N)          /* ... */
            tail = 0;           /* ... */
        signal(mutex);
        printf("number consumed is %d \n",  n);
        signal(consumed);
    }
}
```