# AI Prompt Log

One entry for every AI interaction that contributed to what you submit.
If you used no AI in a lab, write "No AI used." under that lab's heading.

Copy this block for each entry:

```
### YYYY-MM-DD — <tool>
**Goal:** what you wanted
**Prompt:**
> your prompt, verbatim
**Kept / changed / rejected, and why:**
```

---

## Lab 1

### 2026-11-05 — Claude — Urbee

**Goal:** Turn our handwritten stakeholder-session notes into the decision-log table and map each decision to our open questions.

**Prompt:**
> these are the answers we got from proff from the stakeholders session, [our notes]

Follow-up prompts in the same session, while Jan was still in the room:
> 1. before arrival 2. its 14 days before the guests arrival date […] 16. from the check out 17. same like before 2 or 3 years
>
> 1. 1s 2. last stay 3. yes
>
> rearrange the numbers according to our open question file like q1, answer, q2 ans, q3 ans, ........then at last put the other teams question answers

**Kept / changed / rejected, and why:** Kept the table after checking every row against our notes. Claude pointed out unclear decisions (cancellation deadline, room changes, data retention, search time); we asked Jan about them in the session and added his answers.

### 2026-11-10 — Claude — Urbee

**Goal:** Plan the Lab 1 report and draft requirements.md (functional and non-functional requirements, traceability matrix) and the reference app analysis.

**Prompt:**
> lets do the lab report now
>
> The way you have answered looks really complicated to me. Can you tell me and explain me everything in step by step? […]
>
> now can u do the lab report

**Kept / changed / rejected, and why:** Kept the structure and the requirements after checking each one against our use cases and the decision log. Kept the open points instead of inventing targets where Jan gave no number.

### 2026-11-11 — Claude — Urbee

**Goal:** Update our use cases with the stakeholder decisions and align requirements.md with them.

**Prompt:**
> [pasted our use-cases.md, PROMPTS.md and a screenshot of our use case diagram]

**Kept / changed / rejected, and why:** Kept the updated flows after checking them against the decision log. Replaced UC-03 "Accept or decline a booking request" with "Change a booking", because D-06 removed owner approval.

### 2026-11-11 — Claude — Urbee

**Goal:** Understand how the report was built, so that I can explain it and do it myself in the next labs.

**Prompt:**
> Can you just make me understand and help me to understand what actually happened in the lab report and from where we are making the lab report? I just need to know how you did it so that I can understand. […]
>
> do you think will it be easy for me to understand the lab before the lab session […]? Can I explain it to the professor?

**Kept / changed / rejected, and why:** Used Claude's explanation (emails → open questions → Jan's decisions → use cases → requirements with acceptance criteria → traceability → reference app check) to understand the method. Nothing from this went into the files directly.

### 2026-11-11 — Claude — Urbee

**Goal:** Run the reference app and collect screenshots as evidence for the analysis.

**Prompt:**
> could you please guide me for running the app and add the screenshots, because I want to add this […]

**Kept / changed / rejected, and why:** Set up Java 21 and ran the app myself in IntelliJ and took all six screenshots myself. Claude wrote the picture captions in reference-app-lab1.md, which I checked against what I saw in the app.

### 2026-11-11 — Claude — Urbee

**Goal:** Remove the obsolete use case from our use case diagram.

**Prompt:**
> How can I fix the image and from where I will get the correct image if I want to update the image actually?

**Kept / changed / rejected, and why:** Claude removed the bubble "A/D a booking request" and its line from our existing diagram image, because D-06 dropped owner approval. Everything else in the diagram is unchanged; I checked the new image before uploading it.
## Lab 2

## Lab 3

## Lab 4
