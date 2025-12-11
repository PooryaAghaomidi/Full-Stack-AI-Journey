# Development Setup

<p align="center">
  <img src="Images/setup.jpg" width="400"/>
</p>

## Table of Contents

- [Introduction](#introduction)
- [Choosing Your Development Environment](#choosing-your-development-environment)
- [Essential Software Setup](#essential-software-setup)
- [GPU & Driver Setup](#gpu--driver-setup)
- [Python Environment Setup](#python-environment-setup)
- [Jupyter & Notebook Setup](#jupyter--notebook-setup)
- [Docker & Container Setup](#docker--container-setup)
- [SSH & Remote Development](#ssh--remote-development)
- [Environment Variables & Secrets](#environment-variables--secrets)
- [Productivity Tools](#productivity-tools)
- [Final Validation Checklist](#final-validation-checklist)

---

## Introduction

A proper development setup is the foundation of your entire Full-Stack AI Developer Journey.  
If your system is misconfigured — wrong Python version, broken GPU drivers, missing tools — everything else becomes more difficult.

This tutorial ensures you build a **clean, reliable, professional-grade development environment** that supports:

- AI & machine learning
- Deep learning with GPU acceleration
- Backend development
- Data engineering
- MLOps
- Cloud deployment
- Containerized workflows

By the end, you will have a fully configured environment ready for real-world AI development.

---

## Choosing Your Development Environment

Before installing tools, choose *where* you will work.

---

### Local vs Cloud Development

#### Local Machine

✔ Immediate access  
✔ No cost  
✔ Great for learning  
❌ Limited GPU  
❌ Difficult to scale

#### Cloud Machine (AWS/GCP/Azure/RunPod/Lambda)

✔ Access to powerful GPUs (A100, H100, MI300)  
✔ Scalable  
✔ Easy remote access  
❌ Costs money  
❌ Requires security knowledge  

**Recommendation:**  
Start local → move GPU-heavy projects to cloud.

---

### Windows vs Linux for AI Development

#### Linux (Ubuntu) — BEST for AI

✔ Native CUDA, PyTorch support  
✔ Fast command-line tools  
✔ Works well with Docker  

#### Windows

❌ GPU support is harder  
❌ Some packages break  
✔ But WSL2 fixes most issues  

---

### Using WSL2 (Windows Subsystem for Linux)

WSL2 provides a full Linux kernel inside Windows.

**Use WSL2 if:**

- You want to stay on Windows  
- You want Linux-level tools  
- You want native GPU support  

Install Ubuntu with:

```powershell
wsl --install -d Ubuntu
```

---

### Dual Booting Linux

Best for:

- Maximum performance
- Full GPU control
- Offline ML training

---

### ARM vs x86 Considerations

#### x86 (Intel/AMD)

✔ Best compatibility  
✔ CUDA GPU support  
✔ Recommended  

#### ARM (M1/M2/M3 Macs)

✔ Great performance  
❌ CUDA not supported  
✔ PyTorch and TensorFlow support via Metal  

---

### Recommended Environments

#### Beginner

- Windows + WSL2 + Ubuntu  
- No GPU required

#### Intermediate AI Developer

- Ubuntu (20.04 or 22.04)  
- NVIDIA GPU (RTX 3060 or better)

#### Advanced Deep Learning Developer

- Ubuntu  
- RTX 4090 local workstation  
- Cloud GPUs for scale  

---

## Essential Software Setup

---

### Package Managers

#### Windows

Install **Winget** (usually included):

```powershell
winget install Git.Git
```

Optional: Chocolatey

```powershell
Set-ExecutionPolicy Bypass -Scope Process
iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

#### Linux

Ubuntu:

```bash
sudo apt update && sudo apt upgrade
sudo apt install build-essential curl wget git
```

---

### Build Tools

#### Ubuntu

```bash
sudo apt install build-essential cmake pkg-config
```

Required for compiling Python libraries like `torch`, `numpy`, `opencv`.

---

### Git & GitHub Setup

Install Git:

```bash
sudo apt install git
```

Configure:

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

Generate SSH key:

```bash
ssh-keygen -t ed25519
```

---

### Python Installation

Install either:

#### **Option 1 — Miniconda (recommended for beginners)**

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```

#### **Option 2 — pyenv (for pros)**

```bash
curl https://pyenv.run | bash
```

---

### VS Code & Essential Extensions

Extensions to install:

- Python
- Jupyter
- GitLens
- Remote SSH
- Docker
- YAML
- Pylance

---

## GPU & Driver Setup

---

### NVIDIA GPU Drivers

Ubuntu:

```bash
sudo ubuntu-drivers autoinstall
```

Check:

```bash
nvidia-smi
```

---

### CUDA Toolkit

Use the version compatible with PyTorch.

Example:

```bash
sudo apt install cuda-toolkit-12-1
```

---

### cuDNN

Download from NVIDIA website (requires login):

```bash
sudo dpkg -i cudnn-local-repo*.deb
sudo apt install libcudnn8
```

---

### Verifying GPU Setup

Python:

```python
import torch
print(torch.cuda.is_available())
print(torch.cuda.get_device_name(0))
```

---

## Python Environment Setup

---

### venv

```bash
python3 -m venv env
source env/bin/activate
```

---

### conda / miniconda

```bash
conda create -n myenv python=3.10
conda activate myenv
```

---

### pyenv

```bash
pyenv install 3.10.13
pyenv global 3.10.13
```

---

### pipx

Install:

```bash
pip install pipx
pipx ensurepath
```

---

### uv Package Manager

```bash
pip install uv
```

---

## Jupyter & Notebook Setup

---

### Installing Jupyter

```bash
pip install jupyterlab notebook
```

---

### Setting up Kernels

```bash
python -m ipykernel install --user --name=myenv
```

---

### Using VS Code With Jupyter

Choose kernel → Run notebook → GPU supported.

---

### Remote Jupyter Servers

```bash
ssh -L 8888:localhost:8888 user@server
jupyter lab --no-browser --port=8888
```

---

## Docker & Container Setup

---

### Installing Docker

Ubuntu:

```bash
curl -fsSL https://get.docker.com | sudo sh
sudo usermod -aG docker $USER
```

---

### NVIDIA GPU Support for Containers

Install toolkit:

```bash
sudo apt install nvidia-container-toolkit
sudo systemctl restart docker
```

---

### Docker Compose

```bash
sudo apt install docker-compose-plugin
```

---

### Testing GPU in Docker

```bash
docker run --gpus all nvidia/cuda:12.1-base nvidia-smi
```

---

## SSH & Remote Development

---

### Generating SSH Keys

```bash
ssh-keygen -t ed25519
```

---

### Connecting to Remote Servers

```bash
ssh user@server_ip
```

---

### SSH Config File

Edit:

```bash
nano ~/.ssh/config
```

Example:

```shell
Host myserver
    HostName 1.2.3.4
    User ubuntu
    IdentityFile ~/.ssh/id_ed25519
```

---

### VS Code Remote SSH

Install extension → “Remote-SSH: Connect to Host”.

---

### Port Forwarding

```bash
ssh -L 8000:localhost:8000 user@server
```

---

## Environment Variables & Secrets

---

### Global Environment Variables

Edit:

```bash
sudo nano /etc/environment
```

---

### Local Project Variables

Use:

```shell
export API_KEY="123"
```

---

### .env Files

Example:

```shell
DB_USER=admin
DB_PASS=secret
```

---

### direnv

Install:

```bash
sudo apt install direnv
```

---

### Protecting Secrets

- Never commit `.env`  
- Add to `.gitignore`  

---

## Productivity Tools

---

### Terminal Configuration

#### Linux

- Oh-My-Zsh  
- Starship prompt  
- Powerlevel10k  

---

### Multiplexers (tmux)

Install:

```bash
sudo apt install tmux
```

---

### Monitoring Tools

```bash
htop
btop
nvtop
```

---

### Dotfiles

You can store:

- aliases  
- functions  
- editor configs  
- git configs  

Usually via GitHub.

---

## Final Validation Checklist

### Python

✔ `python --version`  
✔ `pip install` works  
✔ venv/conda create environments  

### GPU

✔ `nvidia-smi`  
✔ PyTorch detects GPU  
✔ Docker GPU works  

### VS Code

✔ Extensions installed  
✔ Remote SSH works  
✔ Jupyter kernels recognized  

### Git

✔ Git configured  
✔ SSH key uploaded to GitHub  

### SSH

✔ Can connect to remote VM  
✔ Port forwarding works  

### Docker

✔ Engine & Compose installed  
✔ GPU toolkit installed  

Everything passes = YOU ARE READY.

---

## Note

```text
I will update this tutorial if I acquire any new information.
```

## Sources

```text
Sample
```
