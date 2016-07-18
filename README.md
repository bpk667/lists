# auditd_notes



# Hardening environment
```
#Change attributes to append only
  chattr +a .sh_history
  chattr +a .bash_history

#Protect variables
export HISTCONTROL=
export HISTFILE=$HOME/.bash_history
export HISTFILESIZE=2000
export HISTIGNORE=
export HISTSIZE=1000
export HISTTIMEFORMAT="%a %b %Y %T %z "

typeset -r HISTCONTROL
typeset -r HISTFILE
typeset -r HISTFILESIZE
typeset -r HISTIGNORE
typeset -r HISTSIZE
typeset -r HISTTIMEFORMAT

#For bash:
  shopt -s cmdhist
  shopt -s histappend

  PROMPT_COMMAND="history -a"
  typeset -r PROMPT_COMMAND
```

#EUID trace
```
$ set |grep -i uid
EUID=500
UID=500

$ sudo su -
# set |grep -i uid
EUID=0
UID=0

$ sudo su
# set |grep -i uid
EUID=0
SUDO_UID=500
UID=0

$ sudo bash
# set |grep -i uid
EUID=0
SUDO_UID=500
UID=0
```

#audit.rules
```
-a exit,always -F arch=b32 -S execve
-a exit,always -F arch=b64 -S execve
-a always,exclude -F msgtype=PATH
-a always,exclude -F msgtype=BPRM_FCAPS
-a always,exclude -F msgtype=USER_START
```
