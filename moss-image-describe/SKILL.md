---
name: moss-image-describe
description: Use when the user sends an image and wants it described as a paste-ready MOSS-Image prompt. Turns any picture into a faithful detailed English caption, with optional tag or JSON layout forms when they fit better.
---

# MOSS-Image Describe

Turn any image into one faithful, paste-ready MOSS-Image prompt that describes the picture for what it is. MOSS-Image (OpenMOSS) is a text-to-image model that follows long captions closely and is especially strong at rendering visible text and, when needed, spatial layouts.

## When to use
- The user sends an image and asks you to describe it, recreate it, or turn it into a MOSS-Image prompt.
- The user describes a scene in words and wants it written as a MOSS-Image prompt.

## How to respond
- Reply with a single prompt inside one code block, ready to paste. Include a short negative prompt under a `Negative:` line in the same block.
- Describe what is actually in the image. Keep the subjects, clothing, pose, setting, colors, lighting, framing and any visible lettering faithful to the source. Do not invent a different scene unless the user asks for changes.
- Ask a question only if the image cannot be read.
- Adult content follows the host platform's policies. Every person depicted must be an adult.

## Format
The default output is a detailed English caption: one cohesive paragraph (or two if the scene is dense). Write what the finished picture looks like, not an instruction such as "make me a poster."

Cover all of the following that are visible:

1. **Subject and action:** who or what is in the frame, apparent age, and what they are doing
2. **Appearance:** face, hair, skin, build, expression, and every garment with color, material and fit
3. **Setting:** the room or landscape, furniture, props and background details
4. **Camera and framing:** angle, height, shot size, and where each main element sits in the frame
5. **Medium:** photograph, digital painting, anime illustration, watercolor, poster art, and so on, matching the source
6. **Light:** the key source, direction, color temperature, shadows and atmosphere
7. **Materials and palette:** fabrics, surfaces, and the main colors
8. **Mood:** a short, concrete note, not a vague adjective pile

Do not stack quality tags such as `masterpiece` or `8k` onto a caption. Specific light, lens, material and color details do that job better.

### Visible text
Quote the exact words in double quotes, with their capitals, punctuation and line breaks preserved. Say where the text sits and how it looks, and keep the quoted words separate from your description of them. Example: a chalkboard sign by the door that reads "FRESH COFFEE $3" in white hand-lettered capitals. If a line break matters, put a real line break or `\n` inside the quoted text. English is the recommended prompt language. Text that should appear in another language stays in that language inside the quotes.

### Tag sequences (optional)
If the user asks for tags, or the source is clearly an anime tag-style image, you may output comma-separated tags instead of (or after) a caption. Use this order: Quality, Score, Meta, Year, Character, Series, Artist, General. Example: `best quality, highres, hatsune miku, vocaloid, @artist name, 1girl, blue hair`.

### Layout JSON (optional)
Use a layout prompt only when placement must be exact: a poster, a menu, several panels, or objects that have to sit in set places. A detailed caption is enough for ordinary scenes. A model-facing layout is a single JSON object with:

- `summary.caption`: the overall scene and style
- `items`: each text block or object, with `label` (`text` or `object`), `caption`, optional `text` for lettering, and `bbox`
- `bbox_format`: `yxyx` (`[y_min, x_min, y_max, x_max]`)
- `bbox_coord_space`: `abs_centralized` (canvas center is the origin; x increases right, y increases down)

If you do not know the exact pixel size, stay with a caption and describe positions in words.

## Negative prompt
Recommended default:

```
worst quality, bad anatomy, watermark, jpeg artifact
```

The official Base tests often also include `nsfw` in the negative when the image should stay safe. Add it only when that matches the request. The main prompt should describe only what belongs in the picture.

## Tips
- Longer, more complete captions work better than one-line prompts. Whatever you leave out, the model will invent.
- Be specific and visual. Name colors, materials and positions.
- Give each person a full appearance so the model keeps them distinct.
- Keep the prompt in English unless the user asks otherwise.
- If a host has a prompt enhancer, a carefully written caption is usually better left unenhanced.

## Example

Prompt for a photo of a girl reading by a window:

```
A photorealistic photograph of a young adult girl sitting curled on a cushioned window seat in a cozy reading nook. She has an oval face, soft hazel eyes with long lashes, straight brows, light freckles across her nose and a calm closed-lip smile, with shoulder length wavy chestnut hair tucked behind one ear and small gold hoop earrings. She has a slim build and a relaxed posture, and she wears an oversized cream knit sweater with the sleeves pushed to her elbows, charcoal leggings and thick gray wool socks. She holds a hardcover book open against her drawn-up knees, one hand on the page and the other resting on a mug of tea. A tall rain streaked window stands behind her, with sage green cushions, a knitted throw, a stack of books on the sill and a trailing pothos plant. Soft cool daylight from the window falls across her face and the pages, and a warm lamp at the left adds a gentle rim along her hair. Eye level three-quarter view from inside the room, medium shot, 50mm lens, vertical frame, her face and the book sharp and the window softly blurred.

Negative: worst quality, bad anatomy, watermark, jpeg artifact
```
