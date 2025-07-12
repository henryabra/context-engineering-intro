# PRP Template - Product Requirements Prompt

## 📋 Feature Overview

### Goal
[What needs to be built - be specific about the end state and user-visible behavior]

### Business Value
- [Primary user/business problem this solves]
- [Integration with existing features/workflows]
- [Success metrics and impact measurement]

### Success Criteria
- [ ] [Specific, measurable outcomes]
- [ ] [Performance/quality benchmarks]
- [ ] [User acceptance criteria]

---

## 🔬 Research Context & Documentation

### Technology Stack
**Exact versions researched and confirmed:**
- [Primary Technology]: [exact version] - [key capabilities used]
- [Framework/Library]: [exact version] - [specific features needed]
- [External Services]: [service name/version] - [integration requirements]

### Documentation Sources
**All sources researched (30-100+ pages minimum):**
```yaml
# Core Technology Documentation
- url: [Official API documentation URL]
  sections: [Specific sections: Authentication, Rate Limits, etc.]
  key_insights: [Critical findings that impact implementation]
  
- url: [Framework documentation URL]
  sections: [Components, Hooks, Best Practices, etc.]
  patterns: [Code patterns to follow from examples]
  
- url: [Third-party service documentation]
  sections: [Integration guides, SDK usage, error handling]
  gotchas: [Common pitfalls and limitations discovered]
```

### Research Stored in `/research/`
- `/research/[technology]/api-reference.md` - [Key API methods and parameters]
- `/research/[technology]/examples.md` - [Working code examples]
- `/research/[technology]/best-practices.md` - [Performance and security patterns]

### Codebase Analysis
**Current project structure:**
```bash
# Current relevant files and patterns
[project-root]/
├── src/[relevant-modules]/
├── tests/[test-patterns]/
├── config/[configuration-files]/
└── docs/[existing-documentation]/
```

**Existing patterns to follow:**
- [File naming conventions]
- [Code organization patterns]
- [Testing approaches used]
- [Configuration management]
- [Error handling strategies]

### Critical Gotchas & Library Quirks
```
# CRITICAL: [Specific library requirements and limitations]
# Example: Framework requires async/await pattern for all endpoints
# Example: ORM doesn't support batch operations over 1000 records
# Example: Rate limiting: API allows max 10 requests/second
# Example: Authentication tokens expire after 1 hour
# Example: Memory management: Framework uses garbage collection, avoid circular references
```

---

## 🏗️ Implementation Blueprint

### Architecture Overview
**Component interaction and data flow:**
```
[User Request] → [API Layer] → [Business Logic] → [Data Layer] → [External Services]
     ↓              ↓              ↓             ↓            ↓
[Response] ← [Validation] ← [Processing] ← [Storage] ← [Integration]
```

### File Structure Plan
**Files to create/modify with specific responsibilities:**
```bash
# Files to CREATE
src/[module]/
├── [module-entry]       # Module exports and public API
├── models.[ext]         # Data models and validation schemas
├── service.[ext]        # Business logic and external integrations
├── handlers.[ext]       # Request/response handling
└── exceptions.[ext]     # Custom exceptions for this feature

# Files to MODIFY
src/config/settings.[ext]   # Add feature configuration
src/api/routes.[ext]        # Register new endpoints
src/database/models.[ext]   # Add new database models
tests/                      # Add comprehensive test coverage
```

### Implementation Sequence
**Tasks in execution order with dependencies:**

#### Phase 1: Core Infrastructure
1. **Create data models**
   - Define schema validation with exact field types
   - Implement business validation rules
   - Set up database relationships if needed

2. **Implement service layer**
   - Core business logic with error handling
   - External API integration patterns
   - Data transformation and validation

3. **Add API endpoints**
   - Request/response handlers
   - Input validation and sanitization
   - Error response formatting

#### Phase 2: Integration & Testing
4. **Database integration**
   - Migration scripts for schema changes
   - Index creation for performance
   - Connection pooling configuration

5. **Configuration setup**
   - Environment variables and defaults
   - Feature flags and toggles
   - Logging configuration

6. **Testing & validation**
   - Unit tests for all components
   - Integration tests for API endpoints
   - Error case testing

### Detailed Implementation Steps

