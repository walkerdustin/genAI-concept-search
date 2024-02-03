# Manage Ubuntu Linux

This is a guide to setting up an environemt in wsl for running Ollama locally on windows.

## Setup

```bash
sudo apt update && sudo apt upgrade
```

```bash
sudo apt-get autoclean
sudo apt-get clean
sudo apt-get autoremove
```

## python setup

```bash
sudo apt install python3.10-venv
source venv/bin/activate
python -m pip install --upgrade pip
```

## ollama

```bash
curl https://ollama.ai/install.sh | sh
```
