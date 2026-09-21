# AI Governance

Technical architectures and governance frameworks for responsible deployment of AI in regulated life sciences and pharmacovigilance — covering validation continuity, dynamic change control, and compliance observability in agentic AI systems.

!!! important "Important framing"
    These are my personal working frameworks — tools I use to think about and discuss complex challenges in AI deployment within regulated environments. They are not regulatory guidance, validated industry standards, or formal compliance frameworks. Where I describe what organisations "should" do, I mean it as my professional opinion, not as a mandate.

---

## Framework Library

### 7. Continuous Revalidation, Dynamic Change Control & Observability in Regulated Agentic AI™

**Operationalizing ISO/IEC 42001, EU AI Act, GDPR, and GAMP 5 for Multi-Agent Safety Systems**

`ISO/IEC 42001` · `EU AI Act` · `GDPR` · `GAMP 5`

---

#### 1. Executive Summary & Problem Statement

In regulated life sciences and pharmacovigilance operations (such as Individual Case Safety Report intake, clinical documentation, and CGT manufacturing), traditional computer systems validation assumes deterministic source code, compiled binaries, and frozen releases. In agentic Large Language Model (LLM) architectures, operational behavior is driven dynamically by non-code dependencies: prompt template modifications, chunking heuristics, Retrieval-Augmented Generation (RAG) vector index updates, and dynamic routing graphs.

When engineers tune system prompts or update vector knowledge stores with revised safety summaries or terminology dictionaries, conventional change-control protocols lack explicit criteria to determine whether the update constitutes routine maintenance or a **substantial modification** requiring formal software revalidation. Framework 7 establishes a risk-calibrated change management matrix, immutable audit state reconstruction, and human-in-the-loop observability telemetry.

---

#### 2. The Dynamic AI Change Classification Matrix

*EU AI Act Art. 3(43) & Art. 43; ISO/IEC 42001 Clause 8*

To prevent engineering gridlock while safeguarding regulatory compliance and patient safety, system adjustments are segregated across three structured risk tiers:

<div class="aig-table-wrapper">
<table class="aig-change-matrix">
  <thead>
    <tr>
      <th>Change Level</th>
      <th>Triggers &amp; Examples</th>
      <th>Regulatory Classification</th>
      <th>Required Validation Action</th>
    </tr>
  </thead>
  <tbody>
    <tr class="aig-tier-1">
      <td><span class="aig-tier-badge aig-tier-badge--1">Tier 1</span><br><strong>Minor / Operational</strong></td>
      <td>• Adjusting retrieval top-k chunk count<br>• Minor UI context layout changes<br>• Utility helper script patches</td>
      <td>Non-substantial modification within expected operational variance.</td>
      <td>Automated regression suite execution against a versioned baseline; automatic logging in AI Technical Documentation.</td>
    </tr>
    <tr class="aig-tier-2">
      <td><span class="aig-tier-badge aig-tier-badge--2">Tier 2</span><br><strong>Intermediate / Semantic Boundary</strong></td>
      <td>• Prompt instructions &amp; persona changes<br>• Updating chunking strategies / embedding models<br>• Refreshing reference datasets (MedDRA, SmPCs)<br>• Modifying retrieval similarity cutoffs</td>
      <td>Potential drift or decision boundary shift affecting extraction confidence and reasoning.</td>
      <td>Pre-release benchmark evaluation against a versioned ground-truth dataset; targeted regression verification; formal QA and regulatory sign-off.</td>
    </tr>
    <tr class="aig-tier-3">
      <td><span class="aig-tier-badge aig-tier-badge--3">Tier 3</span><br><strong>Substantial Modification</strong></td>
      <td>• Foundational model replacement (e.g., GPT-4 to a local weights model)<br>• Introducing new agent graph paths<br>• Shifting sign-off authority from human to AI</td>
      <td>Substantial Modification under EU AI Act (Art. 3(43) / Art. 43).</td>
      <td>Full formal revalidation (IQ/OQ/PQ); Annex IV Technical Documentation update; mandatory Data Protection Impact Assessment (GDPR Art. 35) re-execution.</td>
    </tr>
  </tbody>
</table>
</div>

---

#### 3. Multi-Agent Provenance & The Immutable "System State"

*EU AI Act Art. 11, 12 & Annex IV; AIGP Data Lineage & Provenance Standards*

In an agentic pipeline, capturing a single code release or application commit hash is insufficient to satisfy audit requirements. During a regulatory inspection, an organization must be capable of reconstructing the exact operating state of the system for any historical case or narrative generated.

Every transaction execution must bind and serialize an immutable cryptographic audit tuple:

```
Audit Tuple = ⟨ Prompt Hash, Model Version, Index Hash, Run Log ID ⟩
```

1. **Prompt & Workflow Configuration State:** Immutable Git commit hash of prompt templates, graph routing definitions, temperature, and top-p sampling hyperparameters.
2. **Foundational Model State:** Exact provider snapshot tag or cryptographic checksum of local model weights.
3. **Retrieval Index State:** Versioned snapshot identifier of the vector database, chunking policy, and ingested reference corpus active at the timestamp of execution.
4. **Agent Decision Boundaries:** Discrete serialization of intermediate steps (Intake Extraction → Terminology Mapping → Assessment Reasoning → Narrative Generation) ensuring each step's output is independently auditable.

---

#### 4. Closed-Loop Observability: Human Overrides as Governance Telemetry

*EU AI Act Art. 14; GDPR Art. 22; ISO/IEC 42001 Monitoring Controls*

Human-in-the-loop review must function as active oversight rather than passive rubber-stamping. Human interactions are treated as the primary signal for identifying systematic system degradation and coverage limitations:

- **Override Delta Tracking:** Capture structured differences between the agent's proposed draft and the human reviewer's final approved decision (e.g., corrections to MedDRA Preferred Terms, changes to suspect drug causality classifications, or modifications to adverse event seriousness criteria).

- **Coverage Gap Telemetry:** Clustered reviewer overrides occurring within specific therapeutic areas or product classes are classified as retrieval coverage gaps or distribution drift, automatically routing those edge cases back into engineering review rather than treating them merely as routine QC variance.

- **Champion vs. Challenger Deployments:** Prior to promoting a Tier 2 prompt or index modification into production, evaluate the update (Challenger) concurrently against the existing baseline (Champion) across shadow production traffic or curated historical test cohorts to verify that performance metrics meet or exceed validated acceptance criteria.

---

#### 5. Privacy, Data Minimization & Segregated Architecture

*GDPR Art. 5, Art. 9, Art. 25*

Because safety reports and manufacturing lots routinely contain unstructured personal and protected health information (PII/PHI), privacy controls are embedded directly into pipeline architecture:

- **Pre-Processing De-Identification:** Unstructured source data must pass through an initial validated de-identification stage to redact direct patient and reporter identifiers before the text is parsed by downstream reasoning, embedding, or indexing agents.

- **Zero Secondary Retention on Context Stores:** Operational vector databases containing regulatory knowledge bases and reference documentation are kept isolated from short-term case execution memory to prevent the persistent storage of sensitive health data (GDPR Art. 9) within general retrieval indexes.

---

Applying These Frameworks

These frameworks are conceptual starting points for discussion and exploration, not prescriptive playbooks. I am happy to discuss how they might be adapted to specific contexts.

[Get in Touch →](../contact/)
