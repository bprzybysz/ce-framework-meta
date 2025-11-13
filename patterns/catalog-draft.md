# Agentic Patterns Catalog (Draft)

This catalog documents high-value, best-practice patterns for agentic system meta-representation. All patterns below will be drafted, formalized, and validated during initial refinement cycles.

- **Observer (Behavioral):**
  - Pattern: Event-driven propagation, isolated agents, minimal coupling
  - Meta: Agent subscribes and observes state changes
  - Constraint: Only agentic events trigger updates

- **Facade (Structural):**
  - Pattern: Unified interface, hides internals, clear boundary for agent interactions
  - Meta: Encapsulation of agent workflows
  - Constraint: No direct cross-boundary interactions

- **Cascade (Compositional):**
  - Pattern: Parallel or chained execution, error isolation
  - Meta: Define propagation rules across agent graph
  - Constraint: Every node has fallback/terminate handler

- **Sequential/Stateful (Meta):**
  - Pattern: Single agent controls linear progress
  - Meta: State preserved and advanced in discrete steps
  - Constraint: State transitions tracked per agent

- **Validation/Quality Gates (Meta):**
  - Pattern: Automatic enforcement of agent constraints
  - Meta: Review cycles, quality gates at boundaries
  - Constraint: Rules documented and versioned

- **Composition/Integration (Meta):**
  - Pattern: Robust links between agentic modules
  - Meta: Strongly typed edges, pattern compatibility
  - Constraint: Edge types validated on migration

This catalog is initial and must be reviewed during the first refinement cycle, evolving to include further relevant agentic system patterns and additional constraints.