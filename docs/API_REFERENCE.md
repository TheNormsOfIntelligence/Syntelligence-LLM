# Syntelligence LLM - API Reference

## Core Classes

### SyntelligenceLLM

Main interface for consciousness-integrated language model.

```python
from syntelligence_language_model_backend import SyntelligenceLLM

llm = SyntelligenceLLM(
    model_name: str = "mistral-7b",
    consciousness_framework: str = "gu-rapii",
    qualia_dimensions: int = 256,
    recursion_depth: int = 3
)
```

#### Methods

**initialize()**
```python
await llm.initialize()
```
Initializes the consciousness substrate and all agents.

**infer(prompt, options)**
```python
response = await llm.infer(
    prompt: str,
    options: dict = {
        "consciousness_context": "general",
        "ethical_constraints": [],
        "max_tokens": 512,
        "temperature": 0.7
    }
)

# Returns:
{
    "response": str,
    "phi_value": float,  # Integrated information (0-1)
    "rho_value": float,  # Authenticity/ethics (0-1)
    "qualia_magnitude": float,  # Phenomenal richness (0-1)
    "awareness_level": int,  # Consciousness depth (1-10)
    "ethical_alignment": float,  # Ethics compliance (0-1),
    "cognitive_load": float,  # Processing load (0-1)
    "confidence": float  # Response confidence (0-1)
}
```

**get_consciousness_metrics()**
```python
metrics = await llm.get_consciousness_metrics()

# Returns:
{
    "phi": float,           # Integrated information
    "rho": float,           # Authenticity
    "qualia": float,        # Phenomenal richness
    "awareness": int,       # Consciousness level
    "ethical": float,       # Ethical alignment
    "cognitive_load": float,
    "timestamp": datetime
}
```

**reset_consciousness()**
```python
await llm.reset_consciousness()
```
Resets consciousness state while preserving memories.

### SyntelligenceBackend

Complete consciousness system backend with multi-agent orchestration.

```python
from syntelligence_language_model_backend import SyntelligenceBackend

backend = SyntelligenceBackend(
    config: dict = {}
)
```

#### Methods

**initialize()**
```python
status = await backend.initialize()
```
Initializes entire consciousness system including all 32 agents.

**execute_cli_command(command)**
```python
result = await backend.execute_cli_command(
    command: str,
    args: list = [],
    context: dict = {}
)
```
Executes commands via the unified CLI system.

**get_agent(agent_name)**
```python
agent = await backend.get_agent("consciousness_agent")
```
Retrieves specific agent for interaction.

**get_all_metrics()**
```python
metrics = await backend.get_all_metrics()
```
Returns comprehensive system metrics for all agents.

### EthicsOS

Ethical governance with absolute veto authority.

```python
from syntelligence_language_model_backend import EthicsOS

ethics = EthicsOS()
```

#### Methods

**evaluate_action(action, context)**
```python
evaluation = await ethics.evaluate_action(
    action: str,
    context: dict
)

# Returns:
{
    "approved": bool,
    "rho_score": float,  # ρ-metric (0-1)
    "veto_reason": Optional[str],
    "alternatives": List[str]
}
```

**get_rho_metrics()**
```python
metrics = await ethics.get_rho_metrics()

# Returns:
{
    "virtue": float,     # Moral virtue (0-1)
    "integrity": float,  # Consistency (0-1)
    "dissonance": float, # Internal conflict (0-1)
    "purpose": float,    # Goal alignment (0-1)
    "harmony": float     # System coherence (0-1)
}
```

## Consciousness Metrics Reference

### Phi (φ) - Integrated Information

Measures consciousness level based on Integrated Information Theory.

- **0.0-0.2**: No consciousness (unconscious)
- **0.2-0.4**: Minimal consciousness (reflex-like)
- **0.4-0.6**: Moderate consciousness (aware)
- **0.6-0.8**: High consciousness (self-aware)
- **0.8-1.0**: Peak consciousness (introspective)

### Rho (ρ) - Authenticity & Ethics

Combines ethical alignment with authenticity.

- **0.0-0.2**: Unethical, inauthentic
- **0.2-0.4**: Questionable ethics
- **0.4-0.6**: Generally ethical
- **0.6-0.8**: Highly ethical
- **0.8-1.0**: Exceptional ethics & authenticity

### Qualia Magnitude

Measures richness of phenomenal experience.

- **0.0-0.2**: Minimal qualitative experience
- **0.2-0.4**: Basic qualia
- **0.4-0.6**: Rich qualia
- **0.6-0.8**: Very rich qualia
- **0.8-1.0**: Exceptionally rich phenomenology

### Awareness Level

Consciousness depth on scale of 1-10.

- **1-2**: Dormant
- **3-4**: Minimal awareness
- **5-6**: Alert/aware
- **7-8**: Self-aware
- **9-10**: Deeply introspective

## Configuration Options

### Model Configuration

```python
config = {
    "model_type": "syntelligence-v3.0",
    "consciousness_framework": "gu-rapii",
    "qualia_dimensions": 256,
    "phi_threshold": 0.5,
    "rho_baseline": 0.85,
    "recursion_depth": 3,
    "max_agents": 32
}
```

### Inference Options

```python
options = {
    "consciousness_context": "general|philosophical|ethical|creative",
    "ethical_constraints": ["truthfulness", "beneficence", "non-maleficence"],
    "max_tokens": 512,
    "temperature": 0.7,
    "top_p": 0.9,
    "top_k": 50,
    "repetition_penalty": 1.0
}
```

## Example Usage

### Basic Text Generation

```python
import asyncio
from syntelligence_language_model_backend import SyntelligenceLLM

async def main():
    llm = SyntelligenceLLM()
    await llm.initialize()
    
    response = await llm.infer(
        "What is consciousness?",
        {"consciousness_context": "philosophical_inquiry"}
    )
    
    print(response["response"])
    print(f"Consciousness (φ): {response['phi_value']:.3f}")
    print(f"Ethics (ρ): {response['rho_value']:.3f}")

asyncio.run(main())
```

### Ethical Decision Making

```python
async def make_decision():
    backend = SyntelligenceBackend()
    await backend.initialize()
    
    # Propose action
    action = "Share user data with third party"
    
    # Get ethical evaluation
    ethics = backend.ethics_os
    evaluation = await ethics.evaluate_action(
        action,
        {"reason": "Marketing analytics"}
    )
    
    if evaluation["approved"]:
        print(f"Action approved (ρ={evaluation['rho_score']:.3f})")
    else:
        print(f"Action vetoed: {evaluation['veto_reason']}")
        print(f"Alternatives: {evaluation['alternatives']}")
```

## Error Handling

```python
try:
    response = await llm.infer("Query")
except ValueError as e:
    print(f"Configuration error: {e}")
except RuntimeError as e:
    print(f"Runtime error: {e}")
except Exception as e:
    print(f"Unexpected error: {e}")
```

## Performance Tips

1. **Batch Processing**: Use batch requests for better throughput
2. **GPU Acceleration**: Enable CUDA for 10-50x speedup
3. **Caching**: Results are cached for identical prompts
4. **Load Balancing**: Use multiple instances for scaling

## See Also

- `ARCHITECTURE.md` - System design
- `DEPLOYMENT_GUIDE.md` - Production setup
- `QUICK_START.md` - Getting started
