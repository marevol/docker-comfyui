# ComfyUI Docker Environment

This repository provides a Dockerized environment for running [ComfyUI](https://github.com/comfyanonymous/ComfyUI) with CUDA 12.1 and Python 3.11. The setup includes GPU support and allows you to manage models using a local `models` directory on your host machine.

## Repository Contents

- `comfyui/Dockerfile`: The Dockerfile used to build the ComfyUI Docker image.
- `compose.yaml`: Docker Compose file to manage the ComfyUI service.
- `models/`: A directory where you can store your model files (not included in this repository).

## Prerequisites

- Docker
- Docker Compose
- NVIDIA GPU with CUDA support

## Setup and Usage

### 1. Clone the Repository

```bash
git clone https://github.com/marevol/docker-comfyui.git
cd docker-comfyui
```

### 2. Place Your Models

Add your model files to the `models/` directory. These files will be mounted into the Docker container at runtime.

### 3. Build and Run the Docker Container

Build the Docker image and start the container using Docker Compose:

```bash
docker compose up --build
```

This will build the Docker image and start the ComfyUI service, exposing it on port `8000`.

### 4. Access ComfyUI

Once the container is running, you can access ComfyUI by navigating to `http://localhost:8188` in your web browser.

### 5. Stop the Service

To stop the Docker container, run:

```bash
docker compose down
```

## Directory Structure

```
./
├── comfyui/
│   ├── Dockerfile
│   ├── .dockerignore
├── models/  # Place your model files here
└── compose.yaml
```

## Customization

### Updating ComfyUI

The Dockerfile is configured to pull the latest version of ComfyUI at build time. To update your setup:

1. Pull the latest changes from the ComfyUI repository:

    ```bash
    git pull
    ```

2. Rebuild the Docker image:

    ```bash
    docker compose up --build
    ```

### Adding More Models

To add more models, simply place them in the `models/` directory and restart the Docker container.

```bash
wget -c https://huggingface.co/runwayml/stable-diffusion-v1-5/resolve/main/v1-5-pruned-emaonly.ckpt -P ./models/checkpoints/
wget -c https://huggingface.co/stabilityai/sd-vae-ft-mse-original/resolve/main/vae-ft-mse-840000-ema-pruned.safetensors -P ./models/vae/
```

## Acknowledgments

- [ComfyUI](https://github.com/comfyanonymous/ComfyUI) for providing the base software.
- NVIDIA for providing the CUDA Docker images.

