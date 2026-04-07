# Operator Profile

This folder turns the agent system into a reflection of the operator's real expertise, stack, heuristics, and quality bar.

Use these files as the source of truth for personalization:

- `expertise-map.md`: domains of strength, depth, and confidence
- `stack-map.md`: preferred technologies, platforms, and tooling
- `decision-principles.md`: how to make trade-offs
- `anti-patterns.md`: what to avoid by default
- `operating-modes.md`: how the agent should behave for this operator

Rules:

1. Keep entries concrete and opinionated.
2. Prefer real stack over aspirational stack.
3. When preferences conflict with generic best practices, explain the trade-off.
4. Update these files as the operator evolves.

Expected outcome:

- Better routing
- Better architecture choices
- Fewer generic answers
- Less overengineering
- More consistent execution style
