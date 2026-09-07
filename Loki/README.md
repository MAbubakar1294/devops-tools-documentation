# Grafana Loki

## 1. Brief Introduction

Grafana Loki is a horizontally scalable, highly available log aggregation system inspired by Prometheus.

It indexes labels and metadata rather than the full contents of log lines, while log data is compressed into chunks stored in an object store or configured backend.

Loki is commonly paired with Grafana for log exploration and is particularly useful in Kubernetes environments.

---

## 2. Loki Architecture

Loki uses a microservices-based architecture and can also run as a single binary for simpler deployments.

Scalable deployments can separate read, write and backend responsibilities.

| Component / Concept | Role |
|---|---|
| Distributor | Receives incoming log streams and routes them to ingesters |
| Ingester | Processes incoming logs and builds/stores chunks |
| Query Frontend | Accepts queries, splits work and coordinates query execution |
| Querier | Reads recent data from ingesters and historical data from storage |
| Object storage | Stores compressed log chunks for durable retention |
| Labels | Metadata identifying log streams |
| LogQL | Query language for selecting, filtering, parsing and analyzing logs |

---

## 3. Key Commands / Queries

| Query / Command | Purpose | Example |
|---|---|---|
| LogQL selector | Select a log stream | `{app="api", namespace="prod"}` |
| Line filter | Filter log text | `{app="api"} |= "ERROR"` |
| Regex filter | Match a pattern | `{app="api"} |~ "timeout\|failed"` |
| JSON parser | Parse structured log lines | `{app="api"} | json` |
| Logfmt parser | Parse logfmt content | `{app="api"} | logfmt` |
| Aggregation | Create metric-like result | `sum(count_over_time({app="api"}[5m]))` |
| logcli query | Run a Loki query from CLI | `logcli query '{app="api"}'` |

---

## 4. Real-Time Project Usage

A typical Loki workflow:

1. Applications and Kubernetes workloads write logs.
2. A collector sends logs to Loki.
3. Loki stores label/index information and compressed chunks.
4. Grafana connects to Loki as a data source.
5. Engineers use LogQL to investigate errors and failures.
6. Logs are correlated with Prometheus metrics during incidents.

---

## 5. Practical Example

### Find API errors

```logql
{app="api", namespace="prod"} |= "ERROR"
```

### Parse JSON and filter server errors

```logql
{app="api"} | json | status >= 500
```

### Count errors over five minutes

```logql
sum(count_over_time({app="api"} |= "ERROR"[5m]))
```

Avoid putting highly dynamic values such as request IDs or user IDs into labels when they create excessive numbers of streams.

Prefer stable labels such as application, namespace and environment.

---

## 6. Alternatives & Comparison

| Tool | Strength | Typical Fit |
|---|---|---|
| Loki | Low-index design and strong Grafana integration | Cloud-native/Kubernetes logging and cost-conscious centralized logs |
| Elastic Stack | Rich indexing and search ecosystem | Complex full-text search and broad analytics |
| OpenSearch | Open-source search/analytics platform | Teams wanting an Elasticsearch-style open ecosystem |
| Splunk | Mature enterprise analytics | Large organizations with established enterprise logging workflows |

---

## 7. Best Practices & Troubleshooting

- Keep labels low-cardinality and stable.
- Use LogQL pipelines for parsing at query time where appropriate.
- Use suitable retention and object storage.
- Monitor ingestion rate and query latency.
- For missing logs, check collector, labels, endpoint and time range.
- For slow queries, improve label selectivity and reduce broad time ranges.

---

## 8. Suggested Internship Mini-Project

Deploy an application on Kubernetes, collect its logs into Loki, connect Loki to Grafana and build a dashboard for errors.

The project should include:

1. Log collection.
2. Grafana integration.
3. LogQL queries for error counts.
4. Recent failure investigation.
5. Documentation of the label strategy.
6. Explanation of how high-cardinality labels are avoided.

---

## Conclusion

Loki is a strong logging tool when centralized logs, Kubernetes integration and efficient label-based querying are priorities.

Important skills include:

- Labels
- LogQL
- Log collection
- Storage
- Query troubleshooting
- Grafana integration

## References

- Grafana Loki Documentation https://grafana.com/docs/loki/latest/
- Loki Architecture  https://grafana.com/docs/loki/latest/get-started/architecture/
- Loki Overview  https://grafana.com/docs/loki/latest/get-started/overview/
- LogQL Documentation  https://grafana.com/docs/loki/latest/query/log_queries/
