---

## Application Load Balancing

---

## Agenda

- What is Load Balacing?
- Classic ELB vs ALB
- Key ALB concepts
- Cool Features the ALB Offers
- Deployment Using the ALB Recap
- Live Demo on AWS

---

## What is Load Balancing?

- Distributes incoming network traffic across a group of servers
- Ensures high availability and reliability by sending requests to servers that are up and healthy
- How does it choose which server to route to?

+++

### Load Balancing Algorithm

- Round Robin: distributed sequentially
- Least Connection: go to the one with the fewest current connections to clients
- IP Hash: the IP address of the client is used to determine which server receives the request

+++

### How AWS does it?

- Classic ELB: Round Robin & Least Connection (which is called Least Outstanding Requests)
- ALB: Evaluates the listener rules in priority order, then selects a target in a Target Group in round robin fashion

---

## Classic ELB vs ALB

- Classic ELB operates at Layer 4 of the OSI model, whereas ALB operates at Level 7
- But what is the OSI model??

+++?image=assets/osi-model.jpg&size=auto 75%

+++

### ELB v.s. ALB (cont.)

- Classic ELB operates at Layer 4 of the OSI model, whereas ALB operates at Layer 7
- Classic ELB operates at the port level (e.g. TCP port 80 aka HTTP, 443 aka HTTPS)
- At Layer 7, the ALB has the ability to inspect application-level content, not just IP and port
- The ALB offers basically everything the ELB does and more

---

## Key ALB concepts

- *Rules*: determine what actions are taken based on a URL pattern or a host
- *Priorities*: tell the ALB which order to evaluate the rules
- *Target Groups*: used to route requests to all registered targets as part of a rule
- Each Target Group specifies a protocol/port and configures its own healthcheck 

---

## Cool Features the ALB Offers

- Deletion Protection
- Native HTTP/2 (*)
- Host-based Routing (*)
- Path-based Routing (*)
- Redirects & Fixed Response
- Containerized Application Support (Amazon ECS)

+++

### HTTP/2 Support

- Allows multiple requests to be sent on the same connection (up to 128)
- Compresses header data
- Supports SSL connection to clients

+++

### Host-based Routing

- alb.quorum.us would go to a different target group (which is how we currently do deployment, more on this later)
- Grassroots subdomains can now go to their own target groups and instances!
- Can include up to 3 wildcard characters
- E.g. `*.quorum.us` matches nami.quorum.us but not quorum.us

+++

### Path-based Routing

- Only applies to the path of the URL, not its query parameters
- E.g. `/img/*` would go to its own target group that fetches static files
- E.g. `/login` can be forwarded to a microservice (e.g. an AWS Lambda) that does just authentication

---

## Deployment Using the ALB Recap

+++?image=assets/QBits_Khoa.002.jpeg&size=auto 70%

+++?image=assets/QBits_Khoa.003.jpeg&size=auto 70%

+++?image=assets/QBits_Khoa.004.jpeg&size=auto 70%

+++?image=assets/QBits_Khoa.005.jpeg&size=auto 70%

---

## Live Demo on AWS
