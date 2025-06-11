
# GitHub Copilot Instructions

## CRITICAL: Commit Message Requirements

All commits must follow the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) format to pass automated validation. Otherwise, PRs will be blocked.

### Format

```
<type>(<scope>): <description>

[optional body]

[optional footer(s)]
```

### Valid Examples

```
feat: add authentication middleware
fix(sync): resolve merge conflict
chore: update dependencies
docs: update README
ci: add commit validation
```

### Invalid Examples

```
fix: handle error         # do not prefix with symbols or emojis
Fix: correct bug          # do not use capital letters
added new feature         # do not use past tense
feature: use OAuth2       # do not use "feature", use "feat"
[feat] add login support  # do not use brackets
feat add login            # missing colon
```

### Allowed Types

- feat: — New feature
- fix: — Bug fix
- feat!: / fix!: — Breaking change
- chore: — Maintenance (no version bump)
- docs: — Documentation
- ci: — CI/CD config
- refactor: — Refactoring
- test: — Tests

### Key Rules

- No emojis or symbols
- Type must be lowercase
- Use imperative mood: "add feature", not "added" or "adds"
- Colon and space required: `fix: correct bug`
- One space after the colon
- No brackets or prefixing (e.g., [feat])


## Project Structure

This is a fork of the OSDU repository with automated workflows and semantic versioning using Release Please.

### Branch Strategy

- main: Protected production branch (semantic releases)
- fork_upstream: Auto-sync with upstream repo
- fork_integration: Staging area for conflict resolution

## Automation Workflows

| Workflow              | Purpose                                             |
| --------------------- | --------------------------------------------------- |
| sync.yml              | Sync with upstream, auto-generate PRs               |
| build.yml             | Build & test Java/Maven projects                    |
| validate.yml          | Enforce commit message validation, detect conflicts |
| release.yml           | Automate releases with version bumps                |
| sync-template.yml     | Update from fork template                           |
| cascade.yml           | Propagate template updates to forks                 |
| cascade-monitor.yml   | Monitor propagation status                          |


## Development Guidelines

### Branch Naming

Use descriptive names:

```
feat/issue-123-add-auth
fix/issue-456-fix-leak
chore/update-dependencies
```

### Pull Requests

- Create with `gh pr create`
- Use conventional commit format in PR titles
- Reference issues: `Fixes #123`
- Ensure all commits and CI checks pass

### Testing

- Use behavior-driven tests
- Target 80%+ test coverage
- Run locally:

```bash
mvn clean install
mvn test
mvn versions:display-dependency-updates
```


## MCP Integration

Includes tools for Maven dependency management:

- check_version_tool: Check a Maven version and get all version update information
- check_version_batch_tool: Process multiple Maven dependency version checks in a single batch
- list_available_versions_tool: List all available versions grouped by minor version tracks
- scan_java_project_tool: Scan Java Maven projects for vulnerabilities using Trivy
- analyze_pom_file_tool: Analyze a single Maven POM file for dependencies and vulnerabilities


## Working with Upstream

1. fork_upstream: auto-receives updates
2. fork_integration: staging and validation
3. main: protected release branch
4. Use feature branches to resolve conflicts and open PRs

## Copilot Commit Checklist

Before committing, ensure:

- Starts with valid lowercase type (feat:, fix:, etc.)
- No emojis or symbols
- Colon and space present
- Uses imperative mood
- No past tense or brackets
- One space after colon

## Quick Reference

### Key Files

- CHANGELOG.md – Auto-generated release notes
- .github/workflows/ – GitHub Actions configs
- pom.xml – Maven config

### Useful Commands

```bash
gh workflow view
gh pr status
gh release list
gh issue list --label copilot
```

## Support

For questions or issues:
1. Check CHANGELOG.md for recent changes
2. Review workflow run logs for failures
3. Create an issue with appropriate labels
4. Tag with `claude` if additional AI assistance is needed or if working on issues from `claude`
5. Reference upstream repository documentation for OSDU-specific guidance