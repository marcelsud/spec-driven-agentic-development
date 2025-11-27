---
description: Suggest the next feature to work on based on priority, dependencies, and completion status
allowed-tools: Read(*), Glob(*), Grep(*)
---

# Suggest Next Feature

Analyze all features and recommend which one to work on next based on priority, dependencies, and completion status.

## Your Task

Evaluate all features in the `features/` directory and provide a prioritized recommendation for which feature to implement next.

## Process

### Step 1: Discover All Features

Use `Glob` to find all feature directories:
```
Glob pattern: features/*/context.md
```

Extract feature names from the paths.

### Step 2: Analyze Each Feature

For each discovered feature, gather:

#### 2.1 Completion Status

Read `features/[feature-name]/tasks.md` and count:
- **Total tasks**: Match pattern `## Task \d+:` or `### Task \d+:`
- **Completed tasks**: Match pattern `\[IMPLEMENTED\]` or `\[COMPLETE\]`
- **Calculate percentage**: completed / total * 100

Categorize status:
| Percentage | Status |
|------------|--------|
| 0% | Not Started |
| 1-99% | In Progress |
| 100% | Complete |

#### 2.2 Priority Indicators

**From naming convention:**
- Extract numeric prefix (e.g., `01-feature-name` → priority 1)
- Features without prefix default to priority 99

**From context.md:**
- Look for "Priority:" or "priority:" mentions
- Look for keywords: "critical", "urgent", "blocker", "MVP", "required"

#### 2.3 Dependencies

Read `features/[feature-name]/context.md` Dependencies section.

Look for:
- Explicit mentions of other features
- Phrases like "depends on", "requires", "after", "needs"
- References to other feature names

Build a dependency map:
```
feature-a:
  depends_on: []
  blocks: [feature-b, feature-c]
feature-b:
  depends_on: [feature-a]
  blocks: [feature-d]
```

### Step 3: Calculate Recommendation Scores

For each **incomplete** feature (status != Complete), calculate a score:

```
score = (priority_score * 0.40) + (dependency_score * 0.35) + (progress_score * 0.25)
```

#### Priority Score (40% weight)
```
priority_score = 100 - (priority_number * 5)
```
- Priority 1 → 95 points
- Priority 2 → 90 points
- Priority 10 → 50 points
- Priority 99 (no prefix) → 5 points

#### Dependency Score (35% weight)
```
dependency_score = base + blocker_bonus - blocked_penalty
```
- **Base**: 50 points
- **Blocker bonus**: +10 points for each feature this blocks
- **Blocked penalty**: -30 points if depends on incomplete feature

Examples:
- No dependencies, blocks nothing → 50
- No dependencies, blocks 2 features → 70
- Depends on incomplete feature → 20 (blocked)

#### Progress Score (25% weight)

Reward momentum on in-progress features:
```
if status == "In Progress":
    progress_score = 50 + (completion_percentage * 0.5)
else:  # Not Started
    progress_score = 40
```
- Not started → 40 points
- In progress (30% done) → 65 points
- In progress (80% done) → 90 points

### Step 4: Generate Recommendation

Present findings in this format:

```markdown
## Next Feature Recommendation

### Recommended: [feature-name]

**Reason**: [Clear explanation of why this feature should be next]

| Metric | Value |
|--------|-------|
| Priority | [X] (from naming/context) |
| Progress | [X/Y tasks (Z%)] |
| Status | [Not Started / In Progress] |
| Dependencies | [None / Depends on: X / Blocks: Y, Z] |
| Score | [calculated score] |

---

### Alternative Options

Ranked by recommendation score:

| Rank | Feature | Priority | Progress | Blocks | Blocked By | Score |
|------|---------|----------|----------|--------|------------|-------|
| 1 | [recommended] | 01 | 30% | 3 | - | 87 |
| 2 | [alternative-1] | 02 | 0% | 1 | - | 72 |
| 3 | [alternative-2] | 03 | 50% | 0 | feature-1 | 45 |

---

### Dependency Map

Visual representation of feature dependencies:

```
[feature-1] (Complete)
    |
    v
