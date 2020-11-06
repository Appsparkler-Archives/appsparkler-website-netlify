---
layout: blog
title: Couchbase
tags: Couchbase
---

### GET all results without nesting in bucket name:
```sql
SELECT t.*
FROM `<bucketname>` t
WHERE id
```

### GET deep nested results with `UNNEST`:
```sql
SELECT t.*
FROM `<bucketName>` as t
UNNEST t.primaryTags primaryTag
WHERE t.id="<id-on-t>" AND primaryTag="<id-on-a-primary-tag>"
```
