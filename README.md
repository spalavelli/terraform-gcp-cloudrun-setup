# Terraform Configuration for GCP: PostgreSQL, Cloud Run, and Internal Load Balancer

This repository contains Terraform configuration files to create and manage the following Google Cloud Platform (GCP) resources:

- A PostgreSQL database instance
- A Cloud Run service
- An internal load balancer

## Prerequisites

Before you begin, ensure you have the following:

- [Terraform](https://www.terraform.io/downloads.html) installed.
- A GCP project.
- GCP credentials with the appropriate permissions (e.g., Cloud SQL Admin, Cloud Run Admin, Compute Admin).
- A `credentials.json` file containing your GCP service account key.

## Configuration

1. **Clone the repository:**

    ```bash
    git clone https://github.com/srinivas951568/terraform-gcp-cloudrun-setup.git
    cd your-repo
    ```

2. **Set up your GCP credentials:**

    Ensure you have a `credentials.json` file in the repository root. This file should contain your GCP service account key.

3. **Edit the Terraform configuration:**

    Update the `provider "google"` block in `main.tf` with your GCP project details:

    ```hcl
    provider "google" {
      project     = "rns-project-id"
      region      = "us-central1"
      zone        = "us-central1-a"
      credentials = file("./credentials.json")
    }
    ```

## Deployment

1. **Initialize Terraform:**

    Run the following command to initialize Terraform and install the necessary providers:

    ```bash
    terraform init
    ```

2. **Apply the configuration:**

    Run the following command to create the resources:

    ```bash
    terraform apply
    ```

    Review the planned changes and type `yes` to confirm the deployment.

## Resources

This Terraform configuration will create the following resources:

- **PostgreSQL Database Instance:**
    - Name: `rns-db-instance`
    - Version: PostgreSQL 13
    - Tier: `db-g1-small`
    - Region: `us-central1`

- **Cloud Run Service:**
    - Name: `rns-cloud-run-service`
    - Location: `us-central1`
    - Image: `nginx:latest`
    - Traffic: 100% to the latest revision

- **Internal Load Balancer:**
    - Forwarding Rule: `rns-ilb-forwarding-rule`
    - Backend Service: `rns-ilb-backend-service`
    - Health Check: `rns-ilb-health-check`
    - Port: 80

## Clean Up

To delete all the resources created by this Terraform configuration, run:

```bash
terraform destroy
# terraform-gcp-cloudrun-setup
