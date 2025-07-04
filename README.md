# GovCloud Onboarding Framework

Simulates secure, AWS-native account provisioning infrastructure using CloudFormation. Includes VPC creation, centralized Transit Gateway routing, and least-privilege multi-environment networking.

- Segmented VPCs for Dev, Shared Services, and Prod
- Centralized routing using AWS Transit Gateway (TGW)
- Propagation via a single TGW Route Table
- Optional hybrid connectivity (On-Prem via Direct Connect)

---

## 📐 Architecture Overview

![GovCloud Onboarding Framework Architecture](architecture/GovCloudArchitecture.png)

---

## 🧱 Stack Overview

| File                            | Purpose                                |
|--------------------------------|---------------------------------------|
| `vpc-dev.yaml`                 | Dev VPC (10.0.0.0/16)                 |
| `vpc-shared.yaml`              | Shared Services VPC (10.10.0.0/16)    |
| `vpc-prod.yaml`                | Prod VPC (10.20.0.0/16)               |
| `tgw-create.yaml`              | Transit Gateway resource               |
| `tgw-attach-dev.yaml`          | TGW attachment for Dev VPC             |
| `tgw-attach-shared.yaml`       | TGW attachment for Shared VPC          |
| `tgw-attach-prod.yaml`         | TGW attachment for Prod VPC            |
| `tgw-route-attach-dev.yaml`    | TGW route table creation + Dev prop    |
| `tgw-route-attach-shared.yaml` | TGW route propagation for Shared VPC   |

> ✅ All VPCs are attached and propagating to `tgw-rtb-00995db6cb853e946`  
> ✅ Central TGW: `tgw-082e28f65a5016d0e`

---

## 🚀 Deployment Example

```bash
aws cloudformation deploy \
  --template-file cloudformation/vpc-dev.yaml \
  --stack-name govcloud-vpc-dev \
  --region us-east-1 \
  --capabilities CAPABILITY_NAMED_IAM
```

Repeat for each VPC, attachment, and route table propagation.

---

## 🔍 Key Concepts Simulated

- Multi-account architecture (Dev, Shared, Prod)
- Transit Gateway + centralized routing
- Least-privilege route propagation
- Scalable GovCloud patterns
- Visual documentation aligned with deployed infra

---

## 📁 File Structure

```bash
govcloud-onboarding-framework/
├── cloudformation/         # All CloudFormation templates
├── architecture/           # Final network architecture diagrams
│   └── GovCloudArchitecture.png
└── README.md
```

---

## ✅ Project Status

- [x] VPCs deployed (Dev, Shared, Prod)
- [x] TGW deployed + attached
- [x] Routing + propagation complete
- [x] Diagram finalized + embedded

---

## 🔁 Quick Deploy Option

To launch the Dev, Shared, and Prod VPCs along with the Transit Gateway:

```bash
./deploy.sh
```

📌 After running the script, edit it to add your real VPC/Subnet/TGW IDs for the TGW attachments and route table propagation.

This keeps deployment simple and structured.