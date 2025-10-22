# Claude Code Market

A curated marketplace of specialized AI agents for Claude Code, designed to enhance your development workflow with battle-tested, production-ready agent configurations.

## What is the Claude Code Market?

The Claude Code Market is a collection of expertly crafted AI agent personas that you can install into your Claude Code projects. Each agent specializes in a specific aspect of software development, from planning and architecture to implementation, testing, and debugging.

## Quick Start

### Browse Available Agents

View all available agents in the [agents.json](./agents.json) catalog or browse the [personas/](./personas/) directory.

### Install an Agent

1. **Choose an agent** from the catalog that fits your needs
2. **Copy the agent file** (e.g., `personas/task-executor.md`)
3. **Paste it** into your project's `.claude/personas/` directory
4. **Invoke the agent** using @ mention (e.g., `@task-executor implement feature`)

### Example Installation

```bash
# Create personas directory in your project
mkdir -p .claude/personas

# Copy desired agent
cp path/to/claude-code-agents/personas/task-executor.md .claude/personas/

# Invoke in Claude Code
# @task-executor execute tasks from specs/my-feature/tasks.md
```

## Agent Categories

### Development
Agents focused on writing and implementing code.

| Agent | Description | Use When |
|-------|-------------|----------|
| **task-executor** | Surgical precision implementation | Executing specific tasks from task lists |

### Quality Assurance
Agents specializing in testing, review, and debugging.

| Agent | Description | Use When |
|-------|-------------|----------|
| **code-reviewer** | Quality & security review expert | After writing or modifying code |
| **debugger** | Error analysis & troubleshooting | Encountering bugs or test failures |

### Planning & Architecture
Agents for design, planning, and documentation.

| Agent | Description | Use When |
|-------|-------------|----------|
| **strategic-planner** | Requirements & technical design | Planning new features or systems |
| **steering-architect** | Project analysis & documentation | Initializing projects or analyzing codebases |

### Data & Analysis
Agents for data-driven insights.

| Agent | Description | Use When |
|-------|-------------|----------|
| **data-scientist** | SQL optimization & analytics | Analyzing data or optimizing queries |

### Product Management
Agents for product strategy and requirements.

| Agent | Description | Use When |
|-------|-------------|----------|
| **product-manager** | PRD creation & requirements | Creating product requirements documents |

### Optimization
Agents for improving efficiency.

| Agent | Description | Use When |
|-------|-------------|----------|
| **llms-txt-generator** | Context optimization | Creating LLM-friendly project summaries |

## Common Workflows

### Feature Development Workflow

A complete end-to-end workflow for implementing new features:

```
1. @steering-architect analyze codebase
   └─> Creates .docs/ foundation with project context

2. @product-manager create PRD for [feature]
   └─> Creates comprehensive product requirements

3. @strategic-planner plan [feature]
   └─> Creates specs/ with requirements, design, and tasks

4. @task-executor execute tasks from specs/[feature]/tasks.md
   └─> Implements feature step-by-step

5. @code-reviewer review recent changes
   └─> Validates quality, security, and best practices
```

### Debugging Workflow

Quick workflow for fixing issues:

```
1. @debugger analyze [error/issue]
   └─> Identifies root cause and proposes fixes

2. @debugger implement fix
   └─> Makes surgical changes to resolve issue

3. @code-reviewer review fix
   └─> Ensures fix doesn't introduce new issues
```

### Data Analysis Workflow

Workflow for data-driven insights:

```
1. @data-scientist analyze [dataset/query]
   └─> Examines data patterns and performance

2. @data-scientist optimize [query/operation]
   └─> Improves SQL queries and data operations
```

## Agent Metadata

Each agent in the catalog includes comprehensive metadata:

```json
{
  "id": "strategic-planner",
  "name": "Strategic Planner",
  "description": "Software architect specializing in...",
  "category": "planning",
  "tags": ["architecture", "design", "planning"],
  "file": "personas/strategic-planner.md",
  "tools": ["Edit", "MultiEdit", "Read", "Grep", "Glob", "WebSearch"],
  "triggers": ["plan", "design", "architect"],
  "use_cases": ["Create technical specifications", "Design system architecture"],
  "expertise": ["Requirements analysis", "Technical design"],
  "version": "1.0.0"
}
```

## Finding the Right Agent

### By Task Type

- **Need to plan?** → `@strategic-planner` or `@product-manager`
- **Need to code?** → `@task-executor`
- **Need to debug?** → `@debugger`
- **Need to review?** → `@code-reviewer`
- **Need to analyze data?** → `@data-scientist`
- **Need project docs?** → `@steering-architect`

