# 3. Rust Web Assembly for web frontend

Date: 2026-01-14

## Status

Accepted

## Context

The issue motivating this decision, and any context that influences or constrains the decision.

ADR: Adoption of Rust-based WebAssembly (Wasm) for Frontend/Edge Logic
Context
Our current architecture relies heavily on JavaScript for client-side logic and localized data processing. However, as the complexity of our application increases—particularly in areas involving heavy data transformation, cryptographic operations, and complex business rules—we are facing several challenges:

Performance Bottlenecks: High-computational tasks in JavaScript often lead to main-thread blocking, resulting in dropped frames and a degraded user experience (UX).

Code Portability & Consistency: We need a way to share critical business logic (e.g., payment validation, data parsing) between our Rust backend and the frontend without re-implementing the logic in JavaScript, which introduces "logic drift" and maintenance overhead.

Security & Sandboxing: For edge computing and plugin systems, we require a high-performance execution environment that is securely sandboxed from the host system.

Operational Efficiency: As we move toward an Agent-Driven Development model, we need an ecosystem where high-performance modules can be compiled into a universal format that runs across browsers, servers, and edge nodes.

Rust, when compiled to WebAssembly, offers near-native execution speed, a robust type system that prevents runtime errors, and a mature tooling ecosystem (such as wasm-bindgen and wasm-pack). This allows us to move performance-critical or shared logic into a highly optimized Wasm binary.

### Libraries

1. Core Interop (JS/Rust Bridge)
wasm-bindgen: The fundamental library for facilitating high-level interactions between Wasm modules and JavaScript. It allows us to import JS functions and export Rust functions/structs.

js-sys: Provides raw bindings to all standard JavaScript global objects and functions (e.g., Date, Math, JSON).

web-sys: Provides raw bindings to all Web APIs, including DOM manipulation, WebGL, Fetch API, and Web Storage.

2. Frontend Framework (Optional but Recommended)
Yew: A modern Rust framework for creating multi-threaded front-end web apps with WebAssembly. It features a component-based pattern similar to React.

Leptos: A full-stack, isomorphic framework that focuses on high performance and fine-grained reactivity.

3. Serialization & Memory
serde-wasm-bindgen: A library to efficiently serialize/deserialize data between Rust and JavaScript using serde. It is generally faster than the default JsValue conversion for complex objects.

getrandom: Must be configured with the js feature to provide cryptographically secure random numbers within a Wasm environment.

4. Performance & Utility
console_error_panic_hook: Essential for debugging. It redirects Rust panic messages to the browser’s console.error, providing readable stack traces.

wee_alloc: (Optional) A tiny allocator for when binary size is extremely critical. It reduces the Wasm footprint by several kilobytes compared to the default allocator.

5. Async Support
wasm-bindgen-futures: A bridge between JavaScript Promises and Rust Futures. Essential for making asynchronous calls (like fetch) from Wasm.

### Project Archetype

```text
{{project_name}}                     # project root
├─ {{project_name}}_wa/        # Web Assembly front end
│   └─ auth/                    # auth-protected route
│   └─ public/                  # public route
│   └─ api/                        # API route
├─ {{project_name}}-shared/  # shared libraries/component between back and front
├─ scripts_local/                     # scripts for local testing
├─ docs/                   # documents
```

## Decision

We will adopt Rust (compiled to WebAssembly) for frontend development, specifically targeting performance-critical modules, shared business logic, and complex data processing components.

Depending on the specific requirements of the module, we will follow these implementation patterns:

Hybrid Approach: Use Rust/Wasm for heavy computation and core logic, while maintaining JavaScript/TypeScript for UI orchestration and simple DOM interactions.

Full-Rust Framework: For new, highly interactive internal tools, we will evaluate the use of Leptos or Yew to manage the entire UI lifecycle in Rust.

## Consequences

1. Positive (Benefits)
Extreme Performance: We can achieve near-native execution speeds for tasks like heavy mathematical calculations, data parsing, and image processing, effectively eliminating UI lag caused by main-thread blocking.

Code Reusability (Single Source of Truth): Core business logic, validation rules, and data structures (via serde) can be shared 1:1 between the Rust backend and the frontend. This drastically reduces "logic drift" and synchronization bugs.

Enhanced Reliability: Rust’s strict type system and memory safety guarantees extend to the frontend, significantly reducing runtime exceptions (undefined is not a function) that are common in traditional JS environments.

Future-Proofing for Edge/Agent Computing: Wasm modules are portable. The same logic we build for the browser today can be deployed to Cloudflare Workers or integrated into our "Marie" agent system in the future without modification.

2. Negative (Trade-offs & Challenges)
Increased Bundle Size: Wasm binaries can be larger than equivalent minified JavaScript. We must implement aggressive optimization (e.g., wasm-opt, wee_alloc) and code-splitting to mitigate impact on initial load times.

Debugging Complexity: Despite improvements in Source Maps, debugging Rust code within browser DevTools remains more difficult than debugging TypeScript. Developers will need to rely more heavily on unit testing in Rust.

Interoperability Overhead: Passing large amounts of data between JavaScript and Wasm (across the "boundary") incurs a serialization/deserialization cost. We must design our APIs to minimize frequent boundary crossings.

Steep Learning Curve: The frontend team will need to gain proficiency in Rust’s ownership and borrowing concepts, which may initially slow down development velocity compared to a pure TS/React stack.