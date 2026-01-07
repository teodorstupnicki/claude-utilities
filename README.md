# Claude Configuration Repository

Personal Claude Code configuration repository with custom agents for DevOps and cloud engineering workflows.

## Overview

This repository contains custom Claude Code agent configurations that extend Claude's capabilities for specific DevOps tasks. All configurations are version-controlled and can be shared across projects or with team members.

## Repository Structure

```
claude-utilities/
├── .claude/
│   └── agents/          # Custom agent configurations
│       └── terraform-azure-validator.md
├── README.md
└── .gitignore
```

## Available Agents

### Terraform Azure Validator

**Agent Name**: `terraform-azure-validator`

**Purpose**: Expert Terraform and Azure cloud security validator for DevOps Engineers working with Azure resources.

**Capabilities**:
- Validates Terraform syntax and structure
- Security vulnerability detection
- CIS Azure Foundations Benchmark compliance checking
- Identifies misconfigurations in Azure resources
- Generates detailed remediation recommendations
- Reviews resource tagging and naming conventions

**Key Security Checks**:
- Storage accounts (HTTPS-only, TLS 1.2+, encryption)
- SQL servers (public access, TDE, auditing)
- Virtual networks (NSG rules, segmentation)
- Key vaults (soft delete, access policies)
- Virtual machines (managed identities, encryption)
- App Services (HTTPS-only, TLS settings)
- Container registries and AKS clusters

**Usage**:
```bash
# Invoke the agent directly
claude "Use terraform-azure-validator to review my Terraform files"

# Or let Claude automatically delegate to it
claude "Review my Azure infrastructure code for security issues"
```

## Installation

### Option 1: Clone for Personal Use

Clone this repository to use these agents in any project:

```bash
git clone https://github.com/yourusername/claude-utilities.git ~/.claude-utilities
```

Then symlink the agents directory:

```bash
ln -s ~/.claude-utilities/.claude/agents ~/.claude/agents
```

### Option 2: Use in Specific Projects

Clone or copy the `.claude/agents/` directory into your project:

```bash
# In your project directory
git clone https://github.com/yourusername/claude-utilities.git
cp -r claude-utilities/.claude .
rm -rf claude-utilities
```

Or add as a git submodule:

```bash
git submodule add https://github.com/yourusername/claude-utilities.git .claude-config
ln -s .claude-config/.claude .claude
```

### Option 3: Copy Individual Agents

Copy specific agent files you need:

```bash
mkdir -p .claude/agents
curl -o .claude/agents/terraform-azure-validator.md \
  https://raw.githubusercontent.com/yourusername/claude-utilities/main/.claude/agents/terraform-azure-validator.md
```

## Using the Agents

Once installed, agents work automatically:

1. **Explicit invocation**:
   ```bash
   claude "Use terraform-azure-validator to check my infrastructure code"
   ```

2. **Automatic delegation**:
   Claude will automatically use the appropriate agent based on context:
   ```bash
   claude "Review my Azure Terraform for security issues"
   ```

3. **Interactive mode**:
   ```bash
   claude
   > /agents  # List all available agents
   > Review main.tf for compliance issues
   ```

## Creating New Agents

To add your own custom agents:

1. Create a new Markdown file in `.claude/agents/` with YAML frontmatter:

```markdown
---
name: your-agent-name
description: When this agent should be invoked
tools: Read, Glob, Grep, Edit, Bash
model: sonnet
---

Your agent's system prompt and instructions here...
```

2. Commit and push:

```bash
git add .claude/agents/your-agent-name.md
git commit -m "Add new agent: your-agent-name"
git push
```

## Configuration Files

### Agent File Structure

Each agent is a Markdown file with:
- **YAML frontmatter**: Configuration (name, description, tools, model)
- **Markdown body**: System prompt and detailed instructions

### Required Fields

- `name`: Unique identifier (lowercase with hyphens)
- `description`: When to invoke this agent
- `tools`: Comma-separated list of allowed tools
- `model`: `sonnet`, `opus`, `haiku`, or `inherit`

## Contributing

Contributions welcome! To add a new agent:

1. Fork this repository
2. Create your agent in `.claude/agents/`
3. Update this README with agent documentation
4. Submit a pull request

## Best Practices

- **Focused agents**: Each agent should have a single, clear responsibility
- **Detailed prompts**: Include specific instructions and examples
- **Tool restrictions**: Only grant necessary tools for security
- **Version control**: Commit all changes to share with team
- **Documentation**: Document agent purpose and usage

## Resources

- [Claude Code Documentation](https://code.claude.com/docs)
- [Subagents Guide](https://code.claude.com/docs/en/sub-agents)
- [CIS Azure Foundations Benchmark](https://www.cisecurity.org/benchmark/azure)
- [Terraform Azure Provider](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)

## License

MIT License - Feel free to use and modify for your needs.