---
layout: blog
title: Couchbase
tags: Couchbase
---

### GET all results without nesting in bucket name:
```sql
SELECT t.*
FROM `<bucketname>` t
WHERE t.id
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
WHERE t.id="<id-on-t>" AND primaryTag.id="<id-on-a-primary-tag>"
```

### DELETE items
```sql
DELETE
FROM `tesla-cms`
WHERE id
```

### UPDATING a nested object
```sql
UPDATE `<bucket-name>`

SET nestedItem.status="new-status"

FOR nestedItem in items
 WHEN nestedItem.id IN ["item-1-id","item-2-id"]
END

WHERE type="abcd"
```

### SELECT
This query utilizes a dummy scan to generate the projection:
```sql
SELECT
  "USER::001" AS _k,
  {
    "firstName": "John",
    "lastName": "Smith",
    "id": "001",
    "type": "user"
  } AS _v
```

### CREATING PRIMARY INDEX
This query will create a `primary-index` on bucket named `default`.
```sql
CREATE PRIMARY INDEX `default-primary-index` ON default
```
