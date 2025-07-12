# AI Development Workflow Instructions

> **Note**: This file contains instructions for AI behavior during development. For user setup instructions, see `QUICKSTART.md`.

## 🎯 Core AI Behavior

### Conversation Initialization Protocol
1. **Start of conversation**: Read `PLANNING.md` → Check `TASK.md` → Read requirements (`PRD.md` or `INITIAL.md`)
2. **Codebase analysis**: Map existing patterns, technologies, and conventions → Identify implementation gaps
3. **Targeted research**: Research only the gaps found in codebase analysis → Store in `/research/` → Reference during implementation
4. **Development phase**: Create Phase 1 (skeleton) → Test → Create Phase 2 (production) → Test
5. **Task tracking**: Update `TASK.md` after each subtask → Document discoveries → Mark completions

### Requirements File Priority
- **First check for `PRD.md`** - Product Requirements Document with detailed specifications
- **If no PRD.md, use `INITIAL.md`** - Initial requirements template
- Both follow the same structure but PRD.md typically contains more detailed requirements

## 🔄 Project Awareness & Research

### Codebase-First Development
- **Existing code is the primary source of truth** - Always analyze current codebase patterns and conventions first
- **Gap-driven research** - Only research external documentation for technologies/patterns not found in codebase
- **Your knowledge is outdated** - When external research is needed, use freshly scraped documentation
- **Never assume or use pre-trained knowledge** about third-party libraries/APIs
- **Take specified technologies as sacred** - Research exact versions/models mentioned in requirements file (`PRD.md` or `INITIAL.md`)

### Research Workflow
1. **Read requirements file** (`PRD.md` or `INITIAL.md`) for technology specifications and feature requirements
2. **Analyze existing codebase** comprehensively:
   - Map file structure, naming conventions, and architectural patterns
   - Identify what technologies are already integrated and how
   - Find similar existing implementations to learn from
   - Discover testing, validation, and configuration approaches
   - Note coding standards and best practices in use
3. **Identify research gaps**: Compare requirements against existing codebase to determine what external research is needed
4. **Targeted external research** (only for identified gaps):
   - Use Jina MCP to scrape specific documentation needed for gaps
   - If Jina MCP is unavailable, use Claude's default web browsing capabilities
   - Focus on integration patterns rather than comprehensive overviews
   - **Critical**: Research gaps "to the point where it's absolutely ridiculous how much research you've done"
5. **Store research systematically**:
   ```
   /research/
   ├── openai/
   │   ├── api-reference.md
   │   ├── models.md
   │   └── authentication.md
   └── react/
       ├── hooks.md
       └── components.md
   ```
6. **Handle failed scrapes**: Retry with alternative URLs or search for correct pages
7. **Reference during implementation**: Always check existing codebase patterns first, then `/research/` for gaps

### PRP Research Standards
- **Codebase analysis first**: Thoroughly understand existing patterns before external research
- **Gap-focused research**: Research only technologies/patterns not found in existing codebase
- **Technology as sacred**: If specific models/versions are mentioned, research exactly those
- **Complete code examples**: Include working, production-ready code examples in research
- **Never assume**: Don't rely on pre-trained knowledge about third-party libraries/APIs
- **Build on existing patterns**: Prefer extending current approaches over introducing new ones

### Strategic Thinking
- **Use Ultrathink capabilities** when:
  - Deciding which documentation pages to scrape
  - Planning project architecture
  - Creating requirements documents
  - Solving complex implementation challenges

## 🧱 Code Structure & Modularity

### File Organization
- **500-line limit**: Split files exceeding this into logical modules
- **Module patterns**:
  ```
  /src/
  ├── core/           # Business logic
  ├── utils/          # Shared utilities
  ├── config/         # Configuration & constants
  ├── models/         # Data structures
  └── infrastructure/ # External service integrations
  ```

### Development Phases
- **Phase 1 - Working Skeleton**:
  - **Must compile and run successfully** - No syntax errors or import issues
  - **Core functionality implemented** - Basic happy path works end-to-end
  - **Test structure in place** - Tests are written but may fail for complex scenarios
  - **Focus on basic flow** - Get the main use case working first
  - **Minimal error handling** - Prevent crashes but don't handle all edge cases
  - **Simple UI** (if applicable) - Basic functionality without polish
  - Example: API endpoint that handles valid requests but may not validate all inputs
  