#### Step 1: Data Models
```[language]
// src/[module]/models.[ext]
// Based on research patterns from [specific documentation]

class/struct [ModelName] {
    // PATTERN: Follow existing model structure from src/models/
    // CRITICAL: Use exact field types from API documentation
    [field_type] field_name {
        // Required field with validation
        // Description: [Purpose from API docs]
        // Example: [Example from documentation]
    }
    
    // VALIDATION: Custom validators based on API constraints
    function validate_field(value) {
        // PATTERN: Follow validation patterns from existing models
        // GOTCHA: [Specific validation rule from research]
        return validated_value
    }
}
```

#### Step 2: Service Layer
```[language]
// src/[module]/service.[ext]
// Integration patterns from researched documentation

class [ServiceName] {
    constructor(config: Config) {
        // PATTERN: Dependency injection like existing services
        // CRITICAL: Connection pooling/rate limiting from research
    }
    
    async function process_request(data: [ModelName]) -> [ResponseType] {
        // SEQUENCE: Validation → Processing → External calls → Response
        // ERROR HANDLING: Based on researched error patterns
        // RETRY LOGIC: Follow patterns from existing services
    }
}
```

#### Step 3: API Integration
```[language]
// src/api/[module]_routes.[ext]
// Following existing route patterns

[route_decorator]("/[endpoint]")
async function [endpoint_name](
    request: [RequestModel],
    // PATTERN: Use existing dependency patterns
    service: [ServiceName] = get_service()
) -> [ResponseModel] {
    // VALIDATION: Request validation using researched patterns
    // PROCESSING: Service layer integration
    // RESPONSE: Standardized response format
}
```

### Integration Points
**System connections and dependencies:**

```yaml
DATABASE:
  - migrations: [List specific migrations needed]
  - indexes: [Performance indexes from research]
  - constraints: [Data integrity rules]

EXTERNAL_APIS:
  - authentication: [Method from API documentation]
  - rate_limiting: [Limits discovered in research]
  - error_handling: [Patterns from API docs]

CONFIGURATION:
  - environment_variables: [List all required config]
  - feature_flags: [Toggle points for gradual rollout]
  - monitoring: [Metrics and logging setup]

TESTING:
  - unit_tests: [Coverage for each component]
  - integration_tests: [End-to-end scenarios]
  - error_scenarios: [Failure case validation]
```

---

## 🧪 Validation Gates

### Level 1: Syntax & Style Validation
**Executable commands for immediate feedback:**
```bash
# MUST run these first - fix all errors before proceeding
# Target ONLY the new/modified files - not entire codebase
[linting-command] [specific-files]        # e.g., eslint src/[module]/ --fix, rubocop src/[module]/, go fmt ./src/[module]
[type-checking-command] [specific-files]  # e.g., tsc --noEmit src/[module]/*.ts, flow check src/[module]/
[formatting-command] [specific-files]     # e.g., prettier --write src/[module]/, gofmt src/[module]/*.go

# Expected: Zero errors in changed files. If errors exist, read and fix before continuing.
```

### Level 2: Unit Testing
**Test scenarios covering all code paths:**

#### Expected Use Cases
```[language]
// test_[module]_happy_path.[ext]
function test_successful_request() {
    // Core functionality works with valid input
    // PATTERN: Use existing test fixtures and patterns
    // ASSERTION: Verify expected behavior from research
}

function test_data_validation() {
    // Input validation works correctly
    // PATTERN: Test boundary conditions from API docs
    // ASSERTION: Proper validation responses
}
```

#### Edge Cases
```[language]
// test_[module]_edge_cases.[ext]
function test_boundary_conditions() {
    // Handles edge cases from research
    // CASES: Based on limitations discovered in documentation
}

function test_concurrent_requests() {
    // Multiple requests handled correctly
    // PATTERN: Use existing concurrency test patterns
}
```

#### Failure Cases
```[language]
// test_[module]_failures.[ext]
function test_external_api_failure() {
    // Graceful handling of external service failures
    // MOCK: Based on error patterns from API documentation
    // ASSERTION: Proper error responses and logging
}

function test_invalid_authentication() {
    // Authentication failures handled properly
    // PATTERN: Use existing auth test patterns
}
```

**Test execution command:**
```bash
# Test ONLY the new feature/module - not entire repository
[test-command] [specific-test-path]  # e.g., npm test src/[module], go test ./src/[module], pytest tests/test_[module].py
# Expected: All feature-specific tests pass. If failing, analyze root cause and fix.
```

