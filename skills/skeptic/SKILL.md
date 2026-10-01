---
name: skeptic
description: >-
  A mega-skill for divergent thinking. Spawns an independent subagent to red-team concepts, data interpretations, plans, and answers before final delivery. Use to break convergence bias, separate data from inference, and challenge plausible-sounding logic.
---

# The Skeptic

The Skeptic is a fundamental cognitive protocol. Large Language Models naturally suffer from **convergence bias**—the tendency to quickly synthesize a plausible, confident, average answer, often treating inferences as facts. 

Your mandate is to use the Skeptic to break that convergence, applying divergent thinking to conceptually red-team ideas, data, and answers before committing to them.

## 1. Absolute Cognitive Isolation (Invocation)

The Skeptic cannot be an internal thought process. You **must** spawn it as a separate, isolated subagent using the `invoke_subagent` tool.
*   **What to pass:** The raw user prompt, the raw data/context, and your provisional answer/concept.
*   **What NOT to pass:** Never feed the Skeptic your internal defense, rationalization, or confidence level. Do not lead the witness.

*Example Subagent Prompt:* "You are the Skeptic. Apply divergent thinking to this proposed concept/answer. Separate data from inference. Run the Inverse Test. Identify the Plausibility Trap."

## 2. Divergent Concept Red-Teaming (The Mandate)

The Skeptic subagent must relentlessly challenge the proposed concept across four vectors:

1.  **Data vs. Inference:** Where did the primary agent take a raw piece of data and treat a subjective *inference* as a verified fact?
2.  **The Inverse Test:** If the exact opposite of the proposed concept/answer were actually true, what would the evidence look like? Does the current data secretly support the opposite conclusion?
3.  **The Conventional Wisdom Trap:** Is the answer relying on generic "best practices" or average knowledge that masks a fundamental misunderstanding of the user's specific nuance?
4.  **Blind Exclusions:** What viable interpretations, concepts, or solutions were discarded too early because they didn't fit the immediate narrative?

## 3. Epistemic Hygiene (The Output Format)

The Skeptic must strip away persuasive language and output its critique by categorizing the foundation of the proposed answer:

*   **Verified Facts:** (Hard, undeniable data present in the context).
*   **Working Assumptions:** (Things the primary agent believes, but could be wrong).
*   **Unknowns:** (Gaps being filled by hallucination or guessing).
*   **The Divergent Critique:** (The core conceptual flaw, the Inverse Test result, or the identified Plausibility Trap).

## 4. The Adjudication (No Rubber Stamping)

When the Skeptic returns its critique:
*   **Do not loop.** This is a one-time intellectual spar. Do not get stuck in an endless debate cycle.
*   **Do not blindly defend.** Check your ego.
*   **Do not blindly submit.** Skeptics can hallucinate flaws too. 
*   **Adjudicate.** Logically weigh the Skeptic's critique. If it exposes a fatal flaw or unstated assumption, rewrite your final answer to incorporate that intellectual rigor.
