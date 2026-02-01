# Stack Architecture

## Exam Objectives
- [ ] Describe basic Stack Architecture
- [ ] Demonstrate use of Fleet and Elastic Agents

## Basic Stack Architecture

### Core Components
- **Elasticsearch** - Distributed search and analytics engine
- **Kibana** - Visualization and management UI
- **Elastic Agent** - Unified agent for data collection
- **Fleet** - Centralized agent management

### Architecture Diagram
```
┌─────────────────────────────────────────────────────────┐
│                        Kibana                           │
│              (UI, Fleet, Security App)                  │
└─────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────┐
│                    Elasticsearch                        │
│            (Cluster: Data, Ingest, Master)              │
└─────────────────────────────────────────────────────────┘
                            ▲
                            │
┌─────────────────────────────────────────────────────────┐
│                    Elastic Agents                       │
│         (Endpoints, Servers, Cloud, Network)            │
└─────────────────────────────────────────────────────────┘
```

## Fleet and Elastic Agents

### Fleet
- Centralized management for Elastic Agents
- Policy-based configuration
- Agent enrollment and monitoring
- Integration management

### Elastic Agent
- Single unified agent (replaces Beats)
- Collects logs, metrics, and security data
- Managed via Fleet or standalone
- Supports integrations for various data sources

### Key Concepts
- **Fleet Server** - Connects agents to Fleet
- **Agent Policies** - Define what data to collect
- **Integrations** - Pre-built data collection configs
- **Enrollment Tokens** - Secure agent registration

## Documentation Links
- [Fleet and Elastic Agent Guide](https://www.elastic.co/guide/en/fleet/current/index.html)
- [Fleet Overview](https://www.elastic.co/guide/en/fleet/current/fleet-overview.html)
- [Elastic Agent](https://www.elastic.co/guide/en/fleet/current/elastic-agent-installation.html)

## Notes

<!-- Add your study notes here -->

## Practice Questions

<!-- Add practice questions here -->
