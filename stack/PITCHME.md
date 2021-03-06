---

## Quorum's Tech Stack

### Khoa Tran

---

## What We'll Cover

- What happens when you type quorum.us in the browser?
- Infrastructure
- Quorum's backend and frontend stack
- How code gets deployed
- Developer access to Quorum servers
- Q&A

+++

### Disclaimer

- Lots of information
- Serves as a general introduction
- We'll cover specific topics in depth as the summer progresses
- Stops me at anytime for questions

---

## What Happens When...?

- Based on the age-old interview question, what happens when you type google.com
- (We'll skip the key-pressed events / browser magic that we don't control)

+++?image=assets/quorum_stack.png&size=auto 90%

+++

## At a Glance

- DNS Lookup (quorum.us => 12.34.56.789)
- Elastic Load Balancer & Requests Routing
- Application Server (Nginx, Gunicorn, etc.)
- Database (PostgreSQL)

---

### Load Balancing

- Distributes load across instances
- Monitors the "health" of an instance
- What should we do if our instances are under high load?

+++

### Auto-scaling

- Auto-scales to meet demand and increase throughput
- Scale out (`instances += 1`) under high CPU or high memory
- Scale in (min 2) under low CPU and low memory
- Why 2? Redundancy & failure tolerance

---?image=assets/orge.jpg&size=auto 95%

+++

### nginx

- A reverse proxy configured with HTTPS certs
- Redirects HTTP => HTTPS
- Can handle static files (ours are served via CloudFront instead)
- Passes off the requests to Gunicorn workers

+++

### Application Server (Gunicorn)

- Spawns workers to process requests in parallel
- Depends on how many processors a server/machine has
- Can be sync (in parallel) or async (concurrently)
- Manages the workload and executes the Python and Django code

+++

### Django

- Is where most of our day is spent
- Processes the request from Gunicorn by executing Python code, calling APIs, accessing the database, rendering views, etc.
- Talks to PostgreSQL using the Django ORM

---

## Database (PostgreSQL)

- Hosted by AWS RDS
- Interfaces with Python/Django via the ORM and psycopg2

+++

### Infrastructure (end)

- Questions so far?
- Let's talk about our specific stack next!

---

## Backend Stack

- Python 2.7 -- we have 2.5 years :(
- Django 1.10 (soon to be on 1.11)
- PostgreSQL 10 on RDS
- Nginx / Gunicorn
- Supervisor to watch all of the above (except RDS)

+++

### AWS

- EC2 as our web servers on Ubuntu 14.10
- RDS as our database
- S3 for file storage
- Cloudfront (CDN) for static files
- Cloudwatch for alerts & monitoring
- ... and more!

+++

### Servers

- 2+ production (client-facing) instances
- 2 production (dev-facing) servers to process data (Update, State Update)
- 5+ crawler servers
- Staging/Beta/Testing
- Proxies
- An SSH bastion server that sits in front of our servers and the database

+++

### DevOps

- Primarily in Ansible
- Configures servers, installs packages, monitors instances, etc.
- CI/CD: Shippable, CodeFactor
- Deployment (more later)

+++

### Monitoring

- AWS Cloudwatch
- Pingdom / NewRelic
- Sentry as our error logger
- LogRocket as our session replay tool
- We're working on a better logging system! (i.e. Logly, Logstash/ELK)

---

## Frontend Stack

![](assets/frontend.jpg)

---

## How Code Gets Deployed

![](assets/ansible.png)

+++

### Breaking Down the Process

- Developers make feature branches
- Passes CI automated tests and human code review
- Code is merged into a hotfix/release branch or master
- Changes are live on staging and go through several (automated & human-tested) QA rounds

+++

- Release is merged into master
- `git pull` on Update (the dev-facing production servers)
- A blueprint (an image, or AWS AMI) of staging is made
- Using the blueprint, we then launch an Auto Scaling Group with as many (client-facing) production instances as needed

+++

![](assets/blue-green.jpg)

+++

### Blue-green Deployment

- Also known as immutable or rolling deployment
- Once the new set of instances (green) is ready, we register it behind the ELB
- At the same time, we deregister the old set (blue)
- Minimal downtime, if any, thanks to the one and only routing switch

---

## Developer Access

- An SSH bastion account to connect to the database (and various servers)
- Github accounts to contribute code
- Quorum accounts (dev/prod)
- Sentry for error logging
- AWS accounts, if needed for a project
- IMPORTANT: please turn on 2FA for all of your Quorum accounts

+++

- Authenticating to bastion/db is always the first step
- IP-limited access to all non-client-facing servers
- Needs to access Quorum from home? VPN!

---

## What We Talked About

- Overview of what happens when you go to quorum.us
- Quorum's scalable infrastructure
- Our stack and where we spend most of our time
- Brief intro to deployment
- Accounts & access

---

## Questions?

Thanks!