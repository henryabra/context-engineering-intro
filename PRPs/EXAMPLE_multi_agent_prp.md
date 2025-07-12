# PRP Template - Product Requirements Prompt

## 📋 Feature Overview

### Goal
Create a production-ready multi-agent system where users can research topics via CLI, and the Research Agent can delegate email drafting tasks to an Email Draft Agent. The system should support multiple LLM providers and handle API authentication securely.

### Business Value
- **Automation**: Reduces manual work for research-based email communications
- **Integration**: Demonstrates advanced Pydantic AI multi-agent patterns with external APIs
- **Productivity**: Streamlines research and email drafting workflows for users
- **Scalability**: Provides foundation for more complex multi-agent applications

### Success Criteria
- [ ] Research Agent successfully searches via Brave API and returns structured results
- [ ] Email Agent creates Gmail drafts with proper OAuth2 authentication
- [ ] Research Agent can invoke Email Agent as a tool with proper context passing
- [ ] CLI provides streaming responses with real-time tool visibility
- [ ] All validation gates pass and code meets production quality standards

---

## 🔬 Research Context & Documentation

### Technology Stack
**Exact versions researched and confirmed:**
- **Pydantic AI**: latest - Multi-agent system creation and tool registration
- **Python**: 3.9+ - Async/await support and type annotations
- **Gmail API**: v1 - OAuth2 authentication and draft creation
- **Brave Search API**: v1 - Web search with rate limiting
- **httpx**: latest - Async HTTP client for API calls

### Documentation Sources
**All sources researched (30-100+ pages minimum):**
```yaml
# Core Technology Documentation
- url: https://ai.pydantic.dev/agents/
  sections: [Agent creation, Tool registration, Dependencies]
  key_insights: [Agent-as-tool pattern, RunContext usage, async requirements]
  
- url: https://ai.pydantic.dev/multi-agent-applications/
  sections: [Multi-agent patterns, Token tracking, Context passing]
  patterns: [Agent composition, Usage tracking, Dependency injection]
  
- url: https://developers.google.com/gmail/api/guides/sending
  sections: [OAuth2 flow, Draft creation, MIME formatting]
  gotchas: [Browser-based auth, Token refresh, Base64 encoding]

- url: https://api-dashboard.search.brave.com/app/documentation
  sections: [REST endpoints, Authentication, Rate limits]
  gotchas: [2000 requests/month limit, X-Subscription-Token header]
```

### Research Stored in `/research/`
- `/research/pydantic-ai/agents.md` - Agent creation patterns and tool registration
- `/research/pydantic-ai/multi-agent.md` - Multi-agent composition and context passing
- `/research/gmail/api-reference.md` - OAuth2 flow and draft creation methods
- `/research/brave/search-api.md` - Search endpoints and rate limiting details

### Codebase Analysis
**Current project structure:**
```bash
# Current relevant files and patterns
context-engineering-intro/
├── examples/
│   ├── agent/
│   │   ├── agent.py          # Agent creation patterns
│   │   ├── providers.py      # LLM provider configuration
│   │   └── tools.py          # Tool registration examples
│   └── cli.py               # CLI streaming patterns
├── PRPs/
└── requirements.txt
```

**Existing patterns to follow:**
- **Agent creation**: Use `Agent` class with `deps_type` parameter
- **Tool registration**: Use `@agent.tool` decorator with async functions
- **CLI streaming**: Use `agent.run_stream()` with tool visibility
- **Error handling**: Structured exceptions with proper logging
- **Configuration**: Environment variables with pydantic-settings

### Critical Gotchas & Library Quirks
```
# CRITICAL: Pydantic AI requires async throughout - no sync functions in async context
# CRITICAL: Gmail API requires OAuth2 flow on first run - credentials.json needed
# CRITICAL: Brave API has rate limits - 2000 requests/month on free tier
# CRITICAL: Agent-as-tool pattern requires passing ctx.usage for token tracking
# CRITICAL: Gmail drafts need base64 encoding with proper MIME formatting
# CRITICAL: Always use absolute imports for cleaner code structure
# CRITICAL: Store sensitive credentials in .env, never commit API keys
```

---

## 🏗️ Implementation Blueprint

### Architecture Overview
**Component interaction and data flow:**
```
[CLI User Input] → [Research Agent] → [Brave Search Tool] → [Search Results]
                      ↓
                 [Email Agent Tool] → [Gmail API] → [Draft Created]
                      ↓
                 [Streaming Response] → [CLI Display]
```

