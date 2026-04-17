# ORB-SLAM3 Docker Setup

This document covers building the Docker image used by the
[trumi](https://github.com/TrossenRobotics/trumi) SLAM pipeline.

## Prerequisites

- [Docker](https://docs.docker.com/get-started/get-docker/)
- [Git](https://git-scm.com/)

On Linux, the trumi pipeline calls `docker` without `sudo`. Verify this works first:

```bash
docker run hello-world
```

If you see a permission error, add your user to the `docker` group:

```bash
sudo usermod -aG docker $USER
```

Then either log out and log back in, or run `newgrp docker` to apply the change in the current shell.
Re-run `docker run hello-world` to confirm it works.

> **Note:** Members of the `docker` group can run containers as root, which is equivalent to unrestricted `sudo` access. Only add trusted users.

## Setup

**1. Clone the repository**

```bash
git clone https://github.com/TrossenRobotics/ORB_SLAM3.git
cd ORB_SLAM3
```

**2. Pull submodules**

```bash
git submodule update --init --recursive
```

**3. Build the Docker image**

```bash
docker build -t orb_slam3 .
```

This may take several minutes on the first build.

**4. Verify the image was built successfully**

```bash
docker images orb_slam3
```

If the build succeeded, you should see `orb_slam3:latest` listed with its image ID and size.
If the output shows only headers with no image listed, re-run the build step and check for errors.
