# Generate Product Requirements Prompt (PRP)

## Overview
Generate comprehensive Product Requirements Prompt documents that enable one-pass implementation success through exhaustive research and detailed planning.

## Arguments
**Feature file**: `$ARGUMENTS` (typically `INITIAL.md` or `PRD.md`)

## 🔍 Research Phase (Critical)

### 1. Requirements Analysis
- **Read the feature file completely** to understand scope and requirements
- **Identify all technologies, models, and versions** mentioned as sacred specifications
- **Extract all documentation URLs** provided in the DOCUMENTATION section
- **Note specific examples** referenced in the EXAMPLES section

**🔍 Gap Analysis**: Only interact with user if critical information is missing:
- **Missing technology versions**: If specific versions aren't specified
- **Ambiguous requirements**: If feature descriptions lack clarity
- **Incomplete documentation**: If essential documentation URLs are missing

### 2. Comprehensive Codebase Analysis
**Analysis Standards**: Understand existing patterns to the point where you know exactly how to integrate new features

- **Read PLANNING.md first** to understand architecture, conventions, and constraints
- **Map file structure** and architectural patterns currently in use
- **Identify existing technologies** and their integration patterns
- **Find similar implementations** in the codebase to learn from
- **Discover testing patterns** and validation approaches used
- **Note configuration patterns** and environment setup
- **Understand naming conventions** and coding standards
- **Check build/deployment processes** and tooling

**🔍 Gap Analysis**: Only interact with user if conflicts are found:
- **Conflicting patterns**: If multiple incompatible approaches exist in codebase
- **Missing validation commands**: If no testing/linting commands are discoverable
- **Unclear integration**: If existing patterns don't clearly apply to new feature

### 3. Gap Identification
**Compare requirements against existing codebase to identify what external research is needed:**

- **Missing technologies**: Technologies mentioned in requirements but not found in codebase
- **Integration gaps**: How to connect new technologies with existing patterns
- **Pattern gaps**: Implementation approaches not represented in current codebase
- **Validation gaps**: Testing or quality assurance approaches not currently used

### 4. Targeted External Research
**Research Standards**: For identified gaps, research to the point where it's "absolutely ridiculous how much research you've done"

- **Use Jina MCP** to scrape documentation for gap-identified technologies only
- **Focus on integration patterns** rather than comprehensive overviews
- **Research exact versions/models** specified (treat as sacred truth)
- **Target specific documentation** that addresses the identified gaps
- **Store research systematically** in `/research/` directory:
  ```
  /research/
  ├── [technology-name]/
  │   ├── api-reference.md
  │   ├── getting-started.md
  │   ├── examples.md
  │   └── best-practices.md
  ```

### 5. Implementation Pattern Research
- **Combine codebase patterns with external research** for gap areas
- **Find working code examples** for each technology combination not in codebase
- **Research best practices** and common pitfalls for new technologies
- **Identify error handling patterns** for the specific technologies
- **Document integration requirements** between existing and new components
- **Plan minimal changes** that build on existing patterns

## 🧠 Strategic Planning (Ultrathink)

**Before writing the PRP, engage deep strategic thinking:**

1. **Architecture decisions**: How do components interact?
2. **Implementation sequence**: What order ensures success?
3. **Risk assessment**: What could go wrong and how to prevent it?
4. **Validation strategy**: How to verify each component works?
5. **Context completeness**: What would another AI need to succeed?

**🔍 Gap Analysis**: Only interact with user if architectural decisions are unclear:
- **Multiple viable approaches**: If research reveals equally valid architectural options
- **High-risk decisions**: If implementation choices could significantly impact the system
- **Insufficient context**: If requirements don't provide enough detail for critical decisions

## 📋 PRP Generation

### Phase Structure
Generate **two separate PRP files**:

**Phase 1**: `PRPs/phase-1-[feature-name].md` - **Working Skeleton**
- **Must compile and run successfully** - All syntax correct, imports resolved
- **Core functionality implemented** - Basic happy path works end-to-end
- **Test structure in place** - Tests are written but may fail for complex scenarios
- **Focus on reducing AI cognitive load** - Implement the basic flow without edge cases
- **Minimal error handling** - Prevent crashes but don't handle all scenarios
- **Detailed implementation comments** explaining what Phase 2 needs to complete
- **Working integration points** - Components connect and communicate properly

**Phase 2**: `PRPs/phase-2-[feature-name].md` - **Production Ready**
- **All tests must pass** - Including edge cases and complex scenarios
- Complete feature implementation with comprehensive validation
- Robust error handling and recovery mechanisms
- Full test suite (expected use, edge cases, failure cases)
- Performance optimization and monitoring
- Advanced features and user experience enhancements

### Incremental Implementation Support
**Target for `/execute-prp --focus` compatibility:**
- **Clear section headers** - Use descriptive headers that can be targeted with --focus parameter
- **Logical section boundaries** - Ensure sections can be implemented independently when possible
- **Phase numbering** - Include phase numbers in headers for easy wildcard targeting (e.g., "*Phase 1*")
- **Dependency documentation** - Note when sections depend on others for proper sequencing

### Required PRP Sections

