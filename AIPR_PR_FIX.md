# AIPR PR Command Syntax Fix

This branch contains the fix for AIPR PR command syntax issues.

The main change is updating the command from:
`aipr -t fork_upstream --vulns -p meta -m $LLM_MODEL --max-diff-lines $MAX_DIFF_LINES`

To:
`aipr pr -t fork_upstream --vulns -p meta`

This resolves PR description generation failures in the meta commit strategy.
