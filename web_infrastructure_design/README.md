# web_infrastructure_design

This directory contains the design documentation and configurations for the web infrastructure of our project.

## Table of Contents

- [Learning Objectives](#learning-objectives)
- [Requirements](#requirements)
- [Practice Exercises](#practice-exercises)

## Learning Objectives

This project is based on the learning objectives - see the [LEARNING_OBJECTIVES](https://github.com/Goaty-yagi/holbertonschool-system_engineering-devops/blob/main/web_infrastructure_design/LEARNING_OBJECTIVES.md) file for details.

## Requirements

- A README.md file, at the root of the folder of the project, is mandatory
- For each task, once you are done whiteboarding (on a whiteboard, piece of paper or software or your choice), take a picture/screenshot of your diagram
- This project will be manually reviewed:
- As each task is completed, the name of that task will turn green
- Upload a screenshot, showing that you completed the required levels, to any image hosting service (I personally use imgur but feel free to use anything you want).
- For the following tasks, insert the link from of your screenshot into the answer file
- After pushing your answer file to GitHub, insert the GitHub file link into the URL box
- You will also have to whiteboard each task in front of a mentor, staff or student - no computer or notes will be allowed during the whiteboarding session
- Focus on what you are being asked:
- Cover what the requirements mention, we will explore details in a later project
- Keep in mind that you will have 30 minutes to perform the exercise, you will get points for what is asked in requirements
- Similarly in a job interview, you should answer what the interviewer asked for, be careful about being too verbose - always ask the interviewer if going into details is necessary - speaking too much can play against you
- In this project, again, avoid going in details if not asked

## Practice Exercises

### 0. Simple web stack

<img src='https://github.com/Goaty-yagi/holbertonschool-system_engineering-devops/blob/main/web_infrastructure_design/0-diagram.png'>

**File:** [0-simple_web_stack](https://github.com/Goaty-yagi/holbertonschool-system_engineering-devops/blob/main/web_infrastructure_design/0-simple_web_stack)<br>
**Description:** <br>
On a whiteboard, design a one server web infrastructure that hosts the website that is reachable via www.foobar.com. Start your explanation by having a user wanting to access your website.
**Requirements:** <br>

- You must use:
  -- 1 server
  -- 1 web server (Nginx)
  -- 1 application server
  -- 1 application files (your code base)
  -- 1 database (MySQL)
  -- 1 domain name foobar.com configured with a www record that points to your server IP 8.8.8.8
- You must be able to explain some specifics about this infrastructure:
  -- What is a server
  -- What is the role of the domain name
  -- What type of DNS record www is in www.foobar.com
  -- What is the role of the web server
  -- What is the role of the application server
  -- What is the role of the database
  -- What is the server using to communicate with the computer of the user requesting the website
- You must be able to explain what the issues are with this infrastructure:
  -- SPOF
  -- Downtime when maintenance needed (like deploying new code web server needs to be restarted)
  -- Cannot scale if too much incoming traffic

#### SPOF

There is just one server in use, so if the server has issues and stop running,
this application will be down.

#### Downtime when maintenance needed (like deploying new code web server needs to be restarted)

When you want to deploy a new code, you need to stop the server that decrease reliability and availability.

#### Cannot scale if too much incoming traffic

One server always handles all incoming traffic, so it will be overwhelmed, and might be overflow. Also it is hard to scale up without stopping the server.

### 1. Distributed web infrastructure

<img src='https://github.com/Goaty-yagi/holbertonschool-system_engineering-devops/blob/main/web_infrastructure_design/1-diagram.png'>

**File:** [1-distributed_web_infrastructure](https://github.com/Goaty-yagi/holbertonschool-system_engineering-devops/blob/main/web_infrastructure_design/1-distributed_web_infrastructure)<br>
**Description:** <br>
On a whiteboard, design a three server web infrastructure that hosts the website www.foobar.com.
**Requirements:** <br>

- You must add:
  -- 2 servers
  -- 1 web server (Nginx)
  -- 1 application server
  -- 1 load-balancer (HAproxy)
  -- 1 set of application files (your code base)
  -- 1 database (MySQL)
- You must be able to explain some specifics about this infrastructure:
  -- For every additional element, why you are adding it
  -- What distribution algorithm your load balancer is configured with and how it works
  -- Is your load-balancer enabling an Active-Active or Active-Passive setup, explain the -- difference between both
  -- How a database Primary-Replica (Master-Slave) cluster works
  -- What is the difference between the Primary node and the Replica node in regard to the application
- You must be able to explain what the issues are with this infrastructure:
  -- Where are SPOF
  -- Security issues (no firewall, no HTTPS)
  -- No monitoring

#### For every additional element, why you are adding it

- 2 servers: 1 for load balancer, another is for redundancy to minimize downtime.
- load-balancer: to distribute incoming traffic to increase availability and reliability.

#### What distribution algorithm your load balancer is configured with and how it works

distributes incoming network or application traffic evenly across a group of servers.

#### Is your load-balancer enabling an Active-Active or Active-Passive setup, explain the difference between both

Assume that my load blancer enable an Active-Active set up.

#### How a database Primary-Replica (Master-Slave) cluster works

A Primary-Replica (Master-Slave) database cluster is a configuration in which there is one primary (master) database server and one or more replica (slave) database servers. This architecture is commonly used to achieve high availability, fault tolerance, and scalability in database systems. The primary server handles write operations (INSERT, UPDATE, DELETE), while replica servers are used for read operations (SELECT) and can also serve as backups in case the primary server fails.

#### What is the difference between the Primary node and the Replica node in regard to the application

The primary node and replica nodes in a database cluster serve different roles, and their responsibilities are tailored to specific tasks within the context of the application. Here are the key differences between the primary node and replica nodes:

- Write Operations:
  -- Primary Node (Master): The primary node is responsible for handling write operations. It is the authoritative source for changes to the database. All INSERT, UPDATE, and DELETE operations are initially applied to the primary node.
  -- Replica Nodes (Slaves): Replica nodes are read-only and do not accept direct write operations. They rely on data replication from the primary node to mirror the changes made on the primary.

- Read Operations:
  -- Primary Node (Master): While the primary node handles write operations, it can also handle read operations. However, in systems with heavy read traffic, using replicas for read operations can offload the primary node and improve overall performance.
  -- Replica Nodes (Slaves): Replica nodes are dedicated to handling read operations. They serve as additional nodes that can respond to SELECT queries, providing scalability for read-intensive workloads.

- High Availability and Failover:
  -- Primary Node (Master): The primary node is a single point of failure. In the event of a failure, a failover mechanism may be triggered to promote one of the replica nodes to become the new primary, ensuring continuous service.
  -- Replica Nodes (Slaves): Replica nodes are designed to provide redundancy and high availability. If a replica node fails, it does not typically impact the availability of the overall system for write operations.

- Data Replication:
  -- Primary Node (Master): The primary node is the source of truth for the database. It initiates the replication process, sending changes to the replica nodes to keep them in sync.
  -- Replica Nodes (Slaves): Replica nodes receive and apply changes from the primary node. The replication process can be synchronous or asynchronous, depending on the chosen configuration.

- Consistency:
  -- Primary Node (Master): The primary node ensures data consistency by validating and committing write operations before replication.
  -- Replica Nodes (Slaves): Replica nodes aim to maintain consistency with the primary node by applying changes in the same order and ensuring that the replicated data matches the primary data.

### 2. Secured and monitored web infrastructure

<img src='https://github.com/Goaty-yagi/holbertonschool-system_engineering-devops/blob/main/web_infrastructure_design/2-diagram.png'>

**File:** [2-secured_and_monitored_web_infrastructure](https://github.com/Goaty-yagi/holbertonschool-system_engineering-devops/blob/main/web_infrastructure_design/2-secured_and_monitored_web_infrastructure)<br>
**Description:** <br>
On a whiteboard, design a three server web infrastructure that hosts the website www.foobar.com, it must be secured, serve encrypted traffic, and be monitored.
**Requirements:** <br>

- You must add:
  -- 3 firewalls
  -- 1 SSL certificate to serve www.foobar.com over HTTPS
  -- 3 monitoring clients (data collector for Sumologic or other monitoring services)
- You must be able to explain some specifics about this infrastructure:
  -- For every additional element, why you are adding it
  -- What are firewalls for
  -- Why is the traffic served over HTTPS
  -- What monitoring is used for
  -- How the monitoring tool is collecting data
  -- Explain what to do if you want to monitor your web server QPS
- You must be able to explain what the issues are with this infrastructure:
  -- Why terminating SSL at the load balancer level is an issue
  -- Why having only one MySQL server capable of accepting writes is an issue
  -- Why having servers with all the same components (database, web server and application server) might be a problem

#### :For every additional element, why you are adding it

- 3 firewalls: to filter out malicious requests in each server to increase security.
- SSL certificate: to make an encrypted connection between a client and a server for safe connection.
- 3 monitoring: to check several things like resource utilization (CPU, memory, disk), Availability, error and exception monitoring, alert monitoring to sustain your servers health.

#### :What are firewalls for

- Firewalls are security devices or software components designed to monitor, filter, and control incoming and outgoing network traffic based on predetermined security rules.

#### :Why is the traffic served over HTTPS

- to make sure the connection is encrypted so that the data won't be read even if it is stolen.

#### :What monitoring is used for

- Monitor resource utilization, error, alert and flow of the traffic to collect matrix to be analysed.

#### How the monitoring tool is collecting data

Generally

- 1, Install monitoring tools
- 2, Configure settings and integration
- 3, Set logging wherever you like
- 4, The monitoring tool detects the logging and starts API call to send the logging data

#### Explain what to do if you want to monitor your web server QPS

- Apache Benchmark can be an option
  -- n: The total number of requests to perform during the test.
  -- c: The number of multiple requests to perform at a time.
  -- For example, to send 1000 requests with 10 concurrent requests to your Nginx server's homepage, you would run:

```bash
ab -n 1000 -c 10 http://your-nginx-server/
```

- Then you will get a result includes QPS like this

```bash
Requests per second:    200.00 [#/sec] (mean)
```

- This indicates that the server is handling approximately 200 requests per second on average.

- Why terminating SSL at the load balancer level is an issue
  -- Loss of End-to-End Encryption:
- How to keep SSL to the end?
  -- Re-Encryption at Each Server: In this approach, each server in the chain (load balancer and backend servers) participates in SSL/TLS encryption and decryption. The SSL connection is terminated at the load balancer, and the traffic is re-encrypted before being forwarded to the backend servers. Each backend server then handles its own SSL/TLS termination.
  -- SSL Passthrough to Backend Servers: In this approach, SSL passthrough is used, and SSL/TLS traffic is not decrypted at the load balancer. The encrypted traffic is passed through to each backend server, and each server handles its own SSL/TLS termination.

- Why having only one MySQL server capable of accepting writes is an issue
  -- Single Point of Failure:
  If the sole MySQL server handling write operations fails, the entire write functionality becomes unavailable. This results in downtime and disrupts the application's ability to update or modify data.
  -- Limited Scalability:
  A single MySQL server may become a bottleneck as the application grows. It may not be able to handle increased write traffic or a growing dataset efficiently. This limits the overall scalability of the database system.
  -- Reduced Performance:
  Increased write load on a single server can lead to performance degradation. As the volume of write operations grows, the server might struggle to keep up with the demand, leading to slower response times and potential contention issues.
  -- Difficulty in Maintenance:
  Performing maintenance tasks, such as software updates, patches, or hardware upgrades, on the single MySQL server can be challenging. These tasks often require downtime, impacting the availability of write operations.

- Why having servers with all the same components (database, web server and application server) might be a problem
  -- SPOF
  -- Scalability
  -- Availability

### 3. Scale up

<img src='https://github.com/Goaty-yagi/holbertonschool-system_engineering-devops/blob/main/web_infrastructure_design/3-diagram.png'>

**File:** [3-scale_up](https://github.com/Goaty-yagi/holbertonschool-system_engineering-devops/blob/main/web_infrastructure_design/3-scale_up)<br>
**Description:** <br>
Scale up
**Requirements:** <br>

- You must add:
  -- 1 server
  -- 1 load-balancer (HAproxy) configured as cluster with the other one
  -- Split components (web server, application server, database) with their own server
- You must be able to explain some specifics about this infrastructure:
  -- For every additional element, why you are adding it


### SSL/TLP

<img src='https://github.com/Goaty-yagi/holbertonschool-system_engineering-devops/blob/main/web_infrastructure_design/ssl-tls.png'>

### DNS Server

<img src='https://github.com/Goaty-yagi/holbertonschool-system_engineering-devops/blob/main/web_infrastructure_design/dns-server.png'>

### TCP-three-way-handshake

<img src='https://github.com/Goaty-yagi/holbertonschool-system_engineering-devops/blob/main/web_infrastructure_design/tcp-three-way-handshake.png'>