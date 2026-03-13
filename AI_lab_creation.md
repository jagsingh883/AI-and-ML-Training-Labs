# 🧠 Local AI/ML Lab on Ubuntu

### Ollama + Open WebUI + Docker + Python

This guide shows how to build a **local AI/ML experimentation
environment** using:

-   Ollama -- Local LLM runtime
-   Open WebUI -- ChatGPT-style interface
-   Docker -- Container runtime
-   Python virtual environments -- AI development
-   LangChain / Transformers -- AI development tools

------------------------------------------------------------------------

# Architecture

Browser → Open WebUI → Ollama API → Local Models

Python AI scripts can also call the Ollama API directly.

------------------------------------------------------------------------

# System Requirements

Recommended:

CPU: 8 cores\
RAM: 16--32 GB\
Storage: 100GB+\
GPU: Optional NVIDIA GPU

Supported OS: - Ubuntu 22.04 LTS - Ubuntu 24.04 LTS

------------------------------------------------------------------------

# 1 Update Ubuntu

``` bash
sudo apt update && sudo apt upgrade -y
sudo apt install -y build-essential git curl wget unzip
```

------------------------------------------------------------------------

# 2 Install Python Environment

``` bash
sudo apt install -y python3 python3-pip python3-venv
```

Create workspace

``` bash
mkdir ~/ai-lab
cd ~/ai-lab
```

Create virtual environment

``` bash
python3 -m venv ai-env
```

Activate environment

``` bash
source ai-env/bin/activate
```

Upgrade pip

``` bash
pip install --upgrade pip
```

------------------------------------------------------------------------

# 3 Install AI/ML Libraries

``` bash
pip install numpy pandas matplotlib scikit-learn
pip install torch torchvision torchaudio
pip install jupyterlab notebook
pip install transformers datasets accelerate
pip install langchain
pip install chromadb
pip install sentence-transformers
```

------------------------------------------------------------------------

# 4 Install Docker

``` bash
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
```

Add user to docker group

``` bash
sudo usermod -aG docker $USER
newgrp docker
```

Test docker

``` bash
docker run hello-world
```

------------------------------------------------------------------------

# 5 Install Ollama

``` bash
curl -fsSL https://ollama.com/install.sh | sh
```

Verify

``` bash
ollama --version
```

------------------------------------------------------------------------

# 6 Pull AI Models

Example models

``` bash
ollama pull llama3
ollama pull mistral
ollama pull phi3
ollama pull deepseek-coder
```

List models

``` bash
ollama list
```

Run test model

``` bash
ollama run llama3
```

------------------------------------------------------------------------

# 7 Verify Ollama API

``` bash
curl http://localhost:11434/api/tags
```

Expected output

``` json
{"models":[{"name":"llama3"}]}
```

------------------------------------------------------------------------

# 8 Install Open WebUI

Remove existing container

``` bash
docker rm -f open-webui
```

Run WebUI

``` bash
docker run -d --name open-webui --network host -v open-webui:/app/backend/data ghcr.io/open-webui/open-webui:main
```

Open browser

http://localhost:8080

------------------------------------------------------------------------

# 9 Connect WebUI to Ollama

Inside WebUI

Settings → Connections → Ollama

Endpoint

http://localhost:11434

Refresh models.

------------------------------------------------------------------------

# Useful Docker Commands

List containers

``` bash
docker ps
```

Stop container

``` bash
docker stop open-webui
```

Restart container

``` bash
docker restart open-webui
```

Remove container

``` bash
docker rm open-webui
```

Stop all containers

``` bash
docker stop $(docker ps -q)
```

------------------------------------------------------------------------

# Suggested Project Structure

ai-lab/

models/ notebooks/ rag-projects/ agents/ datasets/ experiments/

------------------------------------------------------------------------

# Security Notes

The docker group has root level privileges. Anyone in this group can
potentially gain root access to the host system.

For production systems consider:

-   Rootless Docker
-   Container security policies
-   Image scanning

------------------------------------------------------------------------

# Future Enhancements

Possible upgrades:

-   GPU acceleration (CUDA)
-   Vector databases
-   RAG pipelines
-   AI agents
-   Local coding assistants

------------------------------------------------------------------------

# License

MIT
