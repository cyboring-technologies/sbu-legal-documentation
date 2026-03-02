---
id: "UX_NARRATIVE_JOURNEY"
title: "UX Narrative: End-to-End Client Journey"
type: "UX, Branding & Visual Design"
version: "v1.0"
last_updated: "2026-03-01"
status: "Approved"
---

# UX Narrative: End-to-End Client Journey

**Context:** *This document narrates the chronological path of a client using the SBU-Legal platform. It focuses entirely on the perceptual experience, emotional tone, and mental model of the user, from clicking the initial CTA to the ultimate incineration of the session. It aligns strictly with the "One-Shot" invariant and Sovereign Engine architecture.*

STATUS: NORMATIVE
ROLE: Perceptual Guide and UX Walkthrough
SCOPE: E2E User Journey (Landing → Incineration)
RELATED TO: `UX_E2E_CONTRACT.md`, `BASE_EXECUTION_CONTRACT.md`, `ENGINE_VISUAL_CONTRACT.md`

---

## 1. The Decision (Landing Page)

The client arrives at the static marketing site. The environment feels institutional, clean, and serious (Institutional Greyscale palette). They are informed about the specific legal output they can obtain, but there is no "system" to log into, no dashboard to explore, and no account to create. 

They make a conscious decision to proceed and click the primary CTA (e.g., "Generar Documento").

**Mental Model:** *"I am requesting a specific, finite legal service."*

---

## 2. Mounting the Engine and The Blank Slate

Clicking the CTA transitions the client directly into the Sovereign Engine. The transition is absolute—the URL might change, but there is no "onboarding", no "Welcome back" message, and no navigation menu. The Engine simply *is*. It occupies the entire viewport, functioning as a completely distinct workspace.

The initial view is minimal. The client is prompted to select a **type of procedure** (e.g., "Contestar Demanda") and upload their foundational document (a PDF or DOCX). They click the primary "Cargar Documento" button to push their file into the Engine.

**Mental Model:** *"I am providing the raw materials for my case."*

---

## 3. Preparation and Strategic Context (Pre-Authority · HITL 1)

The Engine analyzes the uploaded file. The workspace expands into a two-panel view: a static visual preview of their uploaded document locked in the left column, and the active preparation area in the right column. 

Crucially, the client sees the **Strategic Context** box (HITL 1)—a substantive, 3-line input field. Here, they are invited to formally inject additional context, facts, or strategies that the system should know before generating the draft. 

Below this, a clear **Price** for the execution is displayed alongside a payment form. 

At this stage, everything is safe and reversible. The client can change the file, edit the strategy, or simply close the browser without any consequence or data retention. No legal draft exists yet.

**Mental Model:** *"I am setting the parameters. Nothing final has happened yet."*

---

## 4. Crossing the Rubicon (Payment Authorization)

The client completes their payment details and clicks the decisive, primary execution button—often styled with a firm "Autorizar y Ejecutar". 

This is the psychological "Rubicon."

Upon clicking:
1. A brief loading state indicates the Engine is locking the parameters and acquiring execution authority via the Gateway.
2. The payment goes through.
3. The Engine permanently crosses from a reversible sandbox into an irreversible execution state. 

**Mental Model:** *"I have authorized the act. It is now in motion and I cannot go back."*

---

## 5. The Irreversible Execution (Post-Authority)

The Engine immediately utilizes the consumed token to generate the legal draft based on the uploaded file and the Strategic Context. The result streams or appears decisively in the right-hand panel.

The client is now reviewing a generated legal artifact. The UI remains sober and focused. They cannot restart the Engine, they cannot process a different file, and they cannot change their original Strategic Context. They have one document in front of them: the result of their authorization.

**Mental Model:** *"This is the result I paid for."*

---

## 6. The Formal Amendment (HITL 2)

While the act is irreversible, the system logically accommodates one final correction event to ensure accuracy. 

At the bottom of the review panel, the client has the option to click "Refinar". This opens the **Refinement** input (HITL 2)—another substantive, 3-line input box explicitly identical in weight and appearance to the first one. 

The client types a specific instruction (e.g., "Adjust the damages claim to explicitly mention the loss of the vehicle"). They click Submit.

The moment the amendment is submitted, the UX physically enforces the One-Shot rule:
* The 3-line input instantly freezes, turning grey and non-editable. 
* It explicitly labels itself as "Enmienda Aplicada" (Amendment Applied).
* All refinement buttons completely disappear from the screen.

There is no "second try". There is no chat interface. The client sees exactly what they asked for locked permanently into the UI as an unchangeable historical record of their amendment. The Engine processes this one final instruction and updates the draft.

**Mental Model:** *"I have submitted my final correction. It is locked in."*

---

## 7. Approval, Download, and Total Incineration

Once the client is satisfied with the definitive draft (either the initial version or the one post-amendment), they click the green "Aprobar" (Approve) button.

Directly below the frozen amendment, the final CTA appears in green: **"Descargar y Cerrar"** (Download and Close). It warns them clearly that downloading will terminate the session.

The client clicks the button. 

1. Their browser receives the finalized `.docx` file.
2. In the exact same millisecond, the Engine violently incinerates the session. 
3. The workspace panels vanish entirely. 
4. A stark, red-bordered message appears indicating that the session has been closed, all data has been permanently destroyed, and the execution token is dead.

There is no "Thank you for using our service." There is no "Dashboard" to return to. The system has done its job, disposed of all evidence, and ceased to exist for that user.

**Mental Model:** *"I have my document. The system is gone. There is nothing left."*
