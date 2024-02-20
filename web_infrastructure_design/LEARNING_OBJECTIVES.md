# Learning Objectives

- [What is Server](#what_is_server)
- [What is Web server ](#what_is_web_server)
- [What is DNS ](#what_is_dns)
- [What is Load balancer ](#what_is_load_balancer)
- [What if no load balancer ](#what_is_load_balancer)
- [What is Monitoring ](#what_is_monitoring)
- [What is a database](#what_is_a_database)
- [What’s the difference between a web server and an app server?](#what’s_the_difference_between_a_web_server_and_an_app_server?)
- [DNS record types](#dns_record_types)
- [Single point of failure](#single_point_of_failure)
- [How to avoid downtime when deploying new code](#how_to_avoid_downtime_when_deploying_new_code)
- [High availability cluster (active-active/active-passive)](#high_availability_cluster "active-active/active-passive")
- [What is HTTPS](#what_is_http)
- [What is a firewall](#what_is_a_firewall)

## What is Server

A server is a computer or system that is designed to manage network resources and provide services to other computers, known as clients, over a network.

## What is Web server

Web servers handle HTTP requests from clients (typically web browsers) and serve web pages or other web-related content. Apache, Nginx, and Microsoft Internet Information Services (IIS) are popular web server software.

## What is DNS

DNS (Domain Name System) servers resolve domain names to IP addresses, enabling users to access websites using human-readable domain names instead of numerical IP addresses.

## What is Load balancer

A load balancer is a device or software application that distributes incoming network traffic across multiple servers or resources to ensure that no single server is overwhelmed with too much load.

## What if no load balancer

If you don't have a load balancer and rely on a single server to handle all incoming traffic, several challenges and limitations may arise.

### Single Point of Failure:

- A single server becomes a critical point of failure. If that server experiences hardware issues, crashes, or needs maintenance, the entire application or service may become unavailable.

- Limited Scalability:
  Scaling to handle increased traffic can be challenging. A single server has a finite capacity, and as demand grows, it may lead to performance degradation and slower response times.

- Inefficient Resource Utilization:
  Without load balancing, resource utilization may not be optimized. Some servers may be underutilized while others are overwhelmed with traffic, leading to an uneven distribution of resources.

- No High Availability:
  There is no built-in mechanism for high availability. If the server goes down for any reason, users will experience downtime until the server is restored.

- Poor Performance During Maintenance:
  Performing maintenance on a single server requires downtime or service interruptions. With a load balancer, you can take individual servers offline for maintenance without affecting overall service.

- Limited Redundancy:

Without load balancing, redundancy is limited. If the primary server fails, there might be no backup or failover mechanism to handle incoming requests.

- Scalability Challenges:
  Adding additional servers to accommodate growing traffic becomes more complex. Without load balancing, you need to manage traffic distribution manually or consider alternative methods for scaling.

- Difficulty in Handling Traffic Spikes:
  Traffic spikes, such as during a sudden increase in user activity or due to an event, can overwhelm a single server. Load balancing helps distribute such spikes across multiple servers.

In the context of computing and network traffic, a "spike" refers to a sudden and temporary increase in activity or demand.

## What is Monitoring

Refers to the process of observing and tracking the performance, health, and behavior of computer systems, networks, applications, and other components. The goal of monitoring is to ensure the reliability, availability, and optimal performance of IT infrastructure and services. Monitoring involves collecting, analyzing, and presenting data to detect issues, troubleshoot problems, and make informed decisions about resource allocation and system improvements.

- Performance Monitoring:

Tracking the performance metrics of systems and applications, such as CPU usage, memory utilization, disk I/O, network bandwidth, and response times. Performance monitoring helps identify bottlenecks, resource constraints, and areas for optimization.

- Availability Monitoring:

Checking the availability of systems and services to ensure they are accessible and operational. Availability monitoring involves detecting outages, downtime, or disruptions and triggering alerts or notifications when issues arise.

- Health Monitoring:

Assessing the overall health of IT components, including hardware, software, and networks. Health monitoring involves monitoring system logs, error rates, and other indicators to identify potential problems before they impact performance.

## What is a database

A database is a structured collection of data that is organized in a way that makes it easy to manage, retrieve, update, and store information. It serves as a centralized repository for storing and managing data, enabling efficient access and retrieval of information for various purposes. Databases are fundamental to the operation of many software applications, websites, and systems.

## What’s the difference between a web server and an app server?

Web servers and application servers are both critical components in the architecture of web applications, but they serve different purposes and handle different aspects of the web application stack

### Web Server:

#### Primary Purpose:

- Responsibility:
  Web servers are primarily responsible for handling HTTP requests and responses. They serve static content (HTML, CSS, images) and may also handle basic request processing.

#### Static Content:

- Serving Static Files:
  Web servers are designed to efficiently serve static content to clients. This includes files that don't change often, like HTML pages, images, and stylesheets.

#### Request Handling:

- Basic Request Handling:
  Web servers handle incoming HTTP requests, parse them, and respond with the appropriate static content. They often support features like URL mapping and redirects.

#### Examples:

- Common Web Servers:
  Examples of web servers include Apache HTTP Server, Nginx, Microsoft Internet Information Services (IIS), and LiteSpeed.

#### Deployment:

- Common Deployment:
  Web servers are typically deployed at the front end of an architecture, handling initial client requests and directing them to the appropriate components, including application servers if needed.

#### Application Server:

- Primary Purpose:
  Responsibility: Application servers are responsible for executing server-side logic and processing dynamic content. They handle the business logic and application-specific functionality.

#### Dynamic Content:

- Executing Code:
  Application servers execute server-side code (e.g., scripts, servlets, or server-side components) to generate dynamic content based on client requests.

#### Data Processing:

- Database Interaction:
  Application servers often interact with databases, perform data processing, and handle complex business logic, such as user authentication, authorization, and transaction management.

#### Examples:

- Common Application Servers:
  Examples of application servers include Apache Tomcat, WildFly (formerly JBoss), IBM WebSphere, and Microsoft ASP.NET.

#### Integration:

- Middleware Integration:
  Application servers may serve as middleware, integrating with various components and services to provide a comprehensive environment for application development.

#### Deployment:

- Behind the Web Server:
  Application servers are typically deployed behind a web server. The web server handles static content and forwards dynamic requests to the application server for processing.

## DNS

### Browser Sends DNS Query:

- The browser sends a DNS query to a DNS resolver (often provided by the Internet Service Provider or a public DNS service like Google DNS or OpenDNS).

### DNS Resolver Resolution:

- The DNS resolver checks its cache to see if it already knows the IP address associated with the domain. If not, it queries the authoritative DNS servers for the domain.

### DNS Query Includes Various Record Types:

- The DNS query may include various record types depending on the information needed. Commonly, it includes an A record or AAAA record to resolve the domain to an IP address.

### DNS Response:

- The authoritative DNS servers respond to the query with the requested information, including the IP address associated with the domain.

### Browser Sends HTTP Request:

- The browser now has the IP address and can send an HTTP request to the web server associated with that IP address.

### Web Server Processes Request:

- The web server processes the HTTP request, which may involve fetching dynamic content, executing server-side scripts, or serving static files.

### Web Server Sends HTTP Response:

- The web server sends an HTTP response back to the browser, which includes the requested content (HTML, images, etc.).

### Browser Renders Web Page:

- The browser receives the HTTP response, processes the content, and renders the web page for the user.

## DNS record types

### A (Address) Record:

- Purpose:
  Associates a domain name with an IPv4 address. It's used to map a domain to a specific IP address.

### AAAA (IPv6 Address) Record:

- Purpose:
  Similar to the A record but used for IPv6 addresses. Associates a domain name with an IPv6 address.

### CNAME (Canonical Name) Record:

- Purpose:
  Creates an alias for a domain, pointing it to another domain's A or AAAA record. Commonly used for creating subdomains or pointing multiple domain names to the same IP address.

### MX (Mail Exchange) Record:

- Purpose:
  Specifies mail servers responsible for receiving emails on behalf of a domain. It includes the mail server's priority and domain name.

### TXT (Text) Record:

- Purpose:
  Holds text information associated with a domain. Commonly used for various purposes, such as DNS-based verification for services like DKIM and SPF.

## Single point of failure

A "single point of failure" (SPOF) refers to a component or part of a system that, if it fails, will cause the entire system to fail.

## How to avoid downtime when deploying new code

Avoiding downtime when deploying new code is a crucial consideration for maintaining a seamless and continuous user experience.

### Use Blue-Green Deployment:

- Implement a blue-green deployment strategy where you maintain two identical production environments (blue and green). Users access one environment while the other is updated. This approach allows for a smooth transition without downtime.

### Canary Releases:

- Gradually roll out new code to a subset of users (canaries) before deploying it to the entire user base. This allows you to monitor for issues and gather feedback, minimizing the impact of potential problems.

### Feature Toggles (Feature Flags):

Use feature toggles to enable or disable specific features in your application. By turning off new features initially, you can deploy code without affecting the user experience, and then gradually enable features as they are tested and verified.

### Load Balancers and Redundancy:

Utilize load balancers to distribute traffic across multiple servers or instances. This allows you to take individual servers out of rotation for updates without affecting the overall service.

## High availability cluster (active-active/active-passive)

A high availability (HA) cluster is a setup in which multiple servers or nodes work together to ensure continuous operation of a system or application, minimizing downtime and providing redundancy. There are two common configurations for high availability clusters: active-active and active-passive.

### Active-Active Cluster:

- In an active-active cluster, all nodes in the cluster are actively serving traffic or processing requests simultaneously. Each node is capable of handling its share of the workload, and the load is distributed among the nodes.
- Benefits:
  -- Efficient resource utilization: All nodes contribute to processing requests, maximizing the use of resources.
  -- Scalability: The cluster can easily scale by adding more active nodes.
- Considerations:
  -- Requires careful load balancing to distribute traffic evenly among nodes.
  -- Complex coordination between nodes to avoid conflicts and ensure data consistency.

### Active-Passive Cluster:

In an active-passive cluster, one node (or a subset of nodes) actively handles the workload, while the others remain in a passive or standby state. The passive nodes only become active if the active node fails or is taken offline intentionally.

- Benefits:
  -- Simplified management:
  Easier to manage and configure, as only one node is active at a time.
  -- Clear failover mechanism: In case of a failure, traffic is redirected to the passive node(s).
- Considerations:
  -- Resource utilization: Passive nodes are not contributing to processing requests unless the active node fails.
  -- May result in underutilization of resources in normal operation.
Both active-active and active-passive configurations have their use cases, and the choice depends on factors such as the application requirements, desired resource utilization, and the level of complexity the organization is willing to manage.

## What is HTTPS

HTTPS stands for Hypertext Transfer Protocol Secure. It is an extension of HTTP (Hypertext Transfer Protocol) that is used to secure the communication over a computer network, typically the internet. HTTPS is designed to provide a secure and encrypted connection between a user's web browser and the website they are interacting with.


### Encryption:

- HTTPS uses SSL (Secure Sockets Layer) or its successor, TLS (Transport Layer Security), protocols to encrypt the data exchanged between the user's browser and the website's server. This encryption helps protect sensitive information from being intercepted or tampered with during transmission.

### Authentication:

- HTTPS provides a way to authenticate the identity of the website by using digital certificates. These certificates are issued by trusted Certificate Authorities (CAs) and help users verify that they are connecting to the legitimate website and not a malicious impostor.

### Data Integrity:

- The use of encryption in HTTPS not only secures the data but also ensures its integrity. If any data is altered during transmission, it will be detected, and the connection may be terminated to prevent potential security risks.

### SEO Benefits:

- Search engines, such as Google, give preference to websites using HTTPS, considering it as a ranking factor. This incentivizes website owners to adopt secure connections to improve their search engine rankings.

### Secure Transactions:

- HTTPS is crucial for secure online transactions, such as e-commerce transactions, where sensitive information like credit card details and personal data are transmitted over the internet. The secure connection helps prevent unauthorized access to this information.

### Browser Indicators:

- Browsers provide visual indicators, such as a padlock icon, to inform users that they are on a secure, HTTPS-enabled website. This builds trust and confidence among users regarding the safety of their data.

## What is a firewall
A firewall is a network security device or software that monitors and controls incoming and outgoing network traffic based on predetermined security rules. Its primary purpose is to establish a barrier between a trusted internal network and untrusted external networks, such as the internet. Firewalls are a fundamental component of network security and help protect systems and data from unauthorized access, cyber threats, and other potential security risks.

### Packet Filtering:

- Firewalls examine individual data packets and make decisions about whether to allow or block them based on predefined rules. These rules typically consider factors such as source and destination IP addresses, port numbers, and the protocol used.

### Stateful Inspection:
- Stateful firewalls keep track of the state of active connections and make decisions based on the context of the traffic. This allows them to understand the state of a connection and make more informed decisions.

### Proxying and Network Address Translation (NAT):
- Some firewalls act as proxies, forwarding requests on behalf of clients to enhance security. NAT is often used to hide internal IP addresses from external networks, providing an additional layer of security.

### Application Layer Filtering:
- Firewalls can inspect and control traffic at the application layer, allowing or blocking specific applications or services. This is often done using deep packet inspection to analyze the content of data packets.

### Virtual Private Network (VPN) Support:
- Firewalls often include VPN capabilities to establish secure encrypted tunnels for remote users or branch offices to connect to the corporate network over the internet.

### Intrusion Prevention and Detection:
- Some advanced firewalls include intrusion prevention and detection systems (IPS/IDS) to identify and block potentially malicious activity in real-time.

### Logging and Reporting:
- Firewalls maintain logs of network activity, allowing administrators to review and analyze events. They may also generate reports to provide insights into network traffic patterns and security incidents.

### User Authentication and Access Control:
- Firewalls can enforce user authentication and access control policies, restricting access to certain resources based on user credentials and roles.

### Security Zones:
- Firewalls can define security zones to segment a network into different areas with varying levels of trust. This helps contain and control the spread of threats.
