# Short Prompts

Ready-to-paste prompts for using this standard with Claude. You don't need to
repeat the rules in the prompt: they are in
[CLAUDE_PROJECT_DOCUMENTATION_INSTRUCTIONS.md](CLAUDE_PROJECT_DOCUMENTATION_INSTRUCTIONS.md),
and Claude reads that file first.

Replace `<…>` placeholders. If Claude is not running inside a clone of this
repository, give the file as a link:
`https://github.com/filippestrikov/confluence_template/blob/main/CLAUDE_PROJECT_DOCUMENTATION_INSTRUCTIONS.md`

**Default behaviour:** Claude works read-only. It audits, drafts and reports,
and publishes to Confluence or Jira only when the prompt says so
(see prompt 3).

---

## 1. Standard audit (most common)

```text
Audit Jira project <KEY> and Confluence space <SPACE> using CLAUDE_PROJECT_DOCUMENTATION_INSTRUCTIONS.md, identify gaps, and populate the project documentation from verified project sources.
```

Result: an audit, the mapping to the standard, drafts of the missing or
updated pages, and a list of what needs human input. Nothing is published.

## 2. Audit with every source named

```text
Audit project <NAME> using CLAUDE_PROJECT_DOCUMENTATION_INSTRUCTIONS.md.
Jira: <KEY> (board <ID>). Confluence: <SPACE or root page URL>. Repo: <URL>. Environments: <URLs, no production testing>.
Identify gaps and draft the documentation from verified sources only.
```

Use this when the project spans several Jira keys or repos, or when the
Confluence tree sits inside a shared space.

## 3. Publish after review

```text
Publish the reviewed drafts for <NAME> to Confluence <SPACE / parent page URL> following CLAUDE_PROJECT_DOCUMENTATION_INSTRUCTIONS.md step 9. Update existing pages in place, create missing CORE pages, archive nothing without listing it first.
```

## 4. New project, nothing documented yet

```text
Set up documentation for new project <NAME> (Jira <KEY>, Confluence <SPACE>) using CLAUDE_PROJECT_DOCUMENTATION_INSTRUCTIONS.md. Create the CORE page skeleton with verified values and TBD markers; skip CONDITIONAL pages without evidence.
```

## 5. Refresh one page

```text
Refresh the <Environments | Jira Workflow | Regression | …> page of <NAME> from current sources using CLAUDE_PROJECT_DOCUMENTATION_INSTRUCTIONS.md. Report what changed and why.
```

## 6. Quarterly review

```text
Run the quarterly documentation review for <NAME> using CLAUDE_PROJECT_DOCUMENTATION_INSTRUCTIONS.md: find pages past their review date, outdated or conflicting values, and broken links. Draft fixes; don't publish.
```

## 7. Feature page from a ticket

```text
Draft the feature page for <KEY-123> using the feature template in PROJECT_DOCUMENTATION_TEMPLATE.md, from the ticket, its comments, linked issues and Figma links only.
```

## 8. Bug report

```text
Write a Jira bug for <short description> on <environment> following BUG_REPORT_STANDARD.md and the <KEY> project's Bug Reporting page.
```

---

## Tips

- **Name the scope.** One Jira project and one Confluence tree per prompt gives
  the cleanest result. For a client with several projects, list them all
  (prompt 2).
- **Say "publish" only when you mean it.** Without it, Claude drafts and reports.
- **Answer the needs-input list,** then rerun prompt 1 or 5. The answers become
  VERIFIED values.
- **Production is off-limits by default.** If read-only production checks are
  allowed for a project, say so explicitly in the prompt.
