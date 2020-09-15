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
* 