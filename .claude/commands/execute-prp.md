# Execute PRP

Implement a feature using a comprehensive Product Requirements Prompt (PRP) file.

## Arguments
**PRP File**: `$ARGUMENTS` (e.g., `PRPs/phase-1-user-auth.md`)

## 🚀 Execution Process

### 1. **Load & Analyze PRP**
- **Read PRP completely**: Load the specified PRP file and all referenced research
- **Understand context**: Review all technology specifications, constraints, and requirements
- **Analyze codebase patterns**: Ensure understanding of existing patterns referenced in PRP
- **Verify research**: Check `/research/` directory for referenced documentation
- **Extend research if needed**: Perform additional web searches only for missing context not covered by codebase analysis
- **Confirm readiness**: Ensure all dependencies and prerequisites are understood

### 2. **Strategic Planning (Ultrathink)**
**Deep strategic thinking before implementation:**
- **Architecture review**: Understand how components interact and integrate
- **Implementation sequence**: Plan optimal order of development steps
- **Risk assessment**: Identify potential blockers and mitigation strategies
- **Resource check**: Verify all required tools, libraries, and services are available

**Task Management:**
- **Use TodoWrite tool**: Create detailed implementation plan with specific tasks
- **Break down complexity**: Split large features into manageable, testable components
- **Follow PRP structure**: Align todos with the PRP's implementation blueprint
- **Track progress**: Update task status throughout implementation

### 3. **Implementation Execution**
- **Follow PRP blueprint**: Implement according to the detailed plan and pseudocode
- **Prioritize existing patterns**: Build on existing codebase patterns first, then use external research for gaps
- **Maintain codebase standards**: Follow existing file structure and coding conventions
- **Implement incrementally**: Build and test components in logical sequence
- **Handle errors proactively**: Use error handling strategies outlined in PRP

### 4. **Validation & Testing**
- **Phase 1 validation priority**: Ensure compilation and basic functionality work
- **Run validation gates**: Execute all commands specified in PRP's validation section
- **Test systematically**: Run all tests to understand what Phase 2 needs to complete
- **Phase 1 allows failing tests**: Complex test scenarios may fail - this is expected
- **Fix compilation errors only**: Focus on making code compile and basic flow work
- **Verify integration**: Ensure new features connect properly with existing codebase
- **Document failing tests**: Note which tests fail for Phase 2 to address
- **Compilation verification**: Confirm code builds/compiles without errors

### 5. **Quality Assurance**
- **Complete checklist review**: Verify all PRP requirements are implemented
- **Run final validation suite**: Execute comprehensive test and lint commands
- **Performance verification**: Check that implementation meets performance criteria
- **Security review**: Ensure security considerations from PRP are addressed
- **Documentation update**: Update any relevant documentation if specified

### 6. **Completion & Verification**
- **Final PRP review**: Re-read PRP to confirm nothing was missed
- **Success criteria check**: Verify all success criteria from original requirements are met
- **Clean up**: Remove temporary files and organize code structure
- **Report status**: Provide clear completion summary with any notes or observations

## 🔧 Implementation Guidelines

### Code Quality Standards
- **Follow PRP specifications exactly**: Treat technology versions and patterns as sacred
- **Prioritize codebase patterns**: Use existing patterns as primary reference, then PRP research for gaps
- **Maintain consistency**: Follow established codebase patterns and conventions
- **Write production-ready code**: Implement comprehensive error handling and validation

### Error Handling Strategy
- **Use PRP error patterns**: Apply specific failure handling strategies from PRP
- **Fail gracefully**: Implement proper error messages and recovery mechanisms
- **Log appropriately**: Add logging that aligns with existing codebase patterns
- **Test error paths**: Verify error handling works as expected

### Integration Best Practices
- **Respect existing architecture**: Build on current patterns rather than introducing new ones
- **Leverage existing code**: Extend current implementations when possible
- **Test integration points**: Verify new code works with existing components
- **Follow naming conventions**: Use consistent naming that matches codebase standards
- **Document integration**: Add comments explaining how new features connect to existing code

## 🎯 Success Criteria

### Implementation Success
- [ ] All PRP requirements implemented completely
- [ ] **Phase 1**: Code compiles and builds without errors
- [ ] **Phase 1**: Basic happy path functionality works end-to-end
- [ ] **Phase 1**: Test structure in place (tests may fail for complex cases)
- [ ] **Phase 2**: All tests pass including edge cases
- [ ] All validation gates pass successfully (Phase 2)
- [ ] Code follows established patterns and conventions
- [ ] Error handling is comprehensive and tested (Phase 2)
- [ ] Integration with existing codebase is seamless

### Quality Assurance
- [ ] Tests cover expected use, edge cases, and failure scenarios
- [ ] Performance meets or exceeds PRP criteria
- [ ] Security considerations are properly addressed
- [ ] Documentation is updated where specified
- [ ] Code is production-ready and maintainable

## 💡 Key Reminders

- **PRP as single source of truth**: All implementation decisions should reference PRP context
- **Codebase patterns first**: Use existing patterns as primary reference, then PRP research for gaps
- **Phase 1 reduces cognitive load**: Focus on compilation and basic flow, tests may fail
- **Phase 2 completes the implementation**: All tests pass and edge cases are handled
- **Research over assumptions**: Use stored documentation rather than pre-trained knowledge
- **Validation is contextual**: Phase 1 validates compilation/basic flow, Phase 2 validates completeness
- **Incremental progress**: Build skeleton first, then complete implementation
- **Quality over speed**: Two phases increase success rate by reducing complexity