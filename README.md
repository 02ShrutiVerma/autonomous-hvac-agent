# autonomous-hvac-agent
Autonomous HVAC Diagnostic Agent using LangChain, rule logic, memory, and simulated feedback loop.

A LangChain-powered LLM agent that diagnoses HVAC systems, proposes rule updates, stores memory using FAISS, triggers simulated actuator responses, and logs feedback accuracy. Built to demonstrate adaptive, autonomous systems aligned with real-world facility management challenges.


## Project Overview

This project simulates an autonomous AI system for HVAC maintenance. It uses a combination of:
- Symbolic rules (defined in `rules.json`)
- GPT-based audit with LangChain
- Simulated control actions
- Memory via FAISS vector store
- Performance logging against labeled data


## Architecture

             ┌───────────────┐
             │ Sensor CSV    │
             └──────┬────────┘
                    ▼
        ┌────────────────────────┐
        │ Rule-Based Diagnosis   │ ◄── thresholds from rules.json
        └────────────┬───────────┘
                    ▼
        ┌────────────────────────┐
        │ GPT Diagnosis (LLMChain)│
        └────────────┬───────────┘
             ▼        ▼
        (AGREE?)   (DISAGREE?)
             │            ┌────────────────────────────┐
             │            │ Suggest Rule Update (JSON) │
             │            └──────┬─────────────────────┘
             ▼                  ▼
     Simulate Action   ┌────────────────────────┐
                       │ Update rules.json Live │
                       └────────────────────────┘

All steps log to: diagnostic_log.csv
Memory stored in: faiss_memory/

## Core Features

- Dynamic symbolic rule diagnosis from `rules.json`
- LLM-based diagnostic auditing using LangChain
- Automated rule revision proposals
- Actuator tool simulation (fan ON, alert, etc.)
- Vector memory storage using FAISS
- Ground truth comparison and performance logging


## Sample Log Output (diagnostic_log.csv)

| Timestamp       | Rule Diagnosis | GPT Diagnosis | GT Label | Correct | Confidence | Action     | Rule Suggestion       |
|----------------|----------------|---------------|----------|---------|------------|------------|------------------------|
| 2025-07-20     | Fault          | No Fault      | Fault    | False   | Medium     | Alert ON   | temp_threshold: 29     |

---

## Future Enhancements

- Confidence-based rule weighting
- Real-time control system integration
- Multi-agent cooperative planners
- Persistent memory via SQLite or Redis
