# Agentic Patterns: Updated with Examples

This document extends the initial pattern catalog with concrete examples and usage guidance for agentic system implementation.

## Observer (Behavioral)

**Pattern**: Event-driven propagation, isolated agents, minimal coupling

**Meta**: Agent subscribes and observes state changes

**Constraint**: Only agentic events trigger updates

### Example: PRP Execution Observer

```python
class PRPExecutionObserver:
    """Observes PRP execution events and updates tracking."""
    
    def __init__(self, tracking_system):
        self.tracking = tracking_system
        self.subscriptions = []
    
    def subscribe(self, event_type, handler):
        """Subscribe to PRP execution events."""
        self.subscriptions.append((event_type, handler))
    
    def notify(self, event):
        """Notify subscribers of PRP execution events."""
        for event_type, handler in self.subscriptions:
            if event.type == event_type:
                handler(event)

# Usage
observer = PRPExecutionObserver(tracking)
observer.subscribe("phase_complete", update_progress)
observer.subscribe("validation_failed", handle_failure)
```

**Graph Representation**:
```yaml
id: pattern:behavioral:observer:prp-execution
name: PRP Execution Observer
relationships:
  - EXTENDS:pattern:behavioral:observer
  - DEPENDS_ON:pattern:structural:event-bus
  - USES:pattern:meta:progress-tracking
```

---

## Facade (Structural)

**Pattern**: Unified interface, hides internals, clear boundary for agent interactions

**Meta**: Encapsulation of agent workflows

**Constraint**: No direct cross-boundary interactions

### Example: Migration Facade

```python
class MigrationFacade:
    """Unified interface for pattern migration operations."""
    
    def __init__(self):
        self.snapshot_mgr = SnapshotManager()
        self.validation = ValidationSuite()
        self.graph_db = GraphDatabase()
    
    def migrate_pattern(self, pattern_id, target_version):
        """Migrate pattern with automatic snapshot and validation."""
        # Create snapshot
        snapshot_id = self.snapshot_mgr.create()
        
        try:
            # Perform migration
            pattern = self.graph_db.get_pattern(pattern_id)
            updated = pattern.migrate_to(target_version)
            self.graph_db.update(updated)
            
            # Validate
            errors = self.validation.validate(updated)
            if errors:
                raise ValidationError(errors)
            
            return MigrationResult(success=True, snapshot=snapshot_id)
        
        except Exception as e:
            # Rollback on failure
            self.snapshot_mgr.rollback(snapshot_id)
            return MigrationResult(success=False, error=str(e))

# Usage in Claude Code
facade = MigrationFacade()
result = facade.migrate_pattern("pattern:behavioral:observer", "2.0.0")
```

**Graph Representation**:
```yaml
id: pattern:structural:facade:migration
name: Migration Facade
relationships:
  - EXTENDS:pattern:structural:facade
  - COMPOSES:pattern:meta:snapshot
  - COMPOSES:pattern:meta:validation
  - COMPOSES:pattern:meta:rollback
```

---

## Cascade (Compositional)

**Pattern**: Parallel or chained execution, error isolation

**Meta**: Define propagation rules across agent graph

**Constraint**: Every node has fallback/terminate handler

### Example: Validation Cascade

```python
class ValidationCascade:
    """Cascade validation across pattern graph."""
    
    def __init__(self, graph):
        self.graph = graph
        self.handlers = []
    
    def add_validator(self, validator, on_error=None):
        """Add validator to cascade with error handler."""
        self.handlers.append((validator, on_error or self.default_handler))
    
    def validate(self, pattern_id):
        """Run cascade validation on pattern and dependencies."""
        pattern = self.graph.get_pattern(pattern_id)
        dependencies = self.graph.get_dependencies(pattern_id)
        
        # Parallel validation of dependencies
        dep_results = []
        for dep in dependencies:
            try:
                result = self.validate_pattern(dep)
                dep_results.append(result)
            except ValidationError as e:
                # Error isolation - continue cascade
                dep_results.append(ValidationResult(success=False, error=e))
        
        # Validate pattern if dependencies pass
        if all(r.success for r in dep_results):
            return self.validate_pattern(pattern)
        else:
            return ValidationResult(
                success=False,
                error="Dependency validation failed",
                dep_errors=dep_results
            )
    
    def validate_pattern(self, pattern):
        """Run all validators on pattern."""
        for validator, error_handler in self.handlers:
            try:
                result = validator.validate(pattern)
                if not result.success:
                    error_handler(result.error)
            except Exception as e:
                error_handler(e)
        
        return ValidationResult(success=True)

# Usage
cascade = ValidationCascade(graph)
cascade.add_validator(StructuralValidator())
cascade.add_validator(SemanticValidator())
cascade.add_validator(AxiomValidator())

result = cascade.validate("pattern:behavioral:observer")
```

