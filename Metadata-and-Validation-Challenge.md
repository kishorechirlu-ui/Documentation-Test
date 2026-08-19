# Task 3: Metadata and Validation Challenge

## 1. Fixed Metadata Block

```yaml
---
title: StackSync AI Connector
description: Learn how to configure and deploy the StackSync AI Connector within your StackGen pipeline.
ai_index: true
clusters:
  - stackbuilder
  - ai-connectors
read_time: 5 min read
---
```

## 2. Field Explanations

1. **`ai_index`**: Controls whether the document is ingested and indexed by internal AI search engines, RAG pipelines, and assistant bots within the StackGen ecosystem.
2. **`clusters`**: Defines the functional domain categories that group related documentation together for semantic search routing and visual topic aggregation.
3. **`read_time`**: Provides user-facing estimated reading time on the documentation UI while strictly adhering to the mandatory `\d+ min read` schema pattern required by the build validator.
