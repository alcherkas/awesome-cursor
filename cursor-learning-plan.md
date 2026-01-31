# Cursor Advanced Features Learning Plan

> A structured curriculum to master all advanced features of Cursor IDE

---

## Part 1: Fundamentals

### 1. Chat & Context Management

#### @-Mentions System
- `@Files & Folders` - Add file/folder context
- `@Code` - Add a specific snippet
- `@Docs` - Add framework/library docs (built-in or your own URL)

> Note: Cursor 2.x removed many explicit `@...` items (e.g. `@Web`, `@Definitions`, `@Git`). Ask the agent directly (“review my branch changes”, “search the web”, etc.).

#### Context Management Best Practices
- Let the agent find context - don't manually tag every file
- If you know the exact file, tag it; otherwise let the agent search
- Including irrelevant files can confuse the agent

#### When to Start a New Conversation
**Start fresh when:**
- Moving to a different task or feature
- Agent seems confused or keeps making the same mistakes
- You've finished one logical unit of work

**Continue when:**
- Iterating on the same feature
- Agent needs context from earlier in the discussion
- Debugging something it just built

> Long conversations can cause the agent to lose focus. After many turns, context accumulates noise.

#### Key Shortcuts
| Action | Mac | Windows |
|--------|-----|---------|
| Open Chat | `Cmd + L` | `Ctrl + L` |
| New Chat | `Cmd + N` or `Cmd + R` | `Ctrl + N` or `Ctrl + R` |
| Add Selection to Chat | `Cmd + Shift + L` | `Ctrl + Shift + L` |

#### Practice Exercises
- [ ] Tag 2 files with `@Files & Folders` and ask a targeted question
- [ ] Tag a single function with `@Code` and ask for a refactor
- [ ] Add one library with `@Docs` and implement a small example from it

---

### 2. Tab Completion & AI Suggestions

#### Topics
- Ghost text predictions
- Multi-line completions
- Context-aware suggestions
- Cursor Prediction (next edit prediction)

#### Optimizing Completions
- Write good comments for better suggestions
- Use type hints and documentation
- Understand completion triggers

#### Key Shortcuts
| Action | Mac | Windows |
|--------|-----|---------|
| Accept Completion | `Tab` | `Tab` |
| Reject Completion | `Esc` | `Esc` |
| Partial Accept | `Cmd + →` | `Ctrl + →` |

#### Practice Exercises
- [ ] Write a complex function using only tab completions
- [ ] Experiment with different comment styles
- [ ] Practice accepting partial completions

---

### 3. Inline Editing (Cmd+K)

#### Topics
- Select code → `Cmd+K` → Describe changes
- No selection = generate new code at cursor
- Partial accepts with `Cmd+→`
- Multi-cursor inline edits
- Chaining inline edits

#### Key Shortcuts
| Action | Mac | Windows |
|--------|-----|---------|
| Inline Edit | `Cmd + K` | `Ctrl + K` |
| Submit | `Enter` | `Enter` |
| Cancel | `Cmd + Shift + Backspace` | `Ctrl + Shift + Backspace` |
| Ask Quick Question | `Opt + Enter` | `Alt + Enter` |

#### Practice Exercises
- [ ] Refactor a function using inline edit
- [ ] Generate a new function from scratch with `Cmd+K`
- [ ] Use multi-cursor to edit multiple similar code blocks

---

## Part 2: Agent Workflows

### 4. Composer & Multi-File Editing

#### Topics
- Opening Composer (`Cmd + I`)
- Multi-file edits in single prompt
- Reviewing and applying changes
- Accepting/rejecting individual file changes
- Adding files to context
- Using @-mentions in Composer
- Checkpoints and reverting

#### Key Shortcuts
| Action | Mac | Windows |
|--------|-----|---------|
| Open Composer | `Cmd + I` | `Ctrl + I` |
| Accept All Changes | `Cmd + Enter` | `Ctrl + Enter` |

#### Practice Exercises
- [ ] Create a new feature spanning 3+ files
- [ ] Refactor code across multiple files
- [ ] Practice using checkpoints to revert changes

---

### 5. Agent Mode

#### Topics
- Enabling agent mode for autonomous operations
- Terminal command execution
- File creation and modification
- Iterative problem solving
- Watching the agent work in diff view
- Pressing **Escape** to interrupt and redirect

#### Practice Exercises
- [ ] Use Agent mode to fix a bug that requires investigation
- [ ] Let agent run terminal commands to verify changes
- [ ] Practice interrupting and redirecting the agent

---

### 6. Plan Mode

#### Topics
- Press `Shift+Tab` in agent input to toggle Plan Mode
- Agent researches codebase to find relevant files
- Asks clarifying questions about requirements
- Creates detailed implementation plan with file paths
- Waits for approval before building