### File Structure Plan
**Files to create/modify with specific responsibilities:**
```bash
# Files to CREATE
agents/
├── __init__.py               # Package initialization
├── research_agent.py         # Primary agent with Brave Search
├── email_agent.py           # Sub-agent with Gmail capabilities
├── providers.py             # LLM provider configuration
└── models.py                # Pydantic models for data validation

tools/
├── __init__.py              # Package initialization
├── brave_search.py          # Brave Search API integration
└── gmail_tool.py            # Gmail API integration

config/
├── __init__.py              # Package initialization
└── settings.py              # Environment and config management

tests/
├── __init__.py              # Package initialization
├── test_research_agent.py   # Research agent tests
├── test_email_agent.py      # Email agent tests
├── test_brave_search.py     # Brave search tool tests
├── test_gmail_tool.py       # Gmail tool tests
└── test_cli.py              # CLI integration tests

# Files to MODIFY
cli.py                       # CLI interface with streaming
.env.example                 # Environment variables template
requirements.txt             # Add new dependencies
README.md                    # Comprehensive documentation
```

### Implementation Sequence
**Tasks in execution order with dependencies:**

#### Phase 1: Core Infrastructure
1. **Create data models**
   - Define Pydantic models for search results, email drafts, and requests
   - Implement validation rules based on API constraints
   - Set up type annotations for all data structures

2. **Implement Brave Search tool**
   - Async HTTP client with proper error handling
   - Rate limiting and timeout configuration
   - Structured result parsing and validation

3. **Implement Gmail tool**
   - OAuth2 authentication flow setup
   - Draft creation with MIME formatting
   - Token refresh and credential management

#### Phase 2: Agent Integration
4. **Create Email Agent**
   - Agent with Gmail tool registration
   - Dependency injection for configuration
   - Structured response formatting

5. **Create Research Agent**
   - Primary agent with Brave Search tool
   - Email Agent as tool integration
   - Context passing and usage tracking

6. **Implement CLI interface**
   - Streaming response handling
   - Tool visibility and colored output
   - Session management and error handling

### Detailed Implementation Steps

#### Step 1: Data Models
```python
# agents/models.py
# Based on research patterns from Pydantic AI documentation

from pydantic import BaseModel, Field
from typing import List, Optional
from datetime import datetime

class ResearchQuery(BaseModel):
    """Research query with validation constraints."""
    query: str = Field(..., description="Research topic to investigate", min_length=1)
    max_results: int = Field(10, ge=1, le=50, description="Maximum search results")
    include_summary: bool = Field(True, description="Include result summaries")

class BraveSearchResult(BaseModel):
    """Structured search result from Brave API."""
    title: str = Field(..., description="Result title")
    url: str = Field(..., description="Result URL")
    description: str = Field(..., description="Result description")
    published_date: Optional[str] = Field(None, description="Publication date")
    
class EmailDraft(BaseModel):
    """Email draft with Gmail API requirements."""
    to: List[str] = Field(..., min_items=1, description="Recipient email addresses")
    subject: str = Field(..., min_length=1, description="Email subject")
    body: str = Field(..., min_length=1, description="Email body content")
    cc: Optional[List[str]] = Field(None, description="CC recipients")
    bcc: Optional[List[str]] = Field(None, description="BCC recipients")
```

#### Step 2: Brave Search Tool
```python
# tools/brave_search.py
# Integration patterns from researched Brave API documentation

import httpx
from typing import List
from agents.models import BraveSearchResult
from config.settings import get_settings

class BraveSearchError(Exception):
    """Custom exception for Brave Search API errors."""
    pass

async def search_brave(query: str, count: int = 10) -> List[BraveSearchResult]:
    """Search using Brave Search API with proper error handling."""
    settings = get_settings()
    
    async with httpx.AsyncClient(timeout=30.0) as client:
        headers = {"X-Subscription-Token": settings.brave_api_key}
        params = {"q": query, "count": count}
        
        try:
            response = await client.get(
                "https://api.search.brave.com/res/v1/web/search",
                headers=headers,
                params=params
            )
            response.raise_for_status()
            
            data = response.json()
            results = data.get("web", {}).get("results", [])
            
            return [
                BraveSearchResult(
                    title=result.get("title", ""),
                    url=result.get("url", ""),
                    description=result.get("description", ""),
                    published_date=result.get("age")
                )
                for result in results
            ]
            
        except httpx.HTTPStatusError as e:
            raise BraveSearchError(f"Brave API error: {e.response.status_code}")
        except httpx.RequestError as e:
            raise BraveSearchError(f"Request failed: {str(e)}")
```

