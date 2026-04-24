# Step 1 Worksheet: Signal Assessment

Before working with the agent, review each raw material file and assess its value as context for a TPM planning a software initiative for Mary's Place.

**Signal Rating definitions:**

- **high-signal** — Directly useful for understanding what to build, why, or for whom. Should be processed into structured context.
- **maybe** — Partially useful; may have relevant details buried in noise. Could be summarized or mined selectively.
- **noise** — Redundant, out of scope, or too raw to use meaningfully without significant processing.

---

## Assessment

### `raw-materials/01 Marys Place Organization.md`
- **Signal Rating:** maybe
- **Rationale:** This document contains useful and concise info for the general direction and goals of the company which could be helpful in prioritizing but isn't going to directly drive definition of backlog items or technical projects.
- **Action:** Create an overview of the organizational information that extracts key values and points that should be considered when prioritizing work throughout the project.

### `raw-materials/02 Marys Place Current Challenges.md`
- **Signal Rating:** high-signal
- **Rationale:** This document explicitly calls out technical opportunity areas to work on.
- **Action:** Extract the tech opportunities from the document and any challenges directly related to those opportunities that could be potentially solved by adding or specifying requirements

### `raw-materials/03 Intro Call with Marys Place.txt`
- **Signal Rating:** noise
- **Rationale:** This is a very wordy document with a lot of metadata and small talk adding a lot of noise to any actually useful information held within. There may be useful info in there, but it is messy and unstructured.
- **Action:** Pull out any details that seem relevant to the tech opportunities called out in document 2 for additional context, but otherwise leave this alone.

---

## Reflection Questions

After completing the table, consider the following before moving to Step 2:

1. Which file do you expect will require the most effort to process, and why?
> Document 3, the phone call. It has a ton of metadata and small talk and is unstructured and very long.
2. Are there any topics you'd want to know more about that none of these files seem to cover?
> What is the actual initiative we are planning? what are the top current objectives and capacity/skillsets available to work on the project?
3. How would you describe the "primary user" of the software being discussed — and how confident are you in that description based on what you've read?
> The two opportuntiies called out in the challenges document each have separate primary users, it isn't clear at this point what we are building.

> **Note:** There are no wrong answers here. The goal is to build the habit of *evaluating* your sources before asking an AI to synthesize them.

---

**Next:** Return to [README.md](../README.md) and continue with **Step 2: Context Ingestion**.
