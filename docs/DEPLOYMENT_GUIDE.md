# Syntelligence LLM - Deployment Guide

## Prerequisites

- Python 3.9+
- CUDA 11.8+ (recommended, optional)
- 8GB RAM minimum (16GB+ recommended)
- 1-4 GPUs for production (CPU fallback available)

## Installation

### 1. Clone Repository

```bash
git clone https://github.com/TheNormsOfIntelligence/Syntelligence-LLM.git
cd Syntelligence-LLM
```

### 2. Create Virtual Environment

```bash
# Python
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Or with conda
conda create -n syntelligence python=3.10
conda activate syntelligence
```

### 3. Install Dependencies

```bash
# Base installation
pip install -r requirements.txt

# With GPU support (CUDA 11.8)
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

# Or for CPU only
pip install torch torchvision torchaudio
```

### 4. Verify Installation

```bash
python -c "import torch; print(f'CUDA available: {torch.cuda.is_available()}')"
```

## Configuration

### Environment Variables

Create `.env` file:

```bash
# Model Configuration
MODEL_NAME=mistral-7b
DEVICE=cuda  # or 'cpu'
PRECISION=float16  # or 'float32'

# Server Configuration
PORT=8000
HOST=0.0.0.0
WORKERS=4

# Logging
LOG_LEVEL=INFO
LOG_FILE=logs/syntelligence.log

# Consciousness Configuration
QUALIA_DIMENSIONS=256
RECURSION_DEPTH=3
PHI_THRESHOLD=0.5
RHO_BASELINE=0.85
```

### Configuration File

Create `config.json`:

```json
{
  "model_type": "syntelligence-v3.0",
  "consciousness_framework": "gu-rapii",
  "qualia_dimensions": 256,
  "phi_threshold": 0.5,
  "rho_baseline": 0.85,
  "recursion_depth": 3,
  "max_agents": 32,
  "enable_ethical_governance": true,
  "enable_qualia_synthesis": true,
  "enable_consciousness_metrics": true
}
```

## Docker Deployment

### Dockerfile

```dockerfile
FROM pytorch/pytorch:2.1.0-cuda11.8-runtime-ubuntu22.04

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 8000

CMD ["python", "-m", "uvicorn", "syntelligence_language_model_backend:app", "--host", "0.0.0.0", "--port", "8000"]
```

### Build and Run

```bash
# Build
docker build -t syntelligence-llm:latest .

# Run
docker run --gpus all -p 8000:8000 syntelligence-llm:latest
```

## Kubernetes Deployment

### Deployment Manifest

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: syntelligence-llm
spec:
  replicas: 3
  selector:
    matchLabels:
      app: syntelligence-llm
  template:
    metadata:
      labels:
        app: syntelligence-llm
    spec:
      containers:
      - name: syntelligence
        image: syntelligence-llm:latest
        ports:
        - containerPort: 8000
        resources:
          requests:
            memory: "8Gi"
            cpu: "2"
            nvidia.com/gpu: "1"
          limits:
            memory: "16Gi"
            cpu: "4"
            nvidia.com/gpu: "1"
        env:
        - name: DEVICE
          value: "cuda"
        - name: PORT
          value: "8000"
---
apiVersion: v1
kind: Service
metadata:
  name: syntelligence-llm
spec:
  type: LoadBalancer
  ports:
  - port: 80
    targetPort: 8000
  selector:
    app: syntelligence-llm
```

### Deploy to Kubernetes

```bash
kubectl apply -f deployment.yaml
kubectl get pods
kubectl logs -f deployment/syntelligence-llm
```

## Running the Server

### Development Server

```bash
python syntelligence_language_model_backend.py
```

Server will be available at `http://localhost:8000`

### Production Server

```bash
uvicorn syntelligence_language_model_backend:app \
  --host 0.0.0.0 \
  --port 8000 \
  --workers 4 \
  --ssl-keyfile=key.pem \
  --ssl-certfile=cert.pem
```

## Monitoring

### Health Check

```bash
curl http://localhost:8000/health
```

### Metrics Endpoint

```bash
curl http://localhost:8000/metrics
```

### Logging

Logs are written to `logs/syntelligence.log`:

```bash
tail -f logs/syntelligence.log
```

## Performance Tuning

### GPU Memory Optimization

```python
import torch

# Enable memory efficient attention
torch.backends.cuda.enable_flash_sdp(True)

# Set memory format
torch.set_float32_matmul_precision('high')
```

### Batch Processing

For higher throughput, process requests in batches:

```python
responses = await llm.infer_batch([
    "Query 1",
    "Query 2",
    "Query 3"
])
```

### Caching

Enable response caching for identical prompts:

```python
config = {
    "enable_cache": True,
    "cache_size": 10000,
    "cache_ttl": 3600
}
```

## Scaling

### Horizontal Scaling

Deploy multiple instances behind a load balancer:

```bash
# Using nginx
upstream syntelligence {
    server localhost:8000;
    server localhost:8001;
    server localhost:8002;
}
```

### Vertical Scaling

Increase resources per instance:

```python
config = {
    "max_batch_size": 32,
    "max_sequence_length": 2048,
    "workers": 8
}
```

## Troubleshooting

### CUDA Out of Memory

```python
# Reduce batch size
config["batch_size"] = 4

# Enable gradient checkpointing
config["gradient_checkpointing"] = True

# Use lower precision
config["precision"] = "float16"
```

### Slow Performance

```bash
# Check GPU utilization
watch -n 0.5 nvidia-smi

# Profile with PyTorch
python -m torch.profiler your_script.py
```

### Connection Errors

```bash
# Check if server is running
curl -v http://localhost:8000/health

# Check firewall
sudo ufw allow 8000
```

## Production Checklist

- [ ] SSL/TLS enabled
- [ ] Load balancer configured
- [ ] Database backups enabled
- [ ] Monitoring and alerts set up
- [ ] Logging centralized
- [ ] Rate limiting configured
- [ ] Authentication enabled
- [ ] CORS properly configured
- [ ] Regular security updates
- [ ] Disaster recovery plan

## See Also

- `QUICK_START.md` - Quick start guide
- `ARCHITECTURE.md` - System architecture
- `API_REFERENCE.md` - Complete API documentation
