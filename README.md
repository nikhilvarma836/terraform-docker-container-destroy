# terraform-docker-container-destroy:

# Terraform with Docker: Provision Local Docker Container

## Objective  
Provision a local Docker container using Terraform, enabling you to manage container infrastructure as code (IaC).

## Prerequisites

- Terraform installed (version >= 1.0 recommended)  
  [Terraform installation guide](https://learn.hashicorp.com/tutorials/terraform/install-cli)  
- Docker installed and running locally  
  [Docker installation guide](https://docs.docker.com/get-docker/)  
- Basic understanding of Terraform and Docker

## Step 1: Setup Terraform Project Directory

Create a new directory and navigate into it (already done if you follow this guide).

## Step 2: Write Terraform Configuration (`main.tf`)

Create a file named `main.tf` with the configuration:

```hcl
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 2.13.0"
    }
  }
}

provider "docker" {
  # Connects to local Docker daemon by default
}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}

resource "docker_container" "nginx_container" {
  image = docker_image.nginx.latest
  name  = "nginx_terraform"
  ports {
    internal = 80
    external = 8080
  }
}
```

## Step 3: Initialize Terraform

Run the following command to initialize Terraform and download the Docker provider plugin:

```bash
terraform init
```

## Step 4: Preview Infrastructure Changes

To see what Terraform will do, run:

```bash
terraform plan
```

## Step 5: Apply the Terraform Configuration

To create the Docker container, run:

```bash
terraform apply
```

When prompted, type `yes` to confirm.

## Step 6: Verify Docker Container is Running

Check running containers with:

```bash
docker ps
```

Visit [http://localhost:8080](http://localhost:8080) in your browser to see the Nginx welcome page.

## Step 7: Check Terraform State

To list the resources Terraform manages, run:

```bash
terraform state list
```

## Step 8: Destroy the Infrastructure

When finished, clean up the resources with:

```bash
terraform destroy
```

Confirm with `yes` when prompted.

## Summary of Commands

| Command                 | Purpose                                      |
|-------------------------|----------------------------------------------|
| `terraform init`        | Initialize Terraform and download providers |
| `terraform plan`        | Preview changes Terraform will make          |
| `terraform apply`       | Create resources as per configuration        |
| `terraform state list`  | List Terraform-managed resources             |
| `terraform destroy`     | Remove the resources created                   |

## Deliverables

- `main.tf` — Terraform configuration file
- Execution logs from your terminal showing outputs of:
  - `terraform init`
  - `terraform plan`
  - `terraform apply`
  - `terraform state list`
  - `terraform destroy`
