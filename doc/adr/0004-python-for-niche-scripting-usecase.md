# 4. Python for nitch scripting usecase

Date: 2026-04-14

## Status

Accepted

## Context

For niche use cases—such as specialized domain data processing, custom automation tools, and high-performance scripting—we need a foundational stack that addresses several recurring pain points:

1. **Performance**: Scripts must execute within a practical timeframe even as data volume scales.

2. **Memory Efficiency**: Handling large-scale datasets without exhausting hardware resources (RAM).

3. **Expressiveness**: The ability to write complex logic concisely to ensure long-term maintainability.

4. **Interoperability**: Seamless integration with existing numerical and scientific computing ecosystems.

While pandas has been the historical standard, its high memory overhead and implicit data copying often become bottlenecks in specialized, high-throughput environments.

## Decision

We will adopt the following three components as the core "Golden Stack" for all internal scripting projects:

**Python 3.11+**: For its improved interpreter speed and robust type-hinting support.

**Polars**: For high-performance, memory-efficient DataFrame manipulation.

**NumPy**: For low-level numerical arrays and specialized mathematical operations.

### Rationale

#### 1. The Efficiency of Polars
Built on Rust and powered by the Apache Arrow specification, Polars offers:

Lazy API: It optimizes query plans before execution, eliminating redundant computations.

Memory Management: Utilizing Arrow allows for zero-copy operations and significantly lower memory footprints compared to pandas.

Parallelism: It leverages all available CPU cores by default without requiring manual configuration.

#### 2. NumPy as the Mathematical Foundation
While Polars is excellent for structured data, niche scripts often require complex matrix algebra or scientific functions.

NumPy remains the industry standard for these operations.

Polars provides an efficient to_numpy() path, allowing us to switch between "structured tables" and "mathematical matrices" with minimal overhead.

#### 3. Suitability for Niche Domains
Niche scripts often live for a long time and undergo frequent logic tweaks. The Polars API (using pl.col()) encourages a functional, declarative style that is easier to debug and less prone to "SettingWithCopy" warnings found in older libraries.

## Consequences

### Positive
Developer Experience: Clean, method-chained code improves readability.

**Cost Efficiency**: Lower memory usage allows scripts to run on cheaper cloud instances or standard laptop hardware.

**Scalability**: The stack handles datasets that would typically crash a traditional pandas-based script.

### Negative / Risks

**Learning Curve**: Team members familiar with pandas will need to adapt to the "Expressions" syntax of Polars.

**Ecosystem Compatibility**: Some legacy visualization or machine learning libraries may still require an intermediate conversion step to pandas or NumPy.

### Alternatives Considered
**Pure Python**: Too slow for datasets exceeding a few thousand rows.

**Pandas 2.x (with PyArrow backend)**: While an improvement, it still carries legacy API baggage (like the Index object) that complicates the internal logic of specialized scripts.