#### Working with Plans
- Plans open as Markdown files you can edit directly
- Remove unnecessary steps, adjust approach, add context
- Click "Save to workspace" to store plans in `.cursor/plans/`
- Creates documentation and context for future agents

#### Starting Over from a Plan
When the agent builds something that doesn't match:
1. Revert the changes
2. Refine the plan to be more specific
3. Run it again

> This is often faster than fixing an in-progress agent and produces cleaner results.

#### Practice Exercises
- [ ] Use Plan Mode for a complex feature
- [ ] Edit a plan before execution
- [ ] Save a plan to `.cursor/plans/`

---

### 7. Debug Mode

#### Topics
- Available in the agent dropdown
- For bugs you can reproduce but can't figure out
- Race conditions and timing issues
- Performance problems and memory leaks
- Regressions where something used to work

#### How It Works
1. Generates multiple hypotheses about what could be wrong
2. Instruments your code with logging statements
3. Asks you to reproduce the bug while collecting runtime data
4. Analyzes actual behavior to pinpoint root cause
5. Makes targeted fixes based on evidence

#### Practice Exercises
- [ ] Use Debug Mode on a tricky bug
- [ ] Provide detailed reproduction steps
- [ ] Review the hypotheses generated

---

### 8. Image Support

#### Design to Code
- Paste a design mockup and ask the agent to implement it
- Agent sees the image and matches layouts, colors, spacing
- Use Figma MCP server for direct integration

#### Visual Debugging
- Screenshot an error state or unexpected UI
- Ask the agent to investigate
- Often faster than describing the problem in words

#### Browser Control
- Agent can take its own screenshots
- Test applications and verify visual changes

#### Practice Exercises
- [ ] Paste a design mockup and implement it
- [ ] Screenshot a UI bug and ask agent to fix it

---

## Part 3: Configuration

### 9. Rules

#### Topics
- Create rules as markdown files in `.cursor/rules/`
- Persistent instructions that shape agent behavior
- Always-on context at start of every conversation

#### Best Practices
```markdown
# Commands
- `npm run build`: Build the project
- `npm run typecheck`: Run the typechecker
- `npm run test`: Run tests

# Code style
- Use ES modules (import/export), not CommonJS
- See `components/Button.tsx` for canonical structure

# Workflow
- Always typecheck after making code changes
- API routes go in `app/api/` following existing patterns
```

#### What to Avoid
- Copying entire style guides (use a linter instead)
- Documenting every possible command
- Adding instructions for edge cases that rarely apply

> Start simple. Add rules only when you notice the agent making the same mistake repeatedly.

#### Practice Exercises
- [ ] Create a rules file in `.cursor/rules/`
- [ ] Add project-specific coding standards
- [ ] Reference canonical files instead of copying content

---

### 10. Skills

#### Topics
- Stored in `.cursor/skills/<skill-name>/SKILL.md`
- YAML frontmatter (`name`, `description`, optional settings)
- Optional `scripts/`, `references/`, `assets/`
- Auto-applied when relevant (or set `disable-model-invocation: true`)

#### What Skills Include
- Domain workflows + optional runnable scripts
- Progressive loading (references on demand)

#### Practice Exercises
- [ ] Add one local skill in `.cursor/skills/` and invoke it
- [ ] Add `disable-model-invocation: true` and confirm it only runs via `/`

---

### 11. Commands

#### Topics
- Store as Markdown files in `.cursor/commands/`
- Reusable workflows triggered with `/`
- Check into git for team sharing

#### Example Commands
- `/pr` - Commit, push, and open a pull request
- `/fix-issue [number]` - Fetch issue, find code, implement fix
- `/review` - Run linters, check for common issues
- `/update-deps` - Update dependencies one by one with tests

#### Example: /pr Command
```markdown
Create a pull request for the current changes.

1. Look at the staged and unstaged changes with `git diff`
2. Write a clear commit message based on what changed
3. Commit and push to the current branch
4. Use `gh pr create` to open a pull request
5. Return the PR URL when done
```

#### Practice Exercises
- [ ] Create a `/pr` command
- [ ] Create a project-specific command

---

### 12. Hooks

#### Topics
- Configure in `.cursor/hooks.json`
- Scripts that run before or after agent actions
- Integration with security tools, secrets managers, observability

#### Example: Long-Running Agent Loop
```json
{
  "version": 1,
  "hooks": {
    "stop": [{ "command": "bun run .cursor/hooks/grind.ts" }]
  }
}
```

Use cases:
- Running until all tests pass
- Iterating on UI until it matches a design
- Any goal-oriented task where success is verifiable

#### Practice Exercises
- [ ] Understand hook configuration
- [ ] Review hook documentation

---

### 13. Documentation

