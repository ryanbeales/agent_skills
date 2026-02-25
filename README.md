This is a set of skills and workflows to guide AI agents to build projects that better align with you or your organization's goals. It is based off my "Zen of the Staff Engineer" document published on [LinkedIn](https://www.linkedin.com/pulse/zen-staff-engineer-ryan-beales-7hsrc/).

The published article was intended to be a set of guiding principles for making decisions about what and how to build software. The goal is to keep operational and organizational context in mind when making decisions. Here I'm providing a set of skills and workflows to help AI agents follow the same principles.

The TL;DR of the article is:
- Does it align with your core business?: Consider the organization's value stream: does adding this project increase any metrics associated with the core business? (e.g., revenue, cost savings, user retention, etc.)
- Buy vs. build: Prefer pre-built solutions over building your own. Even if an AI can generate it in seconds, it means the AI still has to maintain that code in perpetuity. Do you want to use your token budget for duplicating existing software? (Let _them_ use their token budget!)
- Every line of code needs maintenance: A line of code still requires periodic review and maintenance; it doesn't matter if a human or AI is writing it. Tokens are expensive and we want to use them efficiently. `docker run` is _far_ simpler than duplicating Heroku.

There are caveats to these points in the article, but for AI agents we don't need to worry so much. You might still need to have that context, but the intent of these skills and workflows is to corral the AI into making decisions that align with you and your organization's goals.

AI makes it exceptionally easy to build software now. But _should you?_ You probably don't need to rewrite Postgres as it already exists. You probably don't need to write a C compiler, because one already exists (a Feb 2026 topical example). We make the same decisions unconsciously when we choose to use a library instead of writing our own code, so let's make the AI do that too.

# Usage

This is currently set up for Google Antigravity or Gemini-cli. The workflows and skills will work as-is in other tools but they just need to live in different directories.

Here are examples of where skills and workflows typically live in popular AI tools (at the project level):
- **Google Antigravity / Gemini-cli**: `.agent/skills/` and `.agent/workflows/` (or `_agents/`)
- **Claude Code**: `.claude/skills/` for skills and `CLAUDE.md` in the project root for general rules
- **Cursor**: `.cursor/rules/` directory or a `.cursorrules` file in the project root
- **GitHub Copilot**: `.github/copilot-instructions.md`

There are two workflows:

## interview_company_context

Launched with `/interview_company_context`

This workflow will interview you to understand:
- Your core business
- Your strategic focus
- Build vs. Buy strategy
- Platform questions like: AWS vs GCP vs On-Prem
- CI/CD platform
- Monitoring platform
- What does your local development environment look like? (_Everything_? Mocks/Stubs? Too large to fit on a laptop? etc.)
- Are there any regulatory requirements? (GDPR, HIPAA, SOC2, etc.)

This will generate a `company_context.md` file in the `docs` directory which the skills can refer to. This informs the AI agents on how to _build_ projects.

## interview_operational_context

Launched with `/interview_operational_context`

This workflow will interview you to understand:
- Who looks after the software once it's built?
- Who is responsible when it goes wrong?
- Where do you send alerts and notifications?
- Do we have any resource constraints (budget, CPU, memory, etc.)?
- How do you handle sensitive data (e.g., secrets, PII, etc.)?
- What does your release flow look like?

This will generate a `operational_context.md` file in the `docs` directory which the skills can refer to. This informs the AI agents on how to _run_ projects.


# Results

The two generated documents and the skills can be generated once and used in multiple projects. Start with the files in this repo for a per-project contenxt, or you can then save them in your ai agents global context for skills to refer to.

Here are examples of where global context and skills can be stored for popular AI tools:
- **Google Antigravity / Gemini-cli**: `~/.gemini/antigravity/skills/` or the global workspace configuration directory
- **Claude Code**: `~/.claude/skills/` for global skills and `~/.claude/CLAUDE.md` for global rules
- **Cursor**: In the Cursor Settings under **General > Rules for AI**
- **GitHub Copilot**: Custom instructions can be added locally in VS Code user settings or globally in your GitHub profile settings