---
id: "METADATA_EXTRACTION_ARCHITECTURE_V2"
title: "Metadata Extraction Architecture"
type: "Core Architecture & Systems"
version: "v2.0"
last_updated: "2026-02-19"
status: "Approved"
---

# Metadata Extraction Architecture

**Context:** *Describes the system for extracting structural data from uploaded documents. It emphasizes that this process is deterministic, uses regex/low-cost LLMs, and strictly avoids legal judgment.*

## 1. Architectural Position
**Principles of Sovereignty and Minimal Complexity**

The Engine V2 Metadata Architecture is built upon a single, sovereign decision: **The Engine does not replace legal judgment.**

*   **Human Sovereignty**: Strategic intelligence, legal reasoning, and contextual analysis reside exclusively with the user (the Attorney). The Engine does not attempt to deduce, infer, or guess legal strategy.
*   **Structural Focus**: The Engine serves purely as a structural accelerator. It extracts objective, non-interpretative data (Dates, Amounts, Jurisprudence citations) to facilitate drafting, but it never blocks or gates operation based on the *content* of that data.
*   **Minimal Complexity**: To guarantee the **One-Shot** invariant and minimize the failure surface, the system rejects all recursive logic, conditional dependencies, and cross-validation performance.
*   **Finality**: This architecture is intentional and final. It is not a transitional state; it is the permanent operational mode of Engine V2.

## 2. Scope
This document defines the **Single Source of Truth** for the Metadata Extraction and Validation System.

*   **Scope**: Strictly limited to **Structural Metadata**.
*   **Exclusions**: There is NO strategic metadata. There is NO contextual metadata. There is NO conditional logic. There are NO dependencies between Draft Types and Metadata.
*   **Input**: Raw text from the uploaded document.
*   **Output**: An immutable, validated JSON object containing only structural arrays.

## 3. Location in the Engine Flow
Metadata processing is orchestrated by the **Execution Coordinator** (Durable Object) and strictly follows this linear path:

1.  **Extraction**: `POST /extract` (Regex-based parsing)
2.  **Storage**: `POST /store_extraction` (Volatile DRAM/DO storage)
3.  **Validation**: `POST /review_metadata` (Human-in-the-Loop review)
4.  **Freeze**: `POST /acquire_authority` (Cryptographic hashing)
5.  **Consumption**: `POST /generate` (Prompt injection)

## 4. Metadata Model (Structural-Only)
The system recognizes and processes **only** the following fields. No other fields are permitted, processed, or stored.

| Field | Type | Source | Classification | Frozen at Authority | Used in Prompt |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **`structural.dates`** | `Array` | Deterministic (Regex) | **Structural** | **Yes** | **Yes** |
| **`structural.amounts`** | `Array` | Deterministic (Regex) | **Structural** | **Yes** | **Yes** |
| **`structural.jurisprudence`** | `Array` | Deterministic (Regex) | **Structural** | **Yes** | **Yes** |

**Strict Constraints:**
*   **Structure**: The root object must contain a `structural` key.
*   **Types**: All values must be Arrays.
*   **Content**: The system validates the *format* (Array), not the *truth* of the content.
*   **Vacancy**: Empty arrays (`[]`) are valid. The system does not require data presence to proceed.

## 5. Extraction Pipeline
The pipeline is fully deterministic and stateless.

1.  **Ingestion**: Server logic receives raw text.
2.  **Parsing**: Specific Regex patterns identify potential dates, monetary amounts, and case law citations.
3.  **Sanitization**: The system discards all data that does not fit into the three structural categories.
4.  **Output**: A clean JSON object `{ structural: { dates: [], amounts: [], jurisprudence: [] } }`.

## 6. Logic and Dependencies
**There is no logic engine.**

*   **No Draft Type Dependency**: The selected Draft Type (e.g., "Answer/Oppose") has **zero impact** on metadata requirements.
*   **No Cross-Validation**: The presence of "Dates" does not mandate the presence of "Amounts".
*   **No Conditional Gating**: The system never blocks progress based on the absence or content of specific metadata fields.
*   **No Semantic Analysis**: The Engine does not "read" the metadata to determine case strategy.

## 7. Freeze and Snapshot
To satisfy the **Liability Defense** invariant, all metadata is cryptographically frozen before use.

*   **Trigger**: The `POST /acquire_authority` endpoint.
*   **Mechanism**: SHA-256 Hash of the JSON stringified metadata object.
*   **Immutability**: Once the Authority Token is issued, the metadata object in memory is **read-only**. Any attempt to modify it via API results in rejection.
*   **Cryptographic Fingerprint**: The generated SHA-256 hash is a one-way function. It creates a unique, non-reconstructable identifier for the metadata state.
*   **Privacy Preservation**: The hash does not permit reconstruction of the original data, ensuring that the "Total Incineration" invariant is not violated even if the hash persists in audit trails.

## 8. Integration with Prompt System
The frozen metadata is passed to the LLM via the Prompt Assembly Layer.

*   **Role**: "Trusted Context".
*   **Format**: JSON.
*   **Instruction**: The LLM is instructed to use these structural elements (if present) to populate specific placeholders in the template, treating them as verified facts provided by the human user.

## 9. System Invariants
The Metadata System strictly adheres to the Global SBU-Legal Invariants:

1.  **One-Shot**: The metadata lifecycle is bound to a single session. Re-initialization annihilates all existing metadata.
2.  **Total Incineration**: Upon session close (time-out, completion, or explicit termination), the metadata is securely deleted from memory.
3.  **No Persistence**: Metadata is never written to disk, databases, or logs (except for the anonymized SHA-256 hash).
4.  **Determinism**: The same input text always yields the same initial extraction.
5.  **Technical Neutrality**: The system uses standard JSON and HTTP/REST patterns, avoiding proprietary logic traps.

## 10. Operational Closing
This architecture definition is final and binding for Engine V2.

1.  **Irreversibility**: All operations are strictly bounded by the One-Shot lifecycle.
2.  **No Legal Judgment**: The Engine performs structural extraction only; it does not interpret, advise, or strategize.
3.  **Attorney Sovereignty**: The user retains exclusive control and liability for the legal content. The Machine is a stateless instrument.
