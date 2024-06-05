- [Introduction to Linux](#introduction-to-linux)
- [Group & File Sharing](#group---file-sharing)
  * [Create a group for users](#create-a-group-for-users)
  * [Setting file/directory permissions](#setting-file-directory-permissions)
  * [Change the ownership](#change-the-ownership)
    + [Owner and group:](#owner-and-group-)
    + [Only group:](#only-group-)
- [Python in VScode ssh](#python-in-vscode-ssh)

# Introduction to Linux
- Intro to Ubuntu(Linux): https://ubuntu.com/tutorials/command-line-for-beginners#1-overview
- Common command lines: https://www.hostinger.com/tutorials/linux-commands

==Be cautious when you're deleting files, since deletion is irreversible!!!==
## Group management
Create group: `$ sudo groupadd -g 1009 demo`
1009: group ID

Add user: `$ sudo usermod -aG demo user2`

https://www.redhat.com/sysadmin/linux-groups
## Setting file/directory permissions

`chmod [permissions] [file/directory]`

How to set permissions: https://en.wikipedia.org/wiki/Chmod

For example, `754` would allow:
- "read" (4), "write" (2), and "execute" (1) for the _User_ class; i.e., 7 (4 + 2 + 1).
- "read" (4) and "execute" (1) for the _Group_ class; i.e., 5 (4 + 1).
- Only "read" (4) for the _Others_ class.

## Change the ownership

### Owner and group:
`chown [options] [new_owner][:new_group] [file/directory]`

- both: `chown master:group1 file1.txt`
- group: `chown :group1 file1.txt`
- owner: `chown -c master file1.txt`

More details: https://www.geeksforgeeks.org/chown-command-in-linux-with-examples/

### Only group:
`chgrp [group_name] [file/directory]`

# Python in VScode ssh
- How to connect server in VScode: https://hackmd.io/@MingRuey/HJOJ30ajO
- Manage virtual environment: https://code.visualstudio.com/docs/python/environments
