---

## Quorum's Tech Stack

### Khoa Tran

---

## What We'll Cover

- What happens when you type quorum.us in the browser?
- Infrastructure
- Quorum's backend and frontend stack
- Developer access to Quorum servers
- How code gets deployed
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

+++

![](https://i.imgur.com/G8IunsV.png)

+++

## Load Balancing & Auto-scaling

- Distributes load across instances
- Monitors the "health" of an instance
- Auto-scales to meet demand and increase throughput
- Scale out under high CPU or high memory
- Scale in (min 2) under low CPU and low memory
- Why 2? Redundancy & failure tolerance

+++

## Application Server (nginx)

- nginx: a reverse proxy configured with HTTPS certs
- Redirects HTTP => HTTPS
- Can handle static files (ours are served via CloudFront instead)
- Passes off the requests to Gunicorn workers

+++

## Application Server (gunicorn)

- Redirect the output of one command into another
- `ls -l | grep ^d | wc -l`
- Print the number of subdirectories in the current directory
- Combining tail and grep can be very powerful for reading logs

---

## Bash Aliases and Environment Variables

- alias short = 'LONG COMMAND', e.g. .. = 'cd ..'
- For lasting effect, put in ~/.bash_aliases or ~/.bash_profile
- Similarly, export VAR = 'value'
- `echo $VAR`
- Sourcing with `source`

+++

## Git Aliases

- git alias new_cmd = 'LONG COMMAND'
- Better, put in ~/.gitconfig

```
[alias]
    st = status
    cl = log --pretty --date=relative
```

- I'm lazy, so I use Bash aliases, e.g. `alias st = git status`

+++

## (Z)umping around

- z https://github.com/rupa/z
- ag == find+grep on steroid

---

## Processes

- ps
- psaux on Update
- kill and pkill

+++

## Foreground & Background

- Ctrl+C to terminate
- Ctrl+Z to suspend
- fg, bg, jobs, disown %1 OR nohup

+++

![](https://i.imgur.com/XyPyVUp.png)

---

## SSH, SCP, and SFTP

- username/password or public-private keypair
- `scp file server:/path/on/server`

+++

## Permissions

- `ls -lah` to see details
- `chown` changes owner
- `chgrp` changes groups
- `chmod` changes permission
- 4: read, 2: write, 1: execute
- What's 660? How about 744?

---

## Reading logs and csvs

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