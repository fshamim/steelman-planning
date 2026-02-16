# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository defines a **steelman plan-critique debate system** using Claude Code's agent team infrastructure. It has no application code — only agent and command configurations.

## Architecture

The system implements a two-agent debate loop orchestrated by a team lead:

- **steelman-planner** (`.claude/agents/steelman-planner.md`): Builds plans, steelmans incoming critique, and iteratively improves the plan. Uses Opus model.
- **steelman-critic** (`.claude/agents/steelman-critic.md`): Steelmans plan strengths first, then identifies genuine weaknesses that survive the steelman test. Rates severity 1-10. Uses Opus model.
- **steelman-debate** (`.claude/commands/steelman-debate.md`): Slash command (`/steelman-debate`) that spawns both agents as a team. The lead monitors convergence and intervenes if agents haven't converged after 3 rounds.

## Debate Protocol

1. Planner builds Plan v1, messages it to critic
2. Critic steelmans strengths, critiques weaknesses, rates severity, messages planner
3. Planner steelmans critique, triages points (incorporate/partially address/set aside), produces updated plan
4. Loop continues until critic rates severity ≤ 3, at which point both agents notify the lead
5. Lead synthesizes the final plan and presents it to the user

## Usage

Invoke with: `/steelman-debate <problem or goal description>`

## Output Rules

When a debate converges, the lead must save the **complete final plan** to Tasks.md — not a summary. This includes all phases, steps, code snippets, configs, and verification commands exactly as produced by the planner. Alongside the full plan, include a **summarized debate history** table showing rounds, severity ratings, and key changes per round. Never reduce the final plan to bullet-point summaries.

## Project Rules

- Tasks should be tracked in Tasks.md
- Never push changes to GitHub without explicit user approval
