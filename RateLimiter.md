# RATE LIMITER

## Rate Limiter

Rate limiter is a system that controls the rate of traffic sent or received by a network interface controller. It is used to prevent the network interface controller from being overwhelmed by too much traffic. Rate limiters are used in many different types of networks, including local area networks (LANs), wide area networks (WANs), and the Internet.

## Types of Rate Limiters

There are two main types of rate limiters: 
- Software-based rate limiters: These rate limiters are implemented in software and are used to control the rate of traffic sent or received by a network interface controller.

- Hardware-based rate limiters: These rate limiters are implemented in hardware and are used to control the rate of traffic sent or received by a network interface controller.

## How Rate Limiters Work

Rate limiters work by monitoring the rate of traffic sent or received by a network interface controller and adjusting the rate of traffic to ensure that the network interface controller is not overwhelmed. Rate limiters can be configured to limit the rate of traffic based on a variety of factors, including the type of traffic, the source of the traffic, and the destination of the traffic.

## Algorithms Used in Rate Limiters
- Token Bucket Algorithm
- Leaky Bucket Algorithm
- Fixed Window Algorithm
- Sliding Window Algorithm


### Token Bucket Algorithm
- A token bucket is a container that holds a fixed number of tokens. Token are added to the bucket at a fixed rate. Once the bucket is full, no more tokens are added. 
- When a request is made, a token is removed from the bucket. If there are no tokens in the bucket, the request is denied.
- It will return status code 429 (Too Many Requests) if the bucket is empty.

The token bucket algorithm takes two parameters:
- The maximum number of tokens that the bucket can hold (the bucket size)
- The rate at which tokens are added to the bucket (the refill rate)

### Leaky Bucket Algorithm
- The leaking bucket algorithm is similar to the token bucket except that requests are processed at a fixed rate. It is usually implemented with a first-in-first-out (FIFO) queue. The algorithm works as follows:
- When a request arrives, the system checks if the queue is full. If it is not full, the request is added to the queue.
- If the queue is full, the request is denied.

The leaking bucket algorithm takes two parameters:
- The maximum number of requests that the queue can hold (the queue size)
- The rate at which requests are processed (the processing rate)

### Fixed Window Algorithm
- The fixed window algorithm is a simple rate limiter that limits the number of requests that can be made in a fixed time window. The algorithm works as follows:
- When a request arrives, the system checks if the number of requests made in the current time window is less than the maximum number of requests allowed. If it is, the request is allowed. If it is not, the request is denied.


### Sliding Window Algorithm
- The sliding window algorithm is a more complex rate limiter that limits the number of requests that can be made in a sliding time window. The algorithm works as follows:
- The algorithm keeps track of request timestamps. Timestamp data is usually kept in
cache, such as sorted sets of Redis.
- When a new request comes in, remove all the outdated timestamps. Outdated timestamps
are defined as those older than the start of the current time window.
- Add timestamp of the new request to the log.
- If the log size is the same or lower than the allowed count, a request is accepted.
Otherwise, it is rejected.