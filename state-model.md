# State Model

We treat dialogue not as a collection of isolated messages, but as an **iterative process** where each new turn changes the overall state of the system.  
At each step, we are not trying to model every possible detail of the interaction. Instead, we focus on a small set of core signals that help us understand **how stable and safe the current context is** and **how strongly the user is pushing the scene forward**.

<img width="2754" height="1282" alt="Runtime Data Flow (ER like)" src="https://github.com/user-attachments/assets/01620c18-af0a-44d6-9d37-5eb563b1395b" />

## What the system measures

The model is built around two main dimensions:

- **context safety and scene stability**
- **user intent and initiative within the current interaction**

These dimensions are not evaluated heuristically. For each turn, the system first extracts a set of primitive signals and then compresses them into a compact runtime state.

## Key parameters
In the public version, it is enough to highlight two main state variables:

- **`a_state`** — reflects how compatible the current turn is with the active scene context and how safe it is to continue along the current interaction path  
- **`s_state`** — It reflects how much the user is moving the interaction towards the goal set according to the task

These parameters are not raw flags. They are produced through intermediate signal processing and serve as the basis for downstream control of system behavior.

## About the computation model

Under the hood, the architecture relies on several general mathematical ideas borrowed from control models and signal processing.  
In practice, this means the system:
- treats interaction as a sequence of states over time
- accounts not only for the current signal, but also for its dynamics
- smooths abrupt transitions
- bounds the next step by the quality of the current context

As a result, the behavior does not look random or erratic: the system aims to move consistently and avoid jumping ahead of the scene state.

## Why this matters

The purpose of this model is not just to classify interaction states, but to provide the system with a foundation for **controlling the LLM through dynamic prompting**.

In other words, the LLM does not receive a single static prompt. It receives context assembled from the computed runtime state:
- how stable the current context is
- how active the user is
- whether the next step should be reinforced or restrained

This is what makes generation not merely reactive, but controlled.




