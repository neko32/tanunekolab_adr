# 2. Rust for backend micro service

Date: 2026-01-14

## Status

Accepted

## Context

### Libraries

1. Web Framework & Runtime
Tokio: The industry-standard asynchronous runtime for Rust. Required for high-concurrency network applications.

Axum: A web framework from the Tokio team. It focuses on ergonomic API design and leverages the tower ecosystem for middleware.

2. Serialization & Configuration
Serde: The essential framework for serializing and deserializing Rust data structures (JSON, YAML, etc.).

Config: A library to manage layered configuration (environment variables, TOML, JSON) across different environments (dev/prod).

3. Database & Persistence
SQLx: A modern, async, compile-time checked SQL toolkit. It allows writing raw SQL while ensuring type safety without the overhead of a full ORM.

SeaORM: (Optional) If a high-level ORM is required for complex relational mapping, SeaORM is the preferred choice as it is built on top of SQLx.

4. Observability (Logging & Tracing)
Tracing: A framework for instrumenting Rust programs to collect structured, event-based diagnostic information. Essential for distributed tracing in microservices.

Serde_json: Often used alongside Tracing to output logs in structured JSON format for tools like ELK or Datadog.

5. Error Handling
Anyhow: Used for high-level error handling in applications (e.g., in main or API handlers) where you just need to propagate errors.

Thiserror: Used for creating custom, reusable error types in library-like modules or core business logic.

6. Testing & Utility
Tower-HTTP: Provides essential middleware for Axum, such as CORS, Compression, and Request ID.

Mockall: A powerful library for creating mock objects in unit tests.

### Project Architype

```text
{{project_name}}/
├── .github/              # CI/CD settings（for auto build）
├── app/              # Rust project (logic/API)
│   ├── src/
│   │   ├── main.rs       # entry point
│   │   ├── api/          # API
│   │   └── core/         # System control, heavy calculation etc,..
│   ├── Cargo.toml
│   └── .env              # settings
│   └── bin/              # Compiled rust binaries
└── docs/                 # memo, documents, prompts
└── scripts/                 # scripts to run the service or utilities
```

### Scripts Used on the Server End

If the specifications state that the service should run on a server, create it; however, for command-line tools or client applications, you do not need to generate it.

## Decision

We will use Rust as the primary language for all new backend microservices and performance-critical components.

## Consequences

1. Performance and Efficiency
Rust provides execution speed comparable to C and C++, but with modern safety guarantees. This allows us to handle high-throughput workloads with minimal hardware overhead.

Zero-cost abstractions mean we don't pay a performance penalty for using high-level features.

Reduced cloud infrastructure costs due to lower memory and CPU footprints.

2. Memory Safety without Garbage Collection
Rust’s ownership model ensures memory safety and prevents common bugs like null pointer dereferences and data races at compile time.

Elimination of "Stop-the-world" GC pauses, ensuring predictable latency (P99).

Significantly fewer runtime crashes compared to languages like C++ or Go.

3. Concurrency and Reliability
The "Fearless Concurrency" philosophy allows developers to write multi-threaded code that is guaranteed to be free of data races by the compiler.

Improved reliability for asynchronous processing and distributed systems.

4. Strong Ecosystem and Tooling
The Rust ecosystem (Cargo, crates.io) provides world-class package management and integrated testing frameworks.

Strong support for WebAssembly (Wasm), gRPC, and cloud-native integrations.

### Challenges & Mitigations

#### Learning Curve: Rust has a steeper learning curve than Python or TypeScript.

#### Mitigation

 We will implement a "Rust Guild" for internal mentorship and provide dedicated time for team training.

 Signature: [kazu_neko64](https://github.com/neko32)

#### Compilation Times

Rust’s compiler is thorough, which can lead to slower build times.

#### Mitigation

We will utilize CI/CD caching strategies and tools like sccache to optimize build pipelines.

