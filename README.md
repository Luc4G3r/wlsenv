# wlsenv
_____
Instructions for various tasks in WSL2 development stacks.

## WSLENV
WSLENV serves the purpose of sharing variables between Windows and WSL2 environments. [See Microsoft page](https://devblogs.microsoft.com/commandline/share-environment-vars-between-wsl-and-windows/)

## Permanent share
To permanently share an env var from WSL2 to Windows, I found the only option to be a windows command running on startup containing a `wsl source` command which writes to a text file and then read the file content to a windows env var via `SETX ENV_VAR /F "{{PATH}}" /A 0,0`  
This might look like this:
```
@echo off
wsl source /etc/custom_commands/start_ssh_agent.sh
SETX SSH_AUTH_SOCK /F "C:\Users\Luca\Documents\utility\resources\current_auth_sock.txt" /A 0,0
```
Translating paths from wsl2 to windows can be done via `wslpath` command
