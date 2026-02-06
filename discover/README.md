# Discover

## Exam Objectives
- [ ] Customize the Discover interface to search for data

## Overview

Discover is Kibana's interface for exploring and searching data in Elasticsearch. It allows you to interactively search, filter, and analyze your data.

## Key Features

### Data Views (Index Patterns)
- Define which indices to search
- Configure field formatting
- Set time field for time-based filtering
- Runtime fields for computed values

### Search Bar
- **KQL (Kibana Query Language)** - Default, user-friendly syntax
- **Lucene** - Advanced query syntax option

## KQL Syntax

### Basic Queries
```kql
# Field equals value
user.name: "admin"

# Wildcard
host.name: web*

# Numeric comparison
http.response.status_code >= 400

# Boolean
event.outcome: success
```

### Logical Operators
```kql
# AND (implicit or explicit)
user.name: admin AND event.action: login
user.name: admin event.action: login

# OR
event.outcome: success OR event.outcome: failure

# NOT
NOT user.name: admin

# Grouping
(user.name: admin OR user.name: root) AND event.action: login
```

### Nested Queries
```kql
# Check if field exists
user.name: *

# Nested field queries
user.name: admin AND source.ip: 192.168.*
```

## Customizing the Interface

### Field Selection
- Add/remove columns from document table
- Reorder columns via drag and drop
- Pin important fields

### Saved Searches
- Save frequently used searches
- Include query, filters, columns, and sort order
- Share across dashboards

### Filters
- Click field values to add filters
- Filter for value (+) or filter out (-)
- Pin filters across sessions
- Temporarily disable filters

### Time Filter
- Quick select presets (Last 15 min, Last 24 hours, etc.)
- Absolute time ranges
- Relative time ranges
- Auto-refresh intervals

## Document Exploration

### Document View
- Expand documents to see all fields
- View as table or JSON
- Filter for field values directly
- View surrounding documents

### Field Statistics
- View top values for fields
- Field type information
- Field existence percentage

## Security Use Cases

### Common Security Searches
```kql
# Failed authentication attempts
event.category: authentication AND event.outcome: failure

# Process execution
event.category: process AND event.type: start

# Network connections to external IPs
event.category: network AND NOT destination.ip: 10.0.0.0/8

# File creation events
event.category: file AND event.type: creation

# Specific user activity
user.name: "suspicious_user" AND event.action: *
```

### Investigation Workflow
1. Start with broad time range
2. Use field filters to narrow scope
3. Add relevant columns
4. Save search for reuse
5. Export to Timeline for correlation

## Documentation Links
- [Discover Guide](https://www.elastic.co/guide/en/kibana/current/discover.html)
- [KQL Reference](https://www.elastic.co/guide/en/kibana/current/kuery-query.html)
- [Search Sessions](https://www.elastic.co/guide/en/kibana/current/search-sessions.html)

## Notes

<!-- Add your study notes here -->

## Practice Questions

<!-- Add practice questions here -->
