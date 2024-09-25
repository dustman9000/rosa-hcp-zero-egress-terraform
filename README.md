# ROSA HCP Zero Egress Terraform

This repository contains Terraform configurations to set up an AWS Virtual Private Cloud (VPC) for a Red Hat OpenShift Service on AWS (ROSA) Hypershift (HCP) cluster with zero egress. This setup ensures that all cluster traffic remains within the AWS network, eliminating the need for internet access (egress) for the cluster.

## Features

- **Zero egress configuration:** All network traffic for the ROSA HCP cluster is restricted to the AWS VPC.
- **Customizable networking:** Allows for flexible configuration of subnets, route tables, and security groups.
- **Automated setup:** Utilizes Terraform to automate the creation and configuration of the VPC and associated resources.

## Prerequisites

Before you begin, ensure that you have the following:

- [Terraform](https://www.terraform.io/downloads.html) installed
- AWS CLI configured with proper permissions to manage VPC, subnets, and other resources
- A ROSA account with permissions to deploy ROSA HCP clusters

## Getting Started

1. **Clone the repository:**

   ```bash
   git clone https://github.com/your-org/rosa-hcp-zero-egress-terraform.git
   cd rosa-hcp-zero-egress-terraform
   ```

2. **Initialize Terraform:**

   Run the following command to initialize the Terraform configuration and install any necessary plugins.

   ```bash
   terraform init
   ```

3. **Customize Variables:**

   Modify the `terraform.tfvars` file or pass in variables via the command line to suit your needs. The following variables are configurable:

   - `vpc_cidr_block`: The CIDR block for the VPC.
   - `private_subnets`: List of CIDR blocks for private subnets.
   - `availability_zones`: List of AWS availability zones for the subnets.
   - `region`: AWS region where the resources will be created.
   - `cluster_name`: Unique ROSA HCP cluster name.

4. **Deploy the VPC:**

   Apply the Terraform configuration to create the AWS VPC and related resources.

   ```bash
   terraform apply
   ```

5. **Review Outputs:**

   After the deployment, Terraform will output the necessary VPC details such as VPC ID, private subnet IDs, and security group IDs. These values will be used when deploying the ROSA HCP cluster.

6. **ROSA HCP Deployment:**

   Once the VPC is ready, follow the Red Hat documentation to deploy your ROSA HCP cluster using the VPC and subnet configurations created by Terraform.

## Variables

| Name               | Description                                            | Type   | Default |
|--------------------|--------------------------------------------------------|--------|---------|
| `vpc_cidr_block`    | CIDR block for the VPC                                 | string | `10.0.0.0/16` |
| `private_subnets`   | List of CIDR blocks for the private subnets             | list   | `["10.0.1.0/24", "10.0.2.0/24"]` |
| `availability_zones`| List of AWS availability zones for the private subnets | list   | `["us-west-2a", "us-west-2b"]` |
| `region`            | AWS region where the resources will be deployed        | string | `us-west-2` |

## Outputs

The following outputs are provided after successful deployment:

- `vpc_id`: The ID of the VPC.
- `private_subnet_ids`: List of private subnet IDs.
- `security_group_id`: ID of the security group created for the VPC.

## Cleanup

To destroy the resources created by this Terraform configuration, run:

```bash
terraform destroy
```
