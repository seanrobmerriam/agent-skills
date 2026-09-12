---
name: designing-token-systems
description: Use when creating, extending, auditing, or migrating a token-based visual design system, especially CSS custom properties, color themes, spacing and typography scales, component aliases, or framework token mappings.
---

# Designing Token Systems

Build a coherent contract between visual decisions and component CSS. Optimize for semantic usage, themeability, accessibility, and controlled evolution—not for the largest possible token catalog.

## Workflow

1. Inspect the existing application, styles, components, supported browsers, build tools, themes, and brand constraints. Preserve deliberate conventions; report invalid or contradictory input instead of silently copying it.
2. Establish a brief: visual character, density, target platforms, themes, accessibility target, framework integrations, and required deliverables. Ask only for choices that materially change the system.
3. Inventory current literal values and custom properties. Group repeated values by intent, not merely by identical syntax.
4. Design three layers:
   - **Primitive:** context-free values such as color ramps, dimensions, font families, radii, shadows, and durations.
   - **Semantic:** purpose-based roles such as surfaces, text, borders, actions, focus, and status pairs.
   - **Component:** optional aliases for stable component contracts when semantic roles alone cannot express a component's states.
5. Implement semantic themes by remapping roles. Components consume semantic or component tokens; they do not choose primitive palette steps directly.
6. Map tokens into Tailwind, CSS-in-JS, Style Dictionary, or another framework only after the source-of-truth layer is sound. Keep framework names as adapters, not a second source of truth.
7. Validate syntax, references, cycles, duplicate definitions, scale progression, contrast pairs, focus states, forced-colors behavior, reduced motion, and representative components in every theme.
8. Deliver the token files, an inventory of roles and intended consumers, integration notes, validation results, and any unresolved design decisions.

## Required Decisions

- Choose a source of truth and state it.
- Use one canonical name for each decision; aliases need a migration or interoperability reason.
- Separate fill colors from colors intended for text/icons on that fill.
- Model interactive states explicitly: default, hover, active, focus, selected, and disabled where applicable.
- Keep light, dark, inverted, and high-contrast values aligned by semantic role rather than palette index.
- Prefer bounded scales. Add a token because a real use case needs it, not to complete an arbitrary sequence.
- Treat comments containing contrast ratios as claims that must be recalculated when either color changes.

## Output Shape

Adapt filenames to the project. A CSS-first system typically uses:

```text
styles/
├── tokens/
│   ├── primitives.css
│   ├── colors.css
│   ├── spacing.css
│   ├── typography.css
│   ├── effects.css
│   └── motion.css
└── global.css
```

Include component tokens in component styles or a dedicated file only when they form a reusable public contract. Do not create empty category files.

## References and Validation

- Read [architecture-and-naming.md](references/architecture-and-naming.md) when defining layers, scales, names, themes, or framework adapters.
- Read [accessibility-and-quality.md](references/accessibility-and-quality.md) when selecting colors, typography, motion, focus, or validating a system.
- Run `python scripts/validate_css_tokens.py <file-or-directory>`. Use `--strict` before delivery. The validator supplements a real CSS parser and visual/contrast testing; it does not replace them.

## Completion Contract

Before calling the system complete, provide:

- the source-of-truth token files and import order;
- a primitive-to-semantic-to-component mapping for important roles;
- theme selectors and fallback behavior;
- verified foreground/background contrast pairs;
- a report of validator errors and warnings;
- one representative component-state review across every supported theme.
