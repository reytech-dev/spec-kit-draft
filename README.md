# Spec Kit Draft

A small [GitHub Spec Kit](https://github.com/github/spec-kit) extension that helps you turn a rough feature idea into clarified, polished input for `/speckit.specify`.

Spec Kit Draft does **not** create feature folders, write `spec.md`, run Spec Kit scripts, or modify project files. It is a drafting helper that produces implementation-neutral feature flow text you can review, adjust, and then pass into `/speckit.specify`.

## What this extension does

Spec Kit Draft adds the command:

```text
/speckit.draft.create
````

Alias:

```text
/speckit.draft.new
```

The command helps you prepare better input for `/speckit.specify` by:

* extracting the user-visible feature outcome
* identifying actors, roles, permissions, and core user actions
* surfacing material ambiguity before specification generation
* asking targeted clarification questions when needed
* recording sensible assumptions for low-impact gaps
* producing a single plain-language feature description
* keeping the result implementation-neutral

The output is intended to be copied directly into `/speckit.specify`.

## Why use this?

`/speckit.specify` works best when the initial feature description is clear, complete, and focused on observable product behavior.

This extension adds a lightweight drafting step before specification generation. It helps avoid vague prompts by clarifying:

* user journeys
* success criteria
* edge cases
* privacy and permission expectations
* error, empty, unavailable, and unauthorized states
* accessibility, localization, and responsive behavior when relevant
* explicit non-goals and out-of-scope items

Use it when you have a rough feature idea but want to sharpen the feature contract before creating the formal Spec Kit specification.

## Requirements

* GitHub Spec Kit
* `specify` CLI with extension support
* Spec Kit version `>=0.8.14`

If you have not installed Spec Kit yet, follow the official Spec Kit installation instructions:

```bash
uvx --from git+https://github.com/github/spec-kit.git specify init my-project
```

Or install the CLI as a tool:

```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
```

## Installation

### Install from this repository

From your Spec Kit project directory, clone this repository and add it as an extension:

```bash
git clone https://github.com/reytech-dev/spec-kit-draft.git
specify extension add --dev ./spec-kit-draft
```

Verify that the extension was installed:

```bash
specify extension list
```

You should see the `Specify Draft` extension listed with its provided command.

### Install from a local checkout

If you already have this repository checked out locally:

```bash
cd /path/to/your/spec-kit-project
specify extension add --dev /path/to/spec-kit-draft
```

## Usage

Start your AI coding agent in your Spec Kit project and run:

```text
/speckit.draft.create Describe the feature you want to specify
```

For example:

```text
/speckit.draft.create Users should be able to save a draft route and publish it later when they are ready.
```

The command will either:

1. ask clarification questions if important product details are missing, or
2. return a polished feature-flow draft that you can pass directly to `/speckit.specify`.

Example output shape:

```text
Important assumptions:
- Saved drafts are private to the user until published.
- Drafts remain editable until publication.

Final draft:

Users can save an incomplete route as a private draft so they can return to it later...
```

You can then use the drafted text with Spec Kit:

```text
/speckit.specify <paste the drafted feature text here>
```

## Optional `before_specify` hook

This extension declares an optional `before_specify` hook.

When supported by your Spec Kit workflow, Spec Kit may prompt you before running `/speckit.specify`:

```text
Create a new draft for a specification?
```

If accepted, the draft command runs first so you can clarify the feature input before generating the formal specification.

## Command behavior

The draft command follows these rules:

* It considers the provided user input before doing anything else.
* If no input is provided, it asks for a short feature description.
* It asks clarification questions only when the answer would materially change product scope, user experience, security, privacy, data ownership, acceptance scenarios, or downstream planning.
* It avoids implementation details unless they are part of the product contract.
* It does not create, modify, or delete project files.
* It does not create a Spec Kit feature directory.
* It does not write `spec.md`.
* It does not run Spec Kit scripts.

## Good input examples

```text
/speckit.draft.create Let users invite another user to collaborate on a saved project.
```

```text
/speckit.draft.create Add an admin-only audit log for changes to billing settings.
```

```text
/speckit.draft.create Customers should be able to retry a failed payment from their account page.
```

## Tips

For best results, include:

* who the feature is for
* what the user wants to accomplish
* what should happen when the action succeeds
* what should happen when something fails
* important permission, privacy, or visibility constraints
* anything explicitly out of scope

You do not need to describe implementation details such as frameworks, database tables, GraphQL operations, file paths, or component names unless those details are part of the actual product contract.

## Development

Clone the repository:

```bash
git clone https://github.com/reytech-dev/spec-kit-draft.git
cd spec-kit-draft
```

Install it into a test Spec Kit project:

```bash
cd /path/to/spec-kit-project
specify extension add --dev /path/to/spec-kit-draft
```

Check that the command was registered:

```bash
specify extension list
```

For Claude-based integrations, the command should be available as:

```text
/speckit.draft.create
```

Depending on your Spec Kit integration, registered command files may also appear under your agent-specific command directory.

## Uninstall

Remove the extension from a Spec Kit project:

```bash
specify extension remove draft
```

## Versioning

This extension follows semantic versioning.

Commit messages should follow Conventional Commit style:

```text
<type>(<scope>): <subject>
```

Allowed types:

```text
feat, fix, test, refactor, docs, perf, chore
```

Examples:

```text
feat(command): improve draft clarification flow
fix(manifest): correct command alias
docs(readme): document installation steps
chore(release): configure semantic release
```

## License

MIT
