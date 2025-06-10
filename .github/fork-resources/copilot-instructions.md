# GitHub Copilot Instructions

## CRITICAL: GitHub Copilot Agent Commit Requirements

**BEFORE MAKING ANY COMMIT, READ THIS SECTION CAREFULLY**

This repository has automated validation that WILL FAIL if commits don't follow exact conventional commit format. GitHub Copilot Agent MUST follow these rules:

### Commit Message Validation Rules
1. **FORMAT**: `<type>: <description>` or `<type>(<scope>): <description>`
2. **NO PREFIXES**: Never use ✅, ❌, 🚀, [feat], or any symbols/emojis
3. **LOWERCASE TYPE**: Always use `feat:`, `fix:`, `chore:` (never `Feat:`, `Fix:`)
4. **REQUIRED COLON**: Must have colon and space after type: `feat: ` not `feat`
5. **IMPERATIVE MOOD**: Use "add feature" not "added feature" or "adds feature"

### Valid Examples for Copilot Agent
```
feat: add authentication middleware
fix: resolve sync conflict in pom.xml
chore: update dependencies to latest versions
docs: update README with new configuration
ci: add validation for commit messages
```

### Repository Validation
This repository uses `webiny/action-conventional-commits@v1.1.0` to validate ALL commits. Commits that fail this validation will block PRs from merging.

## Project Overview

You are working with an OSDU fork repository that uses automated synchronization to stay updated with upstream changes. This fork follows a structured development workflow with emphasis on conventional commits for automated release management using Release Please.

## Key Architecture

### Branch Strategy
- `main` - Production branch with strict protection rules and semantic releases
- `fork_upstream` - Automatically tracks upstream repository changes
- `fork_integration` - Staging branch for conflict resolution before merging to main

### Core Workflows
1. **sync.yml** - Automated upstream synchronization with AI-enhanced PR descriptions
2. **build.yml** - Build and test automation for Java/Maven projects
3. **validate.yml** - PR validation, commit message checks, and conflict detection
4. **release.yml** - Automated semantic versioning with Release Please
5. **sync-template.yml** - Template updates from fork management template
6. **cascade.yml** - Propagates template changes to downstream fork repositories
7. **cascade-monitor.yml** - Monitors cascade workflow status and provides notifications

## Development Guidelines

### Commit Messages (CRITICAL)
**STRICT REQUIREMENT: All commits MUST follow conventional commits format exactly** - This is essential for Release Please and CI validation to work correctly.

**REQUIRED FORMAT:**
```
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

**VALID EXAMPLES:**
```
feat: add new feature
fix: correct bug in upstream sync
chore: update dependencies  
docs: improve README documentation
feat!: breaking change to API
feat(auth): add OAuth2 support
fix(sync): resolve merge conflict handling
```

**INVALID FORMATS TO NEVER USE:**
```
❌ ✅ fix: add missing fork-resources handling     # NO emojis/symbols
❌ Fix: correct bug                               # NO capital letters
❌ added new feature                              # NO past tense
❌ feature: add authentication                    # NO "feature", use "feat"
❌ bug fix: resolve issue                        # NO spaces in type
❌ Update dependencies                           # NO imperative without type
❌ [feat] add new feature                        # NO brackets
❌ feat add new feature                          # MISSING colon
```

**Commit Message Types (EXACT SPELLING REQUIRED):**
- `feat:` - New features (triggers minor version bump)
- `fix:` - Bug fixes (triggers patch version bump) 
- `feat!:` or `fix!:` - Breaking changes (triggers major version bump)
- `chore:` - Maintenance tasks (no version bump)
- `docs:` - Documentation updates (no version bump)
- `ci:` - CI/CD changes (no version bump)
- `refactor:` - Code refactoring (no version bump)
- `test:` - Test additions/updates (no version bump)

**CRITICAL RULES FOR GITHUB COPILOT AGENT:**
1. **NO EMOJIS OR SYMBOLS** - Never prefix with ✅, ❌, 🚀, etc.
2. **LOWERCASE TYPE** - Always use lowercase (feat, fix, not Feat, Fix)
3. **COLON REQUIRED** - Must have colon after type: `feat:` not `feat`
4. **NO PAST TENSE** - Use "add feature" not "added feature"
5. **IMPERATIVE MOOD** - Use "fix bug" not "fixes bug"
6. **NO EXTRA WHITESPACE** - One space after colon: `feat: description`

### Branch Naming
Use descriptive branch names:
- `feat/issue-123-add-authentication`
- `fix/issue-456-memory-leak`
- `chore/update-dependencies`

### Pull Requests
- Create PRs using GitHub CLI: `gh pr create`
- Include clear descriptions of changes
- Reference related issues using `Fixes #123` or `Closes #456`
- **CRITICAL**: ALL commits in PR MUST pass conventional commit validation
- **CRITICAL**: PR will be blocked if any commit fails `webiny/action-conventional-commits` validation
- Use conventional commit format in PR titles
- Ensure all CI checks pass before merging

