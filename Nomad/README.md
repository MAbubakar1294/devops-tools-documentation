# HashiCorp Nomad

## 1. Brief Introduction

HashiCorp Nomad is a highly available, distributed and data-center-aware scheduler for long-running services, batch jobs and other workloads.

Nomad servers manage scheduling while clients provide execution capacity.

Nomad uses a declarative jobspec: the operator describes what should run, while Nomad decides where it should run.

Jobs contain task groups and tasks, resource requirements and optional constraints.

---

## 2. Nomad Architecture

Within a region, Nomad servers accept jobs, manage clients and compute placements.

Clients execute allocations.

Regions can include clients from multiple datacenters.

Nomad also includes consensus, gossip and scheduler subsystems.

| Component | Role |
|---|---|
| Nomad servers | Maintain cluster state, accept jobs and compute placements |
| Nomad clients | Run allocated tasks and report status/resource information |
| Region | Logical grouping used for scheduling and cluster organization |
| Datacenter | Location grouping used in placement/topology |
| Job | Declarative desired state for a workload |
| Task group | Set of tasks placed together |
| Task | Individual workload definition, such as a Docker container or executable |

---

## 3. Key Commands

| Command | Purpose | Example |
|---|---|---|
| `nomad agent` | Start an agent | `nomad agent -dev` |
| `nomad job init` | Create example jobspec | `nomad job init` |
| `nomad job validate` | Validate a jobspec | `nomad job validate app.nomad` |
| `nomad job plan` | Preview changes | `nomad job plan app.nomad` |
| `nomad job run` | Submit a job | `nomad job run app.nomad` |
| `nomad job status` | Show job status | `nomad job status web` |
| `nomad job allocs` | List allocations | `nomad job allocs web` |
| `nomad job deployments` | Show deployments | `nomad job deployments web` |
| `nomad job stop` | Stop a job | `nomad job stop web` |
| `nomad job scale` | Scale a task group | `nomad job scale web count=3` |

---

## 4. Real-Time Project Usage

A typical Nomad workflow:

1. Define the workload in a version-controlled jobspec.
2. Validate and plan before deployment.
3. Submit the job to Nomad servers.
4. Nomad schedules allocations onto clients based on resources and constraints.
5. Monitor job and allocation health.
6. Use controlled deployment strategies for updates.
7. Integrate service discovery, secrets and observability as required.

---

## 5. Practical Example

```hcl
job "university-web" {
  datacenters = ["dc1"]

  type = "service"

  group "web" {
    count = 2

    task "app" {
      driver = "docker"

      config {
        image = "nginx:latest"
        ports = ["http"]
      }

      resources {
        cpu    = 500
        memory = 256
      }
    }
  }
}
```

### Validate

```bash
nomad job validate university-web.nomad
```

### Plan

```bash
nomad job plan university-web.nomad
```

### Run

```bash
nomad job run university-web.nomad
```

### Check status

```bash
nomad job status university-web
```

### Check allocations

```bash
nomad job allocs university-web
```

---

## 6. Alternatives & Comparison

| Platform | Strength | Typical Fit |
|---|---|---|
| Nomad | Focused scheduler with broad workload support | Teams wanting a smaller operational surface |
| Kubernetes | Large ecosystem and extensive container orchestration | Complex cloud-native platforms and broad integrations |
| Docker Swarm | Simple Docker-native clustering | Small Docker-centric deployments |
| Apache Mesos | Historically broad resource scheduling | Mostly legacy/specialized environments |

---

## 7. Best Practices & Troubleshooting

- Keep jobspecs in Git and review changes.
- Set resource requirements and constraints intentionally.
- Use validation and plan before important changes.
- Monitor allocations and client health.
- Use appropriate deployment strategies.
- For failed allocations, inspect job status, allocation events and task logs.
- Secure servers and client communication in production.

---

## 8. Suggested Internship Mini-Project

Run a small Nomad lab.

The project should:

1. Deploy a Dockerized web service.
2. Use two allocations.
3. Perform a controlled update.
4. Inspect allocations.
5. Scale the service.
6. Document placement behavior.

---

## Conclusion

Nomad is useful for teams that want a focused scheduler and support for multiple workload types.

Important concepts include:

- Servers
- Clients
- Jobs
- Task groups
- Allocations
- Resources
- Constraints
- Deployment workflows

## References

- Nomad Documentation https://developer.hashicorp.com/nomad/docs
- Nomad Architecture  https://developer.hashicorp.com/nomad/docs/architecture
- Nomad Job Concept   https://developer.hashicorp.com/nomad/docs/concepts/job
- Nomad Job Commands  https://developer.hashicorp.com/nomad/commands/job
