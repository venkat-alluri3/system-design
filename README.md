# System design preparation notes

## System design approach

Discuss how to approach system design interview and make a template to follow in the interview. Came up with this approach after referring to muliple resources.

### 1. Understand the goal of the app [1 min]
 Try to understand what the interviewer is asking us to design and ask generic questions about the application we are trying to build and the end users of the application. This understanding should help us in gathering the requirements of the system. 
 
 ### 2. Requirements clarifications [5 min]
 End goal is to clarify the function and non-function requirements

*Users/Customers*
1. Use cases of the system 
2. How the sytem will be used (Usage patterns)
3. How many will use the system
4. who will use the system 
5. What are the inputs and outputs of the system 

*Scale*
1. How much data is queried per request 
2. Can there be spike in the traffic
3. How much data is processed/ written
4. How many read/wrire queries
5. How much data are we expected to handle

*performance*
1. What is expected write to read delay
2. What is expected p99 latency for the read queries

*Dicuss constraints*
1. Any limitaions in the system
2. What is allowed and what is not allowed

#### 3. Envolope calculations(capacity) [4 min]
What is capacity estimation
A quick and approximate calculation of storage and bandwidth that gives us further insight. Helps to calculate
- traffic estimation (read request per sec, write requests per sec)
- storage estimation (storage needed to store worth 3 yrs of stored 'object')
- bandwidth estimate (#of bytes/sec system should handle for incoming and outgoing traffic)
- cache estimate (memory needed to cache some of the hot read responses, 80-20 rule)
- Read/write ratio
- Latency expected from the system

*How do we do the capacity estimantion and calculations:*

*Userful calculations:*
x Million users * y KB = xy GB
example: 1M users * a documents of 100KB per day = 100GB per day.
x Million users * y MB = xy TB
example: 200M users * a short video of 2MB per day = 400TB per day.

*Byte Number Sizes*
The number of zeros after thousands increments by 3.
Thousands = KB (3 zeros)
Millions = MB(6 zeros)
Billions = GB (9 zeros)
Trillions = TB (12 zeros)
Quadrilions = PB (15 zeros)

Byte Conversions
1B = 8bits
1KB = 1000B
1MB = 1000KB
1GB = 1000MB

Objects
File: 100 KB
Web Page: 100 KB (not including images)
Picture: 200 KB
Short Posted Video: 2MB
Steaming Video: 50MB per minute
Long/Lat: 8B
Lengths
Maximum URL Size: ~2000 (depends on browser)
ASCII charset: 128
Unicode charset: 143, 859

Per Period Numbers
The following numbers are heavily rounded and help determine how often something needs to happen over a period of time. For example, if a server has a million requests per day, it will need to handle 12 requests per second.

|Month  | 1 Billion | 1 Million | 1k      |
|-------|-----------|-----------|---------|
|Day    | 32M       | 32 K      |32       |
|Hour   |1.3M       | 1.3k      |1.30     |
|minute |22k        | 22        |.02      |
|Second | 400       | 0.4       |.0004    |

|Day    | 1 Billion | 1 Million | 1k      |
|-------|-----------|-----------|---------|
|Hour   |42M        | 42k       |42       |
|minute |700k       |  700      |.7       |
|Second |12k        | 12        |.01      |

https://matthewdbill.medium.com/back-of-envelope-calculations-cheat-sheet-d6758d276b05


#### 4. Design Goals [3 min]

1. Latency and Thought requirements
2. Consistency vs Availability 
   - Weak/Strong/eventual ->consistency
   - Failover/replication ->availability

#### 5. High level Design.[5-10min]
1. API's for Read/Write scenarios for crucial componenets
2. Database schema
3. Basic Algorithm
4. High level design for Read/write scenario

#### 6. Scale the design - Deep dive[20min]
1.  Scaling the algorithm
2. Scaling individual components: 
	-> Availability, Consistency and Scale story for each component
        -> Consistency and availability patterns
3. Think about the following components, how they would fit in and how it would help
	1. DNS
 	2. CDN [Push vs Pull]
 	3. Load Balancers [Active-Passive, Active-Active, Layer 4, Layer 7]
	4. Reverse Proxy
	5. Application layer scaling [Microservices, Service Discovery]
	6. DB [RDBMS, NoSQL]
		1.RDBMS 
         		1. Master-slave, Master-master, Federation, Sharding, Denormalization, SQL Tuning
      		2. NoSQL
         		1. Key-Value, Wide-Column, Graph, Document
          		2. Fast-lookups:
           			a. RAM  [Bounded size] => Redis, Memcached
           			b. AP [Unbounded size] => Cassandra, RIAK, Voldemort
           			c. CP [Unbounded size] => HBase, MongoDB, Couchbase, DynamoDB
	7. Caches
    		Client caching, CDN caching, Webserver caching, Database caching, Application caching, Cache @Query level, Cache @Object level
     		Eviction policies
      			a. Cache aside
      			b. Write through
      			c. Write behind
      			d. Refresh ahea
	8. Asynchronism
	- Message queues
      	- Task queues
      	- Back pressure
 	9. Communication
    	- TCP
    	- UDP
        - REST
    	- RPC

   
