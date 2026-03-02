# Agent Collaboration Notes

When multiple agents are working in parallel, do not let them share the same working directory.

1. Use one `git worktree` per agent (each in a separate directory).
2. Create/use one branch per agent, and keep branch names unique (for example: `codex/<agent-id>/<task>`).
3. Do not run `git checkout` concurrently in the same worktree.
4. Merge changes through a single integrator flow (`rebase` or `cherry-pick`) after each agent provides commit SHA(s).

## Build And Source-Of-Truth Rules

This repo uses `.shtml` as source templates and generates `.html` files via Grunt.

1. Edit source files first:
   - Prefer updating `.shtml` and include files under `inc/`.
   - Do not manually hand-edit generated `.html` files unless the task explicitly requires it.
2. Build command:
   - Before running `npm run build`, always wait for manual confirmation from the user that source changes (such as `.shtml` or `inc/*`) are reviewed and approved.
   - Run `npm run build` (same as `grunt build`) only after that confirmation, then commit generated files as `commit build results`.
   - `grunt build` runs `copy` (`*.shtml` -> `*.html`) and `ssi` (flatten includes).
3. Local preview:
   - Run `npm start` to start BrowserSync for local checking.
4. News update rule:
   - For normal news content updates, update `inc/news.html` as source.
   - Let build pipeline regenerate pages such as `index.html` and `news/index.html`; do not maintain those duplicates by hand.
