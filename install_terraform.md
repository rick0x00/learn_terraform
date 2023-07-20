# [Install Terraform](https://developer.hashicorp.com/terraform/tutorials/docker-get-started/install-cli#install-terraform)

---

install basic dependencies

```bash
    apt update
    apt install -y gnupg software-properties-common
```

---

Install the HashiCorp GPG key.

```bash
    wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor |  tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
```

---

Verify the key's fingerprint.

```bash
    gpg --no-default-keyring --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg --fingerprint
```

---

Add the official HashiCorp repository to your system.

```bash
    echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" |  tee /etc/apt/sources.list.d/hashicorp.list
```

---

Update package list of repositories

```bash
    apt update
```

---

Install Terraform from the apt command

```bash
    apt install terraform
```

---

Verify the installation

```bash
    terraform --help
```

---

Enable Terraform autocompletion

```bash
    terraform -install-autocomplete
```
