# 7. DoRA Deploy Frequency and Lead time to deploy

Date: 2026-04-22

## Status

Accepted

## Context

To improve our delivery performance and organizational health, we need to track DORA (DevOps Research and Assessment) metrics, specifically Lead Time for Changes. Currently, tasks are managed primarily via GitHub Issues, with potential expansion to Jira. We need a tool-agnostic definition of checkpoints to ensure consistent measurement regardless of the underlying task management system.

## Decision

We will define and track the following checkpoints as state transitions. These events must be captured and stored in a centralized data warehouse (e.g., BigQuery, Athena) to calculate granular lead times.

### 1. Development Task Checkpoints

|Checkpoint|Event Trigger|Description|
|----------|-------------|-----------|
|**Intake Completed**|Label: intake completed added|The task is refined, estimated and ready for a developer|
|**Development Started**|Label: in progress added|A developer has actively started working on the task.|
|**Review Started**|PR created / Label changed|Code is submitted for peer review.|
|**Review Completed**|PR approved / merged|Peer review is finished, and the code is merged to the main branch.|
|**Issue Closed**|Issue status set to Closed|The specific development task is technically finished.|

### 2. Release Pipeline Checkpoints

These stages track the path from "code complete" to "value delivered to customers."

|Checkpoint|Event Trigger|Description|
|----------|-------------|-----------|
|**Release Created**|Tag/Release created|A release candidate or version tag is generated|
|**Deployed to QA**|Deployment event(QA)|The code is deployed to the staging/QA environment for testing.|
|**Deployed to Prod**|Deployment event(Prod)|The code is deployed to the production environment.|
|**Release Completed**|Post-deploy check success|Verification (A/B testing, Canary analysis) is finished successfully.|

## Consequences

**Granular Bottleneck Analysis**: We can now distinguish between "Time spent in Backlog" vs. "Active Coding Time" vs. "Release Overhead."

**Tool Agnosticism**: By defining these based on labels and events rather than tool-specific features, we can integrate both GitHub and Jira data into the same schema.

**Infrastructure Requirement**: A system (Webhooks + Database) must be implemented to capture these timestamps at the moment they occur, as retrospective API calls may not always provide accurate transition history.

## Metrics to be Derived

**Development Lead Time**: Issue Closed - Development Started

**Intake Latency**: Development Started - Intake Completed

**Deployment Lead Time**: Release Completed - Issue Closed

**Total Delivery Lead Time**: Release Completed - Intake Completed