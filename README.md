# rapid-learning

An agent skill for learning programming topics quickly, with the LLM acting as a tutor rather than a code generator. It sets goals, finds a minimal set of resources, designs short timeboxed activities, guides you through them with questions instead of answers, and records what you learned.

It follows the self-directed learning framework from Kim et al. (2014), as applied to LLM-assisted learning by [Lin (2023)](https://doi.org/10.1177/10451595231184928). The approach came out of [this blog post](https://niccrane.com/posts/llms_for_learning/), which walks through a real session end to end.

## Who it's for

Anyone who wants to understand something rather than just get it done: a concept, a library's internals, an unfamiliar part of a codebase, a technique they'll need again. It works best on tasks just outside your current knowledge.

## What a session looks like

```
You:   I want to understand how htmlwidgets send events back to Shiny.
Agent: What's your motivation for learning this rather than having me write it?
You:   I'll need to do it again and want to know if the code is right.
Agent: Where are you starting from? Have you written an htmlwidget before?
...
Agent: Here's a plan: four activities, about an hour. Activity 1, 20 minutes:
       reverse-engineer how DT handles row selection. Start when ready.
```

The agent asks one question at a time, keeps you to the timeboxes, and lets you do the work.

## Install

**Claude Code**

```
/plugin marketplace add thisisnic/rapid-learning
/plugin install rapid-learning@rapid-learning
```

**Claude.ai**

Download this repository as a zip, then upload it under Settings, Capabilities, Skills.

**Other agents**

Copy this folder into wherever your agent looks for skills. The skill is a single `SKILL.md` following the open [Agent Skills](https://agentskills.io) format.

## Licence

[CC-BY-4.0](LICENSE). Use it, adapt it, share it, with credit.
