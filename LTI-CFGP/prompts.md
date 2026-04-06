## Prompt to Create the Initial Agent Config

Model used: Claude Opus 4.6 high.

Create an agent that acts as a Senior Product Manager and generates the following artifacts:

- Product Requirements Document (PRD)
- User stories
- Product backlog
- Work tickets
- Effort estimation

This agent must gather information needed to produce these artifacts. Users may provide project definition and design documents as inputs.

Create one skill for each artifact area.

### create-prd

The PRD artifact must follow a defined structure. It is fundamental that the artifact includes these two sections:

- Non-Goals / Out-of-Scope
- KPI indicators

The PRD must also use a modular structure with sequential phases and clear dependencies to improve readability for AI agents.

When creating this skill, ask for the document structure that will be generated.

### create-user-story

Artifacts generated with this skill must use a template aligned with best practices, including:

- The 3 C's
- INVEST principle

Acceptance criteria must follow Given/When/Then from Behavior-Driven Development (BDD).

User stories may be embedded in the PRD file or generated in an independent file linked from the PRD.

### prioritize-backlog

Artifacts generated with this skill must follow a MoSCoW prioritization structure.

This artifact may be embedded in the PRD or generated in an independent file linked from the PRD.

### create-work-ticket

Artifacts generated with this skill must include:

- Title
- Description
- Acceptance criteria
- Priority
- Estimation
- Assignee
- Tags
- Comments
- Links to other resources
- Change log

This artifact may be embedded in the PRD or generated in an independent file linked from the PRD.

### estimate-ticket

This skill helps estimate work tickets by creating an estimation artifact and updating existing tickets.

Do not assume anything. Ask for approval of the templates that will be created for the skills.

### Agent Questions

1. Q: Do you approve all 6 templates above (agent + 5 skills), or would you like changes to any of them?  
   A: Approve all - proceed to create files.
2. Q: Should user stories, backlog, and tickets be embedded in the PRD by default, or generated as separate files with links?  
   A: Ask the user for their preference at the beginning. Subsequent generations will follow that preference.
3. Q: Where should the agent and skills be created?  
   A: .github/ (workspace-level, shared with team).

## Prompt to Create PRD

Model used: Claude Opus 4.6 high.

In this GitHub repo https://github.com/cristianguerro/AI4Devs-design-1-202602-Seniors/tree/feature/lti-cfgp there is the LTI ATS - System Design Document.
Create a PRD based on this document.

### Questions for PRD Creation

1. Q: Should subsequent artifacts (roadmap, story map, user stories, backlog, tickets) be embedded in the PRD or in separate linked files?  
   A: Separate files - each artifact in its own file, linked from the PRD.
2. Q: Should I use the default PRD structure, or do you want to customize it before I generate?  
   A: Use default structure - standard sections: Overview, Problem, Goals, Non-Goals, Roadmap, Epics, Personas, Requirements, NFRs, KPIs, etc.
3. Q: Where should the PRD and related files be placed?  
   A: Inside LTI-CFGP folder, named PRD-LTI-CFGP.md.

## Prompt for Product Roadmap, Story Map, Backlog, Tickets, and Estimation

At this stage, with the PRD created, the agent asked for approval and suggested moving to the next phase.
I approved the work and let the agent proceed with the following tasks.

## Afterthoughts

This agent worked as expected and, as a first version, I think it performed really well.
The next update I am considering is adding a skill named something like `create-sprint`, where it takes a reasonable number of user stories and creates an artifact to be used in the next sprint.
That is something I did not take into account when I started the exercise, as I have never been in the position of creating user stories.
This kind of exercise put me in the position of creating a personal project management tool.
