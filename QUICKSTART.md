# Context Engineering Quick Start Guide

## 🚀 Getting Started

### Step 1: Copy Framework Files to Your Project

Copy these essential files from this template to your working repository:

```bash
# Core workflow files
cp CLAUDE.md /path/to/your/project/
cp INITIAL.md /path/to/your/project/

# Create necessary directories
mkdir -p /path/to/your/project/examples
mkdir -p /path/to/your/project/PRPs
mkdir -p /path/to/your/project/research

# Copy Claude Code commands
cp -r .claude /path/to/your/project/

# Copy template files
cp -r PRPs/templates /path/to/your/project/PRPs/
```

### Step 2: Customize CLAUDE.md (Optional)
Edit `CLAUDE.md` in your project to add project-specific rules:
- Coding standards and style guides
- Framework preferences
- Testing requirements
- Security guidelines
- Project-specific constraints

### Step 3: Add Code Examples
Place relevant code examples in the `examples/` folder:
- API patterns your project uses
- Database models and schemas
- Testing patterns and fixtures
- Configuration patterns
- Any code the AI should mimic

## 📋 Development Workflow

### Option A: Direct Development
1. **Start**: Read `PLANNING.md` → Check `TASK.md` → Read requirements (`PRD.md` or `INITIAL.md`)
2. **Research**: AI scrapes documentation (30-100 pages) → Stores in `/research/`
3. **Development**: Create Phase 1 (skeleton) → Test → Create Phase 2 (production) → Test
4. **Tracking**: Update `TASK.md` after each subtask

### Option B: PRP-Driven Development (Recommended)
1. **Requirements**: Create detailed `INITIAL.md` or `PRD.md`
2. **Generate PRP**: Use `/generate-prp INITIAL.md` to create implementation plan
3. **Execute PRP**: Use `/execute-prp PRPs/phase-1-feature.md` and `/execute-prp PRPs/phase-2-feature.md`
4. **Validation**: Run automated checks from PRP validation gates

### Requirements File Priority
- **Check for `PRD.md` first** - Product Requirements Document with detailed specifications
- **Fall back to `INITIAL.md`** - Initial requirements template
- Both follow the same structure but PRD.md typically has more detail

## 🔧 Creating Your Feature Request

### Using INITIAL.md Template
Fill out `INITIAL.md` with your feature requirements:

```markdown
## FEATURE
Build a REST API for user authentication with JWT tokens

### Main Functionality
- User registration and login
- JWT token generation and validation
- Password hashing with bcrypt

### Success Criteria
- [ ] Users can register with email/password
- [ ] Users can login and receive JWT tokens
- [ ] Protected endpoints validate tokens

## EXAMPLES
- **Auth API**: examples/auth_api.py - Standard API structure
- **JWT Handler**: examples/jwt_handler.py - Token management patterns

## DOCUMENTATION
- **FastAPI**: https://fastapi.tiangolo.com/
- **JWT**: https://pyjwt.readthedocs.io/en/latest/
- **bcrypt**: https://passlib.readthedocs.io/en/stable/

## OTHER CONSIDERATIONS
### Technical Requirements
- Language: Python 3.9+
- Framework: FastAPI
- Database: PostgreSQL

### Security Considerations
- Use bcrypt for password hashing
- Implement refresh token rotation
- Add rate limiting for auth endpoints
```

## 🛠️ Using PRP Commands

### Generate Implementation Blueprint
```bash
/generate-prp INITIAL.md (or PRD.md)
```

This creates comprehensive implementation plans:
- `PRPs/phase-1-[feature].md` - Skeleton implementation
- `PRPs/phase-2-[feature].md` - Production-ready version

### Execute Implementation
```bash
# Implement skeleton version
/execute-prp PRPs/phase-1-[feature].md

# Implement production version
/execute-prp PRPs/phase-2-[feature].md
```

## 📁 Project Structure

After setup, your project should have:

```
your-project/
├── CLAUDE.md              # AI workflow instructions
├── INITIAL.md             # Feature requirements template
├── PLANNING.md            # Project architecture (optional)
├── TASK.md               # Task tracking (optional)
├── examples/             # Code examples for AI to follow
├── PRPs/                 # Generated implementation blueprints
├── research/             # AI-scraped documentation
└── .claude/              # Custom commands
    └── commands/
        ├── generate-prp.md
        └── execute-prp.md
```

## ✅ Task Management

### Using TASK.md
Create and update `TASK.md` for tracking:

```markdown
## [2024-01-10] Implement user authentication
- [ ] Research auth libraries in documentation
- [ ] Create Phase 1 skeleton with basic login
- [ ] Add tests for auth module
- [ ] Create Phase 2 with full auth features

### Discovered During Work
- [ ] Need to add password strength validation
- [ ] Consider adding 2FA support
```

**Update rules**:
- Mark completed tasks immediately
- Add discovered tasks under "Discovered During Work"
- Include blockers or dependencies

## 💡 Tips for Success

1. **More Examples = Better Results**: AI performs best with patterns to follow
2. **Be Specific in Requirements**: Don't assume the AI knows your preferences
3. **Use Documentation Links**: Provide 10-15 pages minimum per technology
4. **Specify Exact Versions**: Mention specific models/versions (e.g., "gpt-4-turbo-preview")
5. **Use Validation Gates**: PRPs include test commands ensuring working code
6. **Iterate on PRPs**: Generate and refine before execution

## 🎯 Common Use Cases

- **New Features**: Describe requirements, provide examples, get implementation
- **Refactoring**: Show current patterns, describe desired state
- **Bug Fixes**: Include error logs, expected behavior, relevant code
- **API Integration**: Provide API docs, show existing integration patterns
- **Testing**: Add test patterns to examples/, specify coverage requirements

## 🔄 Advanced Workflow

### For Complex Projects
1. **Phase 1**: Create basic skeleton with core functionality
2. **Phase 2**: Add production features (auth, validation, monitoring)
3. **Validation**: Three-test minimum (expected use, edge cases, failure cases)
4. **Integration**: Ensure compatibility with existing codebase

### File Organization Standards
- **500-line limit**: Split larger files into logical modules
- **Module patterns**: `/src/core/`, `/src/utils/`, `/src/config/`, `/src/models/`
- **Test structure**: Mirror source structure in test directory

## 🚀 Next Steps

1. **Start Small**: Test workflow with a simple feature
2. **Build Examples**: Accumulate code patterns over time
3. **Refine CLAUDE.md**: Update as you discover project patterns
4. **Use PRPs Consistently**: For all major features to ensure quality
5. **Validate Everything**: Run all PRP validation gates before completion