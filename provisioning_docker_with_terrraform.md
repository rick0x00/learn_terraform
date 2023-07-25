# PROVISIONING DOCKER WITH TERRAFORM

---
---

## First steps

Create work directory

```bash
    mkdir learn-terraform-docker-container
    cd learn-terraform-docker-container
```

Create Terraform provisioning file(main.tf)

```hcl
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.1"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name         = "nginx"
  keep_locally = false
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "tutorial"

  ports {
    internal = 80
    external = 8000
  }
}
```

---

## Initialize the directory

initialize the directory now

```bash
terraform init
```

---

## Format and validate the configuration

Format your configuration

```bash
terraform fmt
```

Format your configuration

```bash
terraform validate
```

---

## Create infrastructure

Show changes required by the current configuration

```bash
terraform plan
```

Apply the configuration now

```bash
terraform apply
```

Verify on Web Browser or curl command if the "localhost:8000" return the NGINX Page

```bash
curl localhost:8000
```

Verify docker container created using Docker commands

```bash
docker ps -a
```

---

## Inspect state

Inspect the current state

```bash
terraform show
```

```bash
terraform state list
```

---

## Update configuration

Replacing the ports.external value of 8000 with 8080

```bash
sed -i "/external/s/8000/8080/" main.tf
```

Apply Changes

```bash
terraform apply
```

---

## Define Input Variables

Create a new file called "variables.tf" with the following content

```hcl
variable "container_name" {
  description = "Value of the name for the Docker container"
  type        = string
  default     = "ExampleNginxContainer"
}
```

in "main.tf", update the "docker_container" resource block to use the new variable

```bash
sed -i '/name  = "tutorial"/s/"tutorial"/var.container_name/' main.tf
```

Apply the modifications on the infrastructure

```bash
terraform apply
```

To replace the default variable value use the option "-v" on CLI

```bash
terraform apply -var "container_name=NewVarValue"
```

---

## Query Data with Outputs

Create a file called "outputs.tf"

```hcl
output "container_id" {
  description = "ID of the Docker container"
  value       = docker_container.nginx.id
}

output "image_id" {
  description = "ID of the Docker image"
  value       = docker_image.nginx.id
}
```

Apply the modifications on the infrastructure

```bash
terraform apply
```

Inspect output values

```bash
terraform output
```

---

## Destroy Infrastructure

Destroying

```bash
terraform destroy
```
