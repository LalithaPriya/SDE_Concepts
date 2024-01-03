# Latency, Throughput, and Bandwidth: What, Why, and How

## Latency:

- **What:** Latency is the delay or time taken for data to travel from its source to its destination in a network.
- **Why:** Low latency ensures quick response times and a smooth user experience, crucial for real-time applications.
- **How to Measure:** Use ping times, measuring the round-trip time (RTT) in milliseconds.
- **Example**: When you click a link on a web page, the time it takes for the page to start loading is influenced by latency. If latency is low, the page starts loading quickly; if high, there's a noticeable delay before the page begins to load

## Throughput:

- **What:** Throughput measures the volume of data passing through a network in a specific time period.
- **Why:** High throughput indicates the network's capacity to handle data efficiently, affecting the number of users it can support.
- **How to Measure:** Calculate manually by sending a file and determining data transfer rate or use network testing tools.
- **Example**: Streaming a high-definition video is an example where throughput is crucial. High throughput ensures a smooth and uninterrupted streaming experience, while low throughput may result in buffering and pauses.

## Bandwidth:

- **What:** Bandwidth represents the maximum data transfer capacity of a network.
- **Why:** It defines the upper limit of data that can be transmitted, influencing overall network performance.
- **How to Measure:** Expressed in megabytes per second (MBps), it's a theoretical maximum limit.

## Improving Latency and Throughput:

### Caching:

- **How:** Store frequently accessed data closer to users using proxy servers or content delivery networks (CDNs).
- **Impact:** Reduces the time to retrieve data and lightens the load on the original source, improving both latency and throughput.

### Transport Protocols:

- **How:** Optimize the use of transport protocols like TCP and UDP based on the application requirements.
- **Impact:** TCP focuses on reliability, leading to higher latency but lower packet loss, while UDP prioritizes low latency at the expense of error-checking.

### Quality of Service (QoS):

- **How:** Implement QoS strategies to prioritize network traffic based on categories and assign priority levels.
- **Impact:** Ensures latency-sensitive applications receive preferential treatment, reducing packet loss and enhancing throughput for specific users.
