# Grafana

## 1. Brief Introduction

Grafana is an observability and visualization platform used to query, transform and display data from many sources.

A dashboard contains panels, and panels query data sources to produce charts, tables, logs and other visualizations.

Grafana is commonly used as the visualization layer for Prometheus metrics and Loki logs.

---

## 2. Grafana Architecture

A Grafana deployment includes:

- Grafana server/application
- Configuration database
- Data-source connectors/plugins
- Dashboards
- Panels
- Query editors
- Alerting components

Grafana generally queries external systems rather than storing all observability data itself.

| Component | Role |
|---|---|
| Grafana server | Runs the application, APIs, authentication and dashboards |
| Data source | External system queried by Grafana, such as Prometheus or Loki |
| Panel | Visualization building block that runs queries and renders results |
| Dashboard | Collection of related panels for an operational purpose |
| Query editor | Interface for writing a source-specific query |
| Alerting | Evaluates conditions and routes notifications |
| Plugins | Extend data sources, panels and applications |

---

## 3. Key Operations

| Operation | Purpose | Example / Note |
|---|---|---|
| `grafana-server` | Start Grafana server | Package-based installations |
| `grafana cli plugins list` | List installed plugins | Plugin management |
| Add data source | Connect monitoring/logging backend | Configuration → Data sources |
| Create dashboard | Build an operational dashboard | Dashboard → New |
| Panel query | Retrieve data for a panel | PromQL / LogQL / source query |
| Explore | Investigate data interactively | Explore → choose data source |
| Alert rule | Define an alert condition | Alerting → Alert rules |

---

## 4. Real-Time Project Usage

A typical Grafana workflow:

1. Connect Prometheus for metrics.
2. Connect Loki for logs.
3. Build infrastructure and application dashboards.
4. Use Explore during incidents.
5. Create actionable alerts and route them to an operational channel.
6. Use variables for environments, namespaces or services.

---

## 5. Practical Example

### Prometheus Panel

```promql
sum(rate(http_requests_total[5m]))
```

### Loki Panel

```logql
{namespace="prod", app="api"} |= "ERROR"
```

### Suggested Dashboard Panels

1. Service availability
2. Request rate
3. Error rate
4. P95 latency
5. CPU and memory
6. Recent application errors

A professional dashboard should answer operational questions quickly:

- Is the service available?
- Is traffic abnormal?
- Are errors increasing?
- Is latency degrading?
- Which component is responsible?

---

## 6. Alternatives & Comparison

| Platform | Strength | Typical Fit |
|---|---|---|
| Grafana | Flexible visualization and broad integrations | Teams using Prometheus/Loki and heterogeneous data sources |
| Kibana / OpenSearch Dashboards | Strong search-oriented analytics | Elastic/OpenSearch-centric logging |
| Datadog | Managed integrated observability | Teams preferring SaaS observability |
| New Relic | Managed APM and observability | Organizations preferring commercial APM |

---

## 7. Best Practices & Troubleshooting

- Organize dashboards around services or operational questions.
- Use variables instead of duplicating dashboards.
- Use sensible time ranges and query intervals.
- Control access using folders, roles and permissions.
- For empty panels, test the query in Explore and verify the data source/time range.
- For slow dashboards, reduce query complexity, panel count or broad time ranges.

---

## 8. Suggested Internship Mini-Project

Build a production-style dashboard for a small application.

The project should:

1. Connect Prometheus and Loki.
2. Create panels for availability, request rate, errors, latency and logs.
3. Add a service/environment variable.
4. Configure two meaningful alerts.

---

## Conclusion

Grafana turns raw observability data into a shared operational interface.

Important skills include:

- Data-source configuration
- Query building
- Dashboard design
- Alerting
- Incident investigation

## References

- Grafana Visualization Documentation  https://grafana.com/docs/grafana/latest/visualizations/
- Query and Transform Data  https://grafana.com/docs/grafana/latest/visualizations/panels-visualizations/query-transform-data/
- Grafana Documentation     https://grafana.com/docs/
