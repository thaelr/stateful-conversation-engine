# Stateful Conversation Engine

A stateful orchestration layer for long-session AI-avatar products and businesses where dialogue is part of monetization.

The engine keeps multi-turn conversations coherent, adapts behavior from runtime state, recovers from unstable generations, and connects dialogue progress to product actions such as memory, media, reminders, and monetization flows.

<img width="1429" height="440" alt="flow-diagram" src="https://github.com/user-attachments/assets/a7202aec-2136-4651-a495-116205424504" />


## Beta Snapshot

- 289 beta users, 359 sessions, 5,198 dialogue turns — cold, unoptimized traffic from mature-themed roleplay communities
- One in five sessions passed 30 messages with sustained engagement carrying some users past 100
- 87.7% of turns were dynamically steered by runtime state
- Median recovery after a broken/derailed turn: 12 more turns of stable dialogue

[Read the full beta results](./BETA_RESULTS.md)

## What It Solves

Large model providers ship an API, not a memory and instruction architecture around it — businesses have to build that layer themselves to put AI at the core of a product.

Most products on the market are either narrow in scope or don't hold up over long interactions: they lose coherence, forget facts, and degrade past roughly 30 turns.

This engine adds a control layer around the model: it captures the user's message, extracts runtime signals, checks state, assembles behavior instructions, generates a reply, validates it, and updates persistent memory — every turn.

## System Overview

- **Smart message capture** — normalizes the incoming message and checks whether the user's intent is fully captured before moving on
- **Signal extraction** — reads user intent, context stability, and scene dynamics from the current turn
- **Memory layer** — reads and writes persistent state (facts, scene progress, continuity) via a dedicated state store
- **Dynamic instructions** — turns the current state into concrete behavioral guidance for the model, rather than a single static prompt
- **AI Writer** — generates the reply under those instructions
- **Validation & recovery** — checks output quality; invalid generations are retried or routed to a fallback instead of shipping a broken reply
- **State update** — on a valid reply, memory and runtime state are updated before the next turn

## Implementation Note

This repository documents the system at a product and architecture level. Production workflows, prompts, routing rules, and internal heuristics are proprietary.

The model writes. The engine controls.

---

A closer look at how the engine models a conversation → [state-model.md](./state-model.md)

