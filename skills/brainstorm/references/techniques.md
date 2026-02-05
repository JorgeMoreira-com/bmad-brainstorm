# Brainstorm Techniques Reference

> This reference is loaded by the brainstorm skill during technique browsing and facilitation.
> Each technique includes AskUserQuestion patterns that the facilitator follows step-by-step.

---

## Analytical Techniques

*Root cause analysis, constraints, and critical examination of assumptions.*

### 1. Five Whys

**Use for:** Root cause analysis, debugging persistent failures, understanding why systems behave unexpectedly, post-incident investigation.

**Example:** A deploy pipeline keeps failing → Why? Tests timeout → Why? Database connection pool exhausted → Why? Connection leak in new ORM migration → Why? Missing cleanup in transaction wrapper → Why? No integration test for connection lifecycle. Root cause: missing test coverage for resource cleanup.

**Facilitation Steps:**

1. **Define the problem.** AskUserQuestion — header: "Problem", question: "What specific problem or unexpected behavior are you investigating?"
   - Options: Bug/defect / Performance issue / System failure / Unexpected behavior

2. **Why #1.** AskUserQuestion — header: "Why 1", question: "Why does [stated problem] occur? What's the most immediate cause?"
   - Options: Generate 3-4 contextual options from the user's problem description, plus "Something else"

3. **Why #2.** AskUserQuestion — header: "Why 2", question: "Why does [cause from Why #1] happen?"
   - Options: Derived from previous answer — dig one layer deeper

4. **Why #3.** AskUserQuestion — header: "Why 3", question: "Why does [cause from Why #2] happen?"
   - Options: Continue drilling — look for systemic or structural causes

5. **Why #4-5.** Continue the pattern until the user identifies a root cause that feels actionable. Typically 4-5 levels deep.

6. **Solution.** AskUserQuestion — header: "Fix", question: "What type of solution addresses this root cause?"
   - Options: Fix at source / Add safeguard/test / Redesign component / Add monitoring & alerting

---

### 2. Constraint Mapping

**Use for:** Identifying technical limitations, dependency analysis, capacity planning, finding hidden design space by understanding what's truly fixed vs. assumed.

