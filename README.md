# Steelman Planning

A two-agent debate system for [Claude Code](https://docs.anthropic.com/en/docs/claude-code) that produces better plans by having AI agents argue with each other before you commit to anything.

One agent builds the plan. Another tries to break it. They go back and forth until the plan is solid.

## How it works

```
You: /steelman-debate <describe your problem or goal>

Claude Code spawns two agents in separate tmux panes:

  Planner                          Critic
  ────────                         ──────
  Builds Plan v1            ──→    Steelmans strengths first,
                                   then critiques weaknesses
                            ←──    Rates severity (1-10)
  Steelmans the critique,
  improves plan             ──→    Re-evaluates
                            ←──    ...

  Loop continues until severity ≤ 3, then you get the final plan.
```

Both agents steelman the other side's argument before responding. The planner must articulate why the critique is valid before deciding what to incorporate. The critic must acknowledge what the plan gets right before finding weaknesses.

## Setup

Requires [Claude Code](https://docs.anthropic.com/en/docs/claude-code) with agent teams enabled.

```bash
git clone <this-repo>
cd steelman-planning
claude
```

Then run:

```
/steelman-debate <your problem or goal>
```

## What's in the box

```
.claude/
  agents/
    steelman-planner.md   # Planner agent definition
    steelman-critic.md    # Critic agent definition
  commands/
    steelman-debate.md    # Slash command that orchestrates the debate
```

That's it. No application code. Just agent configs.

## Example

```
/steelman-debate design a migration plan from REST to GraphQL for our billing service
```

The planner builds a phased migration plan. The critic catches that the plan assumes backward compatibility without a versioning strategy, has no rollback path for the data layer, and underestimates client migration effort. Three rounds later you have a plan that accounts for all of that.

## What is steelmanning?

A steelman is the opposite of a strawman. Instead of misrepresenting the other side's argument to make it easier to attack, you represent it in its *strongest possible form* before responding. You assume the other person sees something you don't, and you articulate the best version of their point — even if you disagree.

In a debate context, this means the planner doesn't get to dismiss critique by attacking a weak version of it, and the critic doesn't get to tear down a plan by ignoring what actually works. Both sides have to do the hard work of understanding before responding.

## Why steelman for planning

Regular critique devolves into nitpicking. Steelmanning forces both sides to engage honestly:

- The **planner** must restate each critique in its strongest form before deciding to incorporate or set aside. No hand-waving.
- The **critic** must identify what the plan gets right before finding weaknesses. No drive-by negativity.

This produces plans that survive contact with reality instead of plans that just sound good.

## License

MIT
