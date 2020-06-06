# zookeeper-api-introduction

#What we learn in this Lecture 
1. Fault Tolerant Leader Election Implementation
2. Inject Failures and test our cluster


#Example 1

high-level picture of what we're trying to accomplish let's assume that we have used the leader election algorithm to 
choose a special node in our cluster that cluster can be a compute cluster which receives computational tasks 
and those big tasks are then broken into multiple parallel subtasks and then distributed by the master node in an efficient way the
results are then a synchronously stored in a separate location where the leader either collects them and 
sends them back to the source or aggregates them and sends them to another compute cluster down the pipeline if the master crashes
or becomes temporarily unavailable before it collected the results all that hard computational work that the entire cluster has performed is potentially
lost and that's because only the leader knows how to aggregate it and where to send it later.


#Example 2
Another example where a master workers architecture is often used is in distributed databases on a large scale with millions of users and
billions of records the data is too big to fit on one machine so it is distributed across the cluster the leader then knows where each piece of
data is stored and how to reroute read and write requests to the appropriate charts of the data and in this case as well if the leader becomes unavailable
for even a fraction of a second all our data becomes inaccessible to everybody.
 

#Conclusion 

so in order for our system that we build on top of the master workers
architecture be fault tolerant and available we need our leader election algorithm to be fault tolerant as well it needs to automatically detect and
recover from failures by reelecting a new leader