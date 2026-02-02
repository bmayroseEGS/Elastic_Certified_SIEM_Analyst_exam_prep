# Elastic Common Schema (ECS)

## Exam Objectives
- [ ] Examine the application and guidelines of ECS

## What is ECS?

ECS (Elastic Common Schema) is an open source specification that defines a common set of fields and naming conventions for ingested data in Elasticsearch.

### Purpose
- **Normalization** - Consistent field names across all data sources
- **Correlation** - Easier to correlate events from different sources
- **Reusability** - Dashboards, rules, and queries work across data sources
- **Interoperability** - Third-party tools can integrate seamlessly

## Core Field Sets

| Field Set | Description | Example Fields |
|-----------|-------------|----------------|
| `@timestamp` | Event timestamp | `@timestamp` |
| `agent` | Agent that collected the data | `agent.name`, `agent.version` |
| `client` | Client in network connection | `client.ip`, `client.port` |
| `cloud` | Cloud provider metadata | `cloud.provider`, `cloud.region` |
| `destination` | Destination in network event | `destination.ip`, `destination.port` |
| `ecs` | ECS metadata | `ecs.version` |
| `event` | Event categorization | `event.category`, `event.action`, `event.outcome` |
| `host` | Host information | `host.name`, `host.os.name` |
| `log` | Log file details | `log.level`, `log.file.path` |
| `message` | Log message | `message` |
| `process` | Process information | `process.name`, `process.pid` |
| `server` | Server in network connection | `server.ip`, `server.port` |
| `source` | Source in network event | `source.ip`, `source.port` |
| `user` | User information | `user.name`, `user.id` |

## Event Categorization

### event.kind
- `alert` - Detection rule triggered
- `event` - Regular event
- `metric` - Numeric measurement
- `state` - Current state description
- `signal` - Detection signal

### event.category
- `authentication`
- `file`
- `network`
- `process`
- `registry`
- `web`
- `malware`

### event.type
- `start`, `end`
- `creation`, `deletion`, `change`
- `access`, `allowed`, `denied`
- `connection`, `info`, `error`

### event.outcome
- `success`
- `failure`
- `unknown`

## ECS Guidelines

1. **Use existing fields** - Check ECS before creating custom fields
2. **Namespace custom fields** - Use `labels.*` or custom namespaces
3. **Consistent data types** - Follow ECS field type definitions
4. **Preserve original data** - Store raw data in `event.original`

## Security-Relevant Fields

```
# User activity
user.name, user.id, user.domain

# Process tracking
process.name, process.pid, process.parent.pid, process.command_line

# Network connections
source.ip, source.port, destination.ip, destination.port

# File operations
file.path, file.name, file.hash.sha256

# Authentication
event.category: authentication
event.outcome: success/failure
```

## Documentation Links
- [ECS Reference](https://www.elastic.co/guide/en/ecs/current/index.html)
- [ECS Field Reference](https://www.elastic.co/guide/en/ecs/current/ecs-field-reference.html)
- [ECS Categorization Fields](https://www.elastic.co/guide/en/ecs/current/ecs-category-field-values-reference.html)

## Notes

<!-- Add your study notes here -->

## Practice Questions

<!-- Add practice questions here -->
