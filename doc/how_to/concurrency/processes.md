# Launch multiple processes

Launching a Panel application on multiple processes is effectively a simpler way to scale your application. One major advantage is that it is easy to set up, when deploying your application with `panel serve` simply configure `--num-procs N`, where N is the number of processes. Generally choose an `N` that is no larger than the number of processors on your machine.

The main limitation is that the underlying Tornado multi-process mode does not balance connections across processes. Rather, any incoming connection will be assigned to the first server process that accepts it. Typically any idle process can get a new client regardless of how many clients it already has. In general the resulting distribution of clients across processes will be unequal. Moreover, this still uses significantly more resources since each process has the same overhead and all processes will be contending for the same memory and compute resources. However if your application is single-threaded and you have sufficient memory this is a simple way to make your application scale.