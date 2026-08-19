---
title: StackSync AI Connector
description: Explain how to set up and monitor StackSync AI Connector in StackBuilder.
read_time: 4 min read
customFields:
  ai_index: true
  audience:
    - developer
    - DevOps
  product_version: '1.0'
---

# StackSync AI Connector

## Overview

The StackSync AI Connector synchronizes configuration changes from **appStack** to **Cloud2Code**, keeping downstream deployments aligned with the config source of truth. It fits into the StackBuilder platform as the integration layer between appStack (where configs are authored/changed) and Cloud2Code (where those configs are consumed).

Sync is triggered asynchronously through a webhook rather than on a fixed schedule or manual poll. Because the trigger is event-driven and async, syncs do not always fire immediately or consistently for every config change - this is a known current limitation of the connector.

## Set Up and Usage

1. Ensure your appStack project has the StackSync AI Connector enabled for the environment you want to sync.
2. Configuration changes made in appStack are picked up by an async webhook trigger, which pushes the change toward Cloud2Code. There is no manual "push" step required once the webhook is configured.
3. Monitor sync activity from **StackBuilder**, which is expected to surface sync status. *(This is based on early product guidance and should be confirmed - see Assumptions below.)*
4. To manually trigger a sync from the UI, use the sync action button. Note: this button is currently labeled **Sync Now** and will be renamed to **Run AI Sync** in the next release - update any screenshots or step-by-step instructions referencing the button label after that release ships.

> **Note:** Sync log location has not yet been confirmed. This section will be updated once logging access (UI panel, CLI, or log aggregator) is finalized.

## Troubleshooting

**Sync fails with a metadata error**
Sync failures are commonly caused by an invalid or incomplete `metadata.json` file. Before triggering a sync, confirm the file includes all required fields.

**Missing required fields (`ai_index`, `clusters`)**
If `metadata.json` is missing either the `ai_index` or `clusters` field, the sync will error out. This is reported as a frequent, recurring failure cause — validate both fields are present and non-empty before syncing.

**Sync appears "stuck" or doesn't fire**
Because the trigger is an async webhook, a sync may not fire immediately after a config change. If a sync hasn't appeared after a reasonable wait, check the `metadata.json` fields above first, then verify the webhook trigger itself is reachable/configured correctly.

## Try It Out

```bash
cloud2code import \
  --source <APPSTACK_PROJECT_ID> \
  --config <PATH_TO_METADATA_JSON> \
  --cluster <CLUSTER_NAME> \
  --ai-index <AI_INDEX_NAME>
```

Replace each placeholder with your project's values. `<PATH_TO_METADATA_JSON>` must point to a `metadata.json` file that includes both `ai_index` and `clusters`, or the import will fail.

