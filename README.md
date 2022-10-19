The reason why promises are glorified in the javascript community as a way to do "asynchronous non-blocking operations" is
because they are good at doing jobs that take more time, but not more CPU power. 
By "doing jobs that take more time" I meant jobs like talking to a database, talking to another server, etc which is 99% of what web servers do. 
These jobs are not immediate and will take relatively more time.
Javascript promises accomplish this by pushing the job to a special queue and listening for an event (like a database has returned with data) to happen and 
do a function (often referred to as a "callback function") when that event has happened



node only uses a single core of your CPU no matter how many cores you have.


3 solutions
 childprocess -exec execfile spawn fork
 cluster   
 worker 

Child Process

Make use also of different cores available, but its bad since it costs huge amount of resources to fork a child process since it creates virtual memory.

Forked processes could communicate with the master thread through events and vice versa, but there is no communication between forked processes.

1.exec

exec use for small output and commands in same file          find won't work since it uses buffer

2.excefile

excefile use for small output and commands in differmemt file      find won't worksince it uses buffer

3.spawn
spawn use for larger output because it uses stream instead of single buffer

4.
fork is an instance of worker or which will create a worker process by using cluster module
cluster.fork will create a many instances as per our system depends on number of core





Using fork(), we can solve the problem discussed above by forking a separate nodejs process and executing the function in that process and 
return the answer to the parent process whenever it is done. In that way, the parent process won't be blocked and can continue responding to requests.

fork disadvantage
Separate memory is allocated for each child process which means that there is a time and resource overhead.





Cluster

cluster is like a child process module pm2
Cluster is mainly used for vertically (adding more power to your existing machine) scale your nodejs web server. 
It is built on top of the child_process module. In an Http server, the cluster module uses child_process.fork() to automatically fork processes and 
sets up a master-slave architecture where the parent process distributes the incoming request to the child processes in a round-robin fashion. 
Ideally, the number of processes forked should be equal to the number of cpu cores your machine has.



Built on top of Child_process, but with TCP distributed between clusters.
Best for distributing/balancing incoming http requests, while bad for cpu intensive tasks.
Works by taking advantage of available cores in cpu, by cloning nodeJS webserver instances on other cores.




Worker thread

Worker thread is a continuous parallel thread that runs and accepts messages until the time it is explicitly closed or terminated
we will use workers for more cpu intensive task not for i/o operations

Same as child process, but forked processes can communicate with each other using bufferArray




difference between fork and worker
fork() in child-process spawns out a separate NodeJs process, 
the worker_threads creates a new thread in the existing NodeJs process with a separate event loop


https://youtu.be/9RLeLngtQ3A
https://alvinlal.netlify.app/blog/single-thread-vs-child-process-vs-worker-threads-vs-cluster-in-nodejs
https://livecodestream.dev/post/how-to-work-with-worker-threads-in-nodejs/
https://spectrumstutz.com/nodejs/nodejs-child-process-worker-threads/
https://blog.appsignal.com/2021/02/03/improving-node-application-performance-with-clustering.html


