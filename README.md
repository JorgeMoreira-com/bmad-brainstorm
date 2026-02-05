# BMAD Brainstorm — Claude Code Plugin

Software development brainstorming facilitator with **18 proven techniques** organized into 4 categories. Every interaction uses structured questions with multiple-choice options — no free-form prompts.

## Installation

```bash
# Add the marketplace
/plugin marketplace add JorgeMoreira-com/bmad-brainstorm

# Install the plugin
/plugin install bmad-brainstorm@bmad-brainstorm-marketplace
```

## Usage

Skills are namespaced under the plugin name:

```bash
/bmad-brainstorm:brainstorm                  # Full interactive setup
/bmad-brainstorm:brainstorm <topic>          # Skip setup, use topic directly
/bmad-brainstorm:brainstorm continue         # Resume the most recent session
/bmad-brainstorm:brainstorm five-whys        # Jump to a specific technique
```

## The 18 Techniques

### Analytical (root cause & constraints)
| # | Technique | Best For |
|---|-----------|----------|
| 1 | **Five Whys** | Root cause analysis, debugging persistent failures |
| 2 | **Constraint Mapping** | Identifying real vs. assumed limitations |
| 3 | **Failure Analysis** | Post-mortems, pre-mortems, incident review |
| 4 | **Assumption Reversal** | Challenging "obvious" technical decisions |

### Structured Frameworks (systematic exploration)
| # | Technique | Best For |
|---|-----------|----------|
| 5 | **SCAMPER Method** | Improving existing features through 7 lenses |
| 6 | **Six Thinking Hats** | Evaluating proposals from 6 perspectives |
| 7 | **Morphological Analysis** | Exploring parameter combinations |
| 8 | **Decision Tree Mapping** | Architecture decisions with branching paths |
| 9 | **Solution Matrix** | Comparing approaches across criteria |
| 10 | **Resource Constraints** | MVP thinking, building under tight limits |

### Divergent Thinking (idea generation)
| # | Technique | Best For |
|---|-----------|----------|
| 11 | **First Principles Thinking** | Rebuilding from fundamentals |
| 12 | **What If Scenarios** | Edge cases, scaling thought experiments |
| 13 | **Reverse Brainstorming** | "How could this fail?" → flip to solutions |
| 14 | **Anti-Solution** | Adversarial thinking, finding what breaks |
| 15 | **Provocation Technique** | Extreme statements to extract principles |
| 16 | **Question Storming** | Generate questions before seeking answers |

### Perspective Shifting
| # | Technique | Best For |
|---|-----------|----------|
| 17 | **Role Playing** | User personas, stakeholder analysis |
| 18 | **Chaos Engineering** | "What if X broke?" resilience scenarios |

## How It Works

1. **Setup** — Describe your topic and goal via structured questions
2. **Technique Selection** — Browse the library, get AI recommendations, random pick, or progressive flow
3. **Facilitation** — Step-by-step guided technique execution using multiple-choice questions
4. **Organization** — Cluster ideas, prioritize, and define action items

All session output is saved to `brainstorm-sessions/YYYY-MM-DD-<topic>.md`.

## Session Continuity

Sessions are automatically saved as markdown files. Use `/bmad-brainstorm:brainstorm continue` to resume where you left off. The facilitator detects your progress and picks up from the right phase.

## Coexistence

This plugin uses the skill name `brainstorm` (not `brainstorming`), so it coexists with other brainstorming skills without conflict.

## License

MIT
