# Time & Cost Analysis – GCP Infrastructure Automation (Terraform + Cloud Build)

This document summarizes the time efficiency and cost impact of automating GCP infrastructure deployment using Terraform and Cloud Build.

# 1. Time Efficiency

## 1.1 Manual Deployment (ClickOps)
Provisioning the environment manually in the GCP Console would require:

| Component | Estimated manual time |
|----------|------------------------|
| VPC + subnets | 10 min |
| Firewall rules | 5 min |
| VM instance (x2) | 5 min |
| IAM configuration | 10 min |
| Connecting GitHub → Cloud Build | 10 min |
| Alert policies + log sink | 10 min |

**Total estimated manual configuration time:** ~50 minutes  

## 1.2 Automated Deployment (Terraform + Cloud Build)

- Full deployment triggered by Cloud Build: **~3 min**
- Minimal human intervention required  

Automation reduced provisioning time from ~50 minutes to ~3 minutes,
making deployments roughly 17× faster than manual configuration.


# 2. Cost Analysis

## 2.1 Based on actual Billing Reports

- **Cloud Build:** 0 USD 
- **Cloud Storage (state bucket + logs):** 0 USD 
- **Logging / Monitoring:** 0 USD 
- **Compute Engine:** 0 USD

Real measured cost so far: **0 USD**

## 2.2 Estimated Monthly Cost (Google Pricing Calculator)

| Component | Project Usage | Free Tier Coverage | Actual Cost |
|---|---|---|---|
| VM Instances (2 × e2-micro) | — | 1 e2‑micro VM is covered → time-based limit (~730 h/month) | **1 VM free, 2nd VM: ~6.11 USD/month** |
| Disks (2× 10 GB) | — | Up to 30 GB-month standard HDD is free | **0 USD** |
| Network egress | — | 1 GB/month is free | **0 USD** (assuming low traffic) |
| Cloud Build | — | Free Tier grants 2,500 build-minutes| **0 USD** |
| Logging & Monitoring | — | Free monthly log ingestion and metrics | **0 USD** |

**Total estimated cost with Free Tier ~6.11 USD/month**


# 3. Interpretation

## Cost Efficiency
The environment is extremely low-cost.  
Most GCP services used in this project fall within Free Tier or generate minimal charges.  
CI/CD and monitoring operations have near-zero operational cost.

## Time & Operational Efficiency
Automation drastically reduces deployment time from ~50 minutes (manual) to ~3 minutes.  
Terraform and Cloud Build enable:

- Consistent deployments with zero manual clicking  
- Full reproducibility across environments  
- Lower risk of misconfiguration  


# 4. Conclusion

Using Terraform and Cloud Build for GCP infrastructure provides:

1. **Massive time savings** – full environment ready in minutes, not hours  
2. **Minimal cost** – most services remain within Free Tier  
3. **Reproducibility & reliability** – predictable and consistent deployments  
4. **Safer operations** – lower risk of misconfiguration, controlled rollbacks  
5. **Scalability & auditability** – infrastructure as code ensures traceable, repeatable processes  

**Overall:** Automation is clearly more efficient, reliable, and cost-effective than manual provisioning, and provides a solid foundation for future scaling and team collaboration.