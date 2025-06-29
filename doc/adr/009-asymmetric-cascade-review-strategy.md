# ADR-009: Asymmetric Cascade Review Strategy

## Status
Accepted  
**Revised** - 2025-06-29

## Context
The cascade workflow moves upstream changes through a three-branch hierarchy:
1. `fork_upstream` → `fork_integration` 
2. `fork_integration` → `main`

With the implementation of human-centric cascade triggering (ADR-019) and issue lifecycle tracking (ADR-022), we needed to balance automation efficiency with safety, ensuring that upstream changes are properly vetted before reaching production while minimizing manual intervention where safe.

Key considerations:
- Upstream changes are external and potentially breaking
- Integration branch serves as a testing ground
- Main branch is production and must remain stable
- Manual cascade triggering provides explicit human control
- Conflict resolution always requires human intervention
- Issue tracking provides visibility into review status

## Decision
We will implement an asymmetric review strategy for cascade PRs:

1. **Fork_upstream → Fork_integration**: Human-initiated with tracking
   - Triggered manually by humans after reviewing upstream sync PR
   - Issue lifecycle tracking provides visibility into integration status
   - Conflicts are most likely to occur here
   - Human judgment needed to assess upstream impact

2. **Fork_integration → Main**: Eligible for auto-merge when ALL conditions are met:
   - No conflicts detected
   - All CI checks pass
   - Diff size < 1000 lines
   - No breaking changes (detected via commit messages)
   - Changes already validated in integration branch

## Consequences

### Positive
- **Safety First**: External changes get human review at entry point
- **Efficiency**: Clean, tested changes flow automatically to production
- **Clear Boundaries**: Integration branch serves its purpose as a validation gate
- **Reduced Latency**: Second phase can complete without waiting for reviewers
- **Risk Mitigation**: Large or breaking changes always get manual review

### Negative
- **Asymmetry Complexity**: Different rules for different stages may confuse
- **First-Stage Bottleneck**: All upstream changes need manual review
- **Auto-merge Risk**: Even with safeguards, automated merges carry inherent risk

### Neutral
- **Monitoring Required**: Need to track auto-merge success rates
- **Tunable Parameters**: Diff size threshold can be adjusted based on experience
- **Override Capability**: Can disable auto-merge via environment variables

## Implementation Details

### Phase 1 (Human-Initiated Integration)
```yaml
# Humans manually trigger cascade after reviewing sync PR
# Cascade workflow updates issue tracking
gh issue edit "$ISSUE_NUMBER" \
  --remove-label "human-required" \
  --add-label "cascade-active"

# Integration proceeds with conflict detection
# If conflicts detected, issue updated to cascade-blocked
```

### Phase 2 (Conditionally Automatic)
```yaml
# Create production PR from fork_integration to main
MAIN_BRANCH="fork_integration"
PR_URL=$(gh pr create \
  --base main \
  --head $MAIN_BRANCH \
  --title "🚀 Production Release: Upstream Integration - $(date +%Y-%m-%d)" \
  --body "$PR_BODY" \
  --label "upstream-sync,production-ready,cascade-active,validated,human-required")

# Update tracking issue
gh issue edit "$TRACKING_ISSUE" \
  --remove-label "cascade-active" \
  --add-label "production-ready"

# Auto-merge eligibility based on size and breaking changes
if [[ "$DIFF_LINES" -lt 1000 ]] && [[ "$BREAKING_CHANGES" == "false" ]]; then
  gh pr merge $PR_NUMBER --auto --squash --delete-branch
  gh pr edit $PR_NUMBER --add-label "auto-merge-enabled"
else
  gh pr edit $PR_NUMBER --add-label "manual-review-required"
fi
```

## Alternatives Considered

1. **Fully Manual**: Require review at both stages
   - Rejected: Too slow, defeats automation purpose

2. **Fully Automated**: Auto-merge at both stages when clean
   - Rejected: Too risky for external changes

3. **Reversed Asymmetry**: Auto-merge first stage, manual second
   - Rejected: Backwards from a safety perspective

## Related
- [ADR-001: Three-Branch Fork Management Strategy](001-three-branch-strategy.md)
- [ADR-005: Automated Conflict Management Strategy](005-conflict-management.md)
- [ADR-019: Cascade Monitor Pattern](019-cascade-monitor-pattern.md) - Human-centric cascade triggering
- [ADR-022: Issue Lifecycle Tracking Pattern](022-issue-lifecycle-tracking-pattern.md) - Integration with issue tracking
- [Cascade Workflow Specification](../cascade-workflow.md)