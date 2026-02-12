# Dashboards

## Exam Objectives
- [ ] Construct dashboards for security use cases
- [ ] Demonstrate the use of dashboards

## Overview

Dashboards in Kibana combine multiple visualizations, saved searches, and controls into a single view for monitoring and analysis.

## Creating Dashboards

### Steps to Create
1. Navigate to **Dashboard** → **Create dashboard**
2. Click **Add panel** to add content
3. Choose from:
   - **Visualizations** from library
   - **Saved searches** from Discover
   - **Create new** visualization inline
4. Arrange and resize panels
5. Save dashboard with meaningful name

### Panel Types
| Type | Description |
|------|-------------|
| Visualization | Charts, metrics, tables from Lens or legacy |
| Saved Search | Discover results with selected columns |
| Controls | Interactive filters (dropdowns, sliders) |
| Markdown | Text, links, instructions |
| Image | Static images for branding/context |
| Links | Navigation to other dashboards |

## Dashboard Features

### Time Controls
- Global time picker applies to all panels
- Override per-panel time range if needed
- Auto-refresh intervals

### Filtering
- Click visualization elements to filter
- Add filter pills manually
- Use Controls panel for user-friendly filtering
- Filters apply across all panels

### Controls Panel
```
Input Control Types:
- Options List: Dropdown for field values
- Range Slider: Numeric range selection
- Time Slider: Time range selection
```

### Drill-Down
- Click elements to filter dashboard
- Link to other dashboards
- Open in Discover for raw data
- Navigate to Timeline (Security)

### Dashboard Modes
- **Edit Mode** - Add, remove, resize panels
- **View Mode** - Interactive viewing
- **Full Screen** - Presentation mode

## Dashboard Organization

### Layout Best Practices
```
┌─────────────────────────────────────────────────┐
│  Key Metrics (Metric panels)                    │
├─────────────────────────────────────────────────┤
│  Filters / Controls                             │
├───────────────────────┬─────────────────────────┤
│  Trend Over Time      │  Top Categories         │
│  (Line/Area chart)    │  (Bar/Pie chart)        │
├───────────────────────┴─────────────────────────┤
│  Detailed Data Table                            │
└─────────────────────────────────────────────────┘
```

### Naming Conventions
- Use prefixes: `[Security]`, `[Network]`, `[Auth]`
- Include scope: `[Security] Authentication Overview`
- Version if needed: `Auth Dashboard v2`

## Security Dashboard Examples

### Authentication Dashboard
```
Panels:
1. Metric: Total Login Attempts (24h)
2. Metric: Failed Login Count
3. Metric: Unique Users
4. Line: Login Attempts Over Time (success vs failure)
5. Bar: Top Users with Failed Logins
6. Bar: Top Source IPs for Failed Logins
7. Table: Recent Failed Login Details
8. Map: Geographic Login Distribution

Filters:
- event.category: authentication
- Time range: Last 24 hours
```

### Network Security Dashboard
```
Panels:
1. Metric: Total Connections
2. Metric: Bytes Transferred
3. Area: Network Traffic Over Time
4. Pie: Traffic by Protocol
5. Bar: Top Destination IPs
6. Bar: Top Source IPs
7. Heatmap: Connections by Hour
8. Table: Suspicious Connections

Filters:
- event.category: network
```

### Endpoint Security Dashboard
```
Panels:
1. Metric: Active Endpoints
2. Metric: Alert Count
3. Line: Process Executions Over Time
4. Bar: Top Processes
5. Bar: Alerts by Severity
6. Table: Recent Process Events
7. Table: File Changes

Filters:
- agent.type: endpoint
```

### Alert Overview Dashboard
```
Panels:
1. Metric: Total Alerts
2. Metric: Critical Alerts
3. Metric: Open Cases
4. Donut: Alerts by Severity
5. Bar: Alerts by Rule Name
6. Line: Alert Trend Over Time
7. Bar: Top Hosts with Alerts
8. Table: Recent Alerts with Details

Filters:
- event.kind: signal
```

## Sharing Dashboards

### Export Options
- **Share** → Generate short URL
- **Share** → Embed code (iframe)
- **Export** → PDF report
- **Export** → PNG image
- **Export** → CSV (per panel)

### Saved Objects
- Export dashboards as NDJSON
- Import into other Kibana instances
- Include dependencies (visualizations, data views)

## Dashboard Tags and Organization

### Using Tags
- Create descriptive tags: `security`, `network`, `compliance`
- Filter dashboards by tags in listing
- Group related dashboards

### Spaces
- Organize dashboards by team or function
- Control access with role-based permissions
- Separate dev/staging/prod views

## Best Practices

### Performance
- Limit panels to 15-20 per dashboard
- Use appropriate time ranges
- Optimize heavy visualizations
- Consider dashboard loading time

### Usability
- Start with overview, drill into details
- Use consistent color schemes
- Add markdown panels for context
- Include clear titles and descriptions

### Security Monitoring
- Focus on actionable insights
- Include drill-down to raw events
- Add thresholds and reference lines
- Update regularly based on threats

## Documentation Links
- [Dashboard Guide](https://www.elastic.co/guide/en/kibana/current/dashboard.html)
- [Create Dashboards](https://www.elastic.co/guide/en/kibana/current/create-a-dashboard.html)
- [Dashboard Controls](https://www.elastic.co/guide/en/kibana/current/add-controls.html)

## Notes

<!-- Add your study notes here -->

## Practice Questions

<!-- Add practice questions here -->
