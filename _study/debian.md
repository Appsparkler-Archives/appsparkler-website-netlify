---
layout: post
title: Debian
categories: study debian
---

### :whale: How to change color of bash?
- Reference Link: [https://wiki.debian.org/BashColors](https://wiki.debian.org/BashColors)
- Add the following code to the `~/.bashrc` file:
  ```bash
  export LS_OPTIONS='--color=auto'
  eval "`dircolors`"
  alias ls='ls $LS_OPTIONS'
  ```
- Apply changes by executing the following command : 
  * `source /etc/bash.bashrc; source ~/.bashrc`
  * OR
  * `exec bash`
- Check if out is in colors now with `ls`

