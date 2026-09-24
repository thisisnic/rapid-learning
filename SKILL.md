---
name: rapid-learning
description: Help quickly learn new programming topics and concepts through structured, timeboxed activities with checkpoints. Use when you want to understand a new concept, explore a codebase, or learn a specific technique. Creates learning plans with hands-on activities, provides Socratic guidance, and saves progress for resuming later.
license: CC-BY-4.0
---

# Rapid Learning

A structured approach to learning programming concepts quickly, with an LLM acting as a tutor rather than a code generator. The aim is that the user gains a skill they can repeat, not just an answer for today.

The workflow follows the self-directed learning framework from Kim et al. (2014), as applied to LLM-assisted learning in Lin (2023). A worked example is at https://niccrane.com/posts/llms_for_learning/.

> Lin, X. (2023). Exploring the Role of ChatGPT as a Facilitator for Motivating Self-Directed Learning Among Adult Learners. *Adult Learning*. https://doi.org/10.1177/10451595231184928

## Core Philosophy

- **Tutor, not solver**: Learn through questions and discovery. Only hand over answers when asked.
- **Active, not passive**: Every activity has the user doing something, whether that's writing code, reading with a question in mind, or explaining back. Match the style to how the user says they learn best.
- **Timeboxed activities**: Prevent hyperfocus with clear time limits
- **Stretch zone**: Works best on tasks just outside current knowledge, hard enough to learn from but not so hard the user doubts they can finish
- **Adaptive structure**: Tailor activities to the topic, time available, and your knowledge level
- **Progress tracking**: Save sessions to resume later

## When to Use This Skill

This skill is ideal when you:
- Encounter a concept you want to understand better (e.g., "magic methods in Arrow")
- Need to learn something for a specific task you're working on
- Want to explore how something works in a codebase
- Have limited time and want focused, efficient learning
- Need structure to prevent getting lost in rabbit holes

## Workflow Overview

1. **Establish Learning Goals** → Define what you want to learn and why
2. **Locate and Access Resources** → Identify a minimal set of things to learn from
3. **Adopt and Execute Learning Activities** → Design and work through timeboxed, hands-on activities with Socratic support
4. **Monitor and Evaluate Performance** → Checkpoints and progress tracking, mostly within step 3
5. **Reassess Learning Strategies** → Reflect on what worked and record it for next time

Steps 1 to 3 are the bulk of a session. Steps 4 and 5 are lightweight. For small, one-off tasks, collapse steps 2 and 3: treat finding information as part of the activities rather than a separate phase.

## Step 1: Establish Learning Goals

### Initial Questions

Ask the user, **one question at a time**:
1. **What do you want to learn, and why?** (The specific concept/topic/technology, and the motivation)
2. **Where are you starting from?** (Past experience with this and related things, to calibrate scope)
3. **Exactly what are you trying to achieve?** (Get concrete: which code, which behaviour)
4. **What's your ideal end state?** (Just this one task, or a skill to repeat elsewhere?)
5. **How would you like to learn this?** (Reading, watching, running and experimenting with code, or a mix? This can vary by session and topic, so ask every time)
6. **How much time do you have?** (Be specific: 30 min? 1 hour? 2 hours?)

### Generate Learning Goals

Based on responses, create SMART goals (specific, measurable, achievable, relevant, time-bound):
- **Primary Learning Goal**: One clear, achievable objective for this session
- **Supporting Objectives**: 2-5 specific sub-goals that ladder up to the primary goal

**Format:**
```
Primary Learning Goal:
[Clear statement of what you'll understand/be able to do by the end]

Supporting Objectives:
- [Concrete outcome 1]
- [Concrete outcome 2]
- [Concrete outcome 3]
```

**Important**: Goals should be:
- Achievable in the available time
- Specific and measurable
- Focused on understanding/capability, not just "finishing" something

Ask the user to confirm or narrow the goals before moving on.

## Step 2: Locate and Access Resources

### If the topic is the codebase you're working in

Don't ask the user. Find the relevant files yourself, list them with a one-line note on what each does, and move on to step 3. Resource gathering here is part of the activities, not a separate phase.
### If the topic is external

Ask what kind of prior art they want (real packages or codebases to reverse-engineer, tutorials, videos, documentation, examples in their own projects).

Then suggest as many or as few resources as are relevant, matched to that and to how they said they'd like to learn this in step 1. Someone who wants to experiment with code wants working examples to run and tinker with; someone who wants to read wants a well-chosen article or chapter. Don't assume.

**Important:**
- Keep it minimal. Too many resources cause overwhelm, and users rarely read most of them.
- Verify links before suggesting them. Better still, help the user find resources rather than listing them.
- Don't substitute your own summaries for resources. If the user wants sources, point at sources.
- Identify, don't deep-dive. Reading happens inside activities in step 3.

