# Security Application

## Exam Objectives
- [ ] Recognize the capabilities of the Security App
- [ ] Use Explore within the Security App to view security-related events
- [ ] Describe how the Detection Engine searches activity and generates alerts
- [ ] Analyze alerts that are generated from detection rules
- [ ] Correlate relevant data using Timeline
- [ ] Track security issues using Cases
- [ ] Monitor security-related events with dashboards in the Security App
- [ ] Describe how AI is used in the Security App

## Security App Overview

The Elastic Security app provides a unified workspace for security operations including threat detection, investigation, and response.

### Main Sections
| Section | Purpose |
|---------|---------|
| Overview | High-level security posture |
| Alerts | Detection alerts and management |
| Explore | Hosts, Network, Users views |
| Investigate | Timeline, Cases, Osquery |
| Rules | Detection rule management |
| Dashboards | Security-specific dashboards |
| Assets | Asset management |

---

## Explore

### Hosts
- View all monitored hosts
- Host details: OS, IP, risk score, events
- Authentication events per host
- Uncommon processes
- Host risk scores

### Network
- Network flow data overview
- Top source/destination IPs
- DNS activity
- TLS/HTTP traffic
- Geographic map of connections

### Users
- User activity overview
- Authentication events
- User risk scores
- Anomalous user behavior

### Common Explore Workflows
```
1. View hosts list → Click host → See all events for that host
2. View network flows → Filter by IP → Investigate connections
3. View users → Identify risky users → Review authentication events
```

---

## Detection Engine

### How It Works
1. **Detection rules** define search criteria
2. Rules run on a **schedule** (e.g., every 5 minutes)
3. Elasticsearch queries **search incoming data**
4. Matching events **generate alerts**
5. Alerts appear in the **Alerts page**

### Rule Types
| Type | Description |
|------|-------------|
| Custom Query | KQL or Lucene query match |
| Machine Learning | ML job anomaly detection |
| Threshold | Alert when count exceeds value |
| Event Correlation (EQL) | Sequence of events pattern |
| Indicator Match | Matches against threat intel |
| New Terms | New values not seen before |
| ES\|QL | Elasticsearch query language rules |

### Custom Query Rules
```kql
# Example: Detect brute force
event.category: authentication AND event.outcome: failure
# Threshold: > 10 in 5 minutes, group by user.name
```

### EQL (Event Query Language)
```eql
# Sequence: Login failure followed by success from same source
sequence by source.ip, user.name [maxspan=5m]
  [authentication where event.outcome == "failure"] with runs=5
  [authentication where event.outcome == "success"]
```

### Threshold Rules
```
Query: event.category: authentication AND event.outcome: failure
Threshold: >= 10
Group by: user.name
Time window: 5 minutes
```

### Indicator Match Rules
```
Match incoming events against threat intelligence feeds
Source: Incoming events (source.ip, destination.ip)
Indicator: Threat intel index (threat.indicator.ip)
```

### Rule Configuration
- **Severity:** Critical, High, Medium, Low
- **Risk Score:** 0-100
- **Schedule:** Run interval and look-back
- **Actions:** Notifications (email, Slack, webhook)
- **Exceptions:** Exclude known false positives
- **Tags:** Categorize rules (MITRE ATT&CK, etc.)

---

## Alerts

### Alert Management
| Status | Meaning |
|--------|---------|
| Open | New, unreviewed alert |
| Acknowledged | Analyst is reviewing |
| Closed | Resolved, no further action |

### Alert Workflow
```
Open → Acknowledged → Closed
  │                      ▲
  └──────────────────────┘
        (or close directly)
```

### Analyzing Alerts
1. **Review alert details** - Rule name, severity, risk score
2. **Examine event data** - Source, destination, user, process
3. **View rule details** - Understand what triggered
4. **Check timeline** - Correlate with other events
5. **Add to case** - Track investigation
6. **Take action** - Close, add exception, escalate

### Alert Actions
- **Add to Timeline** - Investigate in context
- **Add to Case** - Track as part of an incident
- **Add Exception** - Suppress false positives
- **Mark as** - Open, Acknowledged, Closed
- **Apply bulk actions** - Manage multiple alerts

### Alert Exceptions
```
Conditions to exclude known false positives:
- Field: process.name, Operator: is, Value: approved_scanner.exe
- Can be applied to single rule or all rules
- Exception lists for reuse across rules
```

---

## Timeline

### Purpose
Correlate and investigate events from multiple data sources in a single workspace.

### Key Features
- Drag and drop fields to build queries
- Pin important events
- Add notes and comments
- Save and share timelines
- Convert to templates

