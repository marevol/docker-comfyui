FROM nvidia/cuda:12.1.0-cudnn8-devel-ubuntu22.04

RUN apt-get update && apt-get install -y \
    software-properties-common \
    build-essential \
    wget \
    git \
    curl \
    python3.11 \
    python3.11-venv \
    python3.11-dev \
    && rm -rf /var/lib/apt/lists/*

RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.11 1

WORKDIR /app

RUN git clone https://github.com/comfyanonymous/ComfyUI.git
WORKDIR /app/ComfyUI

RUN python3 -m venv venv \
    && . venv/bin/activate \
    && pip install --upgrade pip \
    && pip install xformers!=0.0.18 -r requirements.txt --extra-index-url https://download.pytorch.org/whl/cu121

CMD ["sh", "-c", ". venv/bin/activate && python main.py --listen 0.0.0.0 --input-directory /app/ComfyUI/input --output-directory /app/ComfyUI/output"]
