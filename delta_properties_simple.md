# Delta Lake Properties - Quick Reference

## Properties You Can Use in CREATE TABLE

| Property | What It Does | Default | Certification ✅ |
|----------|--------------|---------|-----------------|
| `delta.autoOptimize.optimizeWrite` | Auto-compact files during write | false | ✅ |
| `delta.autoOptimize.autoCompact` | Auto-compact after write | false | ✅ |
| `delta.enableChangeDataFeed` | Track INSERT/UPDATE/DELETE changes | false | ✅ |
| `delta.deletedFileRetentionDuration` | How long to keep deleted files (VACUUM) | interval 7 days | ✅ |
| `delta.logRetentionDuration` | Time travel history limit | interval 30 days | ✅ |
| `delta.columnMapping.mode` | Enable column rename/drop | none | ✅ |
| `delta.enableDeletionVectors` | Fast deletes without rewriting files | false | ✅ |
| `delta.appendOnly` | Prevent UPDATE/DELETE operations | false | ✅ |
| `delta.checkpointInterval` | Create checkpoint every N commits | 10 | ✅ |
| `delta.dataSkippingNumIndexedCols` | Number of columns to collect stats | 32 | |
| `delta.minReaderVersion` | Minimum protocol to read table | 1 | ✅ |
| `delta.minWriterVersion` | Minimum protocol to write table | 2 | ✅ |

---

## Properties You Can Use in ALTER TABLE

| Property | What It Does | Common Values |
|----------|--------------|---------------|
| `delta.autoOptimize.optimizeWrite` | Turn on/off auto-optimize write | true / false |
| `delta.autoOptimize.autoCompact` | Turn on/off auto-compact | true / false |
| `delta.enableChangeDataFeed` | Turn on/off change tracking | true / false |
| `delta.deletedFileRetentionDuration` | Change VACUUM retention | interval 0 hours / interval 7 days / interval 30 days |
| `delta.logRetentionDuration` | Change time travel limit | interval 7 days / interval 30 days / interval 90 days |
| `delta.columnMapping.mode` | Enable column operations | none / name |
| `delta.enableDeletionVectors` | Turn on deletion vectors | true / false |
| `delta.appendOnly` | Make table append-only | true / false |
| `delta.checkpointInterval` | Change checkpoint frequency | 5 / 10 / 20 |
| `delta.minReaderVersion` | Upgrade reader version | 1 / 2 / 3 |
| `delta.minWriterVersion` | Upgrade writer version | 2 / 3 / 4 / 5 / 6 / 7 |

---

## Properties You Can Use While WRITING (df.write.option)

| Property | What It Does | Values |
|----------|--------------|--------|
| `mergeSchema` | Add new columns during write | true / false |
| `overwriteSchema` | Replace entire schema | true / false |
| `replaceWhere` | Replace specific data only | "year = 2024" / "month = 1" |
| `delta.autoOptimize.optimizeWrite` | Auto-compact this write only | true / false |

---

## Properties You Can Set in SPARK CONF (spark.conf.set)

| Property | What It Does | Values |
|----------|--------------|--------|
| `spark.databricks.delta.optimizeWrite.enabled` | Enable auto-optimize write globally | true / false |
| `spark.databricks.delta.autoCompact.enabled` | Enable auto-compact globally | true / false |
| `spark.sql.sources.partitionOverwriteMode` | Partition overwrite behavior | static / dynamic |
| `spark.databricks.delta.properties.defaults.enableChangeDataFeed` | Default CDF for new tables | true / false |
| `spark.databricks.delta.vacuum.parallelDelete.enabled` | Speed up VACUUM | true / false |

---

## Feature Requirements (Protocol Versions)

| Feature | Requires |
|---------|----------|
| Basic Delta | Reader v1, Writer v2 |
| CHECK Constraints | Writer v3 |
| Change Data Feed | Writer v4 |
| Column Mapping | Reader v2, Writer v5 |
| Identity Columns | Writer v6 |
| Deletion Vectors | Reader v3, Writer v7 |

---

## Important Default Values (Memorize for Certification)

| Property | Default Value |
|----------|--------------|
| `delta.deletedFileRetentionDuration` | 7 days |
| `delta.logRetentionDuration` | 30 days |
| `delta.checkpointInterval` | 10 commits |
| `delta.minReaderVersion` | 1 |
| `delta.minWriterVersion` | 2 |
| `delta.dataSkippingNumIndexedCols` | 32 |
| `partitionOverwriteMode` | static |

---

## Quick Use Case Guide

| If You Need... | Use This Property |
|----------------|-------------------|
| Faster writes with many small files | `delta.autoOptimize.optimizeWrite` = true |
| Automatic file compaction | `delta.autoOptimize.autoCompact` = true |
| Track data changes (CDC) | `delta.enableChangeDataFeed` = true |
| Rename/drop columns easily | `delta.columnMapping.mode` = name |
| Fast deletes on large tables | `delta.enableDeletionVectors` = true |
| Prevent accidental deletes | `delta.appendOnly` = true |
| Clean up old files | `delta.deletedFileRetentionDuration` = interval X days |
| Time travel further back | `delta.logRetentionDuration` = interval X days |
| Update only specific partitions | `replaceWhere` = "condition" |
| Add columns during write | `mergeSchema` = true |
| Overwrite partition smartly | Set conf: `partitionOverwriteMode` = dynamic |

---

## Summary Table: Where Can You Use Each Property?

| Property | CREATE | ALTER | WRITE | CONF |
|----------|--------|-------|-------|------|
| `delta.autoOptimize.optimizeWrite` | ✅ | ✅ | ✅ | ✅ |
| `delta.autoOptimize.autoCompact` | ✅ | ✅ | | ✅ |
| `delta.enableChangeDataFeed` | ✅ | ✅ | | ✅ |
| `delta.deletedFileRetentionDuration` | ✅ | ✅ | | |
| `delta.logRetentionDuration` | ✅ | ✅ | | |
| `delta.columnMapping.mode` | ✅ | ✅ | | |
| `delta.enableDeletionVectors` | ✅ | ✅ | | |
| `delta.appendOnly` | ✅ | ✅ | | |
| `delta.checkpointInterval` | ✅ | ✅ | | |
| `mergeSchema` | | | ✅ | |
| `overwriteSchema` | | | ✅ | |
| `replaceWhere` | | | ✅ | |
| `partitionOverwriteMode` | | | | ✅ |
