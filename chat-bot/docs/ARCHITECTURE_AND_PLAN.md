# Master Architecture & Implementation Plan

This document consolidates the design decisions, workflows, and implementation strategy for the **Guessing Game Chatbot Agent**.

## 1. System Overview

The system is an Agentic RAG chatbot built with **Mastra Framework** and **MongoDB Vector Search**.

- **Core Feature**: "Guess the Word" game (Animal/Object).
- **Key Capability**: Dynamic "Learning Mode" to ingest new data via chat.
- **Persona**: Polite for game processing, but progressively rude (Toxic) for out-of-scope requests.

## 2. Architecture Workflows

### A. Vector Database Setup

_File: [flow_vector_db.mmd](./flow_vector_db.mmd)_

The foundation for the agent's knowledge.

- **Store**: MongoDB Atlas.
- **Indexing**: Vector Search Index.
- **Process**: Raw Data -> Chunking -> Embedding (Gemini/OpenAI) -> MongoDB.

### B. Agent Configuration & Persona

_File: [flow_agent_config.mmd](./flow_agent_config.mmd)_

The brain of the system.

- **Identity**: Guessing Game Expert.
- **Rules**:
  1.  Only discuss the Game or Weather (if enabled).
  2.  Strictly reject other topics (Politics, Coding code, etc.).
  3.  **3-Strike Rule**: Warning -> Annoyed -> Rude.

### C. Chatbot Interaction Logic

_File: [flow_chatbot_interaction.mmd](./flow_chatbot_interaction.mmd)_

The state machine for handling user messages.

1.  **Intent Analysis**: Check User Intent.
2.  **In-Scope**:
    - **Reset Strikes**: `strikes = 0`.
    - **RAG Loop**: Search -> Threshold Check (0.7) -> Ambiguity Check -> Clarify or Guess.
3.  **Learning Mode**: "Learn: [Content]" -> Ingest Data.
4.  **Out-of-Scope**:
    - **Increment Strikes**: `strikes++`.
    - **Response**:
      - Strike 1: Review scope (Polite).
      - Strike 2: Refusal (Annoyed).
      - Strike 3+: Rude/Toxic dismissal.

### D. Data Ingestion (Vectorization)

_File: [flow_vectorization.mmd](./flow_vectorization.mmd)_

How data enters the system.

- **Pipeline**:
  1.  Input (JSON/Text).
  2.  Mastra Embedding Tool.
  3.  `upsert()` to MongoDB.

## 3. Implementation Strategy

### Phase 1: Foundation

1.  **Dependencies**: Install `@mastra/mongodb` in `chat-bot/`.
2.  **Env Setup**: Configure `MONGO_URI` and API Keys.
3.  **Vectors**: Create `mongo-store.ts` and `seed-db.ts` script.

### Phase 2: Agent Mechanics

1.  **Tools**:
    - `vectorSearchTool`: For retrieving clues.
    - `ingestDataTool`: For learning mode.
2.  **Agent**:
    - Implement `systemPrompt` with Persona instructions.
    - Implement Strike Counter (Memory or Session State).

### Phase 3: Integration & Testing

1.  **Server**: Expose Agent via Mastra Server.
2.  **Test Scenarios**:
    - Valid Game: "4 legs" -> "Dog?".
    - Ambiguity: "4 legs" -> "Living?".
    - Training: "Learn Dragon" -> "Dragon".
    - Rude Mode: Spam "Code web" -> Get scolded.

## 4. Verification Checklist

- [ ] MongoDB Connection Successful.
- [ ] Vectors are stored and retrieved with scores.
- [ ] Agent correctly identifies "Out-of-scope".
- [ ] Agent becomes rude after 3rd strike.
- [ ] Agent resets rudeness after valid input.
