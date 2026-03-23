# Stateful Conversation Engine
Stateful engine for multi-turn LLM interactions with extractors, memory, prompt routing, and recovery.

<img width="3528" height="1978" alt="SCE scheme" src="https://github.com/user-attachments/assets/9f76a388-5d71-490a-b794-51c6b54b983a" />

## Overview
Designed and built a stateful engine for multi-turn LLM interactions. 
The system combines structured extractors, a state computation layer, persistent memory, and runtime prompt orchestration to keep long interactions coherent, adaptive, and resilient. 
Built with n8n, PostgreSQL, Telegram, and LLM APIs, including retry/fallback logic, refusal handling, and observability for production-oriented operation. 

## Architecture 

### 1. Ingress layer & turn creation 
This layer handles UX control and message admission while registering each dialogue turn as a distinct iteration in the runtime loop. It performs validation, deduplication, and creates turn n as part of the system’s sequential state. 

### 2. Scene control layer
The system uses a set of structured extractors for adaptive LLM control:
- contextual coherence and scene stability
- user intent and interaction dynamics within the current context
- persistent scene-memory deltas for cross-turn continuity

### 3. Extraction normalization layer
At this stage, extractor outputs are normalized, JSON payloads are sanitized, and raw model outputs are converted into typed runtime signals for downstream logic. 

### 4. State engine 
The core of the system is a state computation layer that determines the model’s allowed behavior in the current context. Normalized extractor signals are scored and used to compute internal interaction states. The control model is inspired by ideas from signal processing and control systems: interaction is treated as a sequence of signals over time, the size of the next step is bounded by context quality, and smooth stable transitions are achieved using EMA, inertia/friction, and hysteresis.

### 5. Prompt Orchestration 
Based on the computed state, the system dynamically assembles a runtime prompt stack and passes context-appropriate behavioral instructions to the LLM. 

### 6. Generation + Recovery
This layer handles primary LLM response generation and recovery when generation becomes unreliable. It detects refusals, provider-side safety filtering, and multilingual generation artifacts, then routes the interaction through retry or fallback paths when needed.

### 7. Post-Processing layer
After generation, the system validates the output, removes model artifacts, and formats the response for final delivery. This keeps the final message clean, stable, and aligned with the runtime’s behavioral constraints.

### 8. Memory & Observability
This layer updates scene memory, persists runtime traces, and logs model outputs and system behavior for debugging and analysis. It stores scene-memory deltas such as new facts, meaningful changes, and other information that should persist across turns.
