---
draft: true
date: 2024-04-05
categories:
  - Linux
authors:
  - junho
---

A Linux Primer

<!-- more -->


# Linux Commands

- [`curl`](#curl)

## Permissions

```sh
ls -l
    drwxr-xr-x. 4 root root    68 Jun 13 20:25 tuned
    -rw-r--r--. 1 root root  4017 Feb 24  2022 vimrc
```

- File type: - or d
- Permission settings: rw-r--r--
- Extended attributes: dot (.)
- User owner: root
- Group owner: root
- Others
    - First, it checks if you are the file's `owner`. If so, you get the owner's permissions.
    - If not, it checks if you belong to the file's `group`; if so, you get the group's permissions.
    - If neither, "others" permissions apply. These fields are mutually exclusive, so you can't be covered by more than one.

[↑ Back to top](#)
<br><br>


## curl

```sh
curl https://assets.digitalocean.com/articles/command-line-intro/verne_twenty-thousand-leagues.txt

# output to a file
curl -O https://assets.digitalocean.com/articles/command-line-intro/verne_twenty-thousand-leagues.txt
ls verne_twenty-thousand-leagues.txt

# output to a specific filename
curl -o jules.txt https://assets.digitalocean.com/articles/command-line-intro/verne_twenty-thousand-leagues.txt
```