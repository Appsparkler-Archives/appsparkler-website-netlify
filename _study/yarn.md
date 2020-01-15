---
layout: post
title: Yarn
categories: study yarn
---

### CACHE
- CLEAN cache - `yarn cache clean`
- LIST cache dir - `yarn cache dir`

### YarnRC (`.yarnrc`)
- OFFLINE installations
  - ADD the following configs to `.yarnrc`
    - `yarn-offline-mirror "<path/to/dir>` ex. `yarn-offline-mirrow "C:\\my-drive\\yarn-offline-packages"`
    - `yarn-offline-mirror-pruning true`
  - ENSURE the project has a `yarn.lock` file
  - CLEAN `yarn cache` with `yarn cache clean`
  - INSTALL offline `yarn --offline`
  