### Testing
- Write behavior-driven tests, not implementation tests
- For Java projects: use JUnit 5 and Mockito
- Aim for 80%+ test coverage
- Run tests locally before pushing: `mvn test`

## OSDU Fork Development

### Working with Upstream Changes
1. Upstream changes automatically flow to `fork_upstream` branch
2. Changes are validated in `fork_integration` branch
3. Resolved changes are merged to `main` with semantic versioning
4. Monitor sync workflow results and resolve conflicts promptly

### Release Management
- Releases are automated via Release Please
- Version numbers follow semantic versioning based on conventional commits
- CHANGELOG.md is automatically maintained
- GitHub releases are created automatically

### Conflict Resolution
When upstream sync creates conflicts:
1. Review the conflict in `fork_integration` branch
2. Create a feature branch to resolve conflicts
3. Use conventional commit messages for your resolution
4. Submit PR back to `fork_integration`

## Java/Maven Development
```bash
# Build project
mvn clean install

# Run tests with coverage
mvn clean test org.jacoco:jacoco-maven-plugin:0.8.11:report

# Run specific test
mvn test -Dtest=TestClassName#testMethodName

# Check for dependency updates
mvn versions:display-dependency-updates
```

### Working with Issues
When creating issues, use appropriate workflow labels:
- **Workflow State**: `cascade-active`, `cascade-blocked`, `cascade-ready`, `cascade-failed`, `cascade-escalated`
- **Issue Types**: `sync-failed`, `sync-update`, `conflict`, `needs-resolution`, `build-failed`, `template-sync-failed`, `template-update`
- **Priority**: `high-priority`, `escalation`, `emergency`
- **Components**: `upstream-sync`, `dependencies`, `initialization`, `rollback`, `release-tracking`
- **Process**: `auto-merge-enabled`, `manual-review-required`, `production-ready`
- **AI**: Add `copilot` label for AI-suitable tasks

## MCP Server Integration

This repository is configured with the Maven MCP Server for enhanced dependency management:

### Available MCP Tools
- **check_version_tool**: Check Maven dependency versions against Maven Central
- **scan_java_project_tool**: Scan project dependencies for security vulnerabilities  
- **list_available_versions_tool**: List available versions for specific dependencies

### Usage Examples
```
@copilot Check if spring-boot-starter-web has newer versions available
@copilot Scan this project for dependency vulnerabilities
@copilot What versions of jackson-databind are available?
```

### Integration with Workflows
- **Upstream Sync**: Analyze dependency changes for security implications
- **Conflict Resolution**: Use version analysis for dependency conflicts
- **Release Planning**: Security scans inform release timing

### Firewall Configuration
This repository is configured to allow GitHub Copilot Agent access to OSDU-required domains:
- `community.opengroup.org` - OSDU Open Group community resources
- `repo1.maven.org`, `central.maven.org`, `repo.maven.apache.org` - Maven repositories
- `plugins.gradle.org` - Gradle plugins

If you see firewall warnings, check that `COPILOT_AGENT_FIREWALL_ALLOW_LIST_ADDITIONS` is configured in repository variables.

