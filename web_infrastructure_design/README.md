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