[feature-2] ← RECOMMENDED (In Progress: 30%)
    |
    +---> [feature-3] (Blocked)
    |
    +---> [feature-4] (Blocked)

[feature-5] (Not Started, No dependencies)
```

---

### All Features Status

| Feature | Status | Progress | Priority | Dependencies |
|---------|--------|----------|----------|--------------|
| 01-project-setup | Complete | 5/5 (100%) | 01 | None |
| 02-user-auth | In Progress | 3/10 (30%) | 02 | None |
| 03-dashboard | Not Started | 0/8 (0%) | 03 | Needs: 02 |
| 04-api-endpoints | In Progress | 1/12 (8%) | 04 | Needs: 02 |
| 05-admin-panel | Not Started | 0/6 (0%) | 05 | Needs: 02, 03 |

---

### Action

To begin implementation:
```
/spec:execute [recommended-feature-name]
```
```

### Step 5: Handle Edge Cases

#### No Features Found
```
No features found in the `features/` directory.

Create your first feature with:
/spec:create [feature-description]
```

#### All Features Complete
```
All features are complete!

| Feature | Tasks |
|---------|-------|
| [list all] | [X/X (100%)] |

To add a new feature:
/spec:create [feature-description]
```

#### All Incomplete Features Blocked
```
## Blocked State Detected

All remaining features have unmet dependencies:

| Feature | Blocked By | Status of Blocker |
|---------|------------|-------------------|
| feature-b | feature-a | In Progress (50%) |
| feature-c | feature-a | In Progress (50%) |

### Recommended Action
Focus on completing **feature-a** to unblock other features.

/spec:execute feature-a
```

#### Single Feature Exists
```
## Next Feature Recommendation

Only one feature exists: **[feature-name]**

| Metric | Value |
|--------|-------|
| Status | [status] |
| Progress | [X/Y (Z%)] |

/spec:execute [feature-name]
```

## Example Output

```
## Next Feature Recommendation

### Recommended: 02-user-authentication

**Reason**: Highest priority incomplete feature with no blockers. Currently in progress with momentum. Blocks 3 other features - completing it will unblock the most work.

| Metric | Value |
|--------|-------|
| Priority | 02 |
| Progress | 3/10 tasks (30%) |
| Status | In Progress |
| Dependencies | None |
| Blocks | 03-dashboard, 04-api, 05-admin |
| Score | 87/100 |

---

### Alternative Options

| Rank | Feature | Priority | Progress | Blocks | Blocked By | Score |
|------|---------|----------|----------|--------|------------|-------|
| 1 | 02-user-authentication | 02 | 30% | 3 | - | 87 |
| 2 | 06-notifications | 06 | 0% | 0 | - | 52 |
| 3 | 03-dashboard | 03 | 0% | 2 | 02 | 35 |

---

### Dependency Map

```
[01-project-setup] (Complete)
    |
    v
[02-user-authentication] ← RECOMMENDED
    |
    +---> [03-dashboard] (Blocked)
    |         |
    |         +---> [05-admin-panel] (Blocked)
    |
    +---> [04-api-endpoints] (Blocked)

[06-notifications] (Independent)
```

---

### All Features Status

| Feature | Status | Progress | Priority |
|---------|--------|----------|----------|
| 01-project-setup | Complete | 5/5 (100%) | 01 |
| 02-user-authentication | In Progress | 3/10 (30%) | 02 |
| 03-dashboard | Not Started | 0/8 (0%) | 03 |
| 04-api-endpoints | Not Started | 0/12 (0%) | 04 |
| 05-admin-panel | Not Started | 0/6 (0%) | 05 |
| 06-notifications | Not Started | 0/4 (0%) | 06 |

---

### Action

/spec:execute 02-user-authentication
```
