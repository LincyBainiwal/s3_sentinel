# Terraform + Sentinel S3 Policy Learning Project

A hands-on learning project demonstrating how to integrate **Sentinel Policy as Code** with **Terraform** to enforce AWS S3 security best practices.

## 📋 Project Overview

This project enforces that all S3 buckets have public access block configurations enabled with all 4 conditions set to true:
- ✅ `block_public_acls`
- ✅ `ignore_public_acls`  
- ✅ `block_public_policy`
- ✅ `restrict_public_buckets`

## 📁 Project Structure

```
learnsentinel/
├── main.tf                    # Root Terraform configuration
├── variables.tf               # Input variables
├── outputs.tf                 # Output values
├── terraform.tfvars           # Variable values
├── sentinel.hcl               # Sentinel policy configuration
├── .gitignore                 # Git ignore rules
├── README.md                  # This file
│
├── modules/s3/                # S3 Terraform module
│   ├── main.tf
│   ├── variables.tf
│   └── outputs.tf
│
└── policies/s3/               # Policy metadata
    ├── s3-block-public-access-bucket-level.json
    └── README.md
```

## 🚀 Quick Start

### Prerequisites
- Terraform >= 1.0
- Sentinel CLI installed
- AWS credentials (optional, for actual deployment)

### Installation
```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/learnsentinel.git
cd learnsentinel

# Initialize Terraform
terraform init

# Validate configuration
terraform validate
```

### Run Terraform + Sentinel

```bash
# Create Terraform plan
terraform plan

# Apply Sentinel policy
sentinel apply -config=sentinel.hcl
```

**Expected output:**
```
Pass - s3-block-public-access-bucket-level
```

## 📚 Learning Path

1. **Understand Terraform** - Review `main.tf` and module structure
2. **Learn Sentinel** - Check `sentinel.hcl` policy configuration
3. **Test Compliance** - Modify configs to see policy failures
4. **Experiment** - Add more policies or resources

## 🔄 Workflow

```
Write Code → terraform validate → terraform plan → sentinel apply → terraform apply
```

## 📖 Sentinel Policy

**Source:** [GitHub - policy-library-fsbp-policy-set-for-aws-terraform](https://github.com/LincyBainiwal/policy-library-fsbp-policy-set-for-aws-terraform)

The policy validates that:
- All S3 buckets have public access block resources
- All 4 conditions are enabled: block ACLs, ignore ACLs, block policies, restrict access

**Enforcement Level:** `advisory` (warning only, can override)

## 🧪 Testing

### Test Compliant Config (Should Pass)
```bash
terraform plan
sentinel apply -config=sentinel.hcl
# ✅ Pass
```

### Test Non-Compliant Config (Should Fail)
Edit `modules/s3/main.tf` and set `block_public_acls = false`
```bash
terraform plan
sentinel apply -config=sentinel.hcl
# ❌ Fail
```

## 🔐 Security Notes

- `.tfvars` files with secrets are in `.gitignore`
- `.terraform/` directory is ignored (lightweight repo)
- Always keep credentials secure (use AWS profiles)

## 📝 Configuration

Edit these files to customize:
- **terraform.tfvars** - Change bucket name, region, environment
- **sentinel.hcl** - Change enforcement level (advisory → hard-mandatory)
- **modules/s3/main.tf** - Add more S3 configurations

## 🛠️ Troubleshooting

**Error: "Import tfplan/v2 is not available"**
- This is expected when running standalone Sentinel
- Sentinel policies need Terraform Cloud/Enterprise context in production

**Error: "bucket_name required"**
- Edit `terraform.tfvars` and provide a unique bucket name

## 📚 Resources

- [Sentinel Language Docs](https://docs.hashicorp.com/sentinel/language/)
- [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws)
- [AWS Security Hub - S3 Controls](https://docs.aws.amazon.com/securityhub/latest/userguide/s3-controls.html)

## 💡 Next Steps

- [ ] Add more Sentinel policies (RDS, IAM, Networking)
- [ ] Integrate with GitHub Actions CI/CD
- [ ] Connect to Terraform Cloud for remote policy enforcement
- [ ] Add policy tests and test cases
- [ ] Create custom policies for organization standards

## 📄 License

Based on HashiCorp's [Foundational Security Best Practices Policy Library](https://github.com/hashicorp/terraform-foundational-policies-library)

## 👤 Author

[Your Name] - Learning Sentinel & Terraform Integration

## 🤝 Contributing

Feel free to fork and create pull requests with improvements!

---

**Happy Learning! 🚀**
