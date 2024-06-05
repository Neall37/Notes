- [Introduction to Linux](#introduction-to-linux)
- [Group & File management](#group---file-management)
  * [Workflow](#workflow)
  * [Details](#details)
    + [Create a group](#create-a-group)
    + [Change the ownership of files](#change-the-ownership-of-files)
      - [Owner and group:](#owner-and-group-)
      - [Only group:](#only-group-)
- [Python in VScode ssh](#python-in-vscode-ssh)

# Introduction to Linux
- Intro to Ubuntu(Linux): https://ubuntu.com/tutorials/command-line-for-beginners#1-overview
- Common command lines: https://www.hostinger.com/tutorials/linux-commands

**Be cautious when you're deleting files, since deletion is irreversible in Linux!!!**
# Group & File management
## Workflow
- **Create a new group**: You can create a new group using the `groupadd` command. For example, `groupadd mygroup`.
- **Add users to the group**: You can add users to the group using the `usermod` command. For example, `usermod -a -G mygroup user1 user2`.
- **Change the group ownership of a file or directory**: You can change the group ownership of a file or directory using the `chown` command with the `:group` syntax. For example, `chown :mygroup file.txt` or `chown :mygroup /path/to/directory`.
- **Set group permissions**: After changing the group ownership, you need to set the appropriate permissions for the group. This is done using the `chmod` command. For example, to give read and write permissions to the group, you can use `chmod g+rw file.txt` or `chmod g+rw /path/to/directory`. https://en.wikipedia.org/wiki/Chmod

## Details
### Create a group
Create group: `$ sudo groupadd -g 1009 demo`
1009: group ID

Add user: `$ sudo usermod -aG demo user2`

https://www.redhat.com/sysadmin/linux-groups

### Change the ownership of files

#### Owner and group:
`chown [options] [new_owner][:new_group] [file/directory]`

- both: `chown master:group1 file1.txt`
- group: `chown :group1 file1.txt`
- owner: `chown -c master file1.txt`

More details: https://www.geeksforgeeks.org/chown-command-in-linux-with-examples/

#### Only group:
`chgrp [group_name] [file/directory]`

# Python in VScode ssh
- How to connect server in VScode: https://hackmd.io/@MingRuey/HJOJ30ajO
- Manage virtual environment: https://code.visualstudio.com/docs/python/environments