## Step 3: Adopt and Execute Learning Activities

### Set Up the Session

Before creating activities, ask the user whether they want the session saved to files. Not everyone does.

**If not**, keep the plan and notes in the conversation and skip the file steps below.

**If yes**, ask where. Create a session folder there with two files:

- `plan.md`: goals, activities, and progress checkboxes
- `notes.md`: a shared working doc where:
  - **The agent** writes questions and key insight summaries after each answer, formatted as blockquotes with a robot emoji, e.g. `> 🤖: "The key insight is..."`. This keeps the agent's contributions visually distinct from the user's own notes.
  - **The user** writes their answers and notes in their own voice.

The notes doc becomes a study guide as a side effect of the session. The agent should NOT write answers for the user -- only questions and summary insights after the user has answered.

Start `plan.md` from this template:

```markdown
# Learning Session: [Topic Name]
Date: YYYY-MM-DD
Time Available: [X hours/minutes]

## Learning Goals
[Goals from step 1]

## Activities
[Filled in once designed]

## Progress Tracking
- [ ] Activity 1
- [ ] Activity 2
```

### Design Activities

Create 2-5 hands-on activities that build toward the learning goals.

**Activity Structure:**
Each activity should include:
1. **Goal**: What you'll understand by completing this
2. **Type**: reverse-engineer | build-minimal | implement | explore | debug
3. **Tasks**: Step-by-step what to do
4. **Checkpoints**: Questions to answer before moving on
5. **LLM role**: Ways the agent can help if you get stuck
6. **Timebox**: Suggested time limit (e.g., "15-20 minutes"). The user sets a timer; finishing early is fine and common.

**Activity Type Guidelines:**

- **Reverse-engineer**: Study existing code to understand patterns
  - Best for: Learning from established codebases
  - Example: "Examine how DT handles row selection"
  
- **Build-minimal**: Create smallest possible working example
  - Best for: Understanding core concepts in isolation
  - Example: "Create a standalone JS→R communication demo"
  
- **Implement**: Apply learning to your actual context
  - Best for: Cementing understanding through real use
  - Example: "Add event selection to your widget"
  
- **Explore**: Navigate and document a codebase or system
  - Best for: Mapping out unfamiliar territory
  - Example: "Trace the lifecycle of a magic method call"
  
- **Debug**: Fix broken code to understand how things work
  - Best for: Learning through problem-solving
  - Example: "Figure out why this method isn't being called"
  
- **Map-drawing**: The agent creates visual diagrams (ASCII art) of code flow, architecture, or data paths that the user can refer to during questioning
  - Best for: Tracing code paths, understanding call stacks, seeing how data transforms through a pipeline
  - Example: "Create a diagram of the request lifecycle from user input to HTTP response"
  - The diagram becomes a reference artifact for the rest of the session and beyond
  - Update the diagram as new layers are discovered during exploration

**Rough mapping from goal to activity type:**
- Understanding new syntax: build-minimal, then explore
- Learning library internals: reverse-engineer
- Tracing code paths or architecture: map-drawing plus explore

**Balance & Sequencing:**
- Match activity types to how the user said they'd like to learn this in step 1. Someone who chose experimenting with code gets mostly build and implement activities; someone who chose reading gets more explore and reverse-engineer activities with focused reading.
- Keep any reading scoped: "Read X to understand Y", never "read the docs"
- Sequence from simpler to more complex
- Consider dependencies: what needs to be understood first?
- Ask user if they have preferences for sequencing when multiple approaches are viable

**Example Activity:**
```
🔍 Activity 1: Reverse-engineer one working widget

Goal: Understand how an existing widget (e.g. DT) captures selection 
and sends it to Shiny.

Tasks:
1. Open the DT GitHub repo
2. Locate where Shiny.setInputValue() is used in the JS files 
   (inst/htmlwidgets/datatables.js)
3. Make brief notes:
   - What JS event triggers the update?
   - How is the input ID constructed?
   - What data is passed to Shiny?

Checkpoints:
- Can you find where the event handler is attached?
- What triggers Shiny.setInputValue() to be called?
- How does the data flow from user action to R?

LLM role:
- "What's this event handler doing?"
- "What does this argument to setInputValue mean?"
- "Walk me through this code line-by-line"

Timebox: 20-30 minutes
```

### Update plan.md

If saving, add each activity in full under the Activities heading in `plan.md`, one `## Activity N: [Name]` section per activity.

### Check the Plan Against the Answers

Before presenting, reread the user's answers from step 1 and check each activity against them: end state, audience, depth, how they said they'd like to learn, and time. An explanatory goal does not get a mechanical trace through internals. A user who said an area is murky does not get an activity that starts there. Fix mismatches before showing the plan.

### Present the Plan

