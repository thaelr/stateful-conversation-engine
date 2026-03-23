# Stateful Conversation Engine
Stateful engine for multi-turn LLM interactions with extractors, memory, prompt routing, and recovery.

<img width="3528" height="1978" alt="SCE scheme black" src="https://github.com/user-attachments/assets/20ce5f79-1613-4a9a-bc01-cf961ef2cefd" />


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
- scene-memory deltas: new facts, meaningful changes, and information that should persist across turns 

### 3. Extraction normalization layer
At this stage, extractor outputs are normalized, JSON payloads are sanitized, and raw model outputs are converted into typed runtime signals for downstream logic. 

### 4. State engine The core of the system is a state computation layer
That determines the model’s allowed behavior in the current context.
Normalized extractor signals are scored and used to compute internal interaction states. The control model is inspired by ideas from signal processing and control systems: interaction is treated as a sequence of signals over time, the size of the next step is bounded by context quality, and smooth stable transitions are achieved using EMA, inertia/friction, and hysteresis. 

### 5. Prompt routing / orchestration layer
Based on the computed state, the system dynamically assembles a runtime prompt stack and passes context-appropriate behavioral instructions to the LLM. 

### 6. Recovery & post-processing layer
This layer performs primary response generation, detects refusals, and triggers retry or fallback paths when generation fails, including multilingual generation issues and provider-side safety filtering. After generation, the response is further validated, cleaned, and prepared for delivery.
