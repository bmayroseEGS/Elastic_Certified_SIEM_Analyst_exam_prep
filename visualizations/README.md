# Visualizations

## Exam Objectives
- [ ] Create aggregation-based visualizations for security use cases
- [ ] Construct Lens visualizations for security use cases

## Visualization Types

### Aggregation-Based (Legacy)
- Created in Visualize Library
- Based on Elasticsearch aggregations
- More manual configuration
- Types: Area, Bar, Line, Pie, Data Table, Metric, Gauge, etc.

### Lens (Recommended)
- Drag-and-drop interface
- AI-powered suggestions
- Easier to build and modify
- Supports most common visualization needs

## Lens Visualizations

### Getting Started
1. Navigate to **Visualize Library** → **Create visualization** → **Lens**
2. Select data view (index pattern)
3. Drag fields to build visualization
4. Choose chart type from suggestions

### Chart Types in Lens
| Type | Use Case |
|------|----------|
| Bar (vertical/horizontal) | Comparing categories |
| Line | Trends over time |
| Area | Volume over time |
| Pie / Donut | Proportions |
| Metric | Single key values |
| Table | Detailed data |
| Heatmap | Patterns across two dimensions |
| Treemap | Hierarchical proportions |
| Gauge | Progress toward goals |

### Key Concepts

#### Metrics (Y-axis)
- **Count** - Number of documents
- **Sum** - Total of numeric field
- **Average** - Mean of numeric field
- **Min/Max** - Extreme values
- **Unique Count** - Cardinality
- **Percentile** - Distribution points
- **Last Value** - Most recent value

#### Buckets (X-axis / Breakdown)
- **Date Histogram** - Time intervals
- **Terms** - Top values of a field
- **Filters** - Custom groupings
- **Range** - Numeric ranges
- **Significant Terms** - Unusual terms

### Lens Features
- **Formulas** - Custom calculations
- **Reference Lines** - Thresholds and baselines
- **Annotations** - Mark specific events
- **Breakdown** - Split by additional dimension

## Aggregation-Based Visualizations

### Creating Aggregation Visualizations
1. **Visualize Library** → **Create visualization**
2. Select visualization type
3. Configure metrics and buckets
4. Apply filters as needed

### Aggregation Types

#### Metric Aggregations
```
Count, Sum, Average, Min, Max,
Median, Percentiles, Unique Count,
Standard Deviation, Top Hits
```

#### Bucket Aggregations
```
Date Histogram, Histogram, Range,
Date Range, Terms, Significant Terms,
Filters, GeoHash Grid
```

#### Pipeline Aggregations
```
Derivative, Cumulative Sum,
Moving Average, Serial Diff,
Bucket Script
```

## Security Visualization Examples

### Authentication Monitoring
```
Type: Line Chart
Metric: Count
Bucket: Date Histogram (@timestamp)
Split: event.outcome (success/failure)
Filter: event.category: authentication
```

### Top Failed Logins by User
```
Type: Horizontal Bar
Metric: Count
Bucket: Terms (user.name)
Filter: event.category: authentication AND event.outcome: failure
```

### Process Execution Heatmap
```
Type: Heatmap
X-axis: Date Histogram (@timestamp, hourly)
Y-axis: Terms (process.name)
Metric: Count
Filter: event.category: process
```

### Network Traffic by Destination
```
Type: Pie/Donut
Metric: Sum (network.bytes)
Bucket: Terms (destination.ip)
Filter: event.category: network
```

### Alert Severity Distribution
```
Type: Donut
Metric: Count
Bucket: Terms (kibana.alert.severity)
Filter: event.kind: signal
```

### Security Events Timeline
```
Type: Area (Stacked)
Metric: Count
Bucket: Date Histogram (@timestamp)
Split: Terms (event.category)
```

## Best Practices

### Performance
- Limit terms aggregations (top 10-20)
- Use appropriate time ranges
- Consider data sampling for large datasets

### Readability
- Use clear titles and labels
- Choose appropriate color schemes
- Add reference lines for thresholds
- Use legends effectively

### Security Dashboards
- Focus on actionable metrics
- Include drill-down capability
- Combine overview and detail views
- Use consistent time ranges

## Documentation Links
- [Lens Guide](https://www.elastic.co/guide/en/kibana/current/lens.html)
- [Aggregation-Based Visualizations](https://www.elastic.co/guide/en/kibana/current/aggregation-based.html)
- [Kibana Visualize](https://www.elastic.co/guide/en/kibana/current/visualize.html)

## Notes

<!-- Add your study notes here -->

## Practice Questions

<!-- Add practice questions here -->
