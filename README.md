# Ephemeral Initialization Vectors (EIV) and Relational Merkle Closures

**Proof that something existed — even after it is gone.**

This repository publishes two foundational primitives designed for systems that must eliminate sensitive data while still preserving cryptographic proof that it once existed and was properly linked within a larger structure.

- **Ephemeral Initialization Vectors (EIV):**  
  A method of generating non-reproducible cryptographic states that cannot be reconstructed once destroyed — but can still be proven to have existed.

- **Relational Merkle Closures:**  
  A cryptographic structure that preserves not only object-level integrity (like traditional Merkle trees), but also the *relationships* between objects — even when some of them must be removed.

These are released publicly under the MIT License. Anyone is free to extend or commercialize - just don't forget to give acknowledgement IAW MIT license.
---

## 1. What This Solves

Most systems face two conflicting realities:

| Requirement | Direct Conflict |
|-------------|------------------|
| You must be able to **delete** or irreversibly destroy data or keys. | You must also **prove** the data existed and was processed correctly. |
| Privacy laws demand **erasure**. | Audit laws demand **retention of evidence**. |
| Keys and data are supposed to *vanish*. | But third parties may demand proof they were once valid. |

**EIV + Relational Merkle Closure solve this exact tension.**  
They allow a system to say, truthfully and provably:  
> “The data/key used to exist. It is now gone. Here is mathematical proof linking both states.”

---

## 2. What This System *Does*

✔ Enables **irreversible destruction** of cryptographic material or data references.  
✔ Preserves **verifiable proof of prior existence** without retaining the data itself.  
✔ Maintains **structural integrity** across related records using relational Merkle commitments.  
✔ Creates a **publicly verifiable trail** without requiring trust in the operator.  
✔ Functions as a **base layer**; policy and governance can be built on top if desired.

---

## 3. What This System *Does Not* Do

This project **deliberately** does *not* attempt to handle:

✖ Legal or ethical arguments for *whether* something should be deleted.  
✖ Multi-party approval, threshold witnesses, or regulator-managed key shares.  
✖ Sealed receipts, dual-track proofs, or compliance workflows.  
✖ Preventing human collusion, insider abuse, or misuse by legitimate authorities.  
✖ Enforcing law, fairness, or moral correctness cryptographically.

These are social, legal, or organizational problems — not cryptographic ones.

---

## 4. **On Witnesses, Regulators, and Governance — Why This Is Left Open**

Many systems attempt to embed governance directly into cryptography: multi-signature deletion approvals, regulator-held key shares, sealed audit receipts, etc.

This project intentionally **does not go down that road.**

**Why?**

- Governance is a *human* function. Cryptography can **prove** what happened, but it cannot **decide** what should happen.
- Threshold-witness systems add latency, cost, and operational fragility (people go offline, committees stall, keys get lost).
- Even in perfect threshold systems, collusion remains possible — and when it happens, the cryptography only proves the crime was “authorized.”
- Open-source primitives should remain flexible. People who need governance controls can layer them on. People who don’t shouldn't drag them along.

**So instead of prescribing a governance model, this project provides:**

- A minimal, verifiable substrate for *irreversible state transition*.  
- A structure where anyone (regulator, auditor, or adversary) can detect tampering, even if data is gone.  
- A foundation that others are free to extend with N-of-M approvals, time delays, sealed receipts, or jurisdiction-specific laws if they choose.

---

## 5. High-Level Model (No Diagrams — Concept Only)

1. A state or asset is created.  
2. Its cryptographic commitment is stored in a relational Merkle structure.  
3. When that state must be destroyed, its EIV and key material are erased.  
4. The system records a cryptographic proof that the state existed and was linked to others — but retains no recoverable data.  
5. The Merkle structure remains valid before and after destruction — proving integrity across time.

---

## 6. Minimal Usage Concept (Pseudocode Style, Not Executable)

```python
# Step 1: Create object with Ephemeral Initialization Vector
state = create_state(data)
commit = merkle_commit(state)

# Step 2: Persist commit to relational Merkle structure
merkle_tree.add(commit)

# Step 3: Destroy state (key + data)
destroy(state)

# Step 4: Record irreversible destruction event
event = hash(commit + timestamp + "destroyed")
merkle_tree.add(event)

7. License

MIT License.
No warranty, no restriction. Fork it, break it, commercialize it, ignore it.

8. Contribution Philosophy

You don’t need permission to extend this.
If you want to add witnesses, regulators, zk-proofs, smart contracts, or court-order decryption — go ahead.

If you do something interesting with it, attribution under MIT license is required.

9. Final Note

This project solves the irreversible proof problem, not the governance problem.
That is intentional.

Those who see the gap will know how to fill it.
- - - -
  
If you found any of this useful, help me keep my farm animals safe with a new fence.  Yes, I really have a small farm. 
Duck Trails Farm in MS.  We raise Meishan pigs, Cotton Patch Geese, Beltsville Small White Turkeys, and a host of non-heritage breeds all running around loose.
Every fence post helps.  Thanks!  https://ko-fi.com/epistria
