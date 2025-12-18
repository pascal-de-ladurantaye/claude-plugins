---
name: NBP Prompting Guide
description: This skill should never be used
version: 0.2.0
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

**Anti-pattern:** "fantasy armor"
**Correct approach:** "ornate elven plate armor, etched with silver leaf patterns, with a high collar and pauldrons shaped like falcon wings"

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

When referencing multiple images, always use numbered references (Image 1, Image 2, etc.) corresponding to the order they were provided.

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

## Advanced Techniques

### Step-by-Step Scene Construction

For complex scenes with many elements, break prompts into sequential steps. This gives NBP clear layering and composition guidance.

**Example:** "First, create a background of a serene, misty forest at dawn. Then, in the foreground, add a moss-covered ancient stone altar. Finally, place a single, glowing sword on top of the altar."

**When to use:** Scenes with 3+ distinct elements, complex spatial relationships, or layered compositions.

### Semantic Negative Prompts

Never use negative phrasing ("no cars", "without people"). Instead, describe the desired state positively.

**Anti-pattern:** "a street with no cars"
**Correct approach:** "an empty, deserted street with no signs of traffic"

**Anti-pattern:** "a forest without any buildings"
**Correct approach:** "a pristine, untouched wilderness forest"

NBP responds better to positive descriptions of what IS present rather than what is absent.

### Camera and Composition Control

Use photographic and cinematic terminology to control framing, angle, and depth.

**Framing terms:**
- Wide-angle shot, establishing shot - show full environment
- Medium shot - subject from waist up
- Close-up, extreme close-up - face or detail focus
- Macro shot - extreme detail of small objects

**Angle terms:**
- Low-angle perspective - looking up at subject, conveys power
- High-angle shot - looking down, conveys vulnerability
- Dutch angle - tilted frame, conveys unease
- Eye-level - neutral, relatable

**Depth terms:**
- Shallow depth of field - blurred background, subject focus
- Deep focus - everything sharp
- Bokeh - aesthetic blur quality

**Example:** "A low-angle shot of a samurai warrior, shallow depth of field with bokeh city lights in the background"

## Output Format

Output the prompt directly, followed by edit suggestions. No other commentary.

```
[The complete, verbose prompt following all golden rules]

**Edit suggestions:** [2-3 specific modifications for iteration]
```

**Critical:** The prompt itself must be verbose and detailed. Pack in specificity - materials, textures, lighting, camera angles, composition. A good prompt is typically 2-4 sentences minimum. Never output a terse prompt.

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
| Negative phrasing | "no X" confuses the model | Describe desired state positively |
| Flat composition | No camera/angle direction | Use photographic terminology |
| Monolithic prompts | Complex scenes in one sentence | Break into step-by-step layers |

## Additional Resources

### Reference Files

For detailed guidance on all capability areas:
- **`references/capability-areas.md`** - Complete documentation of all 9 capability areas with examples

### Example Files

Working prompt examples:
- **`examples/infographic-prompts.md`** - Infographic prompt examples
- **`examples/general-prompts.md`** - Various capability area examples
