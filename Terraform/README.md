# Terraform

## 1. Brief Introduction

Terraform is an Infrastructure as Code (IaC) tool used to define, provision, change and version infrastructure.

It can manage compute, networking, storage, DNS and many higher-level services through providers.

Terraform represents infrastructure as configuration stored in version control.

The common workflow is:

**Initialize → Format → Validate → Plan → Review → Apply**

Terraform maintains state to map configuration resources to real-world objects.

---

## 2. Terraform Architecture

Terraform CLI reads configuration, loads required providers and compares desired configuration with state and provider APIs.

Providers translate Terraform resources into operations against cloud or service platforms.

| Component | Role |
|---|---|
| Terraform CLI | Runs initialization, planning, application, validation and state operations |
| Configuration | Declarative `.tf` files describing desired infrastructure |
| Provider | Plugin that lets Terraform interact with a platform/API |
| Resource | Managed object such as VM, network or DNS record |
| Module | Reusable collection of Terraform configuration |
| State | Mapping between Terraform resources and real-world objects plus metadata |
| Backend | Location/mechanism for storing state, often remotely for teams |

---

## 3. Key Commands

| Command | Purpose | Example |
|---|---|---|
| `terraform init` | Initialize directory and providers | `terraform init` |
| `terraform fmt` | Format configuration | `terraform fmt -recursive` |
| `terraform validate` | Validate configuration | `terraform validate` |
| `terraform plan` | Preview changes | `terraform plan` |
| `terraform apply` | Apply changes | `terraform apply` |
| `terraform destroy` | Destroy managed resources | `terraform destroy` |
| `terraform show` | Inspect state/plan | `terraform show` |
| `terraform output` | Show outputs | `terraform output` |
| `terraform providers` | Show provider requirements | `terraform providers` |
| `terraform state list` | List resources in state | `terraform state list` |
| `terraform state show` | Inspect a resource in state | `terraform state show aws_instance.web` |

---

## 4. Real-Time Project Usage

A typical Terraform workflow:

1. Create reusable infrastructure modules and store them in Git.
2. Run format and validation in CI.
3. Generate a plan for every infrastructure change.
4. Review the plan before applying.
5. Use remote state and locking where appropriate.
6. Separate environments deliberately.
7. Use CI/CD approvals for production applies.
8. Keep credentials outside source code using recommended identity/secrets mechanisms.

---

## 5. Practical Example

```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 6.0"
    }
  }
}

provider "aws" {
  region = "us-east-1"
}

resource "aws_s3_bucket" "logs" {
  bucket = "example-university-logs-unique"
}

output "bucket_name" {
  value = aws_s3_bucket.logs.bucket
}
```

### Initialize

```bash
terraform init
```

### Format

```bash
terraform fmt
```

### Validate

```bash
terraform validate
```

### Plan

```bash
terraform plan
```

### Apply

```bash
terraform apply
```

Provider/resource schemas depend on the selected platform and provider version.

In production, use reviewed modules, remote state and controlled CI/CD rather than unmanaged manual applies.

---

## 6. Alternatives & Comparison

| Tool | Strength | Typical Fit |
|---|---|---|
| Terraform | Multi-provider declarative IaC and large ecosystem | Multi-cloud and heterogeneous infrastructure |
| Pulumi | IaC using general-purpose languages | Teams preferring TypeScript, Python, Go, C# or Java |
| AWS CloudFormation | AWS-native infrastructure automation | AWS-only environments wanting native integration |
| Azure Bicep | Azure-native declarative IaC | Azure-focused environments |
| Ansible | Configuration/operational automation | Post-provision configuration; complementary rather than identical to Terraform |

---

## 7. Best Practices & Troubleshooting

- Review Terraform changes like application code.
- Use modules to reduce duplication.
- Protect state because it may contain sensitive values.
- Use remote state and locking for team workflows.
- Pin provider versions and review upgrades.
- Inspect `terraform plan` before applying important changes.
- Use `terraform state` commands carefully.
- Keep secrets out of `.tf` files and source control.

---

## 8. Suggested Internship Mini-Project

Provision a small cloud environment containing:

- A network
- A compute resource
- A storage component

The project should:

1. Store the code in Git.
2. Add variables and outputs.
3. Create a reusable module.
4. Execute `init`, `fmt`, `validate`, `plan` and `apply`.
5. Document state storage and protection.

---

## Conclusion

Terraform is a core DevOps IaC skill because it makes infrastructure repeatable, reviewable and version-controlled.

Important areas include:

- Providers
- Resources
- Modules
- Plan/apply workflow
- State management

## References

- Terraform Documentation https://developer.hashicorp.com/terraform/docs
- Terraform CLI https://developer.hashicorp.com/terraform/cli/commands
- Terraform State https://developer.hashicorp.com/terraform/language/state
- Terraform State Commands https://developer.hashicorp.com/terraform/cli/commands/state
