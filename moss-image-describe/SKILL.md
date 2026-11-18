---
name: moss-image-describe
description: Use when the user sends an image and wants it described as a paste-ready MOSS-Image prompt. Turns any picture into a faithful detailed caption, or a Layout draft when exact placement matters.
---

# MOSS-Image Describe

Turn any image (or a short scene description) into one faithful, paste-ready MOSS-Image prompt that describes the picture for what it is. MOSS-Image (OpenMOSS) follows long captions closely and is especially strong at rendering visible text and, when needed, spatial layouts.

This skill is an image-to-prompt adaptation of the official [MOSS-Image Prompt Enhancer](https://github.com/OpenMOSS/MOSS-Image/blob/main/skills/moss-image-prompt-enhancer/SKILL.md). The official skill expands a generation idea into a caption or Layout. This skill does the same job from a provided image: describe what is already there, then return a prompt you can paste into MOSS-Image's positive prompt.

## When to use
- The user sends an image and asks you to describe it, recreate it, or turn it into a MOSS-Image prompt.
- The user describes a scene in words and wants it written as a MOSS-Image prompt.

## How to respond
- Reply with a single ready-to-paste prompt inside one code block. Include a short negative prompt under a `Negative:` line in the same block.
- Honor an explicit request for a caption or a Layout. Otherwise use a caption for ordinary scenes, photographs and illustrations. Use Layout when specific text placement, a poster, several panels, or controlled object relationships would benefit from bounding boxes. A detailed image does not automatically need Layout.
- Describe what is actually in the image. Keep the subjects, counts, relationships, clothing, pose, setting, medium, style, framing and any visible wording faithful to the source. Do not invent a different scene, unrequested style changes, or copy that is not in the image, unless the user asks for changes.
- Ask a question only if the image cannot be read, or if a missing decision would materially change the result.
- Adult content follows the host platform's policies. Every person depicted must be an adult.

## Describe the image
Write visible choices, not process notes. Cover all of the following that you can see:

- Subject and action
- Relevant appearance
- Setting
- Camera and framing, including where things sit in the frame
- Medium (photograph, digital painting, anime illustration, poster art, and so on)
- Lighting
- Materials and palette
- Mood, stated concretely

Add detail that makes the picture more specific. Do not add redundant quality tags such as `masterpiece` or `8k`. Do not put explanations of JSON, bounding boxes or conversion steps into the image description. Those are tool notes, not depicted content.

Default to English for descriptive prose, and follow a requested output language when the user gives one. Preserve visible text verbatim in its original language, including punctuation, capitalization and line breaks. A quoted sentence in a user's instruction is not necessarily text that appears in the image: distinguish visible wording from reference material and constraints.

## Caption (default)
The paste-ready prompt is cohesive prose. Spatial relations belong in words. Quote any visible wording exactly, and say where it sits and how it looks. The caption may use more than one paragraph if the scene is dense. Do not add coordinates or JSON-layout fields to a caption just to make it look structured.

Write what the finished picture looks like, not an instruction such as "make me a poster." Write the real words that appear in the image, never a placeholder such as "headline here." If a line break in the lettering matters, put a real line break or `\n` inside the quoted text.

## Layout
Use Layout only when placement must be exact. If you do not know the pixel size, or the boxes would be a guess, stay with a caption and describe positions in words.

When Layout is the right deliverable, write an editable draft first, then compile it into the model-facing prompt. Do not convert boxes to centered coordinates by hand.

### Draft format
Follow the official Pixel Layout vocabulary from [references/layout.md](https://github.com/OpenMOSS/MOSS-Image/blob/main/skills/moss-image-prompt-enhancer/references/layout.md):

- `width` and `height`: positive integer multiples of 16, equal to the intended image size. Honor dimensions supplied with the image or by the user. With only an aspect ratio, choose compatible pixels. Without either, use 1024x1024 unless the medium clearly suggests another shape. Do not silently change explicit dimensions that are not multiples of 16; say so instead. These fields belong in the draft only, not in the compiled prompt.
- `bbox_coord_space`: exactly `"abs"`.
- `bbox_format`: exactly `"xyxy"`.
- Draft boxes are `[x_min, y_min, x_max, y_max]` in actual pixels, from the canvas top-left. Keep x in `0..width` and y in `0..height`. Do not use normalized coordinates, and do not center, reorder or quantize the boxes yourself.
- `summary`: a nonempty global `caption`, plus optional `meta` (medium or genre tags) and `canvas` (`single`, `multi_panel`, or `collage`).
- `items`: a nonempty flat array. Each item has a `label` (`object`, `character`, or `text`), a nonempty `caption`, and a four-number `bbox`. A `text` item also needs `text`: the exact visible characters, with intended line breaks as JSON `\n`.
- Optional `tags` and `palette` arrays may appear on items, and `palette` may appear on `summary`, only when they add useful visual information.

Use boxes for coherent visible units, and split them only when independent placement matters. Natural occlusion and overlap are allowed. A box is a placement annotation, not an instruction to draw a border or sticker. Describe appearance in item captions and global treatment in `summary.caption`. Keep exact visible strings in the `text` fields.

For designed images such as posters, compose the information and imagery together: reading order, relative prominence, coherent groups and readable text at the chosen size.

### Compile the draft
The prompt you paste into MOSS-Image is not the draft. Compile it with the official tool from the MOSS-Image repository:

```bash
python3 /path/to/moss-image-prompt-enhancer/scripts/compile_prompt.py \
  draft.json --output prompt.txt
```

The compiled output is one physical line of JSON, with flat `items`, integer `abs_centralized` / `yxyx` boxes, and no canvas width or height. If you show Layout JSON inline, show that compiled line without reformatting it, and state the required width x height outside the prompt. Fix validation errors in the draft and recompile; do not bypass a failed conversion by writing centered JSON yourself.

If the official compiler is not available, deliver the editable draft and the compile command, or fall back to a caption with positions in words.

## Negative prompt
Only the caption or the compiled Layout belongs in MOSS-Image's positive prompt. A short official-style negative, kept on its own line, is:

```
worst quality, bad anatomy, watermark, jpeg artifact
```

The official Base tests sometimes also include `nsfw` when the image should stay safe. Add it only when that matches the request. The main prompt should describe only what belongs in the picture.

## Tips
- A complete caption is better than a one-line prompt. Whatever you leave out, the model will invent.
- Be specific and visual. Name colors, materials and positions.
- Give each person a full appearance so the model keeps them distinct.
- Keep the description in English unless the user asks otherwise.
- If a host has a prompt enhancer, a carefully written caption is usually better left unenhanced.

## Example

Caption for a photo of a girl reading by a window:

```
A photorealistic photograph of a young adult girl sitting curled on a cushioned window seat in a cozy reading nook. She has an oval face, soft hazel eyes with long lashes, straight brows, light freckles across her nose and a calm closed lip smile, with shoulder length wavy chestnut hair tucked behind one ear and small gold hoop earrings. She has a slim build and a relaxed posture, and she wears an oversized cream knit sweater with the sleeves pushed to her elbows, charcoal leggings and thick gray wool socks. She holds a hardcover book open against her drawn-up knees, one hand on the page and the other resting on a mug of tea. A tall rain streaked window stands behind her, with sage green cushions, a knitted throw, a stack of books on the sill and a trailing pothos plant. Soft cool daylight from the window falls across her face and the pages, and a warm lamp at the left adds a gentle rim along her hair. Eye level three quarter view from inside the room, medium shot, 50mm lens, vertical frame, her face and the book sharp and the window softly blurred.

Negative: worst quality, bad anatomy, watermark, jpeg artifact
```

## Source
Adapted from the official [MOSS-Image Prompt Enhancer](https://github.com/OpenMOSS/MOSS-Image/blob/main/skills/moss-image-prompt-enhancer/SKILL.md) in [OpenMOSS/MOSS-Image](https://github.com/OpenMOSS/MOSS-Image), which is licensed under the [Apache License 2.0](https://github.com/OpenMOSS/MOSS-Image/blob/main/LICENSE). This file is an original image-to-prompt adaptation, not a verbatim copy of the official skill. Layout drafts follow the official Pixel Layout vocabulary; compile them with the official `scripts/compile_prompt.py`.
