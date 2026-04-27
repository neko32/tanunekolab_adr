# 10. nekokan env

Date: 2026-04-26

## Status

Accepted

## Context

Nekokan Framework's common env set up

## Decision

### Env Types

- local
- dev
- qa
- prod

Current env is known by env variable ENV.

### Env Variables

The following env variables must be available common across all platforms.

|Name|Description|
|----|-----------|
|LD_LIBRARY_PATH|Path for shared libraries|
|NEKOKAN_TMP_DIR|Local temp dir|
|NEKOKAN_CONF_DIR|Directory for resources|
|NEKOKAN_DB_DIR|Local  DB Directory used by nekokan app|
|NEKOKAN_ADMIN_USER|Nekokan admin user name|
|NEKOKAN_ADMIN_GROUP|Nekokan admin group name|
|NEKOKAN_CODE_DIR|Nekokan codebase directory|
|NEKOKAN_CMD_DIR|Nekokan command directory|
|NEKOKAN_LIB_DIR|Nekokan library directory|
|NEKOKAN_BIN_DIR|Nekokan binary directory|
|NEKOKAN_{SRV TYPE}_URL|Nekokan Resource server URL|
|NEKOKAN_{SRV TYPE}_USER|Nekokan Resource server user name|
|NEKOKAN_{SRV TYPE}_PASSWD|Nekokan Resource server password|
|NEKOKAN_{SRV TYPE}_API_KEY|Nekokan Resource server API Key|
|${NEOKKAN_BIN_DIR}/{App Name}|Each app's bin location|
|${NEKOKAN_CONF_DIR}/{App Name}|Each app's config location|
|ANTHROPIC_API_KEY|Anthropic API Key|
|GH_TOKEN|Github API Key|

### Server Types (SRV TYPE)

|Type Name|Description|
|---------|-----------|
|FTP|FTP|
|RDB|Relational Data Base|
|VDB|Vector DB|
|LLM|Large Language Model|


## Consequences

N/A

