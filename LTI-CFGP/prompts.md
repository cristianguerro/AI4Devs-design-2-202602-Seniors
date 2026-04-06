## Prompt to create the initial agent config

Create an agent that act as a senior product manager and ultimately generate the following artifacts: Product Requirements Document (PRD), user stories, Product back log, work tickets and effort stimation. This agent will gather information in order to fulfill this job. User may provide documents with definitions and designs of the project.

For each of these artifacts create skills.

create-PRD
PRD artifact have a defined structure. It is fundamental that the artifact incorporates these two sections: Non-Goals/Out-of-Scope and KPI indicators and that it follows a modular structure and with secuential phases and clear dependencies in order to improve AI agents readability. When creating this skill ask for document structure that will be generated with it.

create-user-story
Artifacts generated with this skill must follow a template following the best practices including: The 3 C's, INVEST prociple, etc. Acceptance criteria must follow the Given/When/Then from Behavior-Driven Development (BDD). Users stories may be embeded in the PRD file or in an independent file with links in the PRD.

prioritize-backlog
Artifact generated with this skill must follow a structure following MoSCoW prioritization. This artifact may be embeded in the PRD or in a independent file with links in the PRD.

create-work-ticket
Artifacts generated with this skill must follow a structure including: title, description, Acceptance criteria, priority, estimation, asignee, tags, comments, links to other resources and a change log. This artifact may be embeded in the PRD or in a independent file with links in the PRD.

estimate-ticket
This skill will help to estimate work tickets creating an artifact and also updating work tickets. 

Not asume anything and ask me for approval of the templates that are going to be created for the skills. 

### Agent questions

Q: Do you approve all 6 templates above (agent + 5 skills), or would you like changes to any of them?
A: Approve all — proceed to create files
Q: Should user stories, backlog, and tickets be embedded in the PRD by default, or generated as separate files with links?
A: Ask the user which is his preference at the begining, subsequent generations will follow user preference.
Q: Where should the agent and skills be created?
A: .github/ (workspace-level, shared with team)


