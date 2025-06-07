# Fork Management Template

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![GitHub Issues](https://img.shields.io/github/issues/danielscholl-osdu/osdu-fork-template)](https://github.com/danielscholl-osdu/osdu-fork-template/issues)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/danielscholl-osdu/osdu-fork-template/pulls)

## 🤖 AI-Driven Development

[![Claude Ready](https://img.shields.io/badge/Claude%20Code-Ready-orange?logo=anthropic)](https://github.com/danielscholl/pr-generator-agent/blob/main/CLAUDE.md)
[![Copilot-Ready](https://img.shields.io/badge/Copilot%20Agent-Ready-8A2BE2?logo=github)](https://github.com/danielscholl-osdu/osdu-fork-template/blob/main/.github/copilot-instructions.md)
[![Template CI](https://img.shields.io/badge/Template%20CI-Active-green?logo=github)](https://github.com/danielscholl-osdu/osdu-fork-template/actions)

This project follows an AI-driven development workflow:
- 🤖 **Built with AI** - Developed and maintained using Claude Code and GitHub Copilot
- 📋 **AI Task Assignment** - Issues labeled with `copilot` are designed for AI implementation
- 📚 **AI-Friendly Documentation** - Comprehensive guides for AI agents in [CLAUDE.md](CLAUDE.md)
- 🔄 **Automated Workflows** - GitHub Actions with AI-enhanced PR descriptions and conflict resolution
- 🎯 **AI-First Architecture** - Designed with clear patterns for AI understanding and modification ([AI Principles](AI_PRINCIPLES.md))

## What is Fork Management Template?

This template automates the complex task of maintaining long-lived forks of upstream repositories. It's designed for teams who need to:

- **Preserve local enhancements** while staying current with upstream changes
- **Automate conflict detection** and resolution workflows
- **Maintain release correlation** between fork and upstream versions
- **Enable AI-driven development** with structured patterns and documentation

**Perfect for**: OSDU projects, enterprise forks, research variations, or any scenario requiring controlled upstream synchronization.

## Core Architecture

The template implements a **three-branch strategy** that creates controlled integration checkpoints:

```
fork_upstream → fork_integration → main
   (mirror)      (conflicts)     (stable)
```

This flow ensures upstream changes are validated before reaching your stable branch, with AI-enhanced conflict analysis at each stage.

## Key Features

✅ **Automated Daily Sync** - Pulls upstream changes with conflict detection  
✅ **AI-Enhanced Analysis** - Intelligent PR descriptions and conflict categorization  
✅ **Branch Protection** - Prevents accidental damage to stable branches  
✅ **Release Correlation** - Tracks your versions against upstream releases  
✅ **Multi-AI Ready** - Optimized for Claude Code and GitHub Copilot collaboration

## Prerequisites

Before starting, ensure you have:
- GitHub account with repository creation permissions
- (Optional) Personal Access Token (PAT) for full automation:
  - Create a secret named `GH_TOKEN` in your repository
  - Required scopes: `repo`, `workflow`, `admin:repo_hook`
  - Without PAT: Manual configuration of branch protection and secrets required

## Quick Start

### 1. Create New Repository
1. Click the "Use this template" button above
2. Choose a name and owner for your new repository
3. Create repository

### 2. Initialize Repository
1. Go to Actions → Select "Initialize Fork" → Click "Run workflow"
2. Follow the setup instructions in the auto-created issue
3. Configure your upstream repository and sync settings

**Next Steps**: See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed workflow guidance

## How It Works

1. **Daily Automation**: Checks upstream for changes and creates sync PRs
2. **Conflict Analysis**: AI categorizes conflicts and suggests resolution approaches  
3. **Staged Integration**: Changes flow through validation checkpoints
4. **Release Tracking**: Maintains correlation between your versions and upstream

**See detailed architecture diagrams and workflows**: [Product Architecture](doc/product-architecture.md)

## Documentation

- 📚 **[CONTRIBUTING.md](CONTRIBUTING.md)** - Step-by-step workflows for contributors and users
- 🤖 **[AI_PRINCIPLES.md](AI_PRINCIPLES.md)** - AI-first development principles and practices
- 🧠 **[AI_EVOLUTION.md](AI_EVOLUTION.md)** - Historical context and patterns for AI agents
- ⚙️ **[CLAUDE.md](CLAUDE.md)** - AI agent instructions and development guidelines
- 🔍 **[Overview](doc/overview.md)** - Conceptual understanding of fork management
- 📋 **[Product Requirements](doc/prd.md)** - Detailed design and requirements
- 📖 **[ADRs](doc/adr/)** - Architectural decisions and rationale
