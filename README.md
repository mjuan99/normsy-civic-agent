# Normsy Civic Agent

A test marketplace containing a standalone Civic Agent skill. It helps an assistant draft and revise constructive replies to hostile civic or political messages using a bundled Normsy manual.

The skill contains Markdown instructions and references. It does not call a backend or require an MCP server, credentials, dependencies, or additional agents.

## Repository layout

```text
.claude-plugin/marketplace.json          Marketplace catalog
plugins/normsy-civic-agent/
  .claude-plugin/plugin.json             Plugin manifest (version 0.1.0)
  skills/civic-agent/
    SKILL.md                            Skill entry point
    references/                         Response guide, examples, and manual
 docs/
  source-snapshot.json                  Knowledge base provenance
  VALIDATION.md                         Behavioral test scenarios
```

The marketplace and plugin identifiers are `normsy-civic-agent`; the plugin display name is **Normsy Civic Agent**. The skill remains named `civic-agent` and retains provider-independent instructions. The manual includes 41 pages and excludes books and conditional guidance.

## Publish to your GitHub

This is a local repository on the dedicated initial branch `setup/marketplace`. It has no remote and no initial commit yet.

1. On GitHub, create an empty repository named `normsy-civic-agent` under your own account. Do not initialize it with a README, license, or .gitignore, because these local files will be pushed.
2. Choose **Public** for the simplest test installation. This makes the bundled manual and instructions publicly readable. A private repository requires configuring authenticated repository access in the client; do not assume external users can install it.
3. From this directory, run the commands below. Replace `YOUR_GITHUB_USERNAME` with your actual GitHub username.

```bash
cd /home/juan/Documents/git/normsy-civic-agent
git add .
git commit -m "Set up Normsy Civic Agent marketplace"
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/normsy-civic-agent.git
git push -u origin HEAD:main
```

Authenticate using your configured GitHub credentials, a personal access token, or SSH. GitHub account passwords are not accepted for Git pushes. If using SSH, use `git@github.com:YOUR_GITHUB_USERNAME/normsy-civic-agent.git` as the remote URL instead.

The push creates the remote `main` branch while keeping the dedicated local branch unchanged. Confirm that `main` is the default branch on GitHub. Future releases from this local branch can be pushed with `git push origin HEAD:main`.

## Install from Claude web or Desktop

Plugins require a paid Claude plan. Your organization's policies may restrict which repositories you can add.

1. Open **Customize → Plugins**.
2. Choose **Add → Add marketplace → Add from a repository**.
3. Enter `YOUR_GITHUB_USERNAME/normsy-civic-agent` or the full GitHub repository URL.
4. Find **Normsy Civic Agent** in the available plugins and select **Add**.
5. Start a fresh conversation and ask: “Use Civic Agent to help me reply without escalating: 'Anyone who votes for that party is an enemy of the country.' I disagree with treating voters as enemies.”
6. Ask for a shorter revision, then test a fresh conversation without explicitly naming Civic Agent.

If you previously uploaded the standalone Civic Agent skill, disable that copy during testing so you can identify which installation is being used. Follow the scenarios in [docs/VALIDATION.md](docs/VALIDATION.md).

Adding this repository does not publish it in Anthropic's public directory. A self-hosted marketplace does not need a public-directory submission. Organization approval and security scans may still apply.

## Validate and test with Claude Code

If Claude Code is installed, run these checks before publishing:

```bash
claude plugin validate .
claude plugin validate ./plugins/normsy-civic-agent
```

For a local install test:

```bash
claude plugin marketplace add /home/juan/Documents/git/normsy-civic-agent
claude plugin install normsy-civic-agent@normsy-civic-agent
```

For a hosted install test:

```bash
claude plugin marketplace add YOUR_GITHUB_USERNAME/normsy-civic-agent
claude plugin install normsy-civic-agent@normsy-civic-agent
```

Inside a Claude Code session, invoke the skill with `/normsy-civic-agent:civic-agent`, followed by your request. Local tests do not prove that a remote repository can be accessed; test the hosted installation after the push as well.

## Maintain the package

The initial skill was copied from `../chp-file-agenet-prototype-dv/civic-agent-skill/civic-agent/`. The sibling `civic-agent-knowledge-base` repository remains the knowledge source of truth; provenance and manual adaptations are recorded in [docs/source-snapshot.json](docs/source-snapshot.json).

For updates, refresh the standalone skill first, review its changes, then sync the reviewed Markdown into `plugins/normsy-civic-agent/skills/civic-agent/` and update the provenance document. Keep reference paths intact and remove obsolete pages from the distribution when applicable. Increase `version` in the plugin manifest, validate, test, commit, and push the new release. Clients may need a marketplace refresh or plugin update; do not assume an immediate update in every environment.

No open-source license has been selected for this test repository. Choose an appropriate license explicitly before offering licensed reuse of the material.

## Official documentation

- [Create and validate a marketplace](https://code.claude.com/docs/en/plugin-marketplaces)
- [Plugin manifest reference](https://code.claude.com/docs/en/plugins-reference)
- [Install plugins and repository marketplaces in Claude](https://support.claude.com/en/articles/13837440-use-plugins-in-claude)
