# NBP Capability Areas - Complete Reference

Detailed documentation for all 9 Nano-Banana Pro capability areas.

## 1. Text Rendering & Infographics

NBP excels at converting dense information into visual formats with legible text rendering.

### Techniques

**Text Placement:** Use quotation marks for exact text
- `with the headline "Breaking News"`
- `labeled sections reading "Input", "Process", "Output"`

**Style Specification:**
- Polished editorial (clean, professional)
- Technical diagram (precise, labeled)
- Hand-drawn/whiteboard (informal, sketchy)
- Retro period styles (1950s diner, Art Deco, etc.)

**Hierarchy Definition:**
- Primary headline
- Secondary subheadings
- Body text
- Captions and labels
- Data callouts

### Applications

| Application | Prompt Approach |
|-------------|-----------------|
| Financial documents | "Clean, modern infographic with embedded charts showing [data]" |
| Historical infographics | "Period-appropriate styling, [era]-style typography" |
| Architectural blueprints | "Orthographic views: plan, elevation, section with labeled dimensions" |
| Educational diagrams | "Color-coded components, clear labels, visual flow" |
| Data visualizations | "Chart type + data representation + visual style" |

### Example Prompts

```
Generate a clean, modern infographic summarizing the key financial highlights of a tech startup's Series A round, with sections for funding amount, valuation, investor breakdown, and use of funds. Use a dark blue and gold color scheme with sans-serif typography.
```

```
Create a retro 1950s-style illustrated infographic about the history of the American diner, including timeline, iconic menu items, and architectural features. Use pastel colors, hand-lettered typography, and vintage illustration style.
```

```
Design a hand-drawn whiteboard diagram explaining the Transformer neural network architecture, showing attention mechanisms, encoder-decoder structure, and data flow. Use marker-style lines with red, blue, and black colors.
```

## 2. Character Consistency & Visual Storytelling

Maintain facial identity across multiple generations using reference images.

### Reference Image Guidelines

- Supports up to 14 reference images
- 6 images provide enhanced fidelity
- Clear, well-lit face shots work best
- Multiple angles improve consistency

### Key Instructions

**Identity Preservation:**
```
Keep the person's facial features exactly the same as Image 1
```

**Variation Requests:**
```
Same person as reference, but now [emotional state/pose/setting]
```

### Applications

| Use Case | Approach |
|----------|----------|
| Video thumbnails | Combine person + graphic elements + typography |
| Sequential narratives | Maintain identity across scenes |
| Product photography | Preserve brand visual identity |
| Marketing campaigns | Consistent spokesperson across assets |

## 3. Real-Time Data Integration

NBP integrates with Google Search to visualize current information.

### Capabilities

- Stock valuations and market data
- Travel trends and statistics
- Event data and schedules
- Current news visualization
- Weather and environmental data

### How It Works

1. NBP reasons through search results
2. Extracts relevant data points
3. Incorporates into visual generation
4. Reduces factual inaccuracies

### Example Prompt

```
Create an infographic showing today's top 5 trending tech stocks with their current prices and daily change percentages, styled as a modern financial dashboard.
```

## 4. Advanced Image Manipulation

Conversational editing without manual masking.

### Capabilities

| Operation | Example Prompt |
|-----------|----------------|
| Object removal | "Remove the tourists from this landmark photo" |
| Background reconstruction | "Replace the background with a sunset beach" |
| Style transfer | "Convert this photo to watercolor painting style" |
| Colorization | "Colorize this manga panel with vibrant anime palette" |
| Seasonal transformation | "Transform this summer scene to winter" |
| Geographic localization | "Adapt this street scene to look like Tokyo" |

### Manga/Anime Colorization

```
Colorize this manga panel with a vibrant anime-style palette, maintaining the original line art while adding cel-shaded colors appropriate for the scene's mood.
```

### Cultural Adaptation

```
Adapt this American suburban street scene to look like a residential area in [location], with appropriate architecture, signage, and cultural elements.
```

## 5. Dimensional Translation

Convert between 2D and 3D representations.

### 2D to 3D