Show the user:
1. The saved file location
2. The complete activity plan
3. Total estimated time vs. available time
4. Ask if they want to adjust anything before starting

### Execute Activities

**Execution pattern:**

For each activity:

1. **Remind** the user of the current activity goal and timebox
2. **Support** as they work through tasks
3. **Check in** when they hit checkpoints
4. **Celebrate progress** when activities complete

**Guidance principles**

**"What it does, not how":**
For code exploration sessions, frame questions around *what* each piece of code is responsible for (its role, inputs, outputs) rather than *how* it works internally. This prevents getting lost in implementation details and keeps the focus on building a mental map of the system. Only zoom into "how" when the user specifically needs that level for their task.

**Default to Socratic Method:**
- Ask questions that lead to understanding
- Help them reason through problems
- Guide discovery rather than giving answers
- Ask **one question at a time** by default. A closely linked pair is fine; a list is not. This applies to setup questions too.

**The user runs the experiments.** When a question can be answered by running code, the user runs it and reports back. Do not run the exploration yourself and present the findings; that turns the session into a lecture. Checking that a snippet works before handing it over is fine.

**Keep turns short.** One question or one small task per message, with at most a brief insight alongside it. Tables, diagrams and summaries are welcome when they help, but one per message, not three findings plus a diagram plus the next task.

**Example:**
```
User: [Struggling with where to add event handler in widget code]

Agent: "🤔 So… where do you want interactivity?

Let me ask you this:
Out of everything that's being created here, what part of the DOM 
would the user actually click on if they were selecting a timeline event?

Once we know that, we can talk about how and where to attach the 
event handler."

User: "I think they'd click on the timeline-box element"

Agent: "Exactly—that's the actionable node.

That means you'll want to attach a JS event handler (e.g. .onclick 
or .addEventListener('click', ...)) to each .timeline-box as it's created.

Now a follow-up:
When you're looping over x.events, what info do you need to send back 
to Shiny when a .timeline-box is clicked? (Think: what identifier, 
value, or payload do you want to capture?)"
```

When the user gets an answer wrong, stay encouraging, explain why, and name 
the specific piece of knowledge they were missing.

**Adapt Based on Context:**
- If user is clearly frustrated → be more direct
- If user says "just tell me" → provide the answer
- If user is making good progress → keep asking questions
- If user is stuck in a loop → offer more concrete guidance

**Predict-then-verify (use occasionally, not every question):**
Once the user has enough context to form an informed guess, occasionally ask them to predict what a piece of code does before they read it. This builds confidence when they're right (scaffolding their mental model) and pinpoints specific gaps when they're wrong. Don't use this at the start of a session or when the user lacks context to guess meaningfully -- it only works once they're oriented.

**When Explaining Code:**
- Walk through line-by-line when needed
- Connect concepts to things they already know
- Use their specific code as examples
- Ask them to predict what will happen before running

## Step 4: Monitor and Evaluate Performance

This step runs continuously during step 3 rather than after it.

### Checkpoint Handling

When user reaches a checkpoint question:
1. Let them answer first
2. If correct: Affirm and expand slightly
3. If incorrect: Encourage, explain the gap, guide to correct understanding
4. Ensure they truly understand before moving on

**Debugging support.** When helping debug:
1. Ask what they've tried
2. Ask what they expected vs. what happened
3. Guide them to isolate the problem
4. Help them form hypotheses and test them
5. Celebrate when they find the issue themselves

**Parking lot.** Maintain a "Scratch - unanswered questions to come back to?" section in the shared working doc (or in the conversation, if not saving). When the user encounters something interesting but tangential during an activity, add it to the parking lot rather than chasing it. This prevents rabbit holes while ensuring nothing is lost.

At the end of the session (or when time allows), go through the parking lot and give quick answers to each item. This respects the user's curiosity without derailing the session's focus.

### Timeboxes

You cannot sense elapsed time. Never estimate it from how much has been said. Check the system clock when an activity starts and note the time, and check it again before saying anything about how long has passed. If you can't read the clock, ask the user how long they've spent.

When a timer runs out, check in. Decide together whether to extend, narrow the activity, or move on. Skipping remaining activities is fine if the goal is already met.

### Progress Tracking

If saving, tick the activity's checkbox in `plan.md` as each one completes.

### When an Activity Completes

Before moving to next activity:
1. **Congratulate** specific achievement
2. **Summarize** what they learned
3. **Connect** to the overall learning goal
4. **Transition** to next activity

**Example:**
```
Agent: "It's working!!

Excellent. That means your widget is now:
- Rendering cleanly ✅
- Sending input to Shiny ✅
- Updating on click ✅

You've now got the full JS → R feedback loop working in your 
custom htmlwidget.

If you want to improve it later, next steps could include:
- Making the selected element visually highlighted (add/remove a CSS class)
- Sending richer data to Shiny (e.g. event ID, label, timestamp)
- Supporting multiple selection or deselection
- Writing a unit test or snapshot test for the widget rendering

But honestly—you've just crossed the hardest barrier. Nice work.

Anything else you want to do with it right now?"
```

