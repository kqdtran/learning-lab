---

## Unix and Log Reading

### Khoa Tran

---

## Agenda

- Basic *nix
- Aliases
- Processes
- ssh, scp, and permissions
- Reading and digesting logs
- Questions?

---

## Basic \*nix

- pwd, cd, ls, rm, mv
- more/less, head/tail to view files
- touch/cat/echo to create/print/write to file
- man / tldr: view the man-ual for a certain command

+++

## History

- history | more
- `export HISTTIMEFORMAT='%F %T '` to see timestamp
- Ctrl + R to search thru history
- !! or Ctrl + P to execute last command
- !X to execute commands at X position in history

+++

## Wildcard and Redirection

- rm -rf ~/*
- < redirect from stdin
- > redirect from stdout, replacing existing content
- >> redirect from stdout, appending after existing content

+++

## Pipe

- Redirect the output of one command into another
- ls -l | grep ^d | wc -l
- Print the number of subdirectories in the current directory
- Combining tail and grep can be very powerful for reading logs

---

## Aliases

- pew pew