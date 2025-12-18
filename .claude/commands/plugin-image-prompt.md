---
description: Generate an Atomic Age style image prompt for a plugin's heading image
argument-hint: Path to the plugin folder (e.g., plugins/nbp-prompt-crafter)
---

Use the `nbp-prompt-crafter:prompt-crafter` agent to craft an image prompt for the plugin at `$ARGUMENTS`. Tell the agent to:
1. Explore the plugin folder (README, plugin.json, agents, skills) to fully understand what it does
2. Read and apply all requirements from `prompts/style-guide.md`
3. Create a visual metaphor capturing the plugin's core function
4. Use 16:9 aspect ratio

Once the agent has finished and output the prompt, copy it to clipboard.
