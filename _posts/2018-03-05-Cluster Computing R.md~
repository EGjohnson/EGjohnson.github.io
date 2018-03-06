
# Introduction
Instead of running an analysis sequentially, you can use multiple cores in parallel. In this example, I will be using multiple cores on my own computer to construct a cluster.

This type of code can be used for cores on the same node/computer. If you wish to use cores across different computers/nodes, then you should look into packages like Rmpi which will help you use a Message Passing Interfaces (MPI) to communicate across nodes.


We will use three wrapper functions that allow us to execute familiar R functions in parallel. These wrapper functions split the work and distribute it to the nodes equally.

We will look at wrappers for parallel implementations of:
* lapply()

* sapply()

* foreach()


# 1. Detecting Cores and Making a Socket Cluster

Include package *parallel*

```R
library(parallel)
```

We can check the number of cores we have to play with like this:

```R
> detectCores()
[1] 8
```

However, we do not want to use *all* of our cores, or we will crash the system.

```R
# Calculate the number of cores and substract 2
number_cores <- detectCores() - 2
```
Now that we know how many cores we are working with we can construct the cluster using *makeCluster* from the *parallel* package. 
If you have Mac/Unix system, use the option FORK (makeFORKcluster) when you construct your cluster. 
Forking only works on Mac/Unix systems but is preferred to the default option PSOCK (makePSOCKcluster).

Forking is preferred because:
  * all environmental variables are included (no manual export to cluster)

  * variables keep the same address (saves memory)

```R
# initiate cluster
my.cluster <- makeCluster(number_cores,type="FORK")
my.cluster
```
```
socket cluster with 6 nodes on host ‘localhost’
```

Remember to close the socket cluster.
```R
# stop cluster and release resources
  stopCluster(my.cluster)
```



# 2. Parallel Function Apply : parSapply() & parLapply()
* lapply --> parLapply (returns list ) 

* sapply --> parSapply (returns array)

The functions *lapply* and *sapply* let us iterate a function over values and returns a list or vector respectively. See below.

```R
b<-100
lapply(1:3, function(x) b+x)
sapply(1:3, function(x) b+x)
```
```
[[1]]
[1] 101

[[2]]
[1] 102

[[3]]
[1] 103

[1] 101 102 103
```

We can distribute the work done over several cores by using their parallel equivalents like so below:

```R

# cluster will only be able to see the variable below if it was Forked. 
# otherwise need to pass it to the cluster
b<-100

# create a cluster using 6 of my computer cores FORK in environmental variables
my.cluster <- makeCluster(number_cores,type="FORK")

# use parralel version of lapply (return list)
my.list<-parLapply(my.cluster, 1:5,function(x) x+b)

#use parallel version of sapply (return array)
my.vector<-parSapply(my.cluster,1:5,function(x) x+b)

# stop cluster and release resources
stopCluster(my.cluster)

print("my.list")
print(my.list)
print("my.vector")
print(my.vector)

```

```
[1] "my.list"
[[1]]
[1] 101

[[2]]
[1] 102

[[3]]
[1] 103

[[4]]
[1] 104

[[5]]
[1] 105

[1] "my.vector"
[1] 101 102 103 104 105

```

What are these wrapper functions actually doing? They are splitting the vector fed to them evenly over the cores and running the function on them, then returning and combining the results. See the workings of the wrapper function *lapply* and *sapply* below. 

```R
> parLapply

function (cl = NULL, X, fun, ...) 
{
    cl <- defaultCluster(cl)
    do.call(c, clusterApply(cl, x = splitList(X, length(cl)), 
        fun = lapply, fun, ...), quote = TRUE)
}
```

```R
> parSapply
function (cl = NULL, X, FUN, ..., simplify = TRUE, USE.NAMES = TRUE) 
{
    FUN <- match.fun(FUN)
    answer <- parLapply(cl, X = as.list(X), fun = FUN, ...)
    if (USE.NAMES && is.character(X) && is.null(names(answer))) 
        names(answer) <- X
    if (!identical(simplify, FALSE) && length(answer)) 
        simplify2array(answer, higher = (simplify == "array"))
    else answer
}

```
Notice that *parSapply* is just a fancy version of *parLapply*. The wrapper *parLapply*, in turn, is just a function that invokes *clusterApply* in a smarter way.


# 3. Parallel Looping: foreach()

* additionally needs: library(foreach), library(doParallel)

* Looping construct for executing R code repeatedly

* supports parallel execution

* Note: cluster needs to be registered with registerDoParallel

```r
library(foreach)
library(Smisc)
library(doParallel)
library(iterators)
```
Without parallization, *foreach()* functions like so:
```r
# multiple ... arguments
the.funct<- function(i,j,k){i+j*k}
foreach(i=1:4, j=4:8,k=9:12) %do% the.funct(i,j,k)
```

```
[[1]]
[1] 37

[[2]]
[1] 52

[[3]]
[1] 69

[[4]]
[1] 88


```

What makes foreach() special is that it offers an option that allows you to choose how you want to combine the results. We will also add a *timeIt()* function from the *Smisc()* package to see how long this sequential implementation of *foreach()* takes.

```r
# with combine argument
the.funct<- function(i,j,k){i+j*k}
timeIt(seq.output<-foreach(i=1:4, j=4:8,k=9:12,.combine=c) %do% the.funct(i,j,k))
print(seq.output)
```
```
0.01 seconds 
[1] 37 52 69 88
```
The output is combined into a nice vector. This took 0.01 seconds.

The process for running *foreach()* in parallel involves one more step than the previous wrappers. You need to register your cluster with the function *registerDoParallel()*, so that you can use the operator *%do%* in parallel.


```r
#set up cluster: only fork on non-windows
my.cluster<-makeCluster(number_cores,type="FORK")
#register mycluster for operator %dopar%
registerDoParallel(my.cluster)
#run iteration over clusters
foreach(i=1:4,j=4:8,k=8:12,.combine = c)  %dopar%  the.funct(i,j,k)
# stop cluster and release resources
stopCluster(my.cluster)
```

```
0.01 seconds 
[1] 33 47 63 81
```
Hey, wait! Why wasn't this any faster?

# When to use R in parallel
Parallel jobs are not always faster if the data set is small, as in the above toy examples. What you need to remember is running jobs in parallel incurs overhead, the data needs to be distributed, workers need to receive instructions, and then all the output needs to be recombined. The performance of your program will only improve if your job takes a long time to run sequentially. 






 
