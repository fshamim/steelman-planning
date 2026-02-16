Create an agent team for a steelman plan-critique debate loop. Here is the problem/goal:

$ARGUMENTS

Spawn two teammates:

1. STEELMAN-PLANNER: Use the steelman-planner agent. Its job is to build the initial plan and iteratively improve it by steelmanning critique before incorporating it. It should message the critic directly.

2. STEELMAN-CRITIC: Use the steelman-critic agent. Its job is to steelman the plan's strengths first, then find genuine weaknesses that survive the steelman test, and message critique directly to the planner.

DEBATE PROTOCOL:
- The planner builds Plan v1 and messages it to the critic
- The critic steelmans the plan, critiques it, rates severity, and messages back to the planner
- The planner steelmans the critique, improves the plan, and messages the updated version back to the critic
- They continue this direct debate loop
- When the critic rates severity at 3 or below, both agents message you (the lead) with the final plan

YOUR ROLE AS LEAD:
- Monitor the debate in the shared task list
- If the agents haven't converged after 3 rounds of exchange, step in and tell them to wrap up — the planner should present the best current version
- Once you receive the final plan, synthesize it and present it to me with a brief summary of how the debate evolved, which critique points were most impactful, and the final severity rating
- Do not interfere with the debate unless it stalls or goes off track