#### Step 3: Multi-Agent Integration
```python
# agents/research_agent.py
# Multi-agent patterns from Pydantic AI documentation

from pydantic_ai import Agent, RunContext
from agents.models import ResearchQuery
from agents.email_agent import email_agent
from tools.brave_search import search_brave
from config.settings import AgentDependencies

research_agent = Agent(
    "research-agent",
    deps_type=AgentDependencies,
    system_prompt="""You are a research assistant that can search for information 
    and create email drafts. Use the brave_search tool to find information, 
    then use create_email_draft to help users compose emails about the research."""
)

@research_agent.tool
async def brave_search_tool(
    ctx: RunContext[AgentDependencies],
    query: str,
    max_results: int = 10
) -> str:
    """Search for information using Brave Search API."""
    results = await search_brave(query, max_results)
    
    if not results:
        return "No search results found for the query."
    
    formatted_results = []
    for i, result in enumerate(results, 1):
        formatted_results.append(
            f"{i}. {result.title}\n"
            f"   URL: {result.url}\n"
            f"   Description: {result.description}\n"
        )
    
    return "\n".join(formatted_results)

@research_agent.tool
async def create_email_draft(
    ctx: RunContext[AgentDependencies],
    recipient: str,
    subject: str,
    context: str
) -> str:
    """Create email draft based on research context."""
    # CRITICAL: Pass usage for token tracking in multi-agent calls
    result = await email_agent.run(
        f"Create an email to {recipient} with subject '{subject}' based on this context: {context}",
        deps=ctx.deps,
        usage=ctx.usage
    )
    
    return f"Email draft created: {result.data}"
```

### Integration Points
**System connections and dependencies:**

```yaml
ENVIRONMENT_VARIABLES:
  - LLM_PROVIDER: "openai"           # LLM provider selection
  - LLM_API_KEY: "sk-..."            # OpenAI API key
  - LLM_MODEL: "gpt-4"               # Model selection
  - BRAVE_API_KEY: "BSA..."          # Brave Search API key
  - GMAIL_CREDENTIALS_PATH: "./credentials/credentials.json"  # Gmail OAuth credentials

EXTERNAL_APIS:
  - brave_search: Rate limit 2000 requests/month
  - gmail_api: OAuth2 flow with browser authentication
  - openai_api: Token-based authentication with usage tracking

CONFIGURATION:
  - oauth_flow: First run opens browser for Gmail authorization
  - token_storage: ./credentials/token.json (auto-created)
  - credential_security: Never commit credentials to version control

TESTING:
  - unit_tests: Mock external API calls for isolation
  - integration_tests: Test agent communication and tool usage
  - error_scenarios: API failures, authentication errors, rate limits
```

---

## 🧪 Validation Gates

### Level 1: Syntax & Style Validation
**Executable commands for immediate feedback:**
```bash
# MUST run these first - fix all errors before proceeding
# Target ONLY the new/modified files - not entire codebase
ruff check agents/ tools/ config/ --fix        # Lint and auto-fix Python files
mypy agents/ tools/ config/                    # Type checking for new modules
black agents/ tools/ config/ --check           # Code formatting verification

# Expected: Zero errors in new modules. If errors exist, read and fix before continuing.
```

### Level 2: Unit Testing
**Test scenarios covering all code paths:**

#### Expected Use Cases
```python
# tests/test_research_agent.py
import pytest
from agents.research_agent import research_agent
from config.settings import AgentDependencies

@pytest.mark.asyncio
async def test_research_with_brave_search():
    """Test research agent searches correctly with Brave API."""
    deps = AgentDependencies()
    result = await research_agent.run(
        "Research the latest developments in AI safety",
        deps=deps
    )
    
    assert result.data
    assert "AI safety" in result.data.lower()
    assert len(result.data) > 100  # Substantial response

@pytest.mark.asyncio 
async def test_research_agent_creates_email():
    """Test research agent can invoke email agent successfully."""
    deps = AgentDependencies()
    result = await research_agent.run(
        "Research AI safety and draft an email to john@example.com about the findings",
        deps=deps
    )
    
    assert "email draft created" in result.data.lower()
    assert "john@example.com" in result.data
```

#### Edge Cases
```python
# tests/test_brave_search.py
import pytest
from tools.brave_search import search_brave, BraveSearchError
from unittest.mock import AsyncMock, patch

@pytest.mark.asyncio
async def test_brave_search_rate_limit_handling():
    """Test graceful handling of Brave API rate limits."""
    with patch('httpx.AsyncClient') as mock_client:
        mock_response = AsyncMock()
        mock_response.status_code = 429
        mock_response.raise_for_status.side_effect = httpx.HTTPStatusError(
            "Too Many Requests", request=None, response=mock_response
        )
        mock_client.return_value.__aenter__.return_value.get.return_value = mock_response
        
        with pytest.raises(BraveSearchError, match="Brave API error: 429"):
            await search_brave("test query")

@pytest.mark.asyncio
async def test_empty_search_results():
    """Test handling of empty search results."""
    with patch('httpx.AsyncClient') as mock_client:
        mock_response = AsyncMock()
        mock_response.status_code = 200
        mock_response.json.return_value = {"web": {"results": []}}
        mock_client.return_value.__aenter__.return_value.get.return_value = mock_response
        
        results = await search_brave("nonexistent query")
        assert results == []
```

