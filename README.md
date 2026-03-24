# Gold Trend Analyser Plugin

This repository now packages the existing skill collection as a reusable plugin source for both GitHub Copilot and Claude Code.

## Included skills

- `gold-trend-analyser`
- `sri-lanka-investment-report`
- `parking-domain-expert`

The `skills\` directory remains the single source of truth for all bundled skills.

## GitHub Copilot / VS Code

This repository includes a Copilot agent plugin manifest at `.github\plugin\plugin.json`.

For local development, register the repository path in VS Code settings:

```json
{
  "chat.pluginLocations": {
    "C:\\path\\to\\gold-trend-analyser": true
  }
}
```

You can also install the repository from source in VS Code with **Chat: Install Plugin From Source** once the repo is pushed to a Git host.

After enabling the plugin, the bundled skills appear in the chat customizations and skills menus.

## Claude Code

This repository includes a Claude plugin manifest at `.claude-plugin\plugin.json`.

For local development, run Claude Code from the repository root with:

```bash
claude --plugin-dir .
```

Then run `/reload-plugins` after changes. The bundled skills are namespaced under the plugin name when invoked manually.

## Notes

- No skill content is duplicated between platforms.
- The Sri Lanka investment skill directory was renamed to `skills\sri-lanka-investment-report` so the folder name matches the skill frontmatter name, which improves standards compatibility.
