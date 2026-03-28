# Ollama and Open Web UI on Docker

A useful docker compose file that enables both stacks + GPU support enabled

- To install NVIDIA drivers on WSL follow: https://docs.nvidia.com/cuda/wsl-user-guide/index.html
- For GPU toolkit: https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#installation
- Ollama official docker hub: https://hub.docker.com/r/ollama/ollama
- Open Web UI official: https://docs.openwebui.com/getting-started/

# Ollama + Open WebUI no WSL2 (CPU / GPU MX110 2GB) — guia rápido

Como testar de verdade se o Ollama está tentando usar GPU

- Entrar no container:

```bash
docker exec -it ollama-server bash
```

- Monitorar GPU:

```bash
docker exec -it ollama-server nvidia-smi -l 1
```

- Rode o modelo Gemma:

```bash
docker exec -it ollama-server ollama pull gemma3:1b
docker exec -it ollama-server ollama run gemma3:1b
```

## Qwen small series

Desabilitar thinking

```
--think=false
```

Habilitar as metricas

```
--verbose
```

- Rode o modelo 0.8B:

```bash
docker exec -it ollama-server ollama pull qwen3.5:0.8b
docker exec -it ollama-server ollama run qwen3.5:0.8b
```

- Exemplo: Limites: cpus: 2.5 , mem_limit: 3g, para o modelo padrão Q8 (eval rate: 8.67 tokens/s)

```
ollama run qwen3.5:0.8b --verbose --think=false
/set parameter temperature 0.7
/set parameter num_predict 250
/set parameter num_ctx 1536
/set parameter num_thread 2
```

- Rode o modelo 2B:

```bash
docker exec -it ollama-server ollama pull qwen3.5:2b
docker exec -it ollama-server ollama run qwen3.5:2b
```

- Exemplo: Limites: cpus: 3.5 , mem_limit: 6g, para o modelo padrão Q8 (eval rate: 6.67 tokens/s)

```
ollama run qwen3.5:2b --verbose --think=false
/set parameter temperature 0.7
/set parameter num_predict 250
/set parameter num_ctx 1536
/set parameter num_thread 2
```

- Rode o model 2B quantizado = Q4_K_M

```
ollama run qwen3.5:2b-q4_K_M --verbose --think=false
```

- Exemplo: Limites: cpus: 3.5 , mem_limit: 7g, para o modelo quantizado (eval rate: 7.92 tokens/s)

```
/set parameter temperature 0.7
/set parameter num_predict 250
/set parameter num_ctx 1536
/set parameter num_thread 3
```

- Rode o modelo 4B:

```bash
docker exec -it ollama-server ollama pull qwen3.5:4b
docker exec -it ollama-server ollama run qwen3.5:4b

```

- Rode o model 4B quantizado = Q4_K_M

```
ollama run qwen3.5:4b-q4_K_M --verbose --think=false
```

- Exemplo: Limites: cpus: 4 , mem_limit: 9g, para o modelo quantizado (eval rate: 3.10 tokens/s)

```
/set parameter temperature 0.7
/set parameter num_predict 250
/set parameter num_ctx 1536
/set parameter num_thread 4
```

Listar modelos:

```bash
docker exec -it ollama-server ollama list
```
