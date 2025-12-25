---
# ALN Programming Language

ALN (Auditable Legal Notation) is a **domain-specific** language for describing deterministic infrastructure, QPU.Datashards, and augmented-human / smart‑city safety envelopes as CSV‑style tables that compile into concrete artifacts instead of remaining a design concept.[web:13][file:1]

ALN focuses on:
- Declarative infra and safety descriptions with strict schemas and reproducible outputs.[web:13][file:1]
- CSV/Markdown/mermaid interoperability so the same source files feed both tools and documentation.[web:22][file:1]
- Public‑only semantics: no classified topologies, secret keys, or enterprise‑internal opcodes in the open repository.[web:13][file:1]

## Status

- Stage: alpha / experimental.[web:14][file:1]
- Stability: the core file format (ALN‑CSV), rowtype names, and CLI surface are being stabilized toward v0.1.0 tags.[web:14][file:1]
- Compatibility: breaking changes can occur between pre‑0.1 tags; pin a Git tag or GitHub Release when integrating.[web:14][web:15]

## What ALN is (and is not)

ALN **is**:
- A textual, table‑oriented language (ALN‑CSV) for infra, safety, and data‑shard descriptions.[file:1]
- A spec + CLI that validate, lint, render and compile ALN sources into normalized CSV and diagrams.[web:14][file:1]
- A public, auditable layer that sits above existing engines (Kubernetes, schedulers, QPU backends, etc.).[web:15][file:1]

ALN is **not**:
- A general‑purpose Turing‑complete language or GPU compiler like other Alan/ALN projects.[web:14][web:20]
- An adventure‑game language (Alan IF) or Turing‑machine DSL; it is unrelated despite similar naming.[web:19][web:22]
- A container for secrets, token keys, or internal Death‑Network constructs; those are explicitly out of scope.[web:13][file:1]

## Quick install

For the reference Rust implementation:

```
git clone https://github.com/Doctor0Evil/ALN-Programming-Language.git
cd ALN-Programming-Language
cargo install --path cmd/aln-cli
```

- Requires: Rust stable toolchain, a C toolchain, and standard build tools, similar to other language compilers.[web:14][file:1]

After installation, the `aln` binary should be on your `PATH`:

```
aln --help
```

## First ALN file (QPU.Datashard “Hello World”)

Create `examples/minimal_qpu_datashard.aln`:

```
destination,docs/qpudatashards
format,ALN-CSV,1.0

rowtype,id,path,role,status
qpudatashard,hello-qpu,shards/hello,datashard,active

entropy,id,p_code,p_data,H_code,H_data
entropy-weights,default,0.6,0.4,1.20,0.80

geo,id,locations
geo-evidence,global,"Phoenix-AZ;San-Francisco-CA;Seattle-WA;Berlin-DE;Singapore-SG"
```

Then run:

```
aln validate examples/minimal_qpu_datashard.aln
aln render  examples/minimal_qpu_datashard.aln --format mermaid
```

- `validate` checks the file against the ALN spec and grammar.[web:14][file:1]
- `render` produces a mermaid‑compatible diagram or CSV, suitable for inclusion in Markdown docs.[web:7][web:9]

## Documentation map

- Language guide: `docs/language-guide.md` — getting started, types, control‑flow via references, modules, interop.[web:22][web:19]
- Spec and grammar: `docs/spec.md`, `docs/grammar.md` — formal definition of tokens, rowtypes, and CSV mapping.[web:19][file:1]
- Design goals / non‑goals: `docs/design-goals.md` — determinism, safety boundaries, public‑only semantics.[web:13][file:1]
- Examples: `examples/` — minimal QPU.Datashard, smart‑city topology, game/engine stub, policy/safety shard.[web:22][file:1]

## Releases and stability

- Tagged releases and GitHub Releases will define stable ALN specs and CLI binaries, similar to other languages in the GitHub programming‑language collection.[web:14][web:15]
- Each release updates `CHANGELOG.md` with spec changes, new rowtypes, and CLI behavior, so integrators can safely upgrade.[web:14][web:15]

---
