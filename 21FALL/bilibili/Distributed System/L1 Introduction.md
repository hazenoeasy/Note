# Distributed System
- a set of cooperating computers that communicating with each other over networked to get some coherent task.
- examples: stroage for big websites or big data computations such as MapReduce.
# why people build it 
- parallelism lots of CPUs  disk arms
- tolerate faults
- phycial reasons
- security / isolated
# Challenges
- concurrency
- partical failure
- performance

# Infrustructure - Abstractions
- Storage 
- Communication
- computation
  
# Implementation Tools
- RPC remote procedure call
- Threads
- concurrency

# Performance
- Scalability  more resource more power 

# FAult Tolerance
- Availbility - keep running
- Recoverability - continue
  
# NV stroage
 advoiding writing NV too much.
 replicate

 # Consistency
 K / V   replication need to be consistent
 weak consistency  also work in some situation
 replicas need to be independed-> more time cost in communication

 # MapReduce -- google
 engineers could write code easily

 - MapReduce will run map function on each of input files.
 - output: a list takes a file as input ,key values.
 - example: 
    (GFS) input -> intermedia value -> output  