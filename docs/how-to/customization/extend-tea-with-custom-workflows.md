---
title: 'Extend TEA with Custom Workflows'
description: Add your own workflows to bmad-tea without patching TEA core
---

# Extend TEA with Custom Workflows

TEA is a standalone module now. That means custom workflows are still supported, but they are not automatically folded into TEA core during updates.

## The Supported Model

Use one of these approaches:

1. Package the workflow as custom content or a custom module.
2. Add a menu entry to `bmad-tea` through BMAD agent customization.
3. Reinstall or quick-update BMAD so the workflow and menu entry are registered.

This keeps your TEA extensions compatible with upstream updates.

## Recommended Approach

### 1. Create the workflow as custom content

Use BMad Builder or your own custom module structure to create a workflow that lives outside TEA core.

- BMAD supports custom modules during install/update.
- BMad Builder is the recommended path for creating reusable custom agents and workflows.

See:

- [How to Customize BMad](https://github.com/bmad-code-org/BMAD-METHOD/blob/main/docs/how-to/customize-bmad.md)
- [BMad Builder (BMB)](https://github.com/bmad-code-org/bmad-builder)

### 2. Attach the workflow to `bmad-tea`

After TEA is installed, use the generated agent customization file for `bmad-tea` under `_bmad/_config/agents/` and append a menu item:

```yaml
menu:
  - trigger: my-custom-workflow
    workflow: 'my-custom/workflows/my-custom-workflow.yaml'
    description: My custom TEA extension workflow
```

This keeps the `bmad-tea` chat/menu experience intact while routing to your custom workflow.

### 3. Reinstall or quick-update BMAD

Run:

```bash
npx bmad-method install
```

Then choose a normal update path so BMAD re-applies the customization and refreshes the workflow registration.

## What Not to Do

- Do not patch TEA core files directly if the workflow is project-specific.
- Do not rely on old embedded-TEA behavior where local workflows appeared to be attached automatically.
- Do not keep custom workflow logic only in chat instructions. Put it in a real workflow or module so it survives updates.

## When to Use Which Approach

- **Project-specific workflow**: add custom content and attach it to `bmad-tea`
- **Reusable internal workflow**: package it as a custom module
- **Reusable public workflow**: consider publishing a standalone BMAD module

## Related Docs

- [TEA Command Reference](/docs/reference/commands.md)
- [TEA Configuration Reference](/docs/reference/configuration.md)
- [How to Customize BMad](https://github.com/bmad-code-org/BMAD-METHOD/blob/main/docs/how-to/customize-bmad.md)