### By Trigger Words

Agents can be automatically triggered by certain keywords:

- **"plan feature"** → Activates `@strategic-planner`
- **"review code"** → Activates `@code-reviewer`
- **"debug error"** → Activates `@debugger`
- **"analyze data"** → Activates `@data-scientist`

### By Expertise Area

Search the [agents.json](./agents.json) file for specific expertise:

```bash
# Find agents with security expertise
jq '.agents[] | select(.expertise | contains(["Security review"]))' agents.json

# Find agents with specific tools
jq '.agents[] | select(.tools | contains(["WebSearch"]))' agents.json

# Find agents by category
jq '.agents[] | select(.category == "quality")' agents.json
```

## Agent Specifications

### Tool Access

Each agent has access to specific Claude Code tools:

- **Edit/MultiEdit/Write**: File modification capabilities
- **Read/Grep/Glob**: Code exploration and search
- **Bash**: Command execution
- **WebSearch**: Internet research capabilities

### Proactive Activation

Some agents are proactive and will automatically activate based on context:

- **code-reviewer**: Automatically activates after code changes
- **debugger**: Automatically activates when errors are detected
- **strategic-planner**: Automatically activates for planning requests

### Agent Interactions

Agents are designed to work together:

- **steering-architect** → Creates `.docs/` for other agents to reference
- **strategic-planner** → Creates `specs/` for task-executor to implement
- **task-executor** → Implements code for code-reviewer to validate
- **debugger** → Fixes issues that code-reviewer identifies

## Advanced Usage

### Programmatic Access

The `agents.json` catalog enables programmatic agent discovery and installation:

```javascript
// Example: Find all quality assurance agents
const catalog = require('./agents.json');
const qaAgents = catalog.agents.filter(a => a.category === 'quality');

// Example: Install agent programmatically
const agent = catalog.agents.find(a => a.id === 'task-executor');
fs.copyFileSync(agent.file, '.claude/personas/task-executor.md');
```

### Custom Workflows

Create custom workflows combining multiple agents:

```markdown
## Code Modernization Workflow
1. @steering-architect analyze legacy codebase
2. @strategic-planner design modernization approach
3. @task-executor refactor components step-by-step
4. @code-reviewer validate improvements
5. @debugger fix any regressions
```

### Agent Customization

You can customize any agent by:

1. Copying the agent file to your project
2. Modifying the YAML frontmatter (name, description, triggers)
3. Adjusting the agent instructions to fit your needs

## Best Practices

### When to Use Agents

- **Use @strategic-planner** BEFORE writing code to plan properly
- **Use @task-executor** for implementation, not @strategic-planner
- **Use @code-reviewer** AFTER any code changes
- **Use @debugger** when tests fail or errors occur
- **Use @steering-architect** when starting new projects

### Agent Workflow Tips

1. **Sequential, not parallel**: Let each agent complete its work before the next
2. **One task at a time**: Especially with @task-executor
3. **Always review**: Never skip @code-reviewer after implementation
4. **Document first**: Use @steering-architect early in projects
5. **Plan before implementing**: @strategic-planner → @task-executor workflow

### Common Pitfalls to Avoid

- **Don't** ask @strategic-planner to write code (use @task-executor)
- **Don't** skip planning and jump straight to @task-executor
- **Don't** forget to run @code-reviewer after changes
- **Don't** use multiple agents simultaneously (sequential is better)

## Contributing

This is an open-source collection of AI agents. Contributions are welcome!

### Adding a New Agent

1. Create a new file in `personas/` following the existing format
2. Add YAML frontmatter with agent metadata
3. Update `agents.json` with the new agent entry
4. Update this MARKET.md with the agent in appropriate category
5. Submit a pull request

### Agent Quality Standards

All agents should:
- Have clear, focused responsibilities
- Include comprehensive documentation
- Define specific triggers and use cases
- Specify required tools
- Follow the established YAML frontmatter format
- Include version information

## Support & Feedback

- **Issues**: Report bugs or request features on [GitHub Issues](https://github.com/jackg825/claude-code-agents/issues)
- **Discussions**: Share workflows and ask questions in [GitHub Discussions](https://github.com/jackg825/claude-code-agents/discussions)
- **Documentation**: Read the full guide in [README.md](./README.md)

## Version History

- **v1.0.0** (2025-10-22): Initial Claude Code Market release
  - 8 specialized agents
  - 6 categories
  - Comprehensive catalog with metadata
  - Installation and usage documentation

## License

MIT License - See [LICENSE](./LICENSE) for details.
