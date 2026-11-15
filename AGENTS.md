# Portfolio API
CRM project for the [portfolio web](https://github.com/mfigueroa23/portfolio-web)
built with NextJS, communicating with the [portfolio backend](https://github.com/mfigueroa23/portfolio-api)
and integrated with CI/CD through GitHub Actions.

## Commands
- `pnpm run dev`: Starts the server in development mode.
- `pnpm run lint`: Runs the linter to check code style.
- `pnpm run test`: Runs the unit and integration tests.

## Documentation rules
- The project has a knowledge base in JIRA and Confluence under the key `PRT`, and the user must review any resource
  before it is created in JIRA or Confluence.
- When a new development is requested, it must be turned into user stories (there can be more than 1) in JIRA
  following this format (`[]` must be checklists):
  ```
  As a <role> I want <feature> so that <benefit>

  ## Acceptance criteria
  [] <acceptance criterion 1>
  [] <acceptance criterion N>
  ```
- When creating a user story, the ticket properties must include:
  - Priority
  - Label (e.g.: `web`, `api`, `panel`, etc.) - it can have more than 1, plus the system it belongs to
  - Start date and due date (estimated)
  - Story points (estimated) following the [Fibonacci](https://en.wikipedia.org/wiki/Fibonacci_sequence) methodology
- If documentation in Confluence is requested, use the templates available in the `PRT` space:
  - `How to`: Documentation of processes and procedures
  - `Troubleshooting`: Documentation of problems and solutions

## Development rules
- Code written in English
- Module-based project architecture
- Simple code without complex logic; if needed, split it into small, reusable functions
- Do not add external dependencies without prior approval from the developer
- Do not build Docker images without prior approval from the developer
- User stories are split into tasks, and these must be small pieces of functional, verifiable code
- When working on a task related to a ticket, a branch must be created following: `<type>/<JIRA-KEY-TICKET>-<description>` e.g.: `feature/PRT-1234-add-new-endpoint`
- Before writing the code, tests must be written for the small verifiable tasks, following the TDD (Test Driven Development) methodology
- When a small task is finished, wait for the developer's approval before making a commit in English, without co-authored-by from any AI, following
  [conventional commits](https://www.conventionalcommits.org/):
  ```
  <type>[scope]: [<JIRA-KEY-TICKET>] <description>

  <General description of the changes made>

  Modified files:
  - <path of the modified file>: <description of the change made>
  ```
- When a pull request is requested, it must be written in English, without co-authored-by from any AI, and follow this structure:
  ```
  <type>[scope]: [<JIRA-KEY-TICKET>] <description>

  <General description of the changes made>

  Modified files:
  - <path of the modified file>: <description of the change made>

  Tests performed:
  - <test name>: <description of the test performed>
  ```

## Versioning rules
- The project follows [semantic versioning](https://semver.org/) `MAJOR.MINOR.PATCH`, and the source of truth
  is the `version` field in `package.json`; the Docker image is published with that version.
- The version is bumped when an epic or a task is finished, with a bump commit that also requires prior approval
  from the developer. The increment is defined by the highest-impact commit type since the last version:
  - `MAJOR`: incompatible changes (`feat!`, `fix!` or `BREAKING CHANGE`), for example a removed endpoint or
    a change in the API contract.
  - `MINOR`: new backward-compatible functionality (`feat`).
  - `PATCH`: fixes and changes without new functionality (`fix`, `perf`, `refactor`, `build`, `ci`, `chore`, etc.).
- The version is bumped with `pnpm version <major|minor|patch> --no-git-tag-version`, in its own commit separate from
  the code changes: `chore(release): [<JIRA-KEY-TICKET>] Bump version to vX.Y.Z`.
- Tags are created only on `main`, on the merge commit, with the format `vX.Y.Z` (same as `package.json`) and
  annotated: `git tag -a vX.Y.Z -m "vX.Y.Z"`. A published tag is never moved or reused.
- The tag and the GitHub release are created manually, never from a workflow, only after the `Release` workflow
  finishes successfully and with prior approval from the developer, using
  `gh release create vX.Y.Z --title "vX.Y.Z" --notes-file <file>`.
- Release notes are written in English, without co-authored-by from any AI, following this structure:
  ```
  ## <Version summary>

  ### Features
  - <description> ([<JIRA-KEY-TICKET>])

  ### Fixes
  - <description> ([<JIRA-KEY-TICKET>])

  ### Other changes
  - <description> ([<JIRA-KEY-TICKET>])

  ### Database
  - <included migration and its impact, or "No migrations">

  ### Docker image
  - `<organization>/<image>:X.Y.Z` (`sha256:<digest>`)
  ```
- Version `1.0.0` is the project baseline: its tag is `v1.0.0` and its release summarizes the initial state.
