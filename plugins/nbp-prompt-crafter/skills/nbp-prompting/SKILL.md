---
name: NBP Prompting Guide
description: This skill should be used when the user asks to "craft an image prompt", "create a prompt for Gemini", "generate an image prompt", "write a prompt for Nano-Banana Pro", "help with image generation prompting", "improve my image prompt", or needs guidance on Nano-Banana Pro (Google Gemini) image generation best practices, infographics creation, or structured prompt crafting.
version: 0.1.0
---

# Nano-Banana Pro Prompting Guide

Nano-Banana Pro (NBP) is Google's Gemini image generation model. It uses reasoning to understand intent rather than keyword matching. This skill provides the knowledge base for crafting optimized NBP prompts.

## The Four Golden Rules

### 1. Edit Over Regeneration

When an image achieves ~80% accuracy, request specific modifications rather than regenerating from scratch.

**Anti-pattern:** Regenerating entirely when minor fixes needed
**Correct approach:** "Adjust the lighting to sunset and render the text in neon blue"

### 2. Natural Language Communication

Treat NBP like briefing a human creative professional. Use complete sentences and descriptive language.

**Anti-pattern:** `Cool car, neon, city, night, 8k`
**Correct approach:** `A cinematic wide shot of a futuristic sports car speeding through a rainy Tokyo street at night`

### 3. Specificity and Description

Replace vague references with concrete details. Include textures, materials, and precise descriptors.

**Anti-pattern:** "a woman"
**Correct approach:** "a sophisticated elderly woman in a vintage Chanel-style suit"

Include material descriptors: "matte finish", "brushed steel", "weathered leather", "frosted glass"

### 4. Contextual Framing

State the purpose, audience, or use case. This informs styling decisions.

**Example:** "for a Brazilian high-end gourmet cookbook" tells NBP to use professional plating, warm lighting, and appetizing presentation.

## Capability Areas

NBP excels in 9 distinct capability areas. Identify which area applies to craft optimal prompts.

### 1. Text Rendering & Infographics (Primary Focus)

NBP excels at converting information into visual formats with legible text.

**Key techniques:**
- Use quotation marks for exact text placement: `with the title "Annual Report 2024"`
- Specify aesthetic style: polished editorial, technical diagram, hand-drawn, retro
- Define text hierarchy: headline, subheading, body, captions

**Example prompts:**
- "Generate a clean, modern infographic summarizing key financial highlights"
- "Make a retro, 1950s-style infographic about the history of the American diner"
- "Create an orthographic blueprint describing this building in plan, elevation, and section"
- "Summarize 'Transformer Neural Network Architecture' as a hand-drawn whiteboard diagram"

**Applications:** Financial documents, historical infographics, architectural blueprints, educational diagrams, data visualizations

### 2. Character Consistency

Maintain facial identity across scenarios using reference images.

**Key instruction:** "Keep the person's facial features exactly the same as Image 1"

Supports up to 14 reference images (6 with enhanced fidelity). Explicitly state identity preservation while describing emotional or postural changes.

### 3-9. Additional Capabilities

For detailed guidance on remaining capability areas, consult `references/capability-areas.md`:
- Real-Time Data Integration
- Advanced Manipulation
- Dimensional Translation (2D↔3D)
- High-Resolution Output (1K-4K)
- Reasoning Mode ("Thinking")
- Sequential Narrative
- Structural Layout Control

## Structured Output Format

When crafting prompts, produce output in this structured format:

```
## Prompt
[The complete, crafted prompt following all golden rules]

## Metadata
- **Aspect Ratio**: [16:9 | 1:1 | 4:3 | 9:16 | 3:2 | 2:3]
- **Resolution**: [1K | 2K | 4K]
- **Capability Area**: [Which of the 9 areas this prompt targets]
- **Edit Refinements**: [2-3 suggested modifications for iteration]
```

## Aspect Ratio Selection

| Ratio | Use Case |
|-------|----------|
| 16:9 | Cinematic, presentations, thumbnails, landscapes |
| 1:1 | Social media, profile images, icons |
| 4:3 | Traditional photo, documents, infographics |
| 9:16 | Mobile, stories, vertical video |
| 3:2 | Standard photography |
| 2:3 | Portrait photography, posters |

## Resolution Selection

| Resolution | Use Case |
|------------|----------|
| 1K | Quick drafts, concepts, social media |
| 2K | Standard output, web use |
| 4K | Print, large format, detailed texture work |

## Prompt Crafting Workflow

1. **Identify capability area** from user's request
2. **Ask 1-2 clarifying questions** if purpose/style unclear
3. **Apply golden rules** to transform rough idea into detailed prompt
4. **Select metadata** (aspect ratio, resolution) based on use case
5. **Suggest edit refinements** for iteration

## Clarifying Questions by Capability Area

### For Infographics/Text
- What data or information should be visualized?
- What aesthetic style? (corporate, retro, hand-drawn, minimalist)

### For Character Work
- Do you have reference images to maintain consistency?
- What emotion or pose variation is needed?

### For General Images
- What is the intended use? (social media, print, presentation)
- Any specific style references? (cinematic, editorial, illustration)

## Common Anti-Patterns

| Anti-Pattern | Problem | Fix |
|--------------|---------|-----|
| Keyword soup | NBP uses reasoning, not keyword matching | Write natural sentences |
| Vague subjects | "a person" lacks detail | Specify age, clothing, demeanor |
| Missing context | No audience/purpose info | State intended use |
| Over-regeneration | Wastes time on 80% good images | Request specific edits |
| Generic textures | "shiny" is vague | "brushed aluminum with fingerprint smudges" |

## Additional Resources

### Reference Files

For detailed guidance on all capability areas:
- **`references/capability-areas.md`** - Complete documentation of all 9 capability areas with examples

### Example Files

Working prompt examples:
- **`examples/infographic-prompts.md`** - Infographic prompt examples
- **`examples/general-prompts.md`** - Various capability area examples
