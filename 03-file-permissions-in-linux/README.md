# File Permissions in Linux

**Course:** Google Cybersecurity Professional Certificate — Course 4: Tools of the Trade: Linux and SQL

## Project Description

As a security professional, it is our job to ensure authorized users have appropriate permissions so that the system stays secure. After examining the existing permissions on the `/home/researcher2/projects` directory, some files had more access granted than necessary, while others didn't have the access they needed. Using Linux commands through the Bash shell, the permissions were modified so that appropriate users had the correct authorization and any unnecessary access was removed.

## Check File and Directory Details

```
researcher2@e88222ccf0f0:~$ pwd
/home/researcher2
researcher2@e88222ccf0f0:~$ cd projects/
researcher2@e88222ccf0f0:~/projects$ ls -la
total 32
drwxr-xr-x 3 researcher2 research_team 4096 Oct  8 08:26 .
drwxr-xr-x 3 researcher2 research_team 4096 Oct  8 09:15 ..
-rw--w---- 1 researcher2 research_team   46 Oct  8 08:26 .project_x.txt
drwx--x--- 2 researcher2 research_team 4096 Oct  8 08:26 drafts
-rw-rw-rw- 1 researcher2 research_team   46 Oct  8 08:26 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Oct  8 08:26 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct  8 08:26 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct  8 08:26 project_t.txt
researcher2@e88222ccf0f0:~/projects$
```

- Changed directory into the `projects` directory.
- Listed all files and directories under `projects` using `ls -la` — the `-l` flag displays a detailed listing of all files/directories and their ownership permissions, and the `-a` flag shows hidden files as well.
- The output shows one hidden file, one subdirectory, and four regular text files, each with its permissions listed.

## Describe the Permissions String

Taking `project_m.txt` as an example, its permissions are represented by the 10-character string `-rw-r-----` from the `ls -la` output:

- **1st character** is `-`, which indicates it is a file, not a directory.
- **2nd, 3rd, 4th characters** are `rw-`, which indicates the user (owner) has read and write permission.
- **5th, 6th, 7th characters** are `r--`, which indicates the group has only read permission.
- **8th, 9th, 10th characters** are `---`, which indicates other users have no read, write, or execute permissions on that file.

## Change File Permissions

The organization does not allow others (users outside the owner and group) to have write access to any file. `project_k.txt` was found with write permission granted to others:

```
-rw-rw-rw- 1 researcher2 research_team   46 Oct  8 04:50 project_k.txt
```

```
researcher2@e88222ccf0f0:~/projects$ chmod o-w project_k.txt
researcher2@e88222ccf0f0:~/projects$ ls -l
total 20
drwx--x--- 2 researcher2 research_team 4096 Oct  8 08:26 drafts
-rw-rw-r-- 1 researcher2 research_team   46 Oct  8 08:26 project_k.txt
-rw-r----- 1 researcher2 research_team   46 Oct  8 08:26 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct  8 08:26 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct  8 08:26 project_t.txt
researcher2@e88222ccf0f0:~/projects$
```

- The permission of `project_k.txt` was changed using `chmod o-w project_k.txt`. This removes write access from "other" users specifically, without touching the user's or group's permissions. Re-listing the directory confirms `project_k.txt` no longer has write access for other users — visible as `-rw-rw-r--` in the updated listing.

## Change File Permissions on a Hidden File

The research team has archived `.project_x.txt`, which is why it's a hidden file (hidden files in Linux start with a period). This file should not have write permissions for anyone, but the user and group should both be able to read it:

```
-rw--w---- 1 researcher2 research_team   46 Oct  8 04:50 .project_x.txt
```

```
researcher2@e88222ccf0f0:~/projects$ chmod u-w,g-w,g+r .project_x.txt
researcher2@e88222ccf0f0:~/projects$ ls -la
total 32
drwxr-xr-x 3 researcher2 research_team 4096 Oct  8 08:26 .
drwxr-xr-x 3 researcher2 research_team 4096 Oct  8 09:15 ..
-r--r----- 1 researcher2 research_team   46 Oct  8 08:26 .project_x.txt
drwx--x--- 2 researcher2 research_team 4096 Oct  8 08:26 drafts
-rw-rw-r-- 1 researcher2 research_team   46 Oct  8 08:26 project_k.txt
-rw------- 1 researcher2 research_team   46 Oct  8 08:26 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct  8 08:26 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct  8 08:26 project_t.txt
researcher2@e88222ccf0f0:~/projects$
```

- Permissions on `.project_x.txt` were changed using `chmod u-w,g-w,g+r .project_x.txt`. Breaking this down: `u-w` removes write access for the user (owner), `g-w` removes write access for the group, and `g+r` adds read permission to the group.
- Confirmed using `ls -la` — line 3 of the updated listing shows the hidden file now has only read permission for both the user and the group (`-r--r-----`), with no write access for anyone.

## Change Directory Permissions

The files and directories in the `projects` directory belong to the `researcher2` user. Only `researcher2` should be allowed to access the `drafts` directory and its contents — but the group currently has execute access:

```
drwx--x--- 2 researcher2 research_team 4096 Oct  8 04:50 drafts
```

```
researcher2@e88222ccf0f0:~/projects$ chmod g-x drafts
researcher2@e88222ccf0f0:~/projects$ ls -l
total 20
drwx------ 2 researcher2 research_team 4096 Oct  8 08:26 drafts
-rw-rw-r-- 1 researcher2 research_team   46 Oct  8 08:26 project_k.txt
-rw------- 1 researcher2 research_team   46 Oct  8 08:26 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct  8 08:26 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Oct  8 08:26 project_t.txt
researcher2@e88222ccf0f0:~/projects$
```

- `chmod g-x drafts` was used to remove execute access for the group. On a directory, execute permission controls whether a user can enter/traverse it — so removing it from the group prevents group members from accessing `drafts` or its contents, leaving only `researcher2` (the owner) with access.
- Confirmed using `ls -l` — line 1 now shows `drwx------`, meaning only the owner retains read, write, and execute permissions.

## Summary

After reviewing the permissions of the files and directory, changes were made so that there is no write access to any file for other users, write access was removed (and read access added) on the hidden file, and execute permission was removed for the group on the `drafts` subdirectory. By modifying these permissions, authorized users retain appropriate access while unauthorized access is removed — keeping the system secure.

---
📄 [View original document](Portfolio%20Activity%203.pdf)

*Part of [security-projects](../).*
