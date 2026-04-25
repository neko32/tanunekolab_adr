# 8. command line scripting

Date: 2026-04-24

## Status

Accepted

## Context

Our development environment spans across Windows, macOS, and Linux. To automate local environment setups, build processes, and general utility tasks, we need a unified strategy for shell scripting.

Previously, the lack of a defined standard led to "it works on my machine" issues, where scripts written for Git Bash wouldn't run on native Windows terminals, or PowerShell scripts were unusable for Mac/Linux contributors.

## Decision

We will adopt the native, most powerful shell environments for their respective operating systems to ensure maximum compatibility with the underlying OS features:

**Windows Environments**: PowerShell (5.1 or Core 7+) is the standard.

**Linux / macOS Environments**: bash (Bourne Again SHell) is the standard.

### Implementation Guidelines

**Native First**: Scripts should leverage the strengths of the native shell (e.g., PowerShell objects for Windows, text-stream processing for bash).

**Shebangs & Extensions**: 
* Use .ps1 for PowerShell scripts.
* Use .sh with a proper shebang (#!/bin/bash) for bash scripts.

**Complex Logic**: If a task requires complex logic that is difficult to maintain in two separate shell languages, the logic should be migrated to a cross-platform language like Python or Node.js.

**Avoid Aliases**: In PowerShell scripts, avoid using aliases like ls or rm to prevent confusion with Linux commands. Use full Cmdlets (e.g., Get-ChildItem).

## Consequences

### Pros

**Performance & Integration**: No need for translation layers or third-party emulators (like MinGW/Git Bash) to access system-level resources.

**Modernity**: PowerShell provides robust error handling and object-oriented data, while bash remains the industry standard for Unix-like systems.

**Onboarding**: New developers can use the default tools provided by their OS without complex pre-requisite installations.

### Cons

**Duplication**: Some utility logic may need to be implemented twice (once for .ps1 and once for .sh).

**Learning Curve**: Contributors may need to be familiar with the basics of both shell environments to maintain the project's tooling.

### Validation

All shared utility scripts must be placed in a /scripts /scripts_local or /tools directory, clearly separated or named by their target shell. CI/CD pipelines will be configured to run the appropriate script based on the runner's OS.
