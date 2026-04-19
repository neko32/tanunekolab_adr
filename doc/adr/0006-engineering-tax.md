# 6. engineering tax

Date: 2026-04-19

## Status

Accepted

## Context

Our current systems are operating stably; however, we acknowledge that technology and knowledge are subject to **continuous depreciation and entropy**. Maintaining a "static" stability without proactive updates leads to:

**Technological Debt**: Accumulation of interest that slows down future feature delivery.

**Skill Decay**: Narrowing the team's ability to respond to modern security threats or performance requirements.

**Risk of Catastrophic Failure**: The gap between our legacy stack and the modern ecosystem increases the Mean Time to Repair (MTTR) during unforeseen outages.

We need a systematic way to reinvest in our foundation to ensure Dynamic Stability.

## Decision

We will implement an **"Engineering Tax" of 20%** of total engineering capacity. This resource is strictly dedicated to:

**Refactoring and Modernization**: Updating libraries, improving code modularity, and decommissioning legacy components.

**Infrastructure Resilience**: Enhancing observability, CI/CD pipelines, and automated testing.

**Knowledge Refresh**: Investigating new technologies to prevent the "Red Queen Hypothesis" effect (running just to stay in place).

### Quantified Allocation (Per Engineer)

Based on a standard 160-hour month:

**Total Capacity**: 160 hours

**Engineering Tax (20%)**: 32 hours/month (Approx. 1 day per week or 1.6 hours per day)

**Feature Delivery**: 128 hours/month

## Consequences

### Positive (Gains)

Reduced Interest: Lower long-term maintenance costs by addressing issues before they compound.

Higher Velocity: Cleaner codebases allow for faster onboarding and quicker feature pivots.

Talent Retention: Engineers remain engaged and motivated by working with modern, sustainable practices.

### Negative (Trade-offs)

**Immediate Feature Throughput**: Short-term roadmap velocity may appear reduced by 20%.

**Planning Overhead**: Requires disciplined backlog management to ensure the "tax" is spent on high-impact technical improvements.

### Compliance and Monitoring

The 20% allocation will be tracked in sprint planning as "System Health" or "Enabler" tasks.

The effectiveness will be measured by monitoring the trend of **Cycle Time** and **Change Failure Rate** over the next quarter.