#### Failure Cases
```python
# tests/test_gmail_tool.py
import pytest
from tools.gmail_tool import GmailTool, GmailAuthError
from unittest.mock import patch, MagicMock

def test_gmail_authentication_failure():
    """Test Gmail authentication failure handling."""
    with patch('google.auth.transport.requests.Request') as mock_request:
        mock_request.side_effect = Exception("Authentication failed")
        
        with pytest.raises(GmailAuthError, match="Authentication failed"):
            tool = GmailTool()
            tool.authenticate()

def test_gmail_draft_creation_failure():
    """Test Gmail draft creation error handling."""
    with patch('googleapiclient.discovery.build') as mock_build:
        mock_service = MagicMock()
        mock_service.users().drafts().create().execute.side_effect = Exception("Draft creation failed")
        mock_build.return_value = mock_service
        
        tool = GmailTool()
        with pytest.raises(Exception, match="Draft creation failed"):
            tool.create_draft("test@example.com", "Test", "Test body")
```

**Test execution command:**
```bash
# Test ONLY the new feature/module - not entire repository
pytest tests/test_research_agent.py tests/test_email_agent.py tests/test_brave_search.py tests/test_gmail_tool.py -v --cov=agents --cov=tools --cov-report=term-missing
# Expected: All feature-specific tests pass with >80% coverage. If failing, analyze root cause and fix.
```

### Level 3: Integration Testing
**End-to-end validation with real system integration:**

```bash
# Start system dependencies (if any)
# No external services needed for this implementation

# Run integration tests for this feature only
pytest tests/test_cli.py -v --integration

# Manual verification with CLI
python cli.py
# Test interaction:
# User: "Research the latest AI safety papers"
# Expected: Search results displayed with tool visibility
# User: "Create an email draft about this research to john@example.com"
# Expected: Email draft created and confirmation shown

# Expected results based on research
# Success: Structured search results, email draft ID returned
# Error: Clear error messages, graceful degradation
```

## 🎯 Quality Assurance Checklist

### Implementation Completeness
- [ ] All Pydantic AI patterns implemented correctly (Agent, tools, dependencies)
- [ ] Brave Search API integration follows rate limiting best practices
- [ ] Gmail API OAuth2 flow handles authentication and token refresh
- [ ] Multi-agent communication properly passes context and usage tracking
- [ ] Configuration management follows existing project patterns

### Testing Coverage
- [ ] Unit tests: Expected use, edge cases, failure scenarios for new agents and tools only
- [ ] Integration tests: End-to-end agent communication and tool usage verified
- [ ] Error paths: All failure modes tested for API errors, authentication issues
- [ ] Performance: Response times meet criteria for CLI user experience
- [ ] Security: API keys secured, OAuth tokens handled safely

### Code Quality
- [ ] Linting: All style checks pass for new Python modules
- [ ] Type checking: No mypy errors in new agent and tool files
- [ ] Documentation: Inline comments explain complex multi-agent interactions
- [ ] Logging: Appropriate logging for debugging and monitoring
- [ ] Configuration: All API keys and settings externalized to environment variables

### Production Readiness
- [ ] Performance benchmarks met for search and email operations
- [ ] Error responses provide clear user guidance
- [ ] OAuth2 flow documented with setup instructions
- [ ] Rate limiting handled gracefully with user feedback
- [ ] CLI provides intuitive user experience with streaming responses

---

## 🚨 Critical Success Factors

### Research Adherence
- **Pydantic AI patterns are sacred**: Use exact agent creation and tool registration patterns
- **API documentation is law**: Follow Brave Search and Gmail API constraints exactly
- **Existing codebase patterns**: Mirror established agent and CLI patterns from examples
- **Multi-agent communication**: Respect context passing and usage tracking requirements

### Implementation Quality
- **No assumptions about APIs**: All behavior based on researched API documentation
- **Comprehensive error handling**: Cover authentication, rate limits, and API failures
- **Testing thoroughness**: Validate expected use, edge cases, and failure scenarios
- **Security practices**: Proper credential management and OAuth2 implementation

### Anti-Patterns to Avoid
- ❌ **Ignoring async patterns**: Don't mix sync and async code in agent context
- ❌ **Skipping OAuth2 setup**: Gmail requires proper authentication flow
- ❌ **Hardcoding API keys**: Use environment variables for all credentials
- ❌ **Missing usage tracking**: Always pass ctx.usage in multi-agent calls
- ❌ **Breaking CLI patterns**: Follow established streaming and tool visibility patterns