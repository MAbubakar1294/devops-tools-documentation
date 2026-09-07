# Kubernetes

## 1. Brief Introduction

Kubernetes is an open-source platform for deploying and operating containerized workloads at cluster scale.

It provides declarative APIs, scheduling, service discovery, scaling, rollout and self-healing mechanisms.

Kubernetes is useful when projects need repeatable deployments, scaling, health management or controlled rollouts across multiple services.

It orchestrates container workloads rather than replacing the need for container images.

---

## 2. Kubernetes Architecture

A Kubernetes cluster consists of a **control plane** and **worker nodes**.

The control plane exposes the API and makes global decisions such as scheduling.

Worker nodes run Pods and contain the components required to run workloads.

| Component | Role |
|---|---|
| kube-apiserver | Front end of the control plane and API entry point |
| etcd | Consistent, highly available key-value store for cluster data |
| kube-scheduler | Selects suitable nodes for unscheduled Pods |
| kube-controller-manager | Runs control loops that reconcile desired and actual state |
| kubelet | Node agent that ensures containers described by PodSpecs are running |
| kube-proxy / network implementation | Supports Service networking |
| Container runtime | Runs containers on worker nodes |
| Pod | Smallest deployable Kubernetes workload unit |

---

## 3. Key kubectl Commands

| Command | Purpose | Example |
|---|---|---|
| `kubectl get` | List resources | `kubectl get pods -A` |
| `kubectl describe` | Show detailed resource information | `kubectl describe pod web-7d8` |
| `kubectl apply` | Create/update from manifests | `kubectl apply -f deployment.yaml` |
| `kubectl delete` | Delete resources | `kubectl delete -f deployment.yaml` |
| `kubectl logs` | Read Pod/container logs | `kubectl logs deployment/web` |
| `kubectl exec` | Run a command in a container | `kubectl exec -it pod/web -- sh` |
| `kubectl rollout` | Inspect/manage rollouts | `kubectl rollout status deploy/web` |
| `kubectl scale` | Change replica count | `kubectl scale deploy/web --replicas=3` |
| `kubectl port-forward` | Forward local port | `kubectl port-forward svc/web 8080:80` |
| `kubectl config` | Manage kubeconfig contexts | `kubectl config get-contexts` |

---

## 4. Real-Time Project Usage

A typical Kubernetes deployment workflow:

1. CI builds and scans a versioned container image.
2. The image is pushed to a registry.
3. A Deployment references the image.
4. Kubernetes schedules Pods onto suitable nodes.
5. A Service provides network access.
6. Probes influence traffic and recovery.
7. Rolling updates change replicas gradually.
8. Metrics and logs are collected for troubleshooting.

---

## 5. Practical Example

### Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: university-web
spec:
  replicas: 3
  selector:
    matchLabels:
      app: university-web
  template:
    metadata:
      labels:
        app: university-web
    spec:
      containers:
        - name: web
          image: registry.example/university-web:1.0.0
          ports:
            - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: university-web
spec:
  selector:
    app: university-web
  ports:
    - port: 80
      targetPort: 8080
```

### Apply the configuration

```bash
kubectl apply -f app.yaml
kubectl get pods
kubectl get svc
kubectl rollout status deployment/university-web
kubectl logs deployment/university-web
```

---

## 6. Alternatives & Comparison

| Platform | Strength | When to Consider |
|---|---|---|
| Kubernetes | Broad ecosystem and declarative orchestration | Cloud-native production platforms and complex workloads |
| HashiCorp Nomad | Focused scheduler with services and batch jobs | Smaller operational footprint or mixed workload scheduling |
| Docker Swarm | Simple Docker-native orchestration | Small environments where advanced Kubernetes features are unnecessary |
| Amazon ECS | AWS-managed container orchestration | Organizations standardizing on AWS-managed services |

---

## 7. Best Practices & Troubleshooting

- Use namespaces and RBAC.
- Set resource requests and limits appropriately.
- Use readiness/liveness probes where meaningful.
- Keep manifests in Git.
- Use rolling updates and controlled rollbacks.
- Troubleshoot Pod status, events, logs, Services/endpoints, networking and node health.
- Protect Secrets and avoid committing credentials.

---

## 8. Suggested Internship Mini-Project

Deploy a two-tier application to a local or managed cluster.

The project should:

1. Create Deployment and Service manifests.
2. Configure probes and resources.
3. Perform a rolling update.
4. Scale replicas.
5. Inspect logs.
6. Simulate a failed rollout.
7. Perform a rollback.

---

## Conclusion

Kubernetes is a core orchestration skill.

Focus on:

- Control plane
- Pods
- Deployments
- Services
- Configuration
- Security
- Scaling
- Troubleshooting

## References

- Kubernetes Cluster Architecture https://kubernetes.io/docs/concepts/architecture/
- kubectl Reference  https://kubernetes.io/docs/reference/kubectl/
- Kubernetes Nodes   https://kubernetes.io/docs/concepts/architecture/nodes/