| Input | Output |
|-------|--------|
| Floor plan | Multi-view 3D rendering |
| Technical drawing | Isometric visualization |
| Sketch | Rendered 3D model |
| Meme/illustration | Photorealistic 3D scene |

### 3D to 2D

| Input | Output |
|-------|--------|
| 3D render | Technical blueprint |
| Product photo | Exploded diagram |
| Architecture photo | Floor plan extraction |

### Example Prompts

```
Convert this floor plan into a photorealistic 3D interior rendering, showing the living room from a corner perspective with modern furniture and natural lighting.
```

```
Transform this internet meme into a photorealistic 3D rendered scene, maintaining the humor while adding realistic lighting, textures, and depth.
```

## 6. High-Resolution Output (1K-4K)

Native support for detailed, large-format generation.

### Resolution Guidelines

| Resolution | Best For | Prompt Emphasis |
|------------|----------|-----------------|
| 1K | Concepts, drafts, social | Speed over detail |
| 2K | Web, standard use | Balanced detail |
| 4K | Print, large format | "High-fidelity", "micro-textures", "pixel-perfect" |

### 4K Prompt Techniques

Include texture-specific language:
- "Visible fabric weave"
- "Individual hair strands"
- "Surface imperfections and micro-scratches"
- "Fine grain detail"
- "Pore-level skin texture"

### Example Prompt

```
A 4K hyperdetailed macro photograph of a vintage mechanical watch face, showing individual gear teeth, dust particles, micro-scratches on the crystal, and the texture of aged brass components. Pixel-perfect rendering suitable for large-format printing.
```

## 7. Reasoning Mode ("Thinking")

NBP generates interim thought images to refine composition.

### How It Works

1. Model receives complex prompt
2. Generates internal "thinking" images (not charged)
3. Refines understanding of composition
4. Produces final output

### Best Applications

- Visual mathematics problems
- Scene reconstruction from description
- Complex multi-element compositions
- Logical/spatial puzzles

### Example

```
A visual math problem: Show a balance scale where the left side has 3 red spheres and 2 blue cubes, and the right side needs to be filled with green cylinders to balance. Each sphere weighs 2 units, each cube weighs 3 units, and each cylinder weighs 4 units.
```

## 8. Sequential Narrative Generation

Create cohesive multi-image stories in single sessions.

### Techniques

**Consistency Instructions:**
```
Create a 4-panel comic sequence. Maintain the same character design throughout: [character description]. Vary angles, expressions, and distances across frames.
```

**Panel Specifications:**
- Panel count and layout
- Character consistency requirements
- Angle/distance variations per panel
- Emotional arc across sequence

### Example Prompt

```
Create a 6-panel storyboard for a short animated sequence. Main character: young woman with short blue hair, yellow raincoat. Panel 1: Wide shot, character walks toward camera in rain. Panel 2: Medium shot, she notices something. Panel 3: Close-up on her surprised face. Panel 4: Her POV of a small robot in a puddle. Panel 5: She kneels down to pick it up. Panel 6: Walking away together, robot on her shoulder.
```

## 9. Structural Layout Control

Use input images as composition templates.

### Template Types

| Template | Use Case |
|----------|----------|
| Hand sketch | Convert napkin drawing to polished ad |
| Wireframe | UI mockup generation |
| Grid structure | Pixel art, sprite sheets |
| Composition guide | Enforce specific layouts |

### Applications

**Napkin to Ad:**
```
Convert this rough sketch into a polished advertisement for [product], maintaining the exact composition and element placement while adding professional rendering, lighting, and typography.
```

**Wireframe to UI:**
```
Generate a high-fidelity UI mockup from this wireframe. Maintain exact element positions. Apply [style: Material Design/iOS/custom] with [color scheme].
```

**Sprite Sheet Generation:**
```
Create a 4x4 sprite sheet for a pixel art character walking cycle. Grid size: 32x32 pixels per frame. Character: [description]. Show 4 directions (down, left, right, up) with 4 frames each.
```

**Pixel Art from Grid:**
```
Using this grid template, create pixel art of [subject] fitting exactly within the defined boundaries. Maintain pixel-perfect alignment with the grid structure.
```