**Graph Representation**:
```yaml
id: pattern:compositional:cascade:validation
name: Validation Cascade
relationships:
  - EXTENDS:pattern:compositional:cascade
  - DEPENDS_ON:pattern:meta:validation
  - USES:pattern:compositional:parallel-execution
```

---

## Sequential/Stateful (Meta)

**Pattern**: Single agent controls linear progress

**Meta**: State preserved and advanced in discrete steps

**Constraint**: State transitions tracked per agent

### Example: PRP Execution State Machine

```python
from enum import Enum

class PRPState(Enum):
    PENDING = "pending"
    IN_PROGRESS = "in_progress"
    VALIDATING = "validating"
    COMPLETED = "completed"
    FAILED = "failed"

class PRPStateMachine:
    """Stateful execution of PRP phases."""
    
    def __init__(self, prp_id):
        self.prp_id = prp_id
        self.state = PRPState.PENDING
        self.current_phase = 0
        self.phase_results = []
    
    def start(self):
        """Start PRP execution."""
        if self.state != PRPState.PENDING:
            raise StateTransitionError("PRP already started")
        
        self.state = PRPState.IN_PROGRESS
        self.log_transition(PRPState.PENDING, PRPState.IN_PROGRESS)
    
    def complete_phase(self, result):
        """Mark current phase complete and advance."""
        if self.state != PRPState.IN_PROGRESS:
            raise StateTransitionError("Invalid state for phase completion")
        
        self.phase_results.append(result)
        self.current_phase += 1
        
        # Check if all phases complete
        if self.current_phase >= self.total_phases:
            self.state = PRPState.VALIDATING
            self.log_transition(PRPState.IN_PROGRESS, PRPState.VALIDATING)
    
    def complete(self):
        """Mark PRP execution complete."""
        if self.state != PRPState.VALIDATING:
            raise StateTransitionError("Must validate before completion")
        
        self.state = PRPState.COMPLETED
        self.log_transition(PRPState.VALIDATING, PRPState.COMPLETED)
    
    def fail(self, error):
        """Mark PRP execution failed."""
        previous_state = self.state
        self.state = PRPState.FAILED
        self.error = error
        self.log_transition(previous_state, PRPState.FAILED)
    
    def log_transition(self, from_state, to_state):
        """Log state transition."""
        # Update progress tracking
        pass

# Usage in Claude Code
prp = PRPStateMachine("PRP-META-001")
prp.start()

for phase in prp.phases:
    result = execute_phase(phase)
    if result.success:
        prp.complete_phase(result)
    else:
        prp.fail(result.error)
        break

if prp.state == PRPState.VALIDATING:
    prp.complete()
```

**Graph Representation**:
```yaml
id: pattern:meta:sequential:prp-state-machine
name: PRP State Machine
relationships:
  - EXTENDS:pattern:meta:sequential
  - DEPENDS_ON:pattern:meta:progress-tracking
  - USES:pattern:meta:validation
```

---

## Validation/Quality Gates (Meta)

**Pattern**: Automatic enforcement of agent constraints

**Meta**: Review cycles, quality gates at boundaries

**Constraint**: Rules documented and versioned

### Example: Refinement Cycle Quality Gates

