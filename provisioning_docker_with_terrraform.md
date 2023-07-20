# PROVISIONING DOCKER WITH TERRAFORM

---

Create work directory

```bash
    mkdir learn-terraform-docker-container
    cd learn-terraform-docker-container
```

---

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

Initialize the project

```bash
    terraform init
```

---

Provisioning the project

```bash
    terraform apply
```

---

Verify on Web Browser or curl command if the "localhost:8000" return the NGINX Page

```bash
    curl localhost:8000
```

---

Verify docker container created using Docker commands

```bash
    docker ps -a
```

---

Destroy the terraform Project

```bash
    terraform destroy
```