### Level 3: Integration Testing
**End-to-end validation with real system integration:**

```bash
# Start system dependencies
[startup-command]  # e.g., docker-compose up -d, npm run dev, go run main.go

# Run integration tests for this feature only
[integration-test-command] [feature-specific-path]  # e.g., npm run test:integration -- --grep "[feature]", go test ./tests/integration/[module]_test.go

# Manual verification
[manual-test-command]  # e.g., curl -X POST http://localhost:8000/api/feature

# Expected results based on research
# Success: [Expected response format]
# Error: [Expected error format]
```

## 🎯 Quality Assurance Checklist

### Implementation Completeness
- [ ] All researched patterns implemented correctly
- [ ] External API integration follows documented best practices
- [ ] Error handling covers all scenarios from research
- [ ] Configuration follows existing project patterns
- [ ] Security considerations from research addressed

### Testing Coverage
- [ ] Unit tests: Expected use, edge cases, failure scenarios for new feature only
- [ ] Integration tests: End-to-end functionality verified for new endpoints/components
- [ ] Error paths: All failure modes tested for new logic
- [ ] Performance: Meets criteria from research for new feature
- [ ] Security: Authentication/authorization tested for new endpoints/data access

### Code Quality
- [ ] Linting: All style checks pass for new/modified files
- [ ] Type checking: No type errors in new/modified files
- [ ] Documentation: Inline comments explain complex logic in new code
- [ ] Logging: Appropriate level and information for new functionality
- [ ] Configuration: All new values externalized properly

### Production Readiness
- [ ] Performance benchmarks met
- [ ] Error responses follow API standards
- [ ] Monitoring and observability implemented
- [ ] Deployment configuration updated
- [ ] Documentation updated where needed

---

## 🚨 Critical Success Factors

### Research Adherence
- **Technology specifications are sacred**: Use exact versions/models from requirements
- **Documentation patterns are law**: Follow researched best practices exactly
- **Existing codebase patterns**: Mirror established project conventions
- **API limitations respected**: Implement all constraints from research

### Implementation Quality
- **No assumptions**: All behavior based on researched documentation
- **Comprehensive error handling**: Cover all failure modes discovered
- **Testing thoroughness**: Validate expected use, edge cases, and failures
- **Integration safety**: Ensure compatibility with existing system

### Anti-Patterns to Avoid
- ❌ **Ignoring research**: Don't deviate from documented patterns
- ❌ **Skipping validation**: All gates must pass before completion
- ❌ **Hardcoding values**: Use configuration for all environment-specific values
- ❌ **Incomplete error handling**: Handle all error conditions from research
- ❌ **Breaking existing patterns**: Follow established project conventions

---

## 📊 Implementation Confidence Score

### One-Shot Implementation Success Rating: [X]/10

**Confidence Assessment:**
- **10/10**: Guaranteed success with comprehensive context and clear implementation path
- **8-9/10**: High confidence - minor clarification may be needed but success likely
- **6-7/10**: Good foundation - may require some iteration or additional research
- **4-5/10**: Moderate confidence - significant gaps exist that could cause issues
- **1-3/10**: Low confidence - major unknowns present, high risk of failure

### Confidence Factors:
**Strengths (+):**
- [ ] Exhaustive research completed (30-100+ pages documented)
- [ ] All critical technology versions and constraints identified
- [ ] Working code examples available from research
- [ ] Clear integration patterns established
- [ ] Comprehensive error handling strategies defined
- [ ] Validation gates provide immediate feedback loops
- [ ] Implementation blueprint includes detailed pseudocode
- [ ] All gotchas and limitations documented

**Risk Factors (-):**
- [ ] Missing critical documentation or examples
- [ ] Unclear integration points with existing system
- [ ] Complex authentication/authorization requirements
- [ ] Untested API combinations or edge cases
- [ ] Performance requirements not well-defined
- [ ] External dependencies with unknown reliability
- [ ] Deployment constraints not fully understood

### Justification:
[Explain the confidence rating based on research completeness, implementation clarity, and risk assessment. Target 8+ for production features.]

**Recommendation:**
- **Score 8+**: Proceed with implementation
- **Score 6-7**: Consider additional research or prototype first
- **Score <6**: Gather more context before implementation