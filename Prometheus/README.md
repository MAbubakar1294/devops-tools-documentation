# Prometheus

## 1. Brief Introduction

Prometheus is an open-source monitoring and alerting toolkit.

It stores numerical measurements as time series with timestamps and labels, normally collecting them by pulling metrics over HTTP from targets.

Prometheus works well for infrastructure and service metrics such as CPU utilization, memory, request rate, error rate and latency.

It is commonly paired with Grafana for visualization and Alertmanager for alert routing.

---

## 2. Prometheus Architecture

The Prometheus server discovers targets, scrapes their metrics endpoints and stores time series.

Exporters expose metrics for systems that do not natively expose Prometheus metrics.

Rules can generate alerts, which are handled by Alertmanager.

Grafana can query Prometheus.

| Component | Role |
|---|---|
| Prometheus server | Scrapes, stores metrics and evaluates rules |
| Targets | Applications/services exposing metrics endpoints |
| Exporters | Expose metrics from systems such as nodes, databases or network devices |
| PromQL | Query language for selecting and calculating time-series data |
| Alert rules | Expressions that generate alerts when conditions are met |
| Alertmanager | Groups, routes and sends alerts |
| Grafana | Common visualization/dashboard layer |

---

## 3. Key Commands / PromQL

| Query / Command | Purpose | Example |
|---|---|---|
| `prometheus --version` | Show version | `prometheus --version` |
| `up` | Check target availability | `up` |
| `rate()` | Calculate counter rate | `rate(http_requests_total[5m])` |
| `sum()` | Aggregate series | `sum(rate(http_requests_total[5m]))` |
| `avg()` | Average values | `avg(up)` |
| `count()` | Count series | `count(up)` |
| `histogram_quantile()` | Estimate histogram quantiles | `histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m]))` |

---

## 4. Real-Time Project Usage

A typical Prometheus workflow:

1. Instrument applications with Prometheus metrics.
2. Configure Prometheus to discover or scrape targets.
3. Use exporters where necessary.
4. Create recording rules for repeated calculations.
5. Create actionable alert rules.
6. Send alerts to Alertmanager.
7. Connect Grafana for dashboards and investigation.

---

## 5. Practical Example

### Check whether a target is up

```promql
up
```

### Request rate

```promql
sum(rate(http_requests_total[5m]))
```

### 5xx error rate

```promql
sum(rate(http_requests_total{status=~"5.."}[5m]))
```

### CPU utilization

```promql
100 * (1 - avg by(instance)(
  rate(node_cpu_seconds_total{mode="idle"}[5m])
))
```

Metric naming and label design are critical.

Avoid uncontrolled label cardinality because every unique label combination creates a separate time series.

---

## 6. Alternatives & Comparison

| Tool | Strength | Typical Fit |
|---|---|---|
| Prometheus | Label-based time series and pull-oriented scraping | Cloud-native infrastructure and application monitoring |
| VictoriaMetrics | Prometheus-compatible scalable metrics platform | Large-scale or long-retention metrics environments |
| InfluxDB | Time-series database with broad ingestion/query options | General time-series workloads |
| Datadog | Managed integrated observability | Teams preferring a SaaS platform |

---

## 7. Best Practices & Troubleshooting

- Use stable, meaningful labels.
- Avoid high-cardinality labels such as arbitrary user IDs.
- Choose scrape intervals based on resolution and capacity.
- Use recording rules for expensive repeated calculations.
- Create actionable alerts and reduce alert noise.
- For missing targets, inspect service discovery and scrape configuration.
- For slow queries, reduce time range, cardinality or computation complexity.

---

## 8. Suggested Internship Mini-Project

Instrument a web application with request and latency metrics.

The project should:

1. Configure Prometheus scraping.
2. Write PromQL for traffic and errors.
3. Create target-down alerts.
4. Create high-error alerts.
5. Visualize the results in Grafana.

---

## Conclusion

Prometheus is a foundational monitoring skill.

Important areas include:

- Time-series data
- Labels
- Scraping
- PromQL
- Rules
- Alerting
- Grafana dashboards

## References

- Prometheus Overview https://prometheus.io/docs/introduction/overview/
- Prometheus Documentation  https://prometheus.io/docs/
- PromQL Basics  https://prometheus.io/docs/prometheus/latest/querying/basics/
