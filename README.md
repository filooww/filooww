<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=26&duration=3000&pause=1000&color=00D9FF&center=true&vCenter=true&width=650&lines=Hi%2C+I'm+Ivan+%F0%9F%91%8B;DevOps+Engineer;AWS+Certified+Solutions+Architect;Kubernetes+%C2%B7+GitOps+%C2%B7+Terraform;Ship+small%2C+ship+often%2C+roll+back+fast" alt="Hi, I'm Ivan — DevOps Engineer" />

**DevOps Engineer** · Plovdiv, Bulgaria

*I build infrastructure, automate deployments, and break things in staging so they don't break in production.*

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ivan-pavlenko-devops)
[![Email](https://img.shields.io/badge/Email-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:vanapawlenco25@gmail.com)

<br/>

<a href="https://www.credly.com/badges/dfcaf925-7ba3-45a1-bde6-13eb1d0873e5"><img src="https://images.credly.com/size/220x220/images/0e284c3f-5164-4b21-8660-0d84737941bc/image.png" width="110" alt="AWS Certified Solutions Architect – Associate" /></a>

**AWS Certified Solutions Architect – Associate** · Oct 2026
<br/><sub>[Verify on Credly](https://www.credly.com/badges/dfcaf925-7ba3-45a1-bde6-13eb1d0873e5)</sub>

</div>

---

### ⭐ Featured: Django on Kubernetes, end-to-end GitOps

[**django-app**](https://github.com/filooww/django-app) · [**django-gitops**](https://github.com/filooww/django-gitops)

![pipeline](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Ffilooww%2Fdjango-app%2Fbadges%2Fpipeline.json&cacheSeconds=300) ![cve](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Ffilooww%2Fdjango-app%2Fbadges%2Fcve.json&cacheSeconds=300) ![canary](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Ffilooww%2Fdjango-app%2Fbadges%2Fcanary.json&cacheSeconds=300) ![k8s](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Ffilooww%2Fdjango-app%2Fbadges%2Fk8s.json&cacheSeconds=300)

A Django + PostgreSQL service deployed two ways: on a self-built 3-node Kubernetes cluster (Kubespray, arm64) and on AWS EC2 with Terraform and Ansible.
CI only builds, scans and publishes the image; the cluster pulls new versions on its own and rolls back a bad release by itself. The badges above are live data from CI and the cluster.

```mermaid
flowchart TB
  subgraph CI["CI · GitHub Actions"]
    direction LR
    src[git tag / push to main] --> build[lint · test · Trivy] --> ghcr[(ghcr.io)]
  end
  subgraph K8S["Kubernetes · pull-based CD"]
    direction LR
    iu[Image Updater] --> repo[(django-gitops)] --> argo[Argo CD] --> ro[Rollouts canary<br/>auto-rollback]
  end
  subgraph AWS["AWS EC2 · Terraform + Ansible"]
    direction LR
    tf[Terraform<br/>VPC · EC2 · EBS · IAM] --> ans[Ansible over SSM] --> ec2[Django + PostgreSQL]
  end
  subgraph SEC["Secrets"]
    direction LR
    vault[(Vault)] --> eso[External Secrets]
  end
  CI -. semver tag .-> K8S
  CI -. commit SHA .-> AWS
  SEC -- secrets --> K8S
```

- **Gitflow** with protected `main` / `develop`: merge only through a PR with a green `ci` check
- **Pull-based CD**: CI has no access to the cluster or the GitOps repo
- **Secrets in Vault**, delivered by External Secrets Operator; Git holds references only
- **Canary with automatic rollback** (Argo Rollouts): 25% of pods → smoke test → 100%; a release that is not ready in 180 s is aborted and traffic stays on the stable version
- **AWS EC2 deployment**: Terraform (VPC, security groups, EBS, IAM per server, S3 state with locking) and 7 idempotent Ansible roles; admin access through SSM, no SSH port open
- **Security checks in CI**: Trivy for the image and for Terraform, TFLint, ansible-lint; PostgreSQL connections over TLS with CA verification; daily EBS snapshots and `pg_dump` to S3
- **Helm chart** with migrations as a Job, probes, non-root read-only containers

---

### 🚀 Other projects

| Project | What it does | Stack |
|---|---|---|
| [**k8s-gitops-platform**](https://github.com/filooww/k8s-gitops-platform) | App-of-apps GitOps platform, HPA verified under k6 load, Trivy-gated CI | Kubernetes · Argo CD · Helm · Prometheus · k6 |
| [**devops-iac-aws**](https://github.com/filooww/devops-iac-aws) | Provision → configure → auto-deploy a Flask app on EC2 | Terraform · Ansible · AWS · GitHub Actions |
| [**auto-vpn**](https://github.com/filooww/auto-vpn) | Auto-connecting corporate VPN with TOTP and a watchdog | Python · Bash · OpenVPN |
| [**crm-free-agents**](https://github.com/filooww/crm-free-agents) | Real-time support-agent availability panel on top of a CRM | JavaScript · Shadow DOM |
| [**Vocab_Reader**](https://github.com/filooww/Vocab_Reader) | IELTS/SAT reading practice with AI provider failover and TTS | Node.js · Express · Redis · Fly.io |

---

### 🛠️ Stack

![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white)
![Helm](https://img.shields.io/badge/Helm-0F1689?style=for-the-badge&logo=helm&logoColor=white)
![Argo CD](https://img.shields.io/badge/Argo_CD-EF7B4D?style=for-the-badge&logo=argo&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Vault](https://img.shields.io/badge/Vault-FFEC6E?style=for-the-badge&logo=vault&logoColor=black)
<br/>
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white)
![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=for-the-badge&logo=ansible&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)
![Trivy](https://img.shields.io/badge/Trivy-1904DA?style=for-the-badge&logo=trivy&logoColor=white)
<br/>
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white)
![k6](https://img.shields.io/badge/k6-7D64FF?style=for-the-badge&logo=k6&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)

---

### 🌱 Now

- **Working on:** production-like load testing of the Django stack: k6 scenarios, Prometheus/Grafana, HPA, PgBouncer
- **Learning:** OpenTelemetry · Loki & Tempo · Kubernetes NetworkPolicies

---

<div align="center">

<img src="https://github-readme-stats.vercel.app/api?username=filooww&show_icons=true&theme=tokyonight&hide_border=true&count_private=true" height="160" />
<img src="https://streak-stats.demolab.com?user=filooww&theme=tokyonight&hide_border=true" height="160" />

</div>
