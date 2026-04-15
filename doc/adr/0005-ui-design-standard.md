# 5. design standard

Date: 2026-04-15

## Status

Accepted

## Context

To ensure product consistency and improve development velocity, a unified set of UI components and visual rules is required. For systems handling complex global data, a "balanced and professional" visual language—one that minimizes decorative clutter while maximizing clarity—is essential. This ADR formalizes the use of the theme defined in [DESIGN.md](../design_standard/DESIGN.md).

## Decision

We will adopt the **"Tanunekolab Cool Theme"** as the standard design stack for all UI development and frontend implementation within this project. All implementations must strictly adhere to the specifications in the referenced DESIGN.md.

### 1. Typography Strictness
**Primary Typeface**: Use -apple-system to ensure high legibility and a native OS feel.

**Secondary Typeface**: Times New Roman is permitted only for supplementary or specific decorative elements.

**Scale and Weights**: Only the defined font sizes (14px to 60px) and weights (300, 400, 600, 700) may be used.

### 2. Color Palette and Roles
**Primary Action (CTA)**: Use Blue (#7297C5) for all primary buttons and calls to action.

**Text Hierarchy**: Use Black (#000000) for primary text and Dark gray (#666666) for secondary information.

**Constraint**: No colors outside the defined palette (White, Blue, Black, Dark/Light Gray) shall be introduced.

### 3. Layout and Spacing Principles
**16px Base Unit**: All spacing, margins, and padding must follow the 16px grid system.

**Spacing Scale**: Use only the values defined in the scale (12px, 14px, 16px, 24px, 28px, 32px, 40px, 120px).

**Depth**: Maintain a flat design aesthetic with minimal shadow usage to reduce cognitive load.

### Compliance Criteria (Checklist)

**Do**: Verify that all spacing aligns with the 16px grid.

**Do**: Ensure #7297C5 is the dominant color for primary user actions.

**Don't**: Introduce external fonts or inline styles that bypass the system.

**Don't**: Use colors or font weights (e.g., 500 or 800) not explicitly listed in the theme.

## Consequences

What becomes easier or more difficult to do and any risks introduced by the change that will need to be mitigated.