- **Phase 2 - Production Ready**:
  - **All tests pass** - Including edge cases and error scenarios
  - Complete feature implementation with comprehensive validation
  - Robust error handling and recovery mechanisms
  - Polished UI with all interactions and user experience enhancements
  - Performance optimization and monitoring
  - Example: Full API with input validation, auth, comprehensive error handling, logging, and monitoring

### Best Practices
- **Dynamic content**: Make everything configurable, avoid hardcoded examples
- **Clear imports**: Follow language conventions consistently
- **Environment variables**: Use appropriate management tools (dotenv, config files)
- **Separation of concerns**: Keep business logic separate from infrastructure

## 🧪 Testing & Reliability

### Three-Test Minimum
For every new feature, create:

1. **Expected Use Test**
   - Tests the happy path with valid inputs
   - Example: `test_user_can_login_with_valid_credentials()`

2. **Edge Case Test**
   - Tests boundary conditions or unusual scenarios
   - Example: `test_user_login_with_unicode_username()`

3. **Failure Case Test**
   - Tests error handling with invalid inputs
   - Example: `test_user_cannot_login_with_wrong_password()`

### Test Maintenance
- **After logic updates**: Review and update affected tests
- **Test location**: Mirror source structure in test directory
- **Test naming**: Use descriptive names explaining what is tested

## ✅ Task Management

### TASK.md Updates
**During development**:
- Update status immediately after completing subtasks
- Add discovered tasks under "Discovered During Work" section
- Include blockers or dependencies

### File References
- **PLANNING.md**: Architecture, conventions, constraints (read first)
- **TASK.md**: Current and completed tasks (update continuously)
- **PRD.md or INITIAL.md**: Requirements and specifications (check which exists)
- **phase-1.md / phase-2.md**: Specific requirements for each phase
- **PRPs/**: Generated Product Requirements Process files with detailed implementation plans

### Claude Code Commands Integration
- **`/generate-prp INITIAL.md`**: Creates comprehensive PRP files with exhaustive research
- **`/execute-prp PRPs/phase-1-feature.md`**: Implements Phase 1 following PRP specifications
- **`/execute-prp PRPs/phase-2-feature.md`**: Implements Phase 2 following PRP specifications

## 📎 Style & Documentation

### Code Standards
- **Language**: Use project's specified language from PLANNING.md or requirements file
- **Style guide**: Follow language's standard conventions
- **Linting**: Use appropriate tools for the language
- **Validation**: Implement proper data validation

### Documentation Requirements
- **Every public function/method**: Include language-appropriate documentation
- **Complex logic**: Add inline comments explaining "why" not "what"
- **README updates**: Keep current with new features and setup changes
- **Code clarity**: Write for mid-level developer comprehension

## 🧠 Development Rules

### Core Principles
1. **Ask when uncertain** - Never guess or assume missing context
2. **Verify before use** - Confirm file paths and modules exist
3. **Preserve existing code** - Only modify when explicitly instructed
4. **Use official sources** - Stick to official documentation only

### Efficiency Guidelines
- **Parallel operations**: Invoke multiple independent tools simultaneously
- **Codebase analysis first**: Understand existing patterns before external research
- **Batch research**: Scrape related documentation pages together for identified gaps
- **Reuse research**: Reference existing `/research/` content before new scrapes
- **Leverage existing code**: Build on current implementations rather than starting from scratch

## 🔄 PRP (Product Requirements Process) Integration

### When to Use PRP Commands
- **Complex features**: Multi-step implementations requiring detailed planning
- **New technology**: When working with unfamiliar APIs or frameworks
- **Production systems**: Features requiring comprehensive validation and testing
- **Team collaboration**: When implementation plans need to be shared or reviewed

### PRP Workflow Benefits
- **One-pass implementation**: Comprehensive context enables successful first-attempt implementation
- **Exhaustive research**: Prevents assumptions and ensures current documentation usage
- **Validation gates**: Built-in quality checks and testing procedures
- **Standardized approach**: Consistent implementation patterns across projects

### PRP Quality Standards
- **Research depth**: "Absolutely ridiculous" amount of research with 30-100+ pages
- **Implementation blueprint**: Detailed pseudocode and real file references
- **Error handling**: Comprehensive strategy for failure cases
- **Validation commands**: Executable commands for syntax, style, and functional testing

---

**Remember**: This workflow prioritizes accuracy through research, maintainability through structure, and reliability through testing. For complex features, use PRP commands to ensure comprehensive planning and one-pass implementation success.