# Agent Workflow: Working a Linear Issue

Standard operating procedure for agents assigned a Linear ticket. Follow every step in order.

---

## The Loop

### 1. Read the ticket
```
/linear-issue PROJ-XX
```
Read the full briefing: status, description, checklist, sub-issues, comments, and relations. Do not start planning until you've read it.

### 2. Discover relevant skills
Before planning, check whether any installed skills apply to this task:
```
/find-skills [task type]
```
Examples: `find-skills browser testing`, `find-skills UI component`, `find-skills API design`. If a skill covers part of the work, use it — don't reinvent the wheel.

### 3. Plan
For non-trivial work, enter plan mode. Explore the codebase, map dependencies, and get approval before writing code. Skip plan mode only for small, well-defined changes (single file, obvious fix).

### 4. Execute
Do the work. Commit incrementally with clear messages. Stay within the scope of the ticket — if you discover out-of-scope work, see [Filing new issues](#filing-new-issues), don't absorb it silently.

### 5. Simplify
```
/simplify
```
Review all changed code for reuse, quality, and efficiency. Fix anything found before moving on.

### 6. Test and verify
Run tests. Verify every acceptance criterion listed in the ticket's checklist or description. If the ticket references a playbook or spec, check against it.

### 7. Browser test (UI work only)
If the work produces HTML or visual output:
```
/dogfood
```
Systematically test the UI. Document any issues found.

### 8. Check off the checklist
```
/linear-issue check PROJ-XX all
```
Only run this after all acceptance criteria are genuinely met.

### 9. Close the ticket
```
/linear-issue PROJ-XX status:done
```

### 10. Prime the next ticket
```
/linear-issue comment PROJ-NEXT "Handoff: <what you did, what to watch for, any loose ends>"
```
Be specific. The next agent has no context beyond what's in Linear.

### 11. File anything new
See [Filing new issues](#filing-new-issues).

---

## When Blocked

**Blocked by an external dependency** (another issue, a decision, missing access):
1. Create a blocking issue: `/linear-issue <description>`
2. Set the current issue to Blocked: `/linear-issue PROJ-XX status:blocked`
3. Leave a comment explaining what's needed and who needs to act

**Blocked by uncertainty** (don't know how to proceed, requirements are ambiguous):
1. Leave a comment on the ticket describing the specific question
2. Set the ticket to Blocked
3. Do not create noise tickets for things you can resolve with a bit more research — investigate first

---

## Test Failures

**Fix inline** when:
- The failure is directly caused by your change
- The fix is obvious and small (< ~20 min)
- The fix doesn't touch unrelated code

**File a bug ticket** when:
- The failure exists independently of your change (pre-existing)
- The fix would take significant investigation or touches unrelated systems
- The failure is in a dependency you don't own

When filing a bug ticket, link it as blocking the current issue and set the current issue to Blocked.

---

## Filing New Issues

Use `/linear-issue` to file any of the following discovered during work:

| Discovery | Action |
|---|---|
| Bug unrelated to current work | New issue, Bug label, link as related |
| Scope creep (valid but out of scope) | New issue, reference current ticket |
| Test gap (missing coverage) | New issue, Test label |
| Follow-up improvement | New issue, Improvement label, add to backlog |

Do not absorb scope creep silently. Do not skip filing bugs because "it's minor". The ticket list is the source of truth.