## Workflow Patterns

### Standard Workflow Structure
```yaml
name: Workflow Name
on:
  schedule:
    - cron: '0 0 * * 0'  # Weekly
  workflow_dispatch:      # Manual trigger

jobs:
  job-name:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      pull-requests: write
      
    steps:
      - uses: actions/checkout@v4
        with:
          token: ${{ secrets.GITHUB_TOKEN }}
          
      - name: Your Logic Here
        run: |
          # Implementation
```

### Error Handling
- Always include error handling in workflows
- Use `if: failure()` for cleanup steps
- Report status to PRs when applicable
- Create issues for persistent failures

## Security Considerations

- Never commit sensitive data or credentials
- Use GitHub Secrets for tokens and API keys
- Security scanning is automated via Trivy
- Follow branch protection rules strictly

## Quick Reference

### Key Files
- `CHANGELOG.md` - Release notes (auto-generated)
- `.github/workflows/` - All automation workflows
- `pom.xml` or `package.json` - Project dependencies

### Environment Variables
- `UPSTREAM_OWNER` - Upstream repository owner
- `UPSTREAM_REPO` - Upstream repository name
- `GITHUB_TOKEN` - Authentication token

### Useful Commands
```bash
# View workflow runs
gh workflow view

# Create PR with conventional commit title
gh pr create --title "feat: add new feature" --body "Description"

# Check PR status
gh pr status

# View issues
gh issue list --label copilot

# Check release status
gh release list
```

## Release Please Integration

### Version Management
- **Patch**: `fix:` commits increment patch version (1.0.0 → 1.0.1)
- **Minor**: `feat:` commits increment minor version (1.0.0 → 1.1.0)  
- **Major**: `feat!:` or `fix!:` commits increment major version (1.0.0 → 2.0.0)

### Changelog Sections
Release Please organizes changes by commit type:
- **Features** - `feat:` commits
- **Bug Fixes** - `fix:` commits
- **Dependencies** - `chore(deps):` commits
- **Documentation** - `docs:` commits

### Breaking Changes
Mark breaking changes clearly:
```
feat!: change API authentication method

BREAKING CHANGE: The authentication method has changed from API keys to OAuth2. 
Update your configuration to use the new oauth settings.
```

## GitHub Copilot Agent Summary

### Pre-Commit Checklist
Before making ANY commit, GitHub Copilot Agent must verify:

1. ✅ **Commit message starts with valid type**: `feat:`, `fix:`, `chore:`, `docs:`, `ci:`, `refactor:`, `test:`
2. ✅ **No symbols or emojis**: No ✅, ❌, 🚀, [brackets], etc.
3. ✅ **Lowercase type**: `feat:` not `Feat:` or `FEAT:`
4. ✅ **Colon and space**: `feat: ` not `feat:` or `feat`
5. ✅ **Imperative mood**: "add feature" not "added feature"
6. ✅ **No past tense**: "fix bug" not "fixed bug"

### Validation Enforcement
- Repository uses `webiny/action-conventional-commits@v1.1.0`
- ALL commits are validated automatically
- Failed validation BLOCKS PR merging
- No exceptions for any branch or contributor

### Common Mistakes to Avoid
```bash
# WRONG - These will fail validation
git commit -m "✅ fix: add missing handling"     # emoji prefix
git commit -m "Fix: correct the bug"             # capital letter
git commit -m "added new feature"                # past tense, no type
git commit -m "feat add authentication"          # missing colon
git commit -m "[feat] new feature"               # brackets

# CORRECT - These will pass validation  
git commit -m "fix: add missing handling"
git commit -m "fix: correct the bug"
git commit -m "feat: add new feature"
git commit -m "feat: add authentication"
git commit -m "feat: add new feature"
```

## Support

For questions or issues:
1. Check CHANGELOG.md for recent changes
2. Review workflow run logs for failures
3. Create an issue with appropriate labels
4. Tag with `claude` if additional AI assistance is needed or if working on issues from `claude`
5. Reference upstream repository documentation for OSDU-specific guidance