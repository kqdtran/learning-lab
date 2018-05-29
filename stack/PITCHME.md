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

---

## What Happens When...?

- Based on the age-old interview question, what happens when you type google.com
- (We'll skip the key-pressed events / browser magic that we don't control)

+++

## At a Glance

- DNS Lookup (quorum.us => 12.34.56.789)
- Elastic Load Balancer & Requests Routing
- Application Server (Nginx, Gunicorn, etc.)
- Database (PostgreSQL)

+++?image=assets/quorum_stack.png&size=auto 90%

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

## Infrastructure (end)

- So far, lots of buzzwords and braindumps
- Questions?

---

## Backend Stack

- Python 2.7 :( -- we have 3 years
- Django 1.10 (soon to be on 1.11)
- PostgreSQL 10
- Nginx / Gunicorn
- Supervisor to watch all of the above (bar Postgres)

+++

### AWS

- EC2 as our web servers / instances on Ubuntu 14.10
- RDS as our database
- S3 for file storage
- Cloudfront (CDN) for static files
- Cloudwatch for alerts & monitoring
- ...

+++

### Servers

- 2+ production (client-facing) instances
- 2 production (dev-facing) servers to process data (Update, State Update)
- Various crawler servers
- Proxies
- An SSH bastion server that sits in front of our servers and the database

+++

### DevOps

- Primarily in Ansible
- Configures servers, installs packages, monitors instances, etc.
- Is essential to our deployment pipeline (more later)
- CI/CD: Shippable, CodeFactor

---

## Frontend Stack

- TODO
- Need Jack's halp

---

## How Code Gets Deployed

- TODO

---

## Developer Access

- tail -f to see running log
- Find a pattern with `grep` or `ag`
- Combine together to see only items relevant to you

+++

## sed

- `sed -n 16224,16240p filename`

+++

## csv

- Manipulating csv with `cut` and `sort`

```
1111,2222,3333,4444
aaaa,bbbb,cccc,dddd

$ cut --complement -f 3 -d, inputfile
1111,2222,4444
aaaa,bbbb,dddd

$ cut -d , -f 1-2,4-, inputfile
```

---

## What else?

- vim/tmux living in terminal
- regular expression! power up `sed` and `awk`

---

## Questions?

Thanks!