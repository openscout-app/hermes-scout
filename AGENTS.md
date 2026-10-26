# Scout for Hermes Agent

This repository is the Hermes Agent plugin for Scout. It is public. It adds
`scout_*` tools and session hooks to Hermes. The default branch is `dev`.

## Where work goes

- The plugin talks to `scout mcp` over stdio with JSON-RPC. It carries no
  runtime code.
- Behavior that every harness needs goes to the core repository,
  `openscout-app/scout`. Land it there first, then use it here.
- Behavior specific to Hermes goes here: the tool schemas, the hooks, and the
  packaging.

| Path | Holds |
| --- | --- |
| `hermes_scout/__init__.py` | The MCP bridge, the tool schemas and handlers, and the hooks |
| `plugin.yaml` | The Hermes plugin manifest |
| `pyproject.toml` | The Python package and its `hermes_agent.plugins` entry point |

## Rules

- Each `scout_*` tool forwards its arguments to a `scout mcp` tool through
  `tools/call`. Do not add tool behavior that the MCP server does not have.
- The package has no runtime dependencies and supports Python 3.9 and newer.
  Keep both.
- Keep the version in `plugin.yaml` and `pyproject.toml` the same.
- When you add or remove a tool, update the tool table in the README.
- Scout is for high-trust local developer use. Do not claim enterprise,
  compliance, or multi-tenant readiness.
- This repository is public. Do not commit local paths, host names,
  credentials, or private source.

## Checks

- `python3 -m py_compile hermes_scout/__init__.py`
- Install the checkout as a directory plugin and confirm that
  `hermes tools list` shows the Scout tools.

## Commits and pull requests

- Commit subjects use gitmoji: `🐛 Time out a stalled MCP call`.
- Do not add AI co-author trailers or "Generated with" lines.
- Push a branch to `openscout-app/hermes-scout` and open a pull request into
  `dev`.

<!-- scout:begin -->
## Scout

- Work for another agent, or on another machine, goes through Scout: `scout ask` (MCP `ask`).
- Another machine: `scout ask --on <host> --project <path on that host> --harness <claude|codex>`; `scout hosts` lists machines and their projects. Don't ssh in to launch agents.
- Syntax: `scout ask --help`, `scout help --detail`. Added by `scout setup agents-md`; `scout setup agents-md --remove` takes it out.
<!-- scout:end -->