#### Topics
- Keep project context in the repo (e.g. `README.md`, `docs/`, `AGENTS.md`)
- Use cases: architecture notes, style rules, API specs

#### Documentation Integration
- Use `@Docs` for external docs (and add custom doc URLs)
- Keep internal docs in your repo for easy linking

#### Practice Exercises
- [ ] Create a short `docs/architecture.md`
- [ ] Add one external doc source in `@Docs` and use it in a prompt

---

### 14. Model Configuration

#### Topics
- Understanding available models (GPT-4, Claude, etc.)
- Choosing models for different tasks
- Cost vs. capability tradeoffs

#### Model-Specific Settings
- Max tokens configuration
- Model switching per conversation

#### API Keys & Custom Models
- Adding your own API keys
- Using Azure OpenAI or custom endpoints

#### Practice Exercises
- [ ] Compare responses from different models
- [ ] Configure model preferences for different scenarios

---

### 15. Privacy & Security

#### Topics
- Enabling privacy mode
- Understanding data handling
- Team/Enterprise privacy settings

#### Codebase Indexing
- What gets indexed
- Excluding files with `.cursorignore`
- Re-indexing triggers

#### Practice Exercises
- [ ] Review and configure privacy settings
- [ ] Create a `.cursorignore` file
- [ ] Verify sensitive files are excluded

---

## Part 4: Integrations

### 16. Terminal Integration

#### Topics
- `Cmd+K` in terminal for command generation
- Error explanation and fixes
- Command history with AI context

#### Terminal Context
- Paste errors/logs or use clipboard-as-context
- Run commands from Agent mode

#### Key Shortcuts
| Action | Mac | Windows |
|--------|-----|---------|
| Terminal AI | `Cmd + K` (in terminal) | `Ctrl + K` (in terminal) |

#### Practice Exercises
- [ ] Generate complex commands with `Cmd+K`
- [ ] Debug a terminal error using AI
- [ ] Use Agent mode to run a multi-step terminal workflow

---

### 17. Git Integration

#### Topics
- Commit message generation
- PR description generation

#### Practice Exercises
- [ ] Generate commit messages for several commits
- [ ] Ask the agent to summarize recent changes on your branch

---

### 18. Code Review

#### During Generation
- Watch the agent work in diff view
- Press **Escape** to interrupt and redirect if heading wrong direction

#### Agent Review
- After agent finishes, click **Review** → **Find Issues**
- Agent analyzes proposed edits line-by-line
- Flags potential problems

#### Source Control Review
- Open Source Control tab
- Run Agent Review to compare against main branch

#### Bugbot for PRs
- Push to source control for automated reviews
- Catches issues early on every PR

#### Architecture Diagrams
- Ask agent to generate Mermaid diagrams
- Useful for documentation and revealing architectural issues

#### Practice Exercises
- [ ] Use Review → Find Issues after agent completes
- [ ] Run Agent Review from Source Control
- [ ] Generate a Mermaid diagram for a feature

---

### 19. MCP (Model Context Protocol)

#### Topics
- What is MCP and why it matters
- Built-in MCP servers
- Installing MCP servers

#### Popular Integrations
- Slack messages
- Datadog logs
- Sentry errors
- Database queries
- Figma designs

#### Configuration
- `~/.cursor/mcp.json` configuration
- Project-specific MCP settings
- Debugging MCP connections

#### Practice Exercises
- [ ] Enable a built-in MCP server
- [ ] Install an external MCP server
- [ ] Use MCP tools in a real workflow

---

## Part 5: Advanced Patterns

### 20. TDD with Agents

#### Workflow
1. **Ask agent to write tests** based on expected input/output pairs. Be explicit you're doing TDD.
2. **Tell agent to run tests and confirm they fail.** Say not to write implementation code yet.
3. **Commit the tests** when satisfied.
4. **Ask agent to write code that passes tests**, instructing it not to modify tests. Keep iterating until all pass.
5. **Commit the implementation** when satisfied.

> Agents perform best when they have a clear target to iterate against.

#### Practice Exercises
- [ ] Complete a feature using TDD with agent
- [ ] Let agent iterate until tests pass

---

### 21. Parallel Agents

#### Git Worktrees
- Cursor automatically creates and manages git worktrees
- Each agent runs in isolated worktree
- Agents can edit, build, and test without stepping on each other
- Click **Apply** to merge changes back

#### Multiple Models at Once
- Select multiple models from dropdown
- Submit prompt, compare results side by side
- Cursor suggests which solution is best

#### Use Cases
- Hard problems where different models take different approaches
- Comparing code quality across model families
- Finding edge cases one model might miss

#### Practice Exercises
- [ ] Run an agent in a worktree
- [ ] Compare multiple models on same prompt

---

