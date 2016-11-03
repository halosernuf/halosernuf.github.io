---
layout: post
title: "Atomic Operation in Multithread"
categories: Multithread
tags: atomic multithread
---
source: [http://www.parallellabs.com/2010/04/15/atomic-operation-in-multithreaded-application/](http://www.parallellabs.com/2010/04/15/atomic-operation-in-multithreaded-application/)

# Is the W/R operation in multithread enviroment ATOMIC?

take x86 as an example, according to Intel [Manuals](http://download.intel.com/design/processor/manuals/253668.pdf). Based on following three mechanism, the system gaurantee the atomic operations in multicore system

（1）Guaranteed atomic operations （detailde in 8.1.1）
（2）Bus locking, using the LOCK# signal and the LOCK instruction prefix
（3）Cache coherency protocols that ensure that atomic operations can be carried out on cached data structures (cache lock); this mechanism is present in the Pentium 4, Intel Xeon, and P6 family processors

## Guaranteed atomic operations

* Reading or writing a byte
* Reading or writing a word aligned on a 16-bit boundary
* Reading or writing a doubleword aligned on a 32-bit boundary

From Pentium processor
* Reading or writing a quadword aligned on a 64-bit boundary
* 16-bit accesses to uncached memory locations that fit within a 32-bit data bus
* Unaligned 16-, 32-, and 64-bit accesses to cached memory that fit within a cache line

## NOT atomic operations 

Accesses to cacheable memory that are split across bus widths, cache lines, and
page boundaries are not guaranteed to be atomic by the Intel Core 2 Duo, Intel®
Atom™, Intel Core Duo, Pentium M, Pentium 4, Intel Xeon, P6 family, Pentium, and Intel486 processors.