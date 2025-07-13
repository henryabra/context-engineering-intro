# Execute PRP

Implement a feature using a comprehensive Product Requirements Prompt (PRP) file with optional section targeting.

## Arguments
**PRP File**: `$ARGUMENTS` (e.g., `PRPs/phase-1-user-auth.md`)

**Optional Focus Parameter**: `--focus="section1,section2"` (target specific sections)

## Usage Examples

```bash
# Execute entire PRP
/execute-prp PRPs/phase-1-feature.md

# Focus on specific sections
/execute-prp PRPs/phase-1-feature.md --focus="Database Schema Changes,Model Class Updates"

# Focus on single section
/execute-prp PRPs/phase-1-feature.md --focus="Phase 1 Database Migration"

# Focus using pattern matching
/execute-prp PRPs/phase-1-feature.md --focus="*Phase 1*,*Database*"
```

## 🎯 Focus Parameter Benefits

### **Incremental Implementation**
- Target specific phases for safe deployment
- Implement complex PRPs in controlled stages
- Reduce cognitive load by focusing on subset

### **Team Coordination** 
- Different team members can work on different sections
- Clear separation of database vs code vs testing changes
- Parallel development of independent components

### **Risk Reduction**
- Test each section independently
- Incremental validation and rollback capability
- Smaller, focused commits and code reviews

## 🚀 Execution Process

### 1. **Load & Analyze PRP**
- **Read PRP completely**: Load the specified PRP file and all referenced research
- **Parse focus parameter**: If `--focus` specified, identify target sections using header matching
- **Section filtering**: Extract only the specified sections for implementation (if focused)
- **Dependency analysis**: Ensure focused sections have necessary context from other sections
- **Understand context**: Review all technology specifications, constraints, and requirements
- **Analyze codebase patterns**: Ensure understanding of existing patterns referenced in PRP
- **Verify research**: Check `/research/` directory for referenced documentation
- **Extend research if needed**: Perform additional web searches only for missing context not covered by codebase analysis
- **Confirm readiness**: Ensure all dependencies and prerequisites are understood

### 2. **Strategic Planning (Ultrathink)**
**Deep strategic thinking before implementation:**
- **Focus scope analysis**: If focused, understand how target sections interact with rest of PRP
- **Architecture review**: Understand how components interact and integrate
- **Implementation sequence**: Plan optimal order of development steps for focused sections
- **Dependency mapping**: Identify prerequisites and dependencies for focused sections
- **Risk assessment**: Identify potential blockers and mitigation strategies
- **Resource check**: Verify all required tools, libraries, and services are available

**Task Management:**
- **Use TodoWrite tool**: Create implementation plan specific to focused sections (or full PRP)
- **Scope todos appropriately**: Only include tasks relevant to focus areas (if focused)
- **Break down complexity**: Split large features into manageable, testable components
- **Follow PRP structure**: Align todos with the PRP's implementation blueprint
- **Cross-reference dependencies**: Note what future sections will need to complete (if focused)
- **Track progress**: Update task status throughout implementation

### 3. **Implementation Execution**
- **Section-specific implementation**: If focused, implement only the sections specified in focus parameter
- **Follow PRP blueprint**: Implement according to the detailed plan and pseudocode
- **Context preservation**: Maintain awareness of full PRP context while implementing focused sections
- **Prioritize existing patterns**: Build on existing codebase patterns first, then use external research for gaps
- **Maintain codebase standards**: Follow existing file structure and coding conventions
- **Implement incrementally**: Build and test components in logical sequence
- **Interface compatibility**: Ensure focused implementation is compatible with future sections
- **Handle errors proactively**: Use error handling strategies outlined in PRP

### 4. **Validation & Testing**
- **Section-specific validation**: If focused, run only validation commands relevant to implemented sections
- **Phase 1 validation priority**: Ensure compilation and basic functionality work
- **Run validation gates**: Execute validation commands specified in PRP's validation section
- **Integration point testing**: Test interfaces between focused and unfocused sections
- **Test systematically**: Run all tests to understand what Phase 2 needs to complete
- **Phase 1 allows failing tests**: Complex test scenarios may fail - this is expected
- **Fix compilation errors only**: Focus on making code compile and basic flow work
- **Verify integration**: Ensure new features connect properly with existing codebase
- **Document failing tests**: Note which tests fail for Phase 2 to address
- **Compilation verification**: Confirm code builds/compiles without errors

### 5. **Quality Assurance**
- **Focused checklist review**: If focused, verify focused section requirements are implemented
- **Partial validation suite**: Execute validation commands relevant to implemented sections
- **Performance verification**: Check that implementation meets performance criteria
- **Security review**: Ensure security considerations from PRP are addressed
- **Future readiness**: Ensure implementation is ready for future section integration
- **Documentation update**: Update documentation relevant to implemented sections

### 6. **Completion & Verification**
- **Section completion report**: If focused, report on what was implemented vs what remains
- **Final PRP review**: Re-read PRP to confirm nothing was missed in focused sections
- **Success criteria check**: Verify focused section success criteria are met
- **Integration notes**: Document how future sections should integrate with current implementation
- **Clean up**: Remove temporary files and organize code structure
- **Dependency tracking**: List what future focused runs will need from current implementation
- **Report status**: Provide clear completion summary with any notes or observations

## 🔧 Implementation Guidelines

### Code Quality Standards
- **Follow PRP specifications exactly**: Treat technology versions and patterns as sacred
- **Prioritize codebase patterns**: Use existing patterns as primary reference, then PRP research for gaps
- **Maintain consistency**: Follow established codebase patterns and conventions
- **Write production-ready code**: Implement comprehensive error handling and validation
- **Context preservation**: If focused, understand full PRP context even when implementing subset
- **Interface planning**: Design focused sections to integrate with unfocused sections

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
- **Focused scope discipline**: If using --focus, only implement sections specified in focus parameter
- **Integration planning**: Design for future section integration when using focused implementation

## 🎯 Focus Parameter Implementation

### Focus Section Identification
- **Header matching**: Match section headers exactly (case-insensitive)
- **Wildcard support**: Use `*` for pattern matching in section names  
- **Comma separation**: Multiple sections separated by commas
- **Substring matching**: Partial header matches supported

### Focus Matching Examples
```bash
--focus="Database Schema"           # Exact match
--focus="*Phase 1*"                # Wildcard pattern  
--focus="Database,Model,Service"    # Multiple sections
--focus="Phase 1*,*Test*"          # Mixed patterns
```

### Section Extraction Logic
- Extract from matching header to next same-level header
- Include all subsections within matched section
- Preserve code blocks, examples, and validation commands
- Maintain section context and cross-references

### Header Detection Patterns
```regex
## (.+?)           # Level 2 headers
### (.+?)          # Level 3 headers  
#### (.+?)         # Level 4 headers
```