# INSTALL DOCKER ENGINE

---

Install Docker Engine

- [Install Docker](https://docs.docker.com/engine/install/debian/)

```bash
# Install using the convenience script
# Download script
curl -fsSL https://get.docker.com -o get-docker.sh
# Show the script will run
sh ./get-docker.sh --dry-run
# Run the script, and install docker
sh get-docker.sh
# test Docker installation
docker version
docker run hello-world
# Setting docker to rootless execution
usermod -aG docker $USER
su -c "docker run hello-world" $USER
```