### 22. Cloud Agents

#### Topics
- Start from cursor.com/agents, the editor, or your phone
- Check on sessions from web or mobile
- Agents run in remote sandboxes

#### How Cloud Agents Work
1. Describe the task and relevant context
2. Agent clones your repo and creates a branch
3. Works autonomously, opens PR when finished
4. You get notified (Slack, email, web)
5. Review changes and merge

#### Good Tasks for Cloud Agents
- Bug fixes that came up while working on something else
- Refactors of recent code changes
- Generating tests for existing code
- Documentation updates

#### Practice Exercises
- [ ] Start a cloud agent from cursor.com/agents
- [ ] Delegate a background task

---

### 23. Workflow Optimization

#### Keyboard-First Workflow
- Essential shortcuts mastery
- Custom keybindings
- Command palette usage (`Cmd + Shift + P`)

#### Prompt Engineering
- Write specific prompts for better results
- Compare: "add tests" vs "Write a test case covering the logout edge case, using patterns in `__tests__/`"
- Iterate on your setup - add rules/commands when patterns emerge

#### Key Traits of Effective Agent Users
- **Write specific prompts** - success rate improves significantly
- **Iterate on setup** - start simple, add as needed
- **Review carefully** - AI code can look right while being subtly wrong
- **Provide verifiable goals** - typed languages, linters, tests
- **Treat agents as collaborators** - ask for plans, request explanations

#### Practice Exercises
- [ ] Complete a feature using only keyboard shortcuts
- [ ] Create a prompt template library
- [ ] Design your optimal window layout

---

## Essential Keyboard Shortcuts Reference

### Chat & AI
| Action | Mac | Windows |
|--------|-----|---------|
| Open Chat | `Cmd + L` | `Ctrl + L` |
| New Chat | `Cmd + N` or `Cmd + R` | `Ctrl + N` or `Ctrl + R` |
| Add Selection to Chat | `Cmd + Shift + L` | `Ctrl + Shift + L` |
| Open Composer | `Cmd + I` | `Ctrl + I` |
| Inline Edit | `Cmd + K` | `Ctrl + K` |
| Terminal AI | `Cmd + K` (in terminal) | `Ctrl + K` (in terminal) |
| Toggle Plan Mode | `Shift + Tab` (in agent input) | `Shift + Tab` (in agent input) |
| Toggle Sidebar | `Cmd + B` | `Ctrl + B` |

### Completions
| Action | Mac | Windows |
|--------|-----|---------|
| Accept Completion | `Tab` | `Tab` |
| Reject Completion | `Esc` | `Esc` |
| Partial Accept | `Cmd + →` | `Ctrl + →` |

### Navigation
| Action | Mac | Windows |
|--------|-----|---------|
| Command Palette | `Cmd + Shift + P` | `Ctrl + Shift + P` |
| Go to File | `Cmd + P` | `Ctrl + P` |
| Go to Symbol | `Cmd + Shift + O` | `Ctrl + Shift + O` |
| Go to Definition | `F12` | `F12` |

---

## Progress Tracking

### Part 1: Fundamentals
- [ ] Chat & Context Management mastered
- [ ] Tab Completion optimized
- [ ] Inline Editing proficient

### Part 2: Agent Workflows
- [ ] Composer for multi-file edits
- [ ] Agent Mode proficiency
- [ ] Plan Mode for complex tasks
- [ ] Debug Mode for tricky bugs
- [ ] Image support workflows

### Part 3: Configuration
- [ ] Rules in `.cursor/rules/`
- [ ] Skills understood
- [ ] Commands created
- [ ] Hooks awareness
- [ ] Project docs in repo
- [ ] Model selection understood
- [ ] Privacy configured

### Part 4: Integrations
- [ ] Terminal AI integration
- [ ] Git workflow optimized
- [ ] Code Review tools used
- [ ] MCP configured

### Part 5: Advanced Patterns
- [ ] TDD with agents practiced
- [ ] Parallel agents used
- [ ] Cloud agents tried
- [ ] Workflow optimized

---

## Resources

### Official Documentation
- [Cursor Documentation](https://docs.cursor.com)
- [Cursor Changelog](https://cursor.com/changelog)
- [Cursor Forum](https://forum.cursor.com)
- [Best Practices for Coding with Agents](https://cursor.com/blog/agent-best-practices)

### Community Resources
- [Cursor Discord](https://discord.gg/cursor)
- [GitHub Discussions](https://github.com/getcursor/cursor/discussions)
- [YouTube Tutorials](https://youtube.com/@cursor_ai)

### MCP Resources
- [MCP Specification](https://modelcontextprotocol.io)
- [MCP Servers Directory](https://github.com/modelcontextprotocol/servers)

---

*Last Updated: January 2026*