```python
class RefinementQualityGate:
    """Quality gates for refinement cycle completion."""
    
    def __init__(self, cycle_id):
        self.cycle_id = cycle_id
        self.gates = []
    
    def add_gate(self, name, validator, threshold):
        """Add quality gate with threshold."""
        self.gates.append({
            "name": name,
            "validator": validator,
            "threshold": threshold
        })
    
    def evaluate(self):
        """Evaluate all quality gates."""
        results = []
        
        for gate in self.gates:
            value = gate["validator"]()
            passed = value >= gate["threshold"]
            
            results.append({
                "gate": gate["name"],
                "value": value,
                "threshold": gate["threshold"],
                "passed": passed
            })
        
        all_passed = all(r["passed"] for r in results)
        return QualityGateResult(passed=all_passed, gates=results)

# Usage for Cycle 2
gate = RefinementQualityGate("cycle-2")
gate.add_gate("coverage", lambda: calculate_coverage(), threshold=0.65)
gate.add_gate("error_rate", lambda: calculate_error_rate(), threshold=0.03)
gate.add_gate("validation_pass", lambda: run_validation_suite(), threshold=1.0)

result = gate.evaluate()
if not result.passed:
    raise QualityGateError("Cycle 2 quality gates not met", result.gates)
```

**Graph Representation**:
```yaml
id: pattern:meta:quality-gate:refinement-cycle
name: Refinement Cycle Quality Gate
relationships:
  - EXTENDS:pattern:meta:quality-gate
  - VALIDATES:pattern:meta:refinement-cycle
  - DEPENDS_ON:pattern:meta:validation
  - DEPENDS_ON:pattern:meta:metrics
```

---

## Composition/Integration (Meta)

**Pattern**: Robust links between agentic modules

**Meta**: Strongly typed edges, pattern compatibility

**Constraint**: Edge types validated on migration

### Example: Pattern Composition Validator

```python
class PatternCompositionValidator:
    """Validate pattern composition rules."""
    
    def __init__(self, graph):
        self.graph = graph
        self.rules = self.load_composition_rules()
    
    def validate_composition(self, pattern_ids):
        """Validate a set of patterns can be composed."""
        patterns = [self.graph.get_pattern(pid) for pid in pattern_ids]
        
        # Check for conflicts
        conflicts = self.check_conflicts(patterns)
        if conflicts:
            return CompositionResult(
                valid=False,
                error="Pattern conflicts detected",
                conflicts=conflicts
            )
        
        # Check dependencies satisfied
        missing = self.check_dependencies(patterns)
        if missing:
            return CompositionResult(
                valid=False,
                error="Missing dependencies",
                missing=missing
            )
        
        # Check composition rules
        violations = self.check_rules(patterns)
        if violations:
            return CompositionResult(
                valid=False,
                error="Composition rule violations",
                violations=violations
            )
        
        return CompositionResult(valid=True)
    
    def check_conflicts(self, patterns):
        """Check for CONFLICTS_WITH edges."""
        conflicts = []
        for i, p1 in enumerate(patterns):
            for p2 in patterns[i+1:]:
                if self.graph.has_edge(p1.id, p2.id, "CONFLICTS_WITH"):
                    conflicts.append((p1.id, p2.id))
        return conflicts
    
    def check_dependencies(self, patterns):
        """Check all dependencies are included."""
        pattern_ids = {p.id for p in patterns}
        missing = []
        
        for pattern in patterns:
            deps = self.graph.get_dependencies(pattern.id)
            for dep in deps:
                if dep.id not in pattern_ids:
                    missing.append((pattern.id, dep.id))
        
        return missing
    
    def check_rules(self, patterns):
        """Check composition rules (AND/OR/XOR)."""
        violations = []
        # Implement rule checking logic
        return violations

# Usage
validator = PatternCompositionValidator(graph)
result = validator.validate_composition([
    "pattern:behavioral:observer",
    "pattern:structural:facade",
    "pattern:meta:validation"
])

if not result.valid:
    raise CompositionError(result.error, result.conflicts)
```

**Graph Representation**:
```yaml
id: pattern:meta:composition:validator
name: Pattern Composition Validator
relationships:
  - EXTENDS:pattern:meta:composition
  - VALIDATES:pattern:meta:composition
  - DEPENDS_ON:pattern:meta:validation
  - USES:pattern:structural:graph-traversal
constraints:
  - "All CONFLICTS_WITH edges must be respected"
  - "All DEPENDS_ON edges must be satisfied"
  - "Composition rules (AND/OR/XOR) must be validated"
```

---

## Summary

All patterns now include:
1. Concrete code examples
2. Usage in CE framework context
3. Graph representation with relationships
4. Validation and integration guidance

These patterns form the foundation for the graph-based CE framework meta-repository and enable rapid PRP generation and execution in Claude Code.
