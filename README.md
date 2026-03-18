# Ollama and Open Web UI on Docker

A useful docker compose file that enables both stacks + GPU support enabled

- To install NVIDIA drivers on WSL follow: https://docs.nvidia.com/cuda/wsl-user-guide/index.html
- For GPU toolkit: https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#installation
- Ollama official docker hub: https://hub.docker.com/r/ollama/ollama
- Open Web UI official: https://docs.openwebui.com/getting-started/

# Ollama + Open WebUI no WSL2 (MX110 2GB) — guia rápido
Como testar de verdade se o Ollama está tentando usar GPU

Rode um modelo pequeno:
```bash
docker exec -it ollama-server ollama pull gemma3:1b
docker exec -it ollama-server ollama run gemma3:1b
```

Rode um modelo maior:
```bash
docker exec -it ollama-server ollama pull qwen3.5:4b
docker exec -it ollama-server ollama run qwen3.5:4b
```

Listar modelos:
```bash
docker exec -it ollama-server ollama list
```

Monitorar GPU:
```bash
docker exec -it ollama-server nvidia-smi -l 1
```

Entrar no container:
```bash
docker exec -it ollama-server bash
```