#### 1. Context & Research Summary
- **Codebase analysis**: Existing patterns, technologies, and conventions found
- **Technology stack**: Exact versions and models (existing + new)
- **Gap analysis**: What external research was needed and why
- **Documentation sources**: URLs with specific sections referenced for gaps
- **Key insights**: Critical findings from codebase analysis and gap research
- **Integration strategy**: How new features will build on existing patterns

#### 2. Implementation Blueprint
- **Pseudocode outline**: Step-by-step implementation approach
- **File structure**: Specific files to create/modify with rationale
- **Dependencies**: External libraries and their integration points
- **Configuration**: Environment variables and setup requirements

#### 3. Detailed Implementation Plan
- **Task sequence**: Ordered list of implementation steps
- **Code examples**: Working snippets from research for each major component
- **Integration points**: How components connect and communicate
- **Error handling**: Specific strategies for each failure mode

#### 4. Validation Gates
**Must be executable commands** appropriate for the project:

**Phase 1 Validation** (focus on compilation and basic flow):
```bash
# Compilation/Syntax Check (MUST PASS)
# Example for Python: python -m py_compile src/*.py
# Example for Node.js: npx tsc --noEmit
# Example for general: make build

# Basic smoke test (SHOULD PASS - verify basic instantiation/connectivity)
# Example for Python: python -c "import mymodule; mymodule.init()"
# Example for Node.js: npm run test:smoke
# Example for general: make test-smoke

# Full test suite (MAY FAIL - run to see what Phase 2 needs to fix)
# Example for Python: uv run pytest tests/ -v || true
# Example for Node.js: npm test || true
# Note: Use || true to prevent CI failure, but review failed tests
```

**Phase 2 Validation** (comprehensive):
```bash
# Full test suite
# Example for Python: uv run pytest tests/ -v --cov
# Example for Node.js: npm test
# Example for general: make test-all

# Performance/Integration tests
# Example for Python: uv run pytest tests/integration/ -v
# Example for Node.js: npm run test:integration
```

**🔍 Gap Analysis**: Only interact with user if validation is unclear:
- **No discoverable commands**: If project lacks clear testing/validation setup
- **Custom validation needed**: If feature requires specialized testing not found in codebase

#### 5. Quality Assurance
- **Test coverage**: Specific test cases for each feature
- **Performance criteria**: Response time and resource usage targets
- **Security considerations**: Data handling and API security measures
- **Monitoring**: How to verify the implementation works in production

## 📁 Output Requirements

### File Naming
- `PRPs/phase-1-[descriptive-feature-name].md`
- `PRPs/phase-2-[descriptive-feature-name].md`

### Content Standards
- **Complete context**: Everything needed for successful implementation
- **Working code examples**: Production-ready snippets from research
- **Executable validation**: Commands that can be run to verify success
- **Clear implementation path**: Step-by-step instructions with rationale

## ✅ Quality Checklist

Before finalizing each PRP, verify:

**General Requirements:**
- [ ] **Codebase understanding**: Existing patterns and conventions thoroughly analyzed
- [ ] **Gap identification**: Clear understanding of what external research was needed
- [ ] **Research completeness**: Sufficient documentation researched for identified gaps
- [ ] **Technology accuracy**: Exact versions/models specified and researched
- [ ] **Implementation clarity**: Clear step-by-step instructions
- [ ] **Code examples**: Working snippets for each major component
- [ ] **Context completeness**: Another AI could implement successfully
- [ ] **Codebase alignment**: Builds on existing patterns and conventions

**Phase 1 Specific Requirements:**
- [ ] **Compilation guarantee**: Implementation must compile/build without errors
- [ ] **Basic functionality**: Core happy path works end-to-end
- [ ] **Test structure**: Tests are written (may fail for complex cases)
- [ ] **Reduced cognitive load**: Focus on getting basic flow working
- [ ] **Integration readiness**: Components connect properly with existing codebase

**Phase 2 Specific Requirements:**
- [ ] **All tests pass**: Including edge cases and complex scenarios
- [ ] **Production readiness**: Comprehensive error handling and validation
- [ ] **Performance optimization**: Meets performance criteria and monitoring
- [ ] **Full test coverage**: Complete test suite with all scenarios

## 📊 Success Metrics

**Rate each PRP on confidence for one-pass implementation (1-10 scale):**
- **10**: Guaranteed success with comprehensive context
- **8-9**: High confidence with minor clarification potentially needed
- **6-7**: Good foundation but may require iteration
- **Below 6**: Requires more research and context

**Target**: Every PRP should score 8+ for one-pass implementation success.

**🔍 Final Gap Check**: Only interact with user if confidence is low:
- **Confidence score below 7**: If PRP lacks sufficient context for reliable implementation
- **Critical unknowns**: If essential implementation details remain unclear after research

## 🎯 Remember

The goal is **one-pass implementation success** through:
- Comprehensive codebase analysis that reveals existing patterns
- Targeted research that fills only the identified gaps
- Complete context that enables autonomous implementation
- Validated approaches that prevent common pitfalls
- Clear instructions that guide successful execution
- **Gap-driven clarification** only when essential information is missing

## 💡 Gap Identification Guidelines

- **Prefer inference over interaction**: Use research and codebase analysis to fill gaps
- **Only ask when blocking**: User interaction should be last resort for critical unknowns
- **Be specific**: When asking, provide context about what's missing and why it's needed
- **Offer researched options**: Present alternatives discovered through research rather than open-ended questions