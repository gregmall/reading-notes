# Redis
* **Remote Dictionary Server**
- All data resides in-memory in contrast with that of databases which store data on disk or ssd.
    - avoids seek time
* Redis Vs Memcached
- Memcached is designed for simplicity
- Redis offers rich set of features for wide range of use cases. 
* Benefits of Redis
- In-memory data store
    - data resides in servers main memory
    - supports more operations and faster response time
- Flexible data structures
    - Strings - text or binary data up to 512 MB 
    - Lists - a collection of Strings in the order they were added
    - Sets- an unordered collection of strings with the ability to intersect, union, and diff other Set types
    - Sorted Sets - Sets ordered by a value
    - Hashes - a data structure for storing a list of fields and values
    - Bitmaps - a data type that offers bit level operations
    - HyperLogLogs - a probabilistic data structure to estimate the unique items in a data set
- Simplicity and ease-of-use
    - enables user to write fewer lines of code 
    - comes with native data structures and many options to manipulate and interact with data
- Replication and persistence
    - supports asynchronous replication 
    - supports point-in-time backups
- High availability and scalability
    - allows user to build highly available solutions providing consistent performance and reliability
- Extensibility
    - open source
    - no vendor or technology lock
* Popular Redis Use cases
- Caching
    - decreases data access latency
    - easily scale for higher loads without growing the back end
- Chat, messaging, and queues
    - supports chat rooms, comment streams, social media feeds and server intercommunication
    - easy to implement lightweight queue
- Gaming leader boards
    - real time ranked list
- Session store
    - sub-millisecond latency, scale and resiliency
- Rich media streaming
    - fast in-memory data store to power live streaming use cases
- Geospatial
    - add location-based features such as drive time, drive distance and points of interest on applications
- Machine Learning
    - fast in-memory data store to build, train and deploy machine learning models
- Real-time analytics
    - real0time analytics use cases such as social media analytics, ad targeting, personalization and IoT.

# Queue
* places elements in a sequence.
    - FIFO - first in first out: first element that is enqueued will be the first one dequeued.
* Basic operations of a queue
- Enqueue() - inserts an element to the end of the queue
- Dequeue() - Removes an element from the start of the queue
- isEmpty() = Returns true if the queue is empty
- Top() - Returns the first element of the queue

# Task queues Overview

* Basically, tasks can be prioritized. Information about the tasks to be performed can be stored in the queue along with the task to be worked on. 

# Task queues FIFO
* First in, first out
    - handles queues in the order that they arrive: first to arrive is the first to be worked upon
    - there is a complicated example in the reading.  Link follows: [FIFO](https://redislabs.com/ebook/part-2-core-concepts/chapter-6-application-components-in-redis/6-4-task-queues/6-4-1-first-in-first-out-queues/)                                                               

# Bull Quickstart
* Bull is a Node library that implements a fast and robust queue system based on redis

* **Getting Started**
```
$ npm instal bull --save
```

## **Simple Queues**
- Queue instance can have 3 main different roles:
    - job producer
    - job consumer
    - events listener

- **Producer**
    - a Node program that adds a job to the queue
    - example:
```
const myFirstQueue = new Bull('my-first-queue');

const job = await myFirstQueue.add({
  foo: 'bar'
});
```
- **Consumer**
    - consumer (or worker) is a Node program that defines a process
    - example:
```
const myFirstQueue = new Bull('my-first-queue');

myFirstQueue.process(async (job) => {
  return doSomething(job.data);
});

```
 - process function will be called every time the worker is idling and there are jobs to process in the queue
 - process will be kept busy processing jobs one by one until all of them are done
 - providing progress information to an external listener can be accomplished by using progress method on the job object:
 - example:
```
myFirstQueue.process( async (job) => {
  let progress = 0;
  for(i = 0; i < 100; i++){
    await doSomething(job.data);
    progress += 10;
    job.progress(progress);
  }
});
```
* **Listeners**
    - just listen to event that happen in the queue
    - can attach listener to any instance
    - example:
```
myFirstQueue.process( async (job) => {
  let progress = 0;
  for(i = 0; i < 100; i++){
    await doSomething(job.data);
    progress += 10;
    job.progress(progress);
  }
});
```
* **A Job's Lifecycle**

![job lifecycle image](/assets/job-lifecycle.png)

* **Stalled jobs**
    - a job that is being processed but where Bull suspects that the process function has hanged.
    - this happens then the process function is processing a job and is keeping the CPU so busy that the worker in not able to tell the queue that it is still working on the job.
    - can be retried by another idle worker or can be moved to the failed status

## **Events**
* Events can be local for a given queue or can be global
- local:
```
queue.on('completed', job => {
  console.log(`Job with id ${job.id} has been completed`);
})
```
- global:
```
queue.on('global:completed', jobId => {
  console.log(`Job with id ${jobId} has been completed`);
})
```
## **Queue Options**
* **Rate Limiter**
    - limit the number of jobs processed in a unit of time
    - example:
```
// Limit queue to max 1.000 jobs per 5 seconds.
const myRateLimitedQueue = new Queue('rateLimited', {
  limiter: {
    max: 1000,
    duration: 5000
  }
});
```
* **Named jobs**
    - gives jobs names.  duh
    - examples:
```
// Jobs producer
const myJob = await transcoderQueue.add('image', { input: 'myimagefile' });
const myJob = await transcoderQueue.add('audio', { input: 'myaudiofile' });
const myJob = await transcoderQueue.add('video', { input: 'myvideofile' });
```

```
// Worker
transcoderQueue.process('image', processImage);
transcoderQueue.process('audio', processAudio);
transcoderQueue.process('video', processVideo);
```

* **Sandboxed Processors**
    - when defining a process function it is possible to provide a concurrency setting
    - allows the worker to process several jobs in parallel

## **Job types**
* **LIFO**
    - last in first out
    - jobs added to the beginning of the queue 
    - example
```
const myJob = await myqueue.add({ foo: 'bar' }, { lifo: true });
```
* **Delayed**
    - jobs in the queue are delayed a certain amount of time before they will be processed
    - example:
```
// Delayed 5 seconds
const myJob = await myqueue.add({ foo: 'bar' }, { delay: 5000 });
```
* **Prioritized**
    - jobs can be added to a queue with a priority value
    - example:
```
const myJob = await myqueue.add({ foo: 'bar' }, { priority: 3 });
```

* **Repeatable**
    - special jobs that repeat themselves indefinitely or until a given maximum date or number or repetitions
    - example:
```
// Repeat every 10 seconds for 100 times.
const myJob = await myqueue.add(
  { foo: 'bar' },
  {
    repeat: {
      every: 10000,
      limit: 100
    }
  }
);

// Repeat payment job once every day at 3:15 (am)
paymentsQueue.add(paymentsData, { repeat: { cron: '15 3 * * *' } });
```


