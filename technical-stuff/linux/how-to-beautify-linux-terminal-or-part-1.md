# How to Beautify Linux Terminal \| Part 1

## For Normal Users

add the following line at the end of `/home/UserName/.bashrc` file.

```bash
PS1='\[\033[01;32m\]\u@\h\[\033[00m\] \[\033[01;34m\]\W\[\033[00m\]\\$ '
```

or

```bash
PS1='\[\033[01;32m\]\u@\h\[\033[00m\] \[\e[1m\e[97m\]( \[\033[01;34m\]\W\[\033[00m\] \[\e[1m\e[97m\])\[\033[01;32m\]-> \[\e[m\]\[\e[0;37m\]'
```

## For root user

add the following line at the end of `/root/.bashrc` file.

```bash
PS1='\[\e[0;31m\]\u@\h\[\e[m\] \[\e[1;34m\]\W\[\e[m\] \[\e[0;31m\]\$ \[\e[m\]\[\e[0;37m\]'
```

or

```bash
PS1='\[\e[0;31m\]\u@\h\[\e[m\] \[\e[1m\e[97m\]( \[\e[1;34m\]\W\[\e[m\]\[\e[1m\e[97m\] )\[\e[0;31m\]-> \[\e[m\]\[\e[0;37m\]'
```

