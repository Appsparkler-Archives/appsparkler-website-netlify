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
Example Data:
```json
{
  "id": "1234-abcd",
  "primaryTags": [
    {"id": "12-primary-tag"},
    {"id": "24-primary-tag"}
  ]
}
```
```sql
SELECT t.*
FROM `<bucketName>` t
UNNEST t.primaryTags primaryTag
WHERE t.id="<id-on-t>" AND primaryTag="<id-on-a-primary-tag>"
```

### DELETE items
```sql
DELETE
FROM `tesla-cms`
WHERE id
```