### Timeline Interface
```
┌─────────────────────────────────────────────────┐
│  Query Bar (KQL / EQL)                          │
├─────────────────────────────────────────────────┤
│  Filters and Data Providers                     │
├─────────────────────────────────────────────────┤
│  Event Stream                                   │
│  ├── Event 1 (expandable)                       │
│  ├── Event 2 (pinned)                           │
│  ├── Event 3                                    │
│  └── Event 4                                    │
├─────────────────────────────────────────────────┤
│  Notes                                          │
└─────────────────────────────────────────────────┘
```

### Data Providers
- Drag fields into the Data Providers area
- Combine with AND/OR logic
- Filter events dynamically

### Investigation Workflow with Timeline
1. Start from an alert → **Add to Timeline**
2. Expand time range for context
3. Add data providers to filter
4. Pin relevant events
5. Add notes for documentation
6. Attach timeline to a case

### Timeline Templates
- Create reusable investigation templates
- Pre-configure columns and queries
- Share across team

---

## Cases

### Purpose
Track, manage, and collaborate on security issues and investigations.

### Case Features
| Feature | Description |
|---------|-------------|
| Title & Description | Document the issue |
| Tags | Categorize cases |
| Status | Open, In Progress, Closed |
| Severity | Critical, High, Medium, Low |
| Assignees | Assign to team members |
| Comments | Collaborate with notes |
| Alerts | Attach related alerts |
| Timelines | Attach investigation timelines |
| Connectors | Integrate with external tools |

### Case Workflow
```
Open → In Progress → Closed
```

### Connectors
Integrate cases with external systems:
- **Jira** - Create/update issues
- **ServiceNow (ITSM/SIR)** - Incident management
- **IBM Resilient** - SOAR integration
- **Swimlane** - Case management
- **Webhook** - Custom integrations

### Using Cases
1. **Create case** - Title, description, severity, tags
2. **Attach alerts** - Link related detection alerts
3. **Attach timelines** - Include investigation evidence
4. **Add comments** - Document findings and actions
5. **Push to external** - Sync with Jira/ServiceNow
6. **Close case** - Document resolution

---

## Security Dashboards

### Built-in Dashboards
- **Overview** - High-level security posture
- **Detection & Response** - Alert trends and metrics
- **Entity Analytics** - User and host risk scores

### Custom Security Dashboards
Build dashboards for:
- SOC operations monitoring
- Compliance reporting
- Threat hunting metrics
- Incident response KPIs

---

## AI in the Security App

### Elastic AI Assistant
- **Natural language queries** - Ask questions about security data
- **Alert investigation** - AI-guided alert triage
- **Rule creation assistance** - Help writing detection rules
- **Case summarization** - Summarize case findings
- **Query generation** - Convert natural language to KQL/EQL
- **Workflow automation** - Suggest response actions

### Attack Discovery
- AI-powered identification of attack patterns
- Correlates alerts and events to surface campaigns
- Highlights critical attack chains

### AI Features
| Feature | Description |
|---------|-------------|
| AI Assistant | Chat-based security copilot |
| Attack Discovery | Automated attack chain identification |
| Alert summarization | AI-generated alert context |
| Suggested actions | Recommended investigation steps |

### How AI is Applied
```
1. Analyst opens alert
2. AI Assistant provides context and summary
3. Suggests related events to investigate
4. Recommends response actions
5. Helps document findings in cases
```

---

## MITRE ATT&CK Integration

### Framework Coverage
- Detection rules mapped to ATT&CK techniques
- Coverage view shows gaps
- Helps prioritize rule development

### Tactics
```
Reconnaissance → Resource Development → Initial Access →
Execution → Persistence → Privilege Escalation →
Defense Evasion → Credential Access → Discovery →
Lateral Movement → Collection → Command and Control →
Exfiltration → Impact
```

---

## Documentation Links
- [Elastic Security Overview](https://www.elastic.co/guide/en/security/current/index.html)
- [Detection Rules](https://www.elastic.co/guide/en/security/current/detection-engine-overview.html)
- [Timeline](https://www.elastic.co/guide/en/security/current/timelines-ui.html)
- [Cases](https://www.elastic.co/guide/en/security/current/cases-overview.html)
- [AI Assistant](https://www.elastic.co/guide/en/security/current/security-assistant.html)
- [Explore - Hosts](https://www.elastic.co/guide/en/security/current/hosts-overview.html)
- [Explore - Network](https://www.elastic.co/guide/en/security/current/network-page-overview.html)

## Notes

<!-- Add your study notes here -->

## Practice Questions

<!-- Add practice questions here -->
