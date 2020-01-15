---
layout: post
title:  Docker
date:   2019-10-18 12:40:47 -0500
categories: study docker
---
### Docker volume
- REMOVE all volumes - `docker volume rm $(docker volume ls -q)`

### Docker Compose
- EXECUTING multi-line script instead of single line in `command`:
  1. ADD a file to serve as an **entrypoint** - ex. `docker-entrypoint.sh`
  2. ADD `entrypoint` key under any service pointing to the file added in 1.
  3. [Stackoverflow Reference Link](https://stackoverflow.com/questions/30063907/using-docker-compose-how-to-execute-multiple-commands)
