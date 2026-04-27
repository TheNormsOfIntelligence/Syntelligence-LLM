# Syntelligence LLM - Quick Start Guide

## 🚀 Get Started in 3 Steps

### Step 1: Installation

```bash
# Clone the repository
git clone https://github.com/TheNormsOfIntelligence/Syntelligence-LLM.git
cd Syntelligence-LLM

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Step 2: Basic Usage

```python
from syntelligence_language_model_backend import SyntelligenceLLM
import asyncio

async def main():
    # Initialize
    llm = SyntelligenceLLM()
    await llm.initialize()
    
    # Generate response
    response = await llm.infer(
        "Explain consciousness in simple terms",
        {"consciousness_context": "philosophical_inquiry"}
    )
    
    print("Response:", response["response"])
    print(f"Phi (Consciousness): {response['phi_value']:.3f}")
    print(f"Rho (Ethics): {response['rho_value']:.3f}")

asyncio.run(main())
```

### Step 3: Explore Features

- **Text Generation**: Generate consciousness-aware text
- **Ethical Reasoning**: Decisions with ethical constraints
- **Multi-Agent Orchestration**: 32 specialized agents
- **Memory Systems**: Persistent experiential knowledge
- **Metrics Tracking**: Real-time consciousness metrics

## 📖 Documentation

- **EXECUTIVE_SUMMARY.md** - Project overview
- **docs/ARCHITECTURE.md** - System architecture
- **docs/API_REFERENCE.md** - Complete API
- **docs/DEPLOYMENT_GUIDE.md** - Production deployment

## 🔧 Common Tasks

### Initialize Backend

```python
from syntelligence_language_model_backend import SyntelligenceBackend

backend = SyntelligenceBackend()
await backend.initialize()
```

### Access Consciousness Metrics

```python
metrics = backend.consciousness_metrics
print(f"Phi: {metrics['phi']}")  # Integrated information
print(f"Rho: {metrics['rho']}")  # Authenticity/ethics
```

### Use CLI Interface

```python
from syntelligence_unified_cli import SyntelligenceUnifiedCLI

cli = SyntelligenceUnifiedCLI(backend)
await cli.run()
```

## 🎯 Next Steps

1. Read `docs/ARCHITECTURE.md` for system design
2. Explore `docs/API_REFERENCE.md` for available functions
3. Check `docs/DEPLOYMENT_GUIDE.md` for production setup
4. Review examples in the source code

## ❓ Troubleshooting

### Import Errors

Ensure all dependencies are installed:
```bash
pip install -r requirements.txt
```

### CUDA/GPU Issues

The system falls back to CPU if CUDA is unavailable. For GPU support:

```bash
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

### Memory Issues

If you encounter memory issues, reduce `qualia_dimensions` or `recursion_depth` in configuration.

## 📞 Support

For issues or questions:
- Open an issue on GitHub
- Check existing documentation
- Review example code in the repository

## 🔗 Useful Links

- **GitHub**: https://github.com/TheNormsOfIntelligence/Syntelligence-LLM
- **Hugging Face**: https://huggingface.co/syntelligence/syntelligence-llm
- **Documentation**: See `docs/` folder