**Example:** "We can't add real-time features" → Is that a real constraint (no WebSocket support in infra) or assumed (nobody's tried it)? Mapping constraints reveals the actual design space is larger than believed.

**Facilitation Steps:**

1. **Constraint type.** AskUserQuestion — header: "Type", question: "What kind of constraints are you working within?"
   - Options: Technical/infrastructure / Resource/team / Time/deadline / Business/compliance
   - multiSelect: true

2. **List constraints.** AskUserQuestion — header: "List", question: "Within [selected types], what specific constraints do you face?"
   - Options: Generate 3-4 common constraints for the selected types, plus "Let me describe one"

3. **Real vs. assumed.** AskUserQuestion — header: "Verify", question: "For each constraint — is it verified/real or assumed/untested?"
   - Options: Present each listed constraint with "Real" / "Assumed" / "Not sure"
   - multiSelect: true

4. **Challenge assumptions.** AskUserQuestion — header: "Challenge", question: "For assumed constraints, what would change if we removed them?"
   - Options: Opens new architecture / Simplifies implementation / Enables feature X / Negligible impact

5. **Design within truth.** AskUserQuestion — header: "Approach", question: "Given only the real constraints, what approaches become possible?"
   - Options: Generate from the opened design space

---

### 3. Failure Analysis

**Use for:** Post-mortems, pre-mortems, incident review, learning from production failures, building resilience.

**Example:** API outage post-mortem → What failed? Auth service timeout cascade → What was the detection gap? No alerts on p99 latency → What's the systemic issue? Single point of failure in auth, no circuit breaker.

**Facilitation Steps:**

1. **Failure scope.** AskUserQuestion — header: "Scope", question: "What kind of failure are you analyzing?"
   - Options: Past incident (post-mortem) / Potential failure (pre-mortem) / Pattern of recurring issues / Near-miss that was caught

2. **Timeline.** AskUserQuestion — header: "Timeline", question: "Walk through the sequence — what happened first, and what cascaded?"
   - Options: Present timeline phases: Trigger → Detection → Response → Resolution → Recovery

3. **Detection gap.** AskUserQuestion — header: "Detection", question: "How was the failure detected, and what was the gap between occurrence and detection?"
   - Options: Monitoring caught it / User reported / Found during deploy / Discovered accidentally

4. **Root cause category.** AskUserQuestion — header: "Cause", question: "What category does the root cause fall into?"
   - Options: Code defect / Configuration error / Infrastructure failure / Process gap / Missing test coverage

5. **Systemic lessons.** AskUserQuestion — header: "Lesson", question: "What systemic improvement prevents this class of failure?"
   - Options: Add automated test / Improve monitoring / Add redundancy / Change process / Improve documentation

---

### 4. Assumption Reversal

**Use for:** Challenging "obvious" technical decisions, questioning inherited architecture, finding innovation by inverting beliefs.

**Example:** "The frontend must be a SPA" → What if it were server-rendered? Multi-page with HTMX? Static with progressive enhancement? Each reversal opens different architectural possibilities.

**Facilitation Steps:**

1. **Surface assumptions.** AskUserQuestion — header: "Assumptions", question: "What are the 'obvious' truths or established beliefs about your system/project?"
   - Options: Architecture pattern is X / We must use technology Y / Users need feature Z / Performance requires approach W

2. **Pick one to reverse.** AskUserQuestion — header: "Reverse", question: "Which assumption would be most interesting to flip?"
   - Options: List the assumptions the user identified

3. **Explore the reversal.** AskUserQuestion — header: "Explore", question: "If [reversed assumption] were true, what would change about your approach?"
   - Options: Completely different architecture / Simpler implementation / New capabilities / Breaks everything (explore why)

4. **Extract value.** AskUserQuestion — header: "Value", question: "Even if the full reversal is impractical, what useful insight does it reveal?"
   - Options: Hybrid approach possible / Current approach over-engineered / Missing a simpler alternative / Confirms current choice is right

---

## Structured Frameworks

*Systematic exploration using established methodologies.*

### 5. SCAMPER Method

**Use for:** Systematically improving existing features, APIs, or workflows by examining them through 7 lenses.

**SCAMPER:** Substitute / Combine / Adapt / Modify / Put to other uses / Eliminate / Reverse

**Example:** Improving a REST API → **Substitute:** Replace polling with WebSockets? **Combine:** Merge user+profile endpoints? **Adapt:** Borrow GraphQL's field selection? **Modify:** Batch endpoint for mobile? **Put to other uses:** Open as public API? **Eliminate:** Remove deprecated v1 endpoints? **Reverse:** Client-driven schema?

**Facilitation Steps:**

1. **Target.** AskUserQuestion — header: "Target", question: "What existing feature, system, or workflow do you want to improve?"
   - Options: API/endpoint / UI component / Workflow/process / Data model / Developer experience

2. **Substitute.** AskUserQuestion — header: "Substitute", question: "What component, technology, or approach could you replace with something else?"
   - Options: Generate contextual substitution suggestions

3. **Combine.** AskUserQuestion — header: "Combine", question: "What could you merge or integrate that's currently separate?"
   - Options: Generate contextual combination suggestions

4. **Adapt.** AskUserQuestion — header: "Adapt", question: "What idea from another domain, product, or system could you borrow?"
   - Options: From competitor / From different industry / From open source / From internal tool

5. **Modify/Eliminate/Reverse.** AskUserQuestion — header: "Transform", question: "Looking at the remaining lenses — what could you magnify, eliminate, or reverse?"
   - Options: Scale up a feature / Remove complexity / Reverse a flow or dependency / Rearrange the order

6. **Best ideas.** AskUserQuestion — header: "Select", question: "Which SCAMPER ideas are most promising?"
   - Options: Present the ideas generated across lenses
   - multiSelect: true

---

### 6. Six Thinking Hats

**Use for:** Evaluating a proposal, feature, or architecture decision from 6 distinct perspectives to avoid groupthink.

**Hats:** White (Facts) / Red (Feelings) / Yellow (Benefits) / Black (Risks) / Green (Creativity) / Blue (Process)

**Facilitation Steps:**

1. **Subject.** AskUserQuestion — header: "Subject", question: "What decision, proposal, or design are you evaluating?"
   - Options: New feature / Architecture change / Technology choice / Process change

2. **White Hat — Facts.** AskUserQuestion — header: "Facts", question: "What do we know for certain? What data, metrics, or evidence exists?"
   - Options: Have metrics / Have user feedback / Have benchmarks / Mostly assumptions

3. **Red Hat — Gut feelings.** AskUserQuestion — header: "Feelings", question: "What's your instinct about this? What excites or worries you?"
   - Options: Excited — feels right / Uneasy — something's off / Mixed — see both sides / Neutral — need more info

4. **Yellow Hat — Benefits.** AskUserQuestion — header: "Benefits", question: "What are the best possible outcomes if this succeeds?"
   - Options: Generate 3-4 contextual benefits

5. **Black Hat — Risks.** AskUserQuestion — header: "Risks", question: "What could go wrong? What are the risks and downsides?"
   - Options: Technical risk / Timeline risk / User adoption risk / Maintenance burden

6. **Green Hat — Alternatives.** AskUserQuestion — header: "Creative", question: "What creative alternatives or modifications haven't been considered?"
   - Options: Generate from gaps identified in previous hats

7. **Blue Hat — Decision.** AskUserQuestion — header: "Decision", question: "Given all perspectives, what's your decision or next step?"
   - Options: Proceed as planned / Modify approach / Investigate further / Reject and try alternative

---

### 7. Morphological Analysis

**Use for:** Exploring combinations of independent design parameters to discover novel solutions — great for API design, feature configuration, or architecture composition.

**Example:** Designing a notification system → Parameters: Channel (email/push/SMS), Trigger (event/schedule/threshold), Content (template/dynamic/AI), Priority (immediate/batched/digest). Combinations reveal options like "AI-generated push notification triggered by threshold, delivered as digest."

**Facilitation Steps:**

1. **Define parameters.** AskUserQuestion — header: "Parameters", question: "What are the independent design dimensions or parameters for your system?"
   - Options: Generate 3-4 likely parameters from context, plus "Add custom parameter"

2. **Values per parameter.** For each parameter, AskUserQuestion — header: "[Param name]", question: "What are the possible values for [parameter]?"
   - Options: Generate 3-4 values per parameter

3. **Interesting combinations.** AskUserQuestion — header: "Combine", question: "Which parameter combinations seem most promising or surprising?"
   - Options: Present 4-5 notable combinations from the matrix
   - multiSelect: true

4. **Evaluate.** AskUserQuestion — header: "Evaluate", question: "For selected combinations — what are the trade-offs?"
   - Options: High value + feasible / Innovative but risky / Simple but limited / Complex but comprehensive

---

### 8. Decision Tree Mapping

**Use for:** Architecture decisions with branching consequences, technology selection, migration planning — anywhere choices create divergent paths.

**Facilitation Steps:**

1. **Decision point.** AskUserQuestion — header: "Decision", question: "What's the key decision you're facing?"
   - Options: Technology choice / Architecture pattern / Build vs. buy / Migration strategy

2. **Options.** AskUserQuestion — header: "Options", question: "What are the main options available?"
   - Options: Generate 3-4 from context

3. **For each option — consequences.** AskUserQuestion — header: "If [option]", question: "If you choose [option], what's the next decision it creates?"
   - Options: Contextual second-order decisions

4. **Criteria.** AskUserQuestion — header: "Criteria", question: "What criteria matter most for this decision?"
   - Options: Performance / Developer experience / Time to market / Long-term maintainability
   - multiSelect: true

5. **Score.** AskUserQuestion — header: "Winner", question: "Given your criteria, which path looks strongest?"
   - Options: Present options with summary of downstream consequences

---

### 9. Solution Matrix

**Use for:** Comparing multiple approaches, technology stacks, or vendors across consistent criteria.

**Facilitation Steps:**

1. **Define solutions.** AskUserQuestion — header: "Solutions", question: "What solutions or approaches are you comparing?"
   - Options: Generate from context, 3-4 options

2. **Define criteria.** AskUserQuestion — header: "Criteria", question: "What criteria should you evaluate against?"
   - Options: Performance / Cost / Complexity / Team expertise / Community support / Scalability
   - multiSelect: true

3. **Rate each.** For each solution × criterion, AskUserQuestion — header: "[Solution]", question: "How does [solution] rate on [criterion]?"
   - Options: Strong / Adequate / Weak / Unknown

4. **Weights.** AskUserQuestion — header: "Weights", question: "Which criteria matter most?"
   - Options: Present criteria for ranking

5. **Decision.** AskUserQuestion — header: "Result", question: "Based on the matrix, which solution wins?"
   - Options: Present solutions ranked by weighted score

---

### 10. Resource Constraints

**Use for:** MVP thinking, building under tight resource limits, efficiency optimization, doing more with less.

**Facilitation Steps:**

1. **Constraint type.** AskUserQuestion — header: "Limits", question: "What's the primary constraint you're designing around?"
   - Options: Time (deadline) / Budget (cost) / Team size / Technical capability

2. **Scope.** AskUserQuestion — header: "Scope", question: "What's the full scope of what you'd like to build?"
   - Options: Present feature categories for the user to describe

3. **Must-have vs. nice-to-have.** AskUserQuestion — header: "Priority", question: "Which capabilities are absolutely essential?"
   - Options: Present features from scope description
   - multiSelect: true

4. **Creative constraints.** AskUserQuestion — header: "Creative", question: "Given only the must-haves and your constraint, what creative shortcuts exist?"
   - Options: Use existing library / Simplify UX / Reduce scope further / Leverage managed service

5. **Plan.** AskUserQuestion — header: "Plan", question: "What's your constrained-but-viable plan?"
   - Options: Present synthesized approach options

---

## Divergent Thinking

*Breaking patterns, generating volume, exploring the edges.*

### 11. First Principles Thinking

**Use for:** Rebuilding understanding from fundamentals, questioning inherited complexity, designing elegant solutions by stripping away accumulated assumptions.

**Example:** "We need a microservices architecture" → First principle: we need independent deployability and team autonomy → Could also achieve with modular monolith, or serverless, or module federation.

**Facilitation Steps:**

1. **Current approach.** AskUserQuestion — header: "Current", question: "What's the current approach or conventional wisdom you want to examine?"
   - Options: Architecture pattern / Technology choice / Process/workflow / Feature design

2. **Strip to fundamentals.** AskUserQuestion — header: "Fundamentals", question: "What is the actual underlying need or problem this serves?"
   - Options: Guide user to articulate the core need without referencing specific solutions

3. **What's truly required?** AskUserQuestion — header: "Required", question: "From first principles, what properties must the solution have?"
   - Options: Generate fundamental requirements (not implementation-specific)

4. **Rebuild.** AskUserQuestion — header: "Rebuild", question: "Starting only from these requirements, what solutions are possible?"
   - Options: Present 3-4 different approaches that satisfy the fundamental requirements

5. **Compare.** AskUserQuestion — header: "Compare", question: "How does this first-principles solution compare to the conventional approach?"
   - Options: Simpler / More complex but better / About the same / Reveals hybrid opportunity

---

### 12. What If Scenarios

**Use for:** Edge case exploration, scaling thought experiments, stress-testing designs, future-proofing architecture.

**Facilitation Steps:**

1. **System.** AskUserQuestion — header: "System", question: "What system or design do you want to stress-test?"
   - Options: Current architecture / Proposed design / Specific feature / Data model

2. **Scale what-if.** AskUserQuestion — header: "Scale", question: "What if usage grew 10x/100x/1000x? What breaks first?"
   - Options: Database / API throughput / State management / Cost / User experience

3. **Failure what-if.** AskUserQuestion — header: "Failure", question: "What if [critical component] went down for 24 hours?"
   - Options: Present key components as failure candidates

4. **Change what-if.** AskUserQuestion — header: "Change", question: "What if a core requirement changed dramatically?"
   - Options: New platform / Different user base / Regulatory change / Technology shift

5. **Insights.** AskUserQuestion — header: "Insights", question: "What did these scenarios reveal about your design?"
   - Options: Resilient as-is / Needs specific hardening / Fundamental redesign needed / Reveals new requirements

---

### 13. Reverse Brainstorming

**Use for:** Finding vulnerabilities by asking "How could we make this fail?" then flipping solutions — surprisingly effective for security, UX, and reliability.

**Facilitation Steps:**

1. **Goal.** AskUserQuestion — header: "Goal", question: "What system or experience do you want to improve?"
   - Options: User onboarding / API reliability / Developer experience / Security posture

2. **Reverse: how to break it.** AskUserQuestion — header: "Break it", question: "How could you make [goal] as bad as possible? Think adversarially."
   - Options: Generate 3-4 "worst case" approaches — intentionally terrible ideas

3. **More ways to fail.** AskUserQuestion — header: "More", question: "What other ways could this go wrong?"
   - Options: Present additional failure modes

4. **Flip to solutions.** AskUserQuestion — header: "Flip", question: "Now reverse each failure mode — what's the opposite solution?"
   - Options: Present the inverted solutions derived from failure modes

5. **Prioritize.** AskUserQuestion — header: "Priority", question: "Which flipped solutions have the most impact?"
   - Options: Present solutions for ranking
   - multiSelect: true

---

### 14. Anti-Solution

**Use for:** Adversarial thinking — intentionally design the worst possible version to discover hidden risks, security holes, and fragility points.

**Facilitation Steps:**

1. **Target.** AskUserQuestion — header: "Target", question: "What system are you stress-testing with adversarial thinking?"
   - Options: Authentication / Data pipeline / API / User workflow / Infrastructure

2. **Design the worst version.** AskUserQuestion — header: "Worst", question: "If you wanted this system to be insecure, unreliable, and frustrating — what would you do?"
   - Options: Generate deliberately terrible design choices

3. **Identify real risks.** AskUserQuestion — header: "Real risks", question: "Which of these 'anti-patterns' are actually present (even partially) in your current system?"
   - Options: Present anti-patterns with "Yes, partially" / "No" / "Not sure"
   - multiSelect: true

4. **Defenses.** AskUserQuestion — header: "Defend", question: "For each identified risk, what's the defense?"
   - Options: Generate defensive measures for each confirmed risk

---

### 15. Provocation Technique

**Use for:** Making deliberately provocative or extreme statements to jolt thinking out of conventional patterns — then extracting the useful principle behind the provocation.

**Example:** "What if we had zero tests?" → Provokes thought about what tests actually provide → Leads to insight about confidence, documentation, and refactoring safety → Maybe leads to better test strategy.

**Facilitation Steps:**

1. **Topic.** AskUserQuestion — header: "Topic", question: "What area do you want to think provocatively about?"
   - Options: Testing strategy / Architecture / Team process / Feature priorities

2. **Provocation.** Present a deliberately extreme statement about the topic, then AskUserQuestion — header: "React", question: "Here's a provocation: '[extreme statement]'. What's your immediate reaction?"
   - Options: That's absurd because... / Actually there's a grain of truth / It reveals an assumption / It makes me think about...

3. **Extract principle.** AskUserQuestion — header: "Principle", question: "What useful principle or insight hides behind this provocation?"
   - Options: Generate 3-4 extracted principles

4. **Apply.** AskUserQuestion — header: "Apply", question: "How could you apply this principle practically?"
   - Options: Generate practical applications of the extracted principle

---

### 16. Question Storming

**Use for:** When you're stuck — generate questions instead of answers. Often the reason you're stuck is you're answering the wrong question.

**Facilitation Steps:**

1. **Topic.** AskUserQuestion — header: "Topic", question: "What problem or area are you stuck on?"
   - Options: Technical challenge / Design decision / Strategic direction / Team/process issue

2. **Rapid questions.** AskUserQuestion — header: "Questions", question: "What questions come to mind about this topic? List as many as possible."
   - Options: Why is this hard? / What don't we know? / Who has solved this before? / What are we assuming?
   - multiSelect: true

3. **Question quality.** AskUserQuestion — header: "Best Q", question: "Which questions feel most important or revealing?"
   - Options: Present user's questions for ranking

4. **Reframe.** AskUserQuestion — header: "Reframe", question: "Can the top question be reframed to open new possibilities?"
   - Options: Generate 3-4 reframings of the selected question

5. **Answer the right question.** AskUserQuestion — header: "Answer", question: "Now that you have the right question — what answers emerge?"
   - Options: Generate answer directions based on the reframed question

---

## Perspective Shifting

*Seeing the problem through different eyes.*

### 17. Role Playing

**Use for:** User persona analysis, stakeholder mapping, understanding different perspectives on a feature or system design.

**Facilitation Steps:**

1. **Context.** AskUserQuestion — header: "Context", question: "What feature, system, or decision do you want to examine from different perspectives?"
   - Options: New feature / Existing system / API design / Process change

2. **Choose roles.** AskUserQuestion — header: "Roles", question: "Which perspectives would be most valuable?"
   - Options: End user (non-technical) / Developer consuming the API / Operations/SRE team / New team member / Product manager
   - multiSelect: true

3. **Role 1 perspective.** AskUserQuestion — header: "[Role]", question: "As a [role], what matters most about this? What concerns you?"
   - Options: Generate role-specific concerns and priorities

4. **Role 2+ perspectives.** Repeat for each selected role.

5. **Conflicts.** AskUserQuestion — header: "Conflicts", question: "Where do these perspectives conflict?"
   - Options: Present identified tensions between roles

6. **Resolution.** AskUserQuestion — header: "Resolve", question: "How do you balance or resolve these conflicting needs?"
   - Options: Prioritize [role] / Find compromise / Phase the approach / Accept trade-off

---

### 18. Chaos Engineering (Thought Experiment)

**Use for:** Resilience thinking — "What if X broke?" scenarios to identify single points of failure, missing fallbacks, and recovery gaps. This is the brainstorming version, not actual chaos testing.

**Facilitation Steps:**

1. **System.** AskUserQuestion — header: "System", question: "What system do you want to chaos-test mentally?"
   - Options: Production infrastructure / Data pipeline / Authentication / External dependencies

2. **Pick a component to break.** AskUserQuestion — header: "Break", question: "What component should we imagine failing?"
   - Options: Generate critical components from the described system

3. **Blast radius.** AskUserQuestion — header: "Blast", question: "If [component] fails, what's affected? What cascades?"
   - Options: Full outage / Degraded experience / Data loss risk / Silent corruption / Nothing (isolated)

4. **Detection.** AskUserQuestion — header: "Detect", question: "How would you know [component] has failed?"
   - Options: Monitoring alerts / User reports / Automated health check / You wouldn't know

5. **Recovery.** AskUserQuestion — header: "Recover", question: "What's the recovery path?"
   - Options: Automatic failover / Manual intervention / Restart/redeploy / Restore from backup / No recovery plan

6. **Harden.** AskUserQuestion — header: "Harden", question: "What would make this component more resilient?"
   - Options: Add redundancy / Improve monitoring / Circuit breaker / Graceful degradation / Better backups
