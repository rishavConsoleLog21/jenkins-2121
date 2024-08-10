# Jenkins BlueOcean Setup with Docker

This guide provides step-by-step instructions for setting up Jenkins BlueOcean using Docker. 

## YouTube Link
For a full 1-hour course on Jenkins, watch on YouTube: [Jenkins Course](https://www.youtube.com/watch?v=6YZvp2GwT0A)

## Installation

### 1. Build the Jenkins BlueOcean Docker Image

You can build the Jenkins BlueOcean Docker image using the following command:

```bash
docker build -t myjenkins-blueocean:2.414.2 .
```

**Note:** If you encounter any issues building the image, you can pull a pre-built version from my registry (version `2.332.3-1`):

```bash
docker pull devopsjourney1/jenkins-blueocean:2.332.3-1
docker tag devopsjourney1/jenkins-blueocean:2.332.3-1 myjenkins-blueocean:2.332.3-1
```

### 2. Create the Network `jenkins`

Create a Docker network named `jenkins` using the command:

```bash
docker network create jenkins
```

### 3. Run the Jenkins BlueOcean Container

#### MacOS / Linux

To run the Jenkins BlueOcean container on MacOS or Linux, use the following command:

```bash
docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  myjenkins-blueocean:2.414.2
```

#### Windows

To run the Jenkins BlueOcean container on Windows, use the following command:

```powershell
docker run --name jenkins-blueocean --restart=on-failure --detach `
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 `
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 `
  --volume jenkins-data:/var/jenkins_home `
  --volume jenkins-docker-certs:/certs/client:ro `
  --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.414.2
```

### 4. Get the Initial Admin Password

Retrieve the initial admin password for Jenkins using the following command:

```bash
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword
```

### 5. Connect to Jenkins

Once the container is running, you can connect to Jenkins by navigating to:

[https://localhost:8080/](https://localhost:8080/)

## Installation Reference

For more details, refer to the official Jenkins Docker installation guide: [Jenkins Docker Installation](https://www.jenkins.io/doc/book/installing/docker/)
```

This `README.md` file provides clear instructions for setting up Jenkins BlueOcean using Docker, including how to handle potential issues and where to find additional resources.