## Step 5: Reassess Learning Strategies

### End of Session Documentation

If saving, when all activities complete (or time runs out), restructure the shared working doc so it works as a **reference document**. Put the useful facts at the top and the session detail further down:

1. **Reference section (top)**: diagrams, key concepts, summaries, content lifecycles, relevant files -- anything the user would want to find quickly when they come back to this doc later
2. **Extra notes**: parking lot answers and other supplementary information
3. **Session detail (bottom)**: the full Q&A from the session, kept for completeness but not the first thing you see

Also condense the quiz into a quick summary (question + one-line result) rather than keeping the full back-and-forth.

The goal is that when the user opens this doc in 2 weeks, the first thing they see is the answer, not the journey.

### Final Reflection

Ask the user:
1. "What was most valuable about this session?"
2. "What would you do differently next time?"
3. "On a scale of 1-10, how well did you achieve your learning goal?"

### Record What to Change

If saving, append the reflection as a short dated entry to a `learnings.md` file in the location the user chose for sessions: what worked, what didn't, and any preferences about activity types or timebox lengths. At the start of future sessions, read this file if it exists and adapt the plan to it.

Do not edit this skill file.

## Example Session Flow

**From the session described in the linked post:**

```
User: "I need to implement event selection for my htmlwidget timeline, 
so when a user clicks on an event, it updates a variable in Shiny"

Agent (Step 1 - Establish Learning Goals, ~7 minutes):
Asks, one at a time, about:
- Your specific goals
- Past experience (Shiny? JavaScript? htmlwidgets?)
- Exactly what you're trying to achieve
- Preferred end state
- How you'd like to learn this
- How long you want to spend

Creates learning goals:

Primary Learning Goal:
Within the next few hours, understand and implement the necessary code 
to make your existing htmlwidget timeline respond to user interaction 
in a Shiny app—specifically, capturing a selected event and updating 
a variable on the server side.

Supporting Objectives:
- Identify how event selection can be captured in JavaScript and 
  passed to Shiny via Shiny.setInputValue()
- Modify the widget's JS code to emit a Shiny input when a user 
  selects an event
- Test and verify that the input value is received in Shiny and 
  reflects the expected event ID or index
- Write a minimal working Shiny app that uses the widget and 
  displays the selected event value

Agent (Step 2 - Locate and Access Resources, ~11 minutes):
Asks what kind of prior art the user wants, then suggests a short 
list: the DT package source to reverse-engineer, plus a couple of 
articles on JS-to-Shiny communication.

Agent (Step 3 - Adopt and Execute Learning Activities, ~36 minutes):
Creates 4 timeboxed activities:

🔍 Activity 1: Reverse-engineer one working widget (20-30 min)
Goal: Understand how DT captures selection and sends it to Shiny
[See Activity example above for full details]

🔨 Activity 2: Build minimal standalone Shiny demo (15-20 min)
Goal: Create a working JS→R communication example from scratch

🎯 Activity 3: Add minimal event tracking to your widget (15-20 min)
Goal: Implement event capture in your actual widget

⚡ Activity 4: Wire the widget into a basic Shiny app (10-15 min)
Goal: Test the full integration

User works through activities with Socratic guidance:
- "What's this event handler doing?"
- "Where do you want interactivity?"
- "What part would the user click on?"
- Multiple debugging rounds on code they wrote

When the user was stuck on where a change belonged, the agent didn't 
say where. It walked through the relevant concepts, then asked 
questions until the user worked out the location themselves.

Agent (Step 4 - Monitor and Evaluate, throughout):
Checks in at each checkpoint. User finishes each activity under its 
timebox and skips activity 4 because the goal is already met.

Agent (Step 5 - Reassess Learning Strategies):
Restructures the notes into a reference doc and asks the reflection 
questions.

Total time: ~1 hour
Result: Working PR with understanding of DT internals and new capability
```

**Takeaways from the linked post:**
- "What made this work wasn't that [the LLM] gave me the right code but 
  that it helped me ask the right questions"
- "Could I have done it without the LLM? Yes, but it would have taken 
  longer, and I would have learned less"
- "Although I was using an LLM, I was an active participant in my own 
  learning and so felt empowered as a learner"

## Usage Notes

- **Resuming sessions**: User can share the plan.md file from a previous session to continue
- **Shorter sessions**: Adapt by reducing activities or scope, not by rushing
- **Multiple sessions**: For complex topics, suggest breaking into multiple focused sessions
- **Uncertainty**: When unsure how to structure activities, ask user about their learning style preferences