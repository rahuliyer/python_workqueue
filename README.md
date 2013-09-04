This is a simple workqueue implementation in python. The example below will explain how to use it. The example will use the workqueue to calculate the squares (or any exponent for that matter) of a list of numbers in parallel.

First, we create a processor for the job. The function below calculates the exponent of a given number and stores it in a supplied dictionary.
```
>>> def func(x, n, results):
...     results[x] = math.pow(x, n)
```

Now, we create the workqueue. _num_workers_ is the number of worker threads and _max_queue_size_ is how big the queue can grow. Once the max queue size is hit, the enqueuing thread is blocked until space is available. The remaining params are named params that are passed to the processor as is.
```
res = {}
>>> wq = WorkQueue(func, num_workers = 3, max_queue_size = 5, n = 2, results = res)
```

Adding items to the work queue is as simple as calling _add()_. _add()_ takes just one parameter which is passed to the processor function as the first argument.
```
>>> for i in range(1, 4):
...     wq.add(i)
```

To wait for the completion of all the tasks, call _done()_.
```
wq.done()
>>> res
{1: 1.0, 2: 4.0, 3: 9.0}
```

And that's it!
