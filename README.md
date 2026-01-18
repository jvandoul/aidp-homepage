# AIDP — Agent Interaction & Delegation Protocol

AIDP (Agent Interaction & Delegation Protocol) is a protocol specification
for secure, deterministic, and auditable interaction and delegation
between autonomous agents and execution environments across trust
boundaries.

The protocol defines how an Agent expresses intent, how authority and
constraints are validated, how execution is enforced, and how results
or failures are returned in a verifiable and non-ambiguous manner.

AIDP is designed to address core safety, security, and interoperability
problems in agent-based systems.

---

## Status

This repository hosts an **individual Internet-Draft** under active
development.

Current version:
- `draft-vandoulas-aidp-01`

The draft is not yet associated with an IETF Working Group.

---

## Problem Statement

As AI agents become capable of performing actions on behalf of users,
organizations, and systems, existing interaction models fail to provide
clear answers to fundamental questions:

- Who authorized a given action?
- Under what constraints was the action allowed?
- How is delegation scoped, validated, and revoked?
- How are execution results bound to the original intent?
- How are non-deterministic or unsafe agent loops prevented?

AIDP provides protocol-level mechanisms to address these questions.

---

## Core Message Types

AIDP defines three primary protocol messages:

- **Intent Envelope (IE)**  
  A signed, canonicalized message expressing an Agent’s intent to perform
  a specific action under explicit authority and constraints.

- **Observation (OB)**  
  A cryptographically bound and attested result of execution, linking the
  outcome to the originating Intent Envelope.

- **Problem Details (PD)**  
  A structured error or rejection message produced when an Intent cannot
  be executed.

These messages form a deterministic and auditable interaction loop.

---

## Architectural Model

An AIDP-compliant system consists of two primary roles:

- **Agent Runtime (AR)**  
  Responsible for intent formulation, validation, and deterministic
  reasoning control.

- **Execution Boundary (EB)**  
  Responsible for authority verification, constraint enforcement,
  execution, and observation attestation.

The EB is authoritative for execution decisions, while the AR is
responsible for safe reasoning progression.

---

## Deterministic Agent Control Loop

AIDP enforces a deterministic agent control loop:

- An Agent MUST NOT advance reasoning that causally depends on an Intent
  without receiving a validated Observation.
- Parallel, causally-independent intents are explicitly permitted.
- Deterministic failures trigger retry suppression to prevent infinite
  re-issuance loops.

This model enables autonomous agents without sacrificing safety or
auditability.

---

## Error Propagation & Retry Semantics

Execution failures are communicated via Observations or Problem Details
messages.

AIDP defines:

- Deterministic failure classification
- Optional `execution_advice` for retry and backoff guidance
- Mandatory retry suppression for semantically identical failed intents

These mechanisms prevent non-terminating agent behavior and enforce
reasoning safety.

---

## Canonicalization & Security

All signed messages use a deterministic canonical signing input.

For JSON-based encoding (AIDP-JS):

- Duplicate object member names are forbidden
- Deterministic lexicographic ordering is required
- Messages with duplicate keys MUST be rejected during parsing

These requirements eliminate ambiguity and prevent signature confusion
attacks.

---

## Cross-Domain Interaction

AIDP supports cross-domain agent interaction through explicit identity
resolution and trust boundary enforcement.

Identity references MUST conform to one of the following models:

- Dereferenceable identities
- Self-contained, cryptographically verifiable identities

Issuer validation and revocation checks are enforced at each trust
boundary crossing.

---

## Specification

The normative specification is contained in:

- `draft-vandoulas-aidp-01.txt`

Appendix A of the draft documents changes relative to prior versions.

---

## Non-Goals

AIDP intentionally does NOT define:

- Agent prompting strategies or LLM behavior
- Application-level business logic
- User interfaces or UX
- Policy or rule languages

These concerns are explicitly out of scope.

---

## Contributing

Technical feedback and protocol review are welcome.

This repository currently does not accept code contributions.
Please open an issue to discuss protocol semantics, security properties,
or interoperability concerns.

---

## License

This specification is provided under the terms of the IETF Trust License.
See: https://trustee.ietf.org/license-info/

---

## Author

Ioannis Vandoulas  
Email: jvandoul@gmail.com
