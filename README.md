# WASI SQL Embedding

A proposed [WebAssembly System Interface](https://github.com/WebAssembly/WASI) API.

### Current Phase

WASI SQL Embedding is currently in [Phase 1](https://github.com/WebAssembly/WASI/blob/main/Proposals.md#phase-1---feature-proposal-cg).

### Champions

- Robin Brown

### Phase 4 Advancement Criteria

TODO before entering Phase 2.

## Table of Contents [if the explainer is longer than one printed page]

- [Introduction](#introduction)
- [Goals [or Motivating Use Cases, or Scenarios]](#goals-or-motivating-use-cases-or-scenarios)
- [Non-goals](#non-goals)
- [API walk-through](#api-walk-through)
  - [Use case 1](#use-case-1)
  - [Use case 2](#use-case-2)
- [Detailed design discussion](#detailed-design-discussion)
  - [[Tricky design choice 1]](#tricky-design-choice-1)
  - [[Tricky design choice 2]](#tricky-design-choice-2)
- [Considered alternatives](#considered-alternatives)
  - [[Alternative 1]](#alternative-1)
  - [[Alternative 2]](#alternative-2)
- [Stakeholder Interest & Feedback](#stakeholder-interest--feedback)
- [References & acknowledgements](#references--acknowledgements)

### Introduction

WASI SQL Embedding defines a way for WASM components to be embedded in SQL databases as extensions.
It defines the interfaces for various user objects (like User-Defined Functions a.k.a. UDFs) that can be exported by extensions and called from the database, the way component value types and SQL column types are mapped, and the facilities user objects are allowed to access/use.

WASI SQL Embedding abstracts over different SQL dialects and their types.
Extensions may either explicitly call out the SQL types of their arguments and results or allow them to be inferred.
If an Extension refers to a SQL type that is not supported by a given dialect, the embedder may decide to infer a type that they do support.

WASI SQL Embedding extension components will have some limited access to capabilities like random number generation,
but not any capabilities that access the file system or network.
Code that relies on the network or file-system should satisfy those requirements using virtualizations.

### Goals

The primary goal of WASI SQL Embedding is to enable users to define Wasm-based SQL Extensions in a standard way.

### Non-goals

[If there are "adjacent" goals which may appear to be in scope but aren't, enumerate them here. This section may be fleshed out as your design progresses and you encounter necessary technical and other trade-offs.]

### API walk-through

The full API documentation can be found [here](wasi-proposal-template.md).

[Walk through of how someone would use this API.]

#### Unicode Functionality

If a user wanted to perform unicode normalization on some text in a database,
it would be convenient if they could write a simple extension that takes advantage of existing libraries.

e.g.
```rust
use unicode_normalization::UnicodeNormalization;

fn normalize(input: String) -> String {
  input.nfc().collect::<String>()
}
```
> **Note**
> Bindings-related code and configuration is omitted

After compiling this using WIT-based tooling, they would end up with a fully self-describing database extension.

They could load this into a database and normalize user names like so.
```sql
CREATE EXTENSION unicode FROM "https://...";
...
SELECT unicode_normalize(name) FROM users;
```

#### [Use case 2]

[etc.]

### Detailed design discussion

[This section should mostly refer to the .wit.md file that specifies the API. This section is for any discussion of the choices made in the API which don't make sense to document in the spec file itself.]

#### [Tricky design choice #1]

[Talk through the tradeoffs in coming to the specific design point you want to make.]

```
// Illustrated with example code.
```

[This may be an open question, in which case you should link to any active discussion threads.]

#### [Tricky design choice 2]

[etc.]

### Considered alternatives

[This section is not required if you already covered considered alternatives in the design discussion above.]

#### [Alternative 1]

[Describe an alternative which was considered, and why you decided against it.]

#### [Alternative 2]

[etc.]

### Stakeholder Interest & Feedback

TODO before entering Phase 3.

[This should include a list of implementers who have expressed interest in implementing the proposal]

### References & acknowledgements

Many thanks for valuable feedback and advice from:

- [Person 1]
- [Person 2]
- [etc.]
