![image](assets/heading.png)

# NBP Prompt Crafter

Crafts optimized image generation prompts for Nano-Banana Pro (Google Gemini) following official prompting best practices.

## Features

- Transforms rough ideas into structured, detailed prompts
- Applies the 4 Golden Rules of NBP prompting
- Covers all 9 capability areas with emphasis on infographics
- Outputs structured format with metadata (aspect ratio, resolution, edit refinements)

## Components

- **Skill**: `nbp-prompting` - Knowledge base of prompting patterns and best practices (auto loaded in the agent)
- **Agent**: `prompt-crafter` - Analyzes ideas, asks clarifying questions, generates structured prompts

Only the subagent is meant to be used through this plugin, it will auto-load the Skill to better manage context of the main agent.

## Usage

Ask conversationally to craft an image prompt and the agent will trigger:

- "I need an image of a futuristic city for my presentation"
- "Help me write a prompt for an infographic about company metrics"
- "Create a prompt for a cool car at night, cinematic style"

## Capability Areas

1. Text Rendering & Infographics (emphasized)
2. Character Consistency
3. Real-Time Data Integration
4. Advanced Manipulation
5. Dimensional Translation (2D↔3D)
6. High-Resolution Output
7. Reasoning Mode
8. Sequential Narrative
9. Structural Layout Control

## Output Format

```
## Prompt
[The crafted prompt]

## Metadata
- **Aspect Ratio**: [ratio]
- **Resolution**: [1K/2K/4K]
- **Capability Area**: [detected area]
- **Edit Refinements**: [suggestions for iteration]
```